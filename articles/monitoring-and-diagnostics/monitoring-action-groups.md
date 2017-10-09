---
title: "aaaCreate et gérer des groupes d’actions Bonjour portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate et gérer des groupes d’actions Bonjour portail Azure."
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>Créer et gérer des groupes d’actions Bonjour portail Azure
## <a name="overview"></a>Vue d'ensemble ##
Cet article vous montre comment toocreate et gérer des groupes d’actions Bonjour portail Azure.

Vous pouvez configurer une liste d’actions avec des groupes d’actions. Ces groupes peuvent alors servir pour définir des alertes du journal d’activité. Ces groupes peuvent ensuite être réutilisées par chaque alerte de journal d’activité que vous définissez, vous être assuré que hello même action chaque déclenchement de l’alerte de journal d’activité hello.

Un groupe d’actions peut avoir au plus too10 de chaque type d’action. Chaque action est constituée de hello propriétés suivantes :

* **Nom**: un identificateur unique au sein du groupe d’actions hello.  
* **Type d’action** : envoyer un SMS, envoyer un e-mail ou appeler un Webhook.  
* **Détails**: hello webhook URI, adresse de messagerie ou numéro de téléphone correspondant.

Pour plus d’informations sur la façon de toouse groupes d’actions modèles tooconfigure Azure Resource Manager, consultez [modèles de gestionnaire de ressources du groupe Action](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>Créer un groupe d’actions à l’aide de hello portail Azure ##
1. Bonjour [portal](https://portal.azure.com), sélectionnez **analyse**. Hello **moniteur** panneau consolide toutes vos paramètres de surveillance et données dans une vue.

    ![Hello service de « Analyse »](./media/monitoring-action-groups/home-monitor.png)
2. Bonjour **le journal d’activité** section, sélectionnez **groupes d’actions**.

    ![onglet de « Groupes d’actions » Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. Sélectionnez **ajouter un groupe action**et renseignez les champs hello.

    ![Hello « Ajouter un groupe d’actions » une commande](./media/monitoring-action-groups/add-action-group.png)
4. Entrez un nom dans hello **nom d’Action groupe** zone et entrez un nom dans hello **nom court** boîte. nom court de Hello est utilisé à la place d’un nom de groupe complet de l’action lorsque les notifications sont envoyées à l’aide de ce groupe.

      ![boîte de dialogue groupe d’actions Hello ajouter »](./media/monitoring-action-groups/action-group-define.png)

5. Hello **abonnement** zone autofills avec votre abonnement actuel. Cet abonnement est hello un dans le groupe d’actions hello est enregistré.

6. Sélectionnez hello **groupe de ressources** dans l’action hello groupe est enregistré.

7. Définissez une liste d’actions en indiquant les éléments suivants pour chaque action :

    a. **Nom** : entrez un identificateur unique pour cette action.

    b. **Type d’action** : sélectionnez SMS, e-mail ou webhook.

    c. **Détails**: selon le type d’action hello, entrez un numéro de téléphone, une adresse de messagerie ou un webhook URI.

8. Sélectionnez **OK** groupe d’actions toocreate hello.

## <a name="manage-your-action-groups"></a>Gérer des groupes d’actions ##
Après avoir créé un groupe d’actions, il est visible dans hello **groupes d’actions** section Hello **moniteur** panneau. Sélectionnez hello action groupe toomanage à :

* Ajouter, modifier ou supprimer des actions.
* Supprimer le groupe d’actions hello.

## <a name="next-steps"></a>Étapes suivantes ##
* En savoir plus sur le [comportement des alertes SMS](monitoring-sms-alert-behavior.md).  
* Obtenir un [compréhension de schéma webhook alerte des journaux d’activité hello](monitoring-activity-log-alerts-webhook.md).  
* En savoir plus sur la [limitation de la fréquence](monitoring-alerts-rate-limiting.md) des alertes. 
* Obtenir un [vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md)et découvrez comment tooreceive alertes.  
* Découvrez comment trop[configurer des alertes lors de la validation d’une notification de contrôle d’intégrité du service](monitoring-activity-log-alerts-on-service-notifications.md).
