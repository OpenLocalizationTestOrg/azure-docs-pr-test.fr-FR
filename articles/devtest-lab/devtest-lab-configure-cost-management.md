---
title: "aaaView hello mensuelles estimé du lab tendance du coût dans Azure DevTest Labs | Documents Microsoft"
description: "En savoir plus sur le graphique de tendances de coût estimé mensuel hello Azure DevTest Labs."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a>Vue hello mensuelles estimé du lab tendance du coût dans Azure DevTest Labs
fonctionnalité de gestion des coûts Hello de DevTest Labs permet de suivre le coût de hello de votre laboratoire. Cet article explique comment toouse hello **tendance du coût estimé mensuel** graphique tooview hello estimé coût-to-date du mois civil actuel et hello coût prévu de fin de mois pour hello mois actuel. Dans cet article, vous découvrez comment tooview hello graphique de tendances de coût estimé mensuel Bonjour portail Azure.

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a>Affichage graphique de tendance du coût estimé mensuel hello
tooview hello graphique de tendance du coût estimé mensuel, procédez comme suit : 

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
3. Dans liste hello labs, sélectionnez lab souhaité de hello.   
4. Dans le panneau de hello lab, sélectionnez **paramètres de coût**.
5. Sur du laboratoire hello **coût paramètres** panneau, sélectionnez **tendance du coût Lab**.
6. Hello capture d’écran suivante montre un exemple d’un graphique de coût. 
   
    ![Graphique de coûts](./media/devtest-lab-configure-cost-management/graph.png)

Hello **coût estimé** valeur est hello estimé coût-to-date du mois civil actuel. Hello **coût prévu** est hello coût estimé de hello entière mois actuel, calculée à l’aide coût de laboratoire hello pour hello précédentes cinq jours.

montants de coût Hello sont arrondis toohello nombre entier supérieur. Par exemple : 

* 5.01 arrondit too6 
* 5.50 arrondit too6
* 5.99 arrondit too6

Comme il indique au-dessus du graphique de hello, les coûts de hello vous voyez dans le graphique de hello sont *estimé* coûte à l’aide de [paiement à l’utilisation](https://azure.microsoft.com/offers/ms-azr-0003p/) offrent des taux.
En outre, hello Voici les *pas* inclus dans le calcul du coût de hello :

* Abonnements CSP et Dreamspark sont actuellement pas prises en charge Azure DevTest Labs utilise hello [API facturation Azure](../billing/billing-usage-rate-card-overview.md) lab de hello toocalculate coût, qui ne prend pas en charge les abonnements Dreamspark ou de fournisseur de services cryptographiques.
* Les tarifs de votre offre. Actuellement, nous ne sommes pas en mesure de toouse vos tarifs offre (affichées sous votre abonnement) que vous avez négocié avec Microsoft ou Microsoft partenaires. Nous utilisons les tarifs du paiement à l'utilisation.
* Vos taxes
* Vos remises
* Votre devise de facturation. Coût de laboratoire hello est affichée uniquement dans la devise USD.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Billets de blog connexes
* [Deux tookeep choses plus votre coût de la piste dans DevTest Labs](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [Why Cost Thresholds? (Pourquoi définir des seuils de coût ?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a>Étapes suivantes
Voici certaines choses tootry suivant :

* [Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md) -en savoir comment tooset hello différentes stratégies de toogovern comment votre laboratoire et ses ordinateurs virtuels sont utilisés. 
* [Créer une image personnalisée](devtest-lab-create-template.md) : quand vous créez une machine virtuelle, vous spécifiez une base, qui peut être soit une image personnalisée, soit une image Marketplace. Cet article explique comment toocreate personnalisé de l’image à partir d’un fichier de disque dur virtuel.
* [Configurer des images Marketplace](devtest-lab-configure-marketplace-images.md) : DevTest Labs prend en charge la création de machines virtuelles basées sur des images Azure Marketplace. Cet article explique comment toospecify qui, le cas échéant, les images Azure Marketplace peuvent être utilisés lors de la création de machines virtuelles dans un laboratoire.
* [Créer une machine virtuelle dans un laboratoire](devtest-lab-add-vm-with-artifacts.md) -illustre comment toocreate une machine virtuelle à partir d’une image de base (soit personnalisé ou Marketplace) et comment toowork des artefacts dans votre machine virtuelle.

