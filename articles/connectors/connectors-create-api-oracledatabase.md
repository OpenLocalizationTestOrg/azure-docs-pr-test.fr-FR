---
title: "connecteur de base de données Oracle aaaAdd hello dans vos applications de la logique de Azure | Documents Microsoft"
description: "Utiliser le connecteur de base de données Oracle hello dans une application de logique"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Prise en main connecteur de base de données Oracle hello

À l’aide du connecteur de base de données Oracle hello, créer des workflows d’organisation qui utilisent des données dans votre base de données existante. Ce connecteur peut se connecter tooan de base de données Oracle locale ou une machine virtuelle Azure avec la base de données Oracle installée. Avec ce connecteur, vous pouvez :

* Créer votre flux de travail en ajoutant une nouvelle base de données client tooa clients ou une commande dans une base de données des commandes de mise à jour.
* Utilisez les actions tooget une ligne de données, insérer une nouvelle ligne, ou les supprimer. Par exemple, quand un enregistrement est créé dans Dynamics CRM Online (déclencheur), insérez une ligne dans une base de données Oracle (action). 

Cette rubrique vous montre comment toouse hello dans une application de la logique d’un connecteur de base de données Oracle.

## <a name="prerequisites"></a>Composants requis

* Versions d’Oracle prises en charge : 
    * Oracle 9 et versions ultérieures
    * Logiciel client Oracle 8.1.7 et versions ultérieures

* Installez la passerelle de données locale hello. [Se connecter tooon locale, les données à partir d’applications de logique](../logic-apps/logic-apps-gateway-connection.md) listes hello étapes. passerelle de Hello est requis tooconnect tooan base de données Oracle locale ou une machine virtuelle de Azure avec la base de données Oracle installée. 

    > [!NOTE]
    > passerelle de données locale Hello fait Office de pont et fournit un transfert sécurisé des données entre des données locales (les données qui ne sont pas dans le cloud de hello) et vos applications logiques. Hello même passerelle peut être utilisé avec plusieurs services et plusieurs sources de données. Par conséquent, vous devrez peut-être uniquement passerelle de hello tooinstall qu’une seule fois.

* Installez hello Client Oracle sur l’ordinateur hello où vous avez installé la passerelle de données locale hello. Veillez à tooinstall hello 64 bits du fournisseur de données Oracle pour .NET à partir d’Oracle :  

  [ODAC 12C version 4 (12.1.0.2.4) 64 bits pour Windows x64](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Si le client d’Oracle hello n’est pas installé, une erreur se produit lorsque vous essayez de toocreate ou utilisez hello connexion. Consultez les erreurs courantes hello dans cette rubrique.


## <a name="add-hello-connector"></a>Ajouter hello connecteur

> [!IMPORTANT]
> Ce connecteur ne possède aucun déclencheur. Il possède uniquement des actions. Par conséquent, lorsque vous créez votre application logique, ajoutez un autre déclencheur toostart votre application logique, tel que **planification - périodicité**, ou **demande / réponse - réponse**. 

1. Bonjour [portail Azure](https://portal.azure.com), créer une application vide logique.

2. Au début de hello de votre application logique, sélectionnez hello **demande / réponse - demande** déclencheur : 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. Sélectionnez **Enregistrer**. Au moment de l’enregistrement, une URL de requête est générée automatiquement. 

4. Sélectionnez **Nouvelle étape**, puis sélectionnez **Ajouter une action**. Tapez dans `oracle` toosee hello actions disponibles : 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > Il s’agit également toosee moyen le plus rapide de hello hello des déclencheurs et les actions disponibles pour tous les connecteurs. Tapez dans la partie du nom du connecteur hello, tel que `oracle`. le Concepteur de Hello répertorie tous les déclencheurs et les actions. 

5. Sélectionnez une des actions de hello, tel que **base de données Oracle - Get ligne**. Sélectionnez l’option **Se connecter via la passerelle de données locale**. Entrez le nom du serveur Oracle hello, méthode d’authentification, nom d’utilisateur, mot de passe et sélectionnez hello passerelle :

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. Une fois connecté, sélectionnez une table dans la liste de hello et entrez table tooyour des ID de ligne hello. Vous avez besoin de table de toohello tooknow hello identificateur. Si vous ne connaissez pas, contactez votre administrateur de base de données Oracle et obtenir la sortie hello `select * from yourTableName`. Ceci permet de vous hello vous devez tooproceed informations d’identification personnelle.

    Dans l’exemple suivant de hello, données de la tâche sont retournées depuis une base de données des ressources humaines : 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. Dans cette étape, vous pouvez utiliser une des hello autres toobuild connecteurs votre flux de travail. Si vous souhaitez tootest obtention de données à partir d’Oracle, puis vous envoyez un message électronique avec des données d’Oracle hello à l’aide de hello envoyer par courrier électronique connecteurs, Office 365 ou Gmail de ce type. Utiliser des jetons de hello dynamique à partir de Bonjour Oracle table toobuild Bonjour `Subject` et `Body` de votre adresse de messagerie :

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **Enregistrez** votre application logique, puis sélectionnez **Exécuter**. Fermez le Générateur de hello et observez l’historique des exécutions hello pour l’état de hello. En cas d’échec, sélectionnez la ligne du message ayant échoué hello. Hello concepteur s’ouvre et affiche les étape a échoué et indique hello des informations d’erreur. Si elle réussit, vous devez recevoir un message électronique contenant les informations de hello que vous avez ajouté.


### <a name="workflow-ideas"></a>Idées de workflow

* Vous souhaitez toomonitor hello #oracle #sqlhelp et que vous placez hello tweet dans une base de données afin qu’ils peuvent être consultés et utilisés dans d’autres applications. Dans une application logique, ajoutez hello `Twitter - When a new tweet is posted` déclencher et entrez hello **#oracle** #sqlhelp. Ensuite, ajoutez hello `Oracle Database - Insert row` action, puis sélectionnez votre table :

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* File d’attente du Service Bus tooa sont envoyés. Vous voulez tooget ces messages et les placer dans une base de données. Dans une application logique, ajoutez hello `Service Bus - when a message is received in a queue` déclencheur file d’attente et sélectionnez hello. Ensuite, ajoutez hello `Oracle Database - Insert row` action, puis sélectionnez votre table :

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>Erreurs courantes

#### <a name="error-cannot-reach-hello-gateway"></a>**Erreur**: ne peut pas atteindre hello passerelle

**Cause**: passerelle de données locale hello n’est pas en mesure de tooconnect toohello cloud. 

**Atténuation**: Assurez-vous que votre passerelle s’exécute sur l’ordinateur local, hello où vous l’avez installé et qu’il peut se connecter toohello internet.  Nous vous recommandons ne pas l’installation de passerelle de hello sur un ordinateur qui peut être mis hors tension ou le mode veille. Vous pouvez également redémarrer le service de passerelle de données hello local (PBIEgwService).

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**Erreur**: fournisseur hello utilisé est déconseillé : ' System.Data.OracleClient requiert le logiciel client Oracle version 8.1.7 ou ultérieure.'. Visitez [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) fournisseur officiel de tooinstall hello.

**Cause**: hello Oracle clients SDK n’est pas installé sur l’ordinateur de hello où hello locaux passerelle de données est en cours d’exécution.  

**Résolution**: télécharger et installer le Kit de développement logiciel du client Oracle hello sur hello même ordinateur en tant que passerelle de données locale hello.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**Erreur** : La table « [Tablename] » ne définit aucune colonne clé

**Cause**: table de hello n’a pas de clé primaire.  

**Résolution**: connecteur de base de données Oracle hello requiert qu’une table avec une colonne clé primaire.

#### <a name="currently-not-supported"></a>Actuellement non pris en charge

* Vues et procédures stockées 
* Toute table avec des clés composites
* Types d’objet imbriqués dans des tables
 
## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/oracle/). 

## <a name="get-some-help"></a>Obtenir de l’aide

Hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) est une bonne placez tooask questions, répondez aux questions et voir ce que font les autres utilisateurs Logic Apps. 

Vous pouvez améliorer Logic Apps et les connecteurs en votant et en soumettant vos idées sur [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish). 


## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md)et Explorer les connecteurs disponibles hello dans Logic Apps à notre [liste des API](apis-list.md).
