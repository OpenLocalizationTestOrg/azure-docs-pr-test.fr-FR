---
title: "recommandations de coût de l’Assistant aaaAzure | Documents Microsoft"
description: "Utilisez l’Assistant Azure toooptimize hello coût de vos déploiements Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Recommandations en matière de coûts du conseiller

Le conseiller vous aide à optimiser et à réduire votre dépense Azure globale en identifiant les ressources inactives et sous-utilisées. Vous pouvez extraire les coûts recommandations de hello **coût** onglet tableau de bord de conseiller hello.

![Onglet Coût dans Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>Optimiser le coût de la machine virtuelle en redimensionnant les instances sous-utilisées 
Bien que certains scénarios d’application peuvent entraîner une utilisation faible par sa conception, vous pouvez souvent économies grâce à la gestion de la taille de hello et le nombre de vos ordinateurs virtuels. Advisor surveille l’utilisation de votre machine virtuelle pendant 14 jours et identifie les machines virtuelles faiblement utilisées. Les machines virtuelles dont l’utilisation du processeur est inférieure ou égale à 5 % et celle du réseau est inférieure ou égale à 7 Mo pendant quatre jours ou plus sont considérées comme des machines virtuelles faiblement utilisées.

Affiche l’Assistant vous hello coût estimé de continuer toorun votre machine virtuelle, afin que vous puissiez choisir tooshut vers le bas ou le redimensionner.  

![Recommandations de coûts du conseiller pour le redimensionnement des machines virtuelles](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>Utiliser un objectifs de performances toomanage solution économique de plusieurs bases de données SQL
Le conseiller identifie les instances de serveur SQL pouvant bénéficier de la création de pools de bases de données élastiques. Pools de bases de données élastiques fournissent une solution simple et économique de toomanage des objectifs de performances hello de plusieurs bases de données qui ont des modèles d’utilisation. Pour plus d’informations sur les pools élastiques Azure, consultez la page [Qu’est-ce qu’un pool élastique Azure ?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).

![Recommandations de coût du conseiller pour les pools de bases de données élastiques](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Comment tooaccess coût recommandations dans l’Assistant d’Azure

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Dans le volet gauche de hello, cliquez sur **davantage de services**.

3. Bonjour service sous le volet de menu, **analyse et gestion**, cliquez sur **Azure Advisor**.  
 tableau de bord Hello Advisor s’affiche.

4. Tableau de bord du conseiller hello, cliquez sur hello **coût** onglet.

5. Sélectionnez l’abonnement hello pour lequel vous souhaitez que les recommandations tooreceive, puis cliquez sur **obtenir des recommandations**.

> [!NOTE]
> tooaccess recommandations de l’Assistant, vous devez d’abord *enregistrer votre abonnement* avec l’Assistant. Un abonnement est enregistré quand un *abonnement propriétaire* lance hello hello de tableau de bord et clique sur Advisor **obtenir des recommandations** bouton. Cette opération ne doit être *exécutée qu’une seule fois*. Une fois l’abonnement de hello est enregistré, vous pouvez accéder à des recommandations de l’Assistant en tant que *propriétaire*, *collaborateur*, ou *lecteur* pour un abonnement, un groupe de ressources, ou un ressource spécifique.

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les recommandations de l’Assistant, consultez :
* [Introduction tooAdvisor](advisor-overview.md)
* [Prise en main](advisor-get-started.md)
* [Recommandations du conseiller en matière de performances](advisor-cost-recommendations.md)
* [Recommandations du conseiller en matière de haute disponibilité](advisor-cost-recommendations.md)
* [Recommandations du conseiller en matière de sécurité](advisor-cost-recommendations.md)
