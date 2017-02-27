FROM georchestra/security-proxy

RUN unzip -d /var/lib/jetty/webapps/ROOT /var/lib/jetty/webapps/ROOT.war  \
   && rm -rf /var/lib/jetty/webapps/ROOT.war


# trust all SSL certificates (SSL-bypass)
ADD https://packages.georchestra.org/ssl-bypasser.jar /var/lib/jetty/webapps/ROOT/WEB-INF/lib
RUN chmod 644 /var/lib/jetty/webapps/ROOT/WEB-INF/lib/ssl-bypasser.jar
COPY web.xml /var/lib/jetty/webapps/ROOT/WEB-INF/
# Some hacked classes to allow the use of a basic-auth when querying remote sites using the proxy
COPY Proxy*.class /var/lib/jetty/webapps/ROOT/WEB-INF/classes/org/georchestra/security/
COPY credentials.properties /etc/georchestra/security-proxy/credentials.properties


RUN echo "urbanisme=http://urbanisme:8080/urbanisme/"   >> /etc/georchestra/security-proxy/targets-mapping.properties
RUN echo "cadastrapp=http://cadastrapp:8080/cadastrapp/" >> /etc/georchestra/security-proxy/targets-mapping.properties

