---
title: connecteur de Informix aaaAdd hello dans vos applications logiques | Documents Microsoft
description: "Vue d’ensemble du connecteur Informix avec les paramètres d’API REST"
services: 
documentationcenter: 
author: gplarsen
manager: anneta
editor: 
tags: connectors
ms.assetid: ca2393f0-3073-4dc2-8438-747f5bc59689
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: 7a163e2ebf00fa3109b93e34845d922c2174a48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-informix-connector"></a>Prise en main connecteur de Informix hello
Microsoft connector pour Informix connecte tooresources Logic Apps stockées dans une base de données IBM Informix. connecteur de Informix Hello inclut un ordinateurs client Microsoft toocommunicate tooremote Informix serveur sur un réseau TCP/IP. Cela inclut les bases de données cloud, tels que IBM Informix pour Windows en cours d’exécution dans la virtualisation Azure et des bases de données à l’aide de la passerelle de données locale hello sur site. Consultez hello [prise en charge de la liste](connectors-create-api-informix.md#supported-informix-platforms-and-versions) de IBM Informix plateformes et versions (dans cette rubrique).

connecteur de Hello prend en charge hello des opérations de base de données suivantes :

* énumération des tables de base de données ;
* lecture d’une ligne à l’aide de l’instruction SELECT ;
* lecture de toutes les lignes à l’aide de l’instruction SELECT ;
* ajout d’une ligne à l’aide de l’instruction INSERT ;
* modification d’une ligne à l’aide de l’instruction UPDATE ;
* suppression d’une ligne à l’aide de l’instruction DELETE.

Cette rubrique vous montre les opérations de données dans un tooprocess d’application de la logique d’un connecteur toouse hello.

toolearn en savoir plus sur les applications de la logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Actions disponibles
Ce connecteur prend en charge hello suivant des actions de logique d’application :

* Getables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Affichage de la liste des tables
Création d’une application logique pour toute opération se compose de nombreuses étapes effectuées par le biais du portail Microsoft Azure hello.

Au sein de l’application logique de hello, vous pouvez ajouter des tables de toolist d’une action dans une base de données Informix. Cette action fait en sorte que hello connecteur tooprocess une instruction de schéma Informix, tel que `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `InformixgetTables`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**.  
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez **informix** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **Informix - Get tables (version préliminaire)**.
   
   ![](./media/connectors-create-api-informix/InformixconnectorActions.png)  
6. Bonjour **Informix - Get tables** volet de configuration, sélectionnez **case à cocher** tooenable **se connecter via la passerelle de données locale**. Remarquez que les paramètres de hello tooon site cloud.
   
   * Valeur de type de **Server**, sous forme de hello d’adresse ou alias de numéro de port de deux-points. Par exemple, tapez `ibmserver01:9089`.
   * Renseignez la zone **Base de données**. Par exemple, tapez `nwind`.
   * Renseignez la zone **Authentification**. Par exemple, sélectionnez **De base**.
   * Renseignez la zone **Nom d’utilisateur**. Par exemple, tapez `informix`.
   * Renseignez la zone **Mot de passe**. Par exemple, tapez `Password1`.
   * Renseignez la zone **Passerelle**. Par exemple, sélectionnez **datagateway01**.
7. Sélectionnez **Créer**, puis sélectionnez **Enregistrer**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)
8. Bonjour **InformixgetTables** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
9. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_tables**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure une liste de tables.
   
   ![](./media/connectors-create-api-informix/InformixconnectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Créer des connexions de hello
Ce connecteur prend en charge les connexions toodatabase localement et dans le cloud de hello à l’aide de hello des propriétés de connexion suivantes. 

| Propriété | Description |
| --- | --- |
| Serveur |Obligatoire. Accepte une valeur de chaîne représentant une adresse ou un alias TCP/IP, au format IPv4 ou IPv6, suivis d’un caractère deux-points et d’un numéro de port TCP/IP. |
| Base de données |Obligatoire. Accepte une valeur de chaîne représentant un nom de base de données relationnelle DRDA (RDBNAM). Informix accepte une chaîne de 128 octets (la propriété de base de données correspond à un nom de base de données (dbname) IBM Informix). |
| Authentification |facultatif. Accepte la valeur d’élément de liste De base ou Windows (Kerberos). |
| Nom d’utilisateur |Obligatoire. Accepte une valeur de chaîne. |
| Mot de passe |Obligatoire. Accepte une valeur de chaîne. |
| Passerelle |Obligatoire. Accepte une valeur d’élément de liste, représentant les données passerelle définie tooLogic applications hello local au sein du groupe de stockage hello. |

## <a name="create-hello-on-premises-gateway-connection"></a>Créez hello local de connexion à la passerelle
Ce connecteur peut accéder à une base de données Informix localement à l’aide de la passerelle de données locale hello. Pour plus d’informations, voir les rubriques consacrées aux passerelles. 

1. Bonjour **passerelles** volet de configuration, sélectionnez **case à cocher** tooenable **se connecter via la passerelle**. Consultez hello paramètres changent de cloud tooon local.
2. Valeur de type de **Server**, sous forme de hello d’adresse ou alias de numéro de port de deux-points. Par exemple, tapez `ibmserver01:9089`.
3. Renseignez la zone **Base de données**. Par exemple, tapez `nwind`.
4. Renseignez la zone **Authentification**. Par exemple, sélectionnez **De base**.
5. Renseignez la zone **Nom d’utilisateur**. Par exemple, tapez `informix`.
6. Renseignez la zone **Mot de passe**. Par exemple, tapez `Password1`.
7. Renseignez la zone **Passerelle**. Par exemple, sélectionnez **datagateway01**.
8. Sélectionnez **créer** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Créer la connexion de cloud hello
Ce connecteur peut accéder à une base de données Informix cloud. 

1. Bonjour **passerelles** volet de configuration, laissez le champ hello **case à cocher** désactivé (décoché la case) **se connecter via la passerelle**. 
2. Renseignez la zone **Nom de la connexion**. Par exemple, tapez `hisdemo2`.
3. Valeur de type de **nom du serveur Informix**, sous forme de hello d’adresse ou alias de numéro de port de deux-points. Par exemple, tapez `hisdemo2.cloudapp.net:9089`.
4. Renseignez la zone **Informix database name**(Nom de la base de données Informix). Par exemple, tapez `nwind`.
5. Renseignez la zone **Nom d’utilisateur**. Par exemple, tapez `informix`.
6. Renseignez la zone **Mot de passe**. Par exemple, tapez `Password1`.
7. Sélectionnez **créer** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Extraire toutes les lignes à l’aide de l’instruction SELECT
Vous pouvez créer un toofetch d’action d’application logique toutes les lignes dans la table de Informix hello. Cette action fait en sorte que hello connecteur tooprocess une instruction SELECT de Informix, tel que `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom** (par exemple) « **InformixgetRows** »), **Abonnement**, **Groupe de ressources**, **Emplacement** et **Plan App Service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez **informix** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **Informix - Get lignes (version préliminaire)** .
6. Bonjour **obtenir des lignes (version préliminaire)** action, sélectionnez **modifier la connexion**.
7. Bonjour **connexions** volet de configuration, sélectionnez **nouvel**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorNewConnection.png)
8. Bonjour **passerelles** volet de configuration, laissez le champ hello **case à cocher** désactivé (décoché la case) **se connecter via la passerelle**.
   
   * Renseignez la zone **Nom de la connexion**. Par exemple, tapez `HISDEMO2`.
   * Valeur de type de **nom du serveur Informix**, sous forme de hello d’adresse ou alias de numéro de port de deux-points. Par exemple, tapez `HISDEMO2.cloudapp.net:9089`.
   * Renseignez la zone **Informix database name**(Nom de la base de données Informix). Par exemple, tapez `NWIND`.
   * Renseignez la zone **Nom d’utilisateur**. Par exemple, tapez `informix`.
   * Renseignez la zone **Mot de passe**. Par exemple, tapez `Password1`.
9. Sélectionnez **créer** toocontinue.
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)
10. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
11. Si vous le souhaitez, sélectionnez **Show advanced options** toospecify les options de requête.
12. Sélectionnez **Enregistrer**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsTableName.png)
13. Bonjour **InformixgetRows** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
14. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure une liste de lignes.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>ajout d’une ligne à l’aide de l’instruction INSERT ;
Vous pouvez créer une logique application action tooadd une ligne dans une table Informix. Cette action fait en sorte que hello connecteur tooprocess une instruction INSERT de Informix, tel que `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `InformixinsertRow`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez **informix** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **Informix - ligne d’insertion (version préliminaire)**.
6. Bonjour **obtenir des lignes (version préliminaire)** action, sélectionnez **modifier la connexion**. 
7. Bonjour **connexions** volet de configuration, sélectionnez tooselect une connexion. Par exemple, sélectionnez **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
9. Entrez des valeurs pour toutes les colonnes requises (signalées par un astérisque rouge). Par exemple, tapez `99999` pour **AREAID**, tapez `Area 99999`, puis tapez la valeur `102` pour **REGIONID**. 
10. Sélectionnez **Enregistrer**.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowValues.png)
11. Bonjour **InformixinsertRow** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
12. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure la ligne hello.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Extraire une ligne à l’aide de l’instruction SELECT
Vous pouvez créer une logique application action toofetch une ligne dans une table Informix. Cette action fait en sorte que hello connecteur tooprocess une instruction Informix sélectionnez où, tel que `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `InformixgetRow`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez **informix** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **Informix - Get lignes (version préliminaire)** .
6. Bonjour **obtenir des lignes (version préliminaire)** action, sélectionnez **modifier la connexion**. 
7. Bonjour **connexions** volet de configurations, sélectionnez tooselect une connexion existante. Par exemple, sélectionnez **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
9. Entrez des valeurs pour toutes les colonnes requises (signalées par un astérisque rouge). Par exemple, tapez `99999` pour **AREAID**. 
10. Si vous le souhaitez, sélectionnez **Show advanced options** toospecify les options de requête.
11. Sélectionnez **Enregistrer**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowValues.png)
12. Bonjour **InformixgetRow** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
13. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure la ligne.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Modifier une ligne à l’aide de l’instruction UPDATE
Vous pouvez créer une logique application action toochange une ligne dans une table Informix. Cette action fait en sorte que hello connecteur tooprocess une instruction de mise à jour Informix, tel que `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `InformixupdateRow`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez **informix** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **Informix - la ligne à jour (version préliminaire)**.
6. Bonjour **obtenir des lignes (version préliminaire)** action, sélectionnez **modifier la connexion**. 
7. Bonjour **connexions** volet de configurations, sélectionnez tooselect une connexion existante. Par exemple, sélectionnez **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
9. Entrez des valeurs pour toutes les colonnes requises (signalées par un astérisque rouge). Par exemple, tapez `99999` pour **AREAID**, tapez `Updated 99999`, puis tapez la valeur `102` pour **REGIONID**. 
10. Sélectionnez **Enregistrer**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowValues.png)
11. Bonjour **InformixupdateRow** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
12. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure la ligne hello.
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>suppression d’une ligne à l’aide de l’instruction DELETE.
Vous pouvez créer une logique application action tooremove une ligne dans une table Informix. Cette action fait en sorte que hello connecteur tooprocess une instruction DELETE de Informix, tel que `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `InformixdeleteRow`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez **informix** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **Informix - supprimer la ligne (version préliminaire)**.
6. Bonjour **obtenir des lignes (version préliminaire)** action, sélectionnez **modifier la connexion**. 
7. Bonjour **connexions** volet de configurations, sélectionnez une connexion existante. Par exemple, sélectionnez **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
9. Entrez des valeurs pour toutes les colonnes requises (signalées par un astérisque rouge). Par exemple, tapez `99999` pour **AREAID**. 
10. Sélectionnez **Enregistrer**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowValues.png)
11. Bonjour **InformixdeleteRow** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
12. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure la ligne de hello supprimé.
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowOutputs.png)

## <a name="supported-informix-platforms-and-versions"></a>Plateformes et versions Informix prises en charge
Ce connecteur prend en charge hello lors configuré suivantes : les versions IBM Informix, les connexions client toosupport DRDA Distributed Relational Database Architecture ().

* IBM Informix 12.1
* IBM Informix 11.7

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/informix/). 

## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).

