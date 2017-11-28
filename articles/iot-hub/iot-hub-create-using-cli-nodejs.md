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
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="9bd45-103">Créez un IoT hub à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="9bd45-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="9bd45-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="9bd45-104">Introduction</span></span>

<span data-ttu-id="9bd45-105">Vous pouvez utiliser Azure CLI (azure.js) toocreate et gérer les hubs Azure IoT par programme.</span><span class="sxs-lookup"><span data-stu-id="9bd45-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="9bd45-106">Cet article vous explique comment toouse hello CLI d’Azure (azure.js) toocreate un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9bd45-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="9bd45-107">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="9bd45-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="9bd45-108">CLI Azure (azure.js) – hello CLI pour hello classique et les modèles de déploiement de gestion des ressources comme décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="9bd45-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="9bd45-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -hello nouvelle génération CLI pour le modèle de déploiement de gestion de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="9bd45-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="9bd45-110">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9bd45-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="9bd45-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="9bd45-111">An active Azure account.</span></span> <span data-ttu-id="9bd45-112">Si vous ne possédez pas de compte, vous pouvez en créer un [gratuitement][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="9bd45-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="9bd45-113">[Azure CLI 0.10.4][lnk-CLI-install] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9bd45-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="9bd45-114">Si vous avez déjà hello CLI d’Azure installé, vous pouvez valider la version actuelle de hello invite de commandes hello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9bd45-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="9bd45-115">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9bd45-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9bd45-116">Hello CLI d’Azure doit être en mode Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="9bd45-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="9bd45-117">Configurer votre compte et votre abonnement Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9bd45-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="9bd45-118">À l’invite de commandes hello connexion en tapant hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9bd45-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="9bd45-119">Utilisez hello suggérée navigateur et tooauthenticate de code.</span><span class="sxs-lookup"><span data-stu-id="9bd45-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="9bd45-120">Si vous avez plusieurs abonnements Azure, la connexion tooAzure vous accorde l’accès tooall hello Azure abonnements associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9bd45-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="9bd45-121">Vous pouvez afficher hello abonnements Azure et identifiez celui qui correspond à une valeur par défaut hello, à l’aide de la commande hello :</span><span class="sxs-lookup"><span data-stu-id="9bd45-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="9bd45-122">contexte d’abonnement hello tooset sous lequel vous voulez reste hello toorun hello commandes utilisent :</span><span class="sxs-lookup"><span data-stu-id="9bd45-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="9bd45-123">Si vous n’avez pas de groupe de ressources, vous pouvez en créer un nommé **exampleResourceGroup** :</span><span class="sxs-lookup"><span data-stu-id="9bd45-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="9bd45-124">article de Hello [utiliser hello CLI d’Azure toomanage Azure ressources et groupes de ressources] [ lnk-CLI-arm] fournit plus d’informations sur la façon dont toouse hello CLI d’Azure toomanage Azure ressources.</span><span class="sxs-lookup"><span data-stu-id="9bd45-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="9bd45-125">Création d’un IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9bd45-125">Create an IoT Hub</span></span>

<span data-ttu-id="9bd45-126">Paramètres obligatoires :</span><span class="sxs-lookup"><span data-stu-id="9bd45-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="9bd45-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="9bd45-127">**resource-group**.</span></span> <span data-ttu-id="9bd45-128">nom du groupe de ressources de Hello.</span><span class="sxs-lookup"><span data-stu-id="9bd45-128">hello resource group name.</span></span> <span data-ttu-id="9bd45-129">format de Hello est un trait de soulignement alphanumérique, non-respect de la casse, trait d’union, longueur de 1 à 64.</span><span class="sxs-lookup"><span data-stu-id="9bd45-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="9bd45-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="9bd45-130">**name**.</span></span> <span data-ttu-id="9bd45-131">nom de Hello de hello IoT hub toobe est créé.</span><span class="sxs-lookup"><span data-stu-id="9bd45-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="9bd45-132">format de Hello est un trait de soulignement alphanumérique, non-respect de la casse et trait d’union, longueur de 3 à 50.</span><span class="sxs-lookup"><span data-stu-id="9bd45-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="9bd45-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="9bd45-133">**location**.</span></span> <span data-ttu-id="9bd45-134">Hello emplacement (région/centre de données azure) tooprovision hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9bd45-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="9bd45-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="9bd45-135">**sku-name**.</span></span> <span data-ttu-id="9bd45-136">nom de Hello de hello référence (SKU), un des : [F1, S1, S2 et S3].</span><span class="sxs-lookup"><span data-stu-id="9bd45-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="9bd45-137">Pour hello dernières la liste complète, consultez toohello page de tarification pour IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9bd45-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="9bd45-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="9bd45-138">**units**.</span></span> <span data-ttu-id="9bd45-139">nombre de Hello d’unités configurées.</span><span class="sxs-lookup"><span data-stu-id="9bd45-139">hello number of provisioned units.</span></span> <span data-ttu-id="9bd45-140">Plage : F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span><span class="sxs-lookup"><span data-stu-id="9bd45-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="9bd45-141">Les unités IoT Hub sont basées sur votre nombre total de messages hello et de nombre de périphériques, vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="9bd45-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="9bd45-142">toosee tous hello paramètres disponibles pour la création, vous pouvez utiliser la commande de help hello dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="9bd45-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="9bd45-143">Exemple : toocreate un IoT Hub appelé **exampleIoTHubName** dans le groupe de ressources hello **exampleResourceGroup**, exécutez hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9bd45-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="9bd45-144">Cette commande CLI Azure crée un IoT Hub Standard S1 pour lequel vous êtes facturé.</span><span class="sxs-lookup"><span data-stu-id="9bd45-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="9bd45-145">Vous pouvez supprimer le hub de IoT hello **exampleIoTHubName** à l’aide de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9bd45-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="9bd45-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9bd45-146">Next steps</span></span>

<span data-ttu-id="9bd45-147">toolearn plus sur le développement pour IoT Hub, consultez hello l’article suivant :</span><span class="sxs-lookup"><span data-stu-id="9bd45-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="9bd45-148">[Kits de développement logiciel (SDK) IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="9bd45-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="9bd45-149">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="9bd45-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9bd45-150">[À l’aide de hello toomanage portail Azure IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="9bd45-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
