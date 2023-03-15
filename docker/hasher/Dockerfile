################################################################################
#      Copyright (C) 2020        Sebastian Francisco Colomar Bauza             #
#      SPDX-License-Identifier:  GPL-2.0-only                                  #
################################################################################
ARG                                                                            \
  digest="@sha256:df559e1eb3c1b4884a28caa43ce163425a7f81cf9b7372d33883cf0fea67303f"
ARG                                                                            \
  image="ruby"
ARG                                                                            \
  tag="3.0.0-alpine3.12"
################################################################################
FROM                                                                           \
  ${image}:${tag}${digest}                                                     \
  AS                                                                           \
  multilayer
ARG                                                                            \
  dir=/app
ARG                                                                            \
  src=hasher.rb
RUN                                                                            \
  apk add --update build-base                                                  \
  &&                                                                           \
  gem install sinatra                                                          \
  &&                                                                           \
  gem install thin                                                             \
                                                                               ;
WORKDIR                                                                        \
  ${dir}
COPY                                                                           \
  ${src}                                                                       \
  script
################################################################################
FROM                                                                           \
  scratch                                                                      \
  AS                                                                           \
  production
ARG                                                                            \
  dir=/app
COPY                                                                           \
  --from=multilayer                                                            \
    /                                                                          \
    /
WORKDIR                                                                        \
  ${dir}
################################################################################
CMD                                                                            \
  ["script"]
ENTRYPOINT                                                                     \
  ["ruby"]
ENV                                                                            \
  GEM_HOME                                                                     \
  /usr/local/bundle
ENV                                                                            \
  PATH                                                                         \
  ${GEM_HOME}/bin:${PATH}
EXPOSE                                                                         \
  8080
################################################################################
