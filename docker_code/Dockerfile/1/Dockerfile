FROM davidcaste/alpine-tomcat:jdk8tomcat8

ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
EXPOSE 8080
RUN rm -fr /opt/tomcat/webapps/ROOT

COPY admin.war /opt/tomcat/webapps/admin.war
COPY renobit.war /opt/tomcat/webapps/renobit.war

RUN rm /opt/tomcat/conf/server.xml
COPY server.xml /opt/tomcat/conf/server.xml

COPY docker_entrypoint.sh /docker_entrypoint.sh
RUN chmod +x /docker_entrypoint.sh

CMD ["/opt/tomcat/bin/catalina.sh", "run"]

ENTRYPOINT [ "/docker_entrypoint.sh" ]
 


