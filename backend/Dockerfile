# Use the official Node.js 14 image as a base image
FROM node:14

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install the application's dependencies inside the container
RUN npm install

ARG MONGO_USERNAME
ARG MONGO_PASSWORD
ARG PORT
ARG MONGO_URI
ARG REACT_APP_BACKEND_URL

ENV MONGO_USERNAME=${MONGO_USERNAME}
ENV MONGO_PASSWORD=${MONGO_PASSWORD}
ENV MONGO_URI=${MONGO_URI}
ENV PORT=${PORT}
ENV REACT_APP_BACKEND_URL=${REACT_APP_BACKEND_URL}

# Copy the rest of the application code to the container
COPY . .

# Specify the command to run when the container starts
CMD [ "node", "index.js" ]
