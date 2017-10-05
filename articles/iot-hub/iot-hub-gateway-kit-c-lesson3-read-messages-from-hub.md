---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 3 : Lire des messages | Microsoft Docs"
description: "Exécutez un exemple de code sur votre ordinateur hôte pour lire les messages à partir de votre IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données dans le cloud, collecte de données cloud, service de cloud iot, données iot"
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
ms.openlocfilehash: 45f3595c4848d5c283cdf95604adf8d2c8d6a809
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="5a900-104">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5a900-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5a900-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="5a900-105">What you will do</span></span>

- <span data-ttu-id="5a900-106">Exécutez l’exemple de code sur votre ordinateur hôte pour lire les messages provenant de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a900-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="5a900-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5a900-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5a900-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="5a900-108">What you will learn</span></span>

<span data-ttu-id="5a900-109">Découvrez comment utiliser l’outil gulp pour lire les messages à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a900-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5a900-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="5a900-110">What you need</span></span>

- <span data-ttu-id="5a900-111">L’exemple d’application BLE que vous avez exécuté dans la leçon 3.</span><span class="sxs-lookup"><span data-stu-id="5a900-111">The BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="5a900-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="5a900-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="5a900-113">La chaîne de connexion de l’appareil permet de connecter votre appareil (TI SensorTag ou appareil simulé) à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a900-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span></span> <span data-ttu-id="5a900-114">La chaîne de connexion IoT Hub sert à se connecter au registre des identités de votre IoT Hub pour gérer les appareils autorisés à se connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a900-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="5a900-115">Répertoriez tous les IoT Hubs de votre groupe de ressources en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5a900-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="5a900-116">Si vous n’avez pas modifié la valeur, utilisez `iot-gateway` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="5a900-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span></span>
- <span data-ttu-id="5a900-117">Obtenez la chaîne de connexion de l'IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5a900-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="5a900-118">`{my hub name}` est le nom que vous avez spécifié à la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="5a900-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="5a900-119">Configurer la connexion de l’appareil pour l'exemple de code</span><span class="sxs-lookup"><span data-stu-id="5a900-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="5a900-120">Mettez à jour le fichier de configuration d’appareil `config-azure.json` pour lire les messages de votre IoT Hub sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="5a900-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="5a900-121">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a900-121">To do this, follow these steps:</span></span>

1. <span data-ttu-id="5a900-122">Ouvrez `config-azure.json` dans Visual Studio Code en exécutant la commande suivante dans une fenêtre de console :</span><span class="sxs-lookup"><span data-stu-id="5a900-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="5a900-123">Dans le fichier `config-azure.json`, effectuez les remplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="5a900-123">Make the following replacements in the `config-azure.json` file:</span></span>

   ![capture d’écran de configuration azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="5a900-125">Remplacez `[IoT hub connection string]` par la chaîne de connexion de l’IoT Hub obtenue.</span><span class="sxs-lookup"><span data-stu-id="5a900-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="5a900-126">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5a900-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="5a900-127">Si vous avez un TI SensorTag, assurez-vous que vous avez déjà démarré votre SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5a900-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="5a900-128">Exécutez l’exemple d’application de passerelle et lisez les messages de l'IoT Hub à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5a900-128">Run the gateway sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="5a900-129">La commande exécute l’exemple d’application BLE qui lit et regroupe les données de température de votre SensorTag ou de l’appareil simulé et envoie le message à votre IoT Hub toutes les 2 secondes.</span><span class="sxs-lookup"><span data-stu-id="5a900-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="5a900-130">Elle génère également un processus enfant pour recevoir le message.</span><span class="sxs-lookup"><span data-stu-id="5a900-130">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="5a900-131">Les messages envoyés et reçus sont tous affichés instantanément sur la même fenêtre de console sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="5a900-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="5a900-132">L’exemple d’instance d’application se ferme automatiquement au bout de 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="5a900-132">The sample application instance will terminate automatically in 40 seconds.</span></span>

![Exemple d’application BLE avec des messages envoyés et reçus](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="5a900-134">Résumé</span><span class="sxs-lookup"><span data-stu-id="5a900-134">Summary</span></span>

<span data-ttu-id="5a900-135">Vous avez exécuté un exemple de code pour lire des messages provenant de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a900-135">You've run a sample code to read messages from your IoT hub.</span></span> <span data-ttu-id="5a900-136">Vous êtes prêt à lire les messages qui sont stockés dans votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="5a900-136">You're ready to read the messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a900-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5a900-137">Next steps</span></span>
[<span data-ttu-id="5a900-138">Créer une application de fonction Azure et un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="5a900-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


