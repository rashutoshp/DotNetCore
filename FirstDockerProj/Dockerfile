FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["FirstDockerProj/FirstDockerProj.csproj", "FirstDockerProj/"]
RUN dotnet restore "FirstDockerProj/FirstDockerProj.csproj"
COPY . .
WORKDIR "/src/FirstDockerProj"
RUN dotnet build "FirstDockerProj.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FirstDockerProj.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FirstDockerProj.dll"]