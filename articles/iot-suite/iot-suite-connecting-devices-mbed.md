---
title: "aaaConnect un appareil à l’aide de C sur mbed | Documents Microsoft"
description: "Décrit comment tooconnect un toohello appareil Azure IoT Suite préconfiguré solution d’analyse à distance à l’aide d’une application écrite en C en cours d’exécution sur un appareil mbed."
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
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="d94f3-103">Se connecter à votre solution préconfigurée (mbed) de surveillance à distance de toohello périphérique</span><span class="sxs-lookup"><span data-stu-id="d94f3-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="d94f3-104">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="d94f3-104">Scenario overview</span></span>
<span data-ttu-id="d94f3-105">Dans ce scénario, vous créez un périphérique qui envoie hello suivant la surveillance à distance de télémétrie toohello [solution préconfigurée][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="d94f3-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="d94f3-106">Température externe</span><span class="sxs-lookup"><span data-stu-id="d94f3-106">External temperature</span></span>
* <span data-ttu-id="d94f3-107">Température interne</span><span class="sxs-lookup"><span data-stu-id="d94f3-107">Internal temperature</span></span>
* <span data-ttu-id="d94f3-108">Humidité</span><span class="sxs-lookup"><span data-stu-id="d94f3-108">Humidity</span></span>

<span data-ttu-id="d94f3-109">Par souci de simplicité, code hello sur l’appareil de hello génère des exemples de valeurs, mais nous encourageons exemple hello tooextend par connexion réelle capteurs tooyour appareil et l’envoi de télémétrie réel.</span><span class="sxs-lookup"><span data-stu-id="d94f3-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="d94f3-110">Hello appareil est également en mesure de toorespond toomethods appelée à partir du tableau de bord de solution hello et souhaitée des valeurs de propriété définies dans le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="d94f3-111">toocomplete ce didacticiel, vous avez besoin d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="d94f3-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="d94f3-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d94f3-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d94f3-113">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="d94f3-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d94f3-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d94f3-114">Before you start</span></span>
<span data-ttu-id="d94f3-115">Avant d’écrire du code pour votre appareil, vous devez approvisionner votre solution préconfigurée de surveillance à distance et approvisionner un nouvel appareil personnalisé dans cette solution.</span><span class="sxs-lookup"><span data-stu-id="d94f3-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="d94f3-116">Approvisionner la solution préconfigurée de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="d94f3-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="d94f3-117">APPAREIL Hello vous créez dans ce didacticiel envoie instance tooan de données de hello [surveillance à distance] [ lnk-remote-monitoring] solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="d94f3-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="d94f3-118">Si vous n’avez pas déjà configuré hello solution préconfigurée dans votre compte Azure de surveillance à distance, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d94f3-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="d94f3-119">Sur hello <https://www.azureiotsuite.com/> , cliquez sur  **+**  toocreate une solution.</span><span class="sxs-lookup"><span data-stu-id="d94f3-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="d94f3-120">Cliquez sur **sélectionnez** sur hello **surveillance à distance** panneau toocreate votre solution.</span><span class="sxs-lookup"><span data-stu-id="d94f3-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="d94f3-121">Sur hello **créer distant solutions d’analyse** , entrez un **nom de la Solution** de votre choix, sélectionnez hello **région** vous le souhaitez toodeploy à et sélectionnez hello Azure abonnement toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="d94f3-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="d94f3-122">Cliquez ensuite sur **Créer la solution**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="d94f3-123">Attendez que hello processus de configuration est terminée.</span><span class="sxs-lookup"><span data-stu-id="d94f3-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="d94f3-124">les solutions de Hello préconfiguré utilisent les services Azure facturables.</span><span class="sxs-lookup"><span data-stu-id="d94f3-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="d94f3-125">Veillez tooremove hello solution préconfigurée à partir de votre abonnement lorsque vous avez terminé avec lui tooavoid tous les frais inutiles.</span><span class="sxs-lookup"><span data-stu-id="d94f3-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="d94f3-126">Vous pouvez supprimer complètement une solution préconfigurée de votre abonnement en visitant hello <https://www.azureiotsuite.com/> page.</span><span class="sxs-lookup"><span data-stu-id="d94f3-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="d94f3-127">Lorsque hello processus pour hello solution de surveillance à distance de configuration est terminée, cliquez sur **lancer** tooopen hello solution tableau de bord dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="d94f3-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Tableau de bord de solution][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="d94f3-129">Configurer votre appareil dans la solution de surveillance à distance de hello</span><span class="sxs-lookup"><span data-stu-id="d94f3-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="d94f3-130">Si vous avez déjà approvisionné un appareil dans votre solution, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="d94f3-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="d94f3-131">Vous avez besoin d’informations d’identification de périphérique tooknow hello lorsque vous créez l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="d94f3-132">Pour une solution toohello préconfiguré tooconnect des appareils, il doit s’identifier tooIoT concentrateur à l’aide des informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="d94f3-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="d94f3-133">Vous pouvez récupérer les informations d’identification de périphérique hello à partir du tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="d94f3-134">Pour inclure des informations d’identification de périphérique hello dans votre application cliente, plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d94f3-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="d94f3-135">tooadd une solution d’analyse à distance tooyour périphérique, hello complet suivant les étapes dans le tableau de bord de solution hello :</span><span class="sxs-lookup"><span data-stu-id="d94f3-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="d94f3-136">Dans hello coin inférieur gauche du tableau de bord hello, cliquez sur **ajouter un périphérique**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Ajout d’un appareil][1]
2. <span data-ttu-id="d94f3-138">Bonjour **personnalisé appareil** du panneau, cliquez sur **ajouter un nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Ajout d’un appareil personnalisé][2]
3. <span data-ttu-id="d94f3-140">Choisissez **Me laisser définir mon propre ID d'appareil**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="d94f3-141">Entrez un ID de périphérique tel **mydevice**, cliquez sur **vérifier l’ID** tooverify ce nom n’est pas déjà en cours d’utilisation, puis cliquez sur **créer** appareil de hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="d94f3-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Ajouter ID d’appareil][3]
4. <span data-ttu-id="d94f3-143">Rendre un périphérique de hello de note les informations d’identification (ID de périphérique, nom d’hôte du Hub IoT et clé de périphérique).</span><span class="sxs-lookup"><span data-stu-id="d94f3-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="d94f3-144">Votre application cliente doit ces toohello tooconnect de valeurs solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="d94f3-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="d94f3-145">Cliquez ensuite sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-145">Then click **Done**.</span></span>
   
    ![Afficher les informations d’identification d’un appareil][4]
