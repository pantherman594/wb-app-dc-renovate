FROM us-west2-docker.pkg.dev/shared-pub-buckets-94mvrf/workbench-artifacts/app-workbench-jupyter:latest@sha256:93f9c4fda7088f051fec889f5ba16b1ad1940aeb417a93dbc636993eb7e184a7 

# Install jupyter extensions
RUN --mount=type=bind,from=jupyter-extension-builder,source=/dist,target=/tmp/extensions \
    /tmp/extensions/setup.sh

# Pre-install web framework and data visualization libraries
RUN pip install --no-cache-dir \
    fastapi uvicorn[standard] \
    flask flask-cors \
    plotly pandas boto3 psycopg2-binary
