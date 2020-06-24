FROM node:lts-slim

ENV NODE_ENV production

RUN mkdir -p /app \
    && cd /app \
    && npm install -g maildev
EXPOSE 80 25

CMD ["maildev", "--web", "80", "--smtp", "25"]