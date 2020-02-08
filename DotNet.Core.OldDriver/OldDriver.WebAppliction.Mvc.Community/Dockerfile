#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["OldDriver.WebAppliction.Mvc.Community/OldDriver.WebAppliction.Mvc.Community.csproj", "OldDriver.WebAppliction.Mvc.Community/"]
RUN dotnet restore "OldDriver.WebAppliction.Mvc.Community/OldDriver.WebAppliction.Mvc.Community.csproj"
COPY . .
WORKDIR "/src/OldDriver.WebAppliction.Mvc.Community"
RUN dotnet build "OldDriver.WebAppliction.Mvc.Community.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OldDriver.WebAppliction.Mvc.Community.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OldDriver.WebAppliction.Mvc.Community.dll"]