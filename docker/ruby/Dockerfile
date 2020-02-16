FROM node:12.16.0-buster as builder

FROM ruby:2.5-buster

RUN apt-get update && \
    apt-get install -y default-mysql-client rsync zip

RUN useradd -m jets && \
    gpasswd -a jets sudo && \
    echo "jets:jets" | chpasswd

ENV YARN_VERSION=1.22.0
COPY --from=builder /opt/yarn-v$YARN_VERSION /opt/yarn/
COPY --from=builder /usr/local/bin/node /usr/local/bin/
RUN ln -s /opt/yarn/bin/yarn /usr/local/bin/yarn && \
    ln -s /opt/yarn/bin/yarnpkg /usr/local/bin/yarnpkg

USER jets
ENV APP_HOME=/app
WORKDIR $APP_HOME

COPY ./Gemfile* $APP_HOME/
RUN bundle install
