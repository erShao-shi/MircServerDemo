#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Zhaoxi.MicroService.ClientDemo/Zhaoxi.MicroService.ClientDemo.csproj", "Zhaoxi.MicroService.ClientDemo/"]
COPY ["Zhaoxi.MicroService.Service/Zhaoxi.MicroService.Service.csproj", "Zhaoxi.MicroService.Service/"]
COPY ["Zhaoxi.MicroService.Model/Zhaoxi.MicroService.Model.csproj", "Zhaoxi.MicroService.Model/"]
COPY ["Zhaoxi.MicroService.Interface/Zhaoxi.MicroService.Interface.csproj", "Zhaoxi.MicroService.Interface/"]
RUN dotnet restore "Zhaoxi.MicroService.ClientDemo/Zhaoxi.MicroService.ClientDemo.csproj"
COPY . .
WORKDIR "/src/Zhaoxi.MicroService.ClientDemo"
RUN dotnet build "Zhaoxi.MicroService.ClientDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Zhaoxi.MicroService.ClientDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Zhaoxi.MicroService.ClientDemo.dll"]