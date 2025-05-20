# Use the .NET SDK image
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /source

# Copy the .csproj and restore dependencies
COPY apiproject/*.csproj .
RUN dotnet restore

# Copy the entire project and build
COPY apiproject/. .
RUN dotnet publish -c Release -o /app

# Use the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Apiproject.dll"]