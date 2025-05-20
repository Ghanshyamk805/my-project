FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["apiproject/Apiproject.csproj", "apiproject/"]
RUN dotnet restore "apiproject/Apiproject.csproj"
COPY . .
WORKDIR "/src/apiproject"
RUN dotnet build "Apiproject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Apiproject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Apiproject.dll"]