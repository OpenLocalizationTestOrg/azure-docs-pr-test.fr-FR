---
title: aaaTest proposent de votre machine virtuelle pour hello Marketplace | Documents Microsoft
description: "Comprendre comment tootest votre machine virtuelle de l’image pour hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>Tester votre offre de la machine virtuelle pour hello Azure Marketplace intermédiaire
Désigne un déploiement de votre référence (SKU) « bac à sable » où vous pouvez tester et valider ses fonctionnalités avant de le déployer toohello Marketplace privé de mise en lots. Hello référence (SKU) s’affiche dans la mise en lots comme il le ferait client tooa qui a déployé. Votre image de machine virtuelle doit être certifié toobe envoyée toostaging.

## <a name="step-1-push-your-offer-toostaging"></a>Étape 1 : Push toostaging de votre offre
1. Sur hello **publier** , cliquez sur **Push tooStaging**.
   
    ![dessin](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. Si le portail de publication de hello vous avertit de toutes les erreurs, corrigez-les.
3. Bonjour **qui peut accéder à votre offre intermédiaire ?** boîte de dialogue, entrez la liste hello des abonnements Azure que vous allez utiliser toopreview votre offre Bonjour [portail Azure preview](https://portal.azure.com).
   
   > [!NOTE]
   > Dans le cas de machines virtuelles et de modèles de solutions, veuillez **ne pas** mettre sur liste approuvée des abonnements de type CSP, DreamSpark ou Azure dans Open.
   > 
   > 

    > En cas de Machines virtuelles, lorsque vous cliquez sur le bouton de hello **PUSH tooSTAGING**, effectuée derrière la scène de hello hello comme suit. Vous serez tooview en mesure de hello progression de chaque étape sous l’onglet Publier de hello Bonjour portail de publication. Vous devez vérifier cette page à intervalle régulier (jusqu'à ce que l’état de hello affiche intermédiaire) pour toutes les informations d’échec qui ont besoin de correction à partir de votre principal.

    > - Dans un premier temps votre demande de mise en lots passe équipe certification toohello est chargée de valider le disque dur virtuel hello. Toutefois, si votre demande a marketing uniquement les modifications, puis hello certification étape est ignorée.
    > - Une fois la certification de hello est terminée, la réplication de début offre de hello pour tous les hello centres de données Azure. En règle générale, il prend 24-48hours pour hello réplication toocomplete mais peut prendre jusqu'à une semaine tooa selon la taille de hello du disque dur virtuel hello. Toutefois, si votre demande a marketing uniquement les modifications, la réplication hello est plus rapide.
    > - Lorsque la réplication hello est terminée, puis hello offre sera disponible dans hello [portail Azure](http:/portal.azure.com). À ce hello temps état deviennent intermédiaire Bonjour portail de publication. Une offre intermédiaire est visible dans hello [portail Azure](http:/portal.azure.com) uniquement à l’aide d’identificateurs de messagerie hello associés abonnement hello avec quels hello offre soit préparée.

1. Connectez-vous à toohello [portail Azure preview](https://portal.azure.com) à l’aide d’une des hello abonnements Azure sont répertoriés à l’étape précédente de hello.
2. Recherchez votre offre et validez vos points d'image de machine virtuelle :
   
   * Assurez-vous que le contenu de marketing s’affiche correctement Bonjour Marketplace.
   * Déploiement de bout en bout de l’image de machine virtuelle hello.
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> Votre offre restent dans la mise en lots jusqu'à ce que vous informer Microsoft via le portail de publication de hello [**publier** onglet > cliquez sur le bouton de hello **« Demander l’approbation tooPush tooProduction »**] que vous êtes prêt toopush tooproduction. Il s’agit d’un toohave moment idéal tous les membres de votre équipe vérifier sur tous les éléments de la préparation de votre offre va répertoriées.
> 
> Hello plate-forme intermédiaire est conçu pour test offre hello dans un mode Aperçu par le serveur de publication hello. Nous déconseillons fortement d’utiliser cette plateforme à des fins commerciales.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Maintenant que votre offre est « intermédiaire » et que vous avez testé ses fonctionnalités et contenu commercial, vous pouvez procéder à la publication finale toohello phase, **étape 4**: [déploiement votre toohello offre Marketplace](marketplace-publishing-push-to-production.md).

## <a name="see-also"></a>Voir aussi
* [Mise en route : comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md)

