# Use the official ASP.NET Core SDK image as the build environment
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

# Set working directory
WORKDIR /app

# Copy the project file and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the entire project and build the application
COPY . ./
RUN dotnet publish -c Release -o out

# Stage 2: Create a runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime

# Set working directory
WORKDIR /app

# Copy built files from the previous stage
COPY --from=build /app/out ./

# Expose port 80
EXPOSE 80

# Start the application
ENTRYPOINT ["dotnet", "payments-api.dll"]

