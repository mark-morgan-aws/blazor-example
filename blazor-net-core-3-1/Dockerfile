#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY blazor-net-core-3-1/blazor-net-core-3-1.csproj blazor-net-core-3-1/
RUN dotnet restore "blazor-net-core-3-1/blazor-net-core-3-1.csproj"
COPY . .
WORKDIR "/src/blazor-net-core-3-1"
RUN dotnet build "blazor-net-core-3-1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "blazor-net-core-3-1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "blazor-net-core-3-1.dll"]
