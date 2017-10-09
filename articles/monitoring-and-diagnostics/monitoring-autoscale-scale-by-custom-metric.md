---
title: "aaaGet démarrée avec l’échelle automatique par métrique personnalisée dans Azure | Documents Microsoft"
description: "Découvrez comment tooscale votre ressource en fonction de la métrique personnalisée dans Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Prise en main de la mise à l’échelle automatique par métrique personnalisée dans Azure
Cet article décrit comment tooscale votre ressource par une métrique personnalisée dans le portail Azure.

Azure à l’échelle automatique analyse s’applique uniquement tooVirtual jeux de mise à l’échelle de Machine (mise), services de cloud computing, les plans de service d’application et les environnements app service. 

# <a name="lets-get-started"></a>Prise en main
Cet article suppose que vous disposez d’une application web avec Application Insights déjà configuré. Si vous ne l’avez pas encore fait, vous pouvez [configurer Application Insights pour votre site web ASP.NET][1]

- Ouvrez le [portail Azure][2]
- Cliquez sur l’icône Azure dans le volet de navigation gauche hello.
  ![Lancer Azure Monitor][3]
- Cliquez sur l’échelle automatique de la définition de toutes les ressources hello pour l’automatiquement mise à l’échelle est applicable, ainsi que son état actuel de la mise à l’échelle tooview ![découvrir à l’échelle automatique dans le moniteur de Azure][4]
- Ouvrir le panneau 'd’échelle automatique' dans le moniteur de Azure et sélectionnez une ressource tooscale
> Remarque : des étapes de hello ci-dessous utilisent un plan de service d’application associé à une application web qui a des aperçus d’application configurés.
- Dans le panneau de configuration hello mise à l’échelle pour la ressource de hello, notez que le nombre d’instances actuelles hello est 1. Cliquez sur « Activer la mise à l’échelle automatique ».
  ![Paramètre d’échelle pour la nouvelle application web][5]
- Fournissez un nom pour le paramètre d’échelle hello et hello cliquez sur « Ajouter une règle ». Notez que les options de règle de mise à l’échelle de hello qui s’ouvre dans la partie droite de hello, un volet de contexte. Par défaut, il définit tooscale d’option hello votre instance compter à 1 si percetage de processeur hello de ressource de hello est supérieure à 70 %. Modifier la source de métrique hello haut hello trop « Application Insights », sélectionnez hello la ressource application insights dans hello 'Resource' dropdown et métrique personnalisée de hello puis basé sur lequel vous souhaitez tooscale.
  ![Mettre à l’échelle par métrique personnalisée][6]
- Étape toohello similaire ci-dessus, ajouter une règle de mise à l’échelle qui est ajustée dans et diminuer le nombre de montée en puissance hello par 1 si la métrique personnalisée de hello est au-dessous du seuil.
  ![Mise à l’échelle en fonction du processeur][7]
- Définissez hello instance de limites. Par exemple, si vous souhaitez tooscale entre des instances de 2 à 5 selon les fluctuations de métrique personnalisée hello, définissez 'minimale' trop '2', 'maximum' trop '5' et 'default' trop « 2 »
> Remarque : au cas où il existe un problème de lecture des métriques de ressources hello et capacité actuelle de hello est inférieures à la capacité par défaut de hello, puis disponibilité de hello tooensure de ressource de hello, mise à l’échelle évoluera toohello dont la valeur par défaut. Si la propriété capacity hello est déjà supérieur à la capacité par défaut, la mise à l’échelle n’évolue pas dans.
- Cliquez sur « Enregistrer »

Félicitations ! Vous pouvez maintenant correctement créé votre échelle définissant tooauto mise à l’échelle votre application web basée sur une mesure personnalisée.

> Remarque : hello la même procédure est applicable tooget un rôle de service cloud ou de mise en route.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
