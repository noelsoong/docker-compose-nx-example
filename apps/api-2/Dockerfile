FROM node:20-alpine as development

RUN apk add --no-cache libc6-compat python3 make g++

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build:api-2

FROM node:16-alpine as production
ENV NODE_ENV=production
ENV PORT=3330
EXPOSE ${PORT}

USER node
WORKDIR /app

COPY --from=development /app/dist/apps/api-2 ./
RUN npm install --only=production

CMD ["node", "main"]
