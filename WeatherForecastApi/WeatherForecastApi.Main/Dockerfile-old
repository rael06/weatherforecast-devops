FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WeatherForecastApi.Main/WeatherForecastApi.Main.csproj", "WeatherForecastApi.Main/"]
RUN dotnet restore "WeatherForecastApi.Main/WeatherForecastApi.Main.csproj"
COPY . .
WORKDIR "/src/WeatherForecastApi.Main"
RUN dotnet build "WeatherForecastApi.Main.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WeatherForecastApi.Main.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WeatherForecastApi.Main.dll"]
