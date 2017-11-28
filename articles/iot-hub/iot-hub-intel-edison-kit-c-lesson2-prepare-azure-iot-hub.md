---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 2 : inscription de l’appareil | Documents Microsoft"
description: "Créer un groupe de ressources, créez un Azure IoT hub, inscrire et Edison dans hello Azure IoT hub aide hello CLI d’Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="a0533-103">Créer votre IoT Hub et inscrire Intel Edison</span><span class="sxs-lookup"><span data-stu-id="a0533-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a0533-104">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="a0533-104">What you will do</span></span>
* <span data-ttu-id="a0533-105">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a0533-105">Create a resource group.</span></span>
* <span data-ttu-id="a0533-106">Créer votre concentrateur Azure IoT dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a0533-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="a0533-107">Ajouter le concentrateur de Azure IoT Intel Edison toohello à l’aide de hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="a0533-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="a0533-108">Lorsque vous utilisez hello CLI d’Azure tooadd hub IoT de tooyour Edison, service de hello génère une clé pour tooauthenticate Edison avec le service de hello.</span><span class="sxs-lookup"><span data-stu-id="a0533-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="a0533-109">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a0533-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a0533-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="a0533-110">What you will learn</span></span>
<span data-ttu-id="a0533-111">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a0533-111">In this article, you will learn:</span></span>
* <span data-ttu-id="a0533-112">Comment toouse hello CLI d’Azure toocreate un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a0533-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="a0533-113">Comment toocreate une identité d’appareil pour Edison dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a0533-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a0533-114">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="a0533-114">What you need</span></span>
* <span data-ttu-id="a0533-115">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a0533-115">An Azure account.</span></span> <span data-ttu-id="a0533-116">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a0533-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="a0533-117">Vous devez avoir hello que CLI d’Azure installé.</span><span class="sxs-lookup"><span data-stu-id="a0533-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="a0533-118">Création de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a0533-118">Create your IoT hub</span></span>
<span data-ttu-id="a0533-119">Azure IoT Hub vous permet de connecter, surveiller et gérer des millions de ressources IoT.</span><span class="sxs-lookup"><span data-stu-id="a0533-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="a0533-120">toocreate votre hub IoT, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0533-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="a0533-121">La connexion tooyour compte Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a0533-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="a0533-122">Après une connexion réussie, tous vos abonnements disponibles sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="a0533-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="a0533-123">Définissez hello abonnement de valeur par défaut que vous souhaitez toouse en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a0533-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="a0533-124">`subscription ID or name`se trouvent dans la sortie de hello Hello `az login` ou hello `az account list` commande.</span><span class="sxs-lookup"><span data-stu-id="a0533-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="a0533-125">Inscription du fournisseur de hello en hello suivant de commande en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a0533-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="a0533-126">Les fournisseurs de ressources sont des services qui fournissent des ressources pour votre application.</span><span class="sxs-lookup"><span data-stu-id="a0533-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="a0533-127">Vous devez inscrire le fournisseur de hello avant de pouvoir déployer hello ressource Azure qui hello offres du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="a0533-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="a0533-128">Créer un groupe de ressources nommé iot-exemple dans la région ouest des États-Unis hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a0533-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="a0533-129">`westus`est l’emplacement hello vous créez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a0533-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="a0533-130">Si vous voulez toouse un autre emplacement, vous pouvez exécuter `az account list-locations -o table` toosee tous hello emplacements Azure prend en charge.</span><span class="sxs-lookup"><span data-stu-id="a0533-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="a0533-131">Créez un hub IoT hello iot-exemple groupe de ressources en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a0533-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="a0533-132">Par défaut, hello outil crée un IoT Hub niveau de tarification gratuit hello.</span><span class="sxs-lookup"><span data-stu-id="a0533-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="a0533-133">Pour plus d’informations, consultez la [tarification Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="a0533-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="a0533-134">nom de Hello de votre IoT hub doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="a0533-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="a0533-135">Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a0533-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="a0533-136">Inscription d’Edison dans votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a0533-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="a0533-137">Chaque périphérique qui envoie IoT hub tooyour de messages et reçoit des messages à partir de votre IoT hub doit être enregistré avec un ID unique.</span><span class="sxs-lookup"><span data-stu-id="a0533-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="a0533-138">Inscrivez Edison dans votre IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a0533-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="a0533-139">Résumé</span><span class="sxs-lookup"><span data-stu-id="a0533-139">Summary</span></span>
<span data-ttu-id="a0533-140">Vous avez créé un IoT Hub et enregistré Edison sous une identité d’appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a0533-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="a0533-141">Vous êtes prêt toolearn comment toosend les messages à partir de hub IoT de tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="a0533-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0533-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0533-142">Next steps</span></span>
<span data-ttu-id="a0533-143">[Créer une application de la fonction Azure et un stockage Azure compte tooprocess et magasin IoT hub messages][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="a0533-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md