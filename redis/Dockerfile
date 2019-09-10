FROM centos:latest
MAINTAINER xiaowu "965391514@qq.com"
RUN sed -i -e '/mirrors.cloud.aliyuncs.com/d' -e '/mirrors.aliyuncs.com/d' /etc/yum.repos.d/CentOS-Base.repo
RUN groupadd -r redis && useradd  -r -g redis redis
RUN  yum -y update &&  yum -y install epel-release \
&&   yum -y install redis  && yum -y install wget \
&&   yum -y install net-tools \
&&   yum -y install  ruby && yum  -y install  rubygems
COPY ./sh/redis-3.2.1.gem /tmp/
RUN cd /tmp/  &&  gem install -l ./redis-3.2.1.gem \
&&  rm -f ./redis-3.2.1.gem
COPY  ./sh/redis-trib.rb  /usr/bin
COPY  ./sh/redis.sh       /usr/bin
COPY  ./sh/redis-master.sh       /usr/bin
RUN  mkdir -p /config  && chmod  775  /usr/bin/redis-master.sh && chmod  +x  /usr/bin/redis-trib.rb