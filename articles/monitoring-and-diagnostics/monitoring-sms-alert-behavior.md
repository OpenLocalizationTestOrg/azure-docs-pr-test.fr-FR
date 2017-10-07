---
title: "comportement des alertes dans les groupes d’actions aaaSMS | Documents Microsoft"
description: "Format de message SMS et toounsubscribe de messages tooSMS répond, vous réinscrire vos disponible ou demander de l’aide."
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
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>Comportement des alertes SMS dans les groupes d’actions
## <a name="overview"></a>Vue d'ensemble ##
Groupes d’actions Activer tooconfigure une liste de destinataires. Ces groupes peuvent être utilisées lors de la définition des alertes de journal d’activité ; s’assurer qu’un groupe d’actions particulier est averti hello activité journal alerte est déclenchée. Un de génération d’alertes de la prise en charge des mécanismes de hello est SMS ; alertes de Hello prend en charge la communication bidirectionnelle. Un utilisateur peut répondre alerte tooan à :

- **Se désabonner des alertes :** Un utilisateur peut annuler l’abonnement pour toutes les alertes SMS pour tous les groupes d’actions, ou un groupe d’actions particulier.  
- **Vous réinscrire vos disponible tooalerts :** un utilisateur peut vous réinscrire vos disponible tooall des alertes SMS pour tous les groupes d’actions ou un groupe d’actions au singulier.  
- **Demander de l’aide :** un utilisateur peut demander pour plus d’informations sur hello SMS. Il sera redirigé toothis article

Cet article traite du comportement de hello d’alertes SMS hello et hello utilisateur de hello actions de réponse peut entreprendre en fonction des paramètres régionaux de hello d’utilisateur de hello :

## <a name="usacanada-sms-behavior"></a>Comportement SMS États-Unis/Canada
### <a name="receiving-an-sms-alert"></a>Réception d’une alerte SMS
Un destinataire SMS, qui est configuré comme faisant partie d’un groupe d’actions, recevra un SMS lorsqu’une alerte se déclenche. Hello SMS transitent hello informations suivantes :
* Nom court du groupe d’actions hello cette alerte a été envoyée à
- Titre de l’alerte de hello

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Désabonnement d’alertes SMS pour un groupe d’actions
Un utilisateur peut annuler l’abonnement à partir de SMS pour les alertes pour le groupe d’une action en répond toohello « Stop » au 20873 avec les mots clés de hello : « désactiver &lt;nom court du groupe d’actions&gt;».

P. Un utilisateur souhaitant toounsubscribe à partir d’alertes pour un groupe d’actions avec le nom court de hello « Azure », envoyez un « Stop » au toohello SMS 20873 indiquant que « Désactiver Azure »

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Annulation d’alertes SMS pour tous les groupes d’actions
Un utilisateur peut annuler l’abonnement à partir de toutes les alertes SMS pour tous les groupes d’actions en réponse toohello « Stop » au 20873 avec n’importe quelle Hello après les mots clés :
* STOP

P. Un utilisateur souhaitant toounsubscribe à partir de toutes les alertes SMS pour tous les groupes d’actions, envoyez un « Stop » au toohello SMS 20873 indiquant que « Arrêter »

>[!NOTE]
>Si un utilisateur a annulé son abonnement à partir de SMS des alertes, mais il est ensuite ajouté le nouveau groupe d’actions tooa ; ils seront recevoir des alertes SMS pour ce nouveau groupe d’actions, mais restent non inscrits à partir de tous les groupes d’actions précédent.
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>Resubscribing tooSMS des alertes pour un groupe d’actions
Un utilisateur peut vous réinscrire vos disponible tooSMS pour les alertes pour le groupe d’une action en réponse toohello « Stop » au 20873 avec les mots clés de hello : « activer &lt;nom court du groupe d’actions&gt;».

P. Un utilisateur souhaitant tooalerts tooresubscribe pour un groupe d’actions avec le nom court de hello « Azure », envoyez un « Stop » au toohello SMS 20873 indiquant que « Activer Azure »

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>Resubscribing tooSMS des alertes pour tous les groupes d’actions
Un utilisateur peut réabonner tooall SMS pour les alertes pour tous les groupes d’actions en réponse toohello « Stop » au 20873 avec n’importe quelle Hello après les mots clés :

* START

P. Un utilisateur souhaitant toounsubscribe à partir de toutes les alertes SMS pour tous les groupes d’actions, envoyez un « Stop » au toohello SMS 20873 indiquant que « Démarrer »

### <a name="requesting-help-via-sms"></a>Demande d’aide via SMS
Un utilisateur peut demander pour plus d’informations sur hello SMS qu’ils ont reçu par toohello répond « Stop » au 20873 avec les hello après les mots clés :
* HELP

Une réponse est envoyée utilisateur toohello avec un article de toothis du lien.

## <a name="next-steps"></a>Étapes suivantes
Obtenir un [vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md) et découvrez comment tooget alerté  
En savoir plus sur la [restriction des SMS](monitoring-alerts-rate-limiting.md)  
En savoir plus sur les [groupes de ressources](monitoring-action-groups.md)
