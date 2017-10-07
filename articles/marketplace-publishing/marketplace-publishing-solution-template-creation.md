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
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a>Guide toocreate un modèle de solution pour Azure Marketplace
Après avoir effectué l’étape 1, [compte de la création et l’inscription][link-acct-creation], nous vous interactive sur la création de hello d’un modèle de solution compatible avec Azure à [technique configuration requise pour la création d’un modèle de solution](marketplace-publishing-solution-template-creation-prerequisites.md). Maintenant nous vous guidera à travers les étapes de hello pour la création d’un modèle de solution pour plusieurs machines virtuelles sur hello [portail de publication] [ link-pubportal] pour hello Azure Marketplace.

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a>Créer votre offre de modèle de solution Bonjour portail de publication
Accédez trop [https://publish.windowsazure.com](http://publish.windowsazure.com). Lors de la connexion pour hello première heure toohello [portail de publication](https://publish.windowsazure.com/), hello utilisez même compte avec lequel le profil de vendeur de votre entreprise a été inscrite. Une version ultérieure, vous pouvez ajouter tous les employés de votre société en tant qu’un administrateur de co Bonjour portail de publication.

### <a name="1-select-solution-templates"></a>1. Sélectionner « Modèles de solution »
  ![dessin][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a>2. Créer un modèle de solution
  ![dessin][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a>3. Démarrer avec les topologies
Un modèle de solution est un tooall « parent » de son topologies. Vous pouvez définir plusieurs topologies dans une offre/un modèle de solution. Lorsqu’une offre est envoyée toostaging, il est envoyé avec toutes ses topologies. Suivez les étapes de hello ci-dessous toodefine votre offre :     

* Créer une topologie : « Identificateur de la topologie » désigne généralement hello de topologie de hello pour le modèle de solution hello. identificateur de topologie Hello est utilisé dans les URL de hello, comme indiqué ci-dessous :

  Azure Marketplace : http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}

  Portail Azure : https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}
* Ajouter une nouvelle version.

### <a name="4-get-your-topology-versions-certified"></a>4. Obtenir la certification des versions de votre topologie
Télécharger un fichier zip qui contient tous les fichiers requis tooprovision cette version particulière de la topologie de hello. Ce fichier zip doit contenir des éléments suivants de hello :

* Fichiers *mainTemplate.json* et *createUiDefinition.json* dans le répertoire racine.
* Tous les modèles liés et tous les scripts nécessaires.

  > [!TIP]
  > Alors que les développeurs de travaillent sur la création des topologies de modèle de solution de hello et leur certifié, l’activité hello, marketing et/ou juridiques départements de votre entreprise peuvent travailler sur le contenu marketing et juridiques hello.
  >
  >

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez créé votre modèle de solution et que vous téléchargé le fichier zip de hello, suivez les instructions de hello Bonjour [guide de contenu marketing Marketplace](marketplace-publishing-push-to-staging.md) avant d’installer hello offre toostaging. ensemble complet de hello toosee de marketplace publication d’articles, visitez [mise en route : comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md).

Les rubriques suivantes peuvent également vous intéresser :

* Images de machine virtuelle : [À propos des images de machine virtuelle dans Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)
* Extensions de machine virtuelle : [Présentation de l’agent de machine virtuelle et des extensions de machine virtuelle](https://msdn.microsoft.com/library/azure/dn832621.aspx) et [Fonctionnalités et extensions de machine virtuelle Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)
* Azure Resource Manager : [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) et [Exemples de modèles simples](https://github.com/rjmax/ArmExamples)
* Limite du compte de stockage : [comment tooMonitor de limitation du compte de stockage](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) et [stockage Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
