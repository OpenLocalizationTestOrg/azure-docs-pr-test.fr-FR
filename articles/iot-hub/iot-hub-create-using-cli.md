---
title: "aaaCreate un IoT Hub à l’aide d’Azure CLI (az.py) | Documents Microsoft"
description: "Comment toocreate une à l’aide de Azure IoT hub hello multiplateforme Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>Créez un IoT hub à l’aide de hello Azure CLI 2.0

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introduction

Vous pouvez utiliser Azure CLI 2.0 (az.py) toocreate et gérer les hubs Azure IoT par programme. Cet article vous explique comment toouse hello Azure CLI 2.0 (az.py) toocreate un IoT hub.

Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

* [Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) : hello CLI pour les modèles de déploiement gestion classique et les ressources des hello.
* Azure CLI 2.0 (az.py) - hello nouvelle génération CLI pour le modèle de déploiement de gestion des ressources hello comme décrit dans cet article.

toocomplete ce didacticiel, vous devez hello suivant :

* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.
* [Azure CLI 2.0][lnk-CLI-install].

## <a name="sign-in-and-set-your-azure-account"></a>Se connecter à votre compte Azure et le définir

Connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement.

1. À l’invite de commandes hello exécuter hello [commande login][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    Suivez tooauthenticate d’instructions hello à l’aide de code de hello et connectez-vous à tooyour compte Azure via un navigateur web.

2. Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello associé à vos informations d’identification de comptes Azure. Utilisez hello suivante [toolist de commande hello comptes Azure] [ lnk-az-account-command] disponibles pour vous toouse :
    
    ```azurecli
    az account list 
    ```

    Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toocreate votre hub IoT. Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>Création d’un IoT Hub

Utilisez hello CLI d’Azure toocreate un groupe de ressources, puis ajoutez un IoT hub.

1. Lorsque vous créez un IoT Hub, vous devez le créer dans un groupe de ressources. Utiliser un groupe de ressources existant, ou exécutez hello [commande toocreate un groupe de ressources][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > Hello l’exemple précédent crée un groupe de ressources hello Bonjour emplacement de l’ouest des États-Unis. Vous pouvez afficher une liste des emplacements disponibles en exécutant la commande hello `az account list-locations -o table`.
    >
    >

2. Exécutez hello [commande toocreate un hub IoT] [ lnk-az-iot-command] dans votre groupe de ressources, à l’aide d’un nom global unique pour votre IoT hub :
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> commande précédente Hello crée un hub IoT Bonjour S1 tarification pour lequel vous êtes facturé. Pour plus d’informations, voir la [tarification d’Azure IoT Hub][lnk-iot-pricing].
>
>

## <a name="remove-an-iot-hub"></a>Supprimer un hub IoT

Vous pouvez utiliser hello CLI d’Azure trop[supprimer une ressource individuelle][lnk-az-resource-command], tel qu’un hub IoT, ou supprimer un groupe de ressources et toutes ses ressources, y compris les IoT hubs.

toodelete un IoT hub, exécutez hello de commande suivante :

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

toodelete un groupe de ressources et toutes ses ressources, hello exécution suivant de commandes :

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>Étapes suivantes
toolearn plus sur le développement pour IoT Hub, consultez hello suivant des articles :

* [Guide du développeur IoT Hub][lnk-devguide]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [À l’aide de hello toomanage portail Azure IoT Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
