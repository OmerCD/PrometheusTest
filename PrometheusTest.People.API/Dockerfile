FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["PrometheusTest.People.API/PrometheusTest.People.API.csproj", "PrometheusTest.People.API/"]
RUN dotnet restore "PrometheusTest.People.API/PrometheusTest.People.API.csproj"
COPY . .
WORKDIR "/src/PrometheusTest.People.API"
RUN dotnet build "PrometheusTest.People.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PrometheusTest.People.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PrometheusTest.People.API.dll"]
