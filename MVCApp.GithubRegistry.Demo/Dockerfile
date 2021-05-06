#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["MVCApp.GithubRegistry.Demo/MVCApp.GithubRegistry.Demo.csproj", "MVCApp.GithubRegistry.Demo/"]
RUN dotnet restore "MVCApp.GithubRegistry.Demo/MVCApp.GithubRegistry.Demo.csproj"
COPY . .
WORKDIR "/src/MVCApp.GithubRegistry.Demo"
RUN dotnet build "MVCApp.GithubRegistry.Demo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MVCApp.GithubRegistry.Demo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MVCApp.GithubRegistry.Demo.dll"]