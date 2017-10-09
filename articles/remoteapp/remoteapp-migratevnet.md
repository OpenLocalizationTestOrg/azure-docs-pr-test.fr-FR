---
title: "toomigrate aaaHow à partir d’un réseau virtuel Azure de tooan RemoteApp VNET | Documents Microsoft"
description: "Découvrez comment toomigrate à partir d’un réseau virtuel Azure de tooan RemoteApp VNET"
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
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a><span data-ttu-id="9361d-103">Comment toomigrate une collection hybride à partir d’un réseau virtuel Azure de tooan RemoteApp VNET</span><span class="sxs-lookup"><span data-stu-id="9361d-103">How toomigrate a hybrid collection from a RemoteApp VNET tooan Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9361d-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="9361d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9361d-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="9361d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9361d-106">Bonne nouvelle !</span><span class="sxs-lookup"><span data-stu-id="9361d-106">Good news!</span></span> <span data-ttu-id="9361d-107">Nous avons activé collections de RemoteApp hybride toodeploy directement dans votre existant réseaux virtuels Azure (réseaux virtuels) au lieu de créer des réseaux virtuels RemoteApp spécifiques.</span><span class="sxs-lookup"><span data-stu-id="9361d-107">We have enabled you toodeploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="9361d-108">Cela vous permet de tirer parti de hello dernières fonctionnalités de réseau virtuel (par exemple, ExpressRoute) et donnez à votre tooother de l’accès réseau direct hybride collections services Azure et les ordinateurs virtuels déployés toothat réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9361d-108">This lets you take advantage of hello latest VNET features (like ExpressRoute) and give your hybrid collections direct network access tooother Azure services and virtual machines deployed toothat VNET.</span></span>  <span data-ttu-id="9361d-109">(Ceci améliore les performances et facilite l’installation par rapport aux configurations de réseau virtuel à réseau virtuel).</span><span class="sxs-lookup"><span data-stu-id="9361d-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="9361d-110">Supposons que vous avez déjà créé une collection RemoteApp hybride appelée *OriginalCollection* avec un réseau virtuel RemoteApp appelé *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="9361d-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="9361d-111">Voici hello étapes toomigrate il tooa appelée de nouveau de réseau virtuel Azure *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="9361d-111">Here are hello steps toomigrate it tooa new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="9361d-112">Sur hello **réseaux** onglet Bonjour [portail de gestion](http://manage.windowsazure.com/), créez un réseau virtuel appelé *AzureVNET*, à l’aide hello même emplacement, la configuration de DNS et l’espace d’adressage (au moins pour Hello *AzureVNET* sous-réseaux) en tant que vous avez utilisé pour *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="9361d-112">On hello **Networks** tab in hello [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using hello same location, DNS configuration, and address space (for at least one of hello *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="9361d-113">Configurer *AzureVNET* tooeither héberger ou avoir le déploiement d’Active Directory toohello une connexion réseau qui *OriginalCollection* est joint au.</span><span class="sxs-lookup"><span data-stu-id="9361d-113">Configure *AzureVNET* tooeither host or have network connectivity toohello Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="9361d-114">Sur hello **applications distantes** , onglet de créer une nouvelle collection RemoteApp appelée *nouvelle Collection*.</span><span class="sxs-lookup"><span data-stu-id="9361d-114">On hello **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="9361d-115">(Hello d’utilisation **créer avec le réseau virtuel** n'option pas **création rapide**.)</span><span class="sxs-lookup"><span data-stu-id="9361d-115">(Use hello **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="9361d-116">Configurer *NewCollection* toobe déployé sous-réseau tooa *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="9361d-116">Configure *NewCollection* toobe deployed tooa subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="9361d-117">Configurer *NewCollection* toouse hello même image et les informations de jonction de domaine en tant que vous avez utilisé pour *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="9361d-117">Configure *NewCollection* toouse hello same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="9361d-118">Après quelques heures, *NewCollection* apparaît dans la liste de collections avec le statut Actif.</span><span class="sxs-lookup"><span data-stu-id="9361d-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="9361d-119">Maintenant, si vous n’avez pas besoin toomigrate toutes les informations utilisateur à partir de hello d’origine toohello nouveau regroupement, effectuez ces étapes suivant :</span><span class="sxs-lookup"><span data-stu-id="9361d-119">Now, if you DON’T need toomigrate any user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="9361d-120">Supprimez *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="9361d-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="9361d-121">Supprimez *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="9361d-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="9361d-122">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="9361d-122">And, you’re done!</span></span>

<span data-ttu-id="9361d-123">Ou bien, si vous n’avez pas besoin d’informations utilisateur toomigrate de hello d’origine toohello nouveau regroupement, effectuez ces étapes suivant :</span><span class="sxs-lookup"><span data-stu-id="9361d-123">Alternately, if you DO need toomigrate user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="9361d-124">Envoyer un courrier électronique trop[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) avec votre ID d’abonnement Azure hello du nom de votre collection d’origine et le nom hello de votre nouvelle collection et demandez-lui de toomigrate vos informations utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9361d-124">Send an email too[remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, hello name of your original collection, and hello name of your new collection, and ask them toomigrate your user information.</span></span>
2. <span data-ttu-id="9361d-125">Dans les 2 jours ouvrables équipe de RemoteApp hello passeront liste d’accès utilisateur hello et tous les documents de l’utilisateur et les paramètres utilisateur d’hello d’origine toohello nouveau regroupement.</span><span class="sxs-lookup"><span data-stu-id="9361d-125">Within 2 business days hello RemoteApp team will move hello user access list and all user documents and user settings from hello original collection toohello new collection.</span></span>
3. <span data-ttu-id="9361d-126">Supprimez *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="9361d-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="9361d-127">Supprimez *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="9361d-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="9361d-128">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="9361d-128">And now, you’re done!</span></span>

<span data-ttu-id="9361d-129">Si vous avez des questions ou que vous avez besoin d’aide, envoyez un e-mail [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="9361d-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