5. <span data-ttu-id="d94f3-147">Sélectionnez votre appareil dans la liste des appareils hello dans le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="d94f3-148">Ensuite, dans hello **détails de l’appareil** du panneau, cliquez sur **activer le périphérique**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="d94f3-149">Hello de votre appareil est maintenant **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="d94f3-150">solution de surveillance à distance Hello peut maintenant recevoir les données de télémétrie à partir de votre appareil et d’appeler des méthodes sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="d94f3-151">Générer et exécuter l’exemple de solution hello C</span><span class="sxs-lookup"><span data-stu-id="d94f3-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="d94f3-152">Hello instructions suivantes décrivent les étapes de hello pour se connecter une [compatible mbed Freescale FRDM-K64F] [ lnk-mbed-home] toohello du périphérique distant solutions d’analyse.</span><span class="sxs-lookup"><span data-stu-id="d94f3-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="d94f3-153">Connexion réseau de tooyour hello mbed périphérique et ordinateur de bureau</span><span class="sxs-lookup"><span data-stu-id="d94f3-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="d94f3-154">Connecter hello mbed périphérique tooyour réseau à l’aide d’un câble Ethernet.</span><span class="sxs-lookup"><span data-stu-id="d94f3-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="d94f3-155">Cette étape est nécessaire, car l’application d’exemple hello requiert un accès internet.</span><span class="sxs-lookup"><span data-stu-id="d94f3-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="d94f3-156">Consultez [prise en main de mbed] [ lnk-mbed-getstarted] tooconnect votre PC de bureau tooyour mbed appareil.</span><span class="sxs-lookup"><span data-stu-id="d94f3-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="d94f3-157">Si votre ordinateur de bureau exécutant Windows, consultez [Configuration PC] [ lnk-mbed-pcconnect] dispositif de mbed tooyour accès tooconfigure port série.</span><span class="sxs-lookup"><span data-stu-id="d94f3-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="d94f3-158">Créer un projet de mbed et importer les exemples de code hello</span><span class="sxs-lookup"><span data-stu-id="d94f3-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="d94f3-159">Suivez ces tooadd étapes certains exemple de projet mbed de tooan code.</span><span class="sxs-lookup"><span data-stu-id="d94f3-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="d94f3-160">Vous importez le projet de démarrage d’analyse à distance hello et modifiez hello toouse de projet hello protocole MQTT au lieu de hello protocole AMQP.</span><span class="sxs-lookup"><span data-stu-id="d94f3-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="d94f3-161">Actuellement, vous devez toouse hello MQTT protocole toouse hello appareil fonctionnalités de gestion d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d94f3-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="d94f3-162">Dans votre navigateur web, accédez à toohello mbed.org [site de développement](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="d94f3-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="d94f3-163">Si vous n’avez pas encore inscrit, vous consultez un toocreate option un compte (il est disponible).</span><span class="sxs-lookup"><span data-stu-id="d94f3-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="d94f3-164">Autrement, connectez-vous avec les informations d’identification de votre compte.</span><span class="sxs-lookup"><span data-stu-id="d94f3-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="d94f3-165">Puis cliquez sur **compilateur** dans hello coin supérieur droit de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="d94f3-166">Cette action entraîne un toohello *espace de travail* interface.</span><span class="sxs-lookup"><span data-stu-id="d94f3-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="d94f3-167">Assurez-vous que la plateforme matérielle de hello vous utilisez s’affiche dans le coin supérieur droit hello de fenêtre hello ou cliquez sur icône hello dans hello à droite tooselect votre plateforme matérielle.</span><span class="sxs-lookup"><span data-stu-id="d94f3-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="d94f3-168">Cliquez sur **importation** sur le menu principal de hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="d94f3-169">Puis cliquez sur **cliquez ici tooimport à partir de l’URL**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![Espace de travail de démarrage importation toombed][6]

1. <span data-ttu-id="d94f3-171">Dans la fenêtre contextuelle de hello, entrez le lien de hello pour hello exemple code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ puis cliquez sur **importation**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importer l’espace de travail exemple code toombed][7]

