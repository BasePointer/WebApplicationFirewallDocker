FROM owasp/modsecurity-crs

# Install filebeat
RUN apt-get update && apt-get install -y gnupg2 wget && wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add - && apt-get install apt-transport-https && echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-7.x.list && apt-get update && apt-get install filebeat

# Configure filebeat
COPY filebeat.yml /etc/filebeat/filebeat.yml

# Configure CRS 
COPY crs-setup.conf /etc/modsecurity.d/owasp-crs/crs-setup.conf

# Copy Exclude Rulesets
COPY REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf /etc/modsecurity.d/owasp-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf

# Start filebeat
RUN service filebeat start
