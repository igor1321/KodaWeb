FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["KodaWeb/KodaWeb.csproj", "KodaWeb/"]
RUN dotnet restore "KodaWeb/KodaWeb.csproj"
COPY . .
WORKDIR "/src/KodaWeb"
RUN dotnet build "KodaWeb.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KodaWeb.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "KodaWeb.dll"]
