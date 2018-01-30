# tomee-and-jodd
example project for Apache TomEE and [Jodd](https://www.jodd.org) -> asm problems

steps to reproduce:
- download and install [Apache TomEE plus Edition 1.7.4 ](http://repo.maven.apache.org/maven2/org/apache/openejb/apache-tomee/1.7.4/apache-tomee-1.7.4-plus.zip)
- execute `mvn clean install`
- copy `jodd411.war` into `$CATALINA_HOME/webapps`
- start tomee via `$CATALINA_HOME/bin/catalina.(sh|bat) jpda start`


following stacktrace is thrown:

>  Jan 30, 2018 9:44:16 AM org.apache.openejb.util.JarExtractor extract
INFORMATION: Extracted path: c:\dev\apache-tomee-plus-1.7.4-asm6-test\webapps\jodd411
Jan 30, 2018 9:44:16 AM org.apache.catalina.core.ContainerBase addChildInternal
SCHWERWIEGEND: ContainerBase.addChild: start: 
org.apache.catalina.LifecycleException: Failed to start component [StandardEngine[Catalina].StandardHost[localhost].StandardContext[/jodd411]]
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:153)
	at org.apache.catalina.core.ContainerBase.addChildInternal(ContainerBase.java:899)
	at org.apache.catalina.core.ContainerBase.addChild(ContainerBase.java:875)
	at org.apache.catalina.core.StandardHost.addChild(StandardHost.java:652)
	at org.apache.catalina.startup.HostConfig.deployWAR(HostConfig.java:1091)
	at org.apache.catalina.startup.HostConfig$DeployWar.run(HostConfig.java:1980)
	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at java.lang.Thread.run(Thread.java:745)
Caused by: org.apache.tomee.catalina.TomEERuntimeException: org.apache.openejb.OpenEJBException: Unable to create annotation scanner for web module jodd411: null
	at org.apache.tomee.catalina.TomcatWebAppBuilder.loadApplication(TomcatWebAppBuilder.java:2198)
	at org.apache.tomee.catalina.TomcatWebAppBuilder.startInternal(TomcatWebAppBuilder.java:1147)
	at org.apache.tomee.catalina.TomcatWebAppBuilder.configureStart(TomcatWebAppBuilder.java:1100)
	at org.apache.tomee.catalina.GlobalListenerSupport.lifecycleEvent(GlobalListenerSupport.java:130)
	at org.apache.catalina.util.LifecycleSupport.fireLifecycleEvent(LifecycleSupport.java:117)
	at org.apache.catalina.util.LifecycleBase.fireLifecycleEvent(LifecycleBase.java:90)
	at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5472)
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:147)
	... 10 more
Caused by: org.apache.openejb.OpenEJBException: Unable to create annotation scanner for web module jodd411: null
	at org.apache.openejb.config.DeploymentLoader.addWebModule(DeploymentLoader.java:849)
	at org.apache.openejb.config.DeploymentLoader.load(DeploymentLoader.java:221)
	at org.apache.tomee.catalina.TomcatWebAppBuilder.loadApplication(TomcatWebAppBuilder.java:2196)
	... 17 more
Caused by: java.lang.IllegalArgumentException
	at org.apache.xbean.asm5.ClassReader.<init>(Unknown Source)
	at org.apache.xbean.asm5.ClassReader.<init>(Unknown Source)
	at org.apache.xbean.asm5.ClassReader.<init>(Unknown Source)
	at org.apache.xbean.finder.AnnotationFinder.readClassDef(AnnotationFinder.java:1169)
	at org.apache.xbean.finder.AnnotationFinder.<init>(AnnotationFinder.java:147)
	at org.apache.xbean.finder.AnnotationFinder.<init>(AnnotationFinder.java:160)
	at org.apache.openejb.config.FinderFactory$OpenEJBAnnotationFinder.<init>(FinderFactory.java:514)
	at org.apache.openejb.config.FinderFactory.newFinder(FinderFactory.java:259)
	at org.apache.openejb.config.FinderFactory.create(FinderFactory.java:77)
	at org.apache.openejb.config.FinderFactory.createFinder(FinderFactory.java:66)
	at org.apache.openejb.config.DeploymentLoader.addWebModule(DeploymentLoader.java:841)
	... 19 more
>
> Jan 30, 2018 9:44:16 AM org.apache.catalina.startup.HostConfig deployWAR
SCHWERWIEGEND: Error deploying web application archive C:\dev\apache-tomee-plus-1.7.4-asm6-test\webapps\jodd411.war
java.lang.IllegalStateException: ContainerBase.addChild: start: org.apache.catalina.LifecycleException: Failed to start component [StandardEngine[Catalina].StandardHost[localhost].StandardContext[/jodd411]]
	at org.apache.catalina.core.ContainerBase.addChildInternal(ContainerBase.java:903)
	at org.apache.catalina.core.ContainerBase.addChild(ContainerBase.java:875)
	at org.apache.catalina.core.StandardHost.addChild(StandardHost.java:652)
	at org.apache.catalina.startup.HostConfig.deployWAR(HostConfig.java:1091)
	at org.apache.catalina.startup.HostConfig$DeployWar.run(HostConfig.java:1980)
	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at java.lang.Thread.run(Thread.java:745)


Results:
- stacktrace is thrown in apache-tomee-1.7.5 , too
- with jodd 3.9.1, no exception is thrown
- with jodd 4.0.0, an exception (see above) is thrown
- with jodd 4.1.0, an exception (see above) is thrown
