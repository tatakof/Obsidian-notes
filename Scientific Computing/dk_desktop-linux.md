from https://docs.docker.com/desktop/linux/

1.  Set up the [Docker repository](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository).
2.  Download and install the Debian package. If you have previously installed one of the preview releases, we recommend that you run `sudo apt remove docker-desktop`:
    
    ```
     # 1.
     $ curl https://desktop-stage.docker.com/linux/main/amd64/76787/docker-desktop.deb --output docker-desktop.deb
     # remove previously installed releases
     $ sudo apt remove docker-desktop
     # 2. Download and install the Debian package
     $ sudo apt install ./docker-desktop.deb
    ```
    