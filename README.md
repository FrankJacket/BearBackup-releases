# Ursavault - downloads

<p align="center"><img src="Ursavault.svg" alt="Ursavault: a cartoon bear putting folders into a safe" width="600"></p>

Backup solution for Windows PCs: a server (Docker, web interface) and an agent on each PC. This repository only hosts the **downloads**.

## Windows agent
1. Download `Ursavault-Agent-<version>-win-x64.zip` from the [latest release](../../releases/latest).
2. Check it against `SHA256SUMS.txt`:

       Get-FileHash .\Ursavault-Agent-<version>-win-x64.zip -Algorithm SHA256

3. Unzip it, then run in an elevated PowerShell:

       .\Install-Agent.ps1 -ServerUrl http://<server>:5080 -EnrollmentKey '<key>'

To remove it: `.\Uninstall-Agent.ps1`.

The programs are not code-signed, so Windows SmartScreen may show a warning on first run ("More info" > "Run anyway").

## Server (Docker)

    docker run -d --name ursavault --restart unless-stopped -p 5080:5080 \
      -e EnrollmentKey=<long random value> -e TZ=America/Toronto \
      -v bearbackup-data:/data ghcr.io/frankjacket/ursavault-server:latest

Open `http://<docker host>:5080`. Use the same enrollment key on the agents. Outside a trusted network, put a reverse proxy with HTTPS in front of the container.

## License
Apache License 2.0, see [LICENSE](LICENSE).
