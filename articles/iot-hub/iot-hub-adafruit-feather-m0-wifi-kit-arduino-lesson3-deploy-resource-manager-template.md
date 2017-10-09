---
title: "Connect Arduino (C) tooAzure IoT - leçon 3 : déploiement d’un modèle | Documents Microsoft"
description: "application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "le stockage des données dans le cloud hello, les données stockées dans le cloud, service de cloud computing iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6a84a6d3c5263a85c8997cf69fe446d73ab7a5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="9498e-104">Créer une application de fonction Azure et un compte de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="9498e-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="9498e-105">[Les fonctions Azure](../../articles/azure-functions/functions-overview.md) est une solution pour l’exécution de facilement *fonctions* (petits segments de code) dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="9498e-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="9498e-106">Une application de la fonction Azure héberge l’exécution de hello de vos fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9498e-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="9498e-107">Ce que vous allez faire</span><span class="sxs-lookup"><span data-stu-id="9498e-107">What will you do</span></span>
<span data-ttu-id="9498e-108">Utiliser un toocreate de modèle Azure Resource Manager, une application de la fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="9498e-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="9498e-109">application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="9498e-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="9498e-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page de votre carte mère Adafruit estompe M0 Wi-Fi Arduino dépannage](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9498e-110">If you have any problems, look for solutions on hello [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="9498e-111">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="9498e-111">What will you learn</span></span>
<span data-ttu-id="9498e-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9498e-112">In this article, you will learn:</span></span>
* <span data-ttu-id="9498e-113">Comment toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure ressources.</span><span class="sxs-lookup"><span data-stu-id="9498e-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="9498e-114">Comment toouse Azure application tooprocess messages de hub IoT de fonction et les écrire tooa table dans le stockage Azure Table.</span><span class="sxs-lookup"><span data-stu-id="9498e-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="9498e-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="9498e-115">What do you need</span></span>
<span data-ttu-id="9498e-116">Vous devez avoir accompli avec succès les étapes :</span><span class="sxs-lookup"><span data-stu-id="9498e-116">You must have successfully completed:</span></span>
- <span data-ttu-id="9498e-117">[Bien démarrer avec la carte Arduino][get-started]</span><span class="sxs-lookup"><span data-stu-id="9498e-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="9498e-118">[Créer votre Azure IoT Hub][create-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="9498e-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="9498e-119">Exemple d’application hello ouvert</span><span class="sxs-lookup"><span data-stu-id="9498e-119">Open hello sample app</span></span>
<span data-ttu-id="9498e-120">Ouvrez hello exemple de projet dans Visual Studio Code en exécutant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="9498e-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Structure du référentiel][repo-structure]

* <span data-ttu-id="9498e-122">Hello `app.ino` fichier Bonjour `app` sous-dossier est le fichier de source de la clé hello.</span><span class="sxs-lookup"><span data-stu-id="9498e-122">hello `app.ino` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="9498e-123">Ce fichier source contient hello code toosend un message 20 fois tooyour IoT hub et blink hello DEL pour chaque message qu’elle envoie.</span><span class="sxs-lookup"><span data-stu-id="9498e-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="9498e-124">Hello `config.json` contient les paramètres de configuration requis.</span><span class="sxs-lookup"><span data-stu-id="9498e-124">hello `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="9498e-125">Hello `arm-template.json` fichier est le modèle Azure Resource Manager hello qui contient une application de la fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="9498e-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="9498e-126">Hello `arm-template-param.json` fichier est hello configuration utilisé par le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9498e-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="9498e-127">Hello `ReceiveDeviceMessages` sous-dossier contient du code de Node.js hello pour hello fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="9498e-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="9498e-128">Configurer des modèles Azure Resource Manager et créer des ressources dans Azure</span><span class="sxs-lookup"><span data-stu-id="9498e-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="9498e-129">Hello de mise à jour `arm-template-param.json` fichier dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9498e-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Paramètres de modèle Azure Resource Manager][arm-template-params]

* <span data-ttu-id="9498e-131">Remplacez **[nom de votre IoT Hub]** par **{nom de mon hub}** que vous avez spécifié lorsque vous [avez créé votre IoT Hub et inscrit votre carte Arduino][created-iot-hub-and-registered-arduino-board].</span><span class="sxs-lookup"><span data-stu-id="9498e-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="9498e-132">Remplacez la **[chaîne de préfixe pour les nouvelles ressources]** par un préfixe de votre choix quelconque.</span><span class="sxs-lookup"><span data-stu-id="9498e-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="9498e-133">préfixe de Hello garantit que ce nom de ressource hello est globalement unique tooavoid conflit.</span><span class="sxs-lookup"><span data-stu-id="9498e-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="9498e-134">N’utilisez pas un numéro initial en préfixe de hello ou un tiret.</span><span class="sxs-lookup"><span data-stu-id="9498e-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="9498e-135">Une fois que vous mettez à jour hello `arm-template-param.json` file, déployer hello ressources tooAzure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9498e-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="9498e-136">Il prend environ cinq minutes toocreate ces ressources.</span><span class="sxs-lookup"><span data-stu-id="9498e-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="9498e-137">Lors de la création de la ressource hello est en cours d’exécution, vous pouvez déplacer sur l’article suivant de toohello.</span><span class="sxs-lookup"><span data-stu-id="9498e-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="9498e-138">Résumé</span><span class="sxs-lookup"><span data-stu-id="9498e-138">Summary</span></span>
<span data-ttu-id="9498e-139">Vous avez créé votre tooprocess d’application Azure fonction messages de hub IoT et un stockage Azure compte toostore ces messages.</span><span class="sxs-lookup"><span data-stu-id="9498e-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="9498e-140">Vous pouvez désormais déployer et exécuter des messages appareil-à-cloud de hello exemple toosend sur votre carte mère Arduino.</span><span class="sxs-lookup"><span data-stu-id="9498e-140">You can now deploy and run hello sample toosend device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9498e-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9498e-141">Next steps</span></span>
<span data-ttu-id="9498e-142">[Exécuter un toosend d’application exemple messages appareil-à-cloud sur votre carte mère Arduino][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="9498e-142">[Run a sample application toosend device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md