1. <span data-ttu-id="d94f3-173">Dans la fenêtre de compilateur hello mbed, vous pouvez voir que l’importation de ce projet importe également les différentes bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="d94f3-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="d94f3-174">Certaines sont fournies et gérées par l’équipe de Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), tandis que d’autres sont des bibliothèques tierces disponibles dans le catalogue de bibliothèques mbed hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![Afficher le projet mbed][8]

1. <span data-ttu-id="d94f3-176">Bonjour **espace de travail de programme**, avec le bouton hello **iothub\_amqp\_transport** bibliothèque, cliquez sur **supprimer**, puis cliquez sur **OK** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="d94f3-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="d94f3-177">Bonjour **espace de travail de programme**, avec le bouton hello **azure\_amqp\_c** bibliothèque, cliquez sur **supprimer**, puis cliquez sur **OK**  tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="d94f3-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="d94f3-178">Avec le bouton hello **remote_monitoring** projet Bonjour **espace de travail de programme**, sélectionnez **bibliothèque d’importation**, puis sélectionnez **From URL**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Démarrer l’espace de travail bibliothèque importation toombed][6]

1. <span data-ttu-id="d94f3-180">Dans la fenêtre contextuelle de hello, entrez le lien de hello pour hello MQTT transport bibliothèque https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport / puis cliquez sur **importation**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importer l’espace de travail bibliothèque toombed][12]

