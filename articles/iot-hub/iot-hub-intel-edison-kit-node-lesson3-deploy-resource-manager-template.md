---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 3 : créer l’application de la fonction | Documents Microsoft"
description: "application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "le stockage des données dans le cloud hello, les données stockées dans le cloud, service de cloud computing iot"
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
ms.openlocfilehash: 8ea0a4cdf978158d70e47eaed57e3de378b638d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="2ec50-104">Créer une application de fonction Azure et un compte de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="2ec50-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="2ec50-105">[Les fonctions Azure](../../articles/azure-functions/functions-overview.md) est une solution pour l’exécution de facilement *fonctions* (petits segments de code) dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="2ec50-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="2ec50-106">Une application de la fonction Azure héberge l’exécution de hello de vos fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec50-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="2ec50-107">Ce que vous allez faire</span><span class="sxs-lookup"><span data-stu-id="2ec50-107">What will you do</span></span>
<span data-ttu-id="2ec50-108">Utiliser un toocreate de modèle Azure Resource Manager, une application de la fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec50-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="2ec50-109">application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="2ec50-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="2ec50-110">compte de stockage Hello est utilisé pour la lecture hello persistante des copies des messages à partir de la table Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec50-110">hello storage account is used for reading hello persisted copies of messages from Azure table.</span></span> <span data-ttu-id="2ec50-111">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2ec50-111">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="2ec50-112">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="2ec50-112">What will you learn</span></span>
<span data-ttu-id="2ec50-113">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ec50-113">In this article, you will learn:</span></span>
* <span data-ttu-id="2ec50-114">Comment toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure ressources.</span><span class="sxs-lookup"><span data-stu-id="2ec50-114">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="2ec50-115">Comment toouse Azure application tooprocess messages de hub IoT de fonction et les écrire tooa table dans le stockage Azure Table.</span><span class="sxs-lookup"><span data-stu-id="2ec50-115">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="2ec50-116">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="2ec50-116">What do you need</span></span>
<span data-ttu-id="2ec50-117">Vous devez avoir accompli avec succès les étapes :</span><span class="sxs-lookup"><span data-stu-id="2ec50-117">You must have successfully completed:</span></span>
- <span data-ttu-id="2ec50-118">[Prise en main d’Intel Edison][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="2ec50-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="2ec50-119">[Créer votre Azure IoT Hub][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="2ec50-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="2ec50-120">Exemple d’application hello ouvert</span><span class="sxs-lookup"><span data-stu-id="2ec50-120">Open hello sample app</span></span>
<span data-ttu-id="2ec50-121">Ouvrez hello exemple de projet dans Visual Studio Code en exécutant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="2ec50-121">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Structure du référentiel][repo-structure]

* <span data-ttu-id="2ec50-123">fichier Hello Bonjour `app` sous-dossier est le fichier de source de la clé hello.</span><span class="sxs-lookup"><span data-stu-id="2ec50-123">hello file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="2ec50-124">Ce fichier source contient hello code toosend un message 20 fois tooyour IoT hub et blink hello DEL pour chaque message qu’elle envoie.</span><span class="sxs-lookup"><span data-stu-id="2ec50-124">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="2ec50-125">Hello `arm-template.json` fichier est le modèle Azure Resource Manager hello qui contient une application de la fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec50-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="2ec50-126">Hello `arm-template-param.json` fichier est hello configuration utilisé par le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2ec50-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="2ec50-127">Hello `ReceiveDeviceMessages` sous-dossier contient du code de Node.js hello pour hello fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec50-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="2ec50-128">Configurer des modèles Azure Resource Manager et créer des ressources dans Azure</span><span class="sxs-lookup"><span data-stu-id="2ec50-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="2ec50-129">Hello de mise à jour `arm-template-param.json` fichier dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2ec50-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Paramètres de modèle Azure Resource Manager][arm-template-parameters]

* <span data-ttu-id="2ec50-131">Remplacez **[nom de votre IoT Hub]** par **{nom de mon hub}**, que vous avez spécifié lorsque vous [avez créé votre IoT Hub et inscrit Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="2ec50-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="2ec50-132">Remplacez la **[chaîne de préfixe pour les nouvelles ressources]** par un préfixe de votre choix quelconque.</span><span class="sxs-lookup"><span data-stu-id="2ec50-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="2ec50-133">préfixe de Hello garantit que ce nom de ressource hello est globalement unique tooavoid conflit.</span><span class="sxs-lookup"><span data-stu-id="2ec50-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="2ec50-134">N’utilisez pas un numéro initial en préfixe de hello ou un tiret.</span><span class="sxs-lookup"><span data-stu-id="2ec50-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="2ec50-135">Une fois que vous mettez à jour hello `arm-template-param.json` file, déployer hello ressources tooAzure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2ec50-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="2ec50-136">Il prend environ cinq minutes toocreate ces ressources.</span><span class="sxs-lookup"><span data-stu-id="2ec50-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="2ec50-137">Lors de la création de la ressource hello est en cours d’exécution, vous pouvez déplacer sur l’article suivant de toohello.</span><span class="sxs-lookup"><span data-stu-id="2ec50-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="2ec50-138">Résumé</span><span class="sxs-lookup"><span data-stu-id="2ec50-138">Summary</span></span>
<span data-ttu-id="2ec50-139">Vous avez créé votre tooprocess d’application Azure fonction messages de hub IoT et un stockage Azure compte toostore ces messages.</span><span class="sxs-lookup"><span data-stu-id="2ec50-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="2ec50-140">Vous pouvez désormais déployer et exécuter des messages appareil-à-cloud de hello exemple toosend sur Edison.</span><span class="sxs-lookup"><span data-stu-id="2ec50-140">You can now deploy and run hello sample toosend device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ec50-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ec50-141">Next steps</span></span>
<span data-ttu-id="2ec50-142">[Exécuter un toosend d’application exemple messages appareil-à-cloud sur Intel Edison][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="2ec50-142">[Run a sample application toosend device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md