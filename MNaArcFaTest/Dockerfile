
# See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.


FROM mcr.microsoft.com/azure-functions/dotnet:3.0 AS base

WORKDIR /app
EXPOSE 80


FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["MNaArcFaTest.csproj", ""]

RUN dotnet restore "./MNaArcFaTest.csproj"
COPY. .
WORKDIR "/src/."


# install System.Drawing native dependencies



RUN dotnet build "MNaArcFaTest.csproj" -c Release -o /app/build


FROM build AS publish
RUN dotnet publish "MNaArcFaTest.csproj" -c Release -o /app/publish


FROM base AS final
WORKDIR /app

COPY --from=publish /app/publish .
ENV AzureWebJobsScriptRoot=/app














