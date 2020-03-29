## Build
FROM beevelop/ionic AS ionic
# Create app directory
WORKDIR /usr/src/app
RUN apk --no-cache --virtual build-dependencies add \
    python \
    make \
    g++ \
    && npm install \
    && apk del build-dependencies
# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./
RUN npm ci
# Bundle app source
COPY . .
RUN ionic build

## Run 
FROM nginx:alpine
#COPY www /usr/share/nginx/html
COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html

