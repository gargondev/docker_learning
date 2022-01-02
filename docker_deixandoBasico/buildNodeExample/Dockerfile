FROM node:alpine
LABEL description "Example Environment Node JS Docker"

WORKDIR /usr/app

COPY package*.json ./
RUN npm install 

COPY . .

EXPOSE 3000

CMD ["npm", "start"]