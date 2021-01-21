# BASE 基础镜像
FROM centos:7
ENV MAVEN_VERSION=3.6.3


RUN  cd /etc/yum.repos.d/ && rm -rf * && curl http://mirrors.aliyun.com/repo/Centos-7.repo -o Centos-7.repo && curl http://mirrors.aliyun.com/repo/epel-7.repo -o epel-7.repo \
	&& yum -y install wget java-1.8.0-openjdk java-1.8.0-openjdk-devel \
	&& wget https://mirrors.bfsu.edu.cn/apache/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
    	&& tar xzvf *.gz && rm -rf *.gz  && mv apache-maven-${MAVEN_VERSION} maven \
    	&& mv maven /usr/local/bin \
    	&& export PATH=/usr/local/bin/maven/bin:$PATH \
    	&& ln -s /usr/local/bin/maven/bin/mvn /usr/local/bin/mvn \
	&& yum clean all
ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk

# 安装node js
ENV NODE_VERSION 14.15.4
ENV ARCH=x64
RUN curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-$ARCH.tar.xz \
	 && tar -xJf "node-v$NODE_VERSION-linux-$ARCH.tar.xz" -C /usr/local --strip-components=1  \
	 && rm "node-v$NODE_VERSION-linux-$ARCH.tar.xz" \
	 && ln -s /usr/local/bin/node /usr/local/bin/nodejs
	 
RUN npm config set registry https://registry.npm.taobao.org && npm install -g yarn \
	&& yarn config set registry https://registry.npm.taobao.org  && yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass   \
	&& npm install umi -g \

RUN mvn -version
RUN java -version
