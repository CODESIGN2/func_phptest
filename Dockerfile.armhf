FROM arm32v7/php:7
#Build PHP Package
RUN apt-get update -qqy && apt-get install -qqy wget git ca-certificates unzip && \
    wget -qO /bin/composer https://getcomposer.org/composer.phar && \
    chmod +x /bin/composer

COPY . /tmp/build

WORKDIR /tmp/build

RUN composer update && php vendor/bin/phpunit

FROM arm32v7/php:7
#Package From Build To Slim Down Release

RUN echo "Pulling watchdog binary from Github." && \
curl -sSL https://github.com/openfaas/faas/releases/download/0.6.5/fwatchdog-armhf > /usr/bin/fwatchdog && \
chmod +x /usr/bin/fwatchdog

# Add non root user
RUN adduser --system app
RUN mkdir -p /home/app
RUN chown app /home/app

WORKDIR /home/app

COPY --from=0 /tmp/build .

USER app

ENV fprocess="php app.php"

CMD ["fwatchdog"]
