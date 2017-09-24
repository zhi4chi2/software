# Introduction
# Installation
# Deployment Organization
## Standard Directory Layout
- /WEB-INF/web.xml
- /WEB-INF/classes/
- /WEB-INF/lib/


## Shared Library Files
The details of how Tomcat locates and shares such classes are described in the Class Loader HOW-TO documentation.(http://tomcat.apache.org/tomcat-8.0-doc/class-loader-howto.html)


The location commonly used within a Tomcat installation for shared code is $CATALINA_HOME/lib.


## Web Application Deployment Descriptor
## Tomcat Context Descriptor
A /META-INF/context.xml file can be used to define Tomcat specific configuration options, such as an access log, data sources, session manager configuration and more.


参见 http://tomcat.apache.org/tomcat-8.0-doc/config/context.html


## Deployment With Tomcat
当使用 war 发布时， If you use this approach, and wish to update your application later, you must both replace the web application archive file AND delete the expanded directory that Tomcat created, and then restart Tomcat, in order to reflect your changes. 


# Source Organization
FIXME


# Development Processes
# Sample Application
