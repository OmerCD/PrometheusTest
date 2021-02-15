FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["PrometheusTest.Location.API/PrometheusTest.Location.API.csproj", "PrometheusTest.Location.API/"]
RUN dotnet restore "PrometheusTest.Location.API/PrometheusTest.Location.API.csproj"
COPY . .
WORKDIR "/src/PrometheusTest.Location.API"
RUN dotnet build "PrometheusTest.Location.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PrometheusTest.Location.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PrometheusTest.Location.API.dll"]
