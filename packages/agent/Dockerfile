FROM --platform=linux/amd64 debian:12.11-slim

ARG GIT_SHA
ARG MEDPLUM_VERSION

ENV GIT_SHA ${GIT_SHA}
ENV MEDPLUM_VERSION ${MEDPLUM_VERSION}
ENV MEDPLUM_LOG_LEVEL=${MEDPLUM_LOG_LEVEL:-"INFO"}

COPY medplum-agent-${MEDPLUM_VERSION}-linux /srv/medplum-agent

RUN apt-get update && \
    apt-get install -y iputils-ping && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    adduser -u 5678 --disabled-password --gecos "" app && \
    chmod +x /srv/medplum-agent

WORKDIR /srv

USER app

CMD ./medplum-agent "$MEDPLUM_BASE_URL" "$MEDPLUM_CLIENT_ID" "$MEDPLUM_CLIENT_SECRET" "$MEDPLUM_AGENT_ID" "$MEDPLUM_LOG_LEVEL"
