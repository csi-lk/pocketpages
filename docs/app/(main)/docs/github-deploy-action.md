#

```yaml
on:
  workflow_dispatch:
  push:
    branches:
      - main
name: Deploy website on push
jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest
    steps:
      - name: Get latest code
        uses: actions/checkout@v4

      - name: Sync files
        uses: SamKirkland/FTP-Deploy-Action@v4.3.5
        with:
          security: strict
          protocol: ftps
          server: ${{ secrets.ftp_server }}
          port: ${{ secrets.ftp_port }}
          username: ${{ secrets.ftp_username }}
          password: ${{ secrets.ftp_password }}
          local-dir: ./app/
          server-dir: ./makerlist/
          log-level: verbose
          state-name: pb_hooks/.ftp-deploy-sync-state.json
          exclude: |
            **/.git*
            **/.git*/**
            **/node_modules/**
            .gitignore
            LICENSE
            README.md
```