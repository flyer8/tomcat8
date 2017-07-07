For external access and deploying apps in /manager of Tomcat 8 (Docker container):

Config changed: /usr/local/tomcat/conf/tomcat-users.xml
```
<role rolename="manager-gui"/>
<role rolename="admin-gui"/>
<role rolename="manager-script"/>
<user username="tomcat" password="tomcat" roles="manager-gui,manager-script,admin-gui"/>
```
Commented the context: /usr/local/tomcat/webapps/manager/META-INF/context.xml
```
<Context antiResourceLocking="false" privileged="true" >
<!--
  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
-->
```
Running Docker container:
```
docker run -d --name tomcat --rm -p 8080:8080 flyer8/tomcat8
```
Example of deployin WAR to Tomcat:
```
curl -T "target/webapp1.war" "http://tomcat:tomcat@192.168.0.104:8080/manager/text/deploy?path=/webapp1&update=true"
```
Login: tomcat
password: tomcat
