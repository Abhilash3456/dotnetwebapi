#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebApplication123/WebApplication123.csproj", "WebApplication123/"]
RUN dotnet restore "WebApplication123/WebApplication123.csproj"
COPY . .
WORKDIR "/src/WebApplication123"
RUN dotnet build "WebApplication123.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication123.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication123.dll"]