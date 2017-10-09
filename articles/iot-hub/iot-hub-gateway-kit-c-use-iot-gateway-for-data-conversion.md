---
title: "conversion d’aaaData sur la passerelle IoT avec Azure IoT bord | Documents Microsoft"
description: "Utiliser IoT passerelle tooconvert hello le format de données de capteur via un module personnalisé à partir d’Azure IoT Edge."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conversion de données de passerelle iot, transformation des données de passerelle iot"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="cba81-104">Utiliser une passerelle IoT pour la transformation des données de capteur avec Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="cba81-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="cba81-105">Avant de commencer ce didacticiel, assurez-vous que vous avez terminé hello suivant les leçons dans l’ordre :</span><span class="sxs-lookup"><span data-stu-id="cba81-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="cba81-106">Configurer Intel NUC comme passerelle IoT</span><span class="sxs-lookup"><span data-stu-id="cba81-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="cba81-107">Utilisez IoT passerelle tooconnect choses toohello cloud - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cba81-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="cba81-108">L’un des objectifs d’une passerelle Iot est tooprocess collectées données avant de les envoyer toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="cba81-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="cba81-109">Azure IoT bord présente les modules qui peuvent être créés et assemblés tooform hello le traitement des données de workflow.</span><span class="sxs-lookup"><span data-stu-id="cba81-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="cba81-110">Un module reçoit un message, effectue une action sur celui-ci, puis déplacez-le d’autres tooprocess modules.</span><span class="sxs-lookup"><span data-stu-id="cba81-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="cba81-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="cba81-111">What you learn</span></span>

<span data-ttu-id="cba81-112">Vous allez apprendre comment les messages toocreate un tooconvert de module à partir de hello SensorTag dans un autre format.</span><span class="sxs-lookup"><span data-stu-id="cba81-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="cba81-113">Procédure</span><span class="sxs-lookup"><span data-stu-id="cba81-113">What you do</span></span>

* <span data-ttu-id="cba81-114">Créer un module tooconvert un message reçu dans le format de .json hello.</span><span class="sxs-lookup"><span data-stu-id="cba81-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="cba81-115">Compilez le module de hello.</span><span class="sxs-lookup"><span data-stu-id="cba81-115">Compile hello module.</span></span>
* <span data-ttu-id="cba81-116">Ajoutez hello module toohello BLE exemple d’application à partir d’Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="cba81-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="cba81-117">Exécutez l’exemple d’application hello.</span><span class="sxs-lookup"><span data-stu-id="cba81-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cba81-118">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="cba81-118">What you need</span></span>

* <span data-ttu-id="cba81-119">Hello suivant didacticiels effectuées dans l’ordre :</span><span class="sxs-lookup"><span data-stu-id="cba81-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="cba81-120">Configurer Intel NUC comme passerelle IoT</span><span class="sxs-lookup"><span data-stu-id="cba81-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="cba81-121">Utilisez IoT passerelle tooconnect choses toohello cloud - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cba81-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="cba81-122">Un client SSH qui s’exécute sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="cba81-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="cba81-123">PuTTY est recommandé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="cba81-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="cba81-124">Linux et macOS sont déjà accompagnés d’un client SSH.</span><span class="sxs-lookup"><span data-stu-id="cba81-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="cba81-125">adresse IP de Hello et hello nom d’utilisateur et mot de passe tooaccess hello passerelle à partir du client SSH hello.</span><span class="sxs-lookup"><span data-stu-id="cba81-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="cba81-126">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="cba81-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="cba81-127">Création d’un module</span><span class="sxs-lookup"><span data-stu-id="cba81-127">Create a module</span></span>

1. <span data-ttu-id="cba81-128">Sur l’ordinateur hôte hello, exécutez hello SSH client et toohello IoT passerelle de connexion.</span><span class="sxs-lookup"><span data-stu-id="cba81-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="cba81-129">Cloner des fichiers de source de hello du module de conversion hello à partir de GitHub toohello répertoire de la passerelle de IoT hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="cba81-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="cba81-130">Il s’agit d’un module Azure bord natif écrit en langage de programmation C de hello.</span><span class="sxs-lookup"><span data-stu-id="cba81-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="cba81-131">module de Hello convertit hello suivant un format hello de messages reçus :</span><span class="sxs-lookup"><span data-stu-id="cba81-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="cba81-132">Compilez le module de hello</span><span class="sxs-lookup"><span data-stu-id="cba81-132">Compile hello module</span></span>

<span data-ttu-id="cba81-133">module de hello toocompile, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="cba81-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="cba81-134">Vous obtenez un `libmy_module.so` fichier après la compilation de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="cba81-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="cba81-135">Prenez note du chemin d’accès absolu de hello de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="cba81-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="cba81-136">Ajouter l’application d’exemple hello module toohello BLE</span><span class="sxs-lookup"><span data-stu-id="cba81-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="cba81-137">Dossier d’exemples toohello accédez en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cba81-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="cba81-138">Ouvrez le fichier de configuration de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cba81-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="cba81-139">Ajouter un module en insérant hello suivant code toohello `modules` section.</span><span class="sxs-lookup"><span data-stu-id="cba81-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="cba81-140">Remplacez `[Your libmy_module.so path]` dans le code hello avec hello chemin d’accès absolu hello libmy_module.so' fichier.</span><span class="sxs-lookup"><span data-stu-id="cba81-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="cba81-141">Remplacez le code hello Bonjour `links` section avec hello suivant un :</span><span class="sxs-lookup"><span data-stu-id="cba81-141">Replace hello code in hello `links` section with hello following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="cba81-142">Appuyez sur `ESC`, puis tapez `:wq` fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="cba81-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="cba81-143">Exécutez l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="cba81-143">Run hello sample application</span></span>

1. <span data-ttu-id="cba81-144">Mise sous tension hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="cba81-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="cba81-145">Définir la variable d’environnement SSL_CERT_FILE hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cba81-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="cba81-146">Exécuter l’exemple d’application hello avec le module ajouté hello en exécutant hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cba81-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="cba81-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cba81-147">Next steps</span></span>

<span data-ttu-id="cba81-148">Vous avez correctement utilisation hello IoT passerelle tooconvert message d’appel de SensorTag au format de .json hello.</span><span class="sxs-lookup"><span data-stu-id="cba81-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
