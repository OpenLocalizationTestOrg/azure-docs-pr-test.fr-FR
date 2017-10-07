---
title: "nombre d’instances aaaScale manuellement ou à l’échelle automatique via le portail Azure | Documents Microsoft"
description: "Découvrez comment tooscale vos services Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>Mise à l'échelle manuelle ou automatique du nombre d’instances
Bonjour [Azure Portal](https://portal.azure.com/), vous pouvez définir manuellement le nombre d’instances hello de votre service, ou vous pouvez définir des paramètres toohave il automatiquement mettre à l’échelle en fonction de la demande. Cela est généralement référencé tooas *montée en puissance parallèle* ou *l’échelle en*.

Avant la mise à l’échelle selon le nombre d’instances, vous pensez que la mise à l’échelle est affectée par **niveau tarifaire** dans nombre tooinstance d’addition. Différents niveaux tarifaires peut avoir différents nombres cœurs et la mémoire, et par conséquent, ils offrent de meilleures performances pour hello même nombre d’instances (c'est-à-dire *montée en puissance* ou *à l’échelle*). Cet article aborde plus en détail la *réduction* ou *l’extension des instances*.

Vous pouvez faire évoluer dans le portail de hello, et vous pouvez également utiliser hello [API REST](https://msdn.microsoft.com/library/azure/dn931953.aspx) ou [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust à l’échelle manuellement ou automatiquement.

> [!NOTE]
> Cet article décrit comment toocreate un paramètre dans le portail hello d’échelle automatique [http://portal.azure.com](http://portal.azure.com). Les paramètres de mise à l’échelle créés dans ce portail ne peut pas être modifié à tout portail classique de hello ([http://manage.windowsazure.com](http://manage.windowsazure.com)).
> 
> 

## <a name="scaling-manually"></a>Mise à l'échelle manuelle
1. Bonjour [Azure Portal](https://portal.azure.com/), cliquez sur **Parcourir**, puis accédez toohello ressource tooscale, comme un **plan App Service**.
2. Cliquez sur **Paramètres > Monter en charge (plan App Service).**
3. En haut de hello Hello **échelle** panneau que vous pouvez afficher un historique des actions de mise à l’échelle du service de hello.
   
    ![Volet Scale](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > Seules les actions effectuées par mise à l'échelle automatique seront affichées dans ce graphique. Si vous modifiez manuellement le nombre d’instances hello, modification de hello n’apparaîtront pas dans ce graphique.
   > 
   > 
4. Vous pouvez ajuster manuellement le nombre de hello **Instances** avec le curseur.
5. Cliquez sur hello **enregistrer** commande et vous serez mis à l’échelle nombre toothat d’instances presque immédiatement.

## <a name="scaling-based-on-a-pre-set-metric"></a>Mise à l'échelle en fonction d’une mesure prédéfinie
Si vous souhaitez que le nombre de hello d’instances tooautomatically ajuster selon une mesure, sélectionnez hello métrique que vous souhaitez dans hello **l’échelle** liste déroulante. Pour un **plan App Service**, vous pouvez, par exemple, effectuer une mise à l’échelle via **Pourcentage UC**.

1. Lorsque vous sélectionnez une métrique vous obtiendrez un curseur et/ou, nombre de hello tooenter texte boîtes d’instances que vous souhaitez tooscale entre :
   
    ![Volet Scale avec pourcentage UC](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    Mise à l’échelle n’aura jamais votre service en dessous ou au-dessus des limites hello que vous définissez, quel que soit votre charge.
2. Ensuite, vous choisissez la plage cible de hello pour métrique de hello. Par exemple, si vous avez choisi **pourcentage processeur**, vous pouvez définir une cible de l’UC moyenne de hello sur toutes les instances de hello dans votre service. Une montée en charge se produira lorsque hello moyenne du processeur dépasse le maximum de hello que vous définissez, de même, une échelle de se produit chaque fois que l’UC moyenne de hello descend en dessous hello minimale.
3. Cliquez sur hello **enregistrer** commande. Mise à l’échelle vérifie chaque peu toomake de minutes que vous êtes dans la plage d’instance hello et cible pour votre mesure. Lorsque votre service reçoit du trafic supplémentaire, plusieurs instances vous seront attribuées automatiquement.

## <a name="scale-based-on-other-metrics"></a>Mise à l’échelle en fonction d’autres mesures
Vous pouvez faire évoluer en fonction des métriques que présélections hello qui s’affichent dans hello **l’échelle** liste déroulante et peut même ont un ensemble complexe de montée en puissance parallèle et l’échelle dans les règles.

### <a name="adding-or-changing-a-rule"></a>Ajout ou modification d'une règle
1. Choisissez hello **les règles de performances et de planification** Bonjour **l’échelle** dropdown : ![les règles de Performance](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. Si vous aviez précédemment mise à l’échelle, de vous verrez une vue des règles hello exactes que vous aviez.
3. tooscale basé sur une autre mesure cliquez hello **ajouter une règle** ligne. Vous pouvez également cliquer sur une de hello toochange de lignes existant à partir de la métrique de hello vous aviez précédemment mesure toohello tooscale par.
   ![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)
4. Vous devez maintenant tooselect la métrique que vous souhaitez tooscale par. Lorsque le choix d’une métrique il sont deux choses tooconsider :
   
   * Hello *ressource* provient de la métrique de hello. En règle générale, cela sera être hello même en tant que ressource hello vous mettez à l’échelle. Toutefois, si vous souhaitez tooscale en profondeur hello d’une file d’attente de stockage, les ressources hello sont hello file d’attente tooscale par.
   * Hello *nom de métrique* lui-même.
   * Hello *heure d’agrégation* de métrique de hello. Voici comment les données de salutation sont combiné sur hello *durée*.
5. Après avoir choisi votre mesure choisie seuil hello pour la métrique de hello et de l’opérateur de hello. Vous pouvez, par exemple, dire **Supérieur à** **80 %**.
6. Puis choisissez hello action que vous souhaitez tootake. Il existe deux types d'actions bien distincts :
   
   * Augmente ou diminue, cela ajoutera ou supprimera hello **valeur** nombre d’instances que vous définissez.
   * Augmentez ou diminuez le pourcentage - Cela modifiera le nombre d’instances hello en pourcentage. Par exemple, vous pouvez placer 25 Bonjour **valeur** champ, et si vous aviez actuellement 8 instances, 2 sera ajouté.
   * Augmenter ou diminuer trop - est ainsi définie hello instance nombre toohello **valeur** vous définissez.
7. Enfin, vous pouvez choisir de refroidissement - la durée pendant laquelle cette règle doit attendre après hello précédente échelle action tooscale à nouveau.
8. Après avoir configuré votre règle, cliquez sur **OK**.
9. Après avoir configuré toutes les règles de hello souhaité, être vraiment toohit hello **enregistrer** commande.

### <a name="scaling-with-multiple-steps"></a>Mise à l'échelle en plusieurs étapes
exemples de Hello ci-dessus sont assez simples. Toutefois, si vous souhaitez toobe plus agressive (inférieur ou), vous pouvez même ajouter plusieurs mise à l’échelle des règles pour hello même mesure. Vous pouvez, par exemple, définir deux règles de mise à l'échelle sur Pourcentage UC :

1. Extension d'une instance si le pourcentage UC est supérieur à 60 %
2. Extension de trois instances si le pourcentage UC est supérieur à 85 %

![Règles de mise à l'échelle multiples](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

Avec cette règle supplémentaire, si la charge dépasse 85 % avant une action de mise à l'échelle, vous obtenez deux instances supplémentaires au lieu d'une.

## <a name="scale-based-on-a-schedule"></a>Mise à l'échelle en fonction d’une planification
Par défaut, lorsque vous créez une règle de mise à l'échelle, celle-ci s’appliquera en permanence. Vous pouvez voir que lorsque vous cliquez sur l’en-tête de profil hello :

![Profil](./media/insights-how-to-scale/Insights_Profile.png)

Toutefois, vous souhaiterez peut-être toohave plus agressive échelle pendant hello, hello semaine ou, celle de week-end de hello. Vous pouvez même arrêter intégralement votre service hors des heures de travail.

1. toodo, sur le profil hello avoir, sélectionnez **périodicité** au lieu de **toujours,** et choisissez hello fois que vous souhaitez hello profil tooapply.
2. Par exemple, toohave un profil qui s’applique à la semaine hello, Bonjour **jours** déroulante Décochez **samedi** et **dimanche**.
3. toohave un profil qui s’applique au cours de hello de journée, affectez la valeur hello **l’heure de début** toohello heure toostart au niveau souhaité.
   
    ![Périodicité par défaut](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. Cliquez sur **OK**.
5. Ensuite, vous devez tooadd hello profil que tooapply à d’autres moments. Cliquez sur hello **ajouter un profil de** ligne.
    ![Off Work](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. Vous pouvez, par exemple, intituler votre second nouveau profil **Absent(e) du bureau**.
7. Puis sélectionnez **périodicité** à nouveau, choisissez la plage du nombre d’instance hello souhaité pendant ce temps.
8. Comme avec hello profil par défaut, choisissez hello **jours** vous voulez tooapply de ce profil à et hello **l’heure de début** journée hello.
   
   > [!NOTE]
   > Mise à l’échelle utilisera les règles de l’heure d’été hello pour selon **fuseau horaire** vous sélectionnez. Cependant, lors de l’heure d’été hello UTC décalage affichera le décalage de fuseau horaire de base hello, pas l’offset hello UTC des économies de l’heure d’été.
   > 
   > 
9. Cliquez sur **OK**.
10. Maintenant, vous devez tooadd règles de tout ce que vous souhaitez tooapply pendant votre second profil. Cliquez sur **ajouter une règle**, et ensuite, vous pouvez construire hello même règle vous avez pendant le profil par défaut de hello.
    
    ![Ajouter un règle toooff travail](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. Être toocreate que les deux une règle pour la montée en puissance parallèle et l’échelle dans, ou pendant hello nombre d’instances de profil hello sera uniquement augmenter (ou réduire).
12. Puis, cliquez sur **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
* [Surveiller les métriques de service](insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.
* [Activation de la surveillance et de diagnostics](insights-how-to-use-diagnostics.md) toocollect détaillée des métriques de haute fréquence sur votre service.
* [Réceptions de notifications d’alerte](insights-receive-alert-notifications.md) lorsque des événements opérationnels se produisent ou que des mesures dépassent un seuil.
* [Surveiller les performances de l’application](../application-insights/app-insights-azure-web-apps.md) si vous souhaitez toounderstand exactement comment votre code s’exécute dans le cloud de hello.
* [Afficher les événements et le journal d’activité](insights-debugging-with-events.md) toolearn tout ce qui s’est produite dans votre service.
* [Surveillance de la disponibilité et de la réactivité des pages Web](../application-insights/app-insights-monitor-web-app-availability.md) avec Application Insights pour déterminer si vos pages sont inactives.

