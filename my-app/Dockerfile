FROM public.ecr.aws/docker/library/node:18.19-alpine AS build-step
RUN mkdir -p /app
WORKDIR /app
COPY package.json /app
RUN npm install --force
COPY . /app
RUN npm run build
 
FROM nginx:alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=build-step /app/dist/my-app/browser/ .
RUN ls -ltr /usr/share/nginx/html/
CMD ["nginx", "-g", "daemon off;"]