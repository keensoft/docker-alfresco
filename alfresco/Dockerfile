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

# Install AOS
RUN yum -y update && \
 yum -y install wget && \
 yum -y install unzip && \
 yum clean all

RUN set -x \
        && mkdir /tmp/aos \
        && wget --no-check-certificate https://download.alfresco.com/cloudfront/release/community/201806-GA-build-00113/alfresco-aos-module-distributionzip-1.2.0.zip \
        && unzip alfresco-aos-module-distributionzip-1.2.0.zip -d /tmp/aos \
        && mv /tmp/aos/extension/* $TOMCAT_DIR/shared/classes/alfresco/extension \
        && mv /tmp/aos/alfresco-aos-module-1.2.0.amp amps \
        && mv /tmp/aos/aos-module-license.txt licenses \
        && mv /tmp/aos/_vti_bin.war $TOMCAT_DIR/webapps \
        && rm -rf /tmp/aos alfresco-aos-module-distributionzip-1.2.0.zip
        
COPY alfresco-global.properties $TOMCAT_DIR/shared/classes/alfresco-global.properties
