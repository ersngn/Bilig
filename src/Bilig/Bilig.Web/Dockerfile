FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Bilig.Web/Bilig.Web.csproj", "Bilig.Web/"]
RUN dotnet restore "Bilig.Web/Bilig.Web.csproj"
COPY . .
WORKDIR "/src/Bilig.Web"
RUN dotnet build "Bilig.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Bilig.Web.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Bilig.Web.dll"]
