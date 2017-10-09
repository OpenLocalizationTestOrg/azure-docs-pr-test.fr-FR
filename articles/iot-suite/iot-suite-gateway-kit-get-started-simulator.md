---
title: "aaaConnect un tooAzure passerelle IoT Suite à l’aide d’un NUC Intel | Documents Microsoft"
description: "Utilisez hello Microsoft IoT Commercial passerelle Kit et hello distant préconfigurée solution d’analyse. Utilisez Bonjour Azure IoT bord tooconnect toohello distant analyse de la solution, envoyer la télémétrie simulé toohello cloud et répondre toomethods appelé à partir du tableau de bord de solution hello."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="5c2e3-104">Se connecter à votre toohello de passerelle Azure IoT bord solution préconfigurée de surveillance à distance et d’envoyer la télémétrie simulé</span><span class="sxs-lookup"><span data-stu-id="5c2e3-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="5c2e3-105">Ce didacticiel vous montre comment toouse Azure IoT bord toosimulate température et l’humidité données toosend toohello l’analyse à distance préconfiguré solution.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="5c2e3-106">didacticiel de Hello utilise :</span><span class="sxs-lookup"><span data-stu-id="5c2e3-106">hello tutorial uses:</span></span>

- <span data-ttu-id="5c2e3-107">Un exemple de passerelle du tooimplement IoT bord Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="5c2e3-108">la surveillance à distance Hello IoT Suite, solution préconfigurée comme hello nuage back-end.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="5c2e3-109">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5c2e3-109">Overview</span></span>

<span data-ttu-id="5c2e3-110">Dans ce didacticiel, vous effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c2e3-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="5c2e3-111">Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="5c2e3-112">Cette étape déploie et configure automatiquement plusieurs services Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="5c2e3-113">Configurer votre toocommunicate de périphérique de passerelle Intel NUC avec votre ordinateur et de la solution d’analyse à distance hello.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="5c2e3-114">Configurer hello IoT bord passerelle toosend simulée télémétrie que vous pouvez afficher sur le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="5c2e3-115">Bonjour dispositions de solution de surveillance à distance à un ensemble de services Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="5c2e3-116">déploiement de Hello reflète une architecture d’entreprise réel.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="5c2e3-117">frais de la consommation Azure inutile tooavoid, supprimer votre instance de la solution de hello préconfiguré dans azureiotsuite.com lorsque vous avez terminé avec lui.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="5c2e3-118">Si vous avez besoin de hello solution préconfigurée à nouveau, vous pouvez le recréer facilement.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="5c2e3-119">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5c2e3-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="5c2e3-120">Répétez hello précédentes étapes tooadd un deuxième appareil à l’aide d’un ID de périphérique comme **device02**.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="5c2e3-121">exemple Hello envoie des données à partir de deux appareils simulés dans hello passerelle toohello distant solution d’analyse.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="5c2e3-122">Génération du module de IoT bord hello personnalisé</span><span class="sxs-lookup"><span data-stu-id="5c2e3-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="5c2e3-123">Vous pouvez à présent générer hello IoT bord module personnalisé qui permet de hello passerelle toosend messages toohello distant solution d’analyse.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="5c2e3-124">Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="5c2e3-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="5c2e3-125">Télécharger le code de source de hello pour les modules de IoT bord hello personnalisés à partir de GitHub à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="5c2e3-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="5c2e3-126">Génération du module IoT bord personnalisé de hello, à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="5c2e3-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="5c2e3-127">script de compilation Hello place le module de IoT bord personnalisé hello libsimulator.so dans le dossier de génération hello.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="5c2e3-128">Configurer et exécuter hello IoT passerelle</span><span class="sxs-lookup"><span data-stu-id="5c2e3-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="5c2e3-129">Vous pouvez maintenant configurer hello IoT bord passerelle toosend télémétrie simulé tooyour distant analyse du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="5c2e3-130">Pour plus d’informations sur la configuration d’une passerelle et des modules IoT Edge, voir [Concepts relatifs à Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="5c2e3-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="5c2e3-131">Dans ce didacticiel, vous utilisez standard de hello `vi` éditeur de texte sur hello NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="5c2e3-132">Si vous n’avez pas utilisé `vi` auparavant, vous devez effectuer un didacticiel d’introduction, telles que [Unix - hello vi didacticiel de l’éditeur] [ lnk-vi-tutorial] toofamiliarize vous-même avec cet éditeur.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="5c2e3-133">Vous pouvez également installer hello plus conviviaux [nano](https://www.nano-editor.org/) éditeur à l’aide de la commande hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="5c2e3-134">Fichier de configuration d’exemple hello ouvrir Bonjour **vi** éditeur à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5c2e3-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="5c2e3-135">Recherchez hello lignes dans la configuration de hello pour le module de IoTHub hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="5c2e3-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="5c2e3-136">Remplacez l’espace réservé de hello valeurs hello informations IoT Hub vous avez créé et enregistré à hello Démarrer de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="5c2e3-137">valeur Hello pour IoTHubName ressemble à **yourrmsolution37e08**, et la valeur hello pour IoTSuffix est généralement **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="5c2e3-138">Recherchez hello lignes dans la configuration de hello pour le module de mappage hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="5c2e3-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="5c2e3-139">Remplacez hello **deviceID** et **deviceKey** des espaces réservés avec les identificateurs hello et des clés pour les appareils hello deux créé précédemment dans la solution d’analyse à distance hello.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="5c2e3-140">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-140">Save your changes.</span></span>

<span data-ttu-id="5c2e3-141">Vous pouvez maintenant exécuter hello IoT passerelle hello suivant à l’aide de commandes :</span><span class="sxs-lookup"><span data-stu-id="5c2e3-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="5c2e3-142">passerelle de Hello démarre sur hello Intel NUC et envoie la solution de surveillance à distance de télémétrie simulé toohello :</span><span class="sxs-lookup"><span data-stu-id="5c2e3-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![La passerelle IoT Edge génère la télémétrie simulée][img-simulated telemetry]

<span data-ttu-id="5c2e3-144">Appuyez sur **Ctrl-C** programme de hello tooexit à tout moment.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="5c2e3-145">Télémétrie des consultations de hello</span><span class="sxs-lookup"><span data-stu-id="5c2e3-145">View hello telemetry</span></span>

<span data-ttu-id="5c2e3-146">Hello IoT passerelle envoie maintenant télémétrie simulé toohello une solution d’analyse à distance.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="5c2e3-147">Vous pouvez afficher les données de télémétrie hello sur le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="5c2e3-148">Accédez à tableau de bord toohello solution.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="5c2e3-149">Sélectionnez un des périphériques hello deux vous avez configuré dans la passerelle hello Bonjour **tooView de périphérique** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="5c2e3-150">télémétrie Hello à partir des passerelles hello s’affiche sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![Afficher les données de télémétrie des passerelles hello simulé][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="5c2e3-152">Si vous laissez hello solution en cours d’exécution dans votre compte Azure de surveillance à distance, vous êtes facturé pour hello exécution.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="5c2e3-153">Pour plus d’informations sur la réduction de la consommation lors hello s’exécute la solution de surveillance à distance, consultez [configuration Azure IoT Suite préconfiguré des solutions à des fins de démonstration][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="5c2e3-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="5c2e3-154">Supprimer la solution de hello préconfiguré à partir de votre compte Azure lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c2e3-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c2e3-155">Next steps</span></span>

<span data-ttu-id="5c2e3-156">Visitez hello [centre de développement Azure IoT](https://azure.microsoft.com/develop/iot/) pour plus d’exemples et documentation sur Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5c2e3-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started