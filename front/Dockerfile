FROM oven/bun:1 AS builder

WORKDIR /app

COPY package*.json bunfig.toml* ./
RUN bun install

COPY . .

ARG VITE_BACK_URL
ENV VITE_BACK_URL=$VITE_BACK_URL

RUN bun run build

# Etape 2 : serveur de fichiers statiques
FROM nginx:alpine AS runner

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
