---
title: les transactions aaaMonitor B2B et de journalisation - Azure Logic Apps | Documents Microsoft
description: "Surveiller les messages AS2, X12 et EDIFACT, démarrer la journalisation des diagnostics pour votre compte d’intégration"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a>Surveiller et configurer la journalisation des diagnostics pour la communication B2B dans des comptes d’intégration

Une fois la communication B2B configurée entre deux processus ou applications d’entreprise en cours d’exécution via votre compte d’intégration, ces entités peuvent échanger des messages entre elles. tooconfirm cette communication fonctionne comme prévu, vous pouvez définir la surveillance pour AS2, X12, et les messages EDIFACT, ainsi que de la journalisation des diagnostics pour votre compte d’intégration via hello [Analytique de journal Azure](../log-analytics/log-analytics-overview.md) service. Ce service dans [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) surveille vos environnements cloud et local pour vous aider à maintenir leur disponibilité et leurs performances, et collecte des détails d’exécution et des événements pour un débogage enrichi. Vous pouvez également [utiliser vos données de diagnostic avec d’autres services](#extend-diagnostic-data), tels que Stockage Azure et Azure Event Hubs.

## <a name="requirements"></a>Configuration requise

* Une application logique configurée avec une journalisation des diagnostics. En savoir plus [comment tooset configure une journalisation pour cette application logique](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

  > [!NOTE]
  > Une fois que vous avez répondu cette exigence, vous devez disposer d’un espace de travail Bonjour [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Vous devez utiliser hello même espace de travail OMS lorsque vous configurez la journalisation pour votre compte d’intégration. Si vous n’avez pas un espace de travail OMS, Découvrez [comment toocreate un espace de travail OMS](../log-analytics/log-analytics-get-started.md).

* Un compte d’intégration qui a lié tooyour logique application. En savoir plus [comment toocreate une intégration compte avec une application de la logique de lien tooyour](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a>Activer la journalisation des diagnostics pour votre compte d’intégration

Vous pouvez activer la journalisation directement à partir de votre compte d’intégration ou [via hello service Azure moniteur](#azure-monitor-service). Azure Monitor exerce une surveillance de base avec des données de niveau de l’infrastructure. En savoir plus sur [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a>Activer la journalisation des diagnostics directement à partir de votre compte d’intégration

1. Bonjour [portail Azure](https://portal.azure.com), recherchez et sélectionnez votre compte de l’intégration. Sous **Surveillance**, choisissez **Journaux de diagnostic** comme illustré ici :

   ![Rechercher et sélectionner votre compte d’intégration, choisissez « Journaux de diagnostic »](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. Une fois que vous sélectionnez votre compte d’intégration, hello valeurs suivantes est automatiquement sélectionné. Si ces valeurs sont correctes, choisissez **Activer les diagnostics**. Sinon, sélectionnez les valeurs hello que vous voulez :

   1. Sous **abonnement**, sélectionnez hello abonnement Azure que vous utilisez avec votre compte d’intégration.
   2. Sous **groupe de ressources**, sélectionnez groupe de ressources hello que vous utilisez avec votre compte d’intégration.
   3. Sous **Type de ressource**, sélectionnez **Comptes d'intégration**. 
   4. Sous **Ressource**, sélectionnez votre compte d’intégration. 
   5. Choisissez **Activer les diagnostics**.

   ![Configurer les diagnostics pour votre compte d’intégration](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. Sous **Paramètres de diagnostic**, puis **État**, choisissez **Activé**.

   ![Activer Azure Diagnostics](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Sélectionnez maintenant, hello OMS espace de travail et les données toouse pour la journalisation comme indiqué :

   1. Sélectionnez **envoyer tooLog Analytique**. 
   2. Sous **Log Analytics**, choisissez **Configurer**. 
   3. Sous **espaces de travail OMS**, sélectionnez toouse d’espace de travail OMS hello pour la journalisation.
   4. Sous **journal**, sélectionnez hello **IntegrationAccountTrackingEvents** catégorie.
   5. Choisissez **Enregistrer**.

   ![Configurer Analytique de journal et d’envoyer un journal de tooa de données de diagnostic](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. À présent, [configurez le suivi de vos messages B2B dans OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a>Activer la journalisation des diagnostics via Azure Monitor

1. Bonjour [portail Azure](https://portal.azure.com), on hello menu Azure principal, choisissez **moniteur**, **les journaux de diagnostic**. Sélectionnez ensuite votre compte d’intégration comme illustré ici :

   ![Choisir « Surveiller », « Journaux de diagnostic », sélectionner votre compte d’intégration](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. Une fois que vous sélectionnez votre compte d’intégration, hello valeurs suivantes est automatiquement sélectionné. Si ces valeurs sont correctes, choisissez **Activer les diagnostics**. Sinon, sélectionnez les valeurs hello que vous voulez :

   1. Sous **abonnement**, sélectionnez hello abonnement Azure que vous utilisez avec votre compte d’intégration.
   2. Sous **groupe de ressources**, sélectionnez groupe de ressources hello que vous utilisez avec votre compte d’intégration.
   3. Sous **Type de ressource**, sélectionnez **Comptes d'intégration**.
   4. Sous **Ressource**, sélectionnez votre compte d’intégration.
   5. Choisissez **Activer les diagnostics**.

   ![Configurer les diagnostics pour votre compte d’intégration](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. Sous **Paramètres de diagnostic**, choisissez **Activé**.

   ![Activer Azure Diagnostics](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Sélectionnez maintenant hello OMS espace de travail et les événements catégorie journalisation comme indiqué :

   1. Sélectionnez **envoyer tooLog Analytique**. 
   2. Sous **Log Analytics**, choisissez **Configurer**. 
   3. Sous **espaces de travail OMS**, sélectionnez toouse d’espace de travail OMS hello pour la journalisation.
   4. Sous **journal**, sélectionnez hello **IntegrationAccountTrackingEvents** catégorie.
   5. Une fois ces opérations effectuées, sélectionnez **Enregistrer**.

   ![Configurer Analytique de journal et d’envoyer un journal de tooa de données de diagnostic](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. À présent, [configurez le suivi de vos messages B2B dans OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Étendre la manière dont vous utilisez les données de diagnostic et l’emplacement où vous les utilisez avec d’autres services

Avec Azure Log Analytics, vous pouvez étendre le mode d’utilisation des données de diagnostic de votre application logique avec d’autres services Azure, par exemple : 

* [Archivage des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Flux de données des journaux de Diagnostics Azure tooAzure concentrateurs d’événements](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

Vous pouvez ensuite obtenir une surveillance en temps réel en utilisant les ressources de télémétrie et d’analyse d’autres services, tels que [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) et [Power BI](../log-analytics/log-analytics-powerbi.md). Par exemple :

* [Données de flux de données à partir de concentrateurs d’événements tooStream Analytique](../stream-analytics/stream-analytics-define-inputs.md)
* [Analyser les données de diffusion avec Stream Analytics et créer un tableau de bord analytique en temps réel dans Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)

Selon les options de hello que vous voulez configurer, assurez-vous que vous première [créer un compte de stockage Azure](../storage/common/storage-create-storage-account.md) ou [créer un concentrateur d’événements Azure](../event-hubs/event-hubs-create.md). Puis sélectionnez les options de hello où vous souhaitez toosend les données de diagnostic :

![Envoyer des données tooAzure stockage compte ou événement un concentrateur](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> Périodes de rétention s’appliquent uniquement lorsque vous choisissez un compte de stockage toouse.

## <a name="supported-tracking-schemas"></a>Schémas de suivi pris en charge

Azure prend en charge ces types de schéma, qui ont des schémas, sauf le type personnalisé de hello fixes de suivi.

* [Schéma de suivi AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Schéma de suivi X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Schéma de suivi personnalisé](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a>Étapes suivantes

* [Suivre les messages B2B dans OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Suivre les messages B2B dans OMS")
* [En savoir plus sur hello Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")

