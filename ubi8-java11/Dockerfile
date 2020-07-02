FROM registry.access.redhat.com/ubi8/ubi-minimal
LABEL base=ubi8 engine=jvm version=java11 timezone=UTC port=8080 dir=/opt/app user=app

RUN microdnf install java-11-openjdk-headless openssl hostname bash curl tzdata shadow-utils tar gzip && microdnf clean all
ENV JAVA_HOME=/usr/lib/jvm/jre-11

ENV TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

EXPOSE 8080

RUN mkdir -p /opt/app && ln -s /opt/app /lib && mkdir /opt/db-migrations && ln -s /opt/db-migrations /flyway

WORKDIR /opt/app

RUN groupadd --system --gid=1000 app\
    && useradd --system --no-log-init --gid app --uid=1000 app \
    && chown -R app:app /opt/app \
    && chown -R app:app /opt/db-migrations

USER app

