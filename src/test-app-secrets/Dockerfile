FROM python:3-slim@sha256:8c13a3f37a6a5b71498228e902c4b9f51c1f7900d49fabf71f9a650c6120e0d0

RUN pip install --no-cache-dir pyyaml

COPY --from=wb-secret-receiver /dist/wb-secret-receiver /wb-secret-receiver
