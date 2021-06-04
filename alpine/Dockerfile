FROM ruby:2.7-alpine

LABEL org.opencontainers.image.authors="dev@iloveyatoo.com"

## Install Requirements
RUN apk add --no-cache \
	jq \
	git \
	zlib \
	zlib-dev \
	yaml-dev \
	openssl-dev \
	gdbm-dev \
	readline-dev \
	ncurses-dev \
	libffi-dev \
	libxml2-dev \
	libxslt-dev \
	curl \
	curl-dev \
	icu-dev \
	graphviz \
	mariadb-connector-c-dev \
	postgresql-dev \
	sqlite-dev \
	musl-locales \
	tzdata \
	iputils \
	coreutils \
	build-base \
	shared-mime-info

## Install Bundler
RUN gem install bundler -v 2.2.19

## Create Workdir
RUN mkdir -p /app
WORKDIR /app

## Move Assets
COPY src/Gemfile /app/
COPY src/lib/gemfile_helper.rb /app/lib/
COPY src/vendor/gems/ /app/vendor/gems/
COPY Gemfile.lock /app/

## Bundle Install
RUN RAILS_ENV=production APP_SECRET_TOKEN=secret DATABASE_ADAPTER=mysql2 ON_HEROKU=true bundle install --without test development --path vendor/bundle -j $(nproc)
