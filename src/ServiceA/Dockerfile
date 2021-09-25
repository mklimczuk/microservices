#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Microservices.ServiceA/Microservices.ServiceA.csproj", "Microservices.ServiceA/"]
RUN dotnet restore "Microservices.ServiceA/Microservices.ServiceA.csproj"
COPY . .
WORKDIR "/src/Microservices.ServiceA"
RUN dotnet build "Microservices.ServiceA.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Microservices.ServiceA.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Microservices.ServiceA.dll"]