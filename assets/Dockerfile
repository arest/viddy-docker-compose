FROM node:10

RUN rm -rf /var/lib/apt/lists/*
RUN apt-get update && \
    apt install -y libpq-dev libxml2-dev python-pip libicu-dev ruby-dev && \
    gem install compass

# Install Bower & Grunt
RUN npm install -g bower grunt-cli && \
    echo '{ "allow_root": true }' > /root/.bowerrc

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["bash"]
