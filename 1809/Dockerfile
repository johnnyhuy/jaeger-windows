# escape=`

ARG tag=1809

FROM mcr.microsoft.com/windows/servercore:$tag AS servercore

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ENV MHOLT_ARCHIVER_VERSION 2.0
ENV MHOLT_ARCHIVER_SHA256 c23eab86a8f77e446f2b5dbb03305ac9acfb5187108a0090a4bcb3d908fa9785

RUN [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; `
    Invoke-WebRequest $('https://github.com/mholt/archiver/releases/download/v{0}/archiver_windows_amd64.exe' -f $env:MHOLT_ARCHIVER_VERSION) -OutFile archiver.exe -UseBasicParsing; `
    if ((Get-FileHash archiver.exe -Algorithm sha256).Hash -ne $env:MHOLT_ARCHIVER_SHA256) { Write-Error 'SHA256 mismatch' }

ENV JAEGER_VERSION 1.11.0

RUN [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; `
    Invoke-WebRequest $('https://github.com/jaegertracing/jaeger/releases/download/v{0}/jaeger-{0}-windows-amd64.tar.gz' -f $env:JAEGER_VERSION) -OutFile 'jaeger.tar.gz' -UseBasicParsing
RUN .\archiver.exe open jaeger.tar.gz
RUN Rename-Item -Path $('C:\jaeger-{0}-windows-amd64' -f $env:JAEGER_VERSION) -NewName 'C:\jaeger-all-in-one'

FROM mcr.microsoft.com/windows/nanoserver:$tag

COPY --from=servercore /jaeger-all-in-one /jaeger-all-in-one

EXPOSE 5775/udp 6831/udp 6832/udp
EXPOSE 5778 16686 14268 9411

WORKDIR C:\jaeger-all-in-one
CMD ["jaeger-all-in-one.exe"]