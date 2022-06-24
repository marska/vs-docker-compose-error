#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ConsoleApp00/ConsoleApp00.csproj", "ConsoleApp00/"]
RUN dotnet restore "ConsoleApp00/ConsoleApp00.csproj"
COPY . .
WORKDIR "/src/ConsoleApp00"
RUN dotnet build "ConsoleApp00.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsoleApp00.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleApp00.dll"]