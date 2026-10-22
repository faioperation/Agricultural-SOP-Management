# Multi-stage build for React Vite Frontend
FROM node:20-alpine AS builder
WORKDIR /app

# Build arguments for Vite environment variables
ARG VITE_BASE_URL=/api
ARG VITE_EMAILJS_SERVICE_ID=service_zoux3ru
ARG VITE_EMAILJS_TEMPLATE_ID=template_bup4wlv
ARG VITE_EMAILJS_PUBLIC_KEY=M-TrnCB_xCVsTnsX8
ARG VITE_EMAILJS_AUTO_REPLY_TEMPLATE_ID=template_5gkyyjc

ENV VITE_BASE_URL=$VITE_BASE_URL
ENV VITE_EMAILJS_SERVICE_ID=$VITE_EMAILJS_SERVICE_ID
ENV VITE_EMAILJS_TEMPLATE_ID=$VITE_EMAILJS_TEMPLATE_ID
ENV VITE_EMAILJS_PUBLIC_KEY=$VITE_EMAILJS_PUBLIC_KEY
ENV VITE_EMAILJS_AUTO_REPLY_TEMPLATE_ID=$VITE_EMAILJS_AUTO_REPLY_TEMPLATE_ID

COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Nginx stage to serve frontend static content
FROM nginx:1.25-alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
