
FROM node:18-alpine AS builder
WORKDIR /app


COPY backend/package.json ./
RUN npm install


COPY backend/ ./
RUN npm run build


FROM node:18-alpine AS runner
WORKDIR /app

COPY backend/package.json ./
RUN npm install --production


COPY --from=builder /app/dist ./dist

RUN chown -R node:node /app

USER node

ENV NODE_ENV=production
ENV BACKEND_PORT=3847

EXPOSE 3847

CMD ["node", "dist/index.js"]
