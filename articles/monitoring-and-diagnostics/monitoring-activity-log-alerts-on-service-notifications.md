---
title: "alertes du journal d’activité aaaReceive sur les notifications de service | Documents Microsoft"
description: "Soyez informé par SMS, e-mail ou webhook en cas de service Azure."
author: johnkemnetz
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
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>Créer des alertes de journal d’activité sur les notifications de service
## <a name="overview"></a>Vue d'ensemble
Cet article vous explique comment tooset journal d’activité des alertes pour les notifications de contrôle d’intégrité de service à l’aide de hello portail Azure.  

Vous pouvez recevoir une alerte lorsque Azure envoie des notifications tooyour abonnement Azure de service d’intégrité. Vous pouvez configurer l’alerte hello en fonction de :

- classe Hello de notification de contrôle d’intégrité de service (incident, maintenance, informations, etc.).
- Hello ou les services concernés.
- Hello ou des régions affectées.
- état de Hello de notification de hello (active ou résolu).
- niveau Hello de notifications de hello (information, avertissement, erreur).

Vous pouvez également configurer qui alerte de hello doit être envoyé à :

- sélectionner un groupe d’actions existant ;
- créer un nouveau groupe d’actions (qui peut être utilisé pour les alertes futures).

toolearn savoir plus sur les groupes d’actions, consultez [créer et gérer des groupes d’actions](monitoring-action-groups.md).

Pour plus d’informations sur la notification de contrôle d’intégrité du service tooconfigure des alertes à l’aide de modèles Azure Resource Manager, consultez [modèles Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a>Créer une alerte sur une notification de contrôle d’intégrité de service pour un nouveau groupe d’actions à l’aide de hello portail Azure
1. Bonjour [portal](https://portal.azure.com), sélectionnez **analyse**.

    ![Hello service de « Analyse »](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. Bonjour **le journal d’activité** section, sélectionnez **alertes**.

    ![onglet de « Alertes » Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. Sélectionnez **ajouter une alerte journal activité**et renseignez les champs hello.

    ![Hello « Ajouter une alerte de journal d’activité » de commande](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. Entrez un nom dans hello **nom de l’alerte activité journal** zone et fournissez un **Description**.

    ![boîte de dialogue « Ajouter une alerte de journal d’activité » Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. Hello **abonnement** zone autofills avec votre abonnement actuel. Cet abonnement est alerte de journal utilisé toosave hello activité. ressources d’alerte Hello est toothis déployé les événements d’un abonnement et des analyses dans le journal d’activité hello pour qu’il.

6. Sélectionnez hello **groupe de ressources** les Bonjour ressource alerte est créée. Cela n’est pas le groupe de ressources hello qui est surveillé par l’alerte de hello. Au lieu de cela, il s’agit de groupe de ressources de hello où se trouve la ressource d’alerte hello.

7. Bonjour **catégorie d’événement** boîte, sélectionnez **l’intégrité du Service**. Si vous le souhaitez, sélectionnez hello **Service**, **région**, **Type**, **état**, et **niveau** de service notifications de contrôle d’intégrité que vous souhaitez tooreceive.

8. Sous **alerte via**, sélectionnez hello **nouveau** bouton d’action de groupe. Entrez un nom dans hello **nom d’Action groupe** zone et entrez un nom dans hello **nom court** boîte. nom court de Hello est référencé dans les notifications hello qui sont envoyées lorsque cette alerte se déclenche.

9. Définir une liste de destinataires en fournissant du récepteur hello :

    a. **Nom**: entrez le nom du récepteur hello, alias ou identificateur.

    b. **Type d’action** : sélectionnez SMS, e-mail ou webhook.

    c. **Détails**: selon le type d’action hello choisi, entrez un numéro de téléphone, une adresse de messagerie ou un webhook URI.

10. Sélectionnez **OK** alerte de hello toocreate.

Dans quelques minutes, alerte de hello est actif et commence tootrigger en fonction des conditions hello que vous avez spécifié lors de la création.

Pour plus d’informations sur le schéma de webhook hello pour les alertes de journal d’activité, consultez [Webhooks pour l’activité Azure journaliser les alertes](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>groupe d’actions Hello définie dans ces étapes est réutilisable en tant qu’un groupe d’actions existant pour toutes les définitions d’alerte futures.
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a>Créer une alerte sur une notification de contrôle d’intégrité de service pour un groupe d’actions à l’aide de hello portail Azure

1. Suivez les étapes 1 à 7 dans hello précédente section toocreate votre notification de contrôle d’intégrité du service. 

2. Sous **alerte via**, sélectionnez hello **existant** bouton d’action de groupe. Sélectionnez le groupe d’actions approprié hello.

3. Sélectionnez **OK** alerte de hello toocreate.

Dans quelques minutes, alerte de hello est actif et commence tootrigger en fonction des conditions hello que vous avez spécifié lors de la création.

## <a name="manage-your-alerts"></a>Gérez vos alertes

Après avoir créé une alerte, elle est visible dans hello **alertes** section Hello **moniteur** panneau. Sélectionnez l’alerte hello toomanage à :

* la modifier
* la supprimer
* Désactiver ou activer, si vous souhaitez tootemporarily arrêter ou reprenez la réception des notifications d’alerte de hello.

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur les [notifications sur l’intégrité du service](monitoring-service-notifications.md).
- En savoir plus sur la [limitation du débit des notifications](monitoring-alerts-rate-limiting.md).
- Hello de révision [webhook alerte schéma des journaux d’activité](monitoring-activity-log-alerts-webhook.md).
- Obtenir un [vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md)et découvrez comment tooreceive alertes. 
- En savoir plus sur les [groupes d’actions](monitoring-action-groups.md).
