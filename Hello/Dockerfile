FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY Hello/Hello.csproj Hello/
RUN dotnet restore Hello/Hello.csproj
COPY . .
WORKDIR /src/Hello
RUN dotnet build Hello.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Hello.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Hello.dll"]
