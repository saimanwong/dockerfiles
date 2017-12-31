FROM ubuntu:14.04
LABEL maintainer "Sai Man Wong <saimanwong@protonmail.com>"

# Packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    libleveldb-dev \
    sqlite3 \
    libsqlite3-dev \
    libunwind8-dev \
    apt-transport-https \
    curl \
    gnupg \
    ca-certificates \
    git

# .NET core + Neo CLI
RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg && \
    mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg && \
    sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-trusty-prod trusty main" > /etc/apt/sources.list.d/dotnetdev.list' && \
    apt-get update && \
    apt-get install -y dotnet-sdk-2.0.0 && \
    git clone https://github.com/neo-project/neo-cli

WORKDIR neo-cli

RUN dotnet restore && \
    dotnet publish -c Release

ENTRYPOINT ["dotnet", "neo-cli/bin/Release/netcoreapp2.0/neo-cli.dll"]
