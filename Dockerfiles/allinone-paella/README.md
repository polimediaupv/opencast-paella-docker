# Opencast Docker allinone image with paella bundle

Those docker images are based in the official [opencast docker images](https://hub.docker.com/r/opencast/), but with the [paella-bundle](https://github.com/polimediaupv/paella-matterhorn) addition.


## Introduction

This repository holds `Dockerfiles`

## Usage

Those images extends the official opencast images to add the paella bundle. So, to use them you needs to follow the official instrctions, but replace the `presentation` container with the equivalent with the paella bundle.

## Images

| Official image  | Replaced by (with paella bundle) |
| ------------- | ------------- |
| [opencast/allinone](https://hub.docker.com/r/opencast/allinone/)  | [polimediaupv/opencast-allinone-paella](https://hub.docker.com/r/polimediaupv/opencast-allinone-paella/)  |
| [opencast/presentation](https://hub.docker.com/r/opencast/presentation/)  | [polimediaupv/opencast-presentation-paella](https://hub.docker.com/r/polimediaupv/opencast-presentation-paella/)  |
| [opencast/adminpresentation](https://hub.docker.com/r/opencast/adminpresentation/)  | [polimediaupv/opencast-adminpresentation-paella](https://hub.docker.com/r/polimediaupv/opencast-adminpresentation-paella/)  |

