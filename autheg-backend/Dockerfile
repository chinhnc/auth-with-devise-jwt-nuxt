FROM ruby:2.6.5

ARG UID
RUN adduser rails --uid $UID --disabled-password --gecos ""

ENV APP /usr/src/app
RUN mkdir $APP
WORKDIR $APP

COPY Gemfile* $APP/
RUN bundle install -j3 --path vendor/bundle

COPY . $APP/

RUN gem install rails
RUN bundle

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000
RUN export RUBYOPT=-EUTF-8

CMD ["rails", "server", "-p", "8080", "-b", "0.0.0.0"]
