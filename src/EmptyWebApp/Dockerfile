#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["EmptyWebApp/EmptyWebApp.csproj", "EmptyWebApp/"]
RUN dotnet restore "EmptyWebApp/EmptyWebApp.csproj"
COPY . .
WORKDIR "/src/EmptyWebApp"
RUN dotnet build "EmptyWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EmptyWebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EmptyWebApp.dll"]