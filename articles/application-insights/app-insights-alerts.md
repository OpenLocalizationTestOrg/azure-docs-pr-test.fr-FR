---
title: Alertes aaaSet dans Azure Application Insights | Documents Microsoft
description: "Tenez-vous informé des temps de réponse lents, des exceptions et des autres changements de performances ou d’utilisation de votre application web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>Configuration d’alertes dans Application Insights
[Azure Application Insights] [ start] peut vous alerter toochanges dans les mesures de performances ou d’utilisation dans votre application web. 

Application Insights surveille votre application en temps réel sur une [large éventail de plateformes] [ platforms] toohelp diagnostiquer les problèmes de performances et de comprendre les modèles d’utilisation.

Il existe trois types d’alertes :

* Les **alertes de métrique** indiquent quand une métrique dépasse une valeur seuil pendant une certaine période, comme les temps de réponse, le nombre d’exceptions, l’utilisation du processeur ou les affichages de page. 
* [**Tests Web** ] [ availability] vous indiquent lorsque votre site n’est pas disponible sur hello internet ou répond lentement. [En savoir plus][availability].
* [**Diagnostics proactifs** ](app-insights-proactive-diagnostics.md) sont configurées automatiquement toonotify vous sur les modèles de performances inhabituelles.

Dans cet article, nous allons nous concentrer sur les alertes métriques.

## <a name="set-a-metric-alert"></a>Définir une alerte métrique
Panneau de règles d’alerte hello ouvert, puis utilisez hello ajoutent le bouton. 

![Dans le panneau de règles d’alerte hello, choisissez Ajouter une alerte. Configurer votre application comme hello ressource toomeasure, fournissez un nom pour l’alerte de hello et choisissez une mesure.](./media/app-insights-alerts/01-set-metric.png)

* Ressource hello hello avant de définir d’autres propriétés. **Sélectionnez une ressource hello « (composants) »** si vous souhaitez que les alertes tooset des métriques de performances ou d’utilisation.
* nom de Hello que vous donnez à toohello alerte doit être unique au sein du groupe de ressources hello (et pas seulement de votre application).
* Être prudent toonote unités de hello dans lequel vous êtes invité à valeur de seuil tooenter hello.
* Si vous case hello « Propriétaires messagerie... », les alertes sont envoyées par tooeveryone par courrier électronique qui possède le groupe de ressources toothis accès. tooexpand cet ensemble de personnes, ajoutez-les toohello [groupe de ressources ou d’un abonnement](app-insights-resources-roles-access-control.md) (pas hello ressource).
* Si vous spécifiez « E-mails supplémentaires », les alertes sont envoyées toothose personnes ou groupes (ou non vous activé case à cocher « Envoyer par courrier électronique propriétaires... » hello). 
* Définir un [webhook adresse](../monitoring-and-diagnostics/insights-webhooks-alerts.md) si vous avez configuré une application web qui répond tooalerts. Elle est appelée lorsque hello alerte est activée et il est résolu. (Mais notez qu’à l’heure actuelle, les paramètres de requête ne sont pas transmis en tant que propriétés webhook.)
* Vous pouvez désactiver ou activer hello alerte : hello des boutons haut hello du Panneau de hello.

*Je ne vois pas bouton alerte de hello ajouter.* 

* Utilisez-vous un compte professionnel ? Vous pouvez définir des alertes si vous avez propriétaire ou contributeur de ressource d’application accès toothis. Examinez un panneau de contrôle d’accès hello. [En savoir plus sur le contrôle d’accès][roles].

> [!NOTE]
> Dans le panneau des alertes hello, vous voyez qu’il existe déjà un jeu de l’alerte : [Diagnostics proactifs](app-insights-proactive-failure-diagnostics.md). alerte automatique de Hello surveille un particulier métrique, taux d’échec. Sauf si vous décidez d’alerte proactive de toodisable hello, vous n’avez pas besoin tooset votre propre alerte sur le taux d’échec. 
> 
> 

## <a name="see-your-alerts"></a>Consultez vos alertes
Vous recevez un e-mail lorsqu’une alerte bascule entre les états inactive et active. 

état actuel de Hello de chaque alerte est indiqué dans le panneau de règles d’alerte hello.

Il existe un résumé de l’activité récente dans les alertes de hello de liste déroulante :

![Liste déroulante Alertes](./media/app-insights-alerts/010-alert-drop.png)

historique de Hello des changements d’état est Bonjour journal d’activité :

![Dans Panneau de vue d’ensemble de hello, cliquez sur paramètres, les journaux d’Audit](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>Fonctionnement des alertes
* Une alerte a trois états : « Jamais activée », « Activée » et « Résolue ». Activé signifie hello la condition spécifiée a la valeur est true, lors de la dernière évaluation.
* Une notification est générée lorsqu'une alerte change d'état. (Si la condition d’alerte hello était déjà le cas lorsque vous avez créé l’alerte de hello, vous ne pouvez pas obtenir une notification jusqu'à ce que la condition de hello soit false.)
* Chaque notification génère un message électronique si vous coché hello e-mails case ou fourni des adresses de messagerie. Vous pouvez également examiner de liste déroulante de Notifications hello.
* Une alerte est évaluée chaque fois qu’une mesure arrive, mais pas autrement.
* évaluation de Hello agrège les mesures de hello sur hello précédant la période et compare ensuite nouvel état toohello seuil toodetermine hello.
* période Hello que vous choisissez Spécifie l’intervalle de salutation pendant laquelle les mesures sont agrégées. Il n’affecte pas la fréquence à laquelle hello alerte est évaluée : qui dépend de fréquence de hello d’arrivée des métriques.
* Si aucune donnée n’est reçu pour une mesure particulière pendant un certain temps, intervalle de hello a différents effets sur l’évaluation d’alerte et sur les graphiques hello dans l’Explorateur de métrique. Dans l’Explorateur de métriques, si aucune donnée n’apparaît plus longue que l’intervalle d’échantillonnage de l’organigramme hello, graphique de hello affiche la valeur 0. Mais une alerte en fonction de hello même mesure n’est pas réévaluées et hello reste d’état de l’alerte inchangé. 
  
    Lorsque les données arrivent par la suite, le graphique de hello accède valeur de retour tooa différente de zéro. alerte de Hello prend la valeur en fonction des données hello disponibles pour la période de hello que vous avez spécifié. Si le nouveau point de données hello est hello seule disponible dans la période de hello, hello d’agrégation est basé uniquement sur du point de données.
* Une alerte peut osciller fréquemment entre les états alerte et intègre même si vous définissez une longue période. Cela peut se produire si la valeur de métrique hello tourne autour de seuil de hello. Il n’existe aucun hystérésis dans le seuil de hello : hello transition tooalert se produit au hello même valeur que toohealthy de transition hello.

## <a name="what-are-good-alerts-tooset"></a>Quelles sont les alertes bon tooset ?
Cela dépend de votre application. toostart avec, il est conseillé de la tooset pas trop de mesures. Examinez vos graphiques métriques pendant l’exécution de votre application, le temps de tooget un aspect de comment elle se comporte normalement. Cette pratique permet de trouver des moyens tooimprove ses performances. Puis définissez des alertes tootell vous lorsque les métriques hello sortir hello normale à une zone. 

Les alertes les plus appréciées sont les suivantes :

* Les [mesures de navigateur][client], surtout les **temps de chargement des pages** de navigateur, sont efficaces pour les applications web. Si votre page contient de nombreux scripts, vous devez rechercher d’éventuelles **exceptions du navigateur**. Dans l’ordre tooget ces mesures et les alertes, vous avez tooset [analyse de la page web][client].
* **Temps de réponse de serveur** pour SSI hello d’applications web. Ainsi que la configuration d’alertes, garder un œil sur cette métrique toosee si elle disproportionnellement varie en fonction de taux de demandes élevé : variante peut indiquer que votre application s’exécute avec des ressources insuffisantes. 
* **Exceptions de serveur** -toosee les, vous disposez de certains toodo [le programme d’installation supplémentaire](app-insights-asp-net-exceptions.md).

N’oubliez pas que [diagnostics de taux d’échec proactive](app-insights-proactive-failure-diagnostics.md) automatiquement les taux de hello moniteur à laquelle votre application répond toorequests avec des codes d’échec. 

## <a name="automation"></a>Automatisation
* [Utilisez PowerShell tooautomate configurer les alertes](app-insights-powershell-alerts.md)
* [Utilisez tooalerts répond de webhooks tooautomate](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>Voir aussi
* [Tests web de disponibilité](app-insights-monitor-web-app-availability.md)
* [Automatiser la configuration d’alertes](app-insights-powershell-alerts.md)
* [Diagnostics proactifs](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

