---
title: "Création d’un IoT Hub à l’aide de l’interface de ligne de commande Azure (azure.js) | Microsoft Docs"
description: "Création d’un Azure IoT Hub à l’aide de l’interface de ligne de commande Azure multiplateforme (azure.js)."
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
ms.openlocfilehash: 5e37c6c5e8625ce446ab203f19f9a8b2f1cd5a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli"></a><span data-ttu-id="07e03-103">Création d’un IoT Hub à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="07e03-103">Create an IoT hub using the Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="07e03-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="07e03-104">Introduction</span></span>

<span data-ttu-id="07e03-105">Vous pouvez utiliser l’interface de ligne de commande Azure (azure.js) pour créer et gérer des Azure IoT Hubs de façon programmée.</span><span class="sxs-lookup"><span data-stu-id="07e03-105">You can use Azure CLI (azure.js) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="07e03-106">Cet article explique comment utiliser l’interface de ligne de commande Azure (azure.js) pour créer un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07e03-106">This article shows you how to use the Azure CLI (azure.js) to create an IoT hub.</span></span>

<span data-ttu-id="07e03-107">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="07e03-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="07e03-108">Azure CLI (azure.js) : l’interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager décrits dans cet article.</span><span class="sxs-lookup"><span data-stu-id="07e03-108">Azure CLI (azure.js) – the CLI for the classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="07e03-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) : interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="07e03-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - the next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="07e03-110">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="07e03-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="07e03-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="07e03-111">An active Azure account.</span></span> <span data-ttu-id="07e03-112">Si vous ne possédez pas de compte, vous pouvez en créer un [gratuitement][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="07e03-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="07e03-113">[Azure CLI 0.10.4][lnk-CLI-install] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="07e03-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="07e03-114">Si vous avez déjà installé l’interface de ligne de commande (CLI) Azure, vous pouvez valider la version actuelle à l’invite de commandes avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07e03-114">If you already have the Azure CLI installed, you can validate the current version at the command prompt with the following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="07e03-115">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="07e03-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="07e03-116">L’interface de ligne de commande (CLI) Azure doit être en mode Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="07e03-116">The Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="07e03-117">Configurer votre compte et votre abonnement Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="07e03-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="07e03-118">À l’invite de commandes, connectez-vous en tapant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07e03-118">At the command prompt, login by typing the following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="07e03-119">Utilisez le navigateur web suggéré et le code d’authentification.</span><span class="sxs-lookup"><span data-stu-id="07e03-119">Use the suggested web browser and code to authenticate.</span></span>
1. <span data-ttu-id="07e03-120">Si vous possédez plusieurs abonnements Azure, la connexion à Azure donne accès à tous les abonnements Azure associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="07e03-120">If you have multiple Azure subscriptions, connecting to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="07e03-121">Vous pouvez afficher les abonnements et identifier l’abonnement Azure par défaut à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07e03-121">You can view the Azure subscriptions, and identify which one is the default, using the command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="07e03-122">Pour définir le contexte de l’abonnement sous lequel vous souhaitez exécuter le reste des commandes, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07e03-122">To set the subscription context under which you want to run the rest of the commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="07e03-123">Si vous n’avez pas de groupe de ressources, vous pouvez en créer un nommé **exampleResourceGroup** :</span><span class="sxs-lookup"><span data-stu-id="07e03-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="07e03-124">Pour plus d’informations sur l’utilisation de l’interface de ligne de commande Azure pour gérer des ressources Azure, voir l’article [Utiliser l’interface de ligne de commande Azure pour gérer les ressources et les groupes de ressources Azure][lnk-CLI-arm].</span><span class="sxs-lookup"><span data-stu-id="07e03-124">The article [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] provides more information about how to use the Azure CLI to manage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="07e03-125">Création d’un IoT Hub</span><span class="sxs-lookup"><span data-stu-id="07e03-125">Create an IoT Hub</span></span>

<span data-ttu-id="07e03-126">Paramètres obligatoires :</span><span class="sxs-lookup"><span data-stu-id="07e03-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="07e03-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="07e03-127">**resource-group**.</span></span> <span data-ttu-id="07e03-128">Nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="07e03-128">The resource group name.</span></span> <span data-ttu-id="07e03-129">Le format ne tient pas compte de la casse et accepte les caractères suivants : trait de soulignement, valeurs alphanumériques et trait d’union. La longueur doit être incluse entre 1 et 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="07e03-129">The format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="07e03-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="07e03-130">**name**.</span></span> <span data-ttu-id="07e03-131">Nom de l’instance IoT Hub à créer.</span><span class="sxs-lookup"><span data-stu-id="07e03-131">The name of the IoT hub to be created.</span></span> <span data-ttu-id="07e03-132">Le format ne tient pas compte de la casse et accepte les caractères suivants : trait de soulignement, valeurs alphanumériques et trait d’union. La longueur doit être incluse entre 3 et 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="07e03-132">The format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="07e03-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="07e03-133">**location**.</span></span> <span data-ttu-id="07e03-134">Emplacement (région/centre de données Azure) associé à la configuration de l’instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07e03-134">The location (azure region/datacenter) to provision the IoT hub.</span></span>
* <span data-ttu-id="07e03-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="07e03-135">**sku-name**.</span></span> <span data-ttu-id="07e03-136">Nom de la référence, à choisir parmi les éléments suivants : [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="07e03-136">The name of the sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="07e03-137">Pour obtenir la liste complète la plus récente, reportez-vous à la page relative à la tarification d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07e03-137">For the latest full list, refer to the pricing page for IoT Hub.</span></span>
* <span data-ttu-id="07e03-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="07e03-138">**units**.</span></span> <span data-ttu-id="07e03-139">Nombre d’unités configurées.</span><span class="sxs-lookup"><span data-stu-id="07e03-139">The number of provisioned units.</span></span> <span data-ttu-id="07e03-140">Plage : F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span><span class="sxs-lookup"><span data-stu-id="07e03-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="07e03-141">Le nombre d’unités IoT Hub dépend du nombre total de messages et du nombre d’appareils que vous souhaitez connecter.</span><span class="sxs-lookup"><span data-stu-id="07e03-141">IoT Hub units are based on your total message count and the number of devices you want to connect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="07e03-142">Pour afficher tous les paramètres disponibles pour la création, vous pouvez utiliser la commande d’aide dans une invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="07e03-142">To see all the parameters available for creation, you can use the help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="07e03-143">Voici un exemple rapide. Pour créer une instance IoT Hub appelée **exampleIoTHubName** dans le groupe de ressources **exampleResourceGroup**, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07e03-143">Quick example: To create an IoT Hub called **exampleIoTHubName** in the resource group **exampleResourceGroup**, run the following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="07e03-144">Cette commande CLI Azure crée un IoT Hub Standard S1 pour lequel vous êtes facturé.</span><span class="sxs-lookup"><span data-stu-id="07e03-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="07e03-145">Vous pouvez supprimer l’IoT Hub **exampleIoTHubName** à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07e03-145">You can delete the IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="07e03-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07e03-146">Next steps</span></span>

<span data-ttu-id="07e03-147">Pour en savoir plus sur le développement pour IoT Hub, consultez l’article suivant :</span><span class="sxs-lookup"><span data-stu-id="07e03-147">To learn more about developing for IoT Hub, see the following article:</span></span>

* <span data-ttu-id="07e03-148">[Kits de développement logiciel (SDK) IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="07e03-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="07e03-149">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="07e03-149">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="07e03-150">[Utilisation du portail Azure pour gérer IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="07e03-150">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
