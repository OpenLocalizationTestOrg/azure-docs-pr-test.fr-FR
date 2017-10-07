---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 3 : envoyer des messages | Documents Microsoft"
description: "Déployer et exécuter un tooIntel d’application exemple Edison qui envoie l’IoT hub tooyour de messages et clignote hello DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "service de cloud IOT, arduino envoyer des données toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 83615335027cc792b89d3894578fc3f7a55e5c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="57e0c-104">Exécuter un toosend d’application exemple messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="57e0c-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="57e0c-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="57e0c-105">What you will do</span></span>
<span data-ttu-id="57e0c-106">Cet article vous explique comment toodeploy et exécuter un exemple d’application sur Edison Intel qui envoie des messages tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="57e0c-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="57e0c-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="57e0c-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="57e0c-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="57e0c-108">What you will learn</span></span>
<span data-ttu-id="57e0c-109">Vous découvrez comment toouse hello gulp outil toodeploy et exécuter l’exemple d’application de C hello sur Edison.</span><span class="sxs-lookup"><span data-stu-id="57e0c-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="57e0c-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="57e0c-110">What you need</span></span>
* <span data-ttu-id="57e0c-111">Avant de commencer cette tâche, vous devez avoir terminé avec succès [créer une application de la fonction Azure et un stockage compte tooprocess et magasin IoT hub messages][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="57e0c-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="57e0c-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="57e0c-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="57e0c-113">chaîne de connexion de périphérique Hello est utilisé tooconnect hub IoT de tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="57e0c-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="57e0c-114">Hello la chaîne de connexion de hub IoT est tooconnect utilisé votre identité d’appareil IoT hub toohello représentant Edison dans le hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="57e0c-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="57e0c-115">Liste de tous vos hubs IoT dans votre groupe de ressources en exécutant hello suivant commande CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="57e0c-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="57e0c-116">Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="57e0c-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="57e0c-117">Obtenir la chaîne de connexion de hub IoT hello en exécutant hello suivant commande CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="57e0c-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="57e0c-118">`{my hub name}`est le nom hello que vous avez spécifié lorsque vous créez votre hub IoT et inscrit Edison.</span><span class="sxs-lookup"><span data-stu-id="57e0c-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="57e0c-119">Obtenir la chaîne de connexion de périphérique de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="57e0c-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="57e0c-120">Utilisez `myinteledison` en tant que valeur hello `{device id}` si vous n’avez modifié la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="57e0c-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="57e0c-121">Configurer la connexion du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="57e0c-121">Configure hello device connection</span></span>
1. <span data-ttu-id="57e0c-122">Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="57e0c-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > <span data-ttu-id="57e0c-123">Exécutez également **gulp install-tools**, si vous ne l’avez pas fait dans la leçon 1.</span><span class="sxs-lookup"><span data-stu-id="57e0c-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="57e0c-124">Fichier de configuration de périphérique ouvert hello `config-edison.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="57e0c-124">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. <span data-ttu-id="57e0c-126">Rendre hello suivant remplacements Bonjour `config-edison.json` fichier :</span><span class="sxs-lookup"><span data-stu-id="57e0c-126">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="57e0c-127">Remplacez **[nom d’hôte du périphérique ou adresse IP]** avec l’adresse IP du périphérique hello démarquer lorsque vous avez configuré votre appareil.</span><span class="sxs-lookup"><span data-stu-id="57e0c-127">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="57e0c-128">Remplacez **[chaîne de connexion de périphérique IoT]** avec hello `device connection string` obtenues.</span><span class="sxs-lookup"><span data-stu-id="57e0c-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="57e0c-129">Remplacez **[chaîne de connexion de hub IoT]** avec hello `iot hub connection string` obtenues.</span><span class="sxs-lookup"><span data-stu-id="57e0c-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="57e0c-130">Vous n’avez pas besoin de `azure_storage_connection_string` dans cet article.</span><span class="sxs-lookup"><span data-stu-id="57e0c-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="57e0c-131">Gardez-le tel quel.</span><span class="sxs-lookup"><span data-stu-id="57e0c-131">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="57e0c-132">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="57e0c-132">Deploy and run hello sample application</span></span>
<span data-ttu-id="57e0c-133">Déployer et exécuter l’exemple d’application hello sur Edison en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="57e0c-133">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="57e0c-134">Vérifiez que hello exemple application fonctionne</span><span class="sxs-lookup"><span data-stu-id="57e0c-134">Verify that hello sample application works</span></span>
<span data-ttu-id="57e0c-135">Vous devez voir hello DEL qui est connecté tooEdison clignote toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="57e0c-135">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="57e0c-136">Chaque fois que hello LED clignote, exemple d’application hello envoie un hub IoT de tooyour message et vérifie que ce message de type hello a été envoyé avec succès tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="57e0c-136">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="57e0c-137">En outre, chaque message reçu par IoT hub de hello est imprimé dans la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="57e0c-137">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="57e0c-138">exemple d’application Hello se termine automatiquement après l’envoi des messages de 20.</span><span class="sxs-lookup"><span data-stu-id="57e0c-138">hello sample application terminates automatically after sending 20 messages.</span></span>

![Exemple d’application avec des messages envoyés et reçus][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="57e0c-140">Résumé</span><span class="sxs-lookup"><span data-stu-id="57e0c-140">Summary</span></span>
<span data-ttu-id="57e0c-141">Vous avez déployé et exécuté de hello nouvelle blink exemple d’application sur Edison tooyour IoT hub toosend messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="57e0c-141">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="57e0c-142">Vous surveillez maintenant vos messages qu’ils sont écrits de compte de stockage toohello.</span><span class="sxs-lookup"><span data-stu-id="57e0c-142">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57e0c-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57e0c-143">Next steps</span></span>
<span data-ttu-id="57e0c-144">[Lecture des messages conservés dans le stockage Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="57e0c-144">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md