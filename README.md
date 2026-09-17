# Official configurations for the docker setup of TOLERANT Car
## The configurations for each released version can be found under tags

## Steps to use your own identity provider

-  Make sure, that you have configured your identity provider having a client with clientId and realm matching the values of **TOLERANT_CLIENT_ID** and **TOLERANT_REALM** in the .env file
-  Remove postgres and keycloak from the compose-secure.yml, this includes **services**, **volumes** and **depends_on** sections.
-  Remove the variables **INTERNAL_IDENTITY_PROVIDER_URL** and **INTERNAL_IDENTITY_PROVIDER_PORT** from the **proxy** service in the compose-secure.yml
-  Adjust **INTERNAL_IDENTITY_PROVIDER_URL** and **IDENTITY_PROVIDER_URL** in the .env file to the URL of your identity provider.
-  Remove the mount for the keycloak location from the **proxy** service in the compose-secure.yml

## Steps to use your own ssl certificate
-  Remove openssl from the compose-secure.yml, this includes **services**, **volumes_from** and **depends_on** sections.
-  Comment in the volumes of the proxy service for ssl certificates in the compose-secure.yml
-  Make sure that the ssl certificate and key are under the mounted directory's mentioned in step before
-  Make sure that the variables **CERT_FILENAME** and **CERT_PRIVATE_KEY_FILENAME** in the .env file match your filenames

## Steps to use without gui

### Without security
- Replace the mount for the default.conf.template file for **proxy** with a mount for the default.no.gui.conf.template file in the compose.yml
- Replace the mount for the common.loc.template file for **proxy** with a mount for the common.no.gui.loc.template file in the compose.yml
- Set **GUI_ENABLED** to false for the **backend** service in the compose.yml
- Remove gui from the compose.yml, this includes **services** and **depends_on** sections.

### With enabled security
- Replace the mount for the ssl.conf.template file for **proxy** with a mount for the ssl.no.gui.conf.template file in the compose-secure.yml
- Replace the mount for the common.loc.template file for **proxy** with a mount for the common.no.gui.loc.template file in the compose-secure.yml
- Set **GUI_ENABLED** to false for the **backend** service in the compose-secure.yml
- Remove gui from the compose-secure.yml, this includes **services** and **depends_on** sections.


## Usage

### Starting

**The services can be started using the following commands:**

Without security:

```sh
docker compose up -d
```

With enabled security:

```sh
docker compose -f compose-secure.yml up -d
```

The `docker compose` command should be executed from the directory containing the `compose.yml or compose-secure.yml` file.


### Stopping

**The running services can be stopped using the following commands:**

Without security:

```sh
docker compose down
```

With enabled security:

```sh
docker compose -f compose-secure.yml down
```


The `docker compose` command should be executed from the directory containing the `compose.yml or compose-secure.yml` file.