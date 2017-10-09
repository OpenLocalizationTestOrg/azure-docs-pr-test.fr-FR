---
title: applications aaaUsing App-V avec Azure RemoteApp | Documents Microsoft
description: "Découvrez comment les applications toouse App-V dans Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="e1447-103">Utilisation d'applications App-V dans Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e1447-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e1447-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="e1447-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e1447-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e1447-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e1447-106">Vous pouvez utiliser des applications App-V dans une collection hybride Azure RemoteApp, ce qui nécessite la jonction de domaine.</span><span class="sxs-lookup"><span data-stu-id="e1447-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="e1447-107">Avant de commencer, assurez-vous que client App-V 5.1 de hello tooinstall avec les dernières mises à jour de hello.</span><span class="sxs-lookup"><span data-stu-id="e1447-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="e1447-108">Vous devez toocreate une [image personnalisée](remoteapp-create-custom-image.md) qui inclut le client de hello App-V.</span><span class="sxs-lookup"><span data-stu-id="e1447-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="e1447-109">Il est facile toouse votre infrastructure App-V avec Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e1447-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="e1447-110">Comme une collection hybride est déployée dans un réseau virtuel Azure qui est contrôleur de domaine de l’accès tooyour et machines virtuelles de hello sont joints à un domaine, vous pouvez exploiter votre existante application App-v infrastructure et de déploiement méthodes tooeasyily hôte App-V dans Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e1447-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="e1447-111">Voici quelques considérations que vous devez connaître en fonction de type hello du déploiement d’App-V qu'est actuellement :</span><span class="sxs-lookup"><span data-stu-id="e1447-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="e1447-112">Options de configuration</span><span class="sxs-lookup"><span data-stu-id="e1447-112">Configuration options</span></span> |  | <span data-ttu-id="e1447-113">Positive</span><span class="sxs-lookup"><span data-stu-id="e1447-113">Positive</span></span> | <span data-ttu-id="e1447-114">Negative</span><span class="sxs-lookup"><span data-stu-id="e1447-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e1447-115">Méthode de remise</span><span class="sxs-lookup"><span data-stu-id="e1447-115">Delivery method</span></span> |<span data-ttu-id="e1447-116">Diffusion en continu (à la demande)</span><span class="sxs-lookup"><span data-stu-id="e1447-116">Streaming (on-demand)</span></span> |<span data-ttu-id="e1447-117">Application est toujours hello nouvelle et plus récents</span><span class="sxs-lookup"><span data-stu-id="e1447-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="e1447-118">Première latence</span><span class="sxs-lookup"><span data-stu-id="e1447-118">First time latency</span></span> |
| <span data-ttu-id="e1447-119">Montée</span><span class="sxs-lookup"><span data-stu-id="e1447-119">Mounted</span></span> |<span data-ttu-id="e1447-120">Plus rapide ; application est déjà présente sur hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e1447-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="e1447-121">Encombrement - occupe de l'espace image (limite 127 Go)</span><span class="sxs-lookup"><span data-stu-id="e1447-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="e1447-122">Stockage de l'emplacement d'application</span><span class="sxs-lookup"><span data-stu-id="e1447-122">App location storage</span></span> |<span data-ttu-id="e1447-123">Contenu partagé</span><span class="sxs-lookup"><span data-stu-id="e1447-123">Shared content</span></span> |<span data-ttu-id="e1447-124">L'application est exécutée dans la mémoire de l'instance Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e1447-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="e1447-125">Mange mémoire et la bonne connexion du serveur toostreaming (fichier) à l’emplacement de l’application hello</span><span class="sxs-lookup"><span data-stu-id="e1447-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="e1447-126">Disque (en cache)</span><span class="sxs-lookup"><span data-stu-id="e1447-126">Disk (Cached)</span></span> |<span data-ttu-id="e1447-127">Exécution rapide.</span><span class="sxs-lookup"><span data-stu-id="e1447-127">Fast execution.</span></span> <span data-ttu-id="e1447-128">L'application ne dépend pas de la disponibilité du contenu source</span><span class="sxs-lookup"><span data-stu-id="e1447-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="e1447-129">Encombrement - occupe de l'espace image (limite 127 Go)</span><span class="sxs-lookup"><span data-stu-id="e1447-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="e1447-130">Ciblage</span><span class="sxs-lookup"><span data-stu-id="e1447-130">Targeting</span></span> |<span data-ttu-id="e1447-131">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="e1447-131">User</span></span> |<span data-ttu-id="e1447-132">Nécessite une infrastructure App-V entièrement autonome</span><span class="sxs-lookup"><span data-stu-id="e1447-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="e1447-133">Global (machine)</span><span class="sxs-lookup"><span data-stu-id="e1447-133">Global (machine)</span></span> |<span data-ttu-id="e1447-134">Pré-publication ou cible avec le serveur de publication</span><span class="sxs-lookup"><span data-stu-id="e1447-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="e1447-135">Devez tooupdate votre image Azure si vous souhaitez tooupdate hello application (énorme).</span><span class="sxs-lookup"><span data-stu-id="e1447-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="e1447-136">Occupe de l'espace sur l'image.</span><span class="sxs-lookup"><span data-stu-id="e1447-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="e1447-137">Après avoir créé votre image personnalisée de votre collection hybride, publiez votre application, affecter des utilisateurs et profitez de vos applications App-V existantes hébergées dans Azure RemoteApp remis appareil tooany n’importe où.</span><span class="sxs-lookup"><span data-stu-id="e1447-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

