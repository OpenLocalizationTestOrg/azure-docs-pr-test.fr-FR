---
title: Prise en main des connexions hybrides Azure Relay dans .NET | Microsoft Docs
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
ms.openlocfilehash: 1af23bfd46dd7d3781505473f7c1d86e65ea9bc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="c5748-103">Prise en main des connexions hybrides Relay</span><span class="sxs-lookup"><span data-stu-id="c5748-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="c5748-104">Ce tutoriel présente les [connexions hybrides Azure Relay](relay-what-is-it.md#hybrid-connections) et explique comment utiliser .NET pour créer une application cliente qui envoie des messages à une application d’écouteur correspondante.</span><span class="sxs-lookup"><span data-stu-id="c5748-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use .NET to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="c5748-105">Les opérations que nous allons effectuer</span><span class="sxs-lookup"><span data-stu-id="c5748-105">What will be accomplished</span></span>
<span data-ttu-id="c5748-106">Étant donné que les connexions hybrides nécessitent un client et un serveur, le didacticiel crée deux applications de console.</span><span class="sxs-lookup"><span data-stu-id="c5748-106">Because Hybrid Connections requires both a client and a server component, the tutorial creates two console applications.</span></span> <span data-ttu-id="c5748-107">Voici la procédure à suivre :</span><span class="sxs-lookup"><span data-stu-id="c5748-107">Here are the steps:</span></span>

1. <span data-ttu-id="c5748-108">Créer un espace de noms Relay à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c5748-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="c5748-109">Créer une connexion hybride dans cet espace de noms, à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c5748-109">Create a hybrid connection in that namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="c5748-110">Écrire une application de console (écouteur) de serveur pour recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="c5748-110">Write a server (listener) console application to receive messages.</span></span>
4. <span data-ttu-id="c5748-111">Écrire une application de console (expéditeur) de client pour envoyer des messages.</span><span class="sxs-lookup"><span data-stu-id="c5748-111">Write a client (sender) console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5748-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c5748-112">Prerequisites</span></span>

<span data-ttu-id="c5748-113">Voici les prérequis pour effectuer ce tutoriel :</span><span class="sxs-lookup"><span data-stu-id="c5748-113">To complete this tutorial, you'll need the following prerequisites:</span></span>

1. <span data-ttu-id="c5748-114">[Visual Studio 2015 ou une version ultérieure](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="c5748-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="c5748-115">Les exemples de ce didacticiel utilisent Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c5748-115">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="c5748-116">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c5748-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="c5748-117">1. Créer un espace de noms à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="c5748-117">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="c5748-118">Si vous avez déjà créé un espace de noms Relay, passez à la section [Créer une connexion hybride à l’aide du portail Azure](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="c5748-118">If you have already created a Relay namespace, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="c5748-119">2. Créer une connexion hybride à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="c5748-119">2. Create a hybrid connection using the Azure portal</span></span>
<span data-ttu-id="c5748-120">Si vous avez déjà créé une connexion hybride, passez à la section [Créer une application de serveur](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="c5748-120">If you have already created a hybrid connection, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="c5748-121">3. Créer une application de serveur (récepteur)</span><span class="sxs-lookup"><span data-stu-id="c5748-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="c5748-122">Pour écouter et recevoir des messages à partir de Relay, nous allons écrire une application de console C# à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c5748-122">To listen and receive messages from the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="c5748-123">4. Créer une application cliente (expéditeur)</span><span class="sxs-lookup"><span data-stu-id="c5748-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="c5748-124">Pour envoyer des messages à Relay, nous allons écrire une application de console C# à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c5748-124">To send messages to the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="c5748-125">5. Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="c5748-125">5. Run the applications</span></span>
1. <span data-ttu-id="c5748-126">Exécutez l’application de serveur.</span><span class="sxs-lookup"><span data-stu-id="c5748-126">Run the server application.</span></span>
2. <span data-ttu-id="c5748-127">Exécutez l’application cliente et entrez du texte.</span><span class="sxs-lookup"><span data-stu-id="c5748-127">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="c5748-128">Vérifiez que la console d’application de serveur renvoie le texte entré dans l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="c5748-128">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="c5748-130">Félicitations, vous avez créé une application de connexions hybrides de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="c5748-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5748-131">Étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c5748-131">Next steps:</span></span>
* [<span data-ttu-id="c5748-132">FAQ Relay</span><span class="sxs-lookup"><span data-stu-id="c5748-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="c5748-133">Créer un espace de noms</span><span class="sxs-lookup"><span data-stu-id="c5748-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="c5748-134">Prise en main de Node</span><span class="sxs-lookup"><span data-stu-id="c5748-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

