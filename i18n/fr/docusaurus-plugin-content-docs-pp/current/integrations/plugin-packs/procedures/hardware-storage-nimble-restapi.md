---
id: hardware-storage-nimble-restapi
title: Nimble Storage Rest API
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Vue d'ensemble

HPE Nimble Storage est une technologie de solutions de stockage de données sur des baies Flash dont le siège est basé à San José en Californie. C'est une entité de Hewlett Packard Enterprise. 

Nimble Storage produit des solutions matérielles et logicielles pour le stockage de données en utilisant les protocoles
iSCSI et Fiber Channel. Des solutions de sauvegarde et de protection de données sont également disponibles.

## Contenu du connecteur de supervision

### Objets supervisés

* Nimble Flash Arrays (NimbleOS >=2.3.x)

### Services disponibles

Le connecteur de supervision Nimble SNMP offre les Services suivants:

* Arrays
* Hardware
* Volumes

### Métriques collectées

<Tabs groupId="sync">
<TabItem value="Arrays" label="Arrays">

| Metric name                            | Description (per array )        | Unit    |
| :------------------------------------- | :------------------------------ | :------ |
| status                                 | Array status                    | String  |
| array.space.usage.bytes                | Used space                      | Bytes   |
| array.space.usage.percentage           | Used space                      |   %     |
| array.space.free.bytes                 | Free space                      | Bytes   |
| array.snapshots.compression.rate.count | Snapshot compression ratio      |         |
| array.snapshots.reduction.rate.count   | Snapshot reduction ratio        |         |

</TabItem>
<TabItem value="Hardware" label="Hardware">

| Component name | Description (per array ) | Unit   |
|:---------------|:-------------------------|:-------|
| Disk           | Disk & RAID state        | String |
| Fan            | Fan state & speed        | rpm    |
| Power Supply   | Power Supply state       | String |
| Temperature    | Temperature state        | °C     |

</TabItem>
<TabItem value="Volumes" label="Volumes">

| Metric name                           | Description (per volume)         | Unit    |
| :------------------------------------ | :------------------------------- | :------ |
| status                                | Volume status                    | String  |
| volume.space.usage.bytes              | Space usage                      | Bytes   |
| volume.io.read.usage.bytespersecond   | Read I/O volume                  | Bytes/s |
| volume.io.write.usage.bytespersecond  | Write I/O volume                 | Bytes/s |
| volume.io.read.usage.iops             | Read IOPS count                  | Iops    |
| volume.io.write.usage.iops            | Write IOPS count                 | Iops    |
| volume.io.read.latency.milliseconds   | Read latency                     | ms      |
| volume.io.write.latency.milliseconds  | Write latency                    | ms      |

</TabItem>
</Tabs>

## Prérequis

### Configuration de la Nimble Rest API

L'équipement Nimble doit être joignable sur les ports HTTP TCP/80 ou HTTPS TCP/443. 

Pour valider sa configuration et son fonctionnement, reportez vous à la documentation officielle: 

https://infosight.hpe.com/InfoSight/media/cms/active/public/pubs_REST_API_Reference_NOS_51x.whz/jun1455055569904

## Installation

<Tabs groupId="sync">
<TabItem value="Online License" label="Online License">

1. Installer le Plugin sur chaque Collecteur Centreon devant superviser des équipements Nimble:

```bash
yum install centreon-pack-hardware-storage-nimble-restapi.noarch
```

2. Sur l'interface Web de Centreon, rendez-vous sur la page **Configuration > Gestionnaire de connecteurs de supervision** et installer le connecteur de supervision *Nimble Rest API*

</TabItem>
<TabItem value="Offline License" label="Offline License">

1. Installer le Plugin sur chaque Collecteur Centreon devant superviser des équipements Nimble:

```bash
yum install centreon-plugin-Hardware-Storage-Nimble-Restapi.noarch
```

2. Installer le RPM du connecteur de supervision sur le serveur Centreon Central:

```bash
yum install centreon-pack-hardware-storage-nimble-restapi.noarch
```

3. Sur l'interface Web de Centreon, rendez-vous sur la page **Configuration > Gestionnaire de connecteurs de supervision** et installer le connecteur de supervision *Nimble Rest API*

</TabItem>
</Tabs>

## Configuration

* Ajouter un nouvel Hôte via le menu "Configuration > Hosts".
* Appliquer le Modèle d'Hôte *HW-Storage-Nimble-Restapi* puis configurer les macros obligatoires: 

| Mandatory | Name                | Description                                                                  |
| :-------- | :------------------ | :--------------------------------------------------------------------------- |
| X         | APIPORT             | Port used (Default: 5392)                                                    |
| X         | APIPROTO            | Specify protocol if needed (Default: 'https')                                |
| X         | APIUSERNAME         | Specify the API Username                                                     |
| X         | APIPASSWORD         | Specify the API Password                                                     |    
|           | APIEXTRAOPTIONS     | Any extra option you may want to add to the command (eg. a `--verbose` flag) |

## FAQ

### Que signifient les messages d'erreur suivants:

#### ```UNKNOWN: 501 Protocol scheme 'connect' is not supported |``` 

Si vous utilisez un proxy et que vous rencontrez cette erreur, cela signifie que le Plugin Centreon ne supporte
pas le protocole de connexion imposé par le proxy.

Afin de vous prémunir de ce problème, utiliser le backend HTTP *curl* en ajoutant l'option ci-dessous: 

 ```--http-backend='curl'```.

#### ```UNKNOWN: Cannot load module 'Net::Curl::Easy'```

Ce message d'erreur signifie qu'une dépendance est manquante lors de l'utilisation du backend *curl*. 

Afin de corriger cette erreur, installer la librairie 'Net::Curl::Easy':

```bash
yum install perl-Net-Curl
```
