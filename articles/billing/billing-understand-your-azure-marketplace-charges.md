---
title: aaaUnderstand vos frais de service externes Azure | Documents Microsoft
description: "En savoir plus sur la facturation des frais des services externes, anciennement appelés Marketplace, dans Azure."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a>Présentation de la facturation de vos frais de service externe Azure
Les services externes utilisés toobe appelé Azure Marketplace. En règle générale, il s’agit de services publiés par des tiers et disponibles pour Azure, qui sont complètement intégrés à Azure. Par exemple, ClearDB et SendGrid sont des services externes que vous pouvez acheter dans Azure, mais ils ne sont pas publiés par Microsoft.

Lorsque vous configurez un nouveau service externe ou une ressource, un avertissement s’affiche :

![Avertissement d’achat Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> Les services externes sont publiés par des entreprises autres que Microsoft, mais parfois des produits Microsoft sont également classés en tant que services externes.
> 
> 

## <a name="how-external-services-are-billed"></a>Facturation des services externes
- Les services externes sont facturés séparément. Ils sont traités comme des commandes individuelles au sein de votre abonnement Azure. période de facturation Hello pour chaque service est définie lorsque vous achetez le service de hello. Pas toobe peut être confondue avec la période de facturation hello d’abonnement hello sous lequel vous l’avez achetée. Vous recevez également des factures distinctes et votre carte de crédit est facturée séparément.
- Chaque service externe possède un modèle de facturation différent. Certains services sont facturés selon un mode de paiement à l’utilisation, tandis que d’autres utilisent un modèle de paiement mensuel. Les services externes Azure nécessitent une carte de crédit. Vous ne pouvez pas acheter des services externes avec un paiement par facture.
- Vous ne pouvez pas utiliser de crédits mensuels gratuits pour les services externes. Si vous utilisez un abonnement Azure qui inclut [libre crédits](https://azure.microsoft.com/pricing/spending-limits/), ils ne peut pas être appliqué tooexternal service factures. Utiliser une carte de crédit toopurchase des services externes.


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a>Afficher les dépenses service externe et l’historique dans hello portail Azure
Vous pouvez afficher la liste des services externes hello qui se trouvent sur chaque abonnement dans hello [portail Azure](https://portal.azure.com/): 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) en tant qu’administrateur de compte hello.
2. Dans le menu du Hub hello, sélectionnez **abonnements**.
   
    ![Sélectionnez les abonnements dans le menu du Hub hello](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. Bonjour **abonnements** panneau, abonnement hello select que vous souhaitez tooview, puis sélectionnez **services externes**.
   
    ![Sélectionnez un abonnement dans le panneau de facturation hello](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. Vous devez voir chacune de vos commandes de service externe, hello publisher, niveau de service que vous avez acheté, nom attribué hello ressource et état actuel de la commande hello. toosee dernières factures, sélectionnez un service externe.
   
    ![Sélectionnez un service externe](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. À ce stade, vous pouvez afficher au-delà des montants de facture, y compris la répartition des taxes hello.
   
    ![Afficher l’historique de facturation des services externes](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a>Afficher les dépenses du service externe pour les clients de contrat Entreprise (EA)
Les clients EA peuvent voir les dépenses de service externe et télécharger des rapports dans le portail EA hello. Consultez [Azure Marketplace pour les clients EA](https://ea.azure.com/helpdocs/azureMarketplace) tooget a démarré.

## <a name="manage-payment-methods-for-external-service-orders"></a>Gérer les modes de paiement pour les commandes de service externe
Mettre à jour vos modes de paiement pour les commandes de service externe à partir de hello [centre des comptes](https://account.windowsazure.com/).

> [!NOTE]
> Si vous avez acheté votre abonnement avec un compte professionnel ou scolaire, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake modifie le mode de paiement tooyour.
> 
> 

1. Connectez-vous à toohello [centre des comptes](https://account.windowsazure.com/) et [accédez toohello **marketplace** onglet](https://account.windowsazure.com/Store)
   
    ![Sélectionnez marketplace dans le centre des comptes hello](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. Sélectionnez hello externe service toomanage
   
    ![Sélectionnez hello externe service toomanage](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. Cliquez sur **modifier le mode de paiement** sur le côté droit de hello de page de hello. Ce lien permet d’accéder vous tooa autre portail toomanage votre mode de paiement.
   
    ![Résumé de la commande](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. Cliquez sur **modifier les informations** et suivez les instructions tooupdate vos informations de paiement.
   
    ![Sélectionnez Modifier les informations](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a>Annuler une commande de service externe
Si vous souhaitez toocancel votre commande de service externe, supprimer la ressource de hello Bonjour [portail Azure](https://portal.azure.com).

![Supprimer la ressource](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez des questions, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.

