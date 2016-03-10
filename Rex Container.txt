FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup | sudo bash -
RUN apt-get update
RUN apt-get install -y nodejs
RUN npm -g install npm@latest
Run apt-get install -y nginx
COPY ./rex /etc/nginx/sites-available/rex
RUN ln -s /etc/nginx/sites-available/rex /etc/nginx/sites-enabled/rex
RUN rm /etc/nginx/sites-enabled/default
RUN cd /bdshare/REX_WEB;npm install;bower install;
RUN service nginx start
EXPOSE 3000
CMD ["gulp serve"]