FROM node:18-alpine

WORKDIR /var/www/app

# Install specific npm version globally
RUN npm install -g npm@10.8.1

COPY package*.json ./

RUN npm install

# Update npm packages
RUN npm update

COPY . .

COPY .env .env

EXPOSE 5173

# Start the application with --host flag to expose it on all network interfaces
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]

