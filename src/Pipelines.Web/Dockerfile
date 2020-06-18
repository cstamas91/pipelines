FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
ARG PREFIX
ARG SUFFIX
WORKDIR /app

COPY *.csproj ./
RUN dotnet restore

COPY . ./
RUN dotnet publish -c Release -o out /p:VersionPrefix=$PREFIX /p:VersionSuffix=$SUFFIX

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT [ "dotnet", "Pipelines.Web.dll" ]