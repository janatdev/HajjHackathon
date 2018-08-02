FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY HajjHackathon/HajjHackathon.csproj HajjHackathon/
RUN dotnet restore HajjHackathon/HajjHackathon.csproj
COPY . .
WORKDIR /src/HajjHackathon
RUN dotnet build HajjHackathon.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish HajjHackathon.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HajjHackathon.dll"]
