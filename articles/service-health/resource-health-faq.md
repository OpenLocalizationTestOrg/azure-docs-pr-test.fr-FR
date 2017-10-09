---
title: "Forum aux questions de contrôle d’intégrité de ressource d’aaaAzure | Documents Microsoft"
description: "Vue d’ensemble d’Azure Resource Health"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>FAQ Azure Resource Health
Découvrez hello réponses toocommon sur l’intégrité des ressources Azure.

## <a name="what-is-azure-resource-health"></a>Qu’est-ce qu’Azure Resource Health ?
Resource Health vous permet d’établir des diagnostics et d’obtenir de l’aide lorsqu’un problème touchant Azure a des répercussions sur vos ressources. Il vous informe de la santé de vos ressources hello actuelles et passées et vous permet d’atténuer les problèmes. Resource Health propose un support technique dès lors que vous êtes confronté à des problèmes de service Azure et que vous avez besoin d’aide.  

## <a name="what-is-hello-resource-health-intended-for"></a>Nouveautés hello destinée à l’intégrité des ressources
Une fois qu’un problème lié à une ressource a été détecté, l’intégrité des ressources peut vous aider à diagnostiquer la cause première hello. Il fournit le problème de hello toomitigate aide et support technique lorsque vous avez besoin de plus d’informations sur les problèmes de service Azure.

## <a name="what-health-checks-are-performed-by-resource-health"></a>Quels contrôles d’intégrité sont effectués par Resource Health ?
L’intégrité des ressources effectue plusieurs vérifications selon hello [type de ressource](resource-health-checks-resource-types.md). Ces contrôles sont conçus tooimplement trois types de problèmes : 
- Événements non planifiés, par exemple le redémarrage d’un hôte inattendu
- Événements planifiés, telles que les mises à jour planifiées du système d’exploitation hôte
- Événements déclenchés par des actions de l’utilisateur, par exemple le redémarrage d’une machine virtuelle

## <a name="what-does-each-of-hello-health-status-mean"></a>Que signifie chaque état de santé hello ?
Il existe trois états différents :
- Disponible : Il ne sont pas tous les problèmes connus dans hello plateforme Azure qui pourrait être ayant un impact sur cette ressource
- Non disponible : Contrôle d’intégrité a détecté des problèmes qui ont un impact sur les ressources de hello
- Inconnu : L’intégrité des ressources ne peut pas déterminer la santé d’une ressource hello, car il a annulé la réception des informations le concernant. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>Ce que hello moyenne de l’état inconnu ? Y a-t-il un problème avec ma ressource ?
l’état d’intégrité Hello a la valeur toounknown lorsque l’intégrité des ressources cesse de recevoir des informations sur une ressource spécifique. Alors que cet état n’est pas une indication définitive de l’état hello de ressource hello, dans les cas où vous rencontrez des problèmes, il peut indiquer qu'un problème d’Azure.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>Comment puis-je obtenir de l’aide pour une ressource qui n’est pas disponible ?
Vous pouvez soumettre une demande de support à partir du Panneau de l’intégrité des ressources hello. Vous n’avez pas besoin de contrat de support avec Microsoft tooopen une demande lors de la ressource de hello n’est pas disponible, car les événements de plateforme.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>Resource Health fait-il la différence entre une indisponibilité causée par des problèmes de plateforme et une mauvaise manipulation de l’utilisateur ?
Oui, quand une ressource n’est pas disponible, l’intégrité des ressources identifie la cause première hello dans une de ces catégories : 
-   Action initiée par l’utilisateur
-   Événement planifié 
-   Événement non planifié

Dans le portail hello, les actions initiées par l’utilisateur sont affichées à l’aide d’une icône de notification de bleu, tandis que les événements planifiés et sont à l’aide d’une icône d’avertissement rouge. Plus de détails sont fournis dans hello [vue d’ensemble de l’intégrité des ressources](Resource-health-overview.md).  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>Puis-je intégrer Resource Health à mes outils d’analyse ?
L’intégrité des ressources est un toohelp service conçu diagnostiquer et de réduire les problèmes de service Azure qui affectent vos ressources. Vous pouvez utiliser hello API de contrôle d’intégrité de ressource tooprogrammatically obtenir l’état d’intégrité hello, nous vous recommandons de qu'utiliser les mesures toomonitor vos ressources. Une fois qu’un problème est détecté, l’intégrité des ressources vous permet de déterminer la cause première hello et vous guide à travers les actions tooaddress les. Visitez [moniteur Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn plus d’informations sur la façon dont vous pouvez utiliser les métriques toocheck vos ressources.

## <a name="where-do-i-find-resource-health"></a>Où trouver Resource Health ?
Une fois que vous vous connectez toohello portail Azure, il existe plusieurs méthodes que vous pouvez accéder à l’intégrité des ressources :
- Accédez tooyour ressource. Dans la navigation de gauche hello, sélectionnez **l’intégrité des ressources**
- Accédez à panneau de moniteur Azure toohello.  Dans la navigation de gauche hello, sélectionnez **l’intégrité des ressources**.
- Ouvrez hello **aide et Support** panneau en sélectionnant hello point d’interrogation dans hello coin supérieur droit du portail de hello, puis en sélectionnant **aide et Support**. Une fois le panneau de hello s’ouvre, sélectionnez **l’intégrité des ressources**

Vous pouvez également utiliser hello API de contrôle d’intégrité de ressource tooobtain plus d’informations sur le contrôle d’intégrité hello de vos ressources.

## <a name="is-resource-health-available-for-all-resource-types"></a>Resource Health est-il disponible pour tous les types de ressources ?
Hello la liste des contrôles d’intégrité et les types de ressources pris en charge via l’intégrité des ressources sont accessibles [ici](resource-health-checks-resource-types.md).

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>Que dois-je faire si ma ressource apparaît comme disponible, alors que ce n’est pas le cas ?
Lors de la vérification d’intégrité de hello d’une ressource, à droite dans l’état d’intégrité hello vous pouvez cliquer sur **signaler l’état d’intégrité incorrect**. Avant d’envoyer le rapport de hello, vous pouvez hello donnant des détails supplémentaires sur la raison pour laquelle vous pensez que l’état d’intégrité actuel de hello est incorrect.

## <a name="is-resource-health-available-for-all-azure-regions"></a>Resource Health est-il disponible pour toutes les régions Azure ? 
L’intégrité des ressources est disponible dans entre tous les géographiques Azure sauf hello suivant régions :
- Gouvernement américain - Virginie
- US Gov Iowa
- Est des États-Unis – US DoD
- Centre des États-Unis – US DoD
- Centre de l’Allemagne
- Nord-Est de l’Allemagne
- Chine orientale
- Chine du Nord

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>Comment diffère l’intégrité des ressources de notifications de hello hello ou de tableau de bord de Service d’intégrité de service du portail Azure ?
informations Hello fournies par le contrôle d’intégrité sont plus spécifiques que celle fournie par hello tableau de bord d’intégrité de Service Azure.

Alors que [Azure Status](https://status.azure.com) et des notifications de service de portail hello vous informent sur les problèmes de service qui affectent un large éventail de clients (par exemple, une région Azure), l’intégrité des ressources expose des événements plus précis qui sont pertinentes uniquement toohello de ressource spécifique. Par exemple, si un hôte redémarre inopinément, Resource Health n’avertit que les clients dont les machines virtuelles étaient exécutées sur cet hôte.

Il est toonotice important que tooprovide que terminer de visibilité d’événements ayant un impact sur vos ressources, l’intégrité des ressources également les événements de surfaces sont publiés dans les notifications de Service et que vous hello du tableau de bord de Service de contrôle d’intégrité.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>Dois-je tooactivate l’intégrité des ressources pour chaque ressource ?
Non, les informations d’intégrité sont disponibles pour tous les types de ressources disponibles via Resource Health. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>Nous devons tooenable l’intégrité des ressources pour mon organisation ?
Non.  L’intégrité des ressources Azure est accessible hello portail Azure sans conditions requises d’installation.

## <a name="is-resource-health-available-free-of-charge"></a>Resource Health est-il disponible gratuitement ?
Oui.  Azure Resource Health est gratuit.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>Quelles sont les recommandations hello assurant l’intégrité des ressources ?
En fonction de l’état d’intégrité hello, l’intégrité des ressources fournit des recommandations avec comme objectif de réduire le temps de hello hello vous passé à la résolution des problèmes. Pour les ressources disponibles, les recommandations de hello se concentrent sur comment toosolve hello plus courantes des problèmes rencontrés. Si les ressources hello ne sont pas disponible en raison tooan Azure événement non planifié, le focus de hello sera en vous aidant pendant et après le processus de récupération hello. 

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur Resource Health :
-  [Vue d’ensemble d’Azure Resource Health](Resource-health-overview.md)
-  [Types de ressource et contrôles d’intégrité disponibles par le biais d’Azure Resource Health](resource-health-checks-resource-types.md)
