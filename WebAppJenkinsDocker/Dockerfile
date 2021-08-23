#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#FROM mcr.microsoft.com/dotnet/aspnet:2.1 AS base
#WORKDIR /app
#EXPOSE 80

#FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build
#WORKDIR /src
#COPY ["WebAppJenkinsDocker/WebAppJenkinsDocker.csproj", "WebAppJenkinsDocker/"]
#RUN dotnet restore "WebAppJenkinsDocker/WebAppJenkinsDocker.csproj"
#COPY . .
#WORKDIR "/src/WebAppJenkinsDocker"
#RUN dotnet build "WebAppJenkinsDocker.csproj" -c Release -o /app/build

#FROM build AS publish
#RUN dotnet publish "WebAppJenkinsDocker.csproj" -c Release -o /app/publish

#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "WebAppJenkinsDocker.dll"]

FROM microsoft/dotnet:2.2-sdk AS build-env 
WORKDIR /app

# Copy csproj and restore 
COPY *.csproj ./ 
RUN dotnet restore

# Copy everything else and build 
COPY . ./ 
RUN dotnet publish -c Release -o out

# Build runtime image 
FROM microsoft/dotnet:2.2-aspnetcore-runtime 
WORKDIR /app 
COPY — from=build-env /app/out . 
ENTRYPOINT [“dotnet”, “WebAppJenkinsDocker.dll”]
