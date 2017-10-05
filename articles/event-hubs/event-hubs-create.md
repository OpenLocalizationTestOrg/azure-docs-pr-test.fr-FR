---
title: "Création d’un concentrateur d’événements Azure | Microsoft Docs"
description: "Créer un espace de noms Azure Event Hubs et un concentrateur d’événements avec le portail Azure"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 816bf1426704d3391550e80c0700f1b011683a94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a><span data-ttu-id="6b6d3-103">Créer un espace de noms Event Hubs et un concentrateur d’événements avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6b6d3-103">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="6b6d3-104">Créer un espace de noms Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6b6d3-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="6b6d3-105">Connectez-vous au [portail Azure][Azure portal], puis cliquez sur **Nouveau** en haut à gauche de l’écran.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
1. <span data-ttu-id="6b6d3-106">Cliquez sur **Internet des Objets**, puis sur **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="6b6d3-107">Dans le panneau **Créer un espace de noms** , entrez un nom d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-107">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="6b6d3-108">Le système vérifie immédiatement si le nom est disponible.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-108">The system immediately checks to see if the name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="6b6d3-109">Lorsque vous avez vérifié la disponibilité de l’espace de noms, sélectionnez le niveau tarifaire (Basique ou Standard).</span><span class="sxs-lookup"><span data-stu-id="6b6d3-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="6b6d3-110">Choisissez également un abonnement Azure, un groupe de ressources et l’emplacement où créer la ressource.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> 
1. <span data-ttu-id="6b6d3-111">Cliquez sur **Créer** pour créer l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-111">Click **Create** to create the namespace.</span></span> <span data-ttu-id="6b6d3-112">Vous devrez peut-être attendre quelques minutes pour que le système approvisionne entièrement les ressources.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-112">You may have to wait a few minutes for the system to fully provision the resources.</span></span>
2. <span data-ttu-id="6b6d3-113">Dans la liste des espaces de noms du portail, cliquez sur l’espace de noms que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-113">In the portal list of namespaces, click the newly created namespace.</span></span>
2. <span data-ttu-id="6b6d3-114">Cliquez sur **Stratégies d’accès partagé**, puis sur **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="6b6d3-115">Cliquez sur le bouton Copier pour copier la chaîne de connexion **RootManageSharedAccessKey** dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-115">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="6b6d3-116">Enregistrez cette chaîne de connexion dans un emplacement temporaire, tel que le Bloc-notes, pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-116">Save this connection string in a temporary location, such as Notepad, to use later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="6b6d3-117">Création d'un concentrateur d'événements</span><span class="sxs-lookup"><span data-stu-id="6b6d3-117">Create an event hub</span></span>

1. <span data-ttu-id="6b6d3-118">Dans la liste d’espaces de noms Event Hubs, cliquez sur le nouvel espace de noms.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-118">In the Event Hubs namespace list, click the newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="6b6d3-119">Dans le panneau de l’espace de noms, cliquez sur **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-119">In the namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="6b6d3-120">Cliquez sur **Ajouter un Event Hub**en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-120">At the top of the blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="6b6d3-121">Saisissez un nom pour votre concentrateur d’événements, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="6b6d3-122">Votre concentrateur d’événements est désormais créé et vous disposez des chaînes de connexion dont vous avez besoin pour envoyer et recevoir des événements.</span><span class="sxs-lookup"><span data-stu-id="6b6d3-122">Your event hub is now created, and you have the connection strings you need to send and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b6d3-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b6d3-123">Next steps</span></span>
<span data-ttu-id="6b6d3-124">Pour en savoir plus les hubs d’événements, consultez ces liens :</span><span class="sxs-lookup"><span data-stu-id="6b6d3-124">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="6b6d3-125">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="6b6d3-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6b6d3-126">Vue d’ensemble de l'API Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6b6d3-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/