---
title: DHT-REMOTE
date: 2017-08-17 20:00:42
tags: Distrubute System
cover: /img/default3.png
description: "DHT-REMOTE"
---

# DHT-REMOTE
* Ankai Liang
* 10411998
* CS 549 Assignment4
* [code link](https://github.com/AnkaiLiang/dht-remote)


## Code Explanation
On this assisgnment, we extend the program we did last time with a push-based protocol. So there are a lot code snippets are the same as before. I just list the new sippets I added this time.

### ControllerClient.java
Create a instance of ClientEndpointConfig, using `CommandLineEncoder` as encoder.

```
	// TODO configure the client to use proper encoder for messages sent to server
	private final ClientEndpointConfig cec = ClientEndpointConfig.Builder.create().
			encoders(Arrays.asList(CommandLineEncoder.class)).build();
```
When we need to connect to a remote node.

1. Create a instance of `ClientManager` 
2. Keep looping to wait for the ack from the remote node until got the ack.

```java
	public void connect(URI uri) throws DeploymentException, IOException {
		try {
			shell.msg("Requesting control of node at " + uri.toString() + "...");
			// TODO done make the connection request
			ClientManager clientManager = ClientManager.createClient(ContainerProvider.getWebSocketContainer());
			session = clientManager.connectToServer(this, cec, uri);
			while (true) {
				try {
					// Synchronize with receipt of an ack from the remote node.
					boolean connected = messageLatch.await(100, TimeUnit.SECONDS);
					// TODO done If we are connected, a new toplevel shell has been pushed, execute its CLI.
					// Be sure to return when done, to exit the loop.
					if (connected){
						shellManager.getCurrentShell().cli();
						break;
					}
				} catch (InterruptedException e) {
					// Keep on waiting for the specified time interval
				}
			}
		} catch (IOException e) {
			shell.err(e);
		}
	}
```
If the session has been created, add this controllclient as message handler, and cache the session.

```java
	@Override
	public void onOpen(Session session, EndpointConfig config) {
		// TODO session created, add a message handler for receiving communication from server.
		// We should also cache the session for use by some of the other operations.
		session.addMessageHandler(this);
		this.session = session;
	}
```
If the initializing has not done:

1. if got the ack, means request has been accepted. Create a ProxyShell and add this ProxyShell to the stack of Shell. Set the local running shell is this ProxyShell. Flag the initializing has been done.
2. If the server rejects our request, they will just close the channel.

If the initializing has been done, just running the top Shell on stack and via the message to it. 

```java
	@Override
	public void onMessage(String message) {
		if (initializing) {
			if (SessionManager.ACK.equals(message)) {
				/*
				 * TODO done server has accepted our remote control request, push a proxy shell on the shell stack
				 * and flag that initialization has finished (allowing the UI thread to continue).
				 * Make sure to replace the cached shell in this callback with the new proxy shell!
				 * 
				 * If the server rejects our request, they will just close the channel.
				 */
				try {
					shell.msgln("request accepted.");
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				shell = ProxyShell.createRemoteController(shell, session.getBasicRemote());
				shellManager.addShell(shell);
				endInitialization();
			} else {
				throw new IllegalStateException("Unexpected response to remote control request: " + message);
			}
		} else {
			// TODO done provide the message to the shell
			try {
				shellManager.getCurrentShell().msg(message);
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
```
When shotdown, flag the end of initializing and close the session.

```java
	protected void shutdown() throws IOException {
		/*
		 * TODO Shutdown initiated by error or closure of the connection.  Three cases: 
		 * 1. We are still initializing when this happens (need to unblock the client thread).
		 * 2. We are running an on-going remote control session (need to remove the proxy shell).
		 * 3. The remote control session has terminated (which caused the channel to be closed).
		 */
		if (initializing) 
			endInitialization();
		else if (session.isOpen())
			session.close();
	}
}
```
### ControllerServer.java
If we recive the "quit" message, we close the the current session. Else, we add the commandLine to the input of the current shell.

```java
	@OnMessage
    public void onMessage(String[] commandLine) {
		if (initializing) {
			throw new IllegalStateException("Communication from client before ack of remote control request: " + commandLine[0]);
		} else if (commandLine.length > 0 && IShell.QUIT.equals(commandLine[0])) {
			/*
			 * TODO Stop the current toplevel (local) shell.  It is sufficient to close the session,
			 * which will trigger a callback on onClose() on both sides of the connection.
			 */
			sessionManager.closeCurrentSession();
		} else {
    		/*
    		 * TODO add the commandLine to the input of the current shell
    		 */
			shellManager.getCurrentShell().addCommandLine(commandLine);
		}
    }
```

ControllerServer @ServerEndpoint (include config for decoders), @OnOpen,@OnMessage, @OnClose. There are the annotates of corresponding methods, which relate to the protocol of web socket.

```java
	@ServerEndpoint(
			value = "/control/{client}",
			decoders = CommandLineDecoder.class
			)
	public class ControllerServer {
	...
```

```java
    @OnError
	public void onError(Throwable t) {
	...
	
	@OnClose
	public void onClose(Session session) {
	...
	
	@OnOpen
    public void onOpen(Session session, @PathParam("client") String client) throws IOException {
```

### ProxyContext.java
Override these three method in ContextBase. Implement the text display on remote client console.

```java
	@Override
	public void msg(String m) throws IOException {
		// TODO display the message on the remote client console
		sender.sendText(m);
	}

	@Override
	public void msgln(String m) throws IOException {
		// TODO display the message on the remote client console
		sender.sendText(m + '\n');
	}

	@Override
	public void err(Throwable t) throws IOException {
		// TODO print the stack trace on the remote client console
		sender.sendText(t.getMessage() + '\n');
	}
```

### SessionManager.java

When we accept the remote control request, we will create a local shell with Proxy context on the server endpoint. Then push that shell on the stack, flag the end of initializing and send the ack to response the remote node.

```	java
	public void acceptSession() throws IOException {
		lock.lock();
		try {
			/*
			 *  TODO We are accepting a remote control request.  Push a local shell with a proxy context
			 *  on the shell stack and flag that initialization has completed.  Confirm acceptance of the 
			 *  remote control request by sending an ACK to the client.  The CLI of the newly installed shell
			 *  will be executed by the underlying CLI as part of the "accept" command.
			 */
			ProxyContext proxyContext = ProxyContext.createProxyContext(currentServer.getSession().getBasicRemote());
			LocalShell localshell = LocalShell.createRemotelyControlled(ShellManager.
					getShellManager().
					getCurrentShell().
					getLocal(), proxyContext);
			ShellManager.getShellManager().addShell(localshell);
			currentServer.endInitialization();
			proxyContext.msg(SessionManager.ACK);
		} finally {
			lock.unlock();
		}
	}
```

When reject remote control request, call the session `close()` method. It'll call the corresponding Onclose method on both sides to deal with the other cleaning task.

```java
	public void rejectSession() {
		lock.lock();
		try {
			// TODO reject remote control request by closing the session (provide a reason!)
			CloseReason reason = new CloseReason(CloseCodes.CANNOT_ACCEPT, "request rejected");
			currentServer.getSession().close(reason);
			currentServer = null;
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			lock.unlock();
		}
	}
```

It's similar with above. The reason is different.

```java
	public void closeCurrentSession() {
		lock.lock();
		try {
			// TODO normal shutdown of remote control session (provide a reason!)
			CloseReason reason = new CloseReason(CloseCodes.NORMAL_CLOSURE, null);
			currentServer.getSession().close(reason);
			currentServer = null;
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			lock.unlock();
		}
	}
```

### ShellManaager.java

Call the corresponding method on `Sessinmanager` with the order 'accept' or 'reject'. If the order is 'accept', run the top shell on the stack of shell.

```java
	/**
	 * TODO Accept the pending session (see SessionManager) and 
	 * start running the CLI for the new shell that will have been
	 * pushed on the shell stack.
	 */
	protected void accept(String[] inputs) throws IOException {
		if (inputs.length != 1) {
			msgln("Usage: accept");
		} else {
			// TODO
			sessionManager.acceptSession();
			shellManager.getCurrentShell().cli();
		}
	}
```

```java
	/**
	 * TODO Reject and remove the pending session (see SessionManager).
	 */
	protected void reject(String[] inputs) throws IOException {
		if (inputs.length != 1) {
			msgln("Usage: reject");
		} else {
			// TODO
			sessionManager.rejectSession();
		}
	}
```

## Test
1. Basic connect, reject, accept. 
	* I create 3 different nodes(17,25,45). 
	* node 17 connect to node 25, reject and accept.
2. Connect while already connected (controlling remote node).
	* node 17 connect to node 25, node 25 accept.
	* node 25(remote controlled by proxy shell on node 17) connect to node 45, node 45 accept.
3. Accept while already connected (controlling remote node)
	* node 17 connect to node 25, node 25 accept.
	* node 45 connect to node 17, node 17 accept.