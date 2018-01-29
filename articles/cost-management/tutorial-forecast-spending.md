---
title: "Prévoir les dépenses avec la Gestion des coûts Azure | Microsoft Docs"
description: "Prévoyez les dépenses à l’aide de l’historique d’utilisation et des données de dépenses."
services: cost-management
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 10/11/2017
ms.topic: tutorial
ms.service: cost-management
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: d8b0cd2a3e5f9829f0844783aad22d375eb9d7a8
ms.sourcegitcommit: 0930aabc3ede63240f60c2c61baa88ac6576c508
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2017
---
# <a name="forecast-future-spending"></a>Prévoir les dépenses futures

La Gestion des coûts Azure par Cloudyn vous permet de prévoir les futures dépenses à l’aide de l’historique d’utilisation et des données de dépenses. Les rapports Cloudyn vous permettent d’afficher toutes les données de projection des coûts. Les exemples de ce didacticiel vous guident tout au long de l’étude des projections de coûts à l’aide de rapports. Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Prévoir les dépenses futures

## <a name="forecast-future-spending"></a>Prévoir les dépenses futures

Cloudyn inclut des rapports de prévision des coûts pour vous aider à prévoir les dépenses au fil du temps, en fonction de votre utilisation. Ces rapports vous aident principalement à vous assurer que vos tendances de coûts n’excèdent pas les attentes de votre organisation. Vous utilisez un rapport du coût projeté pour le mois en cours (Current Month Projected Cost) et un rapport du coût projeté annuel (Annual Projected Cost). Ces deux rapports indiquent les dépenses futures projetées si votre utilisation reste relativement cohérente durant vos 30 derniers jours d’utilisation.

Le rapport du coût projeté pour le mois en cours affiche les coûts de vos services. Il prend en compte les coûts depuis le début du mois en cours et du mois précédent pour afficher le coût projeté. Dans le menu des rapports en haut du portail, cliquez sur **Cost** > **Projection and Budget** > **Current Month Projected Cost**. L’image suivante en montre un exemple.

![coût projeté pour le mois en cours](./media/tutorial-forecast-spending/project-month01.png)

Dans l’exemple, vous pouvez voir les services qui ont le plus dépensé. Les coûts Azure sont inférieurs aux coûts AWS. Si vous souhaitez afficher les détails de la projection des coûts pour les machines virtuelles Azure, dans la liste **Filter**, sélectionnez **Azure/VM**.

![Coût projeté des machines virtuelles Azure pour le mois en cours](./media/tutorial-forecast-spending/project-month02.png)

Suivez les mêmes étapes précédentes pour examiner les projections de coûts mensuels d’autres services qui vous intéressent.

Le rapport du coût projeté annuel (Annual Projected Cost) affiche le coût extrapolé de vos services pour les 12 prochains mois.

Dans le menu des rapports en haut du portail, cliquez sur **Cost** > **Projection and Budget** > **Annual Projected Cost**. L’image suivante en montre un exemple.

![rapport du coût projeté annuel](./media/tutorial-forecast-spending/project-annual01.png)

Dans l’exemple, vous pouvez voir les services qui ont le plus dépensé. Comme pour l’exemple mensuel, les coûts Azure ont été inférieurs aux coûts AWS. Si vous souhaitez afficher les détails de la projection des coûts pour les machines virtuelles Azure, dans la liste **Filter**, sélectionnez **Azure/VM**.

![coût projeté annuel des machines virtuelles](./media/tutorial-forecast-spending/project-annual02.png)

Dans l’image ci-dessus, le coût projeté annuel des machines virtuelles Azure est de 28 374 USD.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Prévoir les dépenses futures


Passez au didacticiel suivant pour découvrir comment gérer les coûts avec les rapports de facturation et d’allocation des coûts.

> [!div class="nextstepaction"]
> [Gérer les coûts grâce à des rapports de facturation et d’allocation des coûts](tutorial-manage-costs.md)
