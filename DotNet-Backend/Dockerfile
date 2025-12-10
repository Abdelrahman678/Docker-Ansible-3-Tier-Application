# ----- Stage 1: Build -----
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS builder

# Set working directory inside container
WORKDIR /app

# Copy csproj and restore dependencies
COPY API.csproj .
RUN dotnet restore

# Copy the full source code
COPY . .

# Publish the application
RUN dotnet publish -c Release -o /app/publish --no-restore

# ----- Stage 2: Runtime -----
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

# Set working directory inside container
WORKDIR /app

# Copy published DLLs from the builder stage
COPY --from=builder /app/publish .

# Entry point for the application
ENTRYPOINT ["dotnet", "API.dll"]