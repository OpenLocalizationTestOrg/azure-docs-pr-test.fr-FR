---
title: "Appareil simulé et passerelle Azure IoT - Leçon 3 : Lire des messages | Microsoft Docs"
description: "Exécutez un exemple de code sur votre ordinateur hôte pour lire les messages à partir de votre IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données dans le cloud, collecte de données cloud, service de cloud iot, données iot"
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
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="222b9-104">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="222b9-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="222b9-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="222b9-105">What you will do</span></span>

- <span data-ttu-id="222b9-106">Exécutez l’exemple de code sur votre ordinateur hôte pour lire les messages provenant de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="222b9-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="222b9-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="222b9-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="222b9-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="222b9-108">What you will learn</span></span>

<span data-ttu-id="222b9-109">Découvrez comment utiliser l’outil gulp pour lire les messages à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="222b9-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="222b9-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="222b9-110">What you need</span></span>

- <span data-ttu-id="222b9-111">L'exemple d'appareil simulé de la rubrique [Configurer et exécuter un exemple d’application de téléchargement cloud d’appareil simulé](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="222b9-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="222b9-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="222b9-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="222b9-113">La chaîne de connexion de l’appareil permet de connecter votre appareil simulé à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="222b9-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="222b9-114">La chaîne de connexion IoT Hub sert à se connecter au registre des identités de votre IoT Hub pour gérer les appareils autorisés à se connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="222b9-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="222b9-115">Répertorier tous les IoT Hubs de votre groupe de ressources en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="222b9-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="222b9-116">Si vous n’avez pas modifié la valeur, utilisez `iot-gateway` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="222b9-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="222b9-117">Obtenez la chaîne de connexion de l'IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="222b9-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="222b9-118">`{my hub name}` est le nom que vous avez spécifié à la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="222b9-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="222b9-119">Configurer la connexion de l’appareil pour l'exemple de code</span><span class="sxs-lookup"><span data-stu-id="222b9-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="222b9-120">Mettez à jour les configurations de connexion de l'appareil IoT Hub dans `config-azure.json` en effectuant les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="222b9-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="222b9-121">Ouvrez `config-azure.json` dans Visual Studio Code en exécutant la commande suivante dans une fenêtre de console :</span><span class="sxs-lookup"><span data-stu-id="222b9-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="222b9-122">Dans le fichier `config-azure.json`, effectuez les remplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="222b9-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![capture d’écran de configuration azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="222b9-124">Remplacez `[IoT hub connection string]` par la chaîne de connexion de l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="222b9-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="222b9-125">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="222b9-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="222b9-126">Exécutez l’exemple d’application d'appareil simulé et lisez les messages de l'IoT Hub à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="222b9-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="222b9-127">La commande exécute l’application qui envoie des messages à votre IoT Hub toutes les 2 secondes.</span><span class="sxs-lookup"><span data-stu-id="222b9-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="222b9-128">Elle génère également un processus enfant pour recevoir le message.</span><span class="sxs-lookup"><span data-stu-id="222b9-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="222b9-129">Les messages envoyés et reçus sont tous affichés instantanément sur la même fenêtre de console sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="222b9-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="222b9-130">L’application va s’arrêter dans 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="222b9-130">The application will exit in 40 seconds.</span></span>

![Exemple d’application d'appareil simulé avec des messages envoyés et reçus](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="222b9-132">Résumé</span><span class="sxs-lookup"><span data-stu-id="222b9-132">Summary</span></span>

<span data-ttu-id="222b9-133">Vous avez correctement exécuté l’exemple d’application pour envoyer des données à votre IoT Hub à l'aide d'un appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="222b9-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="222b9-134">Vous avez également lu les messages qui ont été envoyés à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="222b9-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="222b9-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="222b9-135">Next steps</span></span>
[<span data-ttu-id="222b9-136">Créer une application de fonction Azure et un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="222b9-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


