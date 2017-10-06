---
title: aaaUnderstand votre facture Azure | Documents Microsoft
description: "Découvrez comment tooread et comprendre votre utilisation et facturation pour votre abonnement Azure"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>Comprendre votre facture Microsoft Azure
toounderstand votre Azure facturer, comparez votre facture avec le fichier d’utilisation quotidienne détaillées hello et hello Bonjour portail Azure, les rapports de gestion des coûts.

tooobtain un fichier PDF de votre facture et une copie de votre détaillées quotidien d’utilisation CSV téléchargement du fichier, consultez [obtenir votre facture et tous les jours les données d’utilisation de la facturation de Azure](billing-download-azure-invoice-daily-usage-date.md). 

Pour les termes et descriptions détaillés de votre facture et de votre fichier détaillé sur l’utilisation quotidienne, consultez [Comprendre les termes indiqués sur votre facture Microsoft Azure](billing-understand-your-invoice.md) et [Comprendre les termes indiqués sur le fichier Microsoft Azure sur l’utilisation détaillée](billing-understand-your-usage.md). 

Pour plus d’informations sur hello coût des rapports de gestion, consultez [gestion des coûts Azure portal](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started).


## <a name="charges"></a>Comment m’assurer que les frais de hello dans ma facture sont corrects ?
Si vous voulez plus de détails sur des frais indiqués sur votre facture, vous disposez de deux options.

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>Option 1 : Passez en revue votre facture et comparer les coûts et l’utilisation de hello hello détaillée fichier CSV de l’utilisation

Hello un fichier CSV d’utilisation détaillées affiche vos frais par période de facturation et de l’utilisation quotidienne. reportez-vous à votre fichier CSV, d’utilisation détaillée tooget [obtenir votre facture et tous les jours les données d’utilisation de la facturation de Azure](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date).

Vos frais d’utilisation sont affichés au niveau de compteur hello. Hello signification des termes suivants hello identiques dans les deux facture hello et hello fichier détaillées d’utilisation. Par exemple, hello cycle de facture de hello de facturation est période de facturation toohello équivalent indiqué dans le fichier d’utilisation détaillées de hello.

 | Facture (PDF) | Utilisation détaillée (CSV)|
 | --- | --- |
|Cycle de facturation | Période de facturation |
 |Nom |Catégorie du compteur |
 |Type |Sous-catégorie du compteur |
 |Ressource |Nom du compteur |
 |Région |Région du compteur |
 |Consommé |Quantité consommée |
 |Inclus |Quantité incluse |
 |Facturable |Quantité de dépassement |

Hello **frais d’utilisation** section de votre facture a la valeur totale de hello pour chaque compteur qui a été consommée pendant la période de facturation. Par exemple, hello capture d’écran suivante montre un coût d’utilisation hello service Azure Scheduler.

![Frais d’utilisation indiqués sur la facture](./media/billing-understand-your-bill/1.png)

Hello **instruction** section de votre utilisation détaillée de volume partagé de cluster affiche hello même frais. Les deux hello *consommé* montant et *valeur* correspondance hello facture.

![Frais d’utilisation sur le fichier CSV](./media/billing-understand-your-bill/2.png)

toosee une répartition de ces frais sur une base quotidienne, accédez toohello **l’utilisation quotidienne** section Hello CSV. Filtrer pour « Planificateur » sous *catégorie de compteur* et vous pouvez consulter le compteur de hello jours a été utilisé et la quantité a été consommée. Hello *ressource* et *groupe de ressources* informations sont également répertoriées pour la comparaison. Hello *consommé* valeurs doivent additionner de toowhat indiqué sur la facture de hello.

![Section d’utilisation quotidienne Bonjour CSV](./media/billing-understand-your-bill/3.png)

coût de hello tooget par jour, multipliez hello *consommé* montants hello *taux* valeur hello **instruction** section.

toolearn en savoir plus sur la facture de hello, consultez [comprendre votre facture Azure](billing-understand-your-invoice.md).

toolearn sur chacune des colonnes hello Bonjour CSV, consultez [comprendre votre utilisation détaillée Azure](billing-understand-your-invoice.md).

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>Option 2 : Passez en revue votre facture et comparer à l’utilisation de hello et les coûts Bonjour portail Azure

Hello portail Azure peut également vous aider à vérifier vos frais. Hello portail Azure fournit des graphiques de gestion de coût pour une vue d’ensemble rapide de vos frais d’utilisation et hello sur votre facture.

toocontinue avec l’exemple hello ci-dessus, visitez hello [page abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), sélectionnez votre abonnement, puis sélectionnez **analyse coût**. À partir de là, vous pouvez spécifier les hello-intervalle de temps et voir les frais de l’utilisation de service d’Azure Scheduler hello.

![Vue de l’analyse des coûts dans le portail Azure](./media/billing-understand-your-bill/4.png)

analyse quotidienne des coûts toosee hello dans **coût historique**, cliquez sur la ligne hello.

![Affichage de l’historique des coûts dans le portail Azure](./media/billing-understand-your-bill/5.png)

toolearn, voir [empêcher les coûts inattendus avec la gestion des coûts et la facturation Azure](billing-getting-started.md#costs).

## <a name="external"></a>Quels sont les frais associés aux services externes ?
Les services externes (également appelés commandes de la Place de marché Microsoft Azure) sont fournis par les fournisseurs de services indépendants et sont facturés séparément. frais de Hello n’apparaissent pas sur votre facture Azure. toolearn, voir [comprendre vos frais de service externes Azure](billing-understand-your-azure-marketplace-charges.md).

## <a name="payment"></a>Comment effectuer un paiement ?

Si vous configurez une carte de crédit ou une carte bancaire comme mode de paiement, le paiement de hello est facturé automatiquement dans les 10 jours après la fin de la période de facturation hello. Sur votre relevé de carte de crédit, élément de ligne hello serait dire **MSFT Azure**.

Si vous [payer par facturation](billing-how-to-pay-by-invoice.md), envoyer votre emplacement toohello de paiement répertoriée au bas de hello de votre facture. Pour plus d’informations, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>Comment vérifier le statut de hello d’un paiement par carte de crédit ?

[Créer un ticket de support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooask statut hello de votre paiement. 

## <a name="tips-for-cost-management"></a>Conseils pour la gestion des coûts
- Estimer les coûts à l’aide de hello [calculatrice de prix](https://azure.microsoft.com/pricing/calculator/) et [coût total de l’outil de calcul de la propriété](https://aka.ms/azure-tco-calculator)et obtenir hello [détaillées des informations de tarification pour chaque service](https://azure.microsoft.com/en-us/pricing/).
- [Configurez des alertes de facturation](billing-set-up-alerts.md).
- [Examinez votre utilisation et coûts régulièrement à hello Azure portal](billing-getting-started.md#costs).

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.

Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
