---
title: "Configurer des alertes sur l’intégrité du service Azure avec PagerDuty | Microsoft Docs"
description: "Obtenir des notifications personnalisées sur les événements d’intégrité du service sur votre instance PagerDuty."
author: shawntabrizi
manager: scotthit
editor: 
services: service-health
documentationcenter: service-health
ms.assetid: 
ms.service: service-health
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/14/2017
ms.author: shtabriz
ms.openlocfilehash: 9edcb727b9f0af348cacd5533523c4f2e8214703
ms.sourcegitcommit: afc78e4fdef08e4ef75e3456fdfe3709d3c3680b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/16/2017
---
# <a name="configure-service-health-alerts-with-pagerduty"></a>Configurer des alertes sur l’intégrité de service avec PagerDuty

Cet article vous explique comment configurer les notifications sur l’intégrité du service Azure via PagerDuty à l’aide d’un Webhook. À l’aide du type d’intégration Microsoft Azure personnalisé [PagerDuty](https://www.pagerduty.com/), vous pouvez facilement ajouter des alertes sur l’intégrité du service à vos services PagerDuty nouveaux ou existants.

## <a name="creating-a-service-health-integration-url-in-pagerduty"></a>Création d’une URL d’intégration de service d’intégrité dans PagerDuty
1.  Vérifiez que vous êtes inscrit et connecté à votre compte [PagerDuty](https://www.pagerduty.com/).

2.  Accédez à la section **Services** dans PagerDuty.

    ![Section Services dans PagerDuty](./media/webhook-alerts/pagerduty-services-section.png)

3.  Sélectionnez **Ajouter un nouveau service** ou ouvrez un service existant que vous avez configuré.

4.  Dans les **paramètres d’intégration**, sélectionnez les éléments suivants :

    a. **Type d’intégration** : Microsoft Azure

    b. **Nom de l’intégration** : \<Nom\>

    ![Paramètres d’intégration dans PagerDuty](./media/webhook-alerts/pagerduty-integration-settings.png)

5.  Renseignez tous les autres champs obligatoires et sélectionnez **Ajouter**.

6.  Ouvrez cette nouvelle intégration et copiez et enregistrez l’**URL d’intégration**.

    ![URL d’intégration dans PagerDuty](./media/webhook-alerts/pagerduty-integration-url.png)

## <a name="create-an-alert-using-pagerduty-in-the-azure-portal"></a>Créer une alerte à l’aide de PagerDuty dans le portail Azure
### <a name="for-a-new-action-group"></a>Pour un nouveau groupe d’action :
1. Suivez les étapes 1 à 8 de [Créer une alerte sur une notification sur l’intégrité du service pour un nouveau groupe d’actions à l’aide du portail Azure](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).

2. À définir dans la liste des **Actions** :

    a. **Type d’action :** *Webhook*

    b. **Détails :** **URL d’intégration** PagerDuty précédemment enregistrée.

    c. **Nom** : nom, alias ou identificateur du Webhook.

3. Quand vous avez terminé, sélectionnez **Enregistrer** pour créer l’alerte.

### <a name="for-an-existing-action-group"></a>Pour un groupe d’actions existant :
1. Dans le [portail Azure](https://portal.azure.com/), sélectionnez **Moniteur**.

2. Dans la section **Paramètres**, sélectionnez **Groupes d’actions**.

3. Recherchez et sélectionnez le groupe d’actions que vous souhaitez modifier.

4. À ajouter à la liste des **Actions** :

    a. **Type d’action :** *Webhook*

    b. **Détails :** **URL d’intégration** PagerDuty précédemment enregistrée.

    c. **Nom** : nom, alias ou identificateur du Webhook.

5. Quand vous avez terminé, sélectionnez **Enregistrer** pour mettre à jour le groupe d’actions.

## <a name="testing-your-webhook-integration-via-an-http-post-request"></a>Tester l’intégration à Webhook via une demande HTTP POST
1. Créez la charge utile d’intégrité du service que vous souhaitez envoyer. Vous trouverez un exemple de charge utile du Webhook d’intégrité du service sur la page [Webhook des alertes du journal d’activité Azure](../monitoring-and-diagnostics/monitoring-activity-log-alerts-webhook.md).

2. Créez une requête HTTP POST comme suit :

    ```
    POST        https://events.pagerduty.com/integration/<IntegrationKey>/enqueue

    HEADERS     Content-Type: application/json

    BODY        <Service Health payload>
    ```
3. Vous devez recevoir un `202 Accepted` avec un message contenant votre ID d’événement.

4. Accédez à [PagerDuty](https://www.pagerduty.com/) pour confirmer que votre intégration a été définie avec succès.

## <a name="next-steps"></a>Étapes suivantes
- Découvrez comment [configurer des notifications de webhook pour les systèmes de gestion de problème existants](service-health-alert-webhook-guide.md).
- Consultez le [schéma webhook des alertes de journal d’activité](../monitoring-and-diagnostics/monitoring-activity-log-alerts-webhook.md). 
- En savoir plus sur les [notifications sur l’intégrité du service](../monitoring-and-diagnostics/monitoring-service-notifications.md).
- En savoir plus sur les [groupes d’actions](../monitoring-and-diagnostics/monitoring-action-groups.md).