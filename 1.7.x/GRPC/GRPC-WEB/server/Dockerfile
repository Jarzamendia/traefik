FROM jarzamendia/grpc-web-common:grpc-web-lab

COPY ./echo /echo

RUN cd /echo/node-server && \
  npm install

EXPOSE 9090

CMD ["node", "/echo/node-server/server.js"]