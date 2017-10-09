---
title: "alertes de journal d’activité aaaCreate | Documents Microsoft"
description: "Recevoir des alertes par courrier électronique, SMS et webhook lorsque certains événements se produisent dans le journal d’activité hello."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>Créer des alertes de journal d’activité

## <a name="overview"></a>Vue d'ensemble
Alertes de journal d’activité sont des alertes qui activent lorsqu’un nouvel événement de journal d’activité qui produit correspond aux conditions de hello spécifiées dans l’alerte de hello. Il s’agit de ressources Azure, et peuvent donc être créées à l’aide d’un modèle Azure Resource Manager. Ils également peuvent être créés, mis à jour ou supprimés dans hello portail Azure. Cet article présente les concepts de hello alertes de journal d’activité. Il vous montre ensuite comment toouse hello Azure tooset portail d’une alerte sur les événements de journal d’activité.

En général, vous créez alertes de journal d’activité tooreceive notifications lorsque :

* Modifications spécifiques se produisent sur les ressources dans votre abonnement Azure, les groupes de ressources tooparticular souvent étendue ou les ressources. Par exemple, vous pourriez toobe notifié lorsqu’un ordinateur virtuel de myProductionResourceGroup est supprimé. Ou bien, vous souhaiterez toobe averti si de nouveaux rôles assignés utilisateur tooa dans votre abonnement.
* Un événement d’intégrité du service se produit. Événements de contrôle d’intégrité de service incluent la notification des incidents et des événements de maintenance qui s’appliquent tooresources dans votre abonnement.

Dans les deux cas, une alerte de journal d’activité analyse uniquement pour les événements dans l’abonnement hello dans le hello alerte est créée.

Vous pouvez configurer une alerte de journal d’activité basée sur n’importe quelle propriété de niveau supérieur dans l’objet JSON de hello pour un événement de journal d’activité. Toutefois, portail de hello montre les options les plus courantes hello :

- **Catégorie** : administration, intégrité du service, mise à l’échelle automatique et recommandation. Pour plus d’informations, consultez [vue d’ensemble du journal des activités Windows Azure hello](./monitoring-overview-activity-logs.md#categories-in-the-activity-log). toolearn en savoir plus sur les événements de contrôle d’intégrité du service, consultez [recevoir des alertes de journal d’activité sur les notifications de service](./monitoring-activity-log-alerts-on-service-notifications.md).
- **Groupe de ressources**
- **Ressource**
- **Type de ressource**
- **Nom de l’opération**: nom de l’opération hello contrôle d’accès en fonction du rôle Resource Manager.
- **Niveau**: hello de niveau de gravité d’événement hello (commentaires, information, avertissement, erreur ou critique).
- **État**: état hello d’événement hello, généralement démarrées, a échoué ou a réussi.
- **Événement déclenché par**: également appelé hello « appelant ». adresse de messagerie Hello ou identificateur d’Azure Active Directory de l’utilisateur hello qui a effectué l’opération de hello.

>[!NOTE]
>Vous devez spécifier au moins deux des hello précédant les critères dans l’alerte, étant une catégorie de hello. Vous ne pouvez pas créer une alerte active chaque fois qu’un événement est créé dans le journal d’activité de hello.
>
>

Lorsqu’une alerte de journal d’activité est activée, il utilise une action de groupe toogenerate actions ou les notifications. Un groupe d’actions est un jeu réutilisable de destinataires de notifications, telles que des adresses de messagerie, des URL webhook ou des numéros de téléphone SMS. les récepteurs Hello peuvent être référencées à partir de plusieurs alertes toocentralize et regroupement vos canaux de notification. Lorsque vous définissez votre alerte de journal d’activité, vous avez deux options. Vous pouvez :

* utiliser un groupe d’actions existant dans votre alerte de journal d’activité. 
* créer un nouveau groupe d’action. 

toolearn savoir plus sur les groupes d’actions, consultez [créer et gérer des groupes d’actions Bonjour Azure portal](monitoring-action-groups.md).

toolearn en savoir plus sur les notifications de contrôle d’intégrité du service, consultez [recevoir des alertes de journal d’activité sur les notifications de contrôle d’intégrité de service](monitoring-activity-log-alerts-on-service-notifications.md).

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>Créer une alerte sur un événement de journal d’activité avec un nouveau groupe d’actions à l’aide de hello portail Azure
1. Bonjour [portal](https://portal.azure.com), sélectionnez **analyse**.

    ![Hello service de « Analyse »](./media/monitoring-activity-log-alerts/home-monitor.png)
2. Bonjour **le journal d’activité** section, sélectionnez **alertes**.

    ![onglet de « Alertes » Hello](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. Sélectionnez **ajouter une alerte journal activité**et renseignez les champs hello.

4. Entrez un nom dans hello **nom de l’alerte activité journal** et sélectionnez un **Description**.

    ![Hello « Ajouter une alerte de journal d’activité » de commande](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. Hello **abonnement** zone autofills avec votre abonnement actuel. Cet abonnement est hello un dans le groupe d’actions hello est enregistré. ressources d’alerte Hello est toothis déployé abonnement et des analyses journal des événements d’activité à partir de celui-ci.

    ![boîte de dialogue « Ajouter une alerte de journal d’activité » Hello](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. Sélectionnez hello **groupe de ressources** les Bonjour ressource alerte est créée. Il ne s’agit pas de groupe de ressources hello qui est surveillé par l’alerte de hello. Au lieu de cela, il s’agit de groupe de ressources de hello où se trouve la ressource d’alerte hello.

7. Si vous le souhaitez, sélectionnez une **catégorie d’événement** toomodify hello des filtres supplémentaires sont affichés. Pour les événements d’administration, les filtres de hello incluent **groupe de ressources**, **ressource**, **type de ressource**, **nom de l’opération**, **Niveau**, **état**, et **événement déclenché par**. Ces valeurs identifient les événements que cette alerte doit surveiller.

    >[!NOTE]
    >Vous devez spécifier au moins un des hello précédant les critères dans l’alerte. Vous ne pouvez pas créer une alerte active chaque fois qu’un événement est créé dans le journal d’activité de hello.
    >
    >

8. Entrez un nom dans hello **nom d’Action groupe** zone et entrez un nom dans hello **nom court** boîte. nom court de Hello est utilisé à la place d’un nom de groupe complet de l’action lorsque les notifications sont envoyées à l’aide de ce groupe.

9.  Définir une liste d’actions en fournissant l’action hello :

    a. **Nom**: entrez le nom d’action hello, alias ou identificateur.

    b. **Type d’action** : sélectionnez SMS, e-mail ou webhook.

    c. **Détails**: selon le type d’action hello, entrez un numéro de téléphone, une adresse de messagerie ou un webhook URI.

10. Sélectionnez **OK** alerte de hello toocreate.

alerte de Hello prend quelques minutes toofully propager et deviennent alors actifs. Elle se déclenche lorsque de nouveaux événements correspondent aux critères de l’alerte hello.

Pour plus d’informations, consultez [schéma de webhook hello comprendre utilisée dans les alertes de journal d’activité](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>groupe d’actions Hello définie dans ces étapes est réutilisable en tant qu’un groupe d’actions existant pour toutes les définitions d’alerte futures.
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>Créer une alerte sur un événement de journal d’activité pour un groupe d’actions à l’aide de hello portail Azure
1. Suivez les étapes 1 à 7 dans hello précédente section toocreate votre alerte de journal d’activité.

2. Sous **notifier**, sélectionnez hello **existant** bouton d’action de groupe. Sélectionnez un groupe d’actions existant à partir de la liste de hello.

3. Sélectionnez **OK** alerte de hello toocreate.

alerte de Hello prend quelques minutes toofully propager et deviennent alors actifs. Elle se déclenche lorsque de nouveaux événements correspondent aux critères de l’alerte hello.

## <a name="manage-your-alerts"></a>Gérez vos alertes

Après avoir créé une alerte, elle est visible dans la section d’alertes hello du panneau d’analyse hello. Sélectionnez l’alerte hello toomanage à :

* la modifier
* la supprimer
* Désactiver ou activer, si vous souhaitez tootemporarily arrêter ou reprenez la réception des notifications d’alerte de hello.

## <a name="next-steps"></a>Étapes suivantes
- Obtenir une [vue d’ensemble des alertes](monitoring-overview-alerts.md).
- En savoir plus sur la [limitation du débit des notifications](monitoring-alerts-rate-limiting.md).
- Hello de révision [webhook alerte schéma des journaux d’activité](monitoring-activity-log-alerts-webhook.md).
- En savoir plus sur les [groupes d’actions](monitoring-action-groups.md).  
- En savoir plus sur les [notifications sur l’intégrité du service](monitoring-service-notifications.md).
- Créer un [activité journal toutes les opérations du moteur de mise à l’échelle de votre abonnement d’alerte toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Créer un [activité journal toutes les opérations de montée/échelle Échec de mise à l’échelle de votre abonnement d’alerte toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
