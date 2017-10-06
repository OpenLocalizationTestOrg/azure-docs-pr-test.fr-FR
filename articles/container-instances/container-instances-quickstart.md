---
title: "aaaCreate votre premier conteneur d’Instances de conteneurs Azure | Documentation Azure"
description: "Déploiement et prise en main d’Azure Container Instances"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a>Créer son premier conteneur dans Azure Container Instances

Les Instances du conteneur Azure rend facile toocreate et gérer des conteneurs dans Azure. Dans ce démarrage rapide, vous créez un conteneur dans Azure et l’exposer toohello internet avec une adresse IP publique. Cette opération s’effectue en une seule commande. En l’espace de quelques secondes, ceci s’affiche dans votre navigateur :

![L’application déployée à l’aide d’Azure Container Instances est affichée dans le navigateur][aci-app-browser]

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.12 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Les instances Azure Container Instances sont des ressources Azure et doivent être placées dans un groupe de ressources Azure, un ensemble logique dans lequel des ressources Azure sont déployées et gérées.

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Créez un conteneur.

Vous pouvez créer un conteneur en attribuant un nom, une image Docker ainsi qu’un groupe de ressources Azure. Vous pouvez éventuellement exposer hello conteneur toohello internet avec une adresse IP publique. Dans ce cas, nous utilisons un conteneur qui héberge une application web basique écrite dans [Node.js](http://nodejs.org).

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

Après quelques secondes, vous devez obtenir une demande de tooyour de réponse. Au départ, hello conteneur soit dans un **création** état, mais elle doit démarrer dans quelques secondes. Vous pouvez vérifier le statut hello à l’aide de hello `show` commande :

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

Au bas de hello de sortie de hello, vous verrez l’état d’approvisionnement du conteneur hello et son adresse IP :

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

Une fois le conteneur de hello déplace toohello **Succeeded** d’état, vous pouvez l’atteindre dans le navigateur hello à l’aide de l’adresse IP hello fournie. 

![L’application déployée à l’aide d’Azure Container Instances est affichée dans le navigateur][aci-app-browser]

## <a name="pull-hello-container-logs"></a>Collecteur de journaux du conteneur hello

Vous pouvez extraire des journaux de hello du conteneur de hello vous avez créé à l’aide de hello `logs` commande :

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

Output:

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>Supprimer le conteneur de hello

Lorsque vous avez terminé avec le conteneur de hello, vous pouvez le supprimer à l’aide de hello `delete` commande :

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Tous les Hello du code pour le conteneur de hello utilisé dans ce démarrage rapide est disponible [sur GitHub][app-github-repo], ainsi que son fichier Dockerfile. Si vous souhaitez que tootry génération vous-même et déployer des Instances de conteneurs tooAzure à l’aide de hello Registre de conteneur Azure, continuer le didacticiel d’Instances de conteneurs Azure toohello.

> [!div class="nextstepaction"]
> [Didacticiels Azure Container Instances](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png