# Flatpak hello example
=======================


## 1. Install Flatpak

```
$ sudo dnf install flatpak
```


## 2. Install a runtime

```
$ wget https://sdk.gnome.org/keys/gnome-sdk.gpg
$ flatpak remote-add --gpg-import=gnome-sdk.gpg gnome https://sdk.gnome.org/repo/
$ flatpak install gnome org.gnome.Platform 3.20
```

## 3. Create your app
```
$ mkdir hello
$ mkdir hello/files
$ mkdir hello/files/bin
$ mkdir hello/export
```

`hello/files/bin/hello.sh`:

```
#!/bin/sh
echo "Hello world, from a sandbox"
```

`hello/metadata`

```
[Application]
name=org.test.Hello
runtime=org.gnome.Platform/x86_64/3.20
command=hello.sh
```


## 4. Put the app in a repository

```
$ flatpak build-export repo hello
```


## 5. Install

```
$ flatpak --user remote-add --no-gpg-verify tutorial-repo repo
$ flatpak --user install tutorial-repo org.test.Hello
```


## 6. Run

```
$ flatpak run org.test.Hello
```

    Hello world, from a sandbox

