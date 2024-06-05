FROM node:16-bullseye-slim
LABEL authors="Kamil Witczak"

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY . /app

RUN npm i

EXPOSE 8000

CMD ["npm", "start"]