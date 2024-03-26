FROM davidcaste/alpine-tomcat:jdk7tomcat8

ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
EXPOSE 8080
RUN rm -fr /opt/tomcat/webapps/ROOT
COPY renobit-2.1.5.hotfix1.war /opt/tomcat/webapps/renobit/ROOT.war
RUN rm /opt/tomcat/conf/server.xml
RUN mkdir /usr/local/snapshot
COPY server.xml /opt/tomcat/conf/server.xml
CMD ["/opt/tomcat/bin/catalina.sh", "run"]


