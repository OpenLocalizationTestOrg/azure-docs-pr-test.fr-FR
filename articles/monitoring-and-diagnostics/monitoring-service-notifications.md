---
title: "aaaWhat sont des Notifications de contrôle d’intégrité de Service | Documents Microsoft"
description: "Notifications de service d’intégrité autoriser les que messages de contrôle d’intégrité du service tooview publication par Microsoft Azure."
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
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>Notifications d'intégrité de service
## <a name="overview"></a>Vue d'ensemble

Cet article explique comment les notifications de contrôle d’intégrité tooview service à l’aide de hello portail Azure.

Les notifications de service d’intégrité autoriser vous tooview service d’intégrité des messages publié par hello équipe Azure susceptibles d’affecter les ressources hello sous votre abonnement. Ces notifications sont une sous-classe de l’activité de journal des événements et se trouve également sur le panneau de journal d’activité hello. Notifications de contrôle d’intégrité de service peuvent être d’information ou utilisables en fonction de la classe hello.

Il existe cinq classes de notifications de contrôle d’intégrité :  

- **Action requise :** à partir de l’heure tootime nous pouvons notez quelque chose d’inhabituel se produire sur votre compte. Nous pouvons besoin toowork avec vous tooremedy. Nous vous enverrons une notification soit détaillant les actions hello vous devez tootake ou avec plus d’informations sur la façon d’ingénierie toocontact Azure ou prend en charge.  
- **Récupération assistée :** Un événement est survenu et les ingénieurs ont confirmé que l’impact vous affectait toujours. L’équipe d’ingénierie devez toowork avec vous toobring directement votre toorestoration de services.  
- **Incident :** un impact sur les événements de service affecte actuellement un ou plusieurs des ressources hello dans votre abonnement.  
- **Maintenance :** il s’agit d’une notification vous informant d’une activité de maintenance planifiée qui peut avoir un impact sur une ou plusieurs des ressources hello sous votre abonnement.  
- **Informations :** à partir de l’heure tootime nous pouvons vous envoyer des notifications qu’un tooyou de communiquer sur les optimisations potentielles qui peuvent aider à améliorer votre utilisation des ressources.  
- **Sécurité :** Des informations urgentes liées à la sécurité concernant vos solutions s’exécutant sur Azure.

Chaque notification de contrôle d’intégrité du service transitent des détails sur les ressources de tooyour de portée et impact hello. Les détails incluront ce qui suit :

Nom de la propriété | Description
-------- | -----------
channels | Est une des valeurs suivantes de hello : « Admin », « Opération »
correlationId | Est généralement un GUID au format de chaîne hello. Événements appartenant toohello même action uber partagent généralement hello même correlationId.
eventDataId | Est l’identificateur unique de hello d’un événement
eventName | Titre hello d’événement de hello
level | Niveau d’événement de hello. Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires »
resourceProviderName | Nom du fournisseur de ressources hello pour hello affectées les ressources
resourceType| type Hello de ressource de hello affectées les ressources
subStatus | Généralement hello le code d’état HTTP de hello correspondant appel REST, mais peut également inclure d’autres chaînes décrivant un sous-état, telles que ces valeurs courantes : OK (Code d’état HTTP : 200), créé (Code d’état HTTP : 201), accepté (Code d’état HTTP : 202), aucun contenu (HTTP Code d’état : 204), demande incorrecte (Code d’état HTTP : 400), il est introuvable (Code d’état HTTP : 404), conflit (Code d’état HTTP : 409), erreur interne au serveur (Code d’état HTTP : 500), Service indisponible (Code d’état HTTP : 503), délai d’attente de la passerelle (Code d’état HTTP : 504).
eventTimestamp | Horodatage lors de l’événement de hello a été généré par hello du traitement du service Azure hello demande événement hello correspondant.
submissionTimestamp |   Horodatage lors de l’événement de hello sont devenues disponible pour l’interrogation.
subscriptionId | Hello abonnement Azure dans laquelle cet événement a été enregistré.
status | Chaîne décrivant l’état hello d’opération de hello. Certaines valeurs courantes sont : Started, In Progress, Succeeded, Failed, Active, Resolved.
operationName | Nom de l’opération de hello.
category | « ServiceHealth »
resourceId | Id de ressource de hello affectées les ressources.
Properties.title | Hello titre localisé pour cette communication. L’anglais est la langue par défaut de hello.
Properties.communication | Hello localisées des détails de communication hello par un balisage HTML. L’anglais est la valeur par défaut hello.
Properties.incidentType | valeurs possibles : AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | Identifie l’incident hello que cet événement est associé. Utilisez cet incident de toocorrelate hello événements tooan connexes.
Properties.impactedServices | Un séquence d’échappement blob JSON qui décrit les services hello et les régions qui sont affectées par l’incident de hello. Une liste de services, chacun possédant un ServiceName et une liste d’ImpactedRegions, chacune ayant un RegionName.
Properties.defaultLanguageTitle | communication Hello en anglais
Properties.defaultLanguageContent | communication Hello en anglais en tant que balisage html ou texte brut
Properties.stage | Les valeurs possibles pour AssistedRecovery, ActionRequired, Information, Incident et Security sont Active, Resolved. Pour Maintenance, les valeurs possibles sont Active, Planned, InProgress, Canceled, Rescheduled, Resolved et Complete
Properties.communicationId | communication de Hello cet événement est associé.


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>Affichez vos notifications de contrôle d’intégrité du service hello portail Azure
1.  Bonjour [portal](https://portal.azure.com), accédez toohello **moniteur** service

    ![Surveiller](./media/monitoring-service-notifications/home-monitor.png)
2.  Cliquez sur hello **moniteur** tooopen option de panneau d’analyse hello. Ce panneau rassemble tous vos paramètres de surveillance et données dans une vue consolidée. Il commence par toohello **le journal d’activité** section.

3.  Cliquez maintenant sur le service **Notifications de service**

    ![Surveiller](./media/monitoring-service-notifications/service-health-summary.png)
4.  Cliquez sur n’importe quel tooview d’éléments de ligne hello plus de détails

5. Cliquez sur hello **+ ajouter une activité journal alerte** opération tooreceive notifications tooensure vous en êtes informé futures notifications de service de ce type. d’autres informations sur la configuration des alertes sur les notifications de service de toolearn [cliquez ici](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>Étapes suivantes :
Recevez des [notifications d'alerte lorsqu'une notification d’intégrité de service](monitoring-activity-log-alerts-on-service-notifications.md) est publiée  
En savoir plus sur les [alertes du journal d’activité](monitoring-activity-log-alerts.md)
