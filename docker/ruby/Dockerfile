FROM ruby:2.5-alpine

RUN apk update && \
    apk add --no-cache build-base libxml2-dev libxslt-dev

ENV APP_HOME=/app
WORKDIR $APP_HOME

COPY ./Gemfile $APP_HOME
RUN bundle install
