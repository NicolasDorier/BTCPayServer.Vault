# Build system

The process to publish a new version is the following:
1. Bump `BTCPayServer.Vault/Version.csproj` version
2. Commit and push
3. Run `Build/push-new-tag.ps1`
4. Run `build.ps1`
5. Create a new release on github and upload all files in `dist/` there

The build system relies on docker to build the packages. 
Each dockerfile in `<rid>/Dockerfile` will generate a docker image with the package in it.

## How to test Debian

The debian package is easy to test, run:

```bash
docker run --rm --name ubuntu-desktop -p 6080:80 dorowu/ubuntu-desktop-lxde-vnc
```

This will create a linux container with a desktop you can access on http://localhost:6080/
You can then copy the debian package to the vm with

```bash
docker cp ../dist ubuntu-desktop:/root/
```

Then in the terminal inside the ubuntu desktop run

```bash
dpkg -i *.deb
```
