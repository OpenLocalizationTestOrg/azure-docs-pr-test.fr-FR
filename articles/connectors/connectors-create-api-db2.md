---
title: "dans vos applications de la logique d’un connecteur hello DB2 aaaAdd | Documents Microsoft"
description: "Vue d’ensemble du connecteur DB2 avec les paramètres d’API REST"
services: 
documentationcenter: 
author: gplarsen
manager: erikre
editor: 
tags: connectors
ms.assetid: 1c6b010c-beee-496d-943a-a99e168c99aa
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: d836c61231d3c9cfdb30ff9c40a48b1718f3ffb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-db2-connector"></a>Prise en main connecteur DB2 de hello
Connecteur Microsoft pour DB2 connecte tooresources Logic Apps stockées dans une base de données IBM DB2. Ce connecteur inclut un toocommunicate du client Microsoft avec les ordinateurs serveur DB2 distants via un réseau TCP/IP. Cela inclut les bases de données cloud, tels que IBM Bluemix dashDB ou IBM DB2 pour Windows en cours d’exécution dans la virtualisation Azure et des bases de données à l’aide de la passerelle de données locale hello sur site. Consultez hello [prise en charge de la liste](connectors-create-api-db2.md#supported-db2-platforms-and-versions) des plateformes IBM DB2 et des versions (dans cette rubrique).

connecteur de Hello DB2 prend en charge hello des opérations de base de données suivantes :

* énumération des tables de base de données ;
* lecture d’une ligne à l’aide de l’instruction SELECT ;
* lecture de toutes les lignes à l’aide de l’instruction SELECT ;
* ajout d’une ligne à l’aide de l’instruction INSERT ;
* modification d’une ligne à l’aide de l’instruction UPDATE ;
* suppression d’une ligne à l’aide de l’instruction DELETE.

Cette rubrique vous montre les opérations de données dans un tooprocess d’application de la logique d’un connecteur toouse hello.

toolearn en savoir plus sur les applications de la logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Actions disponibles
connecteur de Hello DB2 prend en charge hello suivant des actions de logique d’application :

* GetTables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Affichage de la liste des tables
Création d’une application logique pour toute opération se compose de nombreuses étapes effectuées par le biais du portail Microsoft Azure hello.

Au sein de l’application logique de hello, vous pouvez ajouter des tables de toolist d’une action dans une base de données DB2. Hello action fait en sorte que hello connecteur tooprocess DB2 schema, instruction, telles que `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `Db2getTables`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis définissez hello **Intervalle** tootype **7**.  
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez `db2` Bonjour **recherche pour plusieurs actions** zone d’édition, puis **DB2 - Get tables (version préliminaire)**.
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. Bonjour **DB2 - Get tables** volet de configuration, sélectionnez **case à cocher** tooenable **se connecter via la passerelle de données locale**. Remarquez que les paramètres de hello tooon site cloud.
   
   * Valeur de type de **Server**, sous forme de hello d’adresse ou alias de numéro de port de deux-points. Par exemple, tapez `ibmserver01:50000`.
   * Renseignez la zone **Base de données**. Par exemple, tapez `nwind`.
   * Renseignez la zone **Authentification**. Par exemple, sélectionnez **De base**.
   * Renseignez la zone **Nom d’utilisateur**. Par exemple, tapez `db2admin`.
   * Renseignez la zone **Mot de passe**. Par exemple, tapez `Password1`.
   * Renseignez la zone **Passerelle**. Par exemple, sélectionnez **datagateway01**.
7. Sélectionnez **Créer**, puis sélectionnez **Enregistrer**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. Bonjour **Db2getTables** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
9. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_tables**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure une liste de tables.
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Créer des connexions de hello
Ce connecteur prend en charge les connexions toodatabases hébergée localement et dans le cloud de hello à l’aide de hello des propriétés de connexion suivantes. 

| Propriété | Description |
| --- | --- |
| Serveur |Obligatoire. Accepte une valeur de chaîne qui représente une adresse ou un alias TCP/IP, au format IPv4 ou IPv6, suivis d’un caractère deux-points et d’un numéro de port TCP/IP. |
| Base de données |Obligatoire. Accepte une valeur de chaîne qui représente un nom de base de données relationnelle DRDA (RDBNAM). DB2 pour z/OS accepte une chaîne de 16 octets (la propriété de base de données correspond à un emplacement IBM DB2 pour z/OS). DB2 pour i5/OS accepte une chaîne de 18 octets (la propriété de base de données correspond à une base de données relationnelle IBM DB2 pour i). DB2 pour LUW accepte une chaîne de 8 octets. |
| Authentification |facultatif. Accepte la valeur d’élément de liste De base ou Windows (Kerberos). |
| Nom d’utilisateur |Obligatoire. Accepte une valeur de chaîne. DB2 pour z/OS accepte une chaîne de 8 octets. DB2 pour i accepte une chaîne de 10 octets. DB2 pour Linux ou UNIX accepte une chaîne de 8 octets. DB2 pour Windows accepte une chaîne de 30 octets. |
| Mot de passe |Obligatoire. Accepte une valeur de chaîne. |
| Passerelle |Obligatoire. Accepte une valeur d’élément de liste, représentant les données passerelle définie tooLogic applications hello local au sein du groupe de stockage hello. |

## <a name="create-hello-on-premises-gateway-connection"></a>Créez hello local de connexion à la passerelle
Ce connecteur peut accéder à une base de données DB2 locale à l’aide de la passerelle locale de hello. Pour plus d’informations, voir les rubriques consacrées aux passerelles. 

1. Bonjour **passerelles** volet de configuration, sélectionnez **case à cocher** tooenable **se connecter via la passerelle**. Remarquez que les paramètres de hello tooon site cloud.
2. Valeur de type de **Server**, sous forme de hello d’adresse ou alias de numéro de port de deux-points. Par exemple, tapez `ibmserver01:50000`.
3. Renseignez la zone **Base de données**. Par exemple, tapez `nwind`.
4. Renseignez la zone **Authentification**. Par exemple, sélectionnez **De base**.
5. Renseignez la zone **Nom d’utilisateur**. Par exemple, tapez `db2admin`.
6. Renseignez la zone **Mot de passe**. Par exemple, tapez `Password1`.
7. Renseignez la zone **Passerelle**. Par exemple, sélectionnez **datagateway01**.
8. Sélectionnez **créer** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Créer la connexion de cloud hello
Ce connecteur peut accéder à une base de données DB2 cloud. 

1. Bonjour **passerelles** volet de configuration, laissez le champ hello **case à cocher** désactivé (décoché la case) **se connecter via la passerelle**. 
2. Renseignez la zone **Nom de la connexion**. Par exemple, tapez `hisdemo2`.
3. Valeur de type de **nom du serveur DB2**, sous forme de hello d’adresse ou alias de numéro de port de deux-points. Par exemple, tapez `hisdemo2.cloudapp.net:50000`.
4. Renseignez la zone **DB2 database name**(Nom de la base de données DB2). Par exemple, tapez `nwind`.
5. Renseignez la zone **Nom d’utilisateur**. Par exemple, tapez `db2admin`.
6. Renseignez la zone **Mot de passe**. Par exemple, tapez `Password1`.
7. Sélectionnez **créer** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Extraire toutes les lignes à l’aide de l’instruction SELECT
Vous pouvez définir un toofetch d’action d’application logique de toutes les lignes dans une table DB2. Cela fait en sorte que hello connecteur tooprocess une instruction SELECT de DB2, tel que `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `Db2getRows`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez `db2` Bonjour **recherche pour plusieurs actions** zone d’édition, puis **DB2 - Get lignes (version préliminaire)**.
6. Bonjour **obtenir des lignes (version préliminaire)** action, sélectionnez **modifier la connexion**.
7. Bonjour **connexions** volet de configuration, sélectionnez **nouvel**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. Bonjour **passerelles** volet de configuration, laissez le champ hello **case à cocher** désactivé (décoché la case) **se connecter via la passerelle**.
   
   * Renseignez la zone **Nom de la connexion**. Par exemple, tapez `HISDEMO2`.
   * Valeur de type de **nom du serveur DB2**, sous forme de hello d’adresse ou alias de numéro de port de deux-points. Par exemple, tapez `HISDEMO2.cloudapp.net:50000`.
   * Renseignez la zone **DB2 database name**(Nom de la base de données DB2). Par exemple, tapez `NWIND`.
   * Renseignez la zone **Nom d’utilisateur**. Par exemple, tapez `db2admin`.
   * Renseignez la zone **Mot de passe**. Par exemple, tapez `Password1`.
9. Sélectionnez **créer** toocontinue.
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
11. Si vous le souhaitez, sélectionnez **Show advanced options** toospecify les options de requête.
12. Sélectionnez **Enregistrer**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. Bonjour **Db2getRows** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
14. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure une liste de lignes.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>ajout d’une ligne à l’aide de l’instruction INSERT ;
Vous pouvez définir une logique application action tooadd une ligne dans une table DB2. Cette action fait en sorte que hello connecteur tooprocess une instruction INSERT de DB2, tel que `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `Db2insertRow`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez **db2** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **DB2 - ligne d’insertion (version préliminaire)**.
6. Bonjour **DB2 - ligne d’insertion (version préliminaire)** action, sélectionnez **modifier la connexion**. 
7. Bonjour **connexions** volet de configuration, sélectionnez une connexion. Par exemple, sélectionnez **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
9. Entrez des valeurs pour toutes les colonnes requises (signalées par un astérisque rouge). Par exemple, tapez `99999` pour **AREAID**, tapez `Area 99999`, puis tapez la valeur `102` pour **REGIONID**. 
10. Sélectionnez **Enregistrer**.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. Bonjour **Db2insertRow** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
12. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure la ligne hello.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Extraire une ligne à l’aide de l’instruction SELECT
Vous pouvez définir une logique application action toofetch une ligne dans une table DB2. Cette action fait en sorte que hello connecteur tooprocess une instruction DB2 sélectionnez où, tel que `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom** (par exemple) « **Db2getRow** »), **Abonnement**, **Groupe de ressources**, **Emplacement** et **Plan App Service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste. 
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez **db2** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **DB2 - Get lignes (version préliminaire)**.
6. Bonjour **obtenir des lignes (version préliminaire)** action, sélectionnez **modifier la connexion**. 
7. Bonjour **connexions** volet de configurations, sélectionnez une connexion existante. Par exemple, sélectionnez **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
9. Entrez des valeurs pour toutes les colonnes requises (signalées par un astérisque rouge). Par exemple, tapez `99999` pour **AREAID**. 
10. Si vous le souhaitez, sélectionnez **Show advanced options** toospecify les options de requête.
11. Sélectionnez **Enregistrer**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. Bonjour **Db2getRow** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
13. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure la ligne.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Modifier une ligne à l’aide de l’instruction UPDATE
Vous pouvez définir une logique application action toochange une ligne dans une table DB2. Cette action fait en sorte que hello connecteur tooprocess une instruction de mise à jour de DB2, tel que `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `Db2updateRow`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste.
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** , tapez **db2** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **DB2 - la ligne à jour (version préliminaire)**.
6. Bonjour **DB2 - la ligne à jour (version préliminaire)** action, sélectionnez **modifier la connexion**. 
7. Bonjour **connexions** volet de configurations, sélectionnez tooselect une connexion existante. Par exemple, sélectionnez **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
9. Entrez des valeurs pour toutes les colonnes requises (signalées par un astérisque rouge). Par exemple, tapez `99999` pour **AREAID**, tapez `Updated 99999`, puis tapez la valeur `102` pour **REGIONID**. 
10. Sélectionnez **Enregistrer**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. Bonjour **Db2updateRow** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
12. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure la ligne hello.
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>suppression d’une ligne à l’aide de l’instruction DELETE.
Vous pouvez définir une logique application action tooremove une ligne dans une table DB2. Cette action fait en sorte que hello connecteur tooprocess une instruction DELETE de DB2, tel que `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Créer une application logique
1. Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.
2. Entrez hello **nom**, tel que `Db2deleteRow`, **abonnement**, **groupe de ressources**, **emplacement**, et **application Plan de service**. Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.

### <a name="add-a-trigger-and-action"></a>Ajouter un déclencheur et une action
1. Bonjour **Concepteur d’applications logique**, sélectionnez **LogicApp vide** Bonjour **modèles** liste. 
2. Bonjour **déclencheurs** liste, sélectionnez **périodicité**. 
3. Bonjour **périodicité** déclencheur, sélectionnez **modifier**, sélectionnez **fréquence** tooselect de liste déroulante **jour**, puis sélectionnez  **Intervalle** tootype **7**. 
4. Sélectionnez hello **+ nouvelle étape** zone, puis sélectionnez **ajouter une action**.
5. Bonjour **actions** liste, sélectionnez **db2** Bonjour **recherche pour plusieurs actions** zone d’édition, puis **DB2 - supprimer la ligne (version préliminaire)**.
6. Bonjour **DB2 - supprimer la ligne (version préliminaire)** action, sélectionnez **modifier la connexion**. 
7. Bonjour **connexions** volet de configurations, sélectionnez une connexion existante. Par exemple, sélectionnez **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Bonjour **nom de la Table** liste, sélectionnez hello **bas**, puis sélectionnez **zone**.
9. Entrez des valeurs pour toutes les colonnes requises (signalées par un astérisque rouge). Par exemple, tapez `99999` pour **AREAID**. 
10. Sélectionnez **Enregistrer**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. Bonjour **Db2deleteRow** panneau, au sein de hello **toutes les séries** liste sous **Résumé**, sélectionnez hello premiers dans la liste, élément (la dernière exécution).
12. Bonjour **application logique exécuter** panneau, sélectionnez **détails de l’exécution**. Au sein de hello **Action** liste, sélectionnez **Get_rows**. Consultez la valeur hello pour **état**, qui doit être **Succeeded**. Sélectionnez hello **lien d’entrées** tooview les entrées de hello. Sélectionnez hello **sorties lien**et fournit en sortie hello d’affichage ; qui doit inclure la ligne de hello supprimé.
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>Plateformes et versions DB2 prises en charge
Ce connecteur prend en charge hello suivant plateformes IBM DB2 et les versions, ainsi que les produits compatibles IBM DB2 (par exemple, IBM Bluemix dashDB) qui prennent en charge de la base de données Architecture DRDA (Distributed Relational) SQL Access Manager (SQLAM) version 10 et 11 :

* IBM DB2 pour z/OS 11.1
* IBM DB2 pour z/OS 10.1
* IBM DB2 pour i 7.3
* IBM DB2 pour i 7.2
* IBM DB2 pour i 7.1
* IBM DB2 pour LUW 11
* IBM DB2 pour LUW 10.5

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/db2/). 

## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).

