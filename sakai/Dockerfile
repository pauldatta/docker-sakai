# This is the file that is actually use to build the production images
# It copies a build of Sakai ontop of the sakai tomcat
#

FROM fresco/sakai-tomcat

# Copy all the files in
# COPY tomcat/components /opt/tomcat/components/
# COPY tomcat/lib /opt/tomcat/sakai-lib/
# COPY tomcat/webapps /opt/tomcat/webapps/
COPY sakai.properties /opt/tomcat/sakai/sakai.properties

COPY ./entrypoint.sh /opt/scripts/entrypoint.sh
RUN chmod +x /opt/scripts/entrypoint.sh
RUN chmod +x /opt/tomcat/bin/catalina.sh

# We don't copy local.properties for production
COPY  log4j.properties placeholder.properties sakai.quartz.properties /opt/tomcat/sakai/

# Up the memory for production
ENV CATALINA_OPTS_MEMORY -Xms1g -Xmx2g

# To allow de-reploy and expanding of webapps.
RUN chown sakai /opt/tomcat/webapps

# Create archive folder and make sure it's writeable by the sakai user.
RUN \
  mkdir /opt/tomcat/sakai/archive && \
  chown sakai /opt/tomcat/sakai/archive

CMD ["/opt/tomcat/bin/catalina.sh", "run"]