---
title: "Se connecter framboises Pi (nœud) tooAzure IoT - leçon 3 : déploiement d’un modèle | Documents Microsoft"
description: "application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "le stockage des données dans le cloud hello, les données stockées dans le cloud, service de cloud computing iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b6c0a9530cb80e3f78c0e96037f6f3942b602aea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="d12df-104">Créer une application de fonction Azure et un compte de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="d12df-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="d12df-105">[Les fonctions Azure](../azure-functions/functions-overview.md) est une solution pour l’exécution de facilement *fonctions* (petits segments de code) dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d12df-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="d12df-106">Une application de la fonction Azure héberge l’exécution de hello de vos fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d12df-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d12df-107">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="d12df-107">What you will do</span></span>
<span data-ttu-id="d12df-108">Utiliser un toocreate de modèle Azure Resource Manager, une application de la fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d12df-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="d12df-109">application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="d12df-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="d12df-110">Si vous rencontrez des problèmes, rechercher des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d12df-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d12df-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="d12df-111">What you will learn</span></span>
<span data-ttu-id="d12df-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d12df-112">In this article, you will learn:</span></span>

* <span data-ttu-id="d12df-113">Comment toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure ressources.</span><span class="sxs-lookup"><span data-stu-id="d12df-113">How toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="d12df-114">Comment toouse Azure application tooprocess messages de hub IoT de fonction et les écrire tooa table dans le stockage Azure Table.</span><span class="sxs-lookup"><span data-stu-id="d12df-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d12df-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="d12df-115">What you need</span></span>
<span data-ttu-id="d12df-116">Vous devez avoir accompli avec succès les étapes :</span><span class="sxs-lookup"><span data-stu-id="d12df-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="d12df-117">Prise en main de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="d12df-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="d12df-118">Créer votre Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d12df-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-hello-sample-app"></a><span data-ttu-id="d12df-119">Exemple d’application hello ouvert</span><span class="sxs-lookup"><span data-stu-id="d12df-119">Open hello sample app</span></span>
<span data-ttu-id="d12df-120">Ouvrez hello exemple de projet dans Visual Studio Code en exécutant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d12df-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Structure du référentiel](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="d12df-122">Hello `app.js` fichier Bonjour `app` sous-dossier est le fichier de source de la clé hello.</span><span class="sxs-lookup"><span data-stu-id="d12df-122">hello `app.js` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="d12df-123">Ce fichier source contient hello code toosend un message 20 fois tooyour IoT hub et blink hello DEL pour chaque message qu’elle envoie.</span><span class="sxs-lookup"><span data-stu-id="d12df-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="d12df-124">Hello `arm-template.json` fichier est le modèle Azure Resource Manager hello qui contient une application de la fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d12df-124">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="d12df-125">Hello `arm-template-param.json` fichier est hello configuration utilisé par le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d12df-125">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="d12df-126">Hello `ReceiveDeviceMessages` sous-dossier contient du code de Node.js hello pour hello fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="d12df-126">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="d12df-127">Configurer des modèles Azure Resource Manager et créer des ressources dans Azure</span><span class="sxs-lookup"><span data-stu-id="d12df-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="d12df-128">Hello de mise à jour `arm-template-param.json` fichier dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d12df-128">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Paramètres de modèle Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="d12df-130">Remplacez **[nom de votre IoT Hub]** par **{nom de mon hub}** que vous avez spécifié lorsque vous [avez créé votre IoT Hub et inscrit Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="d12df-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="d12df-131">Remplacez la **[chaîne de préfixe pour les nouvelles ressources]** par un préfixe de votre choix quelconque.</span><span class="sxs-lookup"><span data-stu-id="d12df-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="d12df-132">préfixe de Hello garantit que ce nom de ressource hello est globalement unique tooavoid conflit.</span><span class="sxs-lookup"><span data-stu-id="d12df-132">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="d12df-133">N’utilisez pas un numéro initial en préfixe de hello ou un tiret.</span><span class="sxs-lookup"><span data-stu-id="d12df-133">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="d12df-134">Une fois que vous mettez à jour hello `arm-template-param.json` file, déployer hello ressources tooAzure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d12df-134">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="d12df-135">Il prend environ cinq minutes toocreate ces ressources.</span><span class="sxs-lookup"><span data-stu-id="d12df-135">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="d12df-136">Lors de la création de la ressource hello est en cours d’exécution, vous pouvez déplacer sur l’article suivant de toohello.</span><span class="sxs-lookup"><span data-stu-id="d12df-136">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="d12df-137">Résumé</span><span class="sxs-lookup"><span data-stu-id="d12df-137">Summary</span></span>
<span data-ttu-id="d12df-138">Vous avez créé votre tooprocess d’application Azure fonction messages de hub IoT et un stockage Azure compte toostore ces messages.</span><span class="sxs-lookup"><span data-stu-id="d12df-138">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="d12df-139">Vous pouvez désormais déployer et exécuter des messages appareil-à-cloud de hello exemple toosend sur Pi.</span><span class="sxs-lookup"><span data-stu-id="d12df-139">You can now deploy and run hello sample toosend device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d12df-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d12df-140">Next steps</span></span>
[<span data-ttu-id="d12df-141">Exécuter un toosend d’application exemple messages appareil-à-cloud sur framboises Pi 3</span><span class="sxs-lookup"><span data-stu-id="d12df-141">Run a sample application toosend device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

