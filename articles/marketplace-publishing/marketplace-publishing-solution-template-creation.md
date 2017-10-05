---
title: "Guide de création d’un modèle de solution pour Azure Marketplace | Microsoft Docs"
description: "Instructions détaillées pour créer, certifier et déployer un modèle de solution d’image multimachine virtuelle que d’autres peuvent acheter sur Azure Marketplace."
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
ms.openlocfilehash: b753bfb4bd69bd9aacf4eebd8999397394c28bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="4364b-103">Guide de création d’un modèle de solution pour Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4364b-103">Guide to create a solution template for Azure Marketplace</span></span>
<span data-ttu-id="4364b-104">Une fois l’étape 1 [Création de comptes et inscription][link-acct-creation] exécutée, nous vous avons guidé dans la procédure de création d’un modèle de solution compatible Azure avec la section [Conditions techniques préalables pour créer un modèle de solution](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="4364b-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="4364b-105">À présent, nous allons vous guider dans la procédure de création d’un modèle de solution à plusieurs machines virtuelles dans le [Portail de publication][link-pubportal] pour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4364b-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-the-publishing-portal"></a><span data-ttu-id="4364b-106">Créer votre offre de modèle de solution dans le portail de publication</span><span class="sxs-lookup"><span data-stu-id="4364b-106">Create your solution template offer in the Publishing Portal</span></span>
<span data-ttu-id="4364b-107">Accédez à [https://publish.windowsazure.com](http://publish.windowsazure.com). Pour votre première connexion au [portail de publication](https://publish.windowsazure.com/), utilisez le compte avec lequel le profil de vendeur de votre entreprise a été inscrit.</span><span class="sxs-lookup"><span data-stu-id="4364b-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="4364b-108">Plus tard, vous pourrez ajouter des employés de l’entreprise comme coadministrateurs dans le portail de publication.</span><span class="sxs-lookup"><span data-stu-id="4364b-108">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="4364b-109">1. Sélectionner « Modèles de solution »</span><span class="sxs-lookup"><span data-stu-id="4364b-109">1. Select "Solution templates"</span></span>
  ![dessin][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="4364b-111">2. Créer un modèle de solution</span><span class="sxs-lookup"><span data-stu-id="4364b-111">2. Create a new solution template</span></span>
  ![dessin][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="4364b-113">3. Démarrer avec les topologies</span><span class="sxs-lookup"><span data-stu-id="4364b-113">3. Start with topologies</span></span>
<span data-ttu-id="4364b-114">Un modèle de solution est « parent » de toutes ses topologies.</span><span class="sxs-lookup"><span data-stu-id="4364b-114">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="4364b-115">Vous pouvez définir plusieurs topologies dans une offre/un modèle de solution.</span><span class="sxs-lookup"><span data-stu-id="4364b-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="4364b-116">Quand une offre est envoyée dans l’environnement intermédiaire, toutes ses topologies l’accompagnent.</span><span class="sxs-lookup"><span data-stu-id="4364b-116">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="4364b-117">Suivez les étapes ci-dessous pour définir votre offre :</span><span class="sxs-lookup"><span data-stu-id="4364b-117">Follow the steps below to define your offer:</span></span>     

* <span data-ttu-id="4364b-118">Créer une topologie : « Identificateur de topologie » est généralement le nom de la topologie pour le modèle de solution.</span><span class="sxs-lookup"><span data-stu-id="4364b-118">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span></span> <span data-ttu-id="4364b-119">L’identificateur de topologie est utilisé dans l’URL comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4364b-119">The topology identifier is used in the URL as shown below:</span></span>

  <span data-ttu-id="4364b-120">Azure Marketplace : http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="4364b-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="4364b-121">Portail Azure : https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="4364b-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="4364b-122">Ajouter une nouvelle version.</span><span class="sxs-lookup"><span data-stu-id="4364b-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="4364b-123">4. Obtenir la certification des versions de votre topologie</span><span class="sxs-lookup"><span data-stu-id="4364b-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="4364b-124">Téléchargez un fichier zip contenant tous les fichiers requis pour configurer cette version particulière de la topologie.</span><span class="sxs-lookup"><span data-stu-id="4364b-124">Upload a zip file that contains all required files to provision that particular version of the topology.</span></span> <span data-ttu-id="4364b-125">Ce fichier zip doit contenir les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="4364b-125">This zip file must contain the following:</span></span>

* <span data-ttu-id="4364b-126">Fichiers *mainTemplate.json* et *createUiDefinition.json* dans le répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="4364b-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="4364b-127">Tous les modèles liés et tous les scripts nécessaires.</span><span class="sxs-lookup"><span data-stu-id="4364b-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="4364b-128">Pendant que vos développeurs se chargent de la création des topologies du modèle de solution et obtiennent leur certification, les services commerciaux, marketing et/ou juridique de votre entreprise se chargent du contenu marketing et juridique.</span><span class="sxs-lookup"><span data-stu-id="4364b-128">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="4364b-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4364b-129">Next steps</span></span>
<span data-ttu-id="4364b-130">Maintenant que vous créé votre modèle de solution et téléchargé le fichier zip, suivez les instructions du [Guide de contenu marketing Marketplace](marketplace-publishing-push-to-staging.md) avant de faire passer l’offre en production.</span><span class="sxs-lookup"><span data-stu-id="4364b-130">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span></span> <span data-ttu-id="4364b-131">Vous pouvez accéder à l’ensemble des articles de publication Marketplace via l’article [Prise en main : publier une offre dans Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4364b-131">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="4364b-132">Les rubriques suivantes peuvent également vous intéresser :</span><span class="sxs-lookup"><span data-stu-id="4364b-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="4364b-133">Images de machine virtuelle : [À propos des images de machine virtuelle dans Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="4364b-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="4364b-134">Extensions de machine virtuelle : [Présentation de l’agent de machine virtuelle et des extensions de machine virtuelle](https://msdn.microsoft.com/library/azure/dn832621.aspx) et [Fonctionnalités et extensions de machine virtuelle Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="4364b-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="4364b-135">Azure Resource Manager : [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) et [Exemples de modèles simples](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="4364b-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="4364b-136">Limitations des comptes de stockage : [Surveiller les limitations des comptes de stockage](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) et [Stockage Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="4364b-136">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
