---
title: "Appareil simulé et passerelle Azure IoT - Leçon 2 : Enregistrer un appareil | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, cloud de l’internet des objets, créer un appareil azure iot hub, ti sensortag, ti ble"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="0d717-103">Créer un Azure IoT Hub et inscrire votre appareil</span><span class="sxs-lookup"><span data-stu-id="0d717-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="0d717-104">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="0d717-104">What you will do</span></span>

- <span data-ttu-id="0d717-105">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0d717-105">Create a resource group</span></span>
- <span data-ttu-id="0d717-106">Créer votre premier IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0d717-106">Create your first IoT hub</span></span>
- <span data-ttu-id="0d717-107">Inscrire votre appareil dans votre IoT hub à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0d717-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="0d717-108">Lorsque vous inscrivez votre appareil à votre hub IoT, hello Azure IoT Hub service génère une clé pour votre tooauthenticate toouse de périphérique avec le service de hello.</span><span class="sxs-lookup"><span data-stu-id="0d717-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="0d717-109">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0d717-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0d717-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="0d717-110">What you will learn</span></span>

<span data-ttu-id="0d717-111">Dans cette leçon, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="0d717-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="0d717-112">Comment toouse hello CLI d’Azure toocreate un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0d717-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="0d717-113">Comment tooregister un périphérique dans un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0d717-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0d717-114">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="0d717-114">What you need</span></span>

- <span data-ttu-id="0d717-115">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="0d717-115">An active Azure subscription.</span></span> <span data-ttu-id="0d717-116">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0d717-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="0d717-117">Vous devez avoir hello que CLI d’Azure installé.</span><span class="sxs-lookup"><span data-stu-id="0d717-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="0d717-118">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="0d717-118">Create an IoT hub</span></span>

<span data-ttu-id="0d717-119">toocreate un IoT hub, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0d717-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="0d717-120">La connexion tooyour compte Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0d717-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="0d717-121">Une fois la connexion établie, tous vos abonnements disponibles sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="0d717-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="0d717-122">Définir la valeur par défaut de hello abonnement Azure que vous souhaitez toouse en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0d717-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="0d717-123">`subscription ID or name`se trouvent dans la sortie de hello Hello `az login` ou hello `az account list` commande.</span><span class="sxs-lookup"><span data-stu-id="0d717-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="0d717-124">Inscription du fournisseur de hello en hello suivant de commande en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0d717-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="0d717-125">Les fournisseurs de ressources sont des services qui fournissent des ressources pour votre application.</span><span class="sxs-lookup"><span data-stu-id="0d717-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="0d717-126">Vous devez inscrire le fournisseur de hello avant de pouvoir déployer hello ressource Azure qui hello offres du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="0d717-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="0d717-127">Créer un groupe de ressources nommé `iot-gateway` dans la région ouest des États-Unis hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0d717-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="0d717-128">`westus`est l’emplacement hello vous créez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0d717-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="0d717-129">Si vous voulez toouse un autre emplacement, vous pouvez exécuter `az account list-locations -o table` toosee tous hello emplacements Azure prend en charge.</span><span class="sxs-lookup"><span data-stu-id="0d717-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="0d717-130">Créez un hub IoT Bonjour `iot-gateway` groupe de ressources en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0d717-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="0d717-131">Par défaut, hello outil crée un IoT Hub niveau de tarification gratuit hello.</span><span class="sxs-lookup"><span data-stu-id="0d717-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="0d717-132">Pour plus d’informations, consultez la [tarification Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="0d717-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="0d717-133">nom de Hello de votre IoT hub doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="0d717-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="0d717-134">Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0d717-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="0d717-135">Inscrire votre appareil dans votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0d717-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="0d717-136">Chaque périphérique qui envoie IoT hub tooyour de messages et reçoit des messages à partir de votre IoT hub doit être enregistré avec un ID unique.</span><span class="sxs-lookup"><span data-stu-id="0d717-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="0d717-137">Inscrivez votre appareil dans votre Azure IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0d717-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="0d717-138">Résumé</span><span class="sxs-lookup"><span data-stu-id="0d717-138">Summary</span></span>

<span data-ttu-id="0d717-139">Vous avez créé un IoT Hub et inscrit votre appareil logique sous une identité d’appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0d717-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="0d717-140">Vous êtes prêt toolearn tooconfigure et exécuter une passerelle exemples application toosend de données à partir de votre concentrateur périphérique physique tooyour IoT hello de cloud.</span><span class="sxs-lookup"><span data-stu-id="0d717-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d717-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d717-141">Next steps</span></span>
[<span data-ttu-id="0d717-142">Configurer et exécuter un exemple d’application de téléchargement cloud d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="0d717-142">Configure and run a simulated device cloud upload sample application</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)