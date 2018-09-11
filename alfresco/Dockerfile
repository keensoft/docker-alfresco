FROM alfresco/alfresco-content-repository-community:6.0.7-ga

# Fix to https://issues.alfresco.com/jira/browse/ALF-22013
ENV LC_ALL C.UTF-8 \
    LANG C.UTF-8

ARG TOMCAT_DIR=/usr/local/tomcat

# Logs always under $TOMCAT/logs folder
RUN echo "cd $TOMCAT_DIR/logs" > $TOMCAT_DIR/bin/setenv.sh \
    && chmod +x $TOMCAT_DIR/bin/setenv.sh

# Install modules and addons
RUN mkdir -p $TOMCAT_DIR/amps
COPY modules/amps $TOMCAT_DIR/amps
COPY modules/jars $TOMCAT_DIR/webapps/alfresco/WEB-INF/lib

RUN java -jar $TOMCAT_DIR/alfresco-mmt/alfresco-mmt*.jar install \
    $TOMCAT_DIR/amps $TOMCAT_DIR/webapps/alfresco -directory -nobackup -force