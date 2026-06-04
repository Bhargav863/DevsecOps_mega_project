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

# Copy built static files from builder stage

COPY --from=builder /app/build /usr/share/nginx/html

#  Add custom nginx config (optional but usually required for SPA)
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80
# start the nginx
CMD ["nginx", "-g", "daemon off;"]