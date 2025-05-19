# Windows docker images for the .NET SDK in x86

This repo aims to fill a gap in the [official Docker images](https://hub.docker.com/_/microsoft-dotnet-sdk/) created by Microsoft and provide a x86 SDK.

## Disclaimer

Images are published to ghcr.io/smkanadl/sdk. Use at your own risk! Dockerfiles are heavily inspired by the [official documentation](https://github.com/dotnet/dotnet-docker).

## Problems

Images for windows-2022 are based on the windowsservercore images as the nanoserver images are not capable of running native x86 binaries. https://github.com/microsoft/Windows-Containers/issues/118
Images for windows-2025 are now based on the nanoserver image using FoD to install WoW64. https://techcommunity.microsoft.com/blog/containers/discover-the-new-era-of-windows-server-2025-nano-server-containers/4413060
