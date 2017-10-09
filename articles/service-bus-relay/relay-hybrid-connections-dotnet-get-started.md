---
title: "aaaGet a démarré avec des connexions hybrides relais dans .NET | Documents Microsoft"
description: "Écrivez une application console C# pour les connexions hybrides Azure Relay."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="1759a-103">Prise en main des connexions hybrides Relay</span><span class="sxs-lookup"><span data-stu-id="1759a-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="1759a-104">Ce didacticiel fournit une introduction trop[connexions hybrides de relais Azure](relay-what-is-it.md#hybrid-connections)et montre comment toouse .NET toocreate une application cliente qui envoie les messages d’application écouteur tooa correspondant.</span><span class="sxs-lookup"><span data-stu-id="1759a-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="1759a-105">Les opérations que nous allons effectuer</span><span class="sxs-lookup"><span data-stu-id="1759a-105">What will be accomplished</span></span>
<span data-ttu-id="1759a-106">Étant donné que les connexions hybrides requiert un client et un composant serveur, didacticiel de hello crée deux applications console.</span><span class="sxs-lookup"><span data-stu-id="1759a-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="1759a-107">Voici les étapes hello :</span><span class="sxs-lookup"><span data-stu-id="1759a-107">Here are hello steps:</span></span>

1. <span data-ttu-id="1759a-108">Créer un espace de noms de relais, à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1759a-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="1759a-109">Dans cet espace de noms, à l’aide de hello portail Azure, créez une connexion hybride.</span><span class="sxs-lookup"><span data-stu-id="1759a-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="1759a-110">Écrire des messages tooreceive d’application une console de serveur (récepteur).</span><span class="sxs-lookup"><span data-stu-id="1759a-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="1759a-111">Écrire des messages d’application toosend une console client (expéditeur).</span><span class="sxs-lookup"><span data-stu-id="1759a-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1759a-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1759a-112">Prerequisites</span></span>

<span data-ttu-id="1759a-113">toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="1759a-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="1759a-114">[Visual Studio 2015 ou une version ultérieure](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="1759a-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="1759a-115">exemples de Hello dans ce didacticiel utilisent Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1759a-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="1759a-116">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1759a-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="1759a-117">1. Créer un espace de noms à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1759a-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="1759a-118">Si vous avez déjà créé un espace de noms de relais, raccourcis toohello [créer une connexion hybride à l’aide de hello portail Azure](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="1759a-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="1759a-119">2. Créez une connexion hybride à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1759a-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="1759a-120">Si vous avez déjà créé une connexion hybride, raccourcis toohello [créer une application serveur](#3-create-a-server-application-listener) section.</span><span class="sxs-lookup"><span data-stu-id="1759a-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="1759a-121">3. Créer une application de serveur (récepteur)</span><span class="sxs-lookup"><span data-stu-id="1759a-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="1759a-122">toolisten et recevoir des messages à partir de hello relais, nous écrirons une application console c# à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1759a-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="1759a-123">4. Créer une application cliente (expéditeur)</span><span class="sxs-lookup"><span data-stu-id="1759a-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="1759a-124">toohello de messages toosend de relais, nous écrirons une application console c# à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1759a-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="1759a-125">5. Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="1759a-125">5. Run hello applications</span></span>
1. <span data-ttu-id="1759a-126">Exécutez l’application de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="1759a-126">Run hello server application.</span></span>
2. <span data-ttu-id="1759a-127">Exécutez l’application cliente de hello et saisir du texte.</span><span class="sxs-lookup"><span data-stu-id="1759a-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="1759a-128">Vérifiez que serveur hello application console sorties hello texte qui a été entré dans l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="1759a-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="1759a-130">Félicitations, vous avez créé une application de connexions hybrides de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="1759a-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1759a-131">Étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1759a-131">Next steps:</span></span>
* [<span data-ttu-id="1759a-132">FAQ Relay</span><span class="sxs-lookup"><span data-stu-id="1759a-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="1759a-133">Créer un espace de noms</span><span class="sxs-lookup"><span data-stu-id="1759a-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="1759a-134">Prise en main de Node</span><span class="sxs-lookup"><span data-stu-id="1759a-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

