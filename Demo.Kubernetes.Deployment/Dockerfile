FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
#COPY ["Demo.Kubernetes.Deployment/Demo.Kubernetes.Deployment.csproj", "Demo.Kubernetes.Deployment/"]
COPY . "Demo.Kubernetes.Deployment/"

RUN dotnet restore "Demo.Kubernetes.Deployment/Demo.Kubernetes.Deployment.csproj"
COPY . .
WORKDIR "/src/Demo.Kubernetes.Deployment"
RUN dotnet build "Demo.Kubernetes.Deployment.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Demo.Kubernetes.Deployment.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Demo.Kubernetes.Deployment.dll"]