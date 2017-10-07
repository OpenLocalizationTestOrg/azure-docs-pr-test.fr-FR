---
title: "aaaCreate un IoT hub à l’aide d’Azure CLI (azure.js) | Documents Microsoft"
description: "Comment toocreate une à l’aide de Azure IoT hub hello multiplateforme Azure CLI (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>Créez un IoT hub à l’aide de hello CLI d’Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introduction

Vous pouvez utiliser Azure CLI (azure.js) toocreate et gérer les hubs Azure IoT par programme. Cet article vous explique comment toouse hello CLI d’Azure (azure.js) toocreate un IoT hub.

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

* CLI Azure (azure.js) – hello CLI pour hello classique et les modèles de déploiement de gestion des ressources comme décrit dans cet article.
* [Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -hello nouvelle génération CLI pour le modèle de déploiement de gestion de ressources hello.

toocomplete ce didacticiel, vous devez hello suivant :

* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez en créer un [gratuitement][lnk-free-trial] en quelques minutes.
* [Azure CLI 0.10.4][lnk-CLI-install] ou version ultérieure. Si vous avez déjà hello CLI d’Azure installé, vous pouvez valider la version actuelle de hello invite de commandes hello avec hello de commande suivante :

```azurecli
azure --version
```

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md). Hello CLI d’Azure doit être en mode Azure Resource Manager :
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>Configurer votre compte et votre abonnement Microsoft Azure

1. À l’invite de commandes hello connexion en tapant hello la commande suivante :

   ```azurecli
    azure login
   ```

   Utilisez hello suggérée navigateur et tooauthenticate de code.
1. Si vous avez plusieurs abonnements Azure, la connexion tooAzure vous accorde l’accès tooall hello Azure abonnements associés à vos informations d’identification. Vous pouvez afficher hello abonnements Azure et identifiez celui qui correspond à une valeur par défaut hello, à l’aide de la commande hello :

   ```azurecli
    azure account list
   ```

   contexte d’abonnement hello tooset sous lequel vous voulez reste hello toorun hello commandes utilisent :

   ```azurecli
    azure account set <subscription name>
   ```

1. Si vous n’avez pas de groupe de ressources, vous pouvez en créer un nommé **exampleResourceGroup** :

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> article de Hello [utiliser hello CLI d’Azure toomanage Azure ressources et groupes de ressources] [ lnk-CLI-arm] fournit plus d’informations sur la façon dont toouse hello CLI d’Azure toomanage Azure ressources.

## <a name="create-an-iot-hub"></a>Création d’un IoT Hub

Paramètres obligatoires :

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **resource-group**. nom du groupe de ressources de Hello. format de Hello est un trait de soulignement alphanumérique, non-respect de la casse, trait d’union, longueur de 1 à 64.
* **name**. nom de Hello de hello IoT hub toobe est créé. format de Hello est un trait de soulignement alphanumérique, non-respect de la casse et trait d’union, longueur de 3 à 50.
* **location**. Hello emplacement (région/centre de données azure) tooprovision hello IoT hub.
* **sku-name**. nom de Hello de hello référence (SKU), un des : [F1, S1, S2 et S3]. Pour hello dernières la liste complète, consultez toohello page de tarification pour IoT Hub.
* **units**. nombre de Hello d’unités configurées. Plage : F1 [1-1] : S1, S2 [1-200] : S3 [1-10]. Les unités IoT Hub sont basées sur votre nombre total de messages hello et de nombre de périphériques, vous souhaitez tooconnect.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee tous hello paramètres disponibles pour la création, vous pouvez utiliser la commande de help hello dans l’invite de commandes :

```azurecli
azure iothub create -h
```

Exemple : toocreate un IoT Hub appelé **exampleIoTHubName** dans le groupe de ressources hello **exampleResourceGroup**, exécutez hello commande suivante :

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> Cette commande CLI Azure crée un IoT Hub Standard S1 pour lequel vous êtes facturé. Vous pouvez supprimer le hub de IoT hello **exampleIoTHubName** à l’aide de commande suivante :
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>Étapes suivantes

toolearn plus sur le développement pour IoT Hub, consultez hello l’article suivant :

* [Kits de développement logiciel (SDK) IoT][lnk-sdks]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [À l’aide de hello toomanage portail Azure IoT Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
