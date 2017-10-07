---
title: "les images Linux VM aaaSelect avec hello CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toouse hello serveur de publication toodetermine hello CLI d’Azure, offre, référence (SKU) et la version pour les images de machine virtuelle du Marketplace."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a>Comment toofind Linux VM images Bonjour Azure Marketplace par hello CLI d’Azure
Cette rubrique décrit comment toouse hello images de machine virtuelle Azure CLI 2.0 toofind Bonjour Azure Marketplace. Utilisez cette toospecify informations une image de Marketplace lorsque vous créez un VM Linux.

Assurez-vous que vous avez installé hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et sont enregistrés dans tooan compte Azure (`az login`).

## <a name="terminology"></a>Terminologie

Images de Marketplace sont identifiées dans hello CLI et d’autres outils Azure selon tooa hiérarchie :

* **Serveur de publication** -hello organisation qui a créé l’image de hello. Exemple : Canonical
* **Offre** : groupe d’images associées, créé par un éditeur. Exemple : Ubuntu Server
* **Référence SKU** : instance d’une offre, par exemple une version majeure d’un logiciel. Exemple : 16.04-LTS
* **Version** -hello numéro de version d’une image de référence (SKU). Lorsque vous spécifiez l’image de hello, vous pouvez remplacer le numéro de version hello avec « dernier », qui sélectionne la version la plus récente de la distribution de hello hello.

toospecify une image de Marketplace, vous utilisez généralement hello image *URN*. Hello URN combine ces valeurs, séparées par le signe deux-points ( :) de hello : *Publisher*:*offrent*:*référence (SKU)*:*Version*. 


## <a name="list-popular-images"></a>Liste des images populaires

Exécutez hello [liste d’images de machine virtuelle de az](/cli/azure/vm/image#list) commande, sans hello `--all` option, toosee une liste de machine virtuelle populaires images Bonjour Azure Marketplace. Par exemple, exécutez hello suivant commande toodisplay une liste mise en cache d’images courantes dans un format de table :

```azurecli
az vm image list --output table
```

sortie de Hello inclut hello URN (hello valeur Bonjour *Urn* colonne), qui vous utilisez toospecify hello image. Lorsque vous créez une machine virtuelle avec l’un de ces images Marketplace populaires, vous pouvez spécifier les alias d’URN hello, tel que *UbuntuLTS*.

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a>Recherche d’images spécifiques

toofind une image de machine virtuelle spécifique Bonjour Marketplace, utilisez hello `az vm image list` avec hello `--all` option. Cette version de la commande hello prend quelques toocomplete de temps et peut retourner une sortie longue, donc vous généralement filtrez la liste de hello par `--publisher` ou un autre paramètre. 

Par exemple, hello commande suivante affiche toutes les offres Debian (n’oubliez pas que sans hello `--all` basculer, il recherche uniquement dans le cache local d’images courantes hello) :

```azurecli
az vm image list --offer Debian --all --output table 

```

Résultat partiel : 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

Appliquer des filtres similaires avec hello `--location`, `--publisher`, et `--sku` options. Vous pouvez même effectuer des correspondances partielles sur un filtre, par exemple rechercher `--offer Deb` toofind toutes les images Debian.

Si vous ne spécifiez pas un emplacement particulier avec hello `--location` , hello les valeurs d’option pour `westus` sont retournés par défaut. (définissez un autre emplacement par défaut en exécutant la commande `az configure --defaults location=<location>`).

Par exemple, hello commande suivante répertorie toutes les références SKU 8 Debian dans `westeurope`:

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

Résultat partiel :

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a>Parcourir les images hello 
Une autre façon toofind une image dans un emplacement est toorun hello [image de machine virtuelle az liste-Éditeurs](/cli/azure/vm/image#list-publishers), [image de machine virtuelle az liste-offres](/cli/azure/vm/image#list-offers), et [image de machine virtuelle az liste-SKU](/cli/azure/vm/image#list-skus) commandes dans la séquence. Ces commandes vous permettent de déterminer les valeurs suivantes :

1. Serveurs de publication liste hello image.
2. pour un éditeur donné, en répertoriant ses offres ;
3. pour une offre donnée, en répertoriant ses références SKU.


Par exemple, hello commande suivante répertorie les éditeurs d’image hello Bonjour emplacement de l’ouest des États-Unis :

```azurecli
az vm image list-publishers --location westus --output table
```

Résultat partiel :

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
Utilisez que cette toofind informations offre à partir d’un éditeur spécifique. Par exemple, si canoniques est un serveur de publication image Bonjour emplacement de l’ouest des États-Unis, recherchez leurs offres en exécutant `azure vm image list-offers`. Passez l’emplacement de hello et publisher hello comme hello l’exemple suivant :

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

Output:

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
Vous voyez que dans la région ouest des États-Unis hello, canoniques publie hello **UbuntuServer** offrent sur Azure. Mais les références (SKU) ? l’exécution de ces valeurs, tooget `azure vm image list-skus` et définissez hello, publisher et l’emplacement offre que vous avez découvert :

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

Output:

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

Enfin, utilisez hello `az vm image list` commande toofind une version spécifique de hello SKU souhaité, par exemple, **16.04-LTS**:

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

Output:

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a>Étapes suivantes
Maintenant vous pouvez choisir précisément hello image que vous voulez toouse en prenant acte de hello valeur URN. Passez cette valeur avec hello `--image` paramètre lorsque vous créez une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) commande. N’oubliez pas que vous pouvez éventuellement remplacer le numéro de version hello Bonjour URN avec « dernier ». Cette version est toujours version la plus récente de la distribution de hello hello. toocreate un ordinateur virtuel rapidement en utilisant les informations d’URN hello, consultez [créer et gérer des ordinateurs virtuels Linux par hello CLI d’Azure](tutorial-manage-vm.md).
