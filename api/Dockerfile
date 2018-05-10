FROM node:carbon

# ENV NPM_CONFIG_PREFIX=/usr/src/app/node_modules/.bin
ENV PATH=$PATH:/home/node/app/node_modules/.bin

# Use node user from carbon image
USER node

# Needed because WORKDIR creates directories as root
RUN mkdir -p /home/node/app

# Create app directory, doesnt take USER in mind
WORKDIR /home/node/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install --silent
# If you are building your code for production
# RUN npm install --only=production

# Bundle app source
COPY . .

EXPOSE 3333

CMD ["node", "server.js"]
