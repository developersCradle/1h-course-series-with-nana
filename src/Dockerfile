FROM node:19-alpine

COPY pacakage.json /app/
COPY src /app/ 

# COPY src /app/, last / is important. Docker will create new folder if there is no 

WORKDIR /app

RUN npn install

CMD ["node", "server.js"]