---
title: aaaPlans et facturation dans Azure Scheduler
description: Plans et facturation dans Azure Scheduler
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 13a2be8c-dc14-46cc-ab7d-5075bfd4d724
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 051b8eeb1ea19678b3cef4db3237ebf04c8b0e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a>Plans et facturation dans Azure Scheduler
## <a name="job-collection-plans"></a>Plans de collections de travaux
Collections de travaux sont des entités facturables de hello dans Azure Scheduler. Les collections de travaux contiennent plusieurs travaux et se présentent en trois modes (Gratuit, Standard et Premium) décrits ci-dessous.

| **Plan de collection de travaux** | **Nombre maximal de travaux par Collection de travaux** | **Périodicité maximale** | **Collections de travail max. par abonnement** | **Limites** |
|:--- |:--- |:--- |:--- |:--- |
| **Gratuit** |5 travaux par collection |Une fois par heure. Ne peut pas exécuter des travaux plus souvent qu'une fois par heure |Un abonnement est autorisé d’une collection de travaux gratuite too1 |Impossible d'utiliser un [objet d'autorisation sortante HTTP](scheduler-outbound-authentication.md) |
| **Standard** |50 travaux par collection |Une fois par minute. Ne peut pas exécuter des travaux plus souvent qu'une fois par minute |Un abonnement est autorisé des collections de travaux standard too100 |Ensemble de fonctionnalités accès toofull du planificateur |
| **P10 Premium** |50 travaux par collection |Une fois par minute. Ne peut pas exécuter des travaux plus souvent qu'une fois par minute |Un abonnement est autorisé des too10, 000 collections de travaux P10 Premium. Pour augmenter cette limite, <a href="mailto:wapteams@microsoft.com">contactez-nous</a>. |Ensemble de fonctionnalités accès toofull du planificateur |
| **P20 Premium** |1000 travaux par collection |Une fois par minute. Ne peut pas exécuter des travaux plus souvent qu'une fois par minute |Un abonnement est autorisé des too10, 000 collections de travaux P20 Premium. Pour augmenter cette limite, <a href="mailto:wapteams@microsoft.com">contactez-nous</a>. |Ensemble de fonctionnalités accès toofull du planificateur |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a>Mises à niveau et versions antérieures des Plans de collections de travaux
Vous pouvez mettre à niveau ou rétrograder un plan de la collection de travail à tout moment entre les plans de hello gratuit, Standard et Premium. Toutefois, lorsque vous rétrogradez la collection de travaux gratuite tooa, vers une version antérieure de hello peut échouer pour l’une des hello suivant raisons :

* Une collection de travaux gratuite déjà existe dans l’abonnement de hello
* Un travail dans la collection de tâches hello présente une récurrence plus élevée que la longueur autorisée pour les projets de collections de travaux gratuite. récurrence maximale de Hello autorisé dans une collection de travaux gratuite est une fois par heure
* Il existe plus de 5 tâches dans la collection de tâches hello
* Un travail de collection de tâches hello a une action HTTP ou HTTPS qui utilise un [objet sortant d’autorisation de HTTP](scheduler-outbound-authentication.md)

## <a name="billing-and-azure-plans"></a>Facturation et plans Azure
Les abonnements ne sont pas facturés pour les collections de travaux gratuites. Si vous avez plus de 100 collections de travaux standard (10 facturation unités standard), il s’agit d’un toohave offre une meilleure toutes les collections de travaux dans le plan de hello premium.

Si vous disposez d’une collection de travaux Standard et d’une collection de travaux Premium, une unité de facturation standard *et* une unité de facturation premium vous sont facturées. opérations de service de planificateur Hello en fonction du nombre de hello des collections de travail actif sont définies tooeither standard ou premium ; Cela est expliqué plus loin dans hello deux sections suivantes.

## <a name="standard-billable-units"></a>Unités facturables standard
Une unité facturable standard peut inclure des collections de travaux standard too10. Comme une collection de travaux standard peut avoir de travaux too50 par collection de tâches, une unité de facturation standard permet un toohave d’abonnement de travaux too500 – des exécutions des travaux tooalmost 22 millions par mois.

Si vous avez entre 1 et 10 collections de travaux standard, vous serez facturé pour 1 unité de facturation standard. Si vous avez entre 11 et 20 collections de travaux standard, vous serez facturé pour 2 unités de facturation standard. Si vous avez entre 21 et 30 collections de travaux standard, vous serez facturé pour 3 unités de facturation standard, et ainsi de suite.

## <a name="p10-premium-billable-units"></a>Unités facturables P10 Premium
Une unité de facturables premium P10 peut inclure des too10, les collections de travaux premium P10 000. Comme une collection de travaux premium P10 peut avoir de travaux too50 par collection de tâches, une unité de facturation premium permet un toohave abonnement des too500, 000 travaux – des exécutions des travaux tooalmost 22 milliards par mois.

Si vous avez entre 1 et 10 000 collections de travaux premium, vous serez facturé pour 1 unité de facturation P10 Premium. Si vous avez entre 10 001 et 20 000 collections de travaux premium, vous serez facturé pour 2 unité de facturation P10 Premium, et ainsi de suite.

Par conséquent, la tâche premium P10 collections ont hello même fonctionnalité que les collections de travaux standard de hello fournissent, mais une rupture de prix au cas où votre application nécessite un grand nombre de collections de travaux.

## <a name="p20-premium-billable-units"></a>Unités facturables P20 Premium
Une unité de facturables premium P20 peut inclure des too5, les collections de travaux premium P20 000. Comme une collection de travaux premium P20 peut avoir des too1, 000 travaux par collection de tâches, une unité de facturation premium permet un toohave abonnement des too5, 000 000 tâches – des exécutions des travaux milliards de 220 tooalmost par mois.

Collections de travaux premium P20 fournit des mêmes fonctionnalités que les collections de travaux premium P10 hello mais prend également en charge un travaux numéro supérieur par collection de tâches et un plus grand nombre total de travaux globale que P10 premium permettant vous toohave plus grande.

## <a name="billing-and-active-status"></a>Facturation et état Actif
Collections de tâches sont toujours actives, sauf si votre abonnement entier a été mis à un état temporaire désactivé en raison de problèmes de toobilling. Bonjour tooensure de manière seulement une collection de travaux n’est pas facturée est toohello définissez-le tooeither *libre* plan ou toodelete collection de travaux hello.

Bien que vous pouvez désactiver tous les travaux au sein d’une collection de tâches en une seule opération, il ne modifie pas le statut de la facturation hello de collection de travaux hello : collection de travaux hello sera *toujours* facturé. De même, les collections de travaux vides sont considérées comme actives et seront facturées.

## <a name="pricing"></a>Tarification
Pour plus d’informations sur la tarification, voir l’article [Tarification d’Azure Scheduler](https://azure.microsoft.com/pricing/details/scheduler/).

## <a name="see-also"></a>Voir aussi
 [Présentation d'Azure Scheduler](scheduler-intro.md)

 [Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler](scheduler-concepts-terms.md)

 [Prise en main du planificateur Bonjour portail Azure](scheduler-get-started-portal.md)

 [Informations de référence sur l’API REST d’Azure Scheluler](https://msdn.microsoft.com/library/mt629143)

 [Informations de référence sur les applets de commande PowerShell d’Azure Scheluler](scheduler-powershell-reference.md)

 [Haute disponibilité et fiabilité d’Azure Scheluler](scheduler-high-availability-reliability.md)

 [Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler](scheduler-limits-defaults-errors.md)

 [Authentification sortante d’Azure Scheluler](scheduler-outbound-authentication.md)

