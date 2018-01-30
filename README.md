# tomee-and-jodd
example project for Apache TomEE and Jodd -> asm problems

steps to reproduce:
- download and install [Apache TomEE plus Edition 1.7.4 ](http://repo.maven.apache.org/maven2/org/apache/openejb/apache-tomee/1.7.4/apache-tomee-1.7.4-plus.zip)
- execute `mvn clean install`
- copy `jodd411.war` into `$CATALINA_HOME/webapps`
- start tomee via `$CATALINA_HOME/bin/catalina.(sh|bat) jpda start`
