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
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a><span data-ttu-id="626da-103">Créez un IoT hub à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="626da-103">Create an IoT hub using hello Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="626da-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="626da-104">Introduction</span></span>

<span data-ttu-id="626da-105">Vous pouvez utiliser Azure CLI 2.0 (az.py) toocreate et gérer les hubs Azure IoT par programme.</span><span class="sxs-lookup"><span data-stu-id="626da-105">You can use Azure CLI 2.0 (az.py) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="626da-106">Cet article vous explique comment toouse hello Azure CLI 2.0 (az.py) toocreate un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="626da-106">This article shows you how toouse hello Azure CLI 2.0 (az.py) toocreate an IoT hub.</span></span>

<span data-ttu-id="626da-107">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="626da-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="626da-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) : hello CLI pour les modèles de déploiement gestion classique et les ressources des hello.</span><span class="sxs-lookup"><span data-stu-id="626da-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="626da-109">Azure CLI 2.0 (az.py) - hello nouvelle génération CLI pour le modèle de déploiement de gestion des ressources hello comme décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="626da-109">Azure CLI 2.0 (az.py) - hello next generation CLI for hello resource management deployment model as described in this article.</span></span>

<span data-ttu-id="626da-110">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="626da-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="626da-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="626da-111">An active Azure account.</span></span> <span data-ttu-id="626da-112">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="626da-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="626da-113">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="626da-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="626da-114">Se connecter à votre compte Azure et le définir</span><span class="sxs-lookup"><span data-stu-id="626da-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="626da-115">Connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="626da-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="626da-116">À l’invite de commandes hello exécuter hello [commande login][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="626da-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="626da-117">Suivez tooauthenticate d’instructions hello à l’aide de code de hello et connectez-vous à tooyour compte Azure via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="626da-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

2. <span data-ttu-id="626da-118">Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello associé à vos informations d’identification de comptes Azure.</span><span class="sxs-lookup"><span data-stu-id="626da-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="626da-119">Utilisez hello suivante [toolist de commande hello comptes Azure] [ lnk-az-account-command] disponibles pour vous toouse :</span><span class="sxs-lookup"><span data-stu-id="626da-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="626da-120">Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toocreate votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="626da-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="626da-121">Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :</span><span class="sxs-lookup"><span data-stu-id="626da-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="626da-122">Création d’un IoT Hub</span><span class="sxs-lookup"><span data-stu-id="626da-122">Create an IoT Hub</span></span>

<span data-ttu-id="626da-123">Utilisez hello CLI d’Azure toocreate un groupe de ressources, puis ajoutez un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="626da-123">Use hello Azure CLI toocreate a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="626da-124">Lorsque vous créez un IoT Hub, vous devez le créer dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="626da-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="626da-125">Utiliser un groupe de ressources existant, ou exécutez hello [commande toocreate un groupe de ressources][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="626da-125">Either use an existing resource group, or run hello following [command toocreate a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="626da-126">Hello l’exemple précédent crée un groupe de ressources hello Bonjour emplacement de l’ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="626da-126">hello previous example creates hello resource group in hello West US location.</span></span> <span data-ttu-id="626da-127">Vous pouvez afficher une liste des emplacements disponibles en exécutant la commande hello `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="626da-127">You can view a list of available locations by running hello command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="626da-128">Exécutez hello [commande toocreate un hub IoT] [ lnk-az-iot-command] dans votre groupe de ressources, à l’aide d’un nom global unique pour votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="626da-128">Run hello following [command toocreate an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="626da-129">commande précédente Hello crée un hub IoT Bonjour S1 tarification pour lequel vous êtes facturé.</span><span class="sxs-lookup"><span data-stu-id="626da-129">hello previous command creates an IoT hub in hello S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="626da-130">Pour plus d’informations, voir la [tarification d’Azure IoT Hub][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="626da-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="626da-131">Supprimer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="626da-131">Remove an IoT Hub</span></span>

<span data-ttu-id="626da-132">Vous pouvez utiliser hello CLI d’Azure trop[supprimer une ressource individuelle][lnk-az-resource-command], tel qu’un hub IoT, ou supprimer un groupe de ressources et toutes ses ressources, y compris les IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="626da-132">You can use hello Azure CLI too[delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="626da-133">toodelete un IoT hub, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="626da-133">toodelete an IoT hub, run hello following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="626da-134">toodelete un groupe de ressources et toutes ses ressources, hello exécution suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="626da-134">toodelete a resource group and all its resources, run hello following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="626da-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="626da-135">Next steps</span></span>
<span data-ttu-id="626da-136">toolearn plus sur le développement pour IoT Hub, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="626da-136">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="626da-137">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="626da-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="626da-138">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="626da-138">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="626da-139">[À l’aide de hello toomanage portail Azure IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="626da-139">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

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
