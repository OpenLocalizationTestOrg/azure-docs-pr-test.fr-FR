---
title: "Appareil simulé et passerelle Azure IoT - Leçon 3 : Lire des messages | Microsoft Docs"
description: "Exécuter un exemple de code sur votre hôte ordinateur tooread hello des messages à partir de votre hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données dans le cloud de hello, collecte de données de cloud, le service cloud iot, iot données"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="777a3-104">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="777a3-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="777a3-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="777a3-105">What you will do</span></span>

- <span data-ttu-id="777a3-106">Exécutez exemple de code sur votre hôte tooread ordinateur des messages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="777a3-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="777a3-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="777a3-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="777a3-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="777a3-108">What you will learn</span></span>

<span data-ttu-id="777a3-109">Comment toouse hello gulp tooread messages de l’outil à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="777a3-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="777a3-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="777a3-110">What you need</span></span>

- <span data-ttu-id="777a3-111">exemple d’appareil simulé Hello dans [configurer et exécuter un cloud d’appareil simulé téléchargement l’exemple d’application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="777a3-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="777a3-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="777a3-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="777a3-113">chaîne de connexion de périphérique Hello est utilisé par votre appareil simulé tooconnect tooyour IoT de supervision.</span><span class="sxs-lookup"><span data-stu-id="777a3-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="777a3-114">Hello chaîne de connexion de hub IoT est un registre des identités toohello tooconnect utilisés dans vos appareils IoT hub toomanage hello autorisées tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="777a3-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="777a3-115">Liste de tous vos hubs IoT dans votre groupe de ressources en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="777a3-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="777a3-116">Utilisez `iot-gateway` en tant que valeur hello `{resource group name}` si vous n’avez pas le modifier.</span><span class="sxs-lookup"><span data-stu-id="777a3-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="777a3-117">Obtenir la chaîne de connexion de hub IoT hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="777a3-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="777a3-118">`{my hub name}`est le nom hello que vous avez spécifié dans la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="777a3-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="777a3-119">Configurer la connexion du périphérique pour l’exemple de code hello hello</span><span class="sxs-lookup"><span data-stu-id="777a3-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="777a3-120">Mettre à jour les configurations de connexion IoT hub et de périphérique dans `config-azure.json` en effectuant hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="777a3-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="777a3-121">Ouvrez `config-azure.json` dans le Code de Visual Studio en exécutant hello commande dans une fenêtre de console suivante :</span><span class="sxs-lookup"><span data-stu-id="777a3-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="777a3-122">Rendre hello suivant remplacements Bonjour `config-azure.json` fichier :</span><span class="sxs-lookup"><span data-stu-id="777a3-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![capture d’écran de configuration azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="777a3-124">Remplacez `[IoT hub connection string]` par hello chaîne de connexion de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="777a3-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="777a3-125">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="777a3-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="777a3-126">Exécuter l’exemple d’appareil hello simulée application et lire des messages de IoT Hub par hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="777a3-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="777a3-127">commande Hello s’exécute l’application hello qui envoie IoT hub de messages tooyour toutes les 2 secondes.</span><span class="sxs-lookup"><span data-stu-id="777a3-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="777a3-128">Il génère également un message de salutation tooreceive processus enfant.</span><span class="sxs-lookup"><span data-stu-id="777a3-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="777a3-129">messages de type Hello qui sont envoyés et reçus sont tous les hello afficher instantanément à même de fenêtre dans la console hello machine hôte.</span><span class="sxs-lookup"><span data-stu-id="777a3-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="777a3-130">application Hello s’arrête dans 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="777a3-130">hello application will exit in 40 seconds.</span></span>

![Exemple d’application d'appareil simulé avec des messages envoyés et reçus](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="777a3-132">Résumé</span><span class="sxs-lookup"><span data-stu-id="777a3-132">Summary</span></span>

<span data-ttu-id="777a3-133">Vous avez correctement exécuter tooyour IoT hub hello exemple application toosend données avec un appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="777a3-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="777a3-134">Vous avez également lire les messages de type hello qui ont été envoyés tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="777a3-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="777a3-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="777a3-135">Next steps</span></span>
[<span data-ttu-id="777a3-136">Créer une application de fonction Azure et un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="777a3-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


