Demonstration of bug related to dmk-adapter

Adding dependency com.google.zxing:core:3.5.1 causes Nuxeo boot to fail with a Caused by: java.lang.ClassNotFoundException: com.sun.jdmk.comm.HtmlAdaptorServer in server running nuxeo-2021-HF28-1.0.0.

This project is a Nuxeo bundle that's completely empty except for a ZXing jar (see nuxeo-dmk-bug-core/pom.xml).

Java version: openjdk version "11.0.15" 2022-04-19

Full stack trace:

```
2022-11-17T09:22:50,300 ERROR [NuxeoStarter] Exception during startup
java.lang.NoClassDefFoundError: com/sun/jdmk/comm/HtmlAdaptorServer
	at org.nuxeo.dmk.DmkComponent.newAdaptor(DmkComponent.java:58) ~[nuxeo-dmk-adaptor-2021.1.19.jar:?]
	at org.nuxeo.dmk.DmkComponent.start(DmkComponent.java:120) ~[nuxeo-dmk-adaptor-2021.1.19.jar:?]
	at org.nuxeo.runtime.model.impl.RegistrationInfoImpl.start(RegistrationInfoImpl.java:372) ~[nuxeo-runtime-2021.23.2.jar:?]
	at org.nuxeo.runtime.model.impl.ComponentManagerImpl.startComponent(ComponentManagerImpl.java:758) ~[nuxeo-runtime-2021.23.2.jar:?]
	at org.nuxeo.runtime.model.impl.ComponentManagerImpl.startComponents(ComponentManagerImpl.java:740) ~[nuxeo-runtime-2021.23.2.jar:?]
	at org.nuxeo.runtime.model.impl.ComponentManagerImpl.start(ComponentManagerImpl.java:841) ~[nuxeo-runtime-2021.23.2.jar:?]
	at org.nuxeo.runtime.osgi.OSGiRuntimeService.startComponents(OSGiRuntimeService.java:470) ~[nuxeo-runtime-2021.23.2.jar:?]
	at org.nuxeo.runtime.osgi.OSGiRuntimeService.frameworkEvent(OSGiRuntimeService.java:485) ~[nuxeo-runtime-2021.23.2.jar:?]
	at org.nuxeo.osgi.OSGiAdapter.fireFrameworkEvent(OSGiAdapter.java:223) ~[nuxeo-runtime-osgi-2021.8.6.jar:?]
	at org.nuxeo.osgi.application.loader.FrameworkLoader.doStart(FrameworkLoader.java:226) ~[nuxeo-runtime-osgi-2021.8.6.jar:?]
	at org.nuxeo.osgi.application.loader.FrameworkLoader.start(FrameworkLoader.java:125) ~[nuxeo-runtime-osgi-2021.8.6.jar:?]
	at org.nuxeo.runtime.deployment.NuxeoStarter.start(NuxeoStarter.java:124) ~[nuxeo-runtime-deploy-2021.2.52.jar:?]
	at org.nuxeo.runtime.deployment.NuxeoStarter.contextInitialized(NuxeoStarter.java:93) [nuxeo-runtime-deploy-2021.2.52.jar:?]
	at org.apache.catalina.core.StandardContext.listenerStart(StandardContext.java:4769) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5231) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:183) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.ContainerBase.addChildInternal(ContainerBase.java:726) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.ContainerBase.addChild(ContainerBase.java:698) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.StandardHost.addChild(StandardHost.java:696) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.startup.HostConfig.deployDescriptor(HostConfig.java:690) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.startup.HostConfig$DeployDescriptor.run(HostConfig.java:1889) [catalina-9.0.68.jar:9.0.68]
	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:515) [?:?]
	at java.util.concurrent.FutureTask.run(FutureTask.java:264) [?:?]
	at org.apache.tomcat.util.threads.InlineExecutorService.execute(InlineExecutorService.java:75) [tomcat-util-9.0.68.jar:9.0.68]
	at java.util.concurrent.AbstractExecutorService.submit(AbstractExecutorService.java:118) [?:?]
	at org.apache.catalina.startup.HostConfig.deployDescriptors(HostConfig.java:583) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.startup.HostConfig.deployApps(HostConfig.java:473) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.startup.HostConfig.start(HostConfig.java:1618) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.startup.HostConfig.lifecycleEvent(HostConfig.java:319) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.util.LifecycleBase.fireLifecycleEvent(LifecycleBase.java:123) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.util.LifecycleBase.setStateInternal(LifecycleBase.java:423) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.util.LifecycleBase.setState(LifecycleBase.java:366) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.ContainerBase.startInternal(ContainerBase.java:946) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.StandardHost.startInternal(StandardHost.java:835) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:183) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1396) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1386) [catalina-9.0.68.jar:9.0.68]
	at java.util.concurrent.FutureTask.run(FutureTask.java:264) [?:?]
	at org.apache.tomcat.util.threads.InlineExecutorService.execute(InlineExecutorService.java:75) [tomcat-util-9.0.68.jar:9.0.68]
	at java.util.concurrent.AbstractExecutorService.submit(AbstractExecutorService.java:140) [?:?]
	at org.apache.catalina.core.ContainerBase.startInternal(ContainerBase.java:919) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.StandardEngine.startInternal(StandardEngine.java:265) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:183) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.StandardService.startInternal(StandardService.java:432) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:183) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.core.StandardServer.startInternal(StandardServer.java:930) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:183) [catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.startup.Catalina.start(Catalina.java:772) [catalina-9.0.68.jar:9.0.68]
	at jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[?:?]
	at jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62) ~[?:?]
	at jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[?:?]
	at java.lang.reflect.Method.invoke(Method.java:566) ~[?:?]
	at org.apache.catalina.startup.Bootstrap.start(Bootstrap.java:345) [bootstrap-9.0.68.jar:9.0.68]
	at org.apache.catalina.startup.Bootstrap.main(Bootstrap.java:476) [bootstrap-9.0.68.jar:9.0.68]
Caused by: java.lang.ClassNotFoundException: com.sun.jdmk.comm.HtmlAdaptorServer
	at org.apache.catalina.loader.WebappClassLoaderBase.loadClass(WebappClassLoaderBase.java:1412) ~[catalina-9.0.68.jar:9.0.68]
	at org.apache.catalina.loader.WebappClassLoaderBase.loadClass(WebappClassLoaderBase.java:1220) ~[catalina-9.0.68.jar:9.0.68]
	... 54 more
  ```
