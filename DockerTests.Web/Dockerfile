FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 61516
EXPOSE 44377

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["DockerTests.Web/DockerTests.Web.csproj", "DockerTests.Web/"]
RUN dotnet restore "DockerTests.Web/DockerTests.Web.csproj"
COPY . .
WORKDIR "/src/DockerTests.Web"
RUN dotnet build "DockerTests.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DockerTests.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerTests.Web.dll"]