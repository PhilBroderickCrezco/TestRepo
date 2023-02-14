FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["AzureDevOpsMigrationTest/AzureDevOpsMigrationTest.csproj", "AzureDevOpsMigrationTest/"]
RUN dotnet restore "AzureDevOpsMigrationTest/AzureDevOpsMigrationTest.csproj"
COPY . .
WORKDIR "/src/AzureDevOpsMigrationTest"
RUN dotnet build "AzureDevOpsMigrationTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AzureDevOpsMigrationTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AzureDevOpsMigrationTest.dll"]
