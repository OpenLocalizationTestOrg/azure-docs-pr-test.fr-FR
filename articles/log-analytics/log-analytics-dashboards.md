---
title: "aaaCreate un tableau de bord personnalisé dans Azure journal Analytique | Documents Microsoft"
description: "Ce guide vous aide à comprendre comment les tableaux de bord Analytique de journal peuvent de visualiser toutes vos recherches enregistrées de journal, ce qui vous donne un seul objectif tooview votre environnement."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Créer un tableau de bord personnalisé à utiliser dans Log Analytics

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis vous ne pouvez pas créer de nouveaux tableaux de bord ou modifier des tableaux de bord existants. 

Ce guide vous aide à comprendre comment les tableaux de bord Analytique de journal peuvent de visualiser toutes vos recherches enregistrées de journal, ce qui vous donne un seul objectif tooview votre environnement.

![Exemple de tableau de bord](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

Tous les hello tableaux de bord personnalisés que vous créez dans le portail OMS de hello est également disponibles dans hello application Mobile OMS. Consultez hello suivant pages pour plus d’informations sur les applications de hello.

* [Application mobile OMS à partir de hello Microsoft Store](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [Application mobile OMS d’Apple iTunes](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![Tableau de bord mobile](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>Comment créer un tableau de bord ?
toobegin, page de vue d’ensemble d’OMS toohello accédez. Vous verrez hello **mon tableau de bord** vignette sur hello gauche. Cliquez dessus toodrill vers le bas dans votre tableau de bord.

![Vue d'ensemble](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>Ajout d'une vignette
Dans les tableaux de bord, les vignettes sont alimentées par vos recherches de journal enregistrées. OMS propose un grand nombre de recherches enregistrées de journal prédéfinies qui vous permettent de commencer tout de suite. Ce plan de la façon dont étapes suivantes de hello utilisation toobegin.

Bonjour mon tableau de bord, cliquez simplement sur **personnaliser** tooenter en mode de personnalisation.

![Représentation graphique](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 panneau Hello qui s’ouvre sur le côté droit de hello de page de hello montre toutes les recherches de journal enregistrées de votre espace de travail. toovisualize recherche d’un journal enregistré sous forme de vignette, placez le curseur sur une recherche enregistrée, puis cliquez sur hello **plus** symbole.

![Ajout de vignettes 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

Lorsque vous cliquez sur hello **plus** symbol, une nouvelle vignette s’affiche dans hello mon tableau de bord.

![Ajout de vignettes 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>Modification d'une vignette
Bonjour mon tableau de bord, cliquez simplement sur **personnaliser** tooenter en mode de personnalisation. Cliquez sur vignette hello tooedit. le panneau droit Hello modifie tooedit et propose diverses options :

![Modification d'une vignette](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Modification d'une vignette](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>Visualisations de vignettes
Il existe trois types de toochoose de visualisations de vignette à partir de :

| type de graphique | résultat |
| --- | --- |
| ![Graphique à barres](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |Affiche une chronologie des résultats de vos recherches de journal enregistrées sous forme de graphique à barres, ou une liste de résultats en fonction d’un champ, selon que votre recherche de journal regroupe les résultats par champ ou non. |
| ![métrique](./media/log-analytics-dashboards/oms-dashboards-metric.png) |Affiche le nombre total d'accès à vos résultats de recherche de journal sous la forme d'un nombre dans une vignette. Vignettes de métrique vous permettent de tooset un seuil qui met en surbrillance la vignette de hello lorsque hello seuil est atteint. |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |Affiche une chronologie de vos résultats de recherche journal enregistrés, avec des valeurs représentées sous la forme d’un graphique en courbes. |

### <a name="threshold"></a>Seuil
Vous pouvez créer un seuil sur une vignette à l’aide de la visualisation métrique de hello. Sélectionnez une valeur de seuil sur la vignette de hello sur toocreate. Choisissez si vignette de hello toohighlight lorsque la valeur de hello est supérieure ou inférieure hello choisi seuil, puis valeur hello seuil ci-dessous.

## <a name="organizing-hello-dashboard"></a>Organisation hello le tableau de bord
tooorganize votre tableau de bord, naviguer dans Affichage de mon tableau de bord toohello et cliquez sur **personnaliser** tooenter en mode de personnalisation. Cliquez et faites glisser vignette hello souhaité toomove, déplacez-le toowhere vous souhaitez que votre toobe de vignette.

![Organisation de votre tableau de bord](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>Suppression d'une vignette
tooremove une vignette, accédez vue mon tableau de bord de toohello et cliquez sur **personnaliser** tooenter en mode de personnalisation. Vignette hello sélectionnez vous souhaitez tooremove, puis sur Panneau de droite hello **supprimer une vignette**.

![Suppression d'une vignette](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>Étapes suivantes
* Créer [alertes](log-analytics-alerts.md) dans les notifications toogenerate Analytique de journal et des problèmes de tooremediate.
