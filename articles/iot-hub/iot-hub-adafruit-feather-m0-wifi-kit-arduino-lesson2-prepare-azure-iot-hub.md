---
title: "Connecter Arduino à Azure IoT - Leçon 2 : Enregistrer un appareil | Microsoft Docs"
description: "Créez un groupe de ressources, créez un Azure IoT Hub et inscrivez votre carte Adafruit Feather M0 WiFi dans Azure IoT Hub à l’aide de l’interface de ligne de commande Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "connexion arduino au cloud, azure iot hub, internet des objets cloud, azure iot hub créer un appareil, arduino cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c5ad5e900671c7cedd3cdad2c2aa345315de223b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="b2fcb-104">Créer votre IoT Hub et inscrire votre carte Adafruit Feather M0 WiFi Arduino</span><span class="sxs-lookup"><span data-stu-id="b2fcb-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="b2fcb-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="b2fcb-105">What you will do</span></span>
* <span data-ttu-id="b2fcb-106">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-106">Create a resource group.</span></span>
* <span data-ttu-id="b2fcb-107">Créez votre Azure IoT Hub dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="b2fcb-108">Ajoutez votre carte Arduino à Azure IoT Hub à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-108">Add your Arduino board to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="b2fcb-109">Lorsque vous utilisez l’interface de ligne de commande Azure pour ajouter votre carte Arduino à votre IoT Hub, le service génère une clé permettant à votre carte Arduino de s’authentifier auprès du service.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-109">When you use the Azure CLI to add your Arduino board to your IoT hub, the service generates a key for your Arduino board to authenticate with the service.</span></span> <span data-ttu-id="b2fcb-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshoot].</span><span class="sxs-lookup"><span data-stu-id="b2fcb-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b2fcb-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="b2fcb-111">What you will learn</span></span>
<span data-ttu-id="b2fcb-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b2fcb-112">In this article, you will learn:</span></span>
* <span data-ttu-id="b2fcb-113">Utilisation de l’interface de ligne de commande Azure pour créer un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-113">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="b2fcb-114">Comment créer une identité d’appareil pour votre carte Arduino dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-114">How to create a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b2fcb-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="b2fcb-115">What you need</span></span>
* <span data-ttu-id="b2fcb-116">Un compte Azure</span><span class="sxs-lookup"><span data-stu-id="b2fcb-116">An Azure account</span></span>
* <span data-ttu-id="b2fcb-117">Un ordinateur avec l’interface de ligne de commande Azure installée</span><span class="sxs-lookup"><span data-stu-id="b2fcb-117">A computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="b2fcb-118">Création de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b2fcb-118">Create your IoT hub</span></span>
<span data-ttu-id="b2fcb-119">Azure IoT Hub vous permet de connecter, surveiller et gérer des millions de ressources IoT.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="b2fcb-120">Pour créer votre IoT Hub, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b2fcb-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="b2fcb-121">Connectez-vous à votre compte Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2fcb-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="b2fcb-122">Après une connexion réussie, tous vos abonnements disponibles sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="b2fcb-123">Définissez l’abonnement par défaut que vous souhaitez utiliser en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2fcb-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="b2fcb-124">Vous trouverez `subscription ID or name` dans la sortie de la commande `az login` ou `az account list`.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="b2fcb-125">Inscrivez le fournisseur en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-125">Register the provider by running the following command.</span></span> <span data-ttu-id="b2fcb-126">Les fournisseurs de ressources sont des services qui fournissent des ressources pour votre application.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="b2fcb-127">Vous devez inscrire le fournisseur avant de déployer la ressource Azure proposée par le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="b2fcb-128">Créer un groupe de ressources nommé iot-sample dans la région ouest des États-Unis en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2fcb-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="b2fcb-129">`westus` est l’emplacement où vous créez votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="b2fcb-130">Si vous souhaitez utiliser un autre emplacement, vous pouvez exécuter `az account list-locations -o table` pour voir tous les emplacements pris en charge par Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="b2fcb-131">Créez un IoT Hub dans le groupe de ressources iot-sample en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2fcb-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="b2fcb-132">Par défaut, l’outil crée un IoT Hub dans le niveau de tarification gratuit.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="b2fcb-133">Pour plus d’informations, consultez la [tarification Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="b2fcb-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="b2fcb-134">Le nom de votre IoT Hub doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="b2fcb-135">Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="b2fcb-136">Inscrire votre carte Arduino dans votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b2fcb-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="b2fcb-137">Chaque appareil qui envoie des messages à votre IoT Hub et reçoit des messages de votre IoT Hub doit être inscrit sous un ID unique.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="b2fcb-138">Inscrivez votre carte Arduino dans votre IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b2fcb-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="b2fcb-139">Résumé</span><span class="sxs-lookup"><span data-stu-id="b2fcb-139">Summary</span></span>
<span data-ttu-id="b2fcb-140">Vous avez créé un IoT Hub et enregistré votre carte Arduino sous une identité d’appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="b2fcb-141">Vous êtes prêt à découvrir comment envoyer des messages de votre carte Arduino à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b2fcb-141">You're ready to learn how to send messages from your Arduino board to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2fcb-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b2fcb-142">Next steps</span></span>
<span data-ttu-id="b2fcb-143">[Créer une application de fonction Azure et un compte de stockage Azure pour traiter et stocker les messages du IoT Hub][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="b2fcb-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md