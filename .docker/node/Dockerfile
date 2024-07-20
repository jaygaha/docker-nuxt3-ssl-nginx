# Use an official Node.js 18 image as a base
FROM node:18.20.4-alpine3.20

ARG WORK_DIR
ARG NUXT_PORT
ARG NODE_ENV

ENV WORK_DIR=${WORK_DIR}
ENV NODE_ENV=${NODE_ENV}

# Set the working directory to /app
WORKDIR ${WORK_DIR}

# Copy the package.json and package-lock.json files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the code
COPY . .

RUN npm cache clean --force

RUN npm run build

# Expose the port
EXPOSE ${NUXT_PORT}

# Run the command to start the server
CMD ["npm", "run", "start"]