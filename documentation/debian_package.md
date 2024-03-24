# Debian Package Manual build

[Return to README](../README.md)

utilizes chris boddy's basic work with pybuild via debhelper  
debhelper needs some files: changelog, control, copyright, rules
correct handling of versions requires commits for changes, don't remember where prolly changelog
if everything in the debian folder is left as it is building works as follows:

clone source into a seperate folder containing the full folder (buildung will output to parent directory of the repository) and change into project folder
<br>
<br>
install the dependencies for the build.
```
sudo apt-get install -y dpkg-dev devscripts debhelper-compat dh-python python3-setuptools python3-all
```

build the package
```
debuild --no-tgz-check -us -uc
```

you can verify the build success by running:
```
dpkg-deb --info ../i3-workspace-names-daemon_0.15.0-1_amd64.deb
```

<details>
<summary>if no changes to any build related files in the <code>debian/</code> folder have been made, this should yield the following contents (klick to uncollapse):</summary>

```
new Debian package, version 2.0.
size 25190 bytes: control archive=1150 bytes.
    525 bytes,    13 lines      control
   1138 bytes,    11 lines      md5sums
    297 bytes,    12 lines   *  postinst             #!/bin/sh
    441 bytes,    12 lines   *  prerm                #!/bin/sh
Package: i3-workspace-names-daemon
Version: 0.15.0-1
Architecture: amd64
Maintainer: Floyd Otsoko <floydotsoko@gmx.net>
Installed-Size: 103
Depends: python3-i3ipc, python3:any, dh-python
Suggests: fonts-font-awesome
Section: python
Priority: optional
Homepage: https://github.com/i3-workspace-names-daemon/i3-workspace-names-daemon
Description: Description: Rename i3 workspaces dynamically
  Dynamically update the name of each i3wm workspace using font-awesome icons
  or the names of applications running in each workspace.
```
</details>
<br>

if no changes at all have been made to the source, you by comparing the checksums download `.md5` file from [latest release](https://github.com/CastixGitHub/i3-workspace-names-daemon/releases/latest) and copy into to the folder of the built `.deb` file and run:
`md5sum -c *.md5`