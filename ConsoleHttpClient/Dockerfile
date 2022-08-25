FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ConsoleHttpClient/ConsoleHttpClient.csproj", "ConsoleHttpClient/"]
RUN dotnet restore "ConsoleHttpClient/ConsoleHttpClient.csproj"
COPY . .
WORKDIR "/src/ConsoleHttpClient"
RUN dotnet build "ConsoleHttpClient.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsoleHttpClient.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleHttpClient.dll"]
