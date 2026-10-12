FROM python:3-slim@sha256:a2b82f3c48559aa0a8446d9af49826b6e2b2016f4cd2afabfe6013ec53729170

RUN pip install --no-cache-dir pyyaml

COPY --from=wb-secret-receiver /dist/wb-secret-receiver /wb-secret-receiver
