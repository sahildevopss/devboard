#Stage1-Builder stage - used to build the package and app

FROM node:24-alpine as builder

#This will create a folder myapp and make it as pwd
WORKDIR /myapp

# Cache dependencies: Copy ONLY package files first
COPY package*.json ./

# Install ALL dependencies (including devDependencies like Vite/TypeScript)
RUN npm ci

#This will copy all the code 
COPY . .

#This will create dist folder 
RUN npm run build

#---------stage 1 complete---------------------------

#This is satge 2 (Runner stage) - used to run the application from the builder stage

FROM node:24-alpine

WORKDIR /myapp

COPY package*.json ./

RUN npm install -g vite

COPY --from=builder /myapp/dist ./dist

COPY vite.preview.config.js ./vite.config.js

CMD ["vite", "preview", "--host", "0.0.0.0", "--port", "4173"]
