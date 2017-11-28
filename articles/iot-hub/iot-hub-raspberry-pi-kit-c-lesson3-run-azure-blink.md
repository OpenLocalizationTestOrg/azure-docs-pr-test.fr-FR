---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 3 : exécuter l’exemple | Documents Microsoft"
description: "Déployer et exécuter un tooRaspberry d’application exemple Pi 3 qui envoie l’IoT hub tooyour de messages et clignote hello DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "led clignotante cloud pi, clignotement led à partir du cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="a6c8b-104">Exécuter un toosend d’application exemple messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="a6c8b-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a6c8b-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="a6c8b-105">What you will do</span></span>
<span data-ttu-id="a6c8b-106">Cet article vous explique comment toodeploy et exécuter un exemple d’application sur framboises Pi 3 qui envoie des messages tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="a6c8b-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a6c8b-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a6c8b-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="a6c8b-108">What you will learn</span></span>
<span data-ttu-id="a6c8b-109">Vous allez apprendre comment toouse hello gulp outil toodeploy et exécuter l’exemple d’application de Node.js hello sur Pi.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a6c8b-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="a6c8b-110">What you need</span></span>
* <span data-ttu-id="a6c8b-111">Avant de commencer cette tâche, vous devez avoir terminé avec succès [créer une application de la fonction Azure et un stockage compte tooprocess et magasin IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="a6c8b-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="a6c8b-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="a6c8b-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="a6c8b-113">chaîne de connexion de périphérique Hello est utilisé par votre concentrateur de Pi tooconnect tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="a6c8b-114">Hello chaîne de connexion de hub IoT est un registre des identités toohello tooconnect utilisés dans vos appareils IoT hub toomanage hello autorisées tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="a6c8b-115">Liste de tous vos hubs IoT dans votre groupe de ressources en exécutant hello suivant commande CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="a6c8b-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="a6c8b-116">Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="a6c8b-117">Obtenir la chaîne de connexion de hub IoT hello en exécutant hello suivant commande CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="a6c8b-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="a6c8b-118">`{my hub name}`est le nom hello que vous avez spécifié lorsque vous créez votre hub IoT et inscrit Pi.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="a6c8b-119">Obtenir la chaîne de connexion de périphérique de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a6c8b-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="a6c8b-120">Utilisez `myraspberrypi` en tant que valeur hello `{device id}` si vous n’avez modifié la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="a6c8b-121">Configurer la connexion du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="a6c8b-121">Configure hello device connection</span></span>
1. <span data-ttu-id="a6c8b-122">Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="a6c8b-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="a6c8b-123">Exécutez également **gulp install-tools**, si vous ne l’avez pas fait dans la leçon 1.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="a6c8b-124">Fichier de configuration de périphérique ouvert hello `config-raspberrypi.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a6c8b-124">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="a6c8b-126">Rendre hello suivant remplacements Bonjour `config-raspberrypi.json` fichier :</span><span class="sxs-lookup"><span data-stu-id="a6c8b-126">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="a6c8b-127">Remplacez **[nom d’hôte du périphérique ou adresse IP]** avec hello appareil IP adresse ou nom d’hôte que vous avez obtenu à partir de `device-discovery-cli` ou avec la valeur hello héritée lors de la configuration de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-127">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="a6c8b-128">Remplacez **[chaîne de connexion de périphérique IoT]** avec hello `device connection string` obtenues.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="a6c8b-129">Remplacez **[chaîne de connexion de hub IoT]** avec hello `iot hub connection string` obtenues.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="a6c8b-130">Vous n’avez pas besoin de `azure_storage_connection_string` dans cet article.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="a6c8b-131">Gardez-le tel quel.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-131">Keep it as is.</span></span>

<span data-ttu-id="a6c8b-132">Hello de mise à jour `config-raspberrypi.json` de fichiers afin que vous pouvez déployer des hello exemple d’application à partir de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-132">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="a6c8b-133">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="a6c8b-133">Deploy and run hello sample application</span></span>
<span data-ttu-id="a6c8b-134">Déployer et exécuter l’exemple d’application hello sur Pi en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a6c8b-134">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="a6c8b-135">Vérifiez que hello exemple application fonctionne</span><span class="sxs-lookup"><span data-stu-id="a6c8b-135">Verify that hello sample application works</span></span>
<span data-ttu-id="a6c8b-136">Vous devez voir hello DEL qui est connecté tooPi clignote toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-136">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="a6c8b-137">Chaque fois que hello LED clignote, exemple d’application hello envoie un hub IoT de tooyour message et vérifie que ce message de type hello a été envoyé avec succès tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-137">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="a6c8b-138">En outre, chaque message reçu par IoT hub de hello est imprimé dans la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-138">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="a6c8b-139">exemple d’application Hello se termine automatiquement après l’envoi des messages de 20.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-139">hello sample application terminates automatically after sending 20 messages.</span></span>

![Exemple d’application avec des messages envoyés et reçus](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="a6c8b-141">Résumé</span><span class="sxs-lookup"><span data-stu-id="a6c8b-141">Summary</span></span>
<span data-ttu-id="a6c8b-142">Vous avez déployé et exécuter hello nouvelle blink exemple d’application sur le hub IoT tooyour Pi toosend messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-142">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="a6c8b-143">Vous surveillez maintenant vos messages qu’ils sont écrits de compte de stockage toohello.</span><span class="sxs-lookup"><span data-stu-id="a6c8b-143">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6c8b-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a6c8b-144">Next steps</span></span>
[<span data-ttu-id="a6c8b-145">Lecture des messages conservés dans le Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="a6c8b-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

