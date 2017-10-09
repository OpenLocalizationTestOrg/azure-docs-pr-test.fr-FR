---
title: "récupération d’aaaDisaster pour le compte d’intégration B2B - Azure Logic Apps | Documents Microsoft"
description: "Récupération d’urgence Logic Apps B2B"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Récupération d’urgence inter-régions Logic Apps B2B

Les charges de travail B2B impliquent des transactions monétaires telles que des commandes et des factures. Lors d’un événement d’urgence, il est essentiel pour un Bonjour de toomeet business tooquickly récupérer au niveau de l’entreprise SLA convenu avec leurs partenaires. Cet article explique comment planifier des toobuild une continuité des activités pour les charges de travail B2B. 

* Préparation à la récupération d’urgence 
* Basculer la région toosecondary pendant un événement d’urgence 
* Revenir tooprimary région après un sinistre

## <a name="disaster-recovery-readiness"></a>Préparation à la récupération d’urgence  

1. Identifiez une zone secondaire et créez un [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) dans la région secondaire hello.

2. Ajouter des partenaires, des schémas et des accords pour le flux de messages hello requis où hello statut d’exécution doit toobe répliquée toosecondary région intégration compte.

   > [!TIP]
   > Assurez-vous que la convention de dénomination d’artefact hello intégration compte est la cohérence entre les régions. 

3. hello toopull état d’exécution à partir de la région principale de hello, créez une application de logique dans la région secondaire hello. 

   L’application logique doit disposer d’un *déclencheur* et d’une *action*. 
   déclencheur de Hello doit connecter des compte d’intégration tooprimary région, et action de hello doit au compte d’intégration toosecondary région. 
   En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table d’état région principale exécuter hello et extrait les nouveaux enregistrements de hello, le cas échéant. Hello met à jour leur compte d’intégration toosecondary région. 
   Cela permet d’état d’exécution incrémentielle du tooget à partir de la région de toosecondary région principale.

4. Continuité des activités dans les applications de la logique de compte d’intégration est conçu toosupport basée sur des protocoles B2B - X12, AS2 et EDIFACT. toofind les étapes détaillées, sélectionnez hello les liens correspondants.

5. Hello recommandation est toodeploy toutes les ressources de région principale dans une région secondaire de trop. 

   Ressources de la région principale incluent la base de données SQL Azure ou base de données Azure Cosmos, Azure Service Bus et concentrateurs d’événements Azure utilisé pour la messagerie, la gestion des API Azure et la fonctionnalité d’Azure Logic Apps hello dans Azure App Service.   

6. Établir une connexion à partir d’une région secondaire tooa de région principale. hello toopull état d’exécution à partir d’une région primaire, créez une application de logique dans une région secondaire. 

   application de la logique de Hello doit avoir un déclencheur et une action. 
   déclencheur de Hello doit se connecter à compte d’intégration tooa région principale. 
   action de Hello doit se connecter à compte d’intégration tooa région secondaire. 
   En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table d’état région principale exécuter hello et extrait les nouveaux enregistrements de hello, le cas échéant. 
   Hello met à jour leur compte d’intégration tooa région secondaire. 
   Ce processus permet d’état d’exécution incrémentielle du tooget à partir de la région de hello région principale toohello secondaire.

Continuité des activités dans un compte d’intégration Logic Apps fournit la prise en charge basée sur des protocoles B2B de hello X12, AS2 et EDIFACT. Pour obtenir des instructions détaillées sur l’utilisation de X12 et AS2, consultez les sections de cet articles consacrées à [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) et [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2).

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>Basculer la région secondaire tooa pendant un événement d’urgence

Lors d’un événement d’urgence, lorsque la région principale de hello n’est pas disponible pour la continuité des activités, région secondaire toohello de diriger le trafic. Vous aide à une région secondaire un toorecover entreprise fonctions rapidement toomeet hello RPO/RTO convenu par leurs partenaires. Elle réduit également efforts toofail sur à partir de la région de tooanother d’une région. 

