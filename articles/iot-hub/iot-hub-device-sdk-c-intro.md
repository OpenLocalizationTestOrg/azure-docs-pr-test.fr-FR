---
title: "le périphérique aaaThe Azure IoT SDK pour C | Documents Microsoft"
description: "Prise en main du SDK de périphérique Azure IoT hello pour C et découvrez comment les applications pour appareil toocreate qui communiquent avec un hub IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="15468-103">Azure IoT device SDK pour C</span><span class="sxs-lookup"><span data-stu-id="15468-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="15468-104">Hello **Azure IoT appareil SDK** est un ensemble de bibliothèques conçu le processus de hello toosimplify d’envoi de messages tooand réception de messages hello **Azure IoT Hub** service.</span><span class="sxs-lookup"><span data-stu-id="15468-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="15468-105">Il existe différentes variantes de hello SDK, ciblant chacun une plateforme spécifique, mais cet article décrit hello **appareil Azure IoT SDK pour C**.</span><span class="sxs-lookup"><span data-stu-id="15468-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="15468-106">Dispositif de Azure IoT Hello SDK pour C est écrite en ANSI C (C99) toomaximize portabilité.</span><span class="sxs-lookup"><span data-stu-id="15468-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="15468-107">Cette fonctionnalité rend toooperate convient parfaitement de bibliothèques hello sur plusieurs plateformes et des périphériques, surtout lorsque la réduction du disque et l’encombrement mémoire est une priorité.</span><span class="sxs-lookup"><span data-stu-id="15468-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="15468-108">Il existe un large éventail de plateformes sur quel hello SDK a été testé (voir hello [Azure certifié pour le catalogue de périphérique IoT](https://catalog.azureiotsuite.com/) pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="15468-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="15468-109">Bien que cet article contient des procédures pas à pas de l’exemple de code en cours d’exécution sur la plate-forme de Windows hello, code hello décrit dans cet article est identique sur gamme hello des plateformes prises en charge.</span><span class="sxs-lookup"><span data-stu-id="15468-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="15468-110">Cet article vous présente d’architecture toohello du périphérique de Azure IoT hello SDK pour C. Il montre comment les bibliothèque de périphériques tooinitialize hello, envoyer des données tooIoT Hub et recevoir des messages à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="15468-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="15468-111">informations Hello dans cet article doivent être suffisamment tooget démarré à l’aide du Kit de développement logiciel de hello, mais il fournit également des informations de tooadditional des pointeurs sur les bibliothèques de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="15468-112">Architecture du kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="15468-112">SDK architecture</span></span>

<span data-ttu-id="15468-113">Vous pouvez trouver hello [ **appareil Azure IoT SDK pour C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub référentiel et consulter les détails de hello API Bonjour [référence d’API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="15468-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="15468-114">Vous trouverez la version la plus récente des bibliothèques de hello Hello Bonjour **master** branche du référentiel de hello :</span><span class="sxs-lookup"><span data-stu-id="15468-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="15468-115">Bonjour implémentation de base de hello SDK est Bonjour **iothub\_client** dossier qui contient l’implémentation de hello de couche API la plus basse hello Bonjour SDK : hello **IoTHubClient** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="15468-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="15468-116">Hello **IoTHubClient** bibliothèque contient des API implémentation brutes de messagerie pour envoyer des messages tooIoT concentrateur et de réception de messages à partir de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15468-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="15468-117">Lorsque vous utilisez cette bibliothèque, vous êtes responsable de la mise en œuvre de la sérialisation du message, mais d’autres détails concernant la communication avec IoT Hub sont gérés pour vous.</span><span class="sxs-lookup"><span data-stu-id="15468-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="15468-118">Hello **sérialiseur** dossier contient des fonctions d’assistance et des exemples qui montrent comment les données de tooserialize avant leur envoi à l’aide de Hub IoT tooAzure hello bibliothèque cliente.</span><span class="sxs-lookup"><span data-stu-id="15468-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="15468-119">utilisation de Hello de sérialiseur de hello n’est pas obligatoire et est fournie à titre informatif.</span><span class="sxs-lookup"><span data-stu-id="15468-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="15468-120">toouse hello **sérialiseur** bibliothèque, vous définissez un modèle qui spécifie les données toosend tooIoT Hub et hello messages hello souhaitées tooreceive à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="15468-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="15468-121">Une fois le modèle de hello est défini, hello Kit de développement logiciel vous apporte une surface API qui vous permet de tooeasily travail avec l’appareil-à-cloud et messages cloud-à-appareil sans se préoccuper hello détails de la sérialisation.</span><span class="sxs-lookup"><span data-stu-id="15468-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="15468-122">bibliothèque de Hello dépend d’autres bibliothèques open source qui implémentent le transport à l’aide des protocoles tels que MQTT et AMQP.</span><span class="sxs-lookup"><span data-stu-id="15468-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="15468-123">Hello **IoTHubClient** bibliothèque vis-à-vis d’autres bibliothèques open source :</span><span class="sxs-lookup"><span data-stu-id="15468-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="15468-124">Hello [Azure C partagé utilitaire](https://github.com/Azure/azure-c-shared-utility) bibliothèque, qui fournit des fonctionnalités communes pour les tâches de base (par exemple, les chaînes, la manipulation de la liste et e/s) nécessaire à travers plusieurs liées à Azure C kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="15468-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="15468-125">Hello [uAMQP Azure](https://github.com/Azure/azure-uamqp-c) bibliothèque, ce qui est une implémentation côté client de AMQP optimisée pour les appareils limité en ressources.</span><span class="sxs-lookup"><span data-stu-id="15468-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="15468-126">Hello [uMQTT Azure](https://github.com/Azure/azure-umqtt-c) bibliothèque, qui est une implémentation hello MQTT protocole de bibliothèque à usage général et optimisées pour les appareils limité en ressources.</span><span class="sxs-lookup"><span data-stu-id="15468-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="15468-127">Utilisation de ces bibliothèques est toounderstand plus facilement en examinant les exemples de code.</span><span class="sxs-lookup"><span data-stu-id="15468-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="15468-128">Hello les sections suivantes vous guide plusieurs exemples d’applications hello qui sont inclus dans le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="15468-129">Cette procédure pas à pas doit vous donner une bonne sentir pour hello différentes fonctionnalités de couches de l’architecture hello de hello Kit de développement logiciel et une hello toohow de présentation des API de travail.</span><span class="sxs-lookup"><span data-stu-id="15468-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="15468-130">Avant d’exécuter les exemples hello</span><span class="sxs-lookup"><span data-stu-id="15468-130">Before you run hello samples</span></span>

<span data-ttu-id="15468-131">Avant de pouvoir exécuter les exemples hello dans SDK de périphérique Azure IoT hello pour C, vous devez [créer une instance de hello IoT Hub service](iot-hub-create-through-portal.md) dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="15468-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="15468-132">Puis terminez hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="15468-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="15468-133">Préparer votre environnement de développement</span><span class="sxs-lookup"><span data-stu-id="15468-133">Prepare your development environment</span></span>
* <span data-ttu-id="15468-134">Obtenir les informations d’identification de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="15468-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="15468-135">Préparer votre environnement de développement</span><span class="sxs-lookup"><span data-stu-id="15468-135">Prepare your development environment</span></span>

<span data-ttu-id="15468-136">Les packages sont fournis pour les plates-formes courantes (telles que NuGet pour Windows ou apt_get pour Debian et Ubuntu) et les exemples hello utilisent ces packages lorsqu’il est disponible.</span><span class="sxs-lookup"><span data-stu-id="15468-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="15468-137">Dans certains cas, vous devez toocompile hello SDK pour ou sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="15468-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="15468-138">Si vous devez toocompile hello SDK, consultez [préparer votre environnement de développement](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) dans le référentiel GitHub de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="15468-139">code d’application exemple hello dans tooobtain, télécharger une copie de hello SDK à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="15468-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="15468-140">Obtenir une copie de la source de hello de hello **master** branche Hello [référentiel GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="15468-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="15468-141">Obtenir des informations d’identification de périphérique hello</span><span class="sxs-lookup"><span data-stu-id="15468-141">Obtain hello device credentials</span></span>

<span data-ttu-id="15468-142">Maintenant que vous avez les exemples de code source hello, hello suivant chose toodo est tooget un ensemble d’informations d’identification de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="15468-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="15468-143">Pour un tooaccess périphérique le toobe en mesure d’un hub IoT, vous devez d’abord ajouter hello appareil toohello Registre des identités IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15468-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="15468-144">Lorsque vous ajoutez votre appareil, vous obtenez un ensemble d’informations d’identification de périphérique dont vous avez besoin pour le hub IoT de hello appareil toobe tooconnect en mesure de toohello.</span><span class="sxs-lookup"><span data-stu-id="15468-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="15468-145">exemples d’applications Hello présentés dans la section suivante de hello attendent ces informations d’identification sous forme de hello d’un **chaîne de connexion de périphérique**.</span><span class="sxs-lookup"><span data-stu-id="15468-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="15468-146">Il existe plusieurs toohelp d’outils open source vous gérez votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="15468-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="15468-147">Une application Windows appelée [Explorateur d’appareils](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="15468-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="15468-148">Un outil d’interface de ligne de commande (CLI) multiplateforme node.js appelé [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="15468-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="15468-149">Ce didacticiel utilise hello graphique *Explorateur de périphérique* outil.</span><span class="sxs-lookup"><span data-stu-id="15468-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="15468-150">Vous pouvez également utiliser hello *iothub-explorer* outil si vous préférez toouse un outil CLI.</span><span class="sxs-lookup"><span data-stu-id="15468-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="15468-151">outil Explorateur de périphérique Hello utilise hello Azure IoT service bibliothèques tooperform diverses fonctions sur IoT Hub, y compris l’ajout de périphériques.</span><span class="sxs-lookup"><span data-stu-id="15468-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="15468-152">Si vous utilisez hello appareil explorer outil tooadd un appareil, vous obtenez une chaîne de connexion pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="15468-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="15468-153">Vous avez besoin de cette connexion chaîne toorun hello exemples d’applications.</span><span class="sxs-lookup"><span data-stu-id="15468-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="15468-154">Si vous n’êtes pas familiarisé avec l’outil Explorateur de périphérique hello, hello procédure décrit comment toouse il tooadd un appareil et d’obtenir une chaîne de connexion de périphérique.</span><span class="sxs-lookup"><span data-stu-id="15468-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="15468-155">outil d’explorer des appareils tooinstall hello, consultez [comment toouse hello Explorateur de périphérique pour les appareils IoT Hub](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="15468-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="15468-156">Lorsque vous exécutez le programme de hello, vous voyez cette interface :</span><span class="sxs-lookup"><span data-stu-id="15468-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="15468-157">Entrez votre **chaîne de connexion de Hub IoT** Bonjour premier champ, puis cliquez sur **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="15468-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="15468-158">Cette étape configure l’outil de hello afin qu’il puisse communiquer avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15468-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="15468-159">Lorsque hello chaîne de connexion de IoT Hub est configuré, cliquez sur hello **gestion** onglet :</span><span class="sxs-lookup"><span data-stu-id="15468-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="15468-160">Cet onglet est la gestion des appareils hello inscrits dans votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="15468-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="15468-161">Vous créez un périphérique en cliquant sur hello **créer** bouton.</span><span class="sxs-lookup"><span data-stu-id="15468-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="15468-162">Une boîte de dialogue avec un jeu de clés (primaire et secondaire) préalablement remplies s’affiche.</span><span class="sxs-lookup"><span data-stu-id="15468-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="15468-163">Entrez un **ID d’appareil**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="15468-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="15468-164">Lors de la création de l’appareil de hello, hello périphériques liste des mises à jour avec tous les périphériques hello enregistré, y compris hello que celui que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="15468-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="15468-165">Si vous cliquez avec le bouton droit sur le nouvel appareil, le menu qui suit s’affiche :</span><span class="sxs-lookup"><span data-stu-id="15468-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="15468-166">Si vous choisissez **copier la chaîne de connexion pour le périphérique sélectionné**, chaîne de connexion de périphérique hello est copié toohello Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="15468-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="15468-167">Conservez une copie de la chaîne de connexion de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="15468-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="15468-168">Vous avez besoin lors de l’exécution des exemples d’applications hello décrites dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="15468-169">Lorsque vous avez terminé les étapes de hello ci-dessus, vous êtes prêt toostart en cours d’exécution du code.</span><span class="sxs-lookup"><span data-stu-id="15468-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="15468-170">Les deux exemples, il est une constante haut hello hello principal fichier source qui permet de vous tooenter une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="15468-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="15468-171">Par exemple, hello ligne correspondante à partir de hello **iothub\_client\_exemple\_mqtt** application s’affiche comme suit.</span><span class="sxs-lookup"><span data-stu-id="15468-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="15468-172">Utiliser la bibliothèque IoTHubClient hello</span><span class="sxs-lookup"><span data-stu-id="15468-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="15468-173">Au sein de hello **iothub\_client** dossier Bonjour [azure iot-sdk--c](https://github.com/azure/azure-iot-sdk-c) référentiel, il existe un **exemples** dossier qui contient une application appelée **iothub\_client\_exemple\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="15468-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="15468-174">version de Windows Hello de hello **iothub\_client\_exemple\_mqtt** application inclut hello suivant la solution Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="15468-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="15468-175">Si vous ouvrez ce projet dans Visual Studio 2017, accepter hello invites tooretarget hello projet toohello dernière version.</span><span class="sxs-lookup"><span data-stu-id="15468-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="15468-176">Cette solution inclut un seul projet :</span><span class="sxs-lookup"><span data-stu-id="15468-176">This solution contains a single project.</span></span> <span data-ttu-id="15468-177">Cette solution installe quatre packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="15468-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="15468-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="15468-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="15468-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="15468-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="15468-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="15468-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="15468-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="15468-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="15468-182">Vous devez toujours hello **Microsoft.Azure.C.SharedUtility** lorsque vous travaillez avec le Kit de développement logiciel de hello du package.</span><span class="sxs-lookup"><span data-stu-id="15468-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="15468-183">Cet exemple utilise le protocole MQTT hello, par conséquent, vous devez inclure hello **Microsoft.Azure.umqtt** et **Microsoft.Azure.IoTHub.MqttTransport** packages (il existe des packages équivalentes pour HTTP et AMQP ).</span><span class="sxs-lookup"><span data-stu-id="15468-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="15468-184">Étant donné que l’exemple hello utilise hello **IoTHubClient** bibliothèque, vous devez également inclure hello **Microsoft.Azure.IoTHub.IoTHubClient** package dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="15468-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="15468-185">Vous pouvez trouver l’implémentation hello pour exemple d’application hello Bonjour **iothub\_client\_exemple\_mqtt.c** fichier source.</span><span class="sxs-lookup"><span data-stu-id="15468-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="15468-186">Hello étapes suivantes utilisent ce toowalk d’application exemple vous guide dans les étapes nécessaires toouse hello **IoTHubClient** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="15468-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="15468-187">Initialisation de la bibliothèque de hello</span><span class="sxs-lookup"><span data-stu-id="15468-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="15468-188">Avant de commencer à utiliser avec les bibliothèques hello, vous devrez peut-être tooperform une initialisation spécifique à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="15468-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="15468-189">Par exemple, si vous envisagez de toouse AMQP sur Linux, vous devez initialiser bibliothèque OpenSSL de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="15468-190">Hello exemples Bonjour [référentiel GitHub](https://github.com/Azure/azure-iot-sdk-c) appeler la fonction de l’utilitaire hello **plateforme\_init** lorsque hello client démarre et appeler hello **plateforme\_deinit**  (fonction) avant de quitter.</span><span class="sxs-lookup"><span data-stu-id="15468-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="15468-191">Ces fonctions sont déclarées dans le fichier d’en-tête platform.h hello.</span><span class="sxs-lookup"><span data-stu-id="15468-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="15468-192">Examiner les définitions de ces fonctions pour votre plateforme cible Bonjour hello [référentiel](https://github.com/Azure/azure-iot-sdk-c) toodetermine si vous avez besoin tooinclude tout code d’initialisation propre à la plateforme dans votre client.</span><span class="sxs-lookup"><span data-stu-id="15468-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="15468-193">tout d’abord, toostart dans les bibliothèques de hello, allouer un handle de client IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="15468-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="15468-194">Vous passez d’une copie de la chaîne de connexion de périphérique hello que vous obtenu à partir de la fonction de toothis l’outil Explorateur hello appareil.</span><span class="sxs-lookup"><span data-stu-id="15468-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="15468-195">Vous désignez également toouse de protocole de communication hello.</span><span class="sxs-lookup"><span data-stu-id="15468-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="15468-196">Cet exemple utilise MQTT, mais AMQP et HTTP sont également possibles.</span><span class="sxs-lookup"><span data-stu-id="15468-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="15468-197">Lorsque vous avez valide **IOTHUB\_CLIENT\_gérer**, vous pouvez commencer à appeler hello API toosend et recevoir des messages tooand de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15468-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="15468-198">Envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="15468-198">Send messages</span></span>

<span data-ttu-id="15468-199">exemple d’application Hello définit un hub IoT de boucle toosend messages tooyour.</span><span class="sxs-lookup"><span data-stu-id="15468-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="15468-200">Hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="15468-200">hello following snippet:</span></span>

- <span data-ttu-id="15468-201">Crée un message.</span><span class="sxs-lookup"><span data-stu-id="15468-201">Creates a message.</span></span>
- <span data-ttu-id="15468-202">Ajoute une propriété message toohello.</span><span class="sxs-lookup"><span data-stu-id="15468-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="15468-203">Envoie un message.</span><span class="sxs-lookup"><span data-stu-id="15468-203">Sends a message.</span></span>

<span data-ttu-id="15468-204">Tout d’abord, créez un message :</span><span class="sxs-lookup"><span data-stu-id="15468-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="15468-205">Chaque fois que vous envoyez un message, vous spécifiez une fonction de rappel tooa référence qui est appelée lorsque les données hello sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="15468-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="15468-206">Dans cet exemple, la fonction de rappel hello est appelée **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="15468-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="15468-207">Hello suivant extrait de code montre cette fonction de rappel :</span><span class="sxs-lookup"><span data-stu-id="15468-207">hello following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="15468-208">Notez hello appel toohello **IoTHubMessage\_détruire** lorsque vous avez terminé avec le message d’appel de fonction.</span><span class="sxs-lookup"><span data-stu-id="15468-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="15468-209">Cette fonction libère les ressources de hello alloués lors de la création du message de type hello.</span><span class="sxs-lookup"><span data-stu-id="15468-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="15468-210">Recevoir des messages</span><span class="sxs-lookup"><span data-stu-id="15468-210">Receive messages</span></span>

<span data-ttu-id="15468-211">La réception d’un message est une opération asynchrone.</span><span class="sxs-lookup"><span data-stu-id="15468-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="15468-212">Tout d’abord, vous inscrivez hello rappel tooinvoke lors de l’appareil de hello reçoit un message :</span><span class="sxs-lookup"><span data-stu-id="15468-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="15468-213">Hello dernier paramètre est un toowhatever pointeur void souhaité.</span><span class="sxs-lookup"><span data-stu-id="15468-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="15468-214">Dans l’exemple hello, il s’agit d’un entier de tooan de pointeur, mais elle peut être un pointeur tooa structure de données plus complexe.</span><span class="sxs-lookup"><span data-stu-id="15468-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="15468-215">Ce paramètre permet de toooperate de fonction de rappel hello sur l’état partagé avec un appelant de hello de cette fonction.</span><span class="sxs-lookup"><span data-stu-id="15468-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="15468-216">Lors de l’appareil de hello reçoit un message, hello inscrits fonction de rappel est appelée.</span><span class="sxs-lookup"><span data-stu-id="15468-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="15468-217">Cette fonction de rappel récupère :</span><span class="sxs-lookup"><span data-stu-id="15468-217">This callback function retrieves:</span></span>

* <span data-ttu-id="15468-218">id de message Hello et id de corrélation de message de type hello.</span><span class="sxs-lookup"><span data-stu-id="15468-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="15468-219">contenu du message Hello.</span><span class="sxs-lookup"><span data-stu-id="15468-219">hello message content.</span></span>
* <span data-ttu-id="15468-220">Toutes les propriétés personnalisées à partir du message de type hello.</span><span class="sxs-lookup"><span data-stu-id="15468-220">Any custom properties from hello message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="15468-221">Hello d’utilisation **IoTHubMessage\_GetByteArray** fonction tooretrieve message de type hello, qui dans cet exemple est une chaîne.</span><span class="sxs-lookup"><span data-stu-id="15468-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="15468-222">Annuler l’initialisation de la bibliothèque de hello</span><span class="sxs-lookup"><span data-stu-id="15468-222">Uninitialize hello library</span></span>

<span data-ttu-id="15468-223">Lorsque vous avez terminé d’envoi d’événements et réception de messages, vous pouvez annuler l’initialisation de bibliothèque de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="15468-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="15468-224">toodo émettre donc hello après l’appel de fonction :</span><span class="sxs-lookup"><span data-stu-id="15468-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="15468-225">Cet appel permet de libérer les ressources hello précédemment alloués par hello **IoTHubClient\_CreateFromConnectionString** (fonction).</span><span class="sxs-lookup"><span data-stu-id="15468-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="15468-226">Comme vous pouvez le voir, il est facile toosend et recevoir des messages avec hello **IoTHubClient** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="15468-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="15468-227">bibliothèque Hello gère les détails de hello de communiquer avec IoT Hub, y compris le toouse protocol (du point de vue hello du développeur de hello, c’est une option de configuration simple).</span><span class="sxs-lookup"><span data-stu-id="15468-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="15468-228">Hello **IoTHubClient** bibliothèque fournit également un contrôle précis sur comment les données de salutation tooserialize votre appareil envoie tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15468-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="15468-229">Dans certains cas, ce niveau de contrôle est un avantage, mais dans d’autres, il est un détail d’implémentation que vous ne souhaitez pas toobe concerné avec.</span><span class="sxs-lookup"><span data-stu-id="15468-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="15468-230">Si tel est le cas de hello, vous pouvez envisager d’utiliser hello **sérialiseur** bibliothèque, ce qui est décrit dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="15468-231">Utiliser la bibliothèque sérialiseur hello</span><span class="sxs-lookup"><span data-stu-id="15468-231">Use hello serializer library</span></span>

<span data-ttu-id="15468-232">Point de vue conceptuel hello **sérialiseur** bibliothèque se situe au-dessus hello **IoTHubClient** bibliothèque Bonjour SDK.</span><span class="sxs-lookup"><span data-stu-id="15468-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="15468-233">Il utilise hello **IoTHubClient** bibliothèque pour hello sous-jacent de la communication avec IoT Hub, mais il ajoute des fonctionnalités de modélisation qui suppriment les charge hello de traitement de sérialisation de messages de développeur de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="15468-234">Le fonctionnement de la bibliothèque est mieux illustré par un exemple.</span><span class="sxs-lookup"><span data-stu-id="15468-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="15468-235">À l’intérieur hello **sérialiseur** dossier Bonjour [azure iot-sdk--c référentiel](https://github.com/Azure/azure-iot-sdk-c), est un **exemples** dossier qui contient une application appelée **simplesample \_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="15468-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="15468-236">version de Windows Hello de cet exemple inclut hello suivant la solution Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="15468-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="15468-237">Si vous ouvrez ce projet dans Visual Studio 2017, accepter hello invites tooretarget hello projet toohello dernière version.</span><span class="sxs-lookup"><span data-stu-id="15468-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="15468-238">Comme avec l’exemple précédent de hello, celle-ci comprend plusieurs packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="15468-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="15468-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="15468-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="15468-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="15468-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="15468-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="15468-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="15468-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="15468-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="15468-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="15468-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="15468-244">Vous avez vu la plupart de ces packages dans l’exemple précédent de hello, mais **Microsoft.Azure.IoTHub.Serializer** est nouveau.</span><span class="sxs-lookup"><span data-stu-id="15468-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="15468-245">Ce package est requis lorsque vous utilisez hello **sérialiseur** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="15468-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="15468-246">Vous trouverez une implémentation hello de l’exemple d’application hello Bonjour **simplesample\_mqtt.c** fichier.</span><span class="sxs-lookup"><span data-stu-id="15468-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="15468-247">Hello sections suivantes vous guident dans les parties de clé hello de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="15468-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="15468-248">Initialisation de la bibliothèque de hello</span><span class="sxs-lookup"><span data-stu-id="15468-248">Initialize hello library</span></span>

<span data-ttu-id="15468-249">toostart utilisation de hello **sérialiseur** bibliothèque, les appels API de l’initialisation hello :</span><span class="sxs-lookup"><span data-stu-id="15468-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="15468-250">Hello appel toohello **sérialiseur\_init** fonction est un appel à usage unique et l’initialise hello bibliothèque sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="15468-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="15468-251">Ensuite, vous appelez hello **IoTHubClient\_LL\_CreateFromConnectionString** fonction, qui est hello même API que dans hello **IoTHubClient** exemple.</span><span class="sxs-lookup"><span data-stu-id="15468-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="15468-252">Cet appel définit la chaîne de connexion de votre périphérique (cet appel est également où vous choisissez le protocole de hello souhaité toouse).</span><span class="sxs-lookup"><span data-stu-id="15468-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="15468-253">Cet exemple utilise MQTT comme couche de transport hello, mais il peut utiliser AMQP ou HTTP.</span><span class="sxs-lookup"><span data-stu-id="15468-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="15468-254">Enfin, appelez hello **créer\_modèle\_INSTANCE** (fonction).</span><span class="sxs-lookup"><span data-stu-id="15468-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="15468-255">**WeatherStation** est l’espace de noms hello du modèle de hello et **ContosoAnemometer** est le nom hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="15468-256">Une fois que l’instance de modèle hello est créé, vous pouvez l’utiliser toostart envoyer et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="15468-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="15468-257">Toutefois, il est important toounderstand un quel modèle est.</span><span class="sxs-lookup"><span data-stu-id="15468-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="15468-258">Définir le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="15468-258">Define hello model</span></span>

<span data-ttu-id="15468-259">Un modèle Bonjour **sérialiseur** bibliothèque définit les messages de salutation votre appareil peut envoyer tooIoT messages Hub et hello, appelé *actions* Bonjour langage de modélisation, qui peut recevoir.</span><span class="sxs-lookup"><span data-stu-id="15468-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="15468-260">Vous définissez un modèle à l’aide d’un ensemble de macros C comme hello **simplesample\_mqtt** exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="15468-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="15468-261">Hello **commencer\_espace de noms** et **fin\_espace de noms** macros les deux prennent hello espace de noms du modèle hello en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="15468-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="15468-262">Il est probable que quoi que ce soit entre ces macros est définition hello de votre modèle ou de modèles et structures de données hello qui utilisent des modèles de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="15468-263">Dans cet exemple, il existe un seul modèle appelé **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="15468-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="15468-264">Ce modèle définit deux éléments de données que votre appareil peut envoyer tooIoT Hub : **DeviceId** et **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="15468-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="15468-265">Il définit également trois actions (messages) que votre appareil peut recevoir : **TurnFanOn**, **TurnFanOff** et **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="15468-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="15468-266">Chaque élément de données possède un type et chaque action a un nom (et éventuellement, un ensemble de paramètres).</span><span class="sxs-lookup"><span data-stu-id="15468-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="15468-267">les données de salutation et les actions définies dans le modèle de hello définissent une surface API que vous pouvez utiliser toosend messages tooIoT Hub et répondre toomessages envoyés toohello appareil.</span><span class="sxs-lookup"><span data-stu-id="15468-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="15468-268">Un exemple permet de mieux comprendre l’utilisation de ce modèle.</span><span class="sxs-lookup"><span data-stu-id="15468-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="15468-269">Envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="15468-269">Send messages</span></span>

<span data-ttu-id="15468-270">modèle de Hello définit des données hello vous pouvez envoyer tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15468-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="15468-271">Dans cet exemple, cela signifie qu’un des hello deux éléments de données définis à l’aide de hello **WITH_DATA** (macro).</span><span class="sxs-lookup"><span data-stu-id="15468-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="15468-272">Il existe plusieurs toosend requis d’étapes **DeviceId** et **WindSpeed** IoT hub tooan de valeurs.</span><span class="sxs-lookup"><span data-stu-id="15468-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="15468-273">Hello est tout d’abord tooset hello données toosend :</span><span class="sxs-lookup"><span data-stu-id="15468-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="15468-274">Hello modèle défini précédemment vous permet des valeurs hello tooset en définissant les membres d’un **struct**.</span><span class="sxs-lookup"><span data-stu-id="15468-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="15468-275">Ensuite, sérialiser le message de salutation souhaité toosend :</span><span class="sxs-lookup"><span data-stu-id="15468-275">Next, serialize hello message you want toosend:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="15468-276">Ce code sérialise la mémoire tampon de périphérique dans le cloud tooa hello (référencé par **destination**).</span><span class="sxs-lookup"><span data-stu-id="15468-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="15468-277">code de Hello puis appelle hello **sendMessage** fonction toosend hello message tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="15468-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="15468-278">Hello du deuxième paramètre toolast de **IoTHubClient\_LL\_SendEventAsync** est une fonction de rappel de tooa de référence qui est appelée quand les données hello sont envoyées avec succès.</span><span class="sxs-lookup"><span data-stu-id="15468-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="15468-279">Voici la fonction de rappel hello dans l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="15468-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="15468-280">Hello deuxième paramètre est un contexte de toouser pointeur ; Hello même pointeur passé trop**IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="15468-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="15468-281">Dans ce cas, le contexte de hello est un compteur simple, mais il peut s’agir comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="15468-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="15468-282">C’est tout est toosending les messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="15468-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="15468-283">Hello uniquement gauche toocover consiste comment tooreceive messages.</span><span class="sxs-lookup"><span data-stu-id="15468-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="15468-284">Recevoir des messages</span><span class="sxs-lookup"><span data-stu-id="15468-284">Receive messages</span></span>

<span data-ttu-id="15468-285">Réception d’un message fonctionne de façon similaire toohello fonctionnement de messages de hello **IoTHubClient** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="15468-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="15468-286">Tout d’abord, vous enregistrez une fonction de rappel de message :</span><span class="sxs-lookup"><span data-stu-id="15468-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="15468-287">Ensuite, vous écrivez la fonction de rappel hello est appelée lorsqu’un message est reçu :</span><span class="sxs-lookup"><span data-stu-id="15468-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="15468-288">Ce code est réutilisable--il a hello même pour une solution.</span><span class="sxs-lookup"><span data-stu-id="15468-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="15468-289">Cette fonction reçoit le message de type hello et prend en charge le routage il toohello la fonction appropriée via l’appel de hello trop**EXECUTE\_commande**.</span><span class="sxs-lookup"><span data-stu-id="15468-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="15468-290">fonction Hello appelée dépend à ce stade de la définition de hello d’actions hello dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="15468-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="15468-291">Lorsque vous définissez une action dans votre modèle, que vous devez tooimplement une fonction qui est appelée lorsque votre appareil reçoit le message de type hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="15468-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="15468-292">Par exemple, si votre modèle définit cette action :</span><span class="sxs-lookup"><span data-stu-id="15468-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="15468-293">Définissez une fonction avec cette signature :</span><span class="sxs-lookup"><span data-stu-id="15468-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="15468-294">Notez comment hello nom de fonction hello correspond au nom hello d’action hello dans le modèle de hello et que les paramètres de fonction hello hello correspondent aux paramètres de hello spécifiés pour l’action de hello.</span><span class="sxs-lookup"><span data-stu-id="15468-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="15468-295">Hello premier paramètre est toujours requis et contient une instance de toohello de pointeur de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="15468-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="15468-296">Lors de l’appareil de hello reçoit un message qui correspond à cette signature, la fonction correspondante de hello est appelée.</span><span class="sxs-lookup"><span data-stu-id="15468-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="15468-297">Par conséquent, à l’exception d’ayant un code réutilisable hello tooinclude de **IoTHubMessage**, recevoir des messages est simplement de la définition d’une fonction simple pour chaque action définie dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="15468-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="15468-298">Annuler l’initialisation de la bibliothèque de hello</span><span class="sxs-lookup"><span data-stu-id="15468-298">Uninitialize hello library</span></span>

<span data-ttu-id="15468-299">Lorsque vous avez terminé d’envoi de données et recevoir des messages, vous pouvez annuler l’initialisation de bibliothèque de IoT hello :</span><span class="sxs-lookup"><span data-stu-id="15468-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="15468-300">Chacune de ces trois fonctions s’aligne avec trois fonctions d’initialisation hello décrites précédemment.</span><span class="sxs-lookup"><span data-stu-id="15468-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="15468-301">L’appel de ces API vous permet de libérer les ressources affectées au préalable.</span><span class="sxs-lookup"><span data-stu-id="15468-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15468-302">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="15468-302">Next Steps</span></span>

<span data-ttu-id="15468-303">Cet article couvert les principes fondamentaux de hello de l’utilisation de bibliothèques hello Bonjour **appareil Azure IoT SDK pour C**. Il vous fourni suffisamment toounderstand informations ce qui est inclus dans hello SDK, son architecture, et comment tooget commencer à utiliser les exemples Windows hello.</span><span class="sxs-lookup"><span data-stu-id="15468-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="15468-304">l’article suivant de Hello continue description hello Hello SDK en expliquant [plus sur la bibliothèque de IoTHubClient hello](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="15468-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="15468-305">toolearn plus sur le développement pour IoT Hub, consultez hello [kits de développement logiciel Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="15468-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="15468-306">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="15468-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="15468-307">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="15468-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
