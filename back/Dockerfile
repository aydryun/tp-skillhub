FROM oven/bun:1 AS builder

WORKDIR /app

COPY package*.json bunfig.toml* ./
RUN bun install

COPY . .

# Etape 2 : runner
FROM oven/bun:1 AS runner

WORKDIR /app

COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/src ./src
COPY --from=builder /app/server.js ./server.js
COPY --from=builder /app/package.json ./package.json

EXPOSE 3001

CMD ["bun", "run", "server.js"]

