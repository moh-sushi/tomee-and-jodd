# tomee-and-jodd
example project for Apache TomEE and [Jodd](https://www.jodd.org) -> asm problems

steps to reproduce:
- download and install [Apache TomEE plus Edition 1.7.4 ](http://repo.maven.apache.org/maven2/org/apache/openejb/apache-tomee/1.7.4/apache-tomee-1.7.4-plus.zip)
- execute `mvn clean install`
- copy `jodd411.war` into `$CATALINA_HOME/webapps`
- start tomee via `$CATALINA_HOME/bin/catalina.(sh|bat) jpda start`


full stacktrace : see [stacktrace.txt](stacktrace.txt)

snippet:

`Caused by: java.lang.IllegalArgumentException
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
`


Results:
- stacktrace is thrown in apache-tomee-1.7.5 , too
- with jodd 3.9.1, no exception is thrown
- with jodd 4.0.0, an exception (see above) is thrown
- with jodd 4.1.0, an exception (see above) is thrown


explanation:

in jodd-core there are java 9 class files (META-INF directory) for running jodd in Java 9.
But these classes are read by asm5 (from openejb). and asm5 can not read Java 9 class files.
Therefore the exception (see above) is thrown
