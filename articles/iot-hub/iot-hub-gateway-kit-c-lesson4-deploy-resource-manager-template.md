---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 4 : Créer un conteneur d’application | Microsoft Docs"
description: "Enregistrer des messages à partir de hub IoT de tooyour Intel NUC, notez-les tooAzure le stockage de Table et puis de les lire à partir du cloud de hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "le stockage des données dans le cloud hello, les données stockées dans le cloud, service de cloud computing iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="3a514-104">Créer une application de fonction Azure et un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="3a514-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="3a514-105">Les fonctions Azure est une solution pour l’exécution de facilement _fonctions_ (petits segments de code) dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="3a514-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="3a514-106">Une application de la fonction Azure héberge l’exécution de hello de vos fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3a514-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="3a514-107">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="3a514-107">What you will do</span></span>

- <span data-ttu-id="3a514-108">Utiliser un toocreate de modèle Azure Resource Manager, une application de la fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3a514-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="3a514-109">application de fonction Azure Hello écoute les événements de hub IoT tooAzure, traite les messages entrants et les écrit tooAzure le stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="3a514-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="3a514-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3a514-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="3a514-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="3a514-111">What you will learn</span></span>

<span data-ttu-id="3a514-112">Dans cette leçon, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="3a514-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="3a514-113">Comment toouse Azure Resource Manager toodeploy ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3a514-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="3a514-114">Comment toouse Azure fonction application tooprocess les messages IoT Hub et les écrire tooa table dans le stockage Azure Table.</span><span class="sxs-lookup"><span data-stu-id="3a514-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3a514-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="3a514-115">What you need</span></span>

<span data-ttu-id="3a514-116">Avec succès, vous devez avoir terminé les leçons précédentes hello :</span><span class="sxs-lookup"><span data-stu-id="3a514-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="3a514-117">Leçon 1 : Configurer l’Intel NUC comme passerelle IoT</span><span class="sxs-lookup"><span data-stu-id="3a514-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="3a514-118">Leçon 2 : Préparer votre ordinateur hôte et Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3a514-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="3a514-119">Leçon 3 : Recevoir des messages à partir de SensorTag et lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3a514-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="3a514-120">Ouvrir un exemple d’application</span><span class="sxs-lookup"><span data-stu-id="3a514-120">Open a sample app</span></span>

<span data-ttu-id="3a514-121">Accédez tooyour `iot-hub-c-intel-nuc-gateway-getting-started` dossier de dépôt, les fichiers de configuration de hello initialize et puis ouvrez hello exemple de projet dans Visual Studio Code en exécutant hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3a514-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![structure du référentiel](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="3a514-123">Hello `arm-template.json` fichier est le modèle Azure Resource Manager hello qui contient une application de la fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3a514-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="3a514-124">Hello `arm-template-param.json` fichier est hello configuration utilisé par le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3a514-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="3a514-125">Hello `ReceiveDeviceMessages` sous-dossier contient du code de Node.js hello pour hello fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="3a514-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="3a514-126">Configurer des modèles Azure Resource Manager et créer des ressources dans Azure</span><span class="sxs-lookup"><span data-stu-id="3a514-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="3a514-127">Hello de mise à jour `arm-template-param.json` fichier dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3a514-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![modèle arm json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="3a514-129">Remplacez `[your IoT Hub name]` par `{my hub name}` que vous avez spécifié à la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="3a514-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="3a514-130">Une fois que vous mettez à jour hello `arm-template-param.json` file, déployer hello ressources tooAzure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3a514-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="3a514-131">Utilisez `iot-gateway` en tant que valeur hello `{resource group name}` si vous n’avez pas modifier la valeur hello dans la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="3a514-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="3a514-132">Résumé</span><span class="sxs-lookup"><span data-stu-id="3a514-132">Summary</span></span>

<span data-ttu-id="3a514-133">Vous avez créé votre tooprocess d’application Azure fonction messages de hub IoT et un stockage Azure compte toostore ces messages.</span><span class="sxs-lookup"><span data-stu-id="3a514-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="3a514-134">Vous pouvez maintenant lire les messages envoyés par votre IoT hub de passerelle tooyour.</span><span class="sxs-lookup"><span data-stu-id="3a514-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a514-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a514-135">Next steps</span></span>
<span data-ttu-id="3a514-136">[Lire des messages conservés dans le stockage Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3a514-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
