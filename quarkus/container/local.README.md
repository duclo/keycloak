# Keycloak Image
For more information, see the [Running Keycloak in a container guide](https://www.keycloak.org/server/containers).

## Build the image

If your environment uses a custom CA, pass it as a BuildKit secret so the image can trust the Red Hat repositories during `dnf install`:

    docker build --secret id=somansa_root_ca,src=/usr/local/share/ca-certificates/somansa_root_ca.crt --build-arg KEYCLOAK_VERSION=<VERSION> -t <YOUR_TAG> .

It is possible to download the Keycloak distribution from GitHub:

    docker build --build-arg KEYCLOAK_VERSION=<VERSION> -t <YOUR_TAG> .

It is possible to download the Keycloak distribution from a URL:

    docker build --build-arg KEYCLOAK_DIST=http://<HOST>:<PORT>/keycloak-<VERSION>.tar.gz -t <YOUR_TAG> .

Alternatively, you need to build the local distribution first, then copy the distributions tar package in the `container` folder and point the build command to use the image:

    cp $KEYCLOAK_SOURCE/quarkus/dist/target/keycloak-<VERSION>.tar.gz .
    docker build --build-arg KEYCLOAK_DIST=keycloak-<VERSION>.tar.gz -t <YOUR_TAG> .
