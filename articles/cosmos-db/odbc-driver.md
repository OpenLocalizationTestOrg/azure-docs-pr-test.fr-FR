---
title: "aaaConnect tooAzure Cosmos DB à l’aide des outils de BI analytique | Documents Microsoft"
description: "Découvrez comment toouse hello vues et tables toocreate du pilote ODBC de base de données Azure Cosmos afin que les données normalisées sont consultables dans BI logiciels et de données analytique."
keywords: odbc, pilote odbc
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 9967f4e5-4b71-4cd7-8324-221a8c789e6b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: e12a70f7805445f09fac01411e4bfbccc9a29c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-cosmos-db-using-bi-analytics-tools-with-hello-odbc-driver"></a>Se connecter tooAzure Cosmos DB à l’aide des outils de BI analytique avec le pilote ODBC de hello

permet de pilote ODBC de base de données Azure Cosmos Hello tooAzure de tooconnect vous DB Cosmos analytique de BI d’à l’aide des outils tels que SQL Server Integration Services, Power BI Desktop et Tableau afin que vous pouvez analyser et créer des visualisations de données de votre base de données Azure Cosmos dans les solutions.

pilote ODBC de base de données Azure Cosmos de Hello est conforme à ODBC 3.8 et prend en charge la syntaxe ANSI SQL-92. Bonjour pilote offre des fonctionnalités puissantes toohelp renormalize de données dans la base de données Azure Cosmos. À l’aide du pilote de hello, vous pouvez représenter des données dans la base de données Azure Cosmos en tant que tables et des vues. pilote de Hello vous permet de tooperform les opérations SQL par rapport aux tables de hello et des vues, y compris le groupe par des requêtes, des insertions, mises à jour et suppressions.

## <a name="why-do-i-need-toonormalize-my-data"></a>Pourquoi dois-je toonormalize mes données ?
Azure Cosmos DB est une base de données schemaless, donc il permet le développement rapide d’applications en activant les applications tooiterate leurs données de modèle volée hello et pas limitent tooa stricte de schéma. Une même base de données Azure Cosmos DB peut contenir des documents JSON de différentes structures. C’est parfait pour le développement rapide d’application, mais lorsque vous souhaitez tooanalyze et créez des rapports de vos données à l’aide d’analytique des données et des Outils BI, les données de salutation doit toobe aplatie souvent et respectent le schéma spécifique de tooa.

Il s’agit là du pilote ODBC de hello. En utilisant le pilote ODBC de hello, vous pouvez maintenant renormalisés des données dans la base de données Azure Cosmos dans les tables et vues raccord tooyour des données d’analyse et de création de rapports a besoin. les schémas Hello renormalisé n’ont aucun impact sur les données sous-jacentes de hello et limitent pas les développeurs tooadhere toothem, elles permettent simplement vous tooleverage compatible ODBC tooaccess hello données des outils. Désormais, votre base de données Azure Cosmos DB ne sera pas uniquement l’un des outils favoris de votre équipe de développement. Vos analystes de données vont l’adorer eux aussi.

Permet désormais de démarrer avec le pilote ODBC de hello.

## <a id="install"></a>Étape 1 : Installer le pilote ODBC de base de données Azure Cosmos de hello

1. Télécharger les pilotes hello pour votre environnement :

    * [Microsoft Azure Cosmos DB ODBC 64-bit.msi](https://aka.ms/documentdb-odbc-64x64) pour Windows 64 bits
    * [Microsoft Azure Cosmos DB ODBC 32x64-bit.msi](https://aka.ms/documentdb-odbc-32x64) pour 32 bits sur Windows 64 bits
    * [Microsoft Azure Cosmos DB ODBC 32-bit.msi](https://aka.ms/documentdb-odbc-32x32) pour Windows 32 bits

    Hello exécution msi fichier localement, le hello démarre **Assistant Installation de Microsoft Azure Cosmos DB ODBC Driver**. 
2. Exécutez l’Assistant installation de hello en utilisant le pilote ODBC hello hello par défaut tooinstall d’entrée.
3. Ouvrez hello **administrateur de source de données ODBC** application sur votre ordinateur, vous pouvez faire cela en tapant **des sources de données ODBC** zone de recherche dans les Windows hello. 
    Vous pouvez vérifier le pilote de hello a été installé en cliquant sur hello **pilotes** onglet et la garantie **pilote ODBC de Microsoft Azure Cosmos DB** est répertorié.

    ![Administrateur de sources de données ODBC Azure Cosmos DB](./media/odbc-driver/odbc-driver.png)

## <a id="connect"></a>Étape 2 : Se connecter à base de données de la base de données Azure Cosmos tooyour

1. Après avoir [pilote de ODBC de base de données Azure Cosmos hello installation](#install), Bonjour **administrateur de sources de données ODBC** fenêtre, cliquez sur **ajouter**. Vous pouvez créer un DSN utilisateur ou système. Dans cet exemple, nous créons un DSN utilisateur.
2. Bonjour **créer une nouvelle Source de données** fenêtre, sélectionnez **pilote ODBC de Microsoft Azure Cosmos DB**, puis cliquez sur **Terminer**.
3. Bonjour **le programme d’installation de Azure Cosmos DB ODBC Driver SDN** Outlook, renseignez les éléments suivants de hello : 

    ![Fenêtre de configuration DSN du pilote ODBC Azure Cosmos DB](./media/odbc-driver/odbc-driver-dsn-setup.png)
    - **Nom de Source de données**: votre propre nom convivial pour hello DSN ODBC. Ce nom est le compte de base de données Azure Cosmos tooyour unique, par conséquent, nommer de manière appropriée si vous possédez plusieurs comptes.
    - **Description**: une brève description de la source de données hello.
    - **Hôte** : URI de votre compte Azure Cosmos DB. Vous pouvez l’extraire à partir du Panneau de clés de base de données Azure Cosmos hello Bonjour portail Azure, comme indiqué dans hello suivant capture d’écran. 
    - **Clé d’accès**: hello clé primaire ou secondaire, en lecture-écriture ou en lecture seule à partir du Panneau de clés de base de données Azure Cosmos hello Bonjour portail Azure, comme indiqué dans hello suivant capture d’écran. Nous vous recommandons de qu'utiliser clé en lecture seule de hello si hello DSN est utilisé pour le traitement des données en lecture seule et les rapports.
    ![Panneau Azure Cosmos DB Keys (Clés Azure Cosmos DB)](./media/odbc-driver/odbc-driver-keys.png)
    - **Chiffrer la clé d’accès pour**: sélectionnez hello meilleur choix basée sur des utilisateurs hello de cet ordinateur. 
4. Cliquez sur hello **Test** toomake bouton que vous pouvez vous connecter de compte de base de données Azure Cosmos tooyour. 
5. Cliquez sur **Options avancées** et hello de l’ensemble des valeurs suivantes :
    - **La cohérence de la requête**: hello sélectionnez [au niveau de cohérence](consistency-levels.md) pour vos opérations. valeur par défaut Hello est la Session.
    - **Nombre de nouvelles tentatives**: entrez nombre hello de tooretry une opération si la demande initiale de hello ne se termine pas en raison de la limitation de tooservice.
    - **Fichier de schéma** : plusieurs options vous sont proposées ici.
        - Par défaut, en conservant cette entrée en l’état (vide), les pilotes hello analyse hello première page données pour tous les schémas hello toodetermine de collections de chaque collection. Cette opération est appelée Mappage de la collection. Sans un fichier de schéma défini, pilote de hello est tooperform hello pour chaque session de pilote et peut entraîner un temps d’une application à l’aide de hello DSN de démarrage plus élevée. Nous vous recommandons de toujours associer un fichier de schéma à un DSN.
        - Si vous avez déjà un fichier de schéma (éventuellement une que vous avez créé à l’aide de hello [l’éditeur de schéma](#schema-editor)), vous pouvez cliquer sur **Parcourir**, accédez tooyour fichier, cliquez sur **enregistrer**, puis cliquez sur **OK**.
        - Si vous voulez toocreate un nouveau schéma, cliquez sur **OK**, puis cliquez sur **l’éditeur de schéma** dans la fenêtre principale de hello. Passez toohello [l’éditeur de schéma](#schema-editor) plus d’informations. Lorsque vous créez un nouveau fichier de schéma hello, n’oubliez pas toohello arrière de toogo **Options avancées** fichier de schéma de fenêtre tooinclude hello nouvellement créé.

6. Une fois que vous avez terminé et que vous fermez hello **le programme d’installation de Azure Cosmos DB ODBC Driver DSN** fenêtre, hello nouvelle source de données utilisateur est ajouté à onglet DSN utilisateur de toohello.

    ![Nouveau Azure Cosmos DB ODBC DSN sur l’onglet DSN utilisateur de hello](./media/odbc-driver/odbc-driver-user-dsn.png)

## <a id="#collection-mapping"></a>Étape 3 : Créer une définition de schéma à l’aide de la méthode de mappage de collection hello

Il existe deux types de méthodes d’échantillonnage que vous pouvez utiliser : **mappage de la collection** ou **délimiteurs de la table**. Une session d’échantillonnage peut utiliser les deux méthodes d’échantillonnage, mais chaque collection peut uniquement utiliser une méthode d’échantillonnage spécifique. étapes Hello ci-dessous créent un schéma pour les données de salutation dans un ou plusieurs regroupements à l’aide de la méthode de mappage de collection hello. Cette méthode d’échantillonnage récupère les données de hello dans la page hello d’une structure de hello toodetermine collection de données de hello. Il transpose une table de tooa collection sur hello côté d’ODBC. Cette méthode d’échantillonnage est rapide et efficace lorsque les données de salutation dans une collection sont homogènes. Si une collection contient un type hétérogène de données, nous vous recommandons d’utiliser hello [délimiteurs de la table de mappage méthode](#table-mapping) car il fournit une méthode d’échantillonnage plus robuste de structures de données toodetermine hello dans la collection de hello. 

1. Après avoir effectué les étapes 1 à 4 dans [base de données de base de données Azure Cosmos Connect tooyour](#connect), cliquez sur **l’éditeur de schéma** Bonjour **le programme d’installation de Azure Cosmos DB ODBC Driver DSN** fenêtre.

    ![Bouton de l’éditeur de schéma dans la fenêtre de configuration de source de données du pilote Azure Cosmos ODBC DB hello](./media/odbc-driver/odbc-driver-schema-editor.png)
2. Bonjour **l’éditeur de schéma** fenêtre, cliquez sur **créer un nouveau**.
    Hello **générer le schéma** fenêtre affiche toutes les collections hello Bonjour compte de base de données Azure Cosmos. 
3. Sélectionnez un ou plusieurs toosample de regroupements, puis cliquez sur **exemple**. 
4. Bonjour **mode** tabulation, de base de données hello, de schéma et de table sont représentées. Dans la vue de table hello, analyse de hello affiche hello propriétés associées à des noms de colonnes hello (nom SQL, nom de la Source, etc.).
    Pour chaque colonne, vous pouvez modifier le nom de la colonne du hello SQL, type SQL de hello, longueur SQL (le cas échéant), l’échelle (le cas échéant), précision (le cas échéant) et accepte la valeur null.
    - Vous pouvez définir **masquer la colonne** trop**true** si vous souhaitez tooexclude cette colonne à partir des résultats de la requête. Les colonnes marquées masquer la colonne = true ne sont pas retournés pour la sélection et de projection, même si elles font toujours partie du schéma de hello. Par exemple, vous pouvez masquer toutes les propriétés de système requis de base de données Azure Cosmos hello en commençant par « _ ».
    - Hello **id** colonne est hello seul champ qui ne peuvent pas être masqué car il est utilisé comme clé primaire de hello dans le schéma normalisé de hello. 
5. Une fois que vous avez terminé la définition de schéma de hello, cliquez sur **fichier** | **enregistrer**, parcourir le schéma de hello toosave toohello active, puis cliquez sur **enregistrer**.

    Bonjour future souhaitée toouse ce schéma avec un DSN, ouvrir la fenêtre de configuration de source de données du pilote Azure Cosmos ODBC DB hello (via l’administrateur de sources de données ODBC de hello) et cliquez sur Options avancées, puis dans la zone du fichier de schéma hello, accédez toohello enregistré le schéma. L’enregistrement d’un tooan de fichier de schéma DSN existant modifie les données de salutation DSN connexion tooscope toohello et structure définie par le schéma.

## <a id="table-mapping"></a>Étape 4 : Créer une définition de schéma à l’aide de hello délimiteurs de la table de mappage (méthode)

Il existe deux types de méthodes d’échantillonnage que vous pouvez utiliser : **mappage de la collection** ou **délimiteurs de la table**. Une session d’échantillonnage peut utiliser les deux méthodes d’échantillonnage, mais chaque collection peut uniquement utiliser une méthode d’échantillonnage spécifique. 

Hello étapes suivantes créent un schéma pour les données de salutation dans un ou plusieurs regroupements à l’aide de hello **délimiteurs de la table** méthode de mappage. Nous vous recommandons d’utiliser cette méthode d’échantillonnage lorsque vos collections contiennent des données hétérogènes. Vous pouvez utiliser cette hello tooscope de méthode d’échantillonnage ensemble tooa d’attributs et les valeurs correspondantes. Par exemple, si un document contient une propriété « Type », vous pouvez limiter les valeurs de toohello hello d’échantillonnage de cette propriété. résultat final de Hello d’échantillonnage de hello serait un ensemble de tables pour chacune des valeurs hello pour le Type que vous avez spécifié. Par exemple, Type = Voiture produira une table Voiture tandis que Type = Avion produira une table Avion.

1. Après avoir effectué les étapes 1 à 4 dans [base de données de base de données Azure Cosmos Connect tooyour](#connect), cliquez sur **l’éditeur de schéma** dans la fenêtre de configuration de source de données du pilote Azure Cosmos ODBC DB hello.
2. Bonjour **l’éditeur de schéma** fenêtre, cliquez sur **créer un nouveau**.
    Hello **générer le schéma** fenêtre affiche toutes les collections hello Bonjour compte de base de données Azure Cosmos. 
3. Sélectionnez un regroupement sur hello **vue d’exemples** onglet hello **définition de mappage** colonne pour la collection de hello, cliquez sur **modifier**. Ensuite, dans hello **définition de mappage** fenêtre, sélectionnez **délimiteurs de la Table** (méthode). Puis la hello suivant :

    a. Bonjour **attributs** zone, entrez un nom hello d’une propriété de délimiteur. Il s’agit d’une propriété dans le document que vous souhaitez tooscope d’échantillonnage de hello, par exemple, ville et appuyez sur ENTRÉE. 

    b. Si vous souhaitez uniquement les valeurs de toocertain tooscope hello d’échantillonnage pour l’attribut hello vous venez d’entrer, sélectionnez hello dans la zone de sélection hello, puis entrez une valeur Bonjour **valeur** zone, par exemple, Seattle et appuyez sur ENTRÉE. Vous pouvez continuer à tooadd plusieurs valeurs pour les attributs. Assurez-vous juste que hello correct d’attribut est sélectionné lorsque vous entrez des valeurs.

    Par exemple, si vous incluez un **attributs** valeur de la ville et que vous souhaitez toolimit tooonly de votre table inclut les lignes avec une valeur de la ville de New York et Dubaï, entrez ville dans la zone d’attributs hello et New York et Dubaï Bonjour  **Valeurs** boîte.
4. Cliquez sur **OK**. 
5. Après avoir effectué les définitions de mappage hello pour les collections de hello souhaité toosample, Bonjour **l’éditeur de schéma** fenêtre, cliquez sur **exemple**.
     Pour chaque colonne, vous pouvez modifier le nom de la colonne du hello SQL, type SQL de hello, longueur SQL (le cas échéant), l’échelle (le cas échéant), précision (le cas échéant) et accepte la valeur null.
    - Vous pouvez définir **masquer la colonne** trop**true** si vous souhaitez tooexclude cette colonne à partir des résultats de la requête. Les colonnes marquées masquer la colonne = true ne sont pas retournés pour la sélection et de projection, même si elles font toujours partie du schéma de hello. Par exemple, vous pouvez masquer toutes les propriétés de système requis de base de données Azure Cosmos hello en commençant par « _ ».
    - Hello **id** colonne est hello seul champ qui ne peuvent pas être masqué car il est utilisé comme clé primaire de hello dans le schéma normalisé de hello. 
6. Une fois que vous avez terminé la définition de schéma de hello, cliquez sur **fichier** | **enregistrer**, parcourir le schéma de hello toosave toohello active, puis cliquez sur **enregistrer**.
7. Dans hello **le programme d’installation de Azure Cosmos DB ODBC Driver DSN** fenêtre, cliquez sur ** Options Avancé **. Ensuite, dans hello **fichier de schéma** , parcourir le fichier de schéma toohello enregistrée puis cliquez sur **OK**. Cliquez sur **OK** nouveau toosave hello DSN. Ce schéma de hello enregistre vous avez créé toohello DSN. 

## <a name="optional-creating-views"></a>(Facultatif) Création de vues
Vous pouvez définir et créer des vues dans le cadre du processus d’échantillonnage hello. Ces affichages sont tooSQL équivalentes. Ils sont en lecture seule et les sélections hello étendue et les projections hello que SQL de base de données Azure Cosmos défini. 

toocreate une vue de vos données, en hello **l’éditeur de schéma** fenêtre hello **les définitions de vue** colonne, cliquez sur **ajouter** sur la ligne hello de hello collection toosample. Puis Bonjour **les définitions de vue** fenêtre, hello suivant :
1. Cliquez sur **nouveau**, entrez un nom pour la vue hello, par exemple, EmployeesfromSeattleView, puis sur **OK**.
2. Bonjour **modifier la vue** fenêtre, entrez une requête de base de données Azure Cosmos. Utilisez obligatoirement une requête SQL Azure Cosmos DB, par exemple `SELECT c.City, c.EmployeeName, c.Level, c.Age, c.Gender, c.Manager FROM c WHERE c.City = “Seattle”`, puis cliquez sur **OK**.

Vous pouvez créer autant de vues que vous le souhaitez. Une fois que vous avez terminé la définition de vues hello, vous pouvez ensuite exemples de hello données. 

## <a name="step-5-view-your-data-in-bi-tools-such-as-power-bi-desktop"></a>Étape 5 : Affichage de vos données dans des outils décisionnels comme Power BI Desktop

Vous pouvez utiliser votre nouveau tooconnect de source de données DocumentADB avec des outils compatibles ODBC - cette étape vous indique simplement comment tooconnect tooPower BI Desktop et créer une visualisation Power BI.

1. Ouvrez Power BI Desktop.
2. Cliquez sur **Get Data** (Obtenir les données).
3. Bonjour **obtenir des données** fenêtre, cliquez sur **autres** | **ODBC** | **connexion**.
4. Bonjour **ODBC à partir de** (fenêtre), nom de source de données Sélectionnez hello vous créé, puis cliquez sur **OK**. Vous pouvez laisser hello **Options avancées** entrées vides.
5. Bonjour **accéder à une source de données à l’aide d’un pilote ODBC** fenêtre, sélectionnez **par défaut ou personnalisé** puis cliquez sur **connexion**. Vous n’avez pas besoin de tooinclude hello **d’informations d’identification des propriétés de chaîne de connexion**.
6. Bonjour **Navigator** fenêtre, dans le volet gauche de hello, développez hello de base de données, schéma de hello et table de hello puis sélectionnez. volet de résultats Hello inclut des données hello à l’aide du schéma hello créé.
7. les données de salutation toovisualize dans Power BI desktop, la case hello devant le nom de la table hello, puis cliquez sur **charge**.
8. Dans Power BI Desktop, hello à gauche, sélectionnez onglet des données hello ![Onglet Données de Power BI Desktop](./media/odbc-driver/odbc-driver-data-tab.png) tooconfirm vos données ont été importées.
9. Vous pouvez désormais créer des éléments visuels à l’aide de Power BI en cliquant sur l’onglet Rapports de hello ![onglet Rapports dans Power BI Desktop](./media/odbc-driver/odbc-driver-report-tab.png), puis sur **nouveau Visual**, puis à personnaliser votre vignette. Pour plus d’informations sur la création de visualisations dans Power BI Desktop, consultez [Types de visualisation dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-visualization-types-for-reports-and-q-and-a/).

## <a name="troubleshooting"></a>Résolution des problèmes

Si vous recevez hello l’erreur suivante, assurez-vous hello **hôte** et **clé d’accès** valeurs que vous avez copié hello portail Azure dans [étape 2](#connect) sont corrects, puis réessayez. Utilisez hello copie boutons toohello à droite de hello **hôte** et **clé d’accès** valeurs Bonjour toocopy portail Azure hello valeurs sans erreur.

    [HY000]: [Microsoft][Azure Cosmos DB] (401) HTTP 401 Authentication Error: {"code":"Unauthorized","message":"hello input authorization token can't serve hello request. Please check that hello expected payload is built as per hello protocol, and check hello key being used. Server used hello following payload toosign: 'get\ndbs\n\nfri, 20 jan 2017 03:43:55 gmt\n\n'\r\nActivityId: 9acb3c0d-cb31-4b78-ac0a-413c8d33e373"}`

## <a name="next-steps"></a>Étapes suivantes

toolearn savoir plus sur la base de données Azure Cosmos, consultez [quelle est la base de données Azure Cosmos ?](introduction.md).
