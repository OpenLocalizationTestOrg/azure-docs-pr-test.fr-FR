---
title: "Vue d’ensemble d’Azure IoT Edge | Microsoft Docs"
description: "Décrit les concepts architecturaux clés dans Azure IoT Edge tels que les passerelles, les modules et les répartiteurs."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="b6bb4-103">Concepts architecturaux d’Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b6bb4-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="b6bb4-104">Avant d’examiner un exemple de code ou de créer votre propre passerelle de champ à l’aide d’IoT Edge, vous devez comprendre les concepts fondamentaux qui étayent l’architecture IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="b6bb4-105">Modules IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b6bb4-105">IoT Edge modules</span></span>

<span data-ttu-id="b6bb4-106">Vous créez une passerelle avec Azure IoT Edge en créant et en assemblant des *modules IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="b6bb4-107">Les modules s’échangent des données par le biais de *messages* .</span><span class="sxs-lookup"><span data-stu-id="b6bb4-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="b6bb4-108">Un module reçoit un message, exécute une action sur celui-ci, le transforme éventuellement en un nouveau message, puis le publie sur d'autres modules pour un traitement ultérieur.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="b6bb4-109">Certains modules peuvent uniquement produire de nouveaux messages et ne jamais traiter les messages entrants.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="b6bb4-110">Une chaîne de modules crée un pipeline de traitement des données dans lequel chaque module exécute une transformation de données en un point unique sur ce pipeline.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![Chaîne de modules dans la passerelle créée avec Azure IoT Edge][1]

<span data-ttu-id="b6bb4-112">IoT Edge est composé des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b6bb4-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="b6bb4-113">Des modules pré-écrits qui exécutent des fonctions de passerelles courantes.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="b6bb4-114">Les interfaces qu’un développeur peut utiliser pour écrire des modules personnalisés.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="b6bb4-115">L'infrastructure nécessaire pour déployer et exécuter un ensemble de modules.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="b6bb4-116">Le SDK fournit une couche d’abstraction qui vous permet de créer des passerelles qui s’exécutent sur différents systèmes d’exploitation et plateformes.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Couche d’abstraction Azure IoT Edge][2]

## <a name="messages"></a><span data-ttu-id="b6bb4-118">Messages</span><span class="sxs-lookup"><span data-stu-id="b6bb4-118">Messages</span></span>

<span data-ttu-id="b6bb4-119">L’approche consistant à utiliser des modules pour s’échanger des messages représente un moyen pratique de conceptualiser le fonctionnement d'une passerelle, mais elle ne reflète pas exactement ce qui se produit.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="b6bb4-120">Les modules IoT Edge utilisent un répartiteur pour communiquer entre eux.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="b6bb4-121">Les modules publient des messages sur le répartiteur (en utilisant des modèles de messagerie tels qu’un bus ou les options de publication et d’abonnement), puis laissent le répartiteur acheminer le message vers les modules connectés.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="b6bb4-122">Un module utilise la fonction **Broker_Publish** pour publier un message sur le répartiteur.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="b6bb4-123">Le répartiteur remet les messages à un module en appelant une fonction de rappel.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="b6bb4-124">Un message se compose d'un ensemble de propriétés de clés/valeurs et d’un contenu transmis sous forme d’un bloc de mémoire.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Rôle du répartiteur dans Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="b6bb4-126">Routage et filtrage des messages</span><span class="sxs-lookup"><span data-stu-id="b6bb4-126">Message routing and filtering</span></span>

<span data-ttu-id="b6bb4-127">Deux méthodes permettent d’acheminer des messages vers les modules IoT Edge adéquats :</span><span class="sxs-lookup"><span data-stu-id="b6bb4-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="b6bb4-128">Vous pouvez transmettre un ensemble de liens au répartiteur pour permettre à ce dernier de connaître la source et le récepteur de chaque module.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="b6bb4-129">Un module peut appliquer un filtre sur les propriétés du message.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="b6bb4-130">Un module doit agir sur un message uniquement si le message lui est destiné.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="b6bb4-131">Les liens et le filtrage des messages permettent de créer efficacement un pipeline de messages.</span><span class="sxs-lookup"><span data-stu-id="b6bb4-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6bb4-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6bb4-132">Next steps</span></span>

<span data-ttu-id="b6bb4-133">Pour voir l’application de ces concepts dans un exemple que vous pouvez exécuter, consultez [Explorer l’architecture Azure IoT Edge][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="b6bb4-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md