# Police accountability data, served as a queryable SQLite database.
#
# The published CSVs (https://github.com/copious-git/police-accountability-data)
# are convenient to download and awkward to query. This image loads all nine into
# one SQLite database and serves them through Datasette, which gives you a
# browsable UI, a read-only SQL console and a JSON API over the same data.
#
#   docker run -p 8001:8001 copiousltd/police-accountability-data
#   open http://localhost:8001
#
# Build from the REPOSITORY ROOT so the CSVs are read from data/ directly. Copying them
# into docker/ would give the repo two copies of the same data, free to drift apart:
#   docker build -f docker/Dockerfile -t copiousltd/police-accountability-data .
#
# Data: CC BY 4.0. Sources and method: METHOD.md in the repository.
FROM python:3.12-slim

RUN pip install --no-cache-dir setuptools==75.6.0 datasette==0.65.1 sqlite-utils==3.38

WORKDIR /data
COPY data/ /tmp/csv/
COPY docker/metadata.json /data/metadata.json

# Build the database at image-build time so the container starts instantly and
# is byte-identical wherever it runs.
RUN set -eu; \
    for f in $(find /tmp/csv -name "*.csv"); do \
      table=$(basename "$f" .csv | tr '-' '_'); \
      sqlite-utils insert /data/police-accountability.db "$table" "$f" --csv --detect-types; \
    done; \
    rm -rf /tmp/csv

EXPOSE 8001
CMD ["datasette", "serve", "/data/police-accountability.db", \
     "--metadata", "/data/metadata.json", \
     "--host", "0.0.0.0", "--port", "8001"]
