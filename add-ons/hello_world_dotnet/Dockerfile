FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine

COPY ./*.cs /src/
COPY ./*.csproj /src/

WORKDIR /src
RUN dotnet restore \
  -r linux-musl-x64
  
RUN dotnet publish \
  --no-restore \
  -r linux-musl-x64 \
  --self-contained true \
  -c Release \
  -o /app
  
ENV \
  # Listen on port 8050
  ASPNETCORE_URLS=http://+:8050 \
  # Indicate we're running in a container
  DOTNET_RUNNING_IN_CONTAINER=true \
  # Enable polling mode for file watchers to pickup changes to secrets, infra.xml, etc.
  DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false \
  LC_ALL=en_US.UTF-8 \
  LANG=en_US.UTF-8 \
  # Disable diagnostics to avoid .NET needing write access to /tmp
  COMPlus_EnableDiagnostics=0
  
EXPOSE 8050
ENTRYPOINT ["/app/HelloWorld"]
