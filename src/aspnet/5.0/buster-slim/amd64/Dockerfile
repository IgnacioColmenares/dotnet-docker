ARG REPO=mcr.microsoft.com/dotnet/runtime

# Installer image
FROM amd64/buildpack-deps:buster-curl as installer

# Retrieve ASP.NET Core
RUN curl -fSL --output aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/5.0.13/aspnetcore-runtime-5.0.13-linux-x64.tar.gz \
    && aspnetcore_sha512='d3014d473b3bef0a9645908c768f1c458c53ebfd3ed6f2fd259b2921a6d7401f3c0403e99c0d80a6457ecc229dcf828a4031e17868538d831ae1394bb8aa0ad4' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && tar -ozxf aspnetcore.tar.gz ./shared/Microsoft.AspNetCore.App \
    && rm aspnetcore.tar.gz


# ASP.NET Core image
FROM $REPO:5.0.13-buster-slim-amd64

ENV ASPNET_VERSION=5.0.13

COPY --from=installer ["/shared/Microsoft.AspNetCore.App", "/usr/share/dotnet/shared/Microsoft.AspNetCore.App"]
