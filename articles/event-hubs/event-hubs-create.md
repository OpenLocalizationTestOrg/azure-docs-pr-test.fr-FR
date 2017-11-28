---
title: "aaaCreate un concentrateur d’événements Azure | Documents Microsoft"
description: "Créer un espace de noms Azure Event Hubs et un concentrateur d’événements à l’aide de hello portail Azure"
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
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="61614-103">Créer un espace de noms de concentrateurs d’événements et un concentrateur d’événements à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="61614-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="61614-104">Créer un espace de noms Event Hubs</span><span class="sxs-lookup"><span data-stu-id="61614-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="61614-105">Session toohello [portail Azure][Azure portal], puis cliquez sur **nouveau** à hello haut à gauche de l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="61614-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="61614-106">Cliquez sur **Internet des Objets**, puis sur **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="61614-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="61614-107">Bonjour **créer l’espace de noms** panneau, entrez un nom d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="61614-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="61614-108">système de Hello vérifie immédiatement toosee si le nom hello est disponible.</span><span class="sxs-lookup"><span data-stu-id="61614-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="61614-109">Une fois que nom d’espace de noms hello de fabrication est disponible, choisissez hello tarification (base ou Standard).</span><span class="sxs-lookup"><span data-stu-id="61614-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="61614-110">En outre, choisissez un abonnement Azure, le groupe de ressources et l’emplacement de ressources toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="61614-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="61614-111">Cliquez sur **créer** toocreate hello espace de noms.</span><span class="sxs-lookup"><span data-stu-id="61614-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="61614-112">Vous avez peut-être toowait quelques minutes pour les ressources hello hello système toofully disposition.</span><span class="sxs-lookup"><span data-stu-id="61614-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="61614-113">Dans hello portail la liste des espaces de noms, cliquez sur hello nouvellement créé espace de noms.</span><span class="sxs-lookup"><span data-stu-id="61614-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="61614-114">Cliquez sur **Stratégies d’accès partagé**, puis sur **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="61614-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="61614-115">Cliquez sur Bonjour copie bouton toocopy Bonjour **RootManageSharedAccessKey** Presse-papiers de toohello de chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="61614-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="61614-116">Enregistrez cette chaîne de connexion dans un emplacement temporaire, tel que le bloc-notes, toouse plus tard.</span><span class="sxs-lookup"><span data-stu-id="61614-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="61614-117">Création d'un concentrateur d'événements</span><span class="sxs-lookup"><span data-stu-id="61614-117">Create an event hub</span></span>

1. <span data-ttu-id="61614-118">Dans hello concentrateurs d’événements espace de noms, cliquez sur espace de noms hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="61614-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="61614-119">Dans le panneau espace de noms de hello, cliquez sur **concentrateurs d’événements**.</span><span class="sxs-lookup"><span data-stu-id="61614-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="61614-120">Haut hello du Panneau de hello, cliquez sur **concentrateur d’événements ajouter**.</span><span class="sxs-lookup"><span data-stu-id="61614-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="61614-121">Saisissez un nom pour votre concentrateur d’événements, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="61614-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="61614-122">Votre concentrateur d’événements est créée, et que les chaînes de connexion hello vous devez toosend et recevez des événements.</span><span class="sxs-lookup"><span data-stu-id="61614-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61614-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61614-123">Next steps</span></span>
<span data-ttu-id="61614-124">toolearn en savoir plus sur les concentrateurs d’événements, consultez ces liens :</span><span class="sxs-lookup"><span data-stu-id="61614-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="61614-125">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="61614-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="61614-126">Vue d’ensemble de l'API Event Hubs</span><span class="sxs-lookup"><span data-stu-id="61614-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/