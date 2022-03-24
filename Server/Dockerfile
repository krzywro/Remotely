FROM mcr.microsoft.com/dotnet/aspnet:6.0-bullseye-slim

EXPOSE 5000

ENV ASPNETCORE_ENVIRONMENT="Production"
ENV ASPNETCORE_URLS="http://*:5000"

COPY bin/Release/net6.0/publish /var/www/remotely
COPY DockerMain.sh /

RUN \
  adduser --disabled-password --gecos '' -u 2001 remotely && \
  mkdir /config && \
  mkdir -p /remotely-data && \
  sed -i 's/DataSource=Remotely.db/DataSource=\/remotely-data\/Remotely.db/' /var/www/remotely/appsettings.json && \
  chown -R remotely:remotely /remotely-data && \
  chown -R remotely:remotely /var/www/remotely && \
  chmod 755 /DockerMain.sh

VOLUME "/remotely-data"

WORKDIR /var/www/remotely

USER remotely

ENTRYPOINT ["/DockerMain.sh"]
