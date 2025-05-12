FROM node:18-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
ARG REACT_APP_COLOR
ENV REACT_APP_COLOR=$REACT_APP_COLOR
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
