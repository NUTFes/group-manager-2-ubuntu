FROM ubuntu:20.04

CMD ["/bin/sh"]
RUN apt update && apt install -y tzdata
ENV TZ Asia/Tokyo
RUN apt install -y git vim wget curl
RUN apt install -y gcc git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev 
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt install -y nodejs
RUN apt install -y yarn
# RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -

# MySQL
RUN apt install -y mysql-server mysql-client
RUN apt install -y libmysqlclient-dev
RUN usermod -d /var/lib/mysql/ mysql

RUN apt update
RUN apt upgrade -y

# rbenv
RUN git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> ~/.bashrc
RUN git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
RUN chmod 777 $HOME/.rbenv/bin/rbenv
RUN $HOME/.rbenv/bin/rbenv install 2.7.1
RUN $HOME/.rbenv/bin/rbenv global 2.7.1
RUN /root/.rbenv/shims/gem install rails

RUN mkdir myapp
WORKDIR /myapp
ADD Gemfile /myapp/Gemfile
ADD Gemfile.lock /myapp/Gemfile.lock
COPY . /myapa
RUN /root/.rbenv/shims/bundle install