Il existe une latence attendue lors de la copie des numéros de contrôle à partir d’une région secondaire tooa de région principale. tooavoid envoi contrôle généré en double chiffres toopartners pendant un événement d’urgence, de recommandation de hello est tooincrement des numéros de contrôle hello dans les contrats de région secondaire hello à l’aide de [applets de commande PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>Revenir à des événements de post-incident tooa région principale

région principale toofall tooa arrière lorsqu’il est disponible, procédez comme suit :

1. Arrêter d’accepter les messages de partenaires dans la région secondaire hello.  

2. Incrémenter les numéros de contrôle hello généré pour tous les contrats de région principale hello à l’aide de [applets de commande PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).  

3. Trafic directement à partir de la région principale du toohello hello région secondaire.

4. Vérifiez que cette application logique de hello créée dans la région secondaire de hello pour extraire l’état d’exécution à partir de la région principale de hello est activée.

## <a name="x12"></a>X 12 

La continuité des activités pour les documents EDI X12 documents repose sur les numéros de contrôle :

> [!TIP]
> Vous pouvez également utiliser hello [X12 rapide démarrer modèle](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logique applications. Création de comptes d’intégration principaux et secondaires est des conditions préalables toouse hello par modèle. Hello modèle permet de toocreate deux applications de logique, une pour les numéros de contrôle reçu et l’autre pour les numéros de contrôle généré. Actions et déclencheurs respectifs sont créées dans les applications logique hello, connexion hello déclencheur toohello principal compte d’intégration et le compte d’intégration secondaire toohello hello action.

**Configuration requise**

tooenable la récupération d’urgence pour les messages entrants, sélectionnez les paramètres de vérification des doublons de hello dans les paramètres de réception de l’accord hello X12.

![Sélectionnez les paramètres de vérification des doublons](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. Créez une [application logique](../logic-apps/logic-apps-create-a-logic-app.md) dans la région secondaire.    

2. Lancez une recherche sur **X12** et sélectionnez **X12 - Lors de la modification d’un numéro de contrôle**.   

   ![Recherchez X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   déclencheur de Hello invite tooestablish un compte de connexion d’intégration tooan. 
   Hello déclencheur doit être connecté de compte d’intégration tooa région principale.

3. Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région principale* de hello liste, puis choisissez **créer**.   

   ![Nom du compte d’intégration de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. Hello **toostart DateTime synchronisation des numéro de contrôle** paramètre est facultatif. Hello **fréquence** peut être défini trop**jour**, **heure**, **Minute**, ou **deuxième** avec un intervalle.   

   ![Date/heure et fréquence](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. Sélectionnez **Nouvelle étape** > **Ajouter une action**.

   ![Nouvelle étape, puis Ajouter une action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. Lancez une recherche sur **X12** et sélectionnez **X12 - Ajouter ou mettre à jour des numéros de contrôle**.   

   ![Ajoutez ou mettez à jour les numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. tooconnect compte d’action tooa région secondaire intégration, sélectionnez **modifier la connexion** > **ajouter une nouvelle connexion** pour obtenir la liste des comptes d’intégration disponibles hello. Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région secondaire* de hello liste, puis choisissez **créer**. 

   ![Nom du compte d’intégration de la région secondaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. Basculez tooraw entrées en cliquant sur l’icône de hello dans le coin supérieur droit.

   ![Commutateur tooraw entrées](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. Sélectionnez corps dans le sélecteur de contenu dynamique hello et enregistrez l’application logique de hello.

   ![Champs de contenu dynamique](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table numéro de contrôle de région primaire reçue hello et extrait les nouveaux enregistrements de hello. 
   action de Hello met à jour les enregistrements de hello dans le compte d’intégration hello région secondaire. 
   S’il n’y a aucune mise à jour, l’état de déclencheur hello apparaît comme **ignoré**.   

   ![Table des numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

État d’exécution incrémentielle du hello selon l’intervalle de temps hello, réplique à partir d’une région secondaire tooa de région principale. Lors d’un événement d’urgence, lorsque la région primaire hello n’est pas région secondaire de toohello du trafic direct disponible pour la continuité d’activité. 

## <a name="edifact"></a>EDIFACT 

La continuité des activités pour les documents EDI EDIFACT repose sur les numéros de contrôle.

**Configuration requise**

tooenable la récupération d’urgence pour les messages entrants, sélectionnez les paramètres de vérification des doublons hello dans les paramètres de réception de votre accord EDIFACT.

![Sélectionnez les paramètres de vérification des doublons](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. Créez une [application logique](../logic-apps/logic-apps-create-a-logic-app.md) dans la région secondaire.    

2. Lancez une recherche sur **EDIFACT** et sélectionnez **EDIFACT - Lors de la modification d’un numéro de contrôle**.

   ![Recherchez EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   déclencheur de Hello invite tooestablish un compte de connexion d’intégration tooan. 
   Hello déclencheur doit être connecté de compte d’intégration tooa région principale. 

3. Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région principale* de hello liste, puis choisissez **créer**.    

   ![Nom du compte d’intégration de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. Hello **toostart DateTime synchronisation des numéro de contrôle** paramètre est facultatif. Hello **fréquence** peut être défini trop**jour**, **heure**, **Minute**, ou **deuxième** avec un intervalle.    

   ![Date/heure et fréquence](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. Sélectionnez **Nouvelle étape** > **Ajouter une action**.    

   ![Nouvelle étape, puis Ajouter une action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. Lancez une recherche sur **EDIFACT** et sélectionnez **EDIFACT - Ajouter ou mettre à jour des numéros de contrôle**.   

   ![Ajoutez ou mettez à jour les numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. tooconnect compte d’action tooa région secondaire intégration, sélectionnez **modifier la connexion** > **ajouter une nouvelle connexion** pour obtenir la liste des comptes d’intégration disponibles hello. Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région secondaire* de hello liste, puis choisissez **créer**.

   ![Nom du compte d’intégration de la région secondaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. Basculez tooraw entrées en cliquant sur l’icône de hello dans le coin supérieur droit.

   ![Commutateur tooraw entrées](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. Sélectionnez corps dans le sélecteur de contenu dynamique hello et enregistrez l’application logique de hello.   

   ![Champs de contenu dynamique](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table numéro de contrôle de région primaire reçue hello et extrait les nouveaux enregistrements de hello.
   action de Hello met à jour le compte d’intégration hello enregistrements toohello région secondaire. 
   S’il n’y a aucune mise à jour, l’état de déclencheur hello apparaît comme **ignoré**.

   ![Table des numéros de contrôle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

État d’exécution incrémentielle du hello selon l’intervalle de temps hello, réplique à partir d’une région secondaire tooa de région principale. Lors d’un événement d’urgence, lorsque la région primaire hello n’est pas région secondaire de toohello du trafic direct disponible pour la continuité d’activité. 

## <a name="as2"></a>AS2 

Continuité des activités pour les documents qui utilisent le protocole de AS2 hello est basée sur les ID de message hello et la valeur MIC hello.

> [!TIP]
> Vous pouvez également utiliser hello [modèle de démarrage rapide AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logique applications. Création de comptes d’intégration principaux et secondaires est des conditions préalables toouse hello par modèle. modèle de Hello permet de créer une application de la logique qui a un déclencheur et une action. application de la logique de Hello crée une connexion à partir d’un compte d’intégration principal tooa déclencheur et un compte d’action tooa intégration secondaire.

1. Créer un [application logique](../logic-apps/logic-apps-create-a-logic-app.md) dans la région secondaire hello.  

2. Recherchez **AS2** et sélectionnez **AS2 - Lorsqu’une valeur MIC est créée**.   

   ![Recherchez AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   Un déclencheur vous invite tooestablish un compte de connexion d’intégration tooan. 
   Hello déclencheur doit être connecté de compte d’intégration tooa région principale. 
   
3. Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région principale* de hello liste, puis choisissez **créer**.

   ![Nom du compte d’intégration de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. Hello **synchronisation de valeur DateTime toostart MIC** paramètre est facultatif. Hello **fréquence** peut être défini trop**jour**, **heure**, **Minute**, ou **deuxième** avec un intervalle.   

   ![Date/heure et fréquence](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. Sélectionnez **Nouvelle étape** > **Ajouter une action**.  

   ![Nouvelle étape, puis Ajouter une action](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. Recherchez **AS2** et sélectionnez **AS2 - Ajouter ou mettre à jour les contenus MIC**.  

   ![Ajout ou mise à jour d’un MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. tooconnect compte secondaire intégration tooa d’action, sélectionnez **modifier la connexion** > **ajouter une nouvelle connexion** pour obtenir la liste des comptes d’intégration disponibles hello. Entrez un nom de connexion, sélectionnez votre *compte d’intégration de région secondaire* de hello liste, puis choisissez **créer**.

   ![Nom du compte d’intégration de la région secondaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. Basculez tooraw entrées en cliquant sur l’icône de hello dans le coin supérieur droit.

   ![Commutateur tooraw entrées](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. Sélectionnez corps dans le sélecteur de contenu dynamique hello et enregistrez l’application logique de hello.   

   ![Contenu dynamique](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   En fonction de l’intervalle de temps hello, le déclencheur de hello interroge la table de région principale hello et extrait les nouveaux enregistrements de hello. Hello met à jour leur compte d’intégration toohello région secondaire. 
   S’il n’y a aucune mise à jour, l’état de déclencheur hello apparaît comme **ignoré**.  

   ![Table de la région primaire](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

État d’exécution incrémentielle du hello selon l’intervalle de temps hello, réplique à partir de la région de hello région principale toohello secondaire. Lors d’un événement d’urgence, lorsque la région primaire hello n’est pas région secondaire de toohello du trafic direct disponible pour la continuité d’activité. 

## <a name="next-steps"></a>Étapes suivantes

[Surveiller les messages B2B](logic-apps-monitor-b2b-message.md)

