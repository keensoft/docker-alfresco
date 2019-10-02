FROM alfresco/alfresco-share:6.0

ARG TOMCAT_DIR=/usr/local/tomcat

# Logs always under $TOMCAT/logs folder
RUN echo "cd $TOMCAT_DIR/logs" > $TOMCAT_DIR/bin/setenv.sh \
    && chmod +x $TOMCAT_DIR/bin/setenv.sh

# Install modules and addons
RUN mkdir -p $TOMCAT_DIR/amps_share
COPY modules/amps_share $TOMCAT_DIR/amps_share
COPY modules/jars $TOMCAT_DIR/webapps/share/WEB-INF/lib

RUN java -jar $TOMCAT_DIR/alfresco-mmt/alfresco-mmt*.jar install \
    $TOMCAT_DIR/amps_share $TOMCAT_DIR/webapps/share -directory -nobackup -force

COPY ext-share-config-custom.xml $TOMCAT_DIR/shared/classes/alfresco/web-extension/ext-share-config
