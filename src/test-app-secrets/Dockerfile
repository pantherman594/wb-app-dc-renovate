FROM python:3-slim@sha256:51dafde81dbdb6ebde285137a295cf18a47ca95234fe388a343719cb97305b3d

RUN pip install --no-cache-dir pyyaml

COPY --from=wb-secret-receiver /dist/wb-secret-receiver /wb-secret-receiver
