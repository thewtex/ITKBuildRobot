FROM microsoft/windowsservercore:10.0.14393.1944

RUN @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

RUN powershell -NoProfile -InputFormat None -Command \
  choco install git ninja cmake jdk8 vcbuildtools python -y

# https://github.com/moby/moby/issues/22017
# https://github.com/moby/moby/issues/30033
RUN powershell -command "[Environment]::SetEnvironmentVariable('Path', $env:Path + ';C:\Program Files\CMake\bin', [EnvironmentVariableTarget]::Machine)"

SHELL ["cmd.exe", "/s", "/c"]

# Use shell form to start developer command prompt and any other commands specified
ENTRYPOINT C:\"Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\Tools\VsDevCmd.bat" -arch=amd64&set &&

# Default to console running within developer command prompt environment
CMD ["cmd.exe"]
