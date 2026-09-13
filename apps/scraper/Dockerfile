# Plain Node: the scraper talks to ADE's iCalendar servlet over HTTP and needs
# no browser. It used to run on the Playwright image for Chromium alone.
FROM node:22-slim
WORKDIR /app

RUN npm install -g pnpm@11.21.0

COPY package.json pnpm-lock.yaml pnpm-workspace.yaml ./
COPY apps/api/package.json     apps/api/
COPY apps/scraper/package.json apps/scraper/
COPY apps/web/package.json     apps/web/
COPY packages/db/package.json       packages/db/
COPY packages/shared/package.json   packages/shared/
COPY packages/tsconfig/package.json packages/tsconfig/

RUN pnpm install --frozen-lockfile --filter @studysuite/scraper...

COPY packages/ packages/
COPY apps/scraper/ apps/scraper/

# Watch loop: rescrapes every scrape.intervalMs and stays up.
CMD ["pnpm", "--filter", "@studysuite/scraper", "run", "start"]
