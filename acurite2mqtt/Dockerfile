ARG BUILD_FROM
FROM ${BUILD_FROM}

# Environment variables
ENV MQTT_HOST=127.0.0.1 \
    MQTT_PORT=1883 \
    MQTT_USERNAME="" \
    MQTT_PASSWORD="" \
    MQTT_RETAIN=True \
    MQTT_TOPIC=rtl_433 \
    PROTOCOL="" \
    WHITELIST_ENABLE=False \
    EXPIRE_AFTER=0 \
    WHITELIST="" \
    DISCOVERY_PREFIX=homeassistant \
    DISCOVERY_INTERVAL=600 \
    AUTO_DISCOVERY=True \
    DEBUG=False \
    LANG=C.UTF-8

LABEL maintainer="Jeffrey Stone - Peto" \
      description="RTL433 to Home Assistant via MQTT"

WORKDIR /data

# Copy scripts
COPY entry.sh rtl_433_mqtt_hass.py /scripts/

# Build rtl_433 from source and install dependencies
RUN apk add --no-cache git build-base cmake libusb-dev librtlsdr-dev mosquitto-clients python3 py3-pip \
    && git clone https://github.com/merbanan/rtl_433.git /tmp/rtl_433 \
    && cd /tmp/rtl_433 && mkdir build && cd build \
    && cmake .. && make && make install \
    && rm -rf /tmp/rtl_433 \
    && pip3 install paho-mqtt \
    && chmod +x /scripts/entry.sh /scripts/rtl_433_mqtt_hass.py

# Entrypoint
ENTRYPOINT [ "/scripts/entry.sh" ]
