# Windows docker images for the .NET SDK in x86

This repo aims to fill a gap in the [official Docker images](https://hub.docker.com/_/microsoft-dotnet-sdk/) created by Microsoft and provide a x86 SDK.

## Disclaimer

Images are published to ghcr.io/smkanadl/sdk. Use at your own risk!

## Problems

All images are based on the windowsservercore images as the nanoserver images are not capable of running native x86 binaries. https://github.com/microsoft/Windows-Containers/issues/118