1. <span data-ttu-id="d94f3-182">Répétition hello étape tooadd hello MQTT bibliothèque précédente à partir de https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="d94f3-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="d94f3-183">Votre espace de travail se présente désormais comme hello ci-après :</span><span class="sxs-lookup"><span data-stu-id="d94f3-183">Your workspace now looks like hello following:</span></span>

    ![Afficher l’espace de travail mbed][13]

1. <span data-ttu-id="d94f3-185">Hello ouvrir à distance\_monitoring\remote_monitoring.c fichier et qui n’existe hello remplacer `#include` instructions avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="d94f3-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

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
1. <span data-ttu-id="d94f3-186">Supprimer tous les hello code Bonjour à distance restant\_monitoring\remote\_monitoring.c fichier.</span><span class="sxs-lookup"><span data-stu-id="d94f3-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="d94f3-187">Générer et exécuter l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="d94f3-187">Build and run hello sample</span></span>

<span data-ttu-id="d94f3-188">Ajouter hello tooinvoke de code **distant\_analyse\_exécuter** fonction puis générer et exécuter l’application d’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="d94f3-189">Ajouter un **principal** fonction avec le code suivant à fin hello Hello distant\_hello de tooinvoke fichier monitoring.c **distant\_analyse\_exécuter** (fonction) :</span><span class="sxs-lookup"><span data-stu-id="d94f3-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="d94f3-190">Cliquez sur **compiler** programme de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="d94f3-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="d94f3-191">Vous pouvez sans risque ignorer les avertissements, mais si la génération de hello génère des erreurs, corrigez-les avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="d94f3-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="d94f3-192">Si la génération de hello est réussie, le site Web du compilateur hello mbed génère un fichier .bin nom hello de votre projet et le télécharge tooyour les ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d94f3-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="d94f3-193">Copier hello .bin fichier toohello l’appareil.</span><span class="sxs-lookup"><span data-stu-id="d94f3-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="d94f3-194">L’enregistrement d’unité de toohello de fichier .bin hello provoque hello appareil toorestart et exécuter le programme hello contenue dans le fichier .bin de hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="d94f3-195">Vous pouvez redémarrer manuellement les programme hello à tout moment en appuyant sur bouton Rétablir de hello sur l’appareil de mbed hello.</span><span class="sxs-lookup"><span data-stu-id="d94f3-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="d94f3-196">Connecter l’appareil toohello utilise une application client SSH tel que PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d94f3-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="d94f3-197">Vous pouvez déterminer le port série de hello que votre appareil utilise en vérifiant le Gestionnaire de périphériques Windows.</span><span class="sxs-lookup"><span data-stu-id="d94f3-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="d94f3-198">Dans PuTTY, cliquez sur hello **série** type de connexion.</span><span class="sxs-lookup"><span data-stu-id="d94f3-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="d94f3-199">Appareil de Hello se connecte généralement à 9 600 bauds, entrez 9600 Bonjour **vitesse** boîte.</span><span class="sxs-lookup"><span data-stu-id="d94f3-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="d94f3-200">Cliquez ensuite sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="d94f3-200">Then click **Open**.</span></span>

1. <span data-ttu-id="d94f3-201">programme de Hello commence à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="d94f3-201">hello program starts executing.</span></span> <span data-ttu-id="d94f3-202">Vous avez peut-être tooreset (appuyez sur CTRL + ATTN ou réinitialisation du tableau de presse hello) de carte mère hello si hello programme ne démarre pas automatiquement lorsque vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="d94f3-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
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
