# escape=`

# Installer image
FROM mcr.microsoft.com/windows/servercore:ltsc2022-amd64 AS installer

RUN powershell -Command `
        $ErrorActionPreference = 'Stop'; `
        $ProgressPreference = 'SilentlyContinue'; `
        Invoke-WebRequest `
            -UseBasicParsing `
            -Uri https://dot.net/v1/dotnet-install.ps1 `
            -OutFile dotnet-install.ps1; `
        ./dotnet-install.ps1 `
            -InstallDir '\Program Files (x86)\dotnet' `
            -Architecture x86 `
            -Channel 9.0.3xx; `
        Remove-Item -Force dotnet-install.ps1

# SDK/runtime image
# We currently have to use servercore as nanoserver is ONLY AMD64 and does not support x86 execution #https://github.com/microsoft/Windows-Containers/issues/118
FROM mcr.microsoft.com/windows/servercore:ltsc2022-amd64
LABEL org.opencontainers.image.source="https://github.com/smkanadl/dotnet-docker-x86"

ENV `
    # Enable detection of running in a container
    DOTNET_RUNNING_IN_CONTAINER=true `
    # .NET Runtime version
    DOTNET_VERSION=9.0.7 `
    # Do not generate certificate
    DOTNET_GENERATE_ASPNET_CERTIFICATE=false `
    # Do not show first run text
    DOTNET_NOLOGO=true `
    # SDK version
    DOTNET_SDK_VERSION=9.0.302 `
    # Enable correct mode for dotnet watch (only mode supported in a container)
    DOTNET_USE_POLLING_FILE_WATCHER=true `
    # Skip extraction of XML docs - generally not useful within an image/container - helps performance
    NUGET_XMLDOC_MODE=skip

# In order to set system PATH, ContainerAdministrator must be used
USER ContainerAdministrator
RUN setx /M PATH "%PATH%;C:\Program Files (x86)\dotnet"
USER ContainerUser

COPY --from=installer ["/Program Files (x86)/dotnet", "/Program Files (x86)/dotnet"]
