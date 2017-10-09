---
title: "aaaCreate Docker héberge dans Azure avec une Machine Docker | Documents Microsoft"
description: "Décrit l’utilisation des hôtes de docker toocreate Machine Docker dans Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Créer des hôtes Docker dans Azure avec Docker Machine
En cours d’exécution [Docker](https://www.docker.com/) conteneurs requiert un démon de docker hôte machine virtuelle en cours d’exécution hello.
Cette rubrique décrit comment toouse hello [docker-machine](https://docs.docker.com/machine/) commande toocreate nouvelles machines virtuelles Linux, configuré avec hello démon Docker, s’exécutant dans Azure. 

**Remarque :** 

* *Cet article suppose que la version de docker-machine est 0.9.0-rc2 ou une version supérieure*
* *Les conteneurs Windows sera être pris en charge via docker-machine Bonjour futur proche*

## <a name="create-vms-with-docker-machine"></a>Créer des machines virtuelles avec Docker Machine
Créer des machines virtuelles hôtes docker dans Azure avec hello `docker-machine create` commande à l’aide de hello `azure` pilote. 

Hello pilote Azure nécessite votre ID d’abonnement. Vous pouvez utiliser hello [CLI d’Azure](cli-install-nodejs.md) ou hello [Azure Portal](https://portal.azure.com) tooretrieve votre abonnement Azure. 

**À l’aide de hello portail Azure**

* Sélectionnez **abonnements** de hello de navigation gauche page et copie hello id d’abonnement.

**À l’aide de hello CLI d’Azure**

* Type ```azure account list``` et id d’abonnement copie hello.

Type `docker-machine create --driver azure` toosee hello options et leurs valeurs par défaut.
Vous pouvez également voir hello [documentation du pilote de Azure Docker](https://docs.docker.com/machine/drivers/azure/) pour plus d’informations. 

Hello exemple suivant s’appuie sur hello [les valeurs par défaut](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), mais définit ces valeurs si vous le souhaitez : 

* Azure dns pour le nom hello associé hello adresse IP publique et les certificats générés. Il s’agit de nom DNS de hello de votre machine virtuelle. Hello machine virtuelle peut alors en toute sécurité arrêter, libérer hello dynamiques d’adresse IP et de fournir hello capacité tooreconnect après le démarrage de machine virtuelle de hello à nouveau avec une nouvelle adresse IP. préfixe de nom Hello doit être unique pour cette région UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.
* ouvrir le port 80 sur hello machine virtuelle pour l’accès internet sortant
* taille de stockage premium plus rapide de VM tooutilize de hello
* stockage Premium utilisé pour le disque de machine virtuelle hello

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Choisissez un hôte Docker avec docker-machine
Une fois que vous avez une entrée dans une machine docker pour votre ordinateur hôte, vous pouvez définir hôte par défaut de hello lors de l’exécution des commandes docker.

## <a name="using-powershell"></a>Utiliser PowerShell
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Avec Bash
```bash
eval $(docker-machine env MyDockerHost)
```

Vous pouvez maintenant exécuter des commandes docker sur l’hôte spécifié hello

```
docker ps
docker info
```

## <a name="run-a-container"></a>Exécuter un conteneur
Avec un hôte configuré, vous pouvez maintenant exécuter un tootest de serveur web simple si votre hôte n’a été configuré correctement.
Ici nous allons utiliser une image standard nginx, spécifiez qu’il doit écouter sur le port 80, et que si le redémarrage de la machine virtuelle d’hôte hello, conteneur de hello redémarrent également (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

sortie de Hello doit ressembler à hello qui suit :

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>Conteneur de test hello
Examinez les conteneurs en cours d'exécution en utilisant `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

Et hello toosee en cours d’exécution du conteneur, type `docker-machine ip <VM name>` toofind hello le tooenter d’adresse IP dans le navigateur de hello :

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Exécution d’un conteneur ngnix](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Résumé
Avec docker-machine, vous pouvez facilement approvisionner des hôtes Docker dans Azure pour chacune de vos validations d’hôte Docker.
Pour la production d’hébergement de conteneurs, consultez hello [Service de conteneur Azure](http://aka.ms/AzureContainerService)

toodevelop .NET des Applications de base avec Visual Studio, consultez [outils Docker pour Visual Studio](http://aka.ms/DockerToolsForVS)

