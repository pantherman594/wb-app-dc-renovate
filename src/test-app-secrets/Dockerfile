FROM python:3-slim@sha256:c3e521df8b2b498a7a682e7e18676771cb80c6b75b8699af886b2d554ce40151

RUN pip install --no-cache-dir pyyaml

COPY --from=wb-secret-receiver /dist/wb-secret-receiver /wb-secret-receiver
