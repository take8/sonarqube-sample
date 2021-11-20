FROM sonarqube:lts

RUN apk add wget unzip vim git
# JS, TSの解析は以下も必要
RUN apk add nodejs npm

WORKDIR /opt/sonarqube

# sonar-scanner のダウンロード、解凍
ARG SONAR_SCANNER_VERSION=4.6.2.2472
RUN wget -O sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip
RUN unzip sonar-scanner.zip
RUN rm sonar-scanner.zip

# RUN echo 'export PATH="$PATH:/opt/sonarqube/sonar-scanner-${SONAR_SCANNER_VERSION}-linux/bin"' >> ~/.bashrc
RUN ln -s /opt/sonarqube/sonar-scanner-${SONAR_SCANNER_VERSION}-linux/bin/sonar-scanner /usr/bin/sonar-scanner
