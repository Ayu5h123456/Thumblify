# Node server for Thumbnail backend
FROM node:18-alpine
WORKDIR /app

# copy package files and install production deps
COPY package.json package-lock.json* ./
RUN npm install --production

# copy source code
COPY . .

# expose port the server listens on (matching server.ts)
EXPOSE 3000

# default command
CMD ["npm", "run", "start"]
