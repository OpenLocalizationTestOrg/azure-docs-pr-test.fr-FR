---
title: "visualisation aaaReal au moment des données de capteur à partir de votre concentrateur Azure IoT – applications Web | Documents Microsoft"
description: "Utilisez la fonctionnalité de Web Apps de hello de Microsoft Azure App Service toovisualize température et humidité données sont collectées à partir de capteur de hello et envoyées tooyour Iot hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualisation de données en temps réel, visualisation de données en direct, visualisation de données de capteurs"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="27284-104">Visualiser les données de capteur en temps réel à partir de votre concentrateur Azure IoT par à l’aide de la fonctionnalité d’applications Web hello du Service d’applications Azure</span><span class="sxs-lookup"><span data-stu-id="27284-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="27284-106">Contenu</span><span class="sxs-lookup"><span data-stu-id="27284-106">What you learn</span></span>

<span data-ttu-id="27284-107">Dans ce didacticiel, vous découvrez comment les données de capteur en temps réel de toovisualize votre hub IoT reçoit en exécutant une application web qui sont hébergées sur une application web.</span><span class="sxs-lookup"><span data-stu-id="27284-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="27284-108">Si vous souhaitez que les données de salutation toovisualize tootry dans votre IoT hub à l’aide de Power BI, consultez [données de capteur en temps réel toovisualize utiliser Power BI à partir d’Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="27284-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="27284-109">Procédure</span><span class="sxs-lookup"><span data-stu-id="27284-109">What you do</span></span>

- <span data-ttu-id="27284-110">Bonjour portail Azure, créez une application web.</span><span class="sxs-lookup"><span data-stu-id="27284-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="27284-111">Préparez votre instance IoT Hub pour l’accès aux données via l’ajout d’un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="27284-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="27284-112">Configurer les données de capteur hello web application tooread à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="27284-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="27284-113">Télécharger un toobe d’application web hébergée par l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="27284-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="27284-114">Ouvrez hello web toosee en temps réel température et humidité données d’application à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="27284-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="27284-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="27284-115">What you need</span></span>

- <span data-ttu-id="27284-116">[Configurer votre périphérique](iot-hub-raspberry-pi-kit-node-get-started.md), qui couvre hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="27284-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="27284-117">Un abonnement Azure actif</span><span class="sxs-lookup"><span data-stu-id="27284-117">An active Azure subscription</span></span>
  - <span data-ttu-id="27284-118">Un IoT Hub associé à votre abonnement</span><span class="sxs-lookup"><span data-stu-id="27284-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="27284-119">Une application cliente qui envoie l’Iot hub tooyour de messages</span><span class="sxs-lookup"><span data-stu-id="27284-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="27284-120">Télécharger Git</span><span class="sxs-lookup"><span data-stu-id="27284-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="27284-121">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="27284-121">Create a web app</span></span>

1. <span data-ttu-id="27284-122">Bonjour [portail Azure](https://ms.portal.azure.com/), cliquez sur **nouveau** > **Web + Mobile** > **application Web**.</span><span class="sxs-lookup"><span data-stu-id="27284-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="27284-123">Entrez un nom unique de la tâche, vérifier hello abonnement, spécifiez un groupe de ressources et un emplacement, sélectionnez **code confidentiel toodashboard**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="27284-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="27284-124">Nous vous recommandons de sélectionner hello même emplacement que celui de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="27284-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="27284-125">Cela aide à la vitesse de traitement et réduit le coût de hello de transfert de données.</span><span class="sxs-lookup"><span data-stu-id="27284-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![Créer une application web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="27284-127">Configurer application web hello tooread des données à partir de votre hub IoT</span><span class="sxs-lookup"><span data-stu-id="27284-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="27284-128">Ouvrez hello uniquement, vous avez configuré l’application web.</span><span class="sxs-lookup"><span data-stu-id="27284-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="27284-129">Cliquez sur **paramètres de l’Application**, puis, sous **paramètres de l’application**, ajouter hello suivant des paires clé/valeur :</span><span class="sxs-lookup"><span data-stu-id="27284-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="27284-130">Clé</span><span class="sxs-lookup"><span data-stu-id="27284-130">Key</span></span>                                   | <span data-ttu-id="27284-131">Valeur</span><span class="sxs-lookup"><span data-stu-id="27284-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="27284-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="27284-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="27284-133">Obtenu à partir de iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="27284-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="27284-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="27284-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="27284-135">nom de Hello du groupe de consommateurs hello que vous ajoutez tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="27284-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![Ajouter des paramètres tooyour web application avec des paires clé/valeur](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="27284-137">Cliquez sur **paramètres de l’Application**, sous **paramètres généraux**, hello de bascule **WebSockets** option, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="27284-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![Basculer hello Web sockets (option)](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="27284-139">Télécharger un toobe d’application web hébergée par l’application web hello</span><span class="sxs-lookup"><span data-stu-id="27284-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="27284-140">Sur GitHub, nous avons mis à disposition une application web qui affiche des données de capteur en temps réel à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="27284-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="27284-141">Vous devez toodo est configurer hello web application toowork avec un référentiel Git, télécharger des hello d’application web à partir de GitHub et téléchargez-le tooAzure pour hello web application toohost.</span><span class="sxs-lookup"><span data-stu-id="27284-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="27284-142">Dans l’application web de hello, cliquez sur **Options de déploiement** > **choisir la Source de** > **référentiel Git Local**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="27284-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configurer votre web application déploiement toouse hello référentiel Git local](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="27284-144">Cliquez sur **informations d’identification de déploiement**, créez un utilisateur et mot de passe toouse tooconnect toohello référentiel Git dans Azure, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="27284-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="27284-145">Cliquez sur **vue d’ensemble**et notez la valeur hello **url de clone Git**.</span><span class="sxs-lookup"><span data-stu-id="27284-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![Obtenir l’URL de clone Git hello de votre application web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="27284-147">Ouvrez une commande ou une fenêtre de terminal sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="27284-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="27284-148">Télécharger l’application hello web à partir de GitHub et télécharger tooAzure pour hello web application toohost.</span><span class="sxs-lookup"><span data-stu-id="27284-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="27284-149">toodo, c’est le cas, exécutez hello commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="27284-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="27284-150">\<URL de clone GIT\> URL hello du référentiel Git de hello trouvé sur hello **vue d’ensemble** page de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="27284-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="27284-151">Ouvrez hello web toosee en temps réel température et humidité données d’application à partir de votre hub IoT</span><span class="sxs-lookup"><span data-stu-id="27284-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="27284-152">Sur hello **vue d’ensemble** page de votre application web, cliquez sur l’application web hello URL tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="27284-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![Obtenir l’URL de hello de votre application web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="27284-154">Vous devez voir la température en temps réel de hello et les données de l’humidité à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="27284-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![Page d’application web affichant l’humidité et la température en temps réel](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="27284-156">Vérifiez l’application d’exemple hello est en cours d’exécution sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="27284-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="27284-157">Si non, vous obtenez un graphique vide, vous pouvez consulter des didacticiels toohello sous [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="27284-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27284-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="27284-158">Next steps</span></span>
<span data-ttu-id="27284-159">Vous avez utilisé avec succès vos données de capteur en temps réel de toovisualize application web à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="27284-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="27284-160">Pour une autre façon toovisualize des données depuis Azure IoT Hub, consultez [données de capteur en temps réel toovisualize utiliser Power BI à partir de votre hub IoT](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="27284-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
