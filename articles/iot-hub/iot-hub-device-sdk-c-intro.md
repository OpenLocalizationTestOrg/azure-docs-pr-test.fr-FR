---
title: "Le Kit de développement logiciel (SDK) d’appareil Azure IoT pour C | Microsoft Docs"
description: "Prenez en main Azure IoT device SDK pour C et apprenez à créer des applications d’appareil qui communiquent avec un IoT Hub."
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
ms.openlocfilehash: 459b630f28fe48064f4ba280974f3fdbdb82f0a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="c0d23-103">Azure IoT device SDK pour C</span><span class="sxs-lookup"><span data-stu-id="c0d23-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="c0d23-104">Le **Kit de développement logiciel (SDK) d’appareil Azure IoT** (Azure IoT device SDK) est un ensemble de bibliothèques conçu pour simplifier le processus d’envoi et de réception de messages vers et à partir du service **Azure IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="c0d23-105">Il existe différentes variantes de ce kit de développement logiciel, chacune concernant une plateforme spécifique, mais cet article met l'accent sur le **kit de développement logiciel Azure IoT device SDK pour C**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="c0d23-106">Le kit de développement logiciel d’appareil Azure IoT pour C est rédigé en code ANSI C (C99) afin d’optimiser sa portabilité.</span><span class="sxs-lookup"><span data-stu-id="c0d23-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="c0d23-107">Cette fonctionnalité rend les bibliothèques adaptées pour fonctionner sur plusieurs plateformes et appareils, en particulier quand la réduction de l’encombrement du disque et de l’empreinte mémoire est une priorité.</span><span class="sxs-lookup"><span data-stu-id="c0d23-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="c0d23-108">Le Kit de développement logiciel (SDK) a été testé sur un large éventail de plateformes (consultez le [Catalogue d’appareils certifiés Azure pour l’IoT](https://catalog.azureiotsuite.com/) pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="c0d23-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="c0d23-109">Bien que cet article contienne des procédures pas à pas d’exemple de code s’exécutant sur la plateforme Windows, le code décrit dans cet article est identique sur l’ensemble des plateformes prises en charge.</span><span class="sxs-lookup"><span data-stu-id="c0d23-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="c0d23-110">Cet article, vous initie à l’architecture du kit de développement logiciel (SDK) d’appareil Azure IoT pour C. Il montre comment initialiser la bibliothèque de périphériques, envoyer des données à IoT Hub et recevoir des messages de sa part.</span><span class="sxs-lookup"><span data-stu-id="c0d23-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="c0d23-111">Les informations de cet article sont suffisantes pour commencer à utiliser le Kit de développement logiciel (SDK), mais elles vous fournissent également des indications qui vous permettront d’obtenir des informations supplémentaires sur les bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="c0d23-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="c0d23-112">Architecture du kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="c0d23-112">SDK architecture</span></span>

<span data-ttu-id="c0d23-113">Vous trouverez [**Azure IoT device SDK pour C**](https://github.com/Azure/azure-iot-sdk-c) dans le référentiel GitHub. Vous pouvez consulter les détails de l’[API dans Référence de l’API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="c0d23-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="c0d23-114">Vous trouverez la dernière version des bibliothèques dans la branche **maître** du référentiel :</span><span class="sxs-lookup"><span data-stu-id="c0d23-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="c0d23-115">L’implémentation de base du Kit de développement logiciel (SDK) se trouve dans le dossier **iothub\_client** qui contient l’implémentation de la couche d’API la plus basse du Kit de développement logiciel (SDK) : la bibliothèque **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="c0d23-116">La bibliothèque **IoTHubClient** contient des API implémentant des messages bruts permettant d’envoyer des messages à IoT Hub et de recevoir des messages de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="c0d23-117">Lorsque vous utilisez cette bibliothèque, vous êtes responsable de la mise en œuvre de la sérialisation du message, mais d’autres détails concernant la communication avec IoT Hub sont gérés pour vous.</span><span class="sxs-lookup"><span data-stu-id="c0d23-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="c0d23-118">Le dossier **serializer** contient des fonctions d’assistance et des exemples qui vous montrent comment sérialiser des données avant d’effectuer un envoi à Azure IoT Hub à l’aide de la bibliothèque cliente.</span><span class="sxs-lookup"><span data-stu-id="c0d23-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="c0d23-119">L’utilisation du sérialiseur n’est pas obligatoire et est fournie à titre de commodité.</span><span class="sxs-lookup"><span data-stu-id="c0d23-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="c0d23-120">Pour utiliser la bibliothèque **serializer**, vous définissez un modèle désignant les données que vous souhaitez envoyer à IoT Hub, et les messages que vous attendez de sa part.</span><span class="sxs-lookup"><span data-stu-id="c0d23-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="c0d23-121">Une fois le modèle défini, le Kit de développement logiciel (SDK) vous fournit une surface d’API qui vous permet de travailler facilement avec des messages Appareil vers cloud et Cloud vers appareil, sans se soucier des détails de sérialisation.</span><span class="sxs-lookup"><span data-stu-id="c0d23-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="c0d23-122">La bibliothèque dépend d’autres bibliothèques open source qui implémentent le transport à l’aide de protocoles tels que MQTT et AMQP.</span><span class="sxs-lookup"><span data-stu-id="c0d23-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="c0d23-123">La bibliothèque **IoTHubClient** dépend d’autres bibliothèques open source :</span><span class="sxs-lookup"><span data-stu-id="c0d23-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="c0d23-124">La bibliothèque de [l’utilitaire partagé Azure C](https://github.com/Azure/azure-c-shared-utility), qui fournit des fonctionnalités communes pour les tâches de base (comme la manipulation de chaînes ou de listes et les E/S) nécessaires dans plusieurs Kits de développement logiciel (SDK) C liés à Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d23-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="c0d23-125">La bibliothèque [Azure uAMQP](https://github.com/Azure/azure-uamqp-c), qui est une implémentation côté client du protocole AMQP optimisée pour les appareils avec contraintes de ressources.</span><span class="sxs-lookup"><span data-stu-id="c0d23-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="c0d23-126">La bibliothèque [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) , qui est une bibliothèque à usage général implémentant le protocole MQTT et optimisée pour les appareils avec contraintes de ressources.</span><span class="sxs-lookup"><span data-stu-id="c0d23-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="c0d23-127">L’exemple de code permet de mieux comprendre l’utilisation de ces bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="c0d23-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="c0d23-128">Les sections suivantes vous guident à travers plusieurs exemples d’applications inclus dans le kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="c0d23-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="c0d23-129">Cette procédure pas à pas devrait vous donner une idée des différentes fonctionnalités des couches architecturales du kit de développement logiciel (SDK) et vous initier au fonctionnement de l’API.</span><span class="sxs-lookup"><span data-stu-id="c0d23-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="c0d23-130">Avant d’exécuter les exemples</span><span class="sxs-lookup"><span data-stu-id="c0d23-130">Before you run the samples</span></span>

<span data-ttu-id="c0d23-131">Avant de pouvoir exécuter les exemples du Kit de développement logiciel (SDK) d’appareil Azure IoT pour C, vous devez [créer une instance du service IoT Hub](iot-hub-create-through-portal.md) dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d23-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="c0d23-132">Effectuez ensuite les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="c0d23-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="c0d23-133">Préparer votre environnement de développement</span><span class="sxs-lookup"><span data-stu-id="c0d23-133">Prepare your development environment</span></span>
* <span data-ttu-id="c0d23-134">Obtenir les informations d’identification de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c0d23-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="c0d23-135">Préparer votre environnement de développement</span><span class="sxs-lookup"><span data-stu-id="c0d23-135">Prepare your development environment</span></span>

<span data-ttu-id="c0d23-136">Les packages sont fournis pour les plates-formes courantes (telles que NuGet pour Windows ou apt_get pour Debian et Ubuntu) et les exemples utilisent ces packages lorsqu’ils sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="c0d23-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="c0d23-137">Dans certains cas, vous devez compiler le Kit de développement logiciel (SDK) pour ou sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="c0d23-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="c0d23-138">Si vous avez besoin compiler le Kit de développement logiciel (SDK), consultez [Préparer votre environnement de développement](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) dans le référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="c0d23-139">Pour obtenir l’exemple de code d’application, téléchargez une copie du Kit de développement logiciel (SDK) à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="c0d23-140">Obtenez votre copie de la source à partir de la branche **maître** du [référentiel GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="c0d23-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="c0d23-141">Obtenir les informations d’identification de l’appareil</span><span class="sxs-lookup"><span data-stu-id="c0d23-141">Obtain the device credentials</span></span>

<span data-ttu-id="c0d23-142">Maintenant que vous avez l’exemple de code source, vous devez à présent obtenir un ensemble d’informations d’identification d’appareils.</span><span class="sxs-lookup"><span data-stu-id="c0d23-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="c0d23-143">Pour qu’un appareil puisse accéder à un IoT Hub, vous devez d’abord ajouter l’appareil au registre des identifiés de l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="c0d23-144">Lorsque vous ajoutez votre périphérique, vous obtenez un jeu d’informations d’identification dont vous avez besoin pour permettre au périphérique de se connecter au IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="c0d23-145">Les exemples d’application qui figurent dans la section qui suit attendent ces informations d’identification sous la forme de **chaîne de connexion d’appareil**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="c0d23-146">Il existe plusieurs outils open source pour vous aider à gérer votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="c0d23-147">Une application Windows appelée [Explorateur d’appareils](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="c0d23-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="c0d23-148">Un outil d’interface de ligne de commande (CLI) multiplateforme node.js appelé [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="c0d23-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="c0d23-149">Ce didacticiel utilise l’outil graphique *Explorateur d’appareils*.</span><span class="sxs-lookup"><span data-stu-id="c0d23-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="c0d23-150">Vous pouvez également utiliser l’outil *iothub-explorer* si vous préférez utiliser un outil d’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="c0d23-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="c0d23-151">L’outil Explorateur d’appareils utilise les bibliothèques de service Azure IoT pour effectuer diverses fonctions sur IoT Hub, notamment ajouter des appareils.</span><span class="sxs-lookup"><span data-stu-id="c0d23-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="c0d23-152">Si vous utilisez l'outil Explorateur d'appareils pour ajouter un appareil, vous obtenez une chaîne de connexion pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="c0d23-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="c0d23-153">Vous avez besoin de cette chaîne de connexion pour exécuter les exemples d'applications.</span><span class="sxs-lookup"><span data-stu-id="c0d23-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="c0d23-154">Si vous n’êtes pas familiarisé avec l’outil Explorateur d’appareils, la procédure qui suit explique comment l’utiliser pour ajouter un périphérique et obtenir une chaîne de connexion d’appareil.</span><span class="sxs-lookup"><span data-stu-id="c0d23-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="c0d23-155">Pour installer l’outil Explorateur d’appareils, consultez [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) (comment utiliser l’Explorateur d’appareils pour les appareils IoT Hub).</span><span class="sxs-lookup"><span data-stu-id="c0d23-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="c0d23-156">Lorsque vous exécutez le programme, vous voyez cette interface :</span><span class="sxs-lookup"><span data-stu-id="c0d23-156">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="c0d23-157">Entrez votre **chaîne de connexion IoT Hub** dans le premier champ, puis cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="c0d23-158">Cette étape sert à configurer l’outil pour lui permettre de communiquer avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="c0d23-159">Lorsque la chaîne de connexion IoT Hub est configurée, cliquez sur l’onglet **Gestion** :</span><span class="sxs-lookup"><span data-stu-id="c0d23-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="c0d23-160">C’est depuis cet onglet que vous gérez les appareils inscrits dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="c0d23-161">Vous créez un périphérique en cliquant sur le bouton **Créer** .</span><span class="sxs-lookup"><span data-stu-id="c0d23-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="c0d23-162">Une boîte de dialogue avec un jeu de clés (primaire et secondaire) préalablement remplies s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c0d23-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="c0d23-163">Entrez un **ID d’appareil**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="c0d23-164">Lorsque l’appareil est créé, la liste des appareils s’actualise avec tous les appareils inscrits, dont celui que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="c0d23-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="c0d23-165">Si vous cliquez avec le bouton droit sur le nouvel appareil, le menu qui suit s’affiche :</span><span class="sxs-lookup"><span data-stu-id="c0d23-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="c0d23-166">Si vous choisissez **Copier la chaîne de connexion de l’appareil sélectionné**, la chaîne de connexion en question est copiée dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="c0d23-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="c0d23-167">Conservez une copie de la chaîne de connexion de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c0d23-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="c0d23-168">Vous en avez besoin au moment d’exécuter les exemples d’application décrits dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="c0d23-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="c0d23-169">Lorsque vous avez effectué les opérations ci-dessus, vous êtes prêt à commencer l’exécution du code.</span><span class="sxs-lookup"><span data-stu-id="c0d23-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="c0d23-170">En haut du fichier source principal, les deux exemples décrits ci-dessous contiennent une constante qui permet d’entrer une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="c0d23-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="c0d23-171">Par exemple, la ligne correspondante de l’application **iothub\_client\_sample\_mqtt** se présente comme suit.</span><span class="sxs-lookup"><span data-stu-id="c0d23-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="c0d23-172">Utiliser la bibliothèque IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="c0d23-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="c0d23-173">Dans le dossier **iothub\_client** du référentiel [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) se trouve un dossier **samples** contenant une application appelée **iothub\_client\_sample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="c0d23-174">La version Windows de l’application **iothub\_client\_sample\_mqtt** contient la solution Visual Studio suivante :</span><span class="sxs-lookup"><span data-stu-id="c0d23-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="c0d23-175">Si vous ouvrez ce projet dans Visual Studio 2017, acceptez les invites pour recibler le projet vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="c0d23-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="c0d23-176">Cette solution inclut un seul projet :</span><span class="sxs-lookup"><span data-stu-id="c0d23-176">This solution contains a single project.</span></span> <span data-ttu-id="c0d23-177">Cette solution installe quatre packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="c0d23-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="c0d23-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="c0d23-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="c0d23-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="c0d23-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="c0d23-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="c0d23-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="c0d23-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="c0d23-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="c0d23-182">Quand vous travaillez avec le Kit de développement logiciel (SDK), vous devez toujours utiliser le package **Microsoft.Azure.C.SharedUtility** .</span><span class="sxs-lookup"><span data-stu-id="c0d23-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="c0d23-183">Cet exemple utilise le protocole MQTT, par conséquent vous devez inclure les packages **Microsoft.Azure.umqtt** et **Microsoft.Azure.IoTHub.MqttTransport** (il existe des packages équivalents pour AMQP et HTTP).</span><span class="sxs-lookup"><span data-stu-id="c0d23-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="c0d23-184">Comme l’exemple utilise la bibliothèque **IoTHubClient**, vous devez également inclure le package **Microsoft.Azure.IoTHub.IoTHubClient** dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="c0d23-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="c0d23-185">L’implémentation de l’exemple d’application est disponible dans le fichier source **iothub\_client\_sample\_mqtt.c**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="c0d23-186">Les étapes suivantes utilisent cet exemple d’application pour vous montrer les éléments requis pour utiliser la bibliothèque **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="c0d23-187">Initialiser la bibliothèque</span><span class="sxs-lookup"><span data-stu-id="c0d23-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="c0d23-188">Avant d’utiliser les bibliothèques, vous devrez peut-être procéder à une initialisation spécifique à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="c0d23-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="c0d23-189">Par exemple, si vous prévoyez d’utiliser AMQP sur Linux, vous devez initialiser la bibliothèque OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="c0d23-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="c0d23-190">Les exemples du [référentiel GitHub](https://github.com/Azure/azure-iot-sdk-c) appellent la fonction de l’utilitaire **platform\_init** quand le client démarre et appelle la fonction **platform\_deinit** avant de se fermer.</span><span class="sxs-lookup"><span data-stu-id="c0d23-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="c0d23-191">Ces fonctions sont déclarées dans le fichier d’en-tête platform.h.</span><span class="sxs-lookup"><span data-stu-id="c0d23-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="c0d23-192">Examinez les définitions de ces fonctions pour votre plateforme cible dans le [référentiel](https://github.com/Azure/azure-iot-sdk-c) pour déterminer si vous devez inclure du code d’initialisation spécifique à la plateforme dans votre client.</span><span class="sxs-lookup"><span data-stu-id="c0d23-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="c0d23-193">Pour commencer à travailler avec les bibliothèques, attribuez d’abord un pointeur client IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="c0d23-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="c0d23-194">Transférez une copie de la chaîne de connexion d’appareil (obtenue dans l’outil Explorateur d’appareils) vers cette fonction.</span><span class="sxs-lookup"><span data-stu-id="c0d23-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="c0d23-195">Vous désignez également le protocole de communication à utiliser.</span><span class="sxs-lookup"><span data-stu-id="c0d23-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="c0d23-196">Cet exemple utilise MQTT, mais AMQP et HTTP sont également possibles.</span><span class="sxs-lookup"><span data-stu-id="c0d23-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="c0d23-197">Lorsque vous disposez d’un pointeur **IOTHUB\_CLIENT\_HANDLE** valide, vous pouvez commencer à appeler des API pour envoyer des messages vers IoT Hub et en recevoir de sa part.</span><span class="sxs-lookup"><span data-stu-id="c0d23-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="c0d23-198">Envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="c0d23-198">Send messages</span></span>

<span data-ttu-id="c0d23-199">L’exemple d’application configure une boucle pour envoyer des messages à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="c0d23-200">L'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="c0d23-200">The following snippet:</span></span>

- <span data-ttu-id="c0d23-201">Crée un message.</span><span class="sxs-lookup"><span data-stu-id="c0d23-201">Creates a message.</span></span>
- <span data-ttu-id="c0d23-202">Ajoute une propriété au message.</span><span class="sxs-lookup"><span data-stu-id="c0d23-202">Adds a property to the message.</span></span>
- <span data-ttu-id="c0d23-203">Envoie un message.</span><span class="sxs-lookup"><span data-stu-id="c0d23-203">Sends a message.</span></span>

<span data-ttu-id="c0d23-204">Tout d’abord, créez un message :</span><span class="sxs-lookup"><span data-stu-id="c0d23-204">First, create a message:</span></span>

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
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="c0d23-205">À chaque fois que vous envoyez un message, vous spécifiez une référence à une fonction de rappel invoquée lors de l’envoi des données.</span><span class="sxs-lookup"><span data-stu-id="c0d23-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="c0d23-206">Dans cet exemple, la fonction de rappel est appelée **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="c0d23-207">L’extrait de code suivant illustre cette fonction de rappel :</span><span class="sxs-lookup"><span data-stu-id="c0d23-207">The following snippet shows this callback function:</span></span>

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

<span data-ttu-id="c0d23-208">Notez l’appel de la fonction **IoTHubMessage\_Destroy** quand vous en avez terminé avec le message.</span><span class="sxs-lookup"><span data-stu-id="c0d23-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="c0d23-209">Cette fonction libère les ressources affectées au moment de la création du message.</span><span class="sxs-lookup"><span data-stu-id="c0d23-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="c0d23-210">Recevoir des messages</span><span class="sxs-lookup"><span data-stu-id="c0d23-210">Receive messages</span></span>

<span data-ttu-id="c0d23-211">La réception d’un message est une opération asynchrone.</span><span class="sxs-lookup"><span data-stu-id="c0d23-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="c0d23-212">Tout d’abord, vous enregistrez le rappel à appeler lorsque le périphérique reçoit un message :</span><span class="sxs-lookup"><span data-stu-id="c0d23-212">First, you register the callback to invoke when the device receives a message:</span></span>

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

<span data-ttu-id="c0d23-213">Le dernier paramètre est un pointeur vide vers ce que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="c0d23-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="c0d23-214">Dans l’exemple, il s’agit d’un pointeur vers un entier, mais il peut s’agir d’un pointeur vers une structure de données plus complexe.</span><span class="sxs-lookup"><span data-stu-id="c0d23-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="c0d23-215">Ce paramètre permet à la fonction de rappel de fonctionner sur l’état partagé avec l’appelant de cette fonction.</span><span class="sxs-lookup"><span data-stu-id="c0d23-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="c0d23-216">Lorsque le périphérique reçoit un message, la fonction de rappel enregistrée est appelée.</span><span class="sxs-lookup"><span data-stu-id="c0d23-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="c0d23-217">Cette fonction de rappel récupère :</span><span class="sxs-lookup"><span data-stu-id="c0d23-217">This callback function retrieves:</span></span>

* <span data-ttu-id="c0d23-218">L’ID de message et l’ID de corrélation du message.</span><span class="sxs-lookup"><span data-stu-id="c0d23-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="c0d23-219">Le contenu du message.</span><span class="sxs-lookup"><span data-stu-id="c0d23-219">The message content.</span></span>
* <span data-ttu-id="c0d23-220">Toutes les propriétés personnalisées du message.</span><span class="sxs-lookup"><span data-stu-id="c0d23-220">Any custom properties from the message.</span></span>

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
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
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

<span data-ttu-id="c0d23-221">Utilisez la fonction **IoTHubMessage\_GetByteArray** pour récupérer le message, qui, dans cet exemple, est une chaîne.</span><span class="sxs-lookup"><span data-stu-id="c0d23-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="c0d23-222">Désinitialiser la bibliothèque</span><span class="sxs-lookup"><span data-stu-id="c0d23-222">Uninitialize the library</span></span>

<span data-ttu-id="c0d23-223">Quand vous avez terminé d’envoyer des événements et de recevoir des messages, vous pouvez annuler l’initialisation de la bibliothèque IoT.</span><span class="sxs-lookup"><span data-stu-id="c0d23-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="c0d23-224">Pour ce faire, lancez l'appel de fonction suivant :</span><span class="sxs-lookup"><span data-stu-id="c0d23-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="c0d23-225">Cet appel permet de libérer les ressources allouées précédemment par la fonction **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="c0d23-226">Comme vous pouvez le voir, il est facile d’envoyer et de recevoir des messages avec la bibliothèque **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="c0d23-227">La bibliothèque traite les détails de la communication avec IoT Hub, notamment le protocole à utiliser (du point de vue du développeur, il s’agit d’une option de configuration simple).</span><span class="sxs-lookup"><span data-stu-id="c0d23-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="c0d23-228">La bibliothèque **IoTHubClient** offre également un contrôle précis de la manière de sérialiser les données que votre appareil envoie à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="c0d23-229">Dans certains cas, ce niveau de contrôle est un avantage, mais dans d’autres cas, il s’agit d’un détail d’implémentation qui ne vous concerne pas.</span><span class="sxs-lookup"><span data-stu-id="c0d23-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="c0d23-230">Si tel est le cas, vous pouvez envisager d’utiliser la bibliothèque **serializer**, qui est décrite dans la prochaine section.</span><span class="sxs-lookup"><span data-stu-id="c0d23-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="c0d23-231">Utiliser la bibliothèque du sérialiseur</span><span class="sxs-lookup"><span data-stu-id="c0d23-231">Use the serializer library</span></span>

<span data-ttu-id="c0d23-232">Sur le plan conceptuel, la bibliothèque **serializer** se trouve au-dessus de la bibliothèque **IoTHubClient** dans le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="c0d23-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="c0d23-233">Elle utilise la bibliothèque **IoTHubClient** pour la communication sous-jacente avec IoT Hub, mais ajoute des fonctions de modélisation qui soulagent le développeur de la charge que représente le traitement de la sérialisation de message.</span><span class="sxs-lookup"><span data-stu-id="c0d23-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="c0d23-234">Le fonctionnement de la bibliothèque est mieux illustré par un exemple.</span><span class="sxs-lookup"><span data-stu-id="c0d23-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="c0d23-235">Dans le dossier **serializer** du référentiel [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) se trouve un dossier **samples** (exemples) contenant une application appelée **simplesample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="c0d23-236">La version Windows de cet exemple inclut la solution Visual Studio suivante :</span><span class="sxs-lookup"><span data-stu-id="c0d23-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="c0d23-237">Si vous ouvrez ce projet dans Visual Studio 2017, acceptez les invites pour recibler le projet vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="c0d23-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="c0d23-238">Comme l’exemple précédent, celui-ci contient plusieurs packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="c0d23-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="c0d23-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="c0d23-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="c0d23-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="c0d23-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="c0d23-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="c0d23-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="c0d23-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="c0d23-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="c0d23-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="c0d23-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="c0d23-244">Vous avez vu la plupart de ces packages dans l’exemple précédent, mais **Microsoft.Azure.IoTHub.Serializer** est nouveau.</span><span class="sxs-lookup"><span data-stu-id="c0d23-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="c0d23-245">Ce package est obligatoire lorsque vous utilisez la bibliothèque **serializer**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="c0d23-246">L’implémentation de l’exemple d’application est disponible dans le fichier **simplesample\_mqtt.c**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="c0d23-247">Les sections suivantes vous guident à travers les éléments clés de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="c0d23-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="c0d23-248">Initialiser la bibliothèque</span><span class="sxs-lookup"><span data-stu-id="c0d23-248">Initialize the library</span></span>

<span data-ttu-id="c0d23-249">Pour commencer à travailler avec la bibliothèque **serializer**, appelez les API d’initialisation :</span><span class="sxs-lookup"><span data-stu-id="c0d23-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

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

<span data-ttu-id="c0d23-250">L’appel à la fonction **serializer\_init** est un appel unique qui initialise la bibliothèque sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="c0d23-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="c0d23-251">Vous pouvez ensuite appeler la fonction **IoTHubClient\_LL\_CreateFromConnectionString**, qui est la même API que celle de l’exemple **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="c0d23-252">Cet appel définit la chaîne de connexion de l’appareil (c’est également avec cet appel que vous choisissez le protocole à utiliser).</span><span class="sxs-lookup"><span data-stu-id="c0d23-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="c0d23-253">Cet exemple utilise MQTT comme protocole de transport, mais pourrait utiliser AMQP ou HTTP.</span><span class="sxs-lookup"><span data-stu-id="c0d23-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="c0d23-254">Enfin, appelez la fonction **CREATE\_MODEL\_INSTANCE**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="c0d23-255">**WeatherStation** est l’espace de noms du modèle et **ContosoAnemometer**, celui du modèle lui-même.</span><span class="sxs-lookup"><span data-stu-id="c0d23-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="c0d23-256">Une fois que l’instance de modèle est créée, vous pouvez l’utiliser pour commencer à envoyer et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="c0d23-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="c0d23-257">Cependant, il est important de comprendre ce qu’est un modèle.</span><span class="sxs-lookup"><span data-stu-id="c0d23-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="c0d23-258">Définir le modèle</span><span class="sxs-lookup"><span data-stu-id="c0d23-258">Define the model</span></span>

<span data-ttu-id="c0d23-259">Un modèle de la bibliothèque **serializer** définit les messages que votre appareil peut envoyer à IoT Hub et les messages, appelés *actions* dans le langage de la modélisation, qu’il peut recevoir.</span><span class="sxs-lookup"><span data-stu-id="c0d23-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="c0d23-260">Un modèle se définit avec un ensemble de macros C comme dans l’exemple d’application **simplesample\_mqtt** :</span><span class="sxs-lookup"><span data-stu-id="c0d23-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="c0d23-261">Les macros **BEGIN\_NAMESPACE** et **END\_NAMESPACE** se servent toutes les deux de l’espace de noms du modèle comme argument.</span><span class="sxs-lookup"><span data-stu-id="c0d23-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="c0d23-262">En principe, tous les éléments compris entre ces deux macros sont la définition du ou des modèles et structures de données que les modèles utilisent.</span><span class="sxs-lookup"><span data-stu-id="c0d23-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="c0d23-263">Dans cet exemple, il existe un seul modèle appelé **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="c0d23-264">Ce modèle définit deux éléments de données que votre périphérique peut envoyer à IoT Hub : **DeviceId** et **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="c0d23-265">Il définit également trois actions (messages) que votre appareil peut recevoir : **TurnFanOn**, **TurnFanOff** et **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="c0d23-266">Chaque élément de données possède un type et chaque action a un nom (et éventuellement, un ensemble de paramètres).</span><span class="sxs-lookup"><span data-stu-id="c0d23-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="c0d23-267">Les données et les actions définis dans le modèle définissent une surface API que vous pouvez utiliser pour envoyer des messages à IoT Hub et répondre aux messages envoyés à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c0d23-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="c0d23-268">Un exemple permet de mieux comprendre l’utilisation de ce modèle.</span><span class="sxs-lookup"><span data-stu-id="c0d23-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="c0d23-269">Envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="c0d23-269">Send messages</span></span>

<span data-ttu-id="c0d23-270">Ce modèle définit les données que vous pouvez envoyer à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="c0d23-271">Dans cet exemple, cela correspond à l’un des deux éléments de données définis à l’aide de la macro **WITH_DATA**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="c0d23-272">Plusieurs étapes sont nécessaires pour envoyer les valeurs **DeviceId** et **WindSpeed** à un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c0d23-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="c0d23-273">La première consiste à définir les données que vous souhaitez envoyer :</span><span class="sxs-lookup"><span data-stu-id="c0d23-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="c0d23-274">Le modèle que vous avez défini précédemment vous permet de définir les valeurs en définissant des membres d’un **struct**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="c0d23-275">Ensuite, sérialisez le message que vous voulez envoyer :</span><span class="sxs-lookup"><span data-stu-id="c0d23-275">Next, serialize the message you want to send:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="c0d23-276">Ce code sérialise l’appareil-à-cloud vers une mémoire tampon (référencée par **destination**).</span><span class="sxs-lookup"><span data-stu-id="c0d23-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="c0d23-277">Le code appelle ensuite la fonction **sendMessage** pour envoyer le message à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="c0d23-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="c0d23-278">L’avant-dernier paramètre de **IoTHubClient\_LL\_SendEventAsync** est une référence à une fonction de rappel appelée lorsque l’envoi des données a abouti.</span><span class="sxs-lookup"><span data-stu-id="c0d23-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="c0d23-279">Voici la fonction de rappel dans l’exemple :</span><span class="sxs-lookup"><span data-stu-id="c0d23-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="c0d23-280">Le deuxième paramètre est un pointeur vers le contexte utilisateur, le même pointeur a été transmis à **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="c0d23-281">Dans ce cas, le contexte est un simple compteur, mais il peut s’agir de tout élément que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="c0d23-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="c0d23-282">C’est tout ce qu’il y a à savoir concernant l’envoi de messages d’appareil vers cloud.</span><span class="sxs-lookup"><span data-stu-id="c0d23-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="c0d23-283">Le seul sujet qu’il nous reste à aborder est le mode de réception des messages.</span><span class="sxs-lookup"><span data-stu-id="c0d23-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="c0d23-284">Recevoir des messages</span><span class="sxs-lookup"><span data-stu-id="c0d23-284">Receive messages</span></span>

<span data-ttu-id="c0d23-285">La réception d’un message fonctionne de la même façon que les messages de la bibliothèque **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="c0d23-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="c0d23-286">Tout d’abord, vous enregistrez une fonction de rappel de message :</span><span class="sxs-lookup"><span data-stu-id="c0d23-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="c0d23-287">Vous écrivez ensuite la fonction de rappel invoquée à la réception d’un message :</span><span class="sxs-lookup"><span data-stu-id="c0d23-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="c0d23-288">Ce code est réutilisable. Le code est le même quelle que soit la solution.</span><span class="sxs-lookup"><span data-stu-id="c0d23-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="c0d23-289">Cette fonction reçoit le message et prend en charge son acheminement vers la fonction appropriée via l’appel **d’EXECUTE\_COMMAND**.</span><span class="sxs-lookup"><span data-stu-id="c0d23-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="c0d23-290">La fonction appelée à ce stade dépend de la définition des actions dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="c0d23-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="c0d23-291">Quand vous définissez une action dans votre modèle, vous devez mettre en œuvre une fonction qui est appelée au moment où l’appareil reçoit le message correspondant.</span><span class="sxs-lookup"><span data-stu-id="c0d23-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="c0d23-292">Par exemple, si votre modèle définit cette action :</span><span class="sxs-lookup"><span data-stu-id="c0d23-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="c0d23-293">Définissez une fonction avec cette signature :</span><span class="sxs-lookup"><span data-stu-id="c0d23-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="c0d23-294">Notez que le nom de la fonction correspond au nom de l’action dans le modèle et que les paramètres de la fonction correspondent aux paramètres spécifiés pour l’action.</span><span class="sxs-lookup"><span data-stu-id="c0d23-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="c0d23-295">Le premier paramètre est toujours requis et contient un pointeur vers l’instance de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="c0d23-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="c0d23-296">Lorsque le périphérique reçoit un message qui correspond à cette signature, la fonction associée est appelée.</span><span class="sxs-lookup"><span data-stu-id="c0d23-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="c0d23-297">Ainsi, hormis l’inclusion du code réutilisable d’ **IoTHubMessage**, recevoir des messages revient à définir une fonction simple pour chaque action définie dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="c0d23-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="c0d23-298">Désinitialiser la bibliothèque</span><span class="sxs-lookup"><span data-stu-id="c0d23-298">Uninitialize the library</span></span>

<span data-ttu-id="c0d23-299">Lorsque vous avez terminé d’envoyer les données et de recevoir des messages, vous pouvez annuler l’initialisation de la bibliothèque IoT :</span><span class="sxs-lookup"><span data-stu-id="c0d23-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="c0d23-300">Chacune de ces trois fonctions s’aligne sur les trois fonctions d’initialisation décrites précédemment.</span><span class="sxs-lookup"><span data-stu-id="c0d23-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="c0d23-301">L’appel de ces API vous permet de libérer les ressources affectées au préalable.</span><span class="sxs-lookup"><span data-stu-id="c0d23-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0d23-302">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0d23-302">Next Steps</span></span>

<span data-ttu-id="c0d23-303">Cet article a abordé les principes de base de l’utilisation des bibliothèques dans le **Kit de développement logiciel (SDK) d’appareil Azure IoT (Azure IoT device SDK) pour C**. Il vous a fourni suffisamment d’informations pour comprendre ce qui est inclus dans le Kit de développement logiciel (SDK), son architecture et la manière d’utiliser les exemples Windows.</span><span class="sxs-lookup"><span data-stu-id="c0d23-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="c0d23-304">Le prochain article poursuit la description du kit de développement logiciel en approfondissant les explications relatives à [la bibliothèque IoTHubClient](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="c0d23-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="c0d23-305">Pour en savoir plus sur le développement pour IoT Hub, voir les [Kits de développement logiciel (SDK) Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="c0d23-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="c0d23-306">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="c0d23-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c0d23-307">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="c0d23-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
