---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 3 : Créer un conteneur de fonctions | Microsoft Docs"
description: "L’application de fonction Azure écoute les événements d’Azure IoT Hub, traite les messages entrants et les écrit dans le stockage Table Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "stockage de données dans le cloud, les données stockées dans le cloud, service cloud iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 37ee5962-95ce-40e8-8162-17e735eaec21
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6ada1cbbb560f1373346eca561dceb28d7ca7242
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="16ce5-104">Créer une application de fonction Azure et un compte de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="16ce5-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="16ce5-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) est une solution conçue pour exécuter facilement des petits morceaux de code (« *functions* ») dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="16ce5-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="16ce5-106">Une application de fonction Azure héberge l’exécution de vos fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="16ce5-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="16ce5-107">Ce que vous allez faire</span><span class="sxs-lookup"><span data-stu-id="16ce5-107">What will you do</span></span>
<span data-ttu-id="16ce5-108">Utilisez un modèle Azure Resource Manager pour créer une application de fonction Azure et un compte de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="16ce5-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="16ce5-109">L’application de fonction Azure écoute les événements d’Azure IoT Hub, traite les messages entrants et les écrit dans le stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="16ce5-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="16ce5-110">Le compte de stockage est utilisé pour la lecture des copies persistantes des messages à partir de la table Azure.</span><span class="sxs-lookup"><span data-stu-id="16ce5-110">The storage account is used for reading the persisted copies of messages from Azure table.</span></span> <span data-ttu-id="16ce5-111">Si vous rencontrez des problèmes, recherchez des solutions sur la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="16ce5-111">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="16ce5-112">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="16ce5-112">What will you learn</span></span>
<span data-ttu-id="16ce5-113">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="16ce5-113">In this article, you will learn:</span></span>
* <span data-ttu-id="16ce5-114">Commet utiliser [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) pour déployer des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="16ce5-114">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="16ce5-115">Comment utiliser une application de fonction Azure pour traiter les messages de l’IoT Hub et les écrire dans une table du stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="16ce5-115">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="16ce5-116">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="16ce5-116">What do you need</span></span>
<span data-ttu-id="16ce5-117">Vous devez avoir accompli avec succès les étapes :</span><span class="sxs-lookup"><span data-stu-id="16ce5-117">You must have successfully completed:</span></span>
- <span data-ttu-id="16ce5-118">[Prise en main d’Intel Edison][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="16ce5-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="16ce5-119">[Créer votre Azure IoT Hub][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="16ce5-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="16ce5-120">Ouvrir l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="16ce5-120">Open the sample app</span></span>
<span data-ttu-id="16ce5-121">Ouvrez l’exemple de projet dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="16ce5-121">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Structure du référentiel][repo-structure]

* <span data-ttu-id="16ce5-123">Le fichier se trouvant dans le sous-dossier `app` est le fichier source clé.</span><span class="sxs-lookup"><span data-stu-id="16ce5-123">The file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="16ce5-124">Ce fichier source contient le code pour envoyer un message 20 fois à votre IoT hub et faire clignoter la LED pour chaque message envoyé.</span><span class="sxs-lookup"><span data-stu-id="16ce5-124">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="16ce5-125">Le fichier `arm-template.json` est le modèle Azure Resource Manager qui contient une application de fonction Azure et un compte de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="16ce5-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="16ce5-126">Le fichier `arm-template-param.json` est le fichier de configuration utilisé par le modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="16ce5-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="16ce5-127">Le sous-dossier `ReceiveDeviceMessages` contient le code Node.js pour la fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="16ce5-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="16ce5-128">Configurer des modèles Azure Resource Manager et créer des ressources dans Azure</span><span class="sxs-lookup"><span data-stu-id="16ce5-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="16ce5-129">Mettez à jour le fichier `arm-template-param.json` dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="16ce5-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Paramètres de modèle Azure Resource Manager][arm-template-parameters]

* <span data-ttu-id="16ce5-131">Remplacez **[nom de votre IoT Hub]** par **{nom de mon hub}**, que vous avez spécifié lorsque vous [avez créé votre IoT Hub et inscrit Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="16ce5-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="16ce5-132">Remplacez la **[chaîne de préfixe pour les nouvelles ressources]** par un préfixe de votre choix quelconque.</span><span class="sxs-lookup"><span data-stu-id="16ce5-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="16ce5-133">Le préfixe vous assure que le nom de ressource est globalement unique pour éviter tout conflit.</span><span class="sxs-lookup"><span data-stu-id="16ce5-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="16ce5-134">N’utilisez pas de tiret ni de chiffre initial dans le préfixe.</span><span class="sxs-lookup"><span data-stu-id="16ce5-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="16ce5-135">Une fois que vous avez mis à jour le fichier `arm-template-param.json`, déployez les ressources dans Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="16ce5-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="16ce5-136">La création de ces ressources prend environ cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="16ce5-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="16ce5-137">Pendant la création de ressources, vous pouvez passer à l’article suivant.</span><span class="sxs-lookup"><span data-stu-id="16ce5-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="16ce5-138">Résumé</span><span class="sxs-lookup"><span data-stu-id="16ce5-138">Summary</span></span>
<span data-ttu-id="16ce5-139">Vous avez créé votre application de fonction Azure pour traiter les messages de l’IoT Hub et un compte de Stockage Azure pour stocker ces messages.</span><span class="sxs-lookup"><span data-stu-id="16ce5-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="16ce5-140">Vous pouvez désormais déployer et exécuter l’exemple pour envoyer des messages appareil-à-cloud sur Edison.</span><span class="sxs-lookup"><span data-stu-id="16ce5-140">You can now deploy and run the sample to send device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16ce5-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="16ce5-141">Next steps</span></span>
<span data-ttu-id="16ce5-142">[Exécuter un exemple d’application pour envoyer des messages appareil-à-cloud sur Intel Edison][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="16ce5-142">[Run a sample application to send device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md