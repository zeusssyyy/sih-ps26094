FROM node:20-alpine AS build
WORKDIR /app
ARG VITE_USE_MOCKS=true
ARG VITE_API_BASE=""
ARG VITE_RISK_BASE=""
ENV VITE_USE_MOCKS=$VITE_USE_MOCKS VITE_API_BASE=$VITE_API_BASE VITE_RISK_BASE=$VITE_RISK_BASE
COPY package.json ./
RUN npm install --no-audit --no-fund
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
HEALTHCHECK --interval=30s --timeout=3s CMD wget -qO- localhost >/dev/null || exit 1
