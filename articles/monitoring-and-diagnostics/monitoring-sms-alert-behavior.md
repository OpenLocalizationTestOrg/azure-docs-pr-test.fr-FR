---
title: "Comportement des alertes SMS dans les groupes d’actions | Microsoft Docs"
description: "Format de message SMS et réponse aux messages SMS pour annuler un abonnement, vous réinscrire ou demander de l’aide."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3e4eca174209eeb9cbce1d45111d1e5cc30af8b0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>Comportement des alertes SMS dans les groupes d’actions
## <a name="overview"></a>Vue d'ensemble ##
Les groupes d’actions vous permettent de configurer une liste de destinataires. Ces groupes peuvent être utilisés lors de la définition des alertes de journal d’activité, en veillant à ce qu’un groupe d’actions particulier soit notifié au déclenchement de l’alerte de journal d’activité. Un des mécanismes d’alerte pris en charge est le SMS ; les alertes prennent en charge la communication bidirectionnelle. Un utilisateur peut répondre à une alerte pour :

- **Se désabonner des alertes :** Un utilisateur peut annuler l’abonnement pour toutes les alertes SMS pour tous les groupes d’actions, ou un groupe d’actions particulier.  
- **Se réinscrire aux alertes :** Un utilisateur peut se réinscrire à toutes les alertes SMS pour tous les groupes d’actions, ou à groupe d’actions particulier.  
- **Demander de l’aide :** Un utilisateur peut demander plus d’informations sur le SMS. Ils seront redirigés vers cet article

Cet article traite du comportement des alertes SMS et des actions de réponse que l’utilisateur peut entreprendre en fonction des paramètres régionaux de l’utilisateur :

## <a name="usacanada-sms-behavior"></a>Comportement SMS États-Unis/Canada
### <a name="receiving-an-sms-alert"></a>Réception d’une alerte SMS
Un destinataire SMS, qui est configuré comme faisant partie d’un groupe d’actions, recevra un SMS lorsqu’une alerte se déclenche. Le SMS contiendra les informations suivantes :
* Le nom court du groupe d’actions auquel cette alerte a été envoyée
- Titre de l’alerte

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Désabonnement d’alertes SMS pour un groupe d’actions
Un utilisateur peut se désabonner de SMS pour les alertes pour un groupe d’actions en répondant avec le code 20873 avec les mots-clés « Stop » avec les mots clés : « DISABLE &lt;Nom court du groupe d’actions&gt; ».

P. Un utilisateur souhaitant se désabonner des alertes pour un groupe d’actions avec le nom court « Azure », enverrait ainsi un SMS avec le code 20873 indiquant « DISABLE Azure »

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Annulation d’alertes SMS pour tous les groupes d’actions
Un utilisateur peut se désabonner de toutes les alertes SMS pour tous les groupes d’actions en répondant avec le code 20873 accompagné d’un des mots-clés suivants :
* STOP

P. Un utilisateur souhaitant se désabonner de toutes les alertes SMS pour un groupe d’actions enverrait ainsi un SMS avec le code 20873 indiquant « STOP »

>[!NOTE]
>Si un utilisateur a annulé son abonnement aux alertes SMS, mais est ensuite ajouté à un nouveau groupe d’actions ; il RECEVRA les alertes SMS pour ce nouveau groupe d’actions, mais restera désabonné de tous les groupes d’actions précédents.
>
>

### <a name="resubscribing-to-sms-alerts-for-one-action-group"></a>Réabonnement aux alertes SMS pour un groupe d’actions
Un utilisateur peut se réabonner aux SMS pour les alertes pour un groupe d’actions en répondant avec le code 20873 avec les mots-clés « Stop » avec les mots clés : « ENABLE &lt;Nom court du groupe d’actions&gt; ».

P. Un utilisateur souhaitant se réabonner aux alertes pour un groupe d’actions avec le nom court « Azure », enverrait ainsi un SMS avec le code 20873 indiquant « ENABLE Azure »

### <a name="resubscribing-to-sms-alerts-for-all-action-groups"></a>Réabonnement aux alertes SMS pour tous les groupes d’actions
Un utilisateur peut se réabonner à toutes les alertes SMS pour tous les groupes d’actions en répondant avec le code 20873 accompagné d’un des mots-clés suivants :

* START

P. Un utilisateur souhaitant se réabonner à toutes les alertes SMS pour un groupe d’actions enverrait ainsi un SMS avec le code 20873 indiquant « START »

### <a name="requesting-help-via-sms"></a>Demande d’aide via SMS
Un utilisateur peut demander plus d’informations sur le SMS qu’ils ont reçu en répondant avec le code 20873 accompagné d’un des mots-clés suivants :
* HELP

Une réponse est envoyée à l’utilisateur avec un lien vers cet article.

## <a name="next-steps"></a>Étapes suivantes
Obtenez une [Vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md) et découvrez comment recevoir des alertes  
En savoir plus sur la [restriction des SMS](monitoring-alerts-rate-limiting.md)  
En savoir plus sur les [groupes de ressources](monitoring-action-groups.md)
