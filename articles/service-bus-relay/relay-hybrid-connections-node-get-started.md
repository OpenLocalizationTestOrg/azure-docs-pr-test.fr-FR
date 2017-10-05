---
title: Prise en main des connexions hybrides Azure Relay dans Node | Microsoft Docs
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
ms.openlocfilehash: c3bfc45969f250059988129f532edd12dfe3dcfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="f2a4c-103">Prise en main des connexions hybrides Relay</span><span class="sxs-lookup"><span data-stu-id="f2a4c-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="f2a4c-104">Ce tutoriel présente les [connexions hybrides Azure Relay](relay-what-is-it.md#hybrid-connections) et explique comment utiliser Node.js pour créer une application cliente qui envoie des messages à une application d’écouteur correspondante.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use Node.js to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="f2a4c-105">Les opérations que nous allons effectuer</span><span class="sxs-lookup"><span data-stu-id="f2a4c-105">What will be accomplished</span></span>

<span data-ttu-id="f2a4c-106">Étant donné que les connexions hybrides nécessitent un client et un serveur, vous allez créer deux applications console dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="f2a4c-107">Voici la procédure à suivre :</span><span class="sxs-lookup"><span data-stu-id="f2a4c-107">Here are the steps:</span></span>

1. <span data-ttu-id="f2a4c-108">Créer un espace de noms Relay à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="f2a4c-109">Créer une connexion hybride, à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-109">Create a hybrid connection, using the Azure portal.</span></span>
3. <span data-ttu-id="f2a4c-110">Écrire une application de console de serveur pour recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-110">Write a server console application to receive messages.</span></span>
4. <span data-ttu-id="f2a4c-111">Écrire une application de console de client pour envoyer des messages.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-111">Write a client console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2a4c-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f2a4c-112">Prerequisites</span></span>

1. <span data-ttu-id="f2a4c-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="f2a4c-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="f2a4c-114">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="f2a4c-115">1. Créer un espace de noms à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f2a4c-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="f2a4c-116">Si vous disposez déjà créé un espace de noms Relay, passez à la section [Créer une connexion hybride à l’aide du portail Azure](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f2a4c-116">If you already have a Relay namespace created, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="f2a4c-117">2. Créer une connexion hybride à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="f2a4c-117">2. Create a hybrid connection using the Azure portal</span></span>

<span data-ttu-id="f2a4c-118">Si vous disposez déjà d’une connexion hybride, passez à la section [Créer une application de serveur](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="f2a4c-118">If you already have a hybrid connection created, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="f2a4c-119">3. Créer une application de serveur (récepteur)</span><span class="sxs-lookup"><span data-stu-id="f2a4c-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="f2a4c-120">Pour écouter et recevoir des messages à partir de Relay, nous allons écrire une application de console Node.js.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-120">To listen and receive messages from the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="f2a4c-121">4. Créer une application cliente (expéditeur)</span><span class="sxs-lookup"><span data-stu-id="f2a4c-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="f2a4c-122">Pour envoyer des messages à Relay, nous allons écrire une application de console Node.js.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-122">To send messages to the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="f2a4c-123">5. Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="f2a4c-123">5. Run the applications</span></span>

1. <span data-ttu-id="f2a4c-124">Exécutez l’application serveur : à partir d’un type d’invite de commandes Node.js `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-124">Run the server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="f2a4c-125">Exécutez l’application cliente : à partir d’un type d’invite de commandes Node.js `node sender.js`, puis entrez du texte.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-125">Run the client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="f2a4c-126">Vérifiez que la console d’application de serveur renvoie le texte entré dans l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="f2a4c-126">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="f2a4c-128">Vous avez créé une application de connexions hybrides complète avec Node.js : félicitations !</span><span class="sxs-lookup"><span data-stu-id="f2a4c-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2a4c-129">Étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2a4c-129">Next steps:</span></span>

* [<span data-ttu-id="f2a4c-130">FAQ Relay</span><span class="sxs-lookup"><span data-stu-id="f2a4c-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="f2a4c-131">Créer un espace de noms</span><span class="sxs-lookup"><span data-stu-id="f2a4c-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="f2a4c-132">Prise en main de .NET</span><span class="sxs-lookup"><span data-stu-id="f2a4c-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="f2a4c-133">Prise en main de Node</span><span class="sxs-lookup"><span data-stu-id="f2a4c-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

