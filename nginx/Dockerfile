FROM node:carbon as base-nodejs

# Use node user from carbon image
USER node

# Needed because WORKDIR creates directories as root
RUN mkdir -p /tmp/app && mkdir -p /tmp/web

# Create app directory, doesnt take USER in mind
WORKDIR /tmp/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY ./app/package*.json ./

RUN npm install --silent
# If you are building your code for production
# RUN npm install --only=production

# Bundle app source
COPY --chown=node ./app/ .

# npm run build --production or NODE_ENV=production
RUN npm run build

WORKDIR /tmp/web
COPY ./web/package*.json ./

RUN npm install --silent

# --chown=node because COPY uses root user by default and npm run build fails
COPY --chown=node ./web/ .

# npm run build --production or NODE_ENV=production
RUN npm run build

FROM nginx:1.13.12-alpine

WORKDIR /var/www/app

COPY --from=base-nodejs /tmp/app/dist/ /var/www/app/

WORKDIR /var/www/app

COPY --from=base-nodejs /tmp/web/dist/ /usr/share/nginx/html/

EXPOSE 80