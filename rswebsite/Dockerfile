#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["rswebsite/rswebsite.csproj", "rswebsite/"]
RUN dotnet restore "rswebsite/rswebsite.csproj"
COPY . .
WORKDIR "/src/rswebsite"
RUN dotnet build "rswebsite.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "rswebsite.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "rswebsite.dll"]