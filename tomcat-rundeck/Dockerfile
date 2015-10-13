# The current version of RunDeck requires Java 7 JRE
FROM tomcat:7-jre7

# Current version of RunDeck (target)
ENV RUNDECK_VERSION 2.5.3
ENV RUNDECK_DOWNLOAD_URL http://download.rundeck.org
ENV RUNDECK_WAR_URL $RUNDECK_DOWNLOAD_URL/war/rundeck-$RUNDECK_VERSION.war
ENV APP_CONTEXT rundeck

# Could have piped the curl to the unzip, but if download fails, I want it to show the error as a download issue.
RUN set -x && \
	curl -fSL "$RUNDECK_WAR_URL" -o rundeck.war && \
	unzip -q -d $CATALINA_HOME/webpps/$APP_CONTEXT rundeck.war && \
	rm rundeck.war

# https://github.com/rundeck/rundeck/issues/1187
# the normal jetty/launcher installer creates a "log4j.properties" file for you.
# You would need to create one within the classpath for the webapp, e.g. at $CATALINA_HOME/webapps/rundeck/WEB-INF/classes/log4j.properties
RUN touch $CATALINA_HOME/webpps/$APP_CONTEXT/WEB-INF/classes/log4j.properties
