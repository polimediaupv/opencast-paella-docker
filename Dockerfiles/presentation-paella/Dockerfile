FROM opencast/presentation:2.3.0
MAINTAINER polimedia team <polim@upv.es>

ENV PAELLA_TAG="5.1.8" \
	PAELLA_REPO="https://github.com/polimediaupv/paella-matterhorn.git" \
	PAELLA_SRC="/usr/src/paella-opencast"

RUN	apk add --no-cache --virtual .build-deps \
      tar gzip \
      git \
      make gcc g++ binutils-gold \
      maven \
      python nodejs \
    \
    # Download Opencast
    && mkdir -p "${PAELLA_SRC}" \
    && git clone --recursive "${PAELLA_REPO}" "${PAELLA_SRC}" \
    && cd "${PAELLA_SRC}" \
    && git checkout "${PAELLA_TAG}" \
    \
     # Prepare paella pom.xml to compile
    && cat ${PAELLA_SRC}/pom.xml | sed -e "s/<opencast.version>2.3.0<\/opencast.version>/<opencast.version>${OPENCAST_VERSION}<\/opencast.version>/" > /tmp/pom.xml \
    && mv /tmp/pom.xml ${PAELLA_SRC}/pom.xml \
    \    
     # Compile front-end assets manually as the bundeled node does not run on Alpine
    && npm install -g npm \
    && npm install -g gulp \
    && npm install \
    && gulp paella-opencast:build \
    \
     # Compile and install Paella
    && mvn install -P '!frontend' \
    && cp ${PAELLA_SRC}/target/paella-engage-ui-${PAELLA_TAG}.jar ${OPENCAST_HOME}/deploy/ \
    \
     # Configure paella bundle
    && cat ${OPENCAST_HOME}/etc/security/mh_default_org.xml | sed -e "s/<!-- Everything else is for the admin users -->/<!-- Paella -->\n    <sec:intercept-url pattern=\"\/paella\/ui\/auth.html\" access=\"ROLE_USER\" \/>\n    <sec:intercept-url pattern=\"\/paella\/ui\/**\" access=\"ROLE_ANONYMOUS\" \/>\n\n    <!-- Everything else is for the admin users -->/" > /tmp/mh_default_org.xml \
    && mv /tmp/mh_default_org.xml ${OPENCAST_HOME}/etc/security/mh_default_org.xml \
    \
    && cat ${OPENCAST_HOME}/etc/org.opencastproject.organization-mh_default_org.cfg  | sed -e "s/prop.player=\/engage\/theodul\/ui\/core.html/prop.player=\/paella\/ui\/watch.html/" > /tmp/org.opencastproject.organization-mh_default_org.cfg \
    && mv /tmp/org.opencastproject.organization-mh_default_org.cfg ${OPENCAST_HOME}/etc/org.opencastproject.organization-mh_default_org.cfg \
    \
     # Cleanup
    && apk del --no-cache .build-deps \
    && rm -rf "${PAELLA_SRC}" /tmp/* ~/.m2 ~/.npm ~/.node-gyp /usr/lib/node_modules
    
    
    
    
    
    
    
  