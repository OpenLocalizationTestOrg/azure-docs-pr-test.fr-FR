---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 2 : Enregistrer un appareil | Microsoft Docs"
description: "Créez un groupe de ressources, créez un Azure IoT Hub et inscrivez Edison dans Azure IoT Hub à l’aide de l’interface de ligne de commande Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: c1465cc2-d0d9-4326-967c-64d95b61dd54
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 81584c1b7314c4331ac059b8e3ed782970588ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="7362b-103">Créer votre IoT Hub et inscrire Intel Edison</span><span class="sxs-lookup"><span data-stu-id="7362b-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="7362b-104">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="7362b-104">What you will do</span></span>
* <span data-ttu-id="7362b-105">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7362b-105">Create a resource group.</span></span>
* <span data-ttu-id="7362b-106">Créez votre Azure IoT Hub dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7362b-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="7362b-107">Ajoutez Intel Edison à Azure IoT Hub à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="7362b-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="7362b-108">Lorsque vous utilisez l’interface de ligne de commande Azure pour ajouter Edison à votre IoT Hub, le service génère une clé permettant à Edison de s’authentifier auprès du service.</span><span class="sxs-lookup"><span data-stu-id="7362b-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="7362b-109">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="7362b-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7362b-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="7362b-110">What you will learn</span></span>
<span data-ttu-id="7362b-111">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7362b-111">In this article, you will learn:</span></span>
* <span data-ttu-id="7362b-112">Utilisation de l’interface de ligne de commande Azure pour créer un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7362b-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="7362b-113">Création d’une identité d’appareil pour Edison dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7362b-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7362b-114">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="7362b-114">What you need</span></span>
* <span data-ttu-id="7362b-115">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="7362b-115">An Azure account.</span></span> <span data-ttu-id="7362b-116">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7362b-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="7362b-117">Vous devez avoir installé l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="7362b-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="7362b-118">Création de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7362b-118">Create your IoT hub</span></span>
<span data-ttu-id="7362b-119">Azure IoT Hub vous permet de connecter, surveiller et gérer des millions de ressources IoT.</span><span class="sxs-lookup"><span data-stu-id="7362b-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="7362b-120">Pour créer votre IoT Hub, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7362b-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="7362b-121">Connectez-vous à votre compte Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7362b-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="7362b-122">Après une connexion réussie, tous vos abonnements disponibles sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="7362b-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="7362b-123">Définissez l’abonnement par défaut que vous souhaitez utiliser en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7362b-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="7362b-124">Vous trouverez `subscription ID or name` dans la sortie de la commande `az login` ou `az account list`.</span><span class="sxs-lookup"><span data-stu-id="7362b-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="7362b-125">Inscrivez le fournisseur en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="7362b-125">Register the provider by running the following command.</span></span> <span data-ttu-id="7362b-126">Les fournisseurs de ressources sont des services qui fournissent des ressources pour votre application.</span><span class="sxs-lookup"><span data-stu-id="7362b-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="7362b-127">Vous devez inscrire le fournisseur avant de déployer la ressource Azure proposée par le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="7362b-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="7362b-128">Créer un groupe de ressources nommé iot-sample dans la région ouest des États-Unis en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7362b-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="7362b-129">`westus` est l’emplacement où vous créez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7362b-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="7362b-130">Si vous souhaitez utiliser un autre emplacement, vous pouvez exécuter `az account list-locations -o table` pour voir tous les emplacements pris en charge par Azure.</span><span class="sxs-lookup"><span data-stu-id="7362b-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="7362b-131">Créez un IoT Hub dans le groupe de ressources iot-sample en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7362b-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="7362b-132">Par défaut, l’outil crée un IoT Hub dans le niveau de tarification gratuit.</span><span class="sxs-lookup"><span data-stu-id="7362b-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="7362b-133">Pour plus d’informations, consultez la [tarification Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="7362b-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="7362b-134">Le nom de votre IoT Hub doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="7362b-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="7362b-135">Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="7362b-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="7362b-136">Inscription d’Edison dans votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7362b-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="7362b-137">Chaque appareil qui envoie des messages à votre IoT Hub et reçoit des messages de votre IoT Hub doit être inscrit sous un ID unique.</span><span class="sxs-lookup"><span data-stu-id="7362b-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="7362b-138">Inscrivez Edison dans votre IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7362b-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="7362b-139">Résumé</span><span class="sxs-lookup"><span data-stu-id="7362b-139">Summary</span></span>
<span data-ttu-id="7362b-140">Vous avez créé un IoT Hub et enregistré Edison sous une identité d’appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7362b-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="7362b-141">Vous êtes prêt à découvrir comment envoyer des messages d’Edison à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7362b-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7362b-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7362b-142">Next steps</span></span>
<span data-ttu-id="7362b-143">[Créer une application de fonction Azure et un compte de stockage Azure pour traiter et stocker les messages du IoT Hub][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="7362b-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md