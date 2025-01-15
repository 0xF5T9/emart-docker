FROM node:20

WORKDIR /myapp
COPY emart-backend .
COPY import/upload.zip .

RUN unzip -o upload.zip

RUN npm install --no-audit

CMD [ "npm", "start" ]