FROM python:3-slim@sha256:cad9a2c871761c413caa6fdd6441c783451e740a48aaeba60ae62a8b53525ef6

RUN pip install --no-cache-dir pyyaml

COPY --from=wb-secret-receiver /dist/wb-secret-receiver /wb-secret-receiver
