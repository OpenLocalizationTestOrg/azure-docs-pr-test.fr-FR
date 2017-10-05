---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 2 : Enregistrer un appareil | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, cloud de l’internet des objets, créer un appareil azure iot hub, ti sensortag, ti ble"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 685a479583f5f11f57bef22dc5881285bb1f70d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="ad02b-103">Créer un Azure IoT Hub et inscrire votre appareil</span><span class="sxs-lookup"><span data-stu-id="ad02b-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ad02b-104">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="ad02b-104">What you will do</span></span>

- <span data-ttu-id="ad02b-105">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="ad02b-105">Create a resource group</span></span>
- <span data-ttu-id="ad02b-106">Créer votre premier IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ad02b-106">Create your first IoT hub</span></span>
- <span data-ttu-id="ad02b-107">Inscrire votre appareil dans votre IoT Hub à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="ad02b-107">Register your device in your IoT hub by using the Azure CLI.</span></span> 

<span data-ttu-id="ad02b-108">Lorsque vous inscrivez votre appareil dans votre IoT Hub, le service Azure IoT Hub génère une clé permettant à votre appareil de s’authentifier auprès du service.</span><span class="sxs-lookup"><span data-stu-id="ad02b-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span></span> 

<span data-ttu-id="ad02b-109">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ad02b-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ad02b-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="ad02b-110">What you will learn</span></span>

<span data-ttu-id="ad02b-111">Dans cette leçon, vous allez apprendre ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ad02b-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="ad02b-112">Utilisation de l’interface de ligne de commande Azure pour créer un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad02b-112">How to use the Azure CLI to create an IoT hub.</span></span>
- <span data-ttu-id="ad02b-113">l’inscription d’un appareil dans un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad02b-113">How to register a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ad02b-114">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="ad02b-114">What you need</span></span>

- <span data-ttu-id="ad02b-115">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="ad02b-115">An active Azure subscription.</span></span> <span data-ttu-id="ad02b-116">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ad02b-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="ad02b-117">Vous devez avoir installé l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="ad02b-117">You should have the Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="ad02b-118">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="ad02b-118">Create an IoT hub</span></span>

<span data-ttu-id="ad02b-119">Pour créer un IoT Hub, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ad02b-119">To create an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="ad02b-120">Connectez-vous à votre compte Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ad02b-120">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="ad02b-121">Une fois la connexion établie, tous vos abonnements disponibles sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="ad02b-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="ad02b-122">Définissez l’abonnement Azure par défaut que vous souhaitez utiliser en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ad02b-122">Set the default Azure subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="ad02b-123">Vous trouverez `subscription ID or name` dans la sortie de la commande `az login` ou `az account list`.</span><span class="sxs-lookup"><span data-stu-id="ad02b-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="ad02b-124">Inscrivez le fournisseur en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="ad02b-124">Register the provider by running the following command.</span></span> <span data-ttu-id="ad02b-125">Les fournisseurs de ressources sont des services qui fournissent des ressources pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ad02b-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="ad02b-126">Vous devez inscrire le fournisseur avant de déployer la ressource Azure proposée par le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="ad02b-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="ad02b-127">Créez un groupe de ressources nommé `iot-gateway` dans la région États-Unis de l’Ouest en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ad02b-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="ad02b-128">`westus` est l’emplacement où vous créez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ad02b-128">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="ad02b-129">Si vous souhaitez utiliser un autre emplacement, vous pouvez exécuter `az account list-locations -o table` pour voir tous les emplacements pris en charge par Azure.</span><span class="sxs-lookup"><span data-stu-id="ad02b-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="ad02b-130">Créez un IoT Hub dans le groupe de ressources `iot-gateway` en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ad02b-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="ad02b-131">Par défaut, l’outil crée un IoT Hub dans le niveau de tarification gratuit.</span><span class="sxs-lookup"><span data-stu-id="ad02b-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="ad02b-132">Pour plus d’informations, consultez la [tarification Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="ad02b-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="ad02b-133">Le nom de votre IoT Hub doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="ad02b-133">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="ad02b-134">Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ad02b-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="ad02b-135">Inscrire votre appareil dans votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ad02b-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="ad02b-136">Chaque appareil qui envoie des messages à votre IoT Hub et reçoit des messages de votre IoT Hub doit être inscrit sous un ID unique.</span><span class="sxs-lookup"><span data-stu-id="ad02b-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="ad02b-137">Inscrivez votre appareil dans votre Azure IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ad02b-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="ad02b-138">Résumé</span><span class="sxs-lookup"><span data-stu-id="ad02b-138">Summary</span></span>

<span data-ttu-id="ad02b-139">Vous avez créé un IoT Hub et inscrit votre appareil logique sous une identité d’appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad02b-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="ad02b-140">Vous êtes prêt à découvrir comment configurer et exécuter un exemple d’application de la passerelle pour envoyer des données de votre appareil physique à votre IoT Hub dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="ad02b-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad02b-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad02b-141">Next steps</span></span>
[<span data-ttu-id="ad02b-142">Configurer et exécuter l’exemple d’application BLE</span><span class="sxs-lookup"><span data-stu-id="ad02b-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)