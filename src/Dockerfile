FROM python:3.11-slim

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    DBT_HOME=/usr/app/dbt \
    DBT_PROFILES_DIR=/usr/app/dbt

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    ssh-client \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

WORKDIR $DBT_HOME


RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir dbt-core dbt-postgres

COPY dbt_project.yml profiles.yml packages.yml* ./
COPY models/ ./models/
COPY macros/ ./macros/
COPY seeds/ ./seeds/
COPY tests/ ./tests/


RUN dbt deps


CMD ["dbt", "run"]
