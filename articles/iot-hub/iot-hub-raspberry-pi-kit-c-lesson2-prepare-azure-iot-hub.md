---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 2 : inscription de l’appareil | Documents Microsoft"
description: "Créer un groupe de ressources, créez un Azure IoT hub, inscrire et Pi dans hello Azure IoT hub aide hello CLI d’Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: raspberry pi cloud, connexion pi cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 473658c5a8e1e0d4cfced0efafbad2640a1e0696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="c7ca9-104">Création de votre IoT Hub et inscription de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="c7ca9-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c7ca9-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="c7ca9-105">What you will do</span></span>
* <span data-ttu-id="c7ca9-106">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-106">Create a resource group.</span></span>
* <span data-ttu-id="c7ca9-107">Créer votre concentrateur Azure IoT dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="c7ca9-108">Ajouter framboises Pi 3 toohello Azure IoT hub à l’aide de hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="c7ca9-109">Lorsque vous utilisez hub IoT de hello CLI d’Azure tooadd Pi tooyour, service de hello génère une clé pour tooauthenticate Pi avec le service de hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-109">When you use hello Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="c7ca9-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c7ca9-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="c7ca9-111">What you will learn</span></span>
<span data-ttu-id="c7ca9-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c7ca9-112">In this article, you will learn:</span></span>
* <span data-ttu-id="c7ca9-113">Comment toouse hello CLI d’Azure toocreate un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="c7ca9-114">Comment toocreate une identité d’appareil de Pi dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-114">How toocreate a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c7ca9-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="c7ca9-115">What you need</span></span>
* <span data-ttu-id="c7ca9-116">Un compte Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-116">An Azure account</span></span>
* <span data-ttu-id="c7ca9-117">Un Mac ou un ordinateur Windows avec hello CLI d’Azure installé</span><span class="sxs-lookup"><span data-stu-id="c7ca9-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="c7ca9-118">Création de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c7ca9-118">Create your IoT hub</span></span>
<span data-ttu-id="c7ca9-119">Azure IoT Hub vous permet de connecter, surveiller et gérer des millions de ressources IoT.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="c7ca9-120">toocreate votre hub IoT, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c7ca9-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="c7ca9-121">La connexion tooyour compte Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c7ca9-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="c7ca9-122">Après une connexion réussie, tous vos abonnements disponibles sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="c7ca9-123">Définissez hello abonnement de valeur par défaut que vous souhaitez toouse en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c7ca9-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="c7ca9-124">`subscription ID or name`se trouvent dans la sortie de hello Hello `az login` ou hello `az account list` commande.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="c7ca9-125">Inscription du fournisseur de hello en hello suivant de commande en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="c7ca9-126">Les fournisseurs de ressources sont des services qui fournissent des ressources pour votre application.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="c7ca9-127">Vous devez inscrire le fournisseur de hello avant de pouvoir déployer hello ressource Azure qui hello offres du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="c7ca9-128">Créer un groupe de ressources nommé iot-exemple dans la région ouest des États-Unis hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c7ca9-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="c7ca9-129">`westus`est l’emplacement hello vous créez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="c7ca9-130">Si vous voulez toouse un autre emplacement, vous pouvez exécuter `az account list-locations -o table` toosee tous hello emplacements Azure prend en charge.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="c7ca9-131">Créez un hub IoT hello iot-exemple groupe de ressources en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c7ca9-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="c7ca9-132">Par défaut, hello outil crée un IoT Hub niveau de tarification gratuit hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="c7ca9-133">Pour plus d’informations, consultez la [tarification Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-134">nom de Hello de votre IoT hub doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="c7ca9-135">Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="c7ca9-136">Inscription de Pi dans votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c7ca9-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="c7ca9-137">Chaque périphérique qui envoie IoT hub tooyour de messages et reçoit des messages à partir de votre IoT hub doit être enregistré avec un ID unique.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="c7ca9-138">Inscrivez Pi dans votre hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c7ca9-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="c7ca9-139">Résumé</span><span class="sxs-lookup"><span data-stu-id="c7ca9-139">Summary</span></span>
<span data-ttu-id="c7ca9-140">Vous avez créé un IoT Hub et enregistré Pi sous une identité d’appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="c7ca9-141">Vous êtes prêt toolearn comment toosend les messages à partir de hub IoT de tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-141">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7ca9-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7ca9-142">Next steps</span></span>
<span data-ttu-id="c7ca9-143">[Créer une application de la fonction Azure et un stockage Azure compte tooprocess et magasin IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

