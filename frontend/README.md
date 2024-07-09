# Frontend - ReactJS with ChakraUI

This directory contains the frontend of the application built with ReactJS and ChakraUI.

## Prerequisites

- Node.js (version 14.x or higher)
- npm (version 6.x or higher)

## Setup Instructions

1. **Navigate to the frontend directory**:
    ```sh
    cd frontend
    ```

2. **Install dependencies**:
    ```sh
    npm install
    ```

3. **Run the development server**:
    ```sh
    npm run dev
    ```

4. **Configure API URL**:
   Ensure the API URL is correctly set in the `.env` file.

## Docker Deployment

1. **Build and start the Docker container:**
   ```sh
   docker-compose up --build -d frontend
   ```

## Environment Variables

Set the following environment variables in the `.env` file:

```env
VITE_API_URL=http://bestbuy.crabdance.com:8000
```

## Frontend Dockerfile

Create a `Dockerfile` in the `frontend` directory with the following content:

```dockerfile
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
```
```
