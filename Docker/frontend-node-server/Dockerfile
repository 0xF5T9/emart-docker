FROM node:20

WORKDIR /myapp
COPY vyfood-frontend .

RUN npm install --no-audit

ARG NODE_ENV
ARG API_URL
ARG UPLOAD_URL
ARG PORT
ENV NODE_ENV=${NODE_ENV}
ENV API_URL=${API_URL}
ENV UPLOAD_URL=${UPLOAD_URL}
ENV PORT=${PORT}
RUN npm run build-prod

CMD [ "npm", "start" ]