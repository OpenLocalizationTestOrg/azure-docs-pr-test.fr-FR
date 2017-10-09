---
title: "contrôle d’intégrité de hello aaaMonitor des ressources d’Azure CDN | Documents Microsoft"
description: "Découvrez comment toomonitor hello d’intégrité de vos ressources Azure CDN à l’aide de l’intégrité des ressources Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a>Surveiller la santé hello des ressources d’Azure CDN
  
Azure CDN Resource Health est un sous-ensemble [d’Azure Resource Health](../resource-health/resource-health-overview.md).  Vous pouvez utiliser Azure d’intégrité toomonitor hello contrôle d’intégrité des ressources CDN et recevoir des problèmes de tootroubleshoot des instructions.

>[!IMPORTANT] 
>L’intégrité des ressources Azure CDN comptes uniquement actuellement pour la santé hello de remise globale du CDN et les fonctionnalités de l’API.  Azure CDN Resource Health ne vérifie pas les points de terminaison CDN individuels.
>
>signaux Hello ce flux de contrôle d’intégrité Azure CDN peuvent être up minutes too15 retardées.

## <a name="how-toofind-azure-cdn-resource-health"></a>Comment toofind l’intégrité des ressources Azure CDN

1. Bonjour [portail Azure](https://portal.azure.com), recherchez le profil CDN tooyour.

2. Cliquez sur hello **paramètres** bouton.

    ![Bouton Paramètres](./media/cdn-resource-health/cdn-profile-settings.png)

3. Sous *Support + dépannage*, cliquez sur **Intégrité des ressources**.

    ![Intégrité des ressources CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
>Vous pouvez également trouver des ressources CDN dans hello *l’intégrité des ressources* vignette Bonjour *aide + support* panneau.  Vous pouvez obtenir rapidement trop*aide + support* en cliquant sur hello encerclé **?** dans hello coin supérieur droit du portail de hello.
>
> ![Aide + Support](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a>Messages propres à CDN Azure

Vous trouverez les États associés tooAzure CDN l’intégrité des ressources ci-dessous.

|Message | Action recommandée |
|---|---|
|Vous avez peut-être arrêté, supprimé ou incorrectement configuré un ou plusieurs points de terminaison CDN | Vous avez peut-être arrêté, supprimé ou incorrectement configuré un ou plusieurs points de terminaison CDN.|
|Nous sommes désolés, hello service de gestion CDN est actuellement indisponible | À vérifier les mises à jour d’état ; Si le problème persiste après que hello attendu le temps de résolution, contactez le support technique.|
|Désolé. Vos points de terminaison CDN peuvent être affectés par des problèmes courants liés à certains de nos fournisseurs CDN | À vérifier les mises à jour d’état ; Utilisez toolearn d’outil de résolution des problèmes de hello comment tootest votre origine et le point de terminaison CDN Si le problème persiste après que hello attendu le temps de résolution, contactez le support technique. |
|Nous sommes désolés, les modifications de la configuration des points de terminaison CDN subissent des retards de propagation | À vérifier les mises à jour d’état ; Si vos modifications de configuration ne sont pas complètement propagées dans le temps de hello attendu, contactez le support technique.|
|Nous sommes désolés, que nous rencontrons des problèmes lors du chargement du portail supplémentaire du hello | À vérifier les mises à jour d’état ; Si le problème persiste après que hello attendu le temps de résolution, contactez le support technique.|
Nous sommes désolés, nous rencontrons des problèmes avec certains de nos fournisseurs CDN | À vérifier les mises à jour d’état ; Si le problème persiste après que hello attendu le temps de résolution, contactez le support technique. |

## <a name="next-steps"></a>Étapes suivantes

- [Vue d’ensemble d’Azure Resource Health](../resource-health/resource-health-overview.md)
- [Résolution des problèmes de compression des fichiers CDN](./cdn-troubleshoot-compression.md)
- [Dépannage des points de terminaison de CDN renvoyant des états 404](./cdn-troubleshoot-endpoint.md)