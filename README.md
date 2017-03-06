# Demo App using Bouncy Castle FIPS Provider

This app aims at demonstrating the issue when using Bouncy Castle FIPS Provider started in FIPS unapproved mode and then changing the thread's FIPS mode to approved using `org.bouncycastle.crypto.CryptoServicesRegistrar.setApprovedOnlyMode( true )` API.

A property file fips.properties in WEB-INF/lib has options for running the app in FIPS vs Non-FIPS mode.

**Option to run the app using Bouncy Castle FIPS Provider. If set to true, adds the provider to the top of security provider list.**

fipsEnabled=true

**Option to change the thread's FIPS Mode to approved.**  

setFipsModeApproved=true 

**Note: This app aims to demonstrate the issue when changing the thread's FIPS mode to approved.**

App can be access @ https://<hostname>:8043 and clicking on the link on the page or directly accessing https://<hostname>:8043/SimpleServlet. 

__The page comes up fine when access first time. The issue occurs upon accessing the page later. Try refreshing the page or accessing it later to see the issue. The error in the log file would be as below: 
org.bouncycastle.crypto.fips.FipsUnapprovedOperationError: Attempt to use approved implementation in unapproved thread: SHA-256__

`org.bouncycastle.crypto.fips.FipsUnapprovedOperationError: Attempt to use approved implementation in unapproved thread: SHA-256
	at org.bouncycastle.crypto.internal.io.Utils.approvedModeCheck(Utils.java:16)
	at org.bouncycastle.crypto.internal.io.DigestOutputStream.write(DigestOutputStream.java:42)
	at org.bouncycastle.crypto.UpdateOutputStream.update(UpdateOutputStream.java:58)
	at org.bouncycastle.jcajce.provider.BaseMessageDigest.engineUpdate(BaseMessageDigest.java:51)
	at java.security.MessageDigest.update(MessageDigest.java:325)
	at sun.security.ssl.HandshakeHash.update(HandshakeHash.java:118)
	at sun.security.ssl.InputRecord.hashInternal(InputRecord.java:370)
	at sun.security.ssl.InputRecord.doHashes(InputRecord.java:351)
	at sun.security.ssl.HandshakeInStream.digestNow(HandshakeInStream.java:157)
	at sun.security.ssl.Handshaker.processLoop(Handshaker.java:980)
	at sun.security.ssl.Handshaker$1.run(Handshaker.java:919)
	at sun.security.ssl.Handshaker$1.run(Handshaker.java:916)
	at java.security.AccessController.doPrivileged(Native Method)
	at sun.security.ssl.Handshaker$DelegatedTask.run(Handshaker.java:1369)
	at org.apache.tomcat.util.net.SecureNioChannel.tasks(SecureNioChannel.java:285)
	at org.apache.tomcat.util.net.SecureNioChannel.handshakeUnwrap(SecureNioChannel.java:343)
	at org.apache.tomcat.util.net.SecureNioChannel.handshake(SecureNioChannel.java:192)
	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1534)
	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.run(NioEndpoint.java:1515)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61)
	at java.lang.Thread.run(Thread.java:745)`
