From node:22-alpine As builder

WORKDIR /app
COPY package*.json ./app
#  Clean and fast install using lock file (CI-style)
RUN npm ci 

# Now copy the remaining app source files
COPY . .

# Build the React app (generates static files in /build)
RUN npm build

# Stage 2: Serve with Nginx

FROM nginx:alpine