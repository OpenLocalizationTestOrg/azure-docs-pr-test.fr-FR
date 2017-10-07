---
title: "statistiques d’aaaReal au moment d’Azure CDN | Documents Microsoft"
description: "Statistiques en temps réel fournissent des données en temps réel sur les performances de hello du CDN Azure lors de la remise de contenu tooyour clients."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Statistiques en temps réel dans Microsoft Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Vue d'ensemble
Ce document explique les statistiques en temps réel dans Microsoft Azure CDN.  Cette fonctionnalité fournit des données en temps réel, telles que la bande passante, les États de cache et les connexions simultanées tooyour CDN profil lors de la remise de contenu tooyour clients. Cela permet la surveillance continue de l’intégrité hello de votre service à tout moment, y compris les événements de mise en production.

Hello suivant graphiques est disponible :

* [Bande passante](#bandwidth)
* [Codes d’état](#status-codes)
* [États du cache](#cache-statuses)
* [Connexions](#connections)

## <a name="accessing-real-time-stats"></a>Accès à des statistiques en temps réel
1. Bonjour [Azure Portal](https://portal.azure.com), recherchez le profil CDN tooyour.
   
    ![Panneau du profil CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    portail de gestion CDN Hello s’ouvre.
3. Placez votre curseur sur hello **Analytique** tab, puis pointez sur hello **les statistiques en temps réel** menu volant.  Cliquez sur **HTTP Large Object**.
   
    ![Portail de gestion CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    Hello statistiques en temps réel graphiques sont affichés.

Chacun des graphiques de hello affiche des statistiques en temps réel pour l’intervalle de temps hello sélectionné, lorsque le chargement de la page hello.  graphiques de Hello mettre à jour automatiquement après quelques secondes.  Hello **actualiser le graphique** bouton, le cas échéant, effacera graphique hello, après quoi, il affiche uniquement les données de salutation sélectionnée.

## <a name="bandwidth"></a>Bande passante
![Graphique Bande passante](./media/cdn-real-time-stats/cdn-bandwidth.png)

Hello **la bande passante** graphique affiche la quantité hello de bande passante utilisée pour la plateforme actuelle de hello sur un intervalle de temps hello sélectionné. la partie ombrée Hello du graphique de hello indique l’utilisation de la bande passante. Hello exacte de la bande passante en cours d’utilisation s’affiche directement sous le graphique en courbes hello.

## <a name="status-codes"></a>Codes d’état
![Graphique Code d’état](./media/cdn-real-time-stats/cdn-status-codes.png)

Hello **Codes d’état** graphique indique la fréquence à laquelle certains codes de réponse HTTP sont produisent sur un intervalle de temps hello sélectionné.

> [!TIP]
> Pour obtenir une description de chaque option de code d’état HTTP, consultez la page [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)(Codes d’état HTTP d’Azure CDN).
> 
> 

Une liste des codes d’état HTTP s’affiche directement au-dessus de graphique de hello. Cette liste indique chaque code d’état qui peut être inclus dans le graphique en courbes hello et nombre actuel de hello d’occurrences par seconde pour ce code d’état. Par défaut, une ligne est affichée pour chacun de ces codes d’état dans le graphique de hello. Toutefois, vous pouvez choisir tooonly codes d’état hello moniteur qui ont une signification spéciale pour votre configuration CDN. toodo, les codes d’état souhaité de hello et désactivez toutes les autres options, puis cliquez sur **actualiser le graphique**. 

Vous pouvez masquer temporairement les données consignées pour un code d’état spécifique.  À partir de la légende hello directement sous le graphique de hello, cliquez sur hello code de statut toohide. code d’état Hello est immédiatement masquée dans le graphique de hello. Cliquez à nouveau sur ce code d’état entraîne que toobe option affichée de nouveau.

## <a name="cache-statuses"></a>États du cache
![Graphique États du cache](./media/cdn-real-time-stats/cdn-cache-status.png)

Hello **Cache états** graphique indique la fréquence à laquelle certains types d’états de cache sont produisent sur un intervalle de temps hello sélectionné. 

> [!TIP]
> Pour obtenir une description de chaque option de code d’état du cache, consultez la page [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx)(Codes d’état du cache d’Azure CDN).
> 
> 

Une liste des codes d’état du cache s’affiche directement au-dessus de graphique de hello. Cette liste indique chaque code d’état qui peut être inclus dans le graphique en courbes hello et nombre actuel de hello d’occurrences par seconde pour ce code d’état. Par défaut, une ligne est affichée pour chacun de ces codes d’état dans le graphique de hello. Toutefois, vous pouvez choisir tooonly codes d’état hello moniteur qui ont une signification spéciale pour votre configuration CDN. toodo, les codes d’état souhaité de hello et désactivez toutes les autres options, puis cliquez sur **actualiser le graphique**. 

Vous pouvez masquer temporairement les données consignées pour un code d’état spécifique.  À partir de la légende hello directement sous le graphique de hello, cliquez sur hello code de statut toohide. code d’état Hello est immédiatement masquée dans le graphique de hello. Cliquez à nouveau sur ce code d’état entraîne que toobe option affichée de nouveau.

## <a name="connections"></a>Connexions
![Graphique Connexions](./media/cdn-real-time-stats/cdn-connections.png)

Ce graphique indique le nombre de connexions qui ont été établies tooyour bord serveurs. Chaque demande de ressource qui traverse notre CDN entraîne une connexion.

## <a name="next-steps"></a>Étapes suivantes
* Tenez-vous informé en consultant la page [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)
* Allez plus loin en vous familiarisant avec les [rapports HTTP avancés](cdn-advanced-http-reports.md)
* Analysez les [modes d’utilisation](cdn-analyze-usage-patterns.md)

