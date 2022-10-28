FROM node:18-slim

WORKDIR /app

EXPOSE 3000

COPY start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

USER node

ENTRYPOINT [ "start-container" ]
