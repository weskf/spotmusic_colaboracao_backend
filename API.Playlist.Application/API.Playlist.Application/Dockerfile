#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["API.Playlist.Application/API.Playlist.Application.csproj", "API.Playlist.Application/"]
RUN dotnet restore "API.Playlist.Application/API.Playlist.Application.csproj"
COPY . .
WORKDIR "/src/API.Playlist.Application"
RUN dotnet build "API.Playlist.Application.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "API.Playlist.Application.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "API.Playlist.Application.dll"]