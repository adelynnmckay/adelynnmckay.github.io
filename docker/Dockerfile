FROM ruby:3.2

ENV LANG=C.UTF-8 \
    JEKYLL_ENV=debug \
    BUNDLE_PATH=vendor/bundle

RUN apt-get update -qq && apt-get install -y \
    build-essential \
    nodejs \
    git

WORKDIR /srv/jekyll

# Copy the Jekyll site contents (root of build context)
COPY ./adelynnmckay.github.io ./adelynnmckay.github.io

# Copy the local theme from one directory up (requires correct build context)
COPY ./jekyll-theme-ade ./jekyll-theme-ade

WORKDIR /srv/jekyll/adelynnmckay.github.io

RUN gem install bundler && \
    bundle config set --local path 'vendor/bundle' && \
    (bundle update || true) && \
    bundle install && \
    mkdir -p _site

EXPOSE 4000

CMD ["bundle", "exec", "jekyll", "serve", "--watch", "--host", "0.0.0.0"]
