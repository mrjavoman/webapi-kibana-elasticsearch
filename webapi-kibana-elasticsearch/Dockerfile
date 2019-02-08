FROM microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk-stretch AS build
WORKDIR /src
COPY ["webapi-kibana-elasticsearch/webapi-kibana-elasticsearch.csproj", "webapi-kibana-elasticsearch/"]
RUN dotnet restore "webapi-kibana-elasticsearch/webapi-kibana-elasticsearch.csproj"
COPY . .
WORKDIR "/src/webapi-kibana-elasticsearch"
RUN dotnet build "webapi-kibana-elasticsearch.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "webapi-kibana-elasticsearch.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "webapi-kibana-elasticsearch.dll"]