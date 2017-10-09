---
title: aaaOverview Azure IoT bord | Documents Microsoft
description: "Décrit hello concepts architecturaux clés dans Azure IoT Edge tels que les passerelles, les modules et les services Broker."
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
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="dcff0-103">Concepts architecturaux d’Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="dcff0-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="dcff0-104">Avant de consulter des exemples de code ou créer votre propre passerelle de champ à l’aide de IoT Edge, vous devez comprendre hello principaux concepts qui sous-tendent l’architecture hello du bord de IoT.</span><span class="sxs-lookup"><span data-stu-id="dcff0-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand hello key concepts that underpin hello architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="dcff0-105">Modules IoT Edge</span><span class="sxs-lookup"><span data-stu-id="dcff0-105">IoT Edge modules</span></span>

<span data-ttu-id="dcff0-106">Vous créez une passerelle avec Azure IoT Edge en créant et en assemblant des *modules IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="dcff0-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="dcff0-107">Utilisent des modules *messages* tooexchange des données entre eux.</span><span class="sxs-lookup"><span data-stu-id="dcff0-107">Modules use *messages* tooexchange data with each other.</span></span> <span data-ttu-id="dcff0-108">Un module reçoit un message, effectue une action sur celui-ci, éventuellement transforme un nouveau message et le publie ensuite pour les autres tooprocess modules.</span><span class="sxs-lookup"><span data-stu-id="dcff0-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules tooprocess.</span></span> <span data-ttu-id="dcff0-109">Certains modules peuvent uniquement produire de nouveaux messages et ne jamais traiter les messages entrants.</span><span class="sxs-lookup"><span data-stu-id="dcff0-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="dcff0-110">Une chaîne de modules crée un pipeline de traitement des données avec chaque module effectuant une transformation sur des données à un moment donné de ce pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="dcff0-110">A chain of modules creates a data processing pipeline with each module performing a transformation on hello data at one point in that pipeline.</span></span>

![Chaîne de modules dans la passerelle créée avec Azure IoT Edge][1]

<span data-ttu-id="dcff0-112">IoT bord contient hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="dcff0-112">IoT Edge contains hello following components:</span></span>

* <span data-ttu-id="dcff0-113">Des modules pré-écrits qui exécutent des fonctions de passerelles courantes.</span><span class="sxs-lookup"><span data-stu-id="dcff0-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="dcff0-114">interfaces Hello un développeur peuvent utiliser toowrite des modules personnalisés.</span><span class="sxs-lookup"><span data-stu-id="dcff0-114">hello interfaces a developer can use toowrite custom modules.</span></span>
* <span data-ttu-id="dcff0-115">Hello toodeploy nécessaire d’infrastructure et d’exécuter un ensemble de modules.</span><span class="sxs-lookup"><span data-stu-id="dcff0-115">hello infrastructure necessary toodeploy and run a set of modules.</span></span>

<span data-ttu-id="dcff0-116">Hello SDK fournit une couche d’abstraction qui vous permet de toobuild passerelles toorun sur différentes plateformes et les systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="dcff0-116">hello SDK provides an abstraction layer that enables you toobuild gateways toorun on various operating systems and platforms.</span></span>

![Couche d’abstraction Azure IoT Edge][2]

## <a name="messages"></a><span data-ttu-id="dcff0-118">Messages</span><span class="sxs-lookup"><span data-stu-id="dcff0-118">Messages</span></span>

<span data-ttu-id="dcff0-119">Bien que vous réfléchissez à passer de modules, messages tooeach autres est un moyen pratique de tooconceptualize fonctionnement d’une passerelle, il ne pas refléter correctement ce qui se passe.</span><span class="sxs-lookup"><span data-stu-id="dcff0-119">Although thinking about modules passing messages tooeach other is a convenient way tooconceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="dcff0-120">Les modules IoT bord utilisent un toocommunicate broker entre eux.</span><span class="sxs-lookup"><span data-stu-id="dcff0-120">IoT Edge modules use a broker toocommunicate with each other.</span></span> <span data-ttu-id="dcff0-121">Les modules publier broker toohello de messages (à l’aide de modèles de messagerie telles que les bus ou la publication/abonnement) et laisser ensuite hello broker itinéraire hello message toohello modules tooit connecté.</span><span class="sxs-lookup"><span data-stu-id="dcff0-121">Modules publish messages toohello broker (using messaging patterns such as bus, or publish/subscribe) and then let hello broker route hello message toohello modules connected tooit.</span></span>

<span data-ttu-id="dcff0-122">Un module utilise hello **Broker_Publish** toopublish toohello message broker de la fonction.</span><span class="sxs-lookup"><span data-stu-id="dcff0-122">A module uses hello **Broker_Publish** function toopublish a message toohello broker.</span></span> <span data-ttu-id="dcff0-123">service broker de Hello remet module tooa de messages en appelant une fonction de rappel.</span><span class="sxs-lookup"><span data-stu-id="dcff0-123">hello broker delivers messages tooa module by invoking a callback function.</span></span> <span data-ttu-id="dcff0-124">Un message se compose d'un ensemble de propriétés de clés/valeurs et d’un contenu transmis sous forme d’un bloc de mémoire.</span><span class="sxs-lookup"><span data-stu-id="dcff0-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![rôle Hello Hello Broker dans Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="dcff0-126">Routage et filtrage des messages</span><span class="sxs-lookup"><span data-stu-id="dcff0-126">Message routing and filtering</span></span>

<span data-ttu-id="dcff0-127">Il existe deux façons de modules de IoT bord corrects toodirect messages toohello :</span><span class="sxs-lookup"><span data-stu-id="dcff0-127">There are two ways toodirect messages toohello correct IoT Edge modules:</span></span>

* <span data-ttu-id="dcff0-128">Vous pouvez passer un ensemble de liens peuvent être passés toohello broker afin que service broker de hello sache source de hello et le récepteur pour chaque module.</span><span class="sxs-lookup"><span data-stu-id="dcff0-128">You can pass a set of links can be passed toohello broker so hello broker knows hello source and sink for each module.</span></span>
* <span data-ttu-id="dcff0-129">Un module peut filtrer sur les propriétés de hello de message de type hello.</span><span class="sxs-lookup"><span data-stu-id="dcff0-129">A module can filter on hello properties of hello message.</span></span>

<span data-ttu-id="dcff0-130">Un module doit agir uniquement un message si le message de type hello est destiné.</span><span class="sxs-lookup"><span data-stu-id="dcff0-130">A module should only act upon a message if hello message is intended for it.</span></span> <span data-ttu-id="dcff0-131">Les liens et le filtrage des messages permettent de créer efficacement un pipeline de messages.</span><span class="sxs-lookup"><span data-stu-id="dcff0-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcff0-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dcff0-132">Next steps</span></span>

<span data-ttu-id="dcff0-133">consultez de ces concepts appliqués dans un exemple, vous pouvez exécuter, toosee [architecture Explorer de Azure IoT Edge][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="dcff0-133">toosee these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md