FROM node:alpine as builder

FROM ruby:2.5-alpine

RUN apk update && \
    apk add --no-cache build-base libxml2-dev libxslt-dev git mariadb-dev

RUN adduser -S jets && \
    echo "jets ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    echo 'jets:jets' | chpasswd

ENV YARN_VERSION=1.21.1
COPY --from=builder /opt/yarn-v$YARN_VERSION /opt/yarn/
COPY --from=builder /usr/local/bin/node /usr/local/bin/
RUN ln -s /opt/yarn/bin/yarn /usr/local/bin/yarn && \
    ln -s /opt/yarn/bin/yarnpkg /usr/local/bin/yarnpkg

USER jets
ENV APP_HOME=/app
WORKDIR $APP_HOME

COPY ./Gemfile* $APP_HOME/
RUN bundle install
