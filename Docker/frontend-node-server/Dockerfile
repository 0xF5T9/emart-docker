FROM node:20

WORKDIR /myapp
COPY emart-frontend .

RUN npm install --no-audit

ARG NODE_ENV
ARG API_URL
ARG UPLOAD_URL
ARG PORT
ENV NODE_ENV=${NODE_ENV}
ENV API_URL=${API_URL}
ENV UPLOAD_URL=${UPLOAD_URL}
ENV PORT=${PORT}

# The build task may fail due to insufficient memory on machines with low memory.
# In such case, we can set virtual memory.
# Windows: https://www.ibm.com/docs/en/bpm/8.5.6?topic=environment-tuning-your-windows-virtual-memory-settings
# Ubuntu: https://repost.aws/knowledge-center/ec2-memory-swap-file
RUN NODE_OPTIONS="--max-old-space-size=4096" npm run build-prod

CMD [ "npm", "start" ]