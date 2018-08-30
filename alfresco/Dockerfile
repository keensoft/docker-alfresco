FROM alfresco/alfresco-content-repository-community:6.0.7-ga

# Fix to https://issues.alfresco.com/jira/browse/ALF-22013
ENV LC_ALL C.UTF-8 \
    LANG C.UTF-8

ARG TOMCAT_DIR=/usr/local/tomcat

RUN mkdir -p $TOMCAT_DIR/amps

# Install modules and addons
COPY modules/amps $TOMCAT_DIR/amps
COPY modules/jars $TOMCAT_DIR/webapps/alfresco/WEB-INF/lib

RUN java -jar $TOMCAT_DIR/alfresco-mmt/alfresco-mmt*.jar install \
    $TOMCAT_DIR/amps $TOMCAT_DIR/webapps/alfresco -directory -nobackup -force