FROM ruby:2.5-alpine

RUN apk update && \
    apk add --no-cache build-base libxml2-dev libxslt-dev

RUN adduser -S jets && \
    echo "jets ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    echo 'jets:jets' | chpasswd

USER jets
ENV APP_HOME=/app
WORKDIR $APP_HOME

COPY ./Gemfile* $APP_HOME/
RUN bundle install
