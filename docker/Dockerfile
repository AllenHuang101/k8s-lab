FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY aspnetcorek8s.csproj .
RUN dotnet restore "aspnetcorek8s.csproj"
COPY . .
RUN dotnet build "aspnetcorek8s.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnetcorek8s.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnetcorek8s.dll"]