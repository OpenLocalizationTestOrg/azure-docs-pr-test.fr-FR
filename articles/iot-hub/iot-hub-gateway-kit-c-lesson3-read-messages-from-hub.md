---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 3 : Lire des messages | Microsoft Docs"
description: "Exécuter un exemple de code sur votre hôte ordinateur tooread hello des messages à partir de votre hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données dans le cloud de hello, collecte de données de cloud, le service cloud iot, iot données"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="67b18-104">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="67b18-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="67b18-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="67b18-105">What you will do</span></span>

- <span data-ttu-id="67b18-106">Exécutez exemple de code sur votre hôte tooread ordinateur des messages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="67b18-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="67b18-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="67b18-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="67b18-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="67b18-108">What you will learn</span></span>

<span data-ttu-id="67b18-109">Comment toouse hello gulp tooread messages de l’outil à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="67b18-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="67b18-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="67b18-110">What you need</span></span>

- <span data-ttu-id="67b18-111">Hello exemple d’application BLE qui vous a été correctement exécuté dans la leçon 3.</span><span class="sxs-lookup"><span data-stu-id="67b18-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="67b18-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="67b18-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="67b18-113">chaîne de connexion de périphérique Hello est utilisé par votre appareil (TI SensorTag ou appareil simulé) tooconnect tooyour IoT de supervision.</span><span class="sxs-lookup"><span data-stu-id="67b18-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="67b18-114">Hello chaîne de connexion de hub IoT est un registre des identités toohello tooconnect utilisés dans vos appareils IoT hub toomanage hello autorisées tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="67b18-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="67b18-115">Liste de tous vos hubs IoT dans votre groupe de ressources en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="67b18-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="67b18-116">Utilisez `iot-gateway` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="67b18-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="67b18-117">Obtenir la chaîne de connexion de hub IoT hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="67b18-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="67b18-118">`{my hub name}`est le nom hello que vous avez spécifié dans la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="67b18-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="67b18-119">Configurer la connexion du périphérique pour l’exemple de code hello hello</span><span class="sxs-lookup"><span data-stu-id="67b18-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="67b18-120">Fichier de configuration de mise à jour hello périphérique `config-azure.json` afin que vous pouvez lire les messages de votre hub IoT sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="67b18-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="67b18-121">toodo, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="67b18-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="67b18-122">Ouvrez `config-azure.json` dans le Code de Visual Studio en exécutant hello commande dans une fenêtre de console suivante :</span><span class="sxs-lookup"><span data-stu-id="67b18-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="67b18-123">Rendre hello suivant remplacements Bonjour `config-azure.json` fichier :</span><span class="sxs-lookup"><span data-stu-id="67b18-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![capture d’écran de configuration azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="67b18-125">Remplacez `[IoT hub connection string]` par hello chaîne de connexion de hub IoT que vous avez obtenu.</span><span class="sxs-lookup"><span data-stu-id="67b18-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="67b18-126">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="67b18-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="67b18-127">Si vous avez un TI SensorTag, assurez-vous que vous avez déjà démarré votre SensorTag.</span><span class="sxs-lookup"><span data-stu-id="67b18-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="67b18-128">Exécuter l’application d’exemple hello passerelle et lire des messages de IoT Hub par hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="67b18-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="67b18-129">commande Hello exécute hello BLE exemple d’application qui lit et packages de données de température de votre SensorTag ou d’un appareil simulé et envoie tooyour IoT hub hello message toutes les 2 secondes.</span><span class="sxs-lookup"><span data-stu-id="67b18-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="67b18-130">Il génère également un message de salutation tooreceive processus enfant.</span><span class="sxs-lookup"><span data-stu-id="67b18-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="67b18-131">messages de type Hello qui sont envoyés et reçus sont tous les hello afficher instantanément à même de fenêtre dans la console hello machine hôte.</span><span class="sxs-lookup"><span data-stu-id="67b18-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="67b18-132">instance de l’application exemple Hello se termine automatiquement au bout de 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="67b18-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![Exemple d’application BLE avec des messages envoyés et reçus](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="67b18-134">Résumé</span><span class="sxs-lookup"><span data-stu-id="67b18-134">Summary</span></span>

<span data-ttu-id="67b18-135">Vous avez exécuté un tooread de code d’exemple de messages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="67b18-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="67b18-136">Vous êtes prêt tooread les messages hello qui sont stockés dans votre stockage de table Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="67b18-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67b18-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="67b18-137">Next steps</span></span>
[<span data-ttu-id="67b18-138">Créer une application de fonction Azure et un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="67b18-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


