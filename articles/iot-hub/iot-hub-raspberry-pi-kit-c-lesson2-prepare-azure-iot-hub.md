---
title: "Connecter Raspberry Pi (C) à Azure IoT - Leçon 2 : Enregistrer un appareil | Microsoft Docs"
description: "Créez un groupe de ressources, créez un Azure IoT Hub et inscrivez votre Pi dans Azure IoT Hub à l’aide de l’interface de ligne de commande Azure."
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
ms.openlocfilehash: d7bfd8f6ae8d15dfe09f06a40a4ab415ff2e0a7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="75711-104">Création de votre IoT Hub et inscription de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="75711-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="75711-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="75711-105">What you will do</span></span>
* <span data-ttu-id="75711-106">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="75711-106">Create a resource group.</span></span>
* <span data-ttu-id="75711-107">Créez votre Azure IoT Hub dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="75711-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="75711-108">Ajoutez Raspberry Pi 3 à Azure IoT Hub à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="75711-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="75711-109">Lorsque vous utilisez l’interface de ligne de commande Azure pour ajouter Pi à votre IoT Hub, le service génère une clé permettant à Pi de s’authentifier auprès du service.</span><span class="sxs-lookup"><span data-stu-id="75711-109">When you use the Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="75711-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="75711-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="75711-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="75711-111">What you will learn</span></span>
<span data-ttu-id="75711-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="75711-112">In this article, you will learn:</span></span>
* <span data-ttu-id="75711-113">Utilisation de l’interface de ligne de commande Azure pour créer un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75711-113">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="75711-114">Création d’une identité d’appareil pour Pi dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75711-114">How to create a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="75711-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="75711-115">What you need</span></span>
* <span data-ttu-id="75711-116">Un compte Azure</span><span class="sxs-lookup"><span data-stu-id="75711-116">An Azure account</span></span>
* <span data-ttu-id="75711-117">Un Mac ou un ordinateur Windows avec l’interface de ligne de commande Azure installée</span><span class="sxs-lookup"><span data-stu-id="75711-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="75711-118">Création de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="75711-118">Create your IoT hub</span></span>
<span data-ttu-id="75711-119">Azure IoT Hub vous permet de connecter, surveiller et gérer des millions de ressources IoT.</span><span class="sxs-lookup"><span data-stu-id="75711-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="75711-120">Pour créer votre IoT Hub, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="75711-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="75711-121">Connectez-vous à votre compte Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="75711-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="75711-122">Après une connexion réussie, tous vos abonnements disponibles sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="75711-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="75711-123">Définissez l’abonnement par défaut que vous souhaitez utiliser en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="75711-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="75711-124">Vous trouverez `subscription ID or name` dans la sortie de la commande `az login` ou `az account list`.</span><span class="sxs-lookup"><span data-stu-id="75711-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="75711-125">Inscrivez le fournisseur en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="75711-125">Register the provider by running the following command.</span></span> <span data-ttu-id="75711-126">Les fournisseurs de ressources sont des services qui fournissent des ressources pour votre application.</span><span class="sxs-lookup"><span data-stu-id="75711-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="75711-127">Vous devez inscrire le fournisseur avant de déployer la ressource Azure proposée par le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="75711-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="75711-128">Créer un groupe de ressources nommé iot-sample dans la région ouest des États-Unis en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="75711-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="75711-129">`westus` est l’emplacement où vous créez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="75711-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="75711-130">Si vous souhaitez utiliser un autre emplacement, vous pouvez exécuter `az account list-locations -o table` pour voir tous les emplacements pris en charge par Azure.</span><span class="sxs-lookup"><span data-stu-id="75711-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="75711-131">Créez un IoT Hub dans le groupe de ressources iot-sample en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="75711-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="75711-132">Par défaut, l’outil crée un IoT Hub dans le niveau de tarification gratuit.</span><span class="sxs-lookup"><span data-stu-id="75711-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="75711-133">Pour plus d’informations, consultez la [tarification Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="75711-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="75711-134">Le nom de votre IoT Hub doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="75711-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="75711-135">Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="75711-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="75711-136">Inscription de Pi dans votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="75711-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="75711-137">Chaque appareil qui envoie des messages à votre IoT Hub et reçoit des messages de votre IoT Hub doit être inscrit sous un ID unique.</span><span class="sxs-lookup"><span data-stu-id="75711-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="75711-138">Inscrivez Pi dans votre hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="75711-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="75711-139">Résumé</span><span class="sxs-lookup"><span data-stu-id="75711-139">Summary</span></span>
<span data-ttu-id="75711-140">Vous avez créé un IoT Hub et enregistré Pi sous une identité d’appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75711-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="75711-141">Vous êtes prêt à découvrir comment envoyer des messages de Pi à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75711-141">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75711-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="75711-142">Next steps</span></span>
<span data-ttu-id="75711-143">[Créer une application de fonction Azure et un compte de stockage Azure pour traiter et stocker les messages du IoT Hub](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="75711-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

