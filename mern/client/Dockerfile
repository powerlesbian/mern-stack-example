# FROM node:lts-alpine
# ENV NODE_ENV=production
# WORKDIR /usr/src/app
# COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
# RUN npm install --production --silent && mv node_modules ../
# # RUN npm audit fix
# COPY . .
# EXPOSE 3000
# # RUN chown -R node /usr/src/app
# # USER node
# CMD ["npm", "start"]

# Stage 1 - the build process
FROM node:lts-alpine as build-deps
WORKDIR /usr/src/app
COPY ["package.json", "package-lock.json*", "./"]
RUN npm install --production && mv node_modules ../
COPY . ./
EXPOSE 3000
CMD [ "npm","run","build" ]

# Stage 2 - the production environment
FROM nginx:1.12-alpine
COPY --from=build-deps /usr/src/app/build /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]