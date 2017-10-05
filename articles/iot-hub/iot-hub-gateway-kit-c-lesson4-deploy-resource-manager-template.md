---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 4 : Créer un conteneur d’application | Microsoft Docs"
description: "Enregistrez des messages à partir d’Intel NUC dans votre hub IoT, écrivez-les dans le stockage Table Azure, puis lisez-les à partir du cloud."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "stockage de données dans le cloud, les données stockées dans le cloud, service cloud iot"
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
ms.openlocfilehash: 717c91e8332660f19d596c05a8a23afd8df1d51c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="dd597-104">Créer une application de fonction Azure et un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="dd597-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="dd597-105">Azure Functions est une solution conçue pour exécuter facilement des petits morceaux de code (_fonctions_) dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="dd597-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="dd597-106">Une application de fonction Azure héberge l’exécution de vos fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="dd597-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="dd597-107">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="dd597-107">What you will do</span></span>

- <span data-ttu-id="dd597-108">Utilisez un modèle Azure Resource Manager pour créer une application de fonction Azure et un compte de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="dd597-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="dd597-109">L’application de fonction Azure écoute les événements d’Azure IoT Hub, traite les messages entrants et les écrit dans le stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="dd597-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="dd597-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="dd597-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="dd597-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="dd597-111">What you will learn</span></span>

<span data-ttu-id="dd597-112">Dans cette leçon, vous allez apprendre ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="dd597-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="dd597-113">l’utilisation d’Azure Resource Manager pour déployer des ressources Azure ;</span><span class="sxs-lookup"><span data-stu-id="dd597-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="dd597-114">l’utilisation d’une application de fonction Azure pour traiter les messages de l’IoT Hub et les écrire dans le stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="dd597-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="dd597-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="dd597-115">What you need</span></span>

<span data-ttu-id="dd597-116">Vous devez avoir terminé les leçons précédentes :</span><span class="sxs-lookup"><span data-stu-id="dd597-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="dd597-117">Leçon 1 : Configurer l’Intel NUC comme passerelle IoT</span><span class="sxs-lookup"><span data-stu-id="dd597-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="dd597-118">Leçon 2 : Préparer votre ordinateur hôte et Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="dd597-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="dd597-119">Leçon 3 : Recevoir des messages à partir de SensorTag et lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="dd597-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="dd597-120">Ouvrir un exemple d’application</span><span class="sxs-lookup"><span data-stu-id="dd597-120">Open a sample app</span></span>

<span data-ttu-id="dd597-121">Accédez à votre dossier de référentiel `iot-hub-c-intel-nuc-gateway-getting-started`, initialisez les fichiers de configuration, puis ouvrez l’exemple de projet dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dd597-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![structure du référentiel](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="dd597-123">Le fichier `arm-template.json` est le modèle Azure Resource Manager qui contient une application de fonction Azure et un compte de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="dd597-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="dd597-124">Le fichier `arm-template-param.json` est le fichier de configuration utilisé par le modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd597-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="dd597-125">Le sous-dossier `ReceiveDeviceMessages` contient le code Node.js pour la fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="dd597-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="dd597-126">Configurer des modèles Azure Resource Manager et créer des ressources dans Azure</span><span class="sxs-lookup"><span data-stu-id="dd597-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="dd597-127">Mettez à jour le fichier `arm-template-param.json` dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dd597-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![modèle arm json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="dd597-129">Remplacez `[your IoT Hub name]` par `{my hub name}` que vous avez spécifié à la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="dd597-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="dd597-130">Une fois que vous avez mis à jour le fichier `arm-template-param.json`, déployez les ressources dans Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dd597-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="dd597-131">Si vous n’avez pas modifié la valeur à la leçon 2, utilisez `iot-gateway` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="dd597-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="dd597-132">Résumé</span><span class="sxs-lookup"><span data-stu-id="dd597-132">Summary</span></span>

<span data-ttu-id="dd597-133">Vous avez créé votre application de fonction Azure pour traiter les messages de l’IoT Hub et un compte de Stockage Azure pour stocker ces messages.</span><span class="sxs-lookup"><span data-stu-id="dd597-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="dd597-134">Vous pouvez maintenant lire les messages envoyés par votre passerelle à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dd597-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd597-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dd597-135">Next steps</span></span>
<span data-ttu-id="dd597-136">[Lire des messages conservés dans le stockage Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dd597-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
