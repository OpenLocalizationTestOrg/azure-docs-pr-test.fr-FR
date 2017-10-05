---
title: "Comment migrer un réseau virtuel RemoteApp vers un réseau virtuel Azure | Microsoft Docs"
description: "Découvrir comment migrer un réseau virtuel RemoteApp vers un réseau virtuel Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a><span data-ttu-id="ee5db-103">Comment migrer une collection hybride d’un réseau virtuel RemoteApp à un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="ee5db-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ee5db-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="ee5db-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ee5db-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="ee5db-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ee5db-106">Bonne nouvelle !</span><span class="sxs-lookup"><span data-stu-id="ee5db-106">Good news!</span></span> <span data-ttu-id="ee5db-107">Vous avez désormais la possibilité de déployer des collections RemoteApp hybrides directement sur vos réseaux virtuels (VNET) Azure existants au lieu de devoir créer des réseaux virtuels RemoteApp spécifiques.</span><span class="sxs-lookup"><span data-stu-id="ee5db-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="ee5db-108">Cela vous permet de tirer parti des dernières fonctionnalités de réseau virtuel (comme ExpressRoute) et offre à vos collections hybrides un accès réseau direct à d’autres services Azure et ordinateurs virtuels déployés sur ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ee5db-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span></span>  <span data-ttu-id="ee5db-109">(Ceci améliore les performances et facilite l’installation par rapport aux configurations de réseau virtuel à réseau virtuel).</span><span class="sxs-lookup"><span data-stu-id="ee5db-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="ee5db-110">Supposons que vous avez déjà créé une collection RemoteApp hybride appelée *OriginalCollection* avec un réseau virtuel RemoteApp appelé *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="ee5db-111">Voici les étapes à suivre pour effectuer la migration vers un nouveau réseau virtuel Azure appelé *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="ee5db-112">Dans l’onglet **Réseaux** du [Portail de gestion](http://manage.windowsazure.com/), créez un réseau virtuel appelé *AzureVNET* en utilisant un emplacement, une configuration DNS et un espace d’adressage identiques (pour au moins l’un des sous-réseaux *AzureVNET*) à ceux utilisés pour *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="ee5db-113">Configurez *AzureVNET* de manière à héberger le déploiement d’Active Directory avec lequel la collection *OriginalCollection* est jointe au domaine, ou à établir une connectivité réseau avec ce dernier.</span><span class="sxs-lookup"><span data-stu-id="ee5db-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="ee5db-114">Dans l’onglet **RemoteApps** , créez une collection RemoteApp appelée *Nouvelle Collection*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="ee5db-115">(Utilisez l’option **Créer avec VNET** plutôt que l’option **Création rapide**.)</span><span class="sxs-lookup"><span data-stu-id="ee5db-115">(Use the **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="ee5db-116">Configurez *NewCollection* de manière à être déployée sur un sous-réseau dans *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="ee5db-117">Configurez *NewCollection* de manière à utiliser la même image et les mêmes informations de jonction de domaine que celles utilisées pour *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="ee5db-118">Après quelques heures, *NewCollection* apparaît dans la liste de collections avec le statut Actif.</span><span class="sxs-lookup"><span data-stu-id="ee5db-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="ee5db-119">Si vous n’avez PAS besoin de migrer des informations utilisateur depuis la collection d’origine vers la nouvelle collection, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ee5db-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="ee5db-120">Supprimez *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="ee5db-121">Supprimez *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="ee5db-122">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="ee5db-122">And, you’re done!</span></span>

<span data-ttu-id="ee5db-123">Si vous DEVEZ migrer des informations utilisateur depuis la collection d’origine vers la nouvelle collection, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ee5db-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="ee5db-124">Envoyez un e-mail à [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) avec votre ID d’abonnement Azure, le nom de votre collection d’origine et le nom de votre nouvelle collection, et demandez à migrer vos informations utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ee5db-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span></span>
2. <span data-ttu-id="ee5db-125">Dans les deux jours ouvrés, l’équipe RemoteApp déplace la liste d’accès utilisateur, ainsi que tous les documents et paramètres de l’utilisateur de la collection d’origine vers la nouvelle collection.</span><span class="sxs-lookup"><span data-stu-id="ee5db-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span></span>
3. <span data-ttu-id="ee5db-126">Supprimez *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="ee5db-127">Supprimez *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="ee5db-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="ee5db-128">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="ee5db-128">And now, you’re done!</span></span>

<span data-ttu-id="ee5db-129">Si vous avez des questions ou que vous avez besoin d’aide, envoyez un e-mail [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="ee5db-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

