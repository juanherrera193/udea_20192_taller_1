# you should use the 'node' official image, with the alpine 6.x branch
FROM node:6.17.1-alpine

# then it should use alpine package manager to install tini
RUN apk add --no-cache tini

# then it should create directory /usr/src/app for app files
WORKDIR /usr/src/app

# Node uses a "package manager", so it needs to copy in package.json file
COPY package*.json ./

# then it needs to run 'npm install' to install dependencies from that file
# to keep it clean and small, run 'npm cache clean --force' after above
RUN npm install && npm cache clean --force

# then it needs to copy in all files from current directory
COPY . .

# this app listens on port 3000, but the container should launch on port 80
# so it will respond to http://localhost:80 on your computer
EXPOSE 3000

# then it needs to start container with command '/sbin/tini -- node ./bin/www'
ENTRYPOINT ["/sbin/tini", "--", "node", "./bin/www"]