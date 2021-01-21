# BASE 基础镜像
FROM centos:7


# 安装java
RUN  cd /etc/yum.repos.d/ \
    && rm -rf * \
    && curl http://mirrors.aliyun.com/repo/Centos-7.repo -o Centos-7.repo \
    && curl http://mirrors.aliyun.com/repo/epel-7.repo -o epel-7.repo \
	&& yum -y install java-1.8.0-openjdk java-1.8.0-openjdk-devel \
	&& yum clean all
ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk


# 安装maven https://github.com/carlossg/docker-maven/blob/master/openjdk-8/Dockerfile
ARG MAVEN_VERSION=3.6.3
ARG MAVEN_URL=https://mirrors.bfsu.edu.cn/apache/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz
RUN mkdir -p /usr/share/maven /usr/share/maven/ref \
  && curl -fsSL -o /tmp/apache-maven.tar.gz $MAVEN_URL \
  && tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn


# 安装node js 和yarn  https://github.com/nodejs/docker-node/blob/f14cf35127b04cec97f01e473d59a0df03ac00d1/14/buster/Dockerfile
ENV NODE_VERSION 14.15.4
ENV ARCH=x64
RUN  curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-$ARCH.tar.xz" \
      && tar -xJf "node-v$NODE_VERSION-linux-$ARCH.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
      && rm "node-v$NODE_VERSION-linux-$ARCH.tar.xz"  \
      && ln -s /usr/local/bin/node /usr/local/bin/nodejs
RUN npm install -g yarn
RUN npm config set registry https://registry.npm.taobao.org
RUN	yarn config set registry https://registry.npm.taobao.org
RUN	yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass