# tomee-and-jodd
example project for Apache TomEE and Jodd -> asm problems

steps to reproduce:
- download Apache TomEE plus Edition 1.7.4 
- execute `mvn clean install`
- copy `jodd411.war` into `$CATALINA_HOME/webapps`
- start tomee via `$CATALINA_HOME/bin/catalina.(sh|bat) jpda start`
