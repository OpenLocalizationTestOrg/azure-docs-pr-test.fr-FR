---
title: "aaaGuide toocreating un modèle de solution pour hello Marketplace | Documents Microsoft"
description: "Instructions détaillées sur comment toocreate, certifier et déployer un modèle de Solution Multi-VM Image à l’achat sur hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="00300-103">Guide toocreate un modèle de solution pour Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="00300-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="00300-104">Après avoir effectué l’étape 1, [compte de la création et l’inscription][link-acct-creation], nous vous interactive sur la création de hello d’un modèle de solution compatible avec Azure à [technique configuration requise pour la création d’un modèle de solution](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="00300-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="00300-105">Maintenant nous vous guidera à travers les étapes de hello pour la création d’un modèle de solution pour plusieurs machines virtuelles sur hello [portail de publication] [ link-pubportal] pour hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="00300-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="00300-106">Créer votre offre de modèle de solution Bonjour portail de publication</span><span class="sxs-lookup"><span data-stu-id="00300-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="00300-107">Accédez trop [https://publish.windowsazure.com](http://publish.windowsazure.com). Lors de la connexion pour hello première heure toohello [portail de publication](https://publish.windowsazure.com/), hello utilisez même compte avec lequel le profil de vendeur de votre entreprise a été inscrite.</span><span class="sxs-lookup"><span data-stu-id="00300-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="00300-108">Une version ultérieure, vous pouvez ajouter tous les employés de votre société en tant qu’un administrateur de co Bonjour portail de publication.</span><span class="sxs-lookup"><span data-stu-id="00300-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="00300-109">1. Sélectionner « Modèles de solution »</span><span class="sxs-lookup"><span data-stu-id="00300-109">1. Select "Solution templates"</span></span>
  ![dessin][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="00300-111">2. Créer un modèle de solution</span><span class="sxs-lookup"><span data-stu-id="00300-111">2. Create a new solution template</span></span>
  ![dessin][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="00300-113">3. Démarrer avec les topologies</span><span class="sxs-lookup"><span data-stu-id="00300-113">3. Start with topologies</span></span>
<span data-ttu-id="00300-114">Un modèle de solution est un tooall « parent » de son topologies.</span><span class="sxs-lookup"><span data-stu-id="00300-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="00300-115">Vous pouvez définir plusieurs topologies dans une offre/un modèle de solution.</span><span class="sxs-lookup"><span data-stu-id="00300-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="00300-116">Lorsqu’une offre est envoyée toostaging, il est envoyé avec toutes ses topologies.</span><span class="sxs-lookup"><span data-stu-id="00300-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="00300-117">Suivez les étapes de hello ci-dessous toodefine votre offre :</span><span class="sxs-lookup"><span data-stu-id="00300-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="00300-118">Créer une topologie : « Identificateur de la topologie » désigne généralement hello de topologie de hello pour le modèle de solution hello.</span><span class="sxs-lookup"><span data-stu-id="00300-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="00300-119">identificateur de topologie Hello est utilisé dans les URL de hello, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="00300-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="00300-120">Azure Marketplace : http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="00300-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="00300-121">Portail Azure : https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="00300-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="00300-122">Ajouter une nouvelle version.</span><span class="sxs-lookup"><span data-stu-id="00300-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="00300-123">4. Obtenir la certification des versions de votre topologie</span><span class="sxs-lookup"><span data-stu-id="00300-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="00300-124">Télécharger un fichier zip qui contient tous les fichiers requis tooprovision cette version particulière de la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="00300-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="00300-125">Ce fichier zip doit contenir des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="00300-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="00300-126">Fichiers *mainTemplate.json* et *createUiDefinition.json* dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="00300-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="00300-127">Tous les modèles liés et tous les scripts nécessaires.</span><span class="sxs-lookup"><span data-stu-id="00300-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="00300-128">Alors que les développeurs de travaillent sur la création des topologies de modèle de solution de hello et leur certifié, l’activité hello, marketing et/ou juridiques départements de votre entreprise peuvent travailler sur le contenu marketing et juridiques hello.</span><span class="sxs-lookup"><span data-stu-id="00300-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="00300-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00300-129">Next steps</span></span>
<span data-ttu-id="00300-130">Maintenant que vous avez créé votre modèle de solution et que vous téléchargé le fichier zip de hello, suivez les instructions de hello Bonjour [guide de contenu marketing Marketplace](marketplace-publishing-push-to-staging.md) avant d’installer hello offre toostaging.</span><span class="sxs-lookup"><span data-stu-id="00300-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="00300-131">ensemble complet de hello toosee de marketplace publication d’articles, visitez [mise en route : comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="00300-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="00300-132">Les rubriques suivantes peuvent également vous intéresser :</span><span class="sxs-lookup"><span data-stu-id="00300-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="00300-133">Images de machine virtuelle : [À propos des images de machine virtuelle dans Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="00300-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="00300-134">Extensions de machine virtuelle : [Présentation de l’agent de machine virtuelle et des extensions de machine virtuelle](https://msdn.microsoft.com/library/azure/dn832621.aspx) et [Fonctionnalités et extensions de machine virtuelle Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="00300-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="00300-135">Azure Resource Manager : [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) et [Exemples de modèles simples](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="00300-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="00300-136">Limite du compte de stockage : [comment tooMonitor de limitation du compte de stockage](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) et [stockage Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="00300-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
