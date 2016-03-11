# EXPERIMENTAL Docker support for angular2 build process.
# Build with: docker build -t $USER/angular2:$(git rev-list -n 1 HEAD) .
FROM node:5.7.1
MAINTAINER Alex Eagle
WORKDIR /home

# Copy the minimal file to create a node_modules directory.
# This takes advantage of docker's caching, so that the npm install
# is only re-run when the npm-shrinkwrap.json was modified.
COPY npm-shrinkwrap.json .
RUN npm install --no-progress

COPY . .

# Allow the build to run as root. In a long-lived docker container,
# this is a security vulnerability, but we don't have a CMD so our
# container is not left running after the build completes.
RUN npm run postinstall
RUN npm run build
