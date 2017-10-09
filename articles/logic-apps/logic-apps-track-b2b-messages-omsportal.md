---
title: messages aaaTrack B2B dans Operations Management Suite - Azure Logic Apps | Documents Microsoft
description: "Suivre la communication B2B pour votre compte d’intégration et vos applications logiques dans Operations Management Suite (OMS) avec Azure Log Analytics"
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
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>Effectuer le suivi de la communication B2B Bonjour Microsoft Operations Management Suite (OMS)

Une fois la communication B2B configurée entre deux processus ou applications d’entreprise en cours d’exécution via votre compte d’intégration, ces entités peuvent échanger des messages entre elles. toocheck si ces messages sont traités correctement, vous pouvez effectuer le suivi AS2, X12, et des messages EDIFACT avec [Analytique de journal Azure](../log-analytics/log-analytics-overview.md) Bonjour [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Par exemple, vous pouvez utiliser ces fonctionnalités de suivi basées sur le web pour suivre des messages :

* Nombre et état des messages
* État des accusés de réception
* Corrélation entre les messages et les accusés de réception
* Descriptions détaillées des erreurs en cas d’échec
* Fonctionnalités de recherche

## <a name="requirements"></a>Configuration requise

* Une application logique configurée avec une journalisation des diagnostics. En savoir plus [comment toocreate une application logique](logic-apps-create-a-logic-app.md) et [comment tooset configure une journalisation pour cette application logique](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Un compte d’intégration configuré avec une surveillance et une journalisation. En savoir plus [comment toocreate un compte d’intégration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) et [comment tooset de surveillance et la journalisation pour ce compte](../logic-apps/logic-apps-monitor-b2b-message.md).

* Si vous n’avez pas déjà fait, [publier des données de diagnostic tooLog Analytique](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) dans OMS.

> [!NOTE]
> Une fois que vous avez requise hello précédente, vous devez disposer d’un espace de travail Bonjour [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Vous devez utiliser hello même espace de travail OMS pour le suivi de vos communications B2B dans OMS. 
>  
> Si vous n’avez pas un espace de travail OMS, Découvrez [comment toocreate un espace de travail OMS](../log-analytics/log-analytics-get-started.md).

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>Ajouter hello logique applications B2B solution toohello Operations Management Suite (OMS)

toohave OMS effectuer le suivi des messages B2B pour votre application logique, vous devez ajouter hello **logique applications B2B** du portail OMS toohello solution. En savoir plus sur [Ajout de solutions tooOMS](../log-analytics/log-analytics-get-started.md).

1. Bonjour [portail Azure](https://portal.azure.com), choisissez **plus Services**. Recherchez « log analytics », puis choisissez **Log Analytics** comme illustré ici :

   ![Rechercher Log Analytics](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. Sous **Log Analytics**, recherchez et sélectionnez votre espace de travail OMS. 

   ![Sélectionner votre espace de travail OMS](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. Sous **Gestion**, choisissez **Portail OMS**.

   ![Choisir le portail OMS](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Une fois que la page d’accueil OMS hello s’ouvre, choisissez **galerie des Solutions**.    

   ![Choisir Galerie de solutions](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. Sous **Toutes les solutions**, recherchez et choisissez **Logic Apps B2B**.     

   ![Choisir Logic Apps B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. Sous **Logic Apps B2B**, choisissez **Ajouter**.

   ![Choisir Ajouter](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   Sur la page d’accueil OMS hello hello vignette pour **logique applications B2B Messages** maintenant s’affiche. 
   Cette vignette met à jour le nombre de messages hello lorsque vos messages B2B sont traités.

   ![Page d’accueil d’OMS, vignette Messages B2B Logic Apps](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>Suivre l’état des messages et les détails dans hello Operations Management Suite

1. Une fois vos messages B2B sont traités, vous pouvez afficher l’état de hello et les détails de ces messages. Dans la page d’accueil hello OMS, choisissez hello **logique applications B2B Messages** vignette.

   ![Nombre de messages mis à jour](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > Par défaut, hello **logique applications B2B Messages** vignette affiche des données basées sur une journée. étendue de données de hello toochange l’intervalle tooa, choisissez le contrôle de la plage hello en hello haut hello OMS :
   > 
   > ![Modifier l’étendue des données](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. Après l’état du message hello tableau de bord s’affiche, vous pouvez afficher davantage de détails pour un type de message spécifique, qui affiche des données basées sur une journée. Choisissez la vignette hello pour **AS2**, **X12**, ou **EDIFACT**.

   ![Afficher l’état du message](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   Une liste de messages s’affiche pour la vignette choisie. 
   toolearn savoir plus sur les propriétés hello pour chaque type de message, consultez les descriptions de propriété de message :

   * [Propriétés de message AS2](#as2-message-properties)
   * [Propriétés de message X12](#x12-message-properties)
   * [Propriétés de message EDIFACT](#EDIFACT-message-properties)

   Par exemple, voici comment peut se présenter une liste de messages AS2 :

   ![Afficher les messages AS2](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. les entrées de hello tooview ou d’exportation et des sorties des messages spécifiques, sélectionnez ces messages et choisissez **télécharger**. Lorsque vous y êtes invité, enregistrez l’ordinateur local du tooyour fichier .zip hello et puis extraire ce fichier. 

   dossier d’extraction Hello inclut un dossier pour chaque message sélectionné. 
   Si vous définissez des accusés de réception, dossier de message hello comprend également des fichiers avec les détails de l’accusé de réception. 
   Chaque dossier de message comprend au moins les fichiers suivants : 
   
   * Les fichiers lisible par hello entrée détails de charge utile de charge utile et de sortie
   * Fichiers encodés avec hello entrées et sorties

   Pour chaque type de message, vous pouvez trouver le dossier de hello et formats de nom de fichier ici :

   * [Formats de nom de dossier et de fichier AS2](#as2-folder-file-names)
   * [Formats de nom de dossier et de fichier X12](#x12-folder-file-names)
   * [ EDIFACT](#edifact-folder-file-names)

   ![Télécharger les fichiers de message](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. tooview toutes les actions qui ont hello même ID de série, sur hello **recherche de journal** page, choisissez un message à partir de la liste des messages hello.

   Vous pouvez trier ces actions par colonne, ou rechercher des résultats spécifiques.

   ![Actions avec hello même ID de série](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * résultats toosearch avec des requêtes prédéfinies, choisissez **favoris**.

   * En savoir plus [fonctionnement des requêtes en ajoutant des filtres toobuild](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md). 
   En savoir plus sur [comment la recherche toofind des données avec le journal dans le journal Analytique](../log-analytics/log-analytics-log-searches.md).

   * requête toochange dans la zone de recherche de hello, requête de hello mise à jour avec les colonnes hello et les valeurs que vous souhaitez toouse en tant que filtres.

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>Formats de noms et descriptions de propriétés pour les messages AS2, X 12 et EDIFACT

Pour chaque type de message, voici les descriptions de propriété hello et formats de nom pour les fichiers de message téléchargé.

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>Description de propriétés des messages AS2

Voici les descriptions de propriété hello pour chaque message AS2.

| Propriété | Description |
| --- | --- |
| Sender | partenaire invité de Hello spécifié dans **paramètres de réception**, ou le partenaire d’accueil hello spécifié dans **paramètres d’envoi** pour un accord AS2 |
| Receiver | partenaire d’accueil Hello spécifié dans **paramètres de réception**, ou de partenaire invité de hello spécifiées dans **paramètres d’envoi** pour un accord AS2 |
| Application logique | application de la logique Hello où sont configurées les actions hello AS2 |
| État | Hello état du message AS2 <br>Success = a reçu ou envoyé un message AS2 valide. Aucun MDN n’est configuré. <br>Success = a reçu ou envoyé un message AS2 valide. MDN est configuré et reçu ou envoyé. <br>Failed = a reçu un message AS2 non valide. Aucun MDN n’est configuré. <br>Pending = a reçu ou envoyé un message AS2 valide. Un MDN est configuré et attendu. |
| Ack | Hello état du message MDN <br>Accepted = a reçu ou envoyé un MDN positif. <br>En attente = en attente tooreceive ou envoyer un MDN. <br>Rejected = a reçu ou envoyé un MDN négatif. <br>Non requis = MDN n’est pas configuré dans l’accord de hello. |
| Direction | Hello direction du message AS2 |
| ID de corrélation : | ID de Hello qui met en correspondance tous les déclencheurs de hello et les actions dans une application de logique |
| ID de message | ID de message Hello AS2 à partir des en-têtes de message hello AS2 |
| Timestamp | heure de Hello lorsque hello AS2 action du traitement de message de type hello |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>Formats de noms AS2 pour les fichiers de message téléchargés

Voici les formats de nom hello pour chaque dossier de message téléchargé AS2 et les fichiers.

| Fichier ou dossier | Format du nom |
| :------------- | :---------- |
| Dossier de message | [expéditeur] \_[récepteur]\_AS2\_[ID de corrélation]\_[ID de message]\_[horodatage] |
| Entrée, sortie et, si configurés, fichiers d’accusé de réception | **Charge utile d’entrée** : [expéditeur]\_[récepteur]\_AS2\_[ID de corrélation]\_input_payload.txt </p>**Charge utile de sortie** : [expéditeur]\_[récepteur]\_AS2\_[ID de corrélation]\_sortie\_payload.txt </p></p>**Entrées** : [expéditeur]\_[récepteur]\_AS2\_[ID de corrélation]\_inputs.txt </p></p>**Sorties** : [expéditeur]\_[récepteur]\_AS2\_[ID de corrélation]\_outputs.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>Description de propriétés des messages X12

Voici la description de propriété hello pour chaque X12 message.

| Propriété | Description |
| --- | --- |
| Sender | partenaire invité de Hello spécifié dans **paramètres de réception**, ou le partenaire d’accueil hello spécifié dans **paramètres d’envoi** pour une X12 contrat |
| Receiver | partenaire d’accueil Hello spécifié dans **paramètres de réception**, ou un partenaire invité hello spécifié dans **paramètres d’envoi** pour une X12 contrat |
| Application logique | application de la logique Hello où sont configurées les actions hello X12 |
| État | état du message Hello X12 <br>Success = a reçu ou envoyé un message X12 valide. Aucun accusé de réception fonctionnel configuré. <br>Success = a reçu ou envoyé un message X12 valide. Accusé de réception fonctionnel configuré et reçu ou envoyé. <br>Failed = a reçu ou envoyé un message X12 non valide. <br>Pending = a reçu ou envoyé un message X12 valide. Accusé de réception fonctionnel configuré et attendu. |
| Ack | État de l’accusé de réception fonctionnel (997) <br>Accepted = a reçu ou envoyé un accusé de réception positif. <br>Rejected = a reçu ou envoyé un accusé de réception négatif. <br>Pending = attendait un accusé de réception fonctionnel mais ne l’a pas reçu. <br>En attente = généré un accusé de réception fonctionnel, mais vous ne pouvez pas envoyer toopartner. <br>Not Required = accusé de réception fonctionnel non configuré. |
| Direction | direction du message Hello X12 |
| ID de corrélation : | ID de Hello qui met en correspondance tous les déclencheurs de hello et les actions dans une application de logique |
| Type de message | type de message 12 EDI X de Hello |
| ICN | Hello numéro de contrôle de l’échange de message de type hello X12 |
| TSCN | Hello numéro de contrôle de document informatisé pour le message de type hello X12 |
| Timestamp | heure de Hello lorsque action de hello X12 du traitement de message de type hello |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>Formats de noms X12 pour les fichiers de message téléchargés

Voici les formats de nom hello pour chaque téléchargées X12 dossier et les fichiers de message.

| Fichier ou dossier | Format du nom |
| :------------- | :---------- |
| Dossier de message | [expéditeur] \_[récepteur]\_X12\_[numéro de contrôle d’échange]\_[numéro de contrôle global]\_[numéro de contrôle de document informatisé]\_[horodatage] |
| Entrée, sortie et, si configurés, fichiers d’accusé de réception | **Charge utile d’entrée**: [expéditeur]\_[récepteur]\_X12\_[numéro de contrôle d’échange]\_input_payload.txt </p>**Charge utile de sortie**: [expéditeur]\_[récepteur]\_X12\_[numéro de contrôle d’échange]\_sortie\_payload.txt </p></p>**Entrées**: [expéditeur]\_[récepteur]\_X12\_[numéro de contrôle d’échange]\_inputs.txt </p></p>**Sorties**: [expéditeur]\_[récepteur]\_X12\_[numéro de contrôle d’échange]\_outputs.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>Description de propriétés des messages EDIFACT

Voici les descriptions de propriété hello pour chaque message EDIFACT.

| Propriété | Description |
| --- | --- |
| Sender | partenaire invité de Hello spécifié dans **paramètres de réception**, ou le partenaire d’accueil hello spécifié dans **paramètres d’envoi** pour un accord EDIFACT |
| Receiver | partenaire d’accueil Hello spécifié dans **paramètres de réception**, ou de partenaire invité de hello spécifiées dans **paramètres d’envoi** pour un accord EDIFACT |
| Application logique | application de la logique Hello où configurer des actions d’EDIFACT hello |
| État | Hello état du message EDIFACT <br>Success = a reçu ou envoyé un message EDIFACT valide. Aucun accusé de réception fonctionnel configuré. <br>Success = a reçu ou envoyé un message EDIFACT valide. Accusé de réception fonctionnel configuré et reçu ou envoyé. <br>Failed = a reçu ou envoyé un message EDIFACT non valide. <br>Pending = a reçu ou envoyé un message EDIFACT valide. Accusé de réception fonctionnel configuré et attendu. |
| Ack | État de l’accusé de réception fonctionnel (997) <br>Accepted = a reçu ou envoyé un accusé de réception positif. <br>Rejected = a reçu ou envoyé un accusé de réception négatif. <br>Pending = attendait un accusé de réception fonctionnel mais ne l’a pas reçu. <br>En attente = généré un accusé de réception fonctionnel, mais vous ne pouvez pas envoyer toopartner. <br>Not Required = accusé de réception fonctionnel non configuré. |
| Direction | Hello direction du message EDIFACT |
| ID de corrélation : | ID de Hello qui met en correspondance tous les déclencheurs de hello et les actions dans une application de logique |
| Type de message | Hello, type de message EDIFACT |
| ICN | Hello numéro de contrôle de l’échange de message de type hello EDIFACT |
| TSCN | Hello numéro de contrôle de document informatisé pour le message de salutation EDIFACT |
| Timestamp | heure de Hello lorsque hello action d’EDIFACT du traitement de message de type hello |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>Formats de noms EDIFACT pour les fichiers de message téléchargés

Voici les formats de nom hello pour chaque dossier de message EDIFACT téléchargé et les fichiers.

| Fichier ou dossier | Format du nom |
| :------------- | :---------- |
| Dossier de message | [expéditeur] \_[récepteur]\_EDIFACT\_[numéro de contrôle d’échange]\_[numéro de contrôle global]\_[numéro de contrôle de document informatisé]\_[horodatage] |
| Entrée, sortie et, si configurés, fichiers d’accusé de réception | **Charge utile d’entrée**: [expéditeur]\_[récepteur]\_EDIFACT\_[numéro de contrôle d’échange]\_input_payload.txt </p>**Charge utile de sortie**: [expéditeur]\_[récepteur]\_EDIFACT\_[numéro de contrôle d’échange]\_sortie\_payload.txt </p></p>**Entrées**: [expéditeur]\_[récepteur]\_EDIFACT\_[numéro de contrôle d’échange]\_inputs.txt </p></p>**Sorties**: [expéditeur]\_[récepteur]\_EDIFACT\_[numéro de contrôle d’échange]\_outputs.txt |
|          |             |

## <a name="next-steps"></a>Étapes suivantes

* [Interroger des messages B2B dans Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [Schémas de suivi AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Schémas de suivi X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Schémas de suivi personnalisé](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)