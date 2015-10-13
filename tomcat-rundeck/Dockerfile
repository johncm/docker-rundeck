# The current version of RunDeck requires Java 7 JRE
FROM tomcat:7-jre7

# Current version of RunDeck (target)
ENV RUNDECK_VERSION 2.5.3
ENV RUNDECK_DOWNLOAD_URL http://download.rundeck.org
ENV RUNDECK_WAR_URL $RUNDECK_DOWNLOAD_URL/war/rundeck-$RUNDECK_VERSION.war
ENV RUNDECK_WAR rundeck.war
ENV APP_CONTEXT rundeck
ENV RUNDECK_WEBAPP $CATALINA_HOME/webapps/$APP_CONTEXT

ENV UNZIP -qaL -d $RUNDECK_WEBAPP
# Could have piped the curl to the unzip, but if download fails, I want it to show the error as a download issue.
RUN set -x && \
	mkdir -p $RUNDECK_WEBAPP && \ 
	curl -fSL "$RUNDECK_WAR_URL" -o $RUNDECK_WAR && \
	unzip $RUNDECK_WAR && \
	rm $RUNDECK_WAR

# https://github.com/rundeck/rundeck/issues/1187
# the normal jetty/launcher installer creates a "log4j.properties" file for you.
# You would need to create one within the classpath for the webapp, e.g. at $CATALINA_HOME/webapps/rundeck/WEB-INF/classes/log4j.properties
RUN touch $RUNDECK_WEBAPP/WEB-INF/classes/log4j.properties
