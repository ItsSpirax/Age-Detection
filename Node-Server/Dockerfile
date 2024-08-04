FROM node:18-alpine AS builder
WORKDIR /usr/src/app
COPY . .
RUN npm ci --silent && npm cache clean --force
RUN npm run build

FROM node:18-alpine AS production
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app/.next ./.next
COPY --from=builder /usr/src/app/public ./public
COPY --from=builder /usr/src/app/node_modules ./node_modules
COPY --from=builder /usr/src/app/package.json ./
EXPOSE 3000
USER node
CMD ["npm", "run", "start"]