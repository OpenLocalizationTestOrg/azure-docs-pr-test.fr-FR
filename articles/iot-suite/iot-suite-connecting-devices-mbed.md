---
title: "Connectez un appareil à l’aide de C sur mbed | Microsoft Docs"
description: "Explique comment connecter un appareil à la solution de surveillance à distance Azure IoT Suite préconfigurée à l’aide d’une application écrite en C et exécutée sous mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="6583d-103">Connexion de votre appareil à la solution préconfigurée de surveillance à distance (mbed)</span><span class="sxs-lookup"><span data-stu-id="6583d-103">Connect your device to the remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="6583d-104">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="6583d-104">Scenario overview</span></span>
<span data-ttu-id="6583d-105">Dans ce scénario, vous allez créer un appareil qui envoie la télémétrie suivante à la [solution préconfigurée][lnk-what-are-preconfig-solutions] de surveillance à distance :</span><span class="sxs-lookup"><span data-stu-id="6583d-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="6583d-106">Température externe</span><span class="sxs-lookup"><span data-stu-id="6583d-106">External temperature</span></span>
* <span data-ttu-id="6583d-107">Température interne</span><span class="sxs-lookup"><span data-stu-id="6583d-107">Internal temperature</span></span>
* <span data-ttu-id="6583d-108">Humidité</span><span class="sxs-lookup"><span data-stu-id="6583d-108">Humidity</span></span>

<span data-ttu-id="6583d-109">Par souci de simplicité, le code sur l’appareil génère des valeurs d’exemple, mais nous vous encourageons à étendre l'exemple en connectant des capteurs réels à votre appareil et en envoyant une télémétrie réelle.</span><span class="sxs-lookup"><span data-stu-id="6583d-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="6583d-110">L’appareil est également en mesure de répondre aux méthodes appelées à partir du tableau de bord de la solution et aux valeurs de propriétés souhaitées définies dans le tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="6583d-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="6583d-111">Pour effectuer ce didacticiel, vous avez besoin d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="6583d-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="6583d-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="6583d-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6583d-113">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="6583d-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6583d-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6583d-114">Before you start</span></span>
<span data-ttu-id="6583d-115">Avant d’écrire du code pour votre appareil, vous devez approvisionner votre solution préconfigurée de surveillance à distance et approvisionner un nouvel appareil personnalisé dans cette solution.</span><span class="sxs-lookup"><span data-stu-id="6583d-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="6583d-116">Approvisionner la solution préconfigurée de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="6583d-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="6583d-117">L’appareil que vous créez dans ce didacticiel envoie des données à une instance de la solution préconfigurée de [surveillance à distance][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="6583d-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="6583d-118">Si vous n’avez pas déjà approvisionné la solution préconfigurée de surveillance à distance dans votre compte Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6583d-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="6583d-119">Sur la page <https://www.azureiotsuite.com/>, cliquez sur **+** pour créer une solution.</span><span class="sxs-lookup"><span data-stu-id="6583d-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="6583d-120">Cliquez sur **Sélectionner** dans le panneau **Surveillance à distance** pour créer votre solution.</span><span class="sxs-lookup"><span data-stu-id="6583d-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="6583d-121">Sur la page **Create Remote monitoring solution** (Créer une solution de surveillance à distance), entrez le nom de votre choix dans la zone **Nom de solution**, sélectionnez la **Région** dans laquelle vous souhaitez procéder au déploiement, puis sélectionnez l’abonnement Azure à utiliser.</span><span class="sxs-lookup"><span data-stu-id="6583d-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="6583d-122">Cliquez ensuite sur **Créer la solution**.</span><span class="sxs-lookup"><span data-stu-id="6583d-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="6583d-123">Attendez la fin du processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="6583d-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="6583d-124">Les solutions préconfigurées utilisent des services Azure facturables.</span><span class="sxs-lookup"><span data-stu-id="6583d-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="6583d-125">Veillez à supprimer la solution préconfigurée de votre abonnement lorsque vous avez terminé pour éviter toute facturation inutile.</span><span class="sxs-lookup"><span data-stu-id="6583d-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="6583d-126">Vous pouvez supprimer complètement une solution préconfigurée de votre abonnement à partir de la page <https://www.azureiotsuite.com/>.</span><span class="sxs-lookup"><span data-stu-id="6583d-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="6583d-127">Au terme du processus d’approvisionnement de la solution de surveillance à distance, cliquez sur **Lancer** pour ouvrir le tableau de bord de la solution dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="6583d-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Tableau de bord de solution][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="6583d-129">Configurer votre appareil dans la solution de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="6583d-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="6583d-130">Si vous avez déjà approvisionné un appareil dans votre solution, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="6583d-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="6583d-131">Vous devez connaître les informations d'identification de l’appareil lorsque vous créez l'application cliente.</span><span class="sxs-lookup"><span data-stu-id="6583d-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="6583d-132">Pour qu’un appareil puisse se connecter à la solution préconfigurée, il doit s’identifier auprès d’IoT Hub à l’aide d’informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="6583d-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="6583d-133">Vous pouvez récupérer les informations d’identification de l’appareil à partir du tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="6583d-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="6583d-134">Les informations d’identification de l’appareil seront ajoutées dans votre application cliente dans la suite de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6583d-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="6583d-135">Pour ajouter un appareil à votre solution de surveillance à distance, procédez comme suit dans le tableau de bord de la solution :</span><span class="sxs-lookup"><span data-stu-id="6583d-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="6583d-136">Dans le coin inférieur gauche du tableau de bord, cliquez sur **Ajouter un périphérique**.</span><span class="sxs-lookup"><span data-stu-id="6583d-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Ajout d’un appareil][1]
2. <span data-ttu-id="6583d-138">Dans le panneau **Appareil personnalisé**, cliquez sur **Ajouter nouveau**.</span><span class="sxs-lookup"><span data-stu-id="6583d-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Ajout d’un appareil personnalisé][2]
3. <span data-ttu-id="6583d-140">Choisissez **Me laisser définir mon propre ID d'appareil**.</span><span class="sxs-lookup"><span data-stu-id="6583d-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="6583d-141">Entrez un ID d’appareil comme **monappareil**, cliquez sur **Vérifier l’ID** pour vous assurer que ce nom n’est pas déjà utilisé, puis cliquez sur **Créer** pour approvisionner l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6583d-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Ajouter ID d’appareil][3]
4. <span data-ttu-id="6583d-143">Prenez note des informations d’identification de l’appareil (ID d’appareil, nom d’hôte IoT Hub et clé d’appareil).</span><span class="sxs-lookup"><span data-stu-id="6583d-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="6583d-144">Votre application cliente a besoin de ces valeurs pour se connecter à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="6583d-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="6583d-145">Cliquez ensuite sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="6583d-145">Then click **Done**.</span></span>
   
    ![Afficher les informations d’identification d’un appareil][4]
5. <span data-ttu-id="6583d-147">Sélectionnez votre appareil dans la liste d’appareils du tableau de bord de la solution.</span><span class="sxs-lookup"><span data-stu-id="6583d-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="6583d-148">Ensuite, dans le panneau **Détails de l’appareil**, cliquez sur **Activer l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="6583d-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="6583d-149">L’état de votre appareil est maintenant **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="6583d-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="6583d-150">La solution de surveillance à distance peut désormais recevoir des données de télémétrie à partir de votre appareil et appeler des méthodes sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6583d-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a><span data-ttu-id="6583d-151">Générer et exécuter l'exemple de solution C</span><span class="sxs-lookup"><span data-stu-id="6583d-151">Build and run the C sample solution</span></span>

<span data-ttu-id="6583d-152">Les instructions qui suivent décrivent la procédure de connexion d’un appareil [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] à la solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="6583d-152">The following instructions describe the steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device to the remote monitoring solution.</span></span>

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a><span data-ttu-id="6583d-153">Connectez le périphérique à votre réseau et à votre ordinateur de bureau</span><span class="sxs-lookup"><span data-stu-id="6583d-153">Connect the mbed device to your network and desktop machine</span></span>

1. <span data-ttu-id="6583d-154">Connectez le périphérique mbed à votre réseau avec un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="6583d-154">Connect the mbed device to your network using an Ethernet cable.</span></span> <span data-ttu-id="6583d-155">Cette étape est nécessaire car l'exemple d'application requiert un accès à internet.</span><span class="sxs-lookup"><span data-stu-id="6583d-155">This step is necessary because the sample application requires internet access.</span></span>

1. <span data-ttu-id="6583d-156">Voir [Getting Started with mbed (Prise en main de mbed)][lnk-mbed-getstarted] pour connecter votre appareil mbed à votre ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="6583d-156">See [Getting Started with mbed][lnk-mbed-getstarted] to connect your mbed device to your desktop PC.</span></span>

1. <span data-ttu-id="6583d-157">Si votre ordinateur de bureau exécute Windows, consultez [Configuration PC][lnk-mbed-pcconnect] pour configurer l’accès aux ports série de votre appareil mbed.</span><span class="sxs-lookup"><span data-stu-id="6583d-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] to configure serial port access to your mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-the-sample-code"></a><span data-ttu-id="6583d-158">Créez un projet mbed et importez l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="6583d-158">Create an mbed project and import the sample code</span></span>

<span data-ttu-id="6583d-159">Procédez comme suit pour ajouter un exemple de code à un projet mbed.</span><span class="sxs-lookup"><span data-stu-id="6583d-159">Follow these steps to add some sample code to an mbed project.</span></span> <span data-ttu-id="6583d-160">Vous importez le projet de démarrage de surveillance à distance avant de le modifier pour utiliser le protocole MQTT à la place du protocole AMQP.</span><span class="sxs-lookup"><span data-stu-id="6583d-160">You import the remote monitoring starter project and then change the project to use the MQTT protocol instead of the AMQP protocol.</span></span> <span data-ttu-id="6583d-161">Pour le moment, vous devez utiliser le protocole MQTT pour utiliser les fonctionnalités de gestion des appareils de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6583d-161">Currently, you need to use the MQTT protocol to use the device management features of IoT Hub.</span></span>

1. <span data-ttu-id="6583d-162">Dans votre navigateur Web, accédez [au site de développement](https://developer.mbed.org/)mbed.org.</span><span class="sxs-lookup"><span data-stu-id="6583d-162">In your web browser, go to the mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="6583d-163">Si vous n’êtes pas inscrit, une option servant à créer un compte vous sera présentée (c’est gratuit).</span><span class="sxs-lookup"><span data-stu-id="6583d-163">If you haven't signed up, you see an option to create an account (it's free).</span></span> <span data-ttu-id="6583d-164">Autrement, connectez-vous avec les informations d’identification de votre compte.</span><span class="sxs-lookup"><span data-stu-id="6583d-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="6583d-165">Cliquez sur **Compilateur** dans le coin supérieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="6583d-165">Then click **Compiler** in the upper right-hand corner of the page.</span></span> <span data-ttu-id="6583d-166">Vous accédez à l’interface *Espace de travail*.</span><span class="sxs-lookup"><span data-stu-id="6583d-166">This action brings you to the *Workspace* interface.</span></span>

1. <span data-ttu-id="6583d-167">Assurez-vous que la plate-forme matérielle que vous utilisez figure dans le coin supérieur droit de la fenêtre, ou cliquez sur l’icône du coin droit pour sélectionner votre plateforme matérielle.</span><span class="sxs-lookup"><span data-stu-id="6583d-167">Make sure the hardware platform you're using appears in the upper right-hand corner of the window, or click the icon in the right-hand corner to select your hardware platform.</span></span>

1. <span data-ttu-id="6583d-168">Cliquez sur **Importer** dans le menu principal.</span><span class="sxs-lookup"><span data-stu-id="6583d-168">Click **Import** on the main menu.</span></span> <span data-ttu-id="6583d-169">Cliquez ensuite sur **Click here to import from URL (Cliquez ici pour importer à partir de l’URL)**.</span><span class="sxs-lookup"><span data-stu-id="6583d-169">Then click **Click here to import from URL**.</span></span>
   
    ![Commencer l’importation vers l’espace de travail mbed][6]

1. <span data-ttu-id="6583d-171">Dans la fenêtre contextuelle, entrez le lien de l’exemple de code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, puis cliquez sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="6583d-171">In the pop-up window, enter the link for the sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importer un exemple de code dans l’espace de travail mbed][7]

1. <span data-ttu-id="6583d-173">Vous pouvez voir dans la fenêtre du compilateur mbed que l’importation de ce projet entraîne également l’importation de différentes bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="6583d-173">You can see in the mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="6583d-174">Certaines sont fournies et gérées par l’équipe Azure IoT ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), tandis que d’autres sont des bibliothèques tierces disponibles dans le catalogue de bibliothèques mbed.</span><span class="sxs-lookup"><span data-stu-id="6583d-174">Some are provided and maintained by the Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in the mbed libraries catalog.</span></span>
   
    ![Afficher le projet mbed][8]

1. <span data-ttu-id="6583d-176">Dans le **Program Workspace (Espace de travail du programme)**, cliquez avec le bouton droit sur la bibliothèque **iothub\_amqp\_transport**, puis cliquez sur **Delete (Supprimer)** et sur **OK** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="6583d-176">In the **Program Workspace**, right-click the **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="6583d-177">Dans le **Program Workspace (Espace de travail du programme)**, cliquez avec le bouton droit sur la bibliothèque **azure\_amqp\_c**, puis cliquez sur **Delete (Supprimer)** et sur **OK** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="6583d-177">In the **Program Workspace**, right-click the **azure\_amqp\_c** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="6583d-178">Cliquez avec le bouton droit sur le projet **remote_monitoring** dans le **Program Workspace (Espace de travail du programme)**, puis sélectionnez **Import Library (Importer une bibliothèque)**, puis **From URL (À partir d’une URL)**.</span><span class="sxs-lookup"><span data-stu-id="6583d-178">Right-click the **remote_monitoring** project in the **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Commencer l’importation de la bibliothèque vers l’espace de travail mbed][6]

1. <span data-ttu-id="6583d-180">Dans la fenêtre contextuelle, entrez le lien de la bibliothèque de transport MQTT https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/, puis cliquez sur **Import (Importer)**.</span><span class="sxs-lookup"><span data-stu-id="6583d-180">In the pop-up window, enter the link for the MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importer la bibliothèque vers l’espace de travail mbed][12]

1. <span data-ttu-id="6583d-182">Répétez l’étape précédente pour ajouter la bibliothèque MQTT depuis https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="6583d-182">Repeat the previous step to add the MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="6583d-183">Votre espace de travail se présente désormais comme suit :</span><span class="sxs-lookup"><span data-stu-id="6583d-183">Your workspace now looks like the following:</span></span>

    ![Afficher l’espace de travail mbed][13]

1. <span data-ttu-id="6583d-185">Ouvrez le fichier remote\_monitoring\remote_monitoring.c, puis remplacez les instructions `#include` existantes par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="6583d-185">Open the remote\_monitoring\remote_monitoring.c file and replace the existing `#include` statements with the following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="6583d-186">Supprimez tout le code restant dans le fichier remote\_monitoring\remote\_monitoring.c.</span><span class="sxs-lookup"><span data-stu-id="6583d-186">Delete all the remaining code in the remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="6583d-187">Créer et exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="6583d-187">Build and run the sample</span></span>

<span data-ttu-id="6583d-188">Ajoutez du code pour appeler la fonction **remote\_monitoring\_run**, puis générez et exécutez l’application de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6583d-188">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="6583d-189">Ajoutez une fonction **main** avec le code suivant à la fin du fichier remote\_monitoring.c pour appeler la fonction **remote\_monitoring\_run** :</span><span class="sxs-lookup"><span data-stu-id="6583d-189">Add a **main** function with following code at the end of the remote\_monitoring.c file to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="6583d-190">Cliquez sur **Compiler** pour générer le programme.</span><span class="sxs-lookup"><span data-stu-id="6583d-190">Click **Compile** to build the program.</span></span> <span data-ttu-id="6583d-191">Vous pouvez sans risque ignorer les avertissements, mais si le traitement génère des erreurs, corrigez-les avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="6583d-191">You can safely ignore any warnings, but if the build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="6583d-192">Si le traitement réussit, le site web du compilateur mbed génère un fichier .bin portant le nom de votre projet et le télécharge sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="6583d-192">If the build is successful, the mbed compiler website generates a .bin file with the name of your project and downloads it to your local machine.</span></span> <span data-ttu-id="6583d-193">Copier le fichier .bin sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6583d-193">Copy the .bin file to the device.</span></span> <span data-ttu-id="6583d-194">Lorsque le fichier .bin est enregistré sur le périphérique, ce dernier redémarre et exécute le programme contenu dans le fichier .bin.</span><span class="sxs-lookup"><span data-stu-id="6583d-194">Saving the .bin file to the device causes the device to restart and run the program contained in the .bin file.</span></span> <span data-ttu-id="6583d-195">Vous pouvez redémarrer manuellement le programme à tout moment en appuyant sur le bouton de réinitialisation sur le périphérique mbed.</span><span class="sxs-lookup"><span data-stu-id="6583d-195">You can manually restart the program at any time by pressing the reset button on the mbed device.</span></span>

1. <span data-ttu-id="6583d-196">Connectez-vous à l’appareil en utilisant une application cliente SSH, tel que PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6583d-196">Connect to the device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="6583d-197">Vous pouvez déterminer le port série que votre appareil va utiliser en consultant le Gestionnaire de périphériques Windows.</span><span class="sxs-lookup"><span data-stu-id="6583d-197">You can determine the serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="6583d-198">Dans PuTTY, cliquez sur le type de connexion **Série** .</span><span class="sxs-lookup"><span data-stu-id="6583d-198">In PuTTY, click the **Serial** connection type.</span></span> <span data-ttu-id="6583d-199">Comme l’appareil se connecte généralement à 9 600 bauds, entrez 9 600 dans le champ **Speed** (Vitesse).</span><span class="sxs-lookup"><span data-stu-id="6583d-199">The device typically connects at 9600 baud, so enter 9600 in the **Speed** box.</span></span> <span data-ttu-id="6583d-200">Cliquez ensuite sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="6583d-200">Then click **Open**.</span></span>

1. <span data-ttu-id="6583d-201">Le programme démarre l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6583d-201">The program starts executing.</span></span> <span data-ttu-id="6583d-202">Il se peut que vous deviez réinitialiser le tableau (appuyez sur Ctrl + Pause ou appuyez sur le bouton de réinitialisation du tableau) si le programme ne démarre pas automatiquement à la connexion.</span><span class="sxs-lookup"><span data-stu-id="6583d-202">You may have to reset the board (press CTRL+Break or press the board's reset button) if the program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
