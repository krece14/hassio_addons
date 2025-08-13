ARG BUILD_FROM
FROM ghcr.io/home-assistant/aarch64-base:3.18

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

RUN apk add --no-cache rtl-sdr rtl_433 libusb mosquitto-clients python3 py3-paho-mqtt \
    && chmod +x /scripts/entry.sh \
    && chmod +x /scripts/rtl_433_mqtt_hass.py

# Entrypoint
ENTRYPOINT [ "/scripts/entry.sh" ]
