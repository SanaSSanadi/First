#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["AzureHandsonE1/AzureHandsonE1.csproj", "AzureHandsonE1/"]
RUN dotnet restore "AzureHandsonE1/AzureHandsonE1.csproj"
COPY . .
WORKDIR "/src/AzureHandsonE1"
RUN dotnet build "AzureHandsonE1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AzureHandsonE1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AzureHandsonE1.dll"]