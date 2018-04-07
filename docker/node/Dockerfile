FROM node:8.11

# Update npm to latest version
RUN npm install -g npm

# Set PROJECT USER
RUN useradd -ms /bin/bash project
USER project
WORKDIR /project

CMD tail -f /dev/null
