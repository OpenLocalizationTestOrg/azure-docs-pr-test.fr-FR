---
title: "didacticiel d’Instances de conteneurs aaaAzure - déploiement d’une application | Documents Microsoft"
description: "Didacticiel Azure Container Instances - Déployer des applications"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>Déployer un conteneur de tooAzure Instances de conteneurs

Il s’agit de hello dernière d’un didacticiel en trois parties. Dans les sections précédentes, [une image de conteneur a été créée](container-instances-tutorial-prepare-app.md) et [envoyées tooan Registre de conteneur Azure](container-instances-tutorial-prepare-acr.md). Cette section termine didacticiel de hello en déployant hello conteneur tooAzure les Instances du conteneur. Les étapes terminées sont les suivantes :

> [!div class="checklist"]
> * Définition d’un groupe de conteneurs à l’aide d’un modèle Azure Resource Manager
> * Déploiement de groupe de conteneur hello à l’aide de hello CLI d’Azure
> * Affichage des journaux de conteneurs

## <a name="deploy-hello-container-using-hello-azure-cli"></a>Déployer le conteneur de hello à l’aide de hello CLI d’Azure

Hello CLI d’Azure permet le déploiement d’un conteneur de tooAzure les Instances du conteneur dans une seule commande. Étant donné que l’image de conteneur hello est hébergé dans hello Registre de conteneur Azure privée, vous devez inclure des tooaccess requis des informations d’identification de hello il. Si nécessaire, vous pouvez les interroger comme indiqué ci-dessous.

Serveur de connexion au Registre de conteneurs (mettez-le à jour avec le nom de votre Registre) :

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

Mot de passe du Registre de conteneurs :

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

toodeploy votre image de conteneur à partir du Registre de conteneur hello avec une ressource de demande de 1 cœur d’UC et 1 Go de mémoire, exécutez hello de commande suivante :

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

Après quelques secondes, vous recevrez une réponse initiale de la part d’Azure Resource Manager. état de hello tooview de déploiement hello, utilisez :

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

Nous pouvons continuer à exécuter cette commande jusqu'à ce que l’état hello passe de *en attente* trop*en cours d’exécution*. Nous pouvons ensuite continuer.

## <a name="view-hello-application-and-container-logs"></a>Afficher les journaux d’application et de conteneur hello

Une fois que la réussite du déploiement de hello, ouvrez votre adresse IP du navigateur toohello indiqué dans la sortie de hello Hello de commande suivante :

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hello world application navigateur de hello][aci-app-browser]

Vous pouvez également afficher la sortie du journal hello de conteneur de hello :

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

Output:

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous terminé processus hello du déploiement de vos Instances de conteneurs de tooAzure conteneurs. Hello suit ont été effectuée :

> [!div class="checklist"]
> * Déploiement de conteneur hello d’à l’aide du Registre de conteneur Azure hello hello CLI d’Azure
> * Afficher l’application hello dans le navigateur de hello
> * Affichage des journaux de conteneur hello

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
