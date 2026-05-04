FROM mcr.microsoft.com/dotnet/sdk:8.0 AS builder
WORKDIR /app

COPY . .

RUN dotnet publish -c Release -p:PublishProfile=FolderProfile -o /app/published DevOpsProject/DevOpsProject.CommunicationControl.API.csproj

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runner
WORKDIR /app

RUN groupadd --gid 1000 appuser && \  
    useradd --uid 1000 --gid appuser --shell /bin/bash --create-home appuser  

COPY --from=builder --chown=appuser:appuser /app/published ./

USER appuser

EXPOSE 8080

ENTRYPOINT ["dotnet", "DevOpsProject.CommunicationControl.API.dll"]