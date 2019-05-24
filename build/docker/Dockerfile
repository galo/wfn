FROM ubuntu

RUN mkdir -p /home/app

RUN apt-get update && apt-get install -y curl \
    ca-certificates \
    && echo "Pulling watchdog binary from Github." \
    && curl -sSL https://github.com/openfaas/faas/releases/download/0.13.0/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog \
    && cp /usr/bin/fwatchdog /home/app 
    

# Add non root user
RUN addgroup --system app && adduser -system -group app

RUN chown app /home/app

WORKDIR /home/app

USER app

# Install wasmer and wapm
RUN curl https://get.wasmer.io -sSfL | sh 

ENV WASMER_DIR="/home/app/.wasmer"
ENV WASMER_CACHE_DIR="$WASMER_DIR/cache"
ENV PATH="$WASMER_DIR/bin:$WASMER_DIR/globals/wapm_packages/.bin:$PATH"

# Install the applpication
RUN wapm install cowsay

# Populate example here - i.e. "cat", "sha512sum" or "node index.js"
ENV fprocess="wapm run cowsay  "
# Set to true to see request in function logs
ENV write_debug="false"

EXPOSE 8080

HEALTHCHECK --interval=3s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]
