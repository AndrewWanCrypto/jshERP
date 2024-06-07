FROM node:16.16.0 as builder

WORKDIR /app

COPY package*.json ./
COPY . .
ENV NODE_OPTIONS=--openssl-legacy-provider
RUN yarn install \
    && yarn build

FROM nginx:1.12.2-alpine

COPY --from=builder /app/dist /usr/share/nginx/html
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
