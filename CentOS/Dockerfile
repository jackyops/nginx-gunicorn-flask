# nginx-gunicorn-flask

FROM centos:latest
MAINTAINER Jacky zhou <jackyops@163.com>

RUN yum -y install epel-release
RUN yum -y update
RUN yum -y install python-devel python-pip supervisor gunicorn nginx
RUN pip install gunicorn
RUN yum clean all

# Setup flask application
RUN mkdir -p /deploy/app
COPY app /deploy/app
RUN pip install -r /deploy/app/requirements.txt

# setup nginx 
#RUN rm /etc/nginx/conf.d/default.conf
COPY nginx_flask.conf /etc/nginx/conf.d/default.conf
RUN echo "daemon off;" >>/etc/nginx/nginx.conf 

# Setup supervisord
RUN mkdir -p /var/log/supervisor
COPY supervisord.ini /etc/supervisord.d/
COPY gunicorn.ini /etc/supervisord.d/

# Start processes
# Start processes in docker-compose.yml
# CMD ["/usr/bin/supervisord","-c","/etc/supervisord.conf"]
CMD ["/bin/bash"]
