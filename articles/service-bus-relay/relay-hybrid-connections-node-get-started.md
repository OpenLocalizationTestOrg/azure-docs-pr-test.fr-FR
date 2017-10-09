---
title: "aaaGet a démarré avec des connexions hybrides relais dans le nœud | Documents Microsoft"
description: "Écrivez une application console Node.js pour les connexions hybrides Azure Relay."
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="43049-103">Prise en main des connexions hybrides Relay</span><span class="sxs-lookup"><span data-stu-id="43049-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="43049-104">Ce didacticiel fournit une introduction trop[connexions hybrides de relais Azure](relay-what-is-it.md#hybrid-connections)et montre comment toouse Node.js toocreate une application cliente qui envoie les messages d’application écouteur tooa correspondant.</span><span class="sxs-lookup"><span data-stu-id="43049-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="43049-105">Les opérations que nous allons effectuer</span><span class="sxs-lookup"><span data-stu-id="43049-105">What will be accomplished</span></span>

<span data-ttu-id="43049-106">Étant donné que les connexions hybrides nécessitent un client et un serveur, vous allez créer deux applications console dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="43049-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="43049-107">Voici les étapes hello :</span><span class="sxs-lookup"><span data-stu-id="43049-107">Here are hello steps:</span></span>

1. <span data-ttu-id="43049-108">Créer un espace de noms de relais, à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="43049-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="43049-109">Créer une connexion hybride, à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="43049-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="43049-110">Écrire des messages de console application tooreceive un serveur.</span><span class="sxs-lookup"><span data-stu-id="43049-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="43049-111">Écrire un client toosend les messages d’application console.</span><span class="sxs-lookup"><span data-stu-id="43049-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43049-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="43049-112">Prerequisites</span></span>

1. <span data-ttu-id="43049-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="43049-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="43049-114">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="43049-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="43049-115">1. Créer un espace de noms à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="43049-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="43049-116">Si vous disposez déjà d’un espace de noms de relais créé, passez toohello [créer une connexion hybride à l’aide de hello portail Azure](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="43049-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="43049-117">2. Créez une connexion hybride à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="43049-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="43049-118">Si vous avez déjà une connexion hybride créée, passez toohello [créer une application serveur](#3-create-a-server-application-listener) section.</span><span class="sxs-lookup"><span data-stu-id="43049-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="43049-119">3. Créer une application de serveur (récepteur)</span><span class="sxs-lookup"><span data-stu-id="43049-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="43049-120">toolisten et recevoir des messages à partir de hello relais, nous écrirons une application de console Node.js.</span><span class="sxs-lookup"><span data-stu-id="43049-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="43049-121">4. Créer une application cliente (expéditeur)</span><span class="sxs-lookup"><span data-stu-id="43049-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="43049-122">toosend messages toohello relais, nous écrirons une application de console Node.js.</span><span class="sxs-lookup"><span data-stu-id="43049-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="43049-123">5. Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="43049-123">5. Run hello applications</span></span>

1. <span data-ttu-id="43049-124">Exécutez l’application de serveur hello : à partir d’un type d’invite de commande Node.js `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="43049-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="43049-125">Exécutez l’application cliente de hello : à partir d’un type d’invite de commande Node.js `node sender.js`et entrez du texte.</span><span class="sxs-lookup"><span data-stu-id="43049-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="43049-126">Vérifiez que serveur hello application console sorties hello texte qui a été entré dans l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="43049-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="43049-128">Vous avez créé une application de connexions hybrides complète avec Node.js : félicitations !</span><span class="sxs-lookup"><span data-stu-id="43049-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="43049-129">Étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="43049-129">Next steps:</span></span>

* [<span data-ttu-id="43049-130">FAQ Relay</span><span class="sxs-lookup"><span data-stu-id="43049-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="43049-131">Créer un espace de noms</span><span class="sxs-lookup"><span data-stu-id="43049-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="43049-132">Prise en main de .NET</span><span class="sxs-lookup"><span data-stu-id="43049-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="43049-133">Prise en main de Node</span><span class="sxs-lookup"><span data-stu-id="43049-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

