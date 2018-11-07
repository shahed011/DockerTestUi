FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 61600
EXPOSE 44384

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["DockerTestUi/DockerTestUi.csproj", "DockerTestUi/"]
RUN dotnet restore "DockerTestUi/DockerTestUi.csproj"
COPY . .
WORKDIR "/src/DockerTestUi"
RUN dotnet build "DockerTestUi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DockerTestUi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerTestUi.dll"]