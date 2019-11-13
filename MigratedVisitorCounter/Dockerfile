FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["MigratedVisitorCounter/MigratedVisitorCounter.csproj", "MigratedVisitorCounter/"]
RUN dotnet restore "MigratedVisitorCounter/MigratedVisitorCounter.csproj"
COPY . .
WORKDIR "/src/MigratedVisitorCounter"
RUN dotnet build "MigratedVisitorCounter.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MigratedVisitorCounter.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MigratedVisitorCounter.dll"]