#Specify node version
FROM node:24-alpine AS base
#Create working directory
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .

#For development
FROM base AS dev
EXPOSE 5173
CMD ["npm", "run", "dev"]

#Run build step
FROM base AS build
RUN npm run build

FROM nginx:alpine AS prod
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]