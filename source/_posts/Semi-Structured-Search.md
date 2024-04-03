
---
title: Semi-Structured Search
date: 2023-08-17 20:00:42
tags: Search Infra
description: "DHT-REMOTE"
---

# Semi-Structured Search


## Why We Need Semi-Structured Search
"To organize the world's information and make it universally accessible and useful."

## Key Features
- **Providing High-Quality Content**: Deduplication, delivery of high-quality third-party information, filtering, and ranking.
- **Rich Interactivity**: Includes features like SaveItems, Reading List, Carousels/grid pack, tag/filter.
- **Multi-Dimensional Manner of Information Retrieval**: Provides multiple ways to retrieve information based on the characteristics of the verticals, such as:
    - **Events**: Sorting based on Location/Time/Performer. For example, "events near me," "Events in the next month," "Lady Gaga's events."
    - **Recipe**: Sorting based on Dish/Meal_time/cuisine/ingredient. For example, "how to cook Chinese pork belly."
- **Rich Information Content**: Features a wide range of information such as pictures, videos, clustering, ratings, addresses, previews, books, ticket purchase links, etc.
- **High Scalability**: Can be triggered by different primary query intents as derived_intent, aiming to satisfy users' potential needs, even the ones they have as yet not realized.

# Why We Need to apply this in our search infrastructure

## Primary Features

- **Establish Unified Standards and Frameworks**: Includes MRFT for intents, Scubed Engine for resolution, Recomidia for clustering, and Pringles for tags/chips.
- **Increase Code Reuse Rate**: Modules such as cache, item preview, retrieval, ranking, deduplication, packmsg, saveItems, personalization, tag/chips can be reused. Other features include the online survey template and live experiment logger.
- **Configuration-Driven Development**: Features like intent to fulfillment mappings, response strategy config, bidder config, etcetera are configuration-driven.

## Terminology

### Knowledge Graph (KG)
Knowledge Graph is a large database that stores vast amounts of entities and relationships between these entities. The basic unit is `Triple`, which contains 3 parts: `Subject`, `Predicate`, `Object`. This content is only supported in a Feishu Docs.

### Intent
`Query Intents` (QI) and `Derived Intents` (DI) are generated in the query understanding service (QUS). Sub-derived intents are only used in the this semi-structure search framework. They're generated based on QI or DI in the pre-resolution stage.

# How this Semi-Structured Search Works

This content is only supported in a Feishu Docs

## Query Understanding - QUS

1. With support from Knowledge Graph (KG) and NLP (Natural Language Processing), Query Understanding Service (QUS) can automatically extract patterns from given examples. This mechanism simplifies generating query to Query Intent (QI) mappings. For instance:
    - INTENT `Find_recipe(ingredient=${ingredient})` may be triggered by queries like "How to cook beef", "The best tomato recipes", "Lamp recipe recommendations", etc. resulting in patterns such as "How to cook ${ingredient}", "The best ${ingredient} recipes", "${ingredient} recipe recommendations".
    - INTENT `Find_recipe(dish=${dish}, cuisine=${cuisine})` can be triggered by queries like "How to cook chinese pork steaks", "chinese pork recipes", etc. resulting in patterns like "How to cook ${cuisine} ${ingredient}",  "${cuisine} ${ingredient} recipes".

2. QUS also provides an intent score for each QI. Web service attempts to fulfill all Query Intents (QIs) exceeding the threshold and the corresponding Derived Intents (DIs). With KG's aid, QUS might pick the winner at the QUS stage. For example, for searches like "Barack Obama's university," initial intents may be `Find_School (owner=/m/barack_obama)` and `Find_School (graduated_student=/m/barack_obama)`. Based on KG's relationship data, the second intent might prevail during the QUS.

3. After multiple Query Intents (QIs) and their Derived Intents (DIs) are fulfilled,  Web Service calculates a fulfillment score based on content quality. The Query Intent with the highest sum of "intent score" and "fulfillment score" is the winner and shown to the users.

## Retrieval - Scubed Engine (Scubed = S^3 = Semi-structured-search)

1. Scubed Engine, akin to Elastic Search, supports Term-Based search, distributed storage and processing, flexible data schema, fuzzy matching, geo-queries, date-range queries, and more.
2. Each vertical category needs to build its corpus, allowing search services to be optimized based on the unique characteristics of each vertical. For example, Books vertical has a long update cycle, so it may need to be fully updated once a week, while Events vertical needs to respond to geo-queries, which means its index should be optimized based on the Geo info.
3. Scubed Engine readily supports indexing from Knowledge Graphs through `PathQuery`, a Knowledge Graph query language. Here is an example of an `EventRecord`:

    ```
    EventRecord =
    [type/object/type == /time/event/].{
        Title: /object/name
        Location: /time/event/location
        Description: /time/event/description
        TicketLink: /time/event/ticket./ticket/url
        ...
    }
    ```
4. Lightweight ranking is done within Scubed Engine. Each record has various ranking signals generated from different sources (AI annotators, third-party platforms, aggregated statistical numbers, etc.). Each vertical can define its own lightweight ranking strategy with Scubed through a script, usually focusing on popularity and topicality scores.
5. Scubed, by default, returns the top 500 records to the evaluator.

## Ranking

Ranking includes item-level ranking (lightweight + heavyweight) and whole-page ranking.

### Item-level Ranking

Lightweight ranking was discussed earlier, while heavyweight ranking takes place in Twiddle. Here a more complex ranking is done considering many factors. As with the lightweight ranking, each vertical has its own strategy.
For `P13N` calls, the heavyweight ranking is taken by the Recommendation ML model. It takes `user_embedding_vector`, `doc_embedding_vector`, use explicitly configured preferences, among other signals as input, generating a more accurate affinity score based on collaborative filtering algorithms.

### Whole-page Ranking

Based on the final results shown to the user (pictures, click buttons, content quality, etc.), Web Service calculates a "fulfillment score" for each QI/DI fulfillment, which decides the rank of this feature on the whole page.

# Evaluation 

## In Development

### Ewok
Ewok serves a function analogous to the Fetch & Review platform. It's an internal platform for raters to conduct blind tests between the base and test versions. RD takes responsibility for triaging both wins and losses, then determines which brackets should be fixed in collaboration with the PM.

### Bug Bash
A meeting involving engineers from the front end, back end, serving, and data sides. The objective is to interact with a demo and try to identify as many bugs as possible.

## Before-Launch

### Live-experiment
There are two types of live experiments: counterfactual and non-counterfactual.

#### Counterfactual Experiment
Counterfactual is defined as "what would have happened otherwise." It intends to eliminate "selection bias" when the distribution of the observed group is not representative of the target group of interest.

Counterfactual example:
- Queries that trigger the feature on the control group would also trigger the feature on the experimental group: 7%
- Queries that trigger the feature on the control group but not on experimental group: 3%
- Queries that didn't trigger on the control group but did so on experimental group: 23%
- Queries that didn't trigger the feature on either the control group or the experimental group: 67%

In a counterfactual experiment, backend logic runs twice for each query; once for the control group and once for the experimental group. The experimental framework logs the conditions from both runs, but users only see one side. Metrics can be sliced based on any combination of conditions. 

Since counterfactual experiments can eliminate "selection bias," they're primarily used for quality-related evaluations. Main metrics include: CTR, Manual Refinement, and Return Rate.

#### Non-Counterfactual Experiment
In a non-counterfactual experiment, backend logic runs only once for each query, either for the control group or the experimental group. Users will only see one side. This type of experiment is used to evaluate latency impacts. 

### Online Survey
Along with the live experiment, there may be an option to direct real users to a quick survey. The features share the same questionnaire template, aiming to understand user intent and satisfaction.

