---
title: aaaPricing & facturation - Azure Logic Apps | Documents Microsoft
description: "Découvrez comment fonctionnement la tarification et la facturation avec Azure Logic Apps."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.openlocfilehash: fa10cbbf7657afba7fadb7c76817b7a5e4af7b42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-pricing-model"></a>Modèle de tarification de Logic Apps
Azure Logic Apps permet tooscale et exécuter des flux de travail de l’intégration dans le cloud de hello.  Voici les détails sur hello de facturation et la tarification des plans pour les applications de la logique.
## <a name="consumption-pricing"></a>Tarification de la consommation
La plateforme Logic Apps récemment créée utilise un plan de consommation. Avec le modèle de la tarification de la consommation Logic Apps de hello, vous payez uniquement ce que vous utilisez.  La plateforme Logic Apps n’est pas limitée lors de l’utilisation d’un plan de consommation.
Toutes les actions effectuées lors de l’exécution d’une instance de l’application logique sont mesurées.
### <a name="what-are-action-executions"></a>Que sont les exécutions d’action ?
Chaque étape d’une définition de la logique d’application est une action, qui inclut les étapes du flux de contrôle comme les conditions, les étendues, pour chaque boucle, jusqu'à ce que les boucles, les déclencheurs, appelle les actions toonative tooconnectors et d’appels.
Les déclencheurs sont des actions particulières sont conçu tooinstantiate une nouvelle instance d’une application logique, lorsqu’un événement particulier se produit.  Il existe plusieurs comportements différents pour les déclencheurs, ce qui peut affecter le mode application logique de hello est mesurée.
* **L’interrogation déclencheur** – ce déclencheur interroge en permanence un point de terminaison jusqu'à ce qu’il reçoit un message qui répond aux critères de hello pour la création d’une instance d’une application logique.  intervalle d’interrogation de Hello peut être configuré dans le déclencheur hello Bonjour Concepteur de logique d’application.  Chaque requête d’interrogation compte comme une exécution d’action, même si elle ne crée pas d’instance d’une application logique.
* **Déclencheur de Webhook** – ce déclencheur attend un toosend client il une demande sur un point de terminaison particulier.  Chaque demande envoyée à point de terminaison toohello webhook est considérée comme l’exécution d’une action. Hello demande et hello HTTP Webhook déclencheur sont les deux déclencheurs de webhook.
* **Déclencheur de périodicité** – ce déclencheur crée une instance d’application logique de hello en fonction de l’intervalle de périodicité hello configuré dans le déclencheur de hello.  Par exemple, un déclencheur de périodicité peut être configuré toorun tous les trois jours ou même toutes les minutes.

Exécutions du déclencheur peuvent être consultées dans le panneau des ressources hello Logic Apps Bonjour partie de l’historique du déclencheur.

Toutes les actions exécutées, qu’il s’agisse de réussites ou d’échecs, sont considérées comme des exécutions d’action.  Les actions qui ont été ignorées en raison de la condition tooa n’est-il ne pas remplie ou qui n’a pas d’exécuter, car l’application logique de hello arrêtée avant la fin ne sont pas comptés comme des exécutions de l’action.

Les actions exécutées dans les boucles sont comptées par itération de boucle de hello.  Par exemple, une action unique dans une boucle for each effectuer une itération au sein d’une liste de 10 éléments sont comptés comme nombre hello d’éléments de liste de hello (10) multiplié par le nombre de hello d’actions dans une boucle de hello (1) plus un pour l’initiation de hello de boucle de hello , qui, dans cet exemple, serait (10 * 1) + 1 = 11 exécutions de l’action.
Il n’est pas possible de créer de nouvelles instances des applications logiques qui sont désactivées. Par conséquent, pendant leur période de désactivation, elles ne peuvent pas être facturées.  Être conscients qu’après la désactivation d’une application logique peut prendre un peu de temps pour hello instances tooquiesce avant d’être complètement désactivée.
### <a name="integration-account-usage"></a>Utilisation d’un compte d’intégration
Inclus dans l’utilisation de la consommation est un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) pour l’exploration, de développement et à des fins de tests qui vous toouse hello [B2B/EDI](logic-apps-enterprise-integration-b2b.md) et [le traitement XML](logic-apps-enterprise-integration-xml.md)fonctionnalités de Logic Apps sans coût supplémentaire. Vous sont en mesure de toocreate au maximum un seul compte par région et que vous stockez des accords de too10 et des cartes de 25. Il n’y a pas de limite pour les schémas, les certificats et les partenaires et vous pouvez en télécharger autant que vous en avez besoin.

En outre toohello l’inclusion de comptes avec une consommation d’intégration, vous pouvez également créer les comptes d’intégration standard sans ces limites et avec nos contrats d’applications logique standard. Pour plus d’informations, consultez la page [Tarification Azure](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="app-service-plans"></a>Plans App Service
Applications logique créées précédemment référençant un Plan App Service continue toobehave comme avant. Selon le plan hello choisi, sont limité après que dépassement hello exécutions quotidiennes prescrites mais sont facturées à l’aide du compteur de l’exécution d’action hello.
Les clients EA qui ont un Plan de Service d’application dans leur abonnement, ce qui n’a pas toobe associé explicitement hello application logique, exploiter les avantages de quantités hello inclus.  Par exemple, si vous avez un Plan de Service application Standard dans votre abonnement EA et une application de logique dans hello même abonnement, puis que vous n’êtes pas facturé pour 10 000 exécutions d’action par jour (voir tableau suivant). 

Plans App Service et exécutions d’action quotidiennes autorisées :
|  | Gratuit/Partagé/De base | Standard | Premium |
| --- | --- | --- | --- |
| Exécutions d’action quotidiennes |200 |10 000 |50 000 |
### <a name="convert-from-app-service-plan-pricing-tooconsumption"></a>Convertir à partir d’un Plan App Service tarification tooConsumption
toochange une application de la logique qui a un Plan App Service associé à remove hello référence toohello Plan App Service dans la définition d’application logique hello, modèle de consommation tooa.  Cette modification peut être effectuée avec une applet de commande PowerShell de tooa appel :`Set-AzureRmLogicApp -ResourceGroupName ‘rgname’ -Name ‘wfname’ –UseConsumptionModel -Force`
## <a name="pricing"></a>Tarification
Pour plus d’informations sur la tarification, voir la page de [tarification de Logic Apps](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="next-steps"></a>Étapes suivantes
* [Vue d’ensemble de Logic Apps][whatis]
* [Créer votre première application logique][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-what-are-logic-apps.md
[create]: logic-apps-create-a-logic-app.md

