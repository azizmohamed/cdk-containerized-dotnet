FROM mcr.microsoft.com/dotnet/aspnet:5.0-focal AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:5.0-focal AS build
WORKDIR /CdkApp
COPY ["CdkApp.csproj", "CdkApp/"]
RUN dotnet restore "CdkApp/CdkApp.csproj"
COPY . ./CdkApp
WORKDIR "/CdkApp/CdkApp"
RUN dotnet build "CdkApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CdkApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CdkApp.dll"]

