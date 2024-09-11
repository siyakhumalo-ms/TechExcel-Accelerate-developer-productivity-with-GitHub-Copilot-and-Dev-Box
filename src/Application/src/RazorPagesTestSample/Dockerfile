# Use the official .NET 8 runtime as a parent image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app

# Set environment variable
ENV ASPNETCORE_HTTP_PORTS=80

# Use the SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["RazorPagesTestSample.csproj", "./"]
RUN dotnet restore "./RazorPagesTestSample.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "RazorPagesTestSample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RazorPagesTestSample.csproj" -c Release -o /app/publish

# Use the base image to run the app
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RazorPagesTestSample.dll"]