---
title: "données aaaMove - passerelle de gestion des données | Documents Microsoft"
description: "Configurer une passerelle de données toomove des données entre locaux et hello cloud. Utiliser la passerelle de gestion des données dans Azure Data Factory toomove vos données."
keywords: "passerelle de données, intégration de données, déplacer des données, informations d’identification de passerelle"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>Déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données
Cet article présente l’intégration des données entre les magasins de données locaux et les magasins de données cloud à l’aide de Data Factory. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article et autres articles de concepts de base données fabrique : [datasets](data-factory-create-datasets.md) et [pipelines](data-factory-create-pipelines.md).

## <a name="data-management-gateway"></a>Passerelle de gestion de données
Vous devez installer la passerelle de gestion des données sur votre tooenable d’ordinateur local déplacement des données vers/à partir d’une banque de données locale. passerelle de Hello peut être installé sur le même ordinateur en tant que banque de données hello ou sur un autre ordinateur, tant que passerelle de hello peut se connecter de magasin de données toohello de hello.

> [!IMPORTANT]
> Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour obtenir des informations détaillées sur la passerelle de gestion des données. 

Hello procédure pas à pas suivante vous montre comment toocreate une fabrique de données avec un pipeline qui déplace les données à partir d’un site local **SQL Server** stockage d’objets blob Azure tooan de base de données. Dans le cadre de la procédure pas à pas hello, vous installez et configurez hello passerelle de gestion des données sur votre ordinateur.

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>Procédure pas à pas : copier toocloud de données locale
Dans cette procédure pas à pas vous hello comme suit : 

1. Créer une fabrique de données.
2. Créer une passerelle de gestion des données. 
3. Créer des services liés pour les magasins de données des sources et récepteurs.
4. Créer des groupes de données toorepresent d’entrée et les données de sortie.
5. Créer un pipeline comportant des données copie activité toomove hello.

## <a name="prerequisites-for-hello-tutorial"></a>Configuration requise pour le didacticiel de hello
Avant de commencer cette procédure pas à pas, vous devez disposer de hello suivant des conditions préalables :

* **Abonnement Azure**.  Si vous n'êtes pas abonné, vous pouvez créer un compte d'essai gratuit en quelques minutes. Consultez hello [version d’évaluation gratuite](http://azure.microsoft.com/pricing/free-trial/) article pour plus d’informations.
* **Compte Azure Storage**. Vous utilisez le stockage d’objets blob hello comme un **destination/récepteur** stocker des données dans ce didacticiel. Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) toocreate suit un article.
* **SQL Server**. Dans le cadre de ce didacticiel, vous utilisez une base de données SQL Server locale comme magasin de données **source**. 

## <a name="create-data-factory"></a>Créer une fabrique de données
Dans cette étape, vous utilisez hello Azure toocreate portail une instance d’Azure Data Factory nommée **ADFTutorialOnPremDF**.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **+ NOUVEAU**, **Intelligence + analyse**, puis **Data Factory**.

   ![Nouveau -> DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. Bonjour **nouvelle fabrique de données** , entrez **ADFTutorialOnPremDF** pour hello nom.

    ![Ajouter tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > nom de Hello de fabrique de données Azure hello doit être globalement unique. Si vous recevez une erreur de hello : **nom de fabrique de données « ADFTutorialOnPremDF » n’est pas disponible**, de modifier le nom hello hello fabrique de données (par exemple, yournameADFTutorialOnPremDF) et essayez à nouveau de créer. Utilisez ce nom à la place d'ADFTutorialOnPremDF quand vous effectuez les étapes restantes de ce didacticiel.
   >
   > nom Hello hello fabrique de données peut être enregistré comme un **DNS** nom dans les futures hello et donc devenir visible publiquement.
   >
   >
4. Sélectionnez hello **abonnement Azure** où vous souhaitez toobe de fabrique de données hello créé.
5. Sélectionnez un **groupe de ressources** existant ou créez-en un. Didacticiel de hello, créer un groupe de ressources nommé : **ADFTutorialResourceGroup**.
6. Cliquez sur **créer** sur hello **nouvelle fabrique de données** page.

   > [!IMPORTANT]
   > instances de fabrique de données toocreate, vous devez être membre du hello [collaborateur de fabrique de données](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rôle au niveau de groupe de ressource d’abonnement hello.
   >
   >
7. Une fois la création terminée, vous voyez hello **Data Factory** page comme indiqué dans hello suivant image :

   ![Page d’accueil Data Factory](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>Créer une passerelle
1. Bonjour **Data Factory** , cliquez sur **auteur et déployer** vignette toolaunch hello **éditeur** de fabrique de données hello.

    ![Vignette Créer et déployer](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. Bonjour éditeur Data Factory, cliquez sur **... Plus** sur hello barre d’outils, puis cliquez sur **nouvelle passerelle de données**. Vous pouvez également cliquer sur **passerelles de données** dans hello arborescence, puis cliquez sur **nouvelle passerelle de données**.

   ![Nouvelle passerelle de données sur la barre d’outils](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. Bonjour **créer** , entrez **adftutorialgateway** pour hello **nom**, puis cliquez sur **OK**.     

    ![Page Créer une passerelle](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > Dans cette procédure pas à pas, vous créez la passerelle de logique hello qu’un seul nœud (ordinateur local, Windows). Vous pouvez faire évoluer une passerelle de gestion des données en associant plusieurs machines locales de la passerelle de hello. Vous pouvez monter en puissance une passerelle en augmentant le nombre de travaux de déplacement des données qui peuvent s’exécuter simultanément sur un nœud. Cette fonctionnalité est également disponible pour une passerelle logique à nœud unique. Consultez l’article [Mise à l’échelle de la passerelle de gestion des données dans Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) pour plus d’informations.  
4. Bonjour **configurer** , cliquez sur **installer directement sur cet ordinateur**. Cette action télécharge le package d’installation hello pour la passerelle de hello, installe, configure et enregistre la passerelle hello sur l’ordinateur de hello.  

   > [!NOTE]
   > Utilisez Internet Explorer ou un navigateur web compatible Microsoft ClickOnce.
   >
   > Si vous utilisez Chrome, accédez toohello [Boutique Chrome](https://chrome.google.com/webstore/), recherche avec « ClickOnce » (mot clé), choisissez une des extensions de ClickOnce hello et installez-le.
   >
   > Hello même pour Firefox (complément installation). Cliquez sur **ouvrir le Menu** bouton de barre d’outils hello (**trois lignes horizontales** dans l’angle supérieur droit de hello), cliquez sur **modules complémentaires**, recherche avec « ClickOnce » (mot clé), choisissez une des hello Extensions de ClickOnce et l’installer.    
   >
   >

    ![Passerelle - Page Configurer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    De cette façon est toodownload (un seul clic) de façon plus simple de hello, installer, configurer et inscrire la passerelle de hello en une seule étape. Vous pouvez voir hello **Gestionnaire de Configuration de passerelle de gestion de données de Microsoft** application est installée sur votre ordinateur. Vous pouvez également trouver hello exécutable **ConfigManager.exe** dans le dossier de hello : **C:\Program Files\Microsoft données Gestion Gateway\2.0\Shared**.

    Vous pouvez également télécharger et installer manuellement de passerelle à l’aide de liens de hello dans cette page et inscrire à l’aide de la clé de hello Bonjour **nouvelle clé** zone de texte.

    Consultez [passerelle de gestion des données](data-factory-data-management-gateway.md) de l’article pour tous les hello plus d’informations sur la passerelle de hello.

   > [!NOTE]
   > Vous devez être administrateur sur tooinstall d’ordinateur local hello et configurer la passerelle de gestion des données de hello avec succès. Vous pouvez ajouter des utilisateurs supplémentaires toohello **utilisateurs de gestion des données à l’aide de la passerelle** groupe Windows local. membres de Hello de ce groupe peuvent utiliser passerelle de hello Gestionnaire de Configuration de passerelle de gestion de données outil tooconfigure hello.
   >
   >
5. Attendez quelques minutes, ou patientez jusqu'à ce que vous voyiez hello suivant le message de notification :

    ![Gateway installation successful (Installation réussie de la passerelle)](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. Lancez l’application **Gestionnaire de configuration de passerelle de gestion des données** sur votre ordinateur. Bonjour **recherche** fenêtre, tapez **passerelle de gestion des données** tooaccess cet utilitaire. Vous pouvez également trouver hello exécutable **ConfigManager.exe** dans le dossier de hello : **C:\Program Files\Microsoft données Gestion Gateway\2.0\Shared**

    ![Gestionnaire de configuration de la passerelle](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. Vérifiez que le message `adftutorialgateway is connected toohello cloud service` s’affiche. Hello hello bas affiche la barre d’état **toohello cloud service connecté** avec un **coche verte**.

    Sur hello **accueil** onglet, vous pouvez également effectuer hello fonctionnalités suivantes :

   * **Inscrire** une passerelle avec une clé à partir de hello portail Azure à l’aide du bouton de Registre hello.
   * **Arrêter** hello Service Gestion des données passerelle hôte en cours d’exécution sur votre ordinateur de passerelle.
   * **Planifier les mises à jour** toobe installé à un moment donné de la journée de hello.
   * Afficher lors de la passerelle de hello **dernière mise à jour**.
   * Spécifiez l’heure à laquelle une passerelle toohello de mise à jour peut être installée.
8. Commutateur toohello **paramètres** certificat de hello onglet spécifié dans hello **certificat** section est utilisé tooencrypt/déchiffrer les informations d’identification de banque de données locale hello que vous spécifiez sur le portail hello. (facultatif) Cliquez sur **modification** toouse votre propre certificat à la place. Par défaut, la passerelle de hello utilise certificat hello qui est généré automatiquement par hello service Data Factory.

    ![Configuration de certificat de la passerelle](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    Vous pouvez également effectuer hello actions suivantes sur hello **paramètres** onglet :

   * Afficher ou exporter le certificat hello utilisé par la passerelle de hello.
   * Modifier le point de terminaison HTTPS hello utilisé par la passerelle de hello.    
   * Définir un toobe du proxy HTTP utilisé par la passerelle de hello.     
9. (facultatif) Commutateur toohello **Diagnostics** onglet, vérifiez hello **activer la journalisation documentée** option si vous souhaitez tooenable détaillés de journalisation que vous pouvez utiliser tootroubleshoot des problèmes avec la passerelle de hello. Hello des informations de journalisation peuvent être trouvées dans **Observateur d’événements** sous **journaux des Applications et Services** -> **passerelle de gestion des données** nœud.

    ![Onglet Diagnostic](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    Vous pouvez également effectuer hello suivant actions Bonjour **Diagnostics** onglet :

   * Utilisez **tester la connexion** source de données locale tooan section à l’aide de la passerelle de hello.
   * Cliquez sur **afficher les journaux** toosee hello passerelle de gestion des données de session dans une fenêtre de l’Observateur d’événements.
   * Cliquez sur **d’envoi de journaux** tooupload un fichier zip avec des journaux de dernière sept jours tooMicrosoft toofacilitate dépannage de vos problèmes.
10. Sur hello **Diagnostics** onglet hello **tester la connexion** section, sélectionnez **SqlServer** de type hello de données de hello stocker, entrez le nom hello du serveur de base de données hello, nom du Hello de base de données, spécifiez le type d’authentification, entrez le nom d’utilisateur et mot de passe, puis cliquez sur **Test** tootest si la passerelle de hello peut se connecter toohello de base de données.
11. Navigateur web du commutateur toohello, hello et **portail Azure**, cliquez sur **OK** sur hello **configurer** page puis, dans hello **nouvelle passerelle de données** page.
12. Vous devez voir **adftutorialgateway** sous **passerelles de données** dans l’arborescence hello sur hello gauche.  Si vous cliquez dessus, vous devez voir hello associés JSON.

## <a name="create-linked-services"></a>Créez des services liés
Au cours de cette étape, vous créez deux services liés : **AzureStorageLinkedService** et **SqlServerLinkedService**. Hello **SqlServerLinkedService** lie une base de données SQL Server sur site et le hello **AzureStorageLinkedService** service lié lie une fabrique de données objet blob Azure store toohello. Créer un pipeline plus loin dans cette procédure pas à pas qui copie les données de magasin de hello local SQL Server de base de données toohello objets blob Azure.

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>Ajouter une base de données locale SQL Server de service lié tooan
1. Bonjour **éditeur Data Factory**, cliquez sur **nouveau magasin de données** sur la barre d’outils hello et sélectionnez **SQL Server**.

   ![Nouveau service lié SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. Bonjour **éditeur JSON** sur hello droite, hello comme suit :

   1. Pourquoi **gatewayName**, spécifiez **adftutorialgateway**.    
   2. Bonjour **connectionString**, hello comme suit :    

      1. Pour **nom_serveur**, entrez le nom hello du serveur hello qui héberge la base de données SQL Server hello.
      2. Pour **databasename**, entrez le nom hello de base de données hello.
      3. Cliquez sur **Encrypt** bouton de barre d’outils hello. Application du Gestionnaire d’informations d’identification hello s’affiche.

         ![Application Gestionnaire des informations d’identification](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. Bonjour **informations d’identification du paramètre** boîte de dialogue, spécifiez le type d’authentification, nom d’utilisateur et mot de passe, puis cliquez sur **OK**. Si la connexion de hello est réussie, hello chiffrée sont stockées dans hello JSON et fermeture de la boîte de dialogue hello.
      5. Fermer un onglet de navigateur vide hello lancer la boîte de dialogue hello s’il n’est pas fermé automatiquement et revenir à onglet toohello avec hello portail Azure.

         Sur l’ordinateur de passerelle hello, ces informations d’identification sont **chiffrées** à l’aide d’un certificat qui hello fabrique de données propriétaire de service. Si vous souhaitez que le certificat hello toouse associé hello passerelle de gestion des données au lieu de cela, consultez [définir les informations d’identification en toute sécurité](#set-credentials-and-security).    
   3. Cliquez sur **déployer** sur toodeploy hello service lié SQL Server de la barre de commandes hello. Vous devez voir service hello lié dans l’arborescence hello.

      ![Service lié SQL Server dans l’arborescence de hello](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>Ajout d’un service lié pour un compte de stockage Azure
1. Bonjour **éditeur Data Factory**, cliquez sur **nouveau magasin de données** hello de barre de commandes et cliquez sur **le stockage Azure**.
2. Entrez le nom hello de votre compte de stockage Azure pour hello **nom de compte**.
3. Entrez la clé hello pour votre compte de stockage Azure pour hello **clé de compte**.
4. Cliquez sur **déployer** toodeploy hello **AzureStorageLinkedService**.

## <a name="create-datasets"></a>Créez les jeux de données
Dans cette étape, vous créez une entrée et sortie datasets qui représentent les données d’entrée et de sortie pour l’opération de copie hello (base de données locale SQL Server = > stockage d’objets blob Azure). Avant de créer des jeux de données, procédez comme hello (les étapes détaillées suit la liste de hello) comme suit :

* Créer une table nommée **emp** hello de base de données SQL Server vous avez ajouté en tant qu’une fabrique de données de service lié toohello et insérer quelques exemples d’entrées dans la table de hello.
* Créer un conteneur d’objets blob nommé **adftutorial** Bonjour Azure blob compte de stockage que vous avez ajouté en tant qu’une fabrique de données toohello service lié.

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>Préparer SQL Server sur site hello
1. Dans base de données hello spécifiée pour hello local SQL Server service lié (**SqlServerLinkedService**), utilisez hello suivant hello SQL script toocreate **emp** table hello de base de données.

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. Insérer des exemples dans la table de hello :

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée

1. Bonjour **éditeur Data Factory**, cliquez sur **... Plus**, cliquez sur **nouveau dataset** sur hello de barre de commandes, puis cliquez sur **table SQL Server**.
2. Remplacez hello JSON dans le volet de droite hello hello suivant du texte :

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   Hello Notez les points suivants :

   * **type** est défini trop**SqlServerTable**.
   * **tableName** est défini trop**emp**.
   * **linkedServiceName** est défini trop**SqlServerLinkedService** (vous aviez créé ce service lié plus haut dans cette procédure pas à pas).
   * Pour un jeu de données d’entrée qui n’est pas généré par un autre pipeline Azure Data Factory, vous devez définir **externe** trop**true**. Cela signifie que les données d’entrée hello sont toohello externe produit service Azure Data Factory. Vous pouvez éventuellement spécifier des stratégies de données externes à l’aide de hello **externalData** élément Bonjour **stratégie** section.    

   Pour plus de détails sur les propriétés JSON, voir [Déplacer des données vers/à partir SQL Server](data-factory-sqlserver-connector.md).
3. Cliquez sur **déployer** sur toodeploy hello dataset de la barre de commandes hello.  

### <a name="create-output-dataset"></a>Créer un jeu de données de sortie

1. Bonjour **éditeur Data Factory**, cliquez sur **nouveau dataset** sur hello de barre de commandes, puis cliquez sur **le stockage Blob Azure**.
2. Remplacez hello JSON dans le volet de droite hello hello suivant du texte :

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   Hello Notez les points suivants :

   * **type** est défini trop**AzureBlob**.
   * **linkedServiceName** est défini trop**AzureStorageLinkedService** (vous aviez créé ce service lié à l’étape 2).
   * **folderPath** est défini trop**adftutorial/outfromonpremdf** où outfromonpremdf est le dossier hello dans le conteneur d’adftutorial hello. Créer hello **adftutorial** conteneur s’il n’existe pas.
   * Hello **disponibilité** est défini trop**toutes les heures** (**fréquence** défini trop**heure** et **intervalle** défini trop **1**).  Hello service Data Factory génère une tranche de données de sortie de toutes les heures Bonjour **emp** table Bonjour base de données SQL Azure.

   Si vous ne spécifiez pas un **nom de fichier** pour un **table de sortie**, fichiers hello généré Bonjour **folderPath** sont nommés Bonjour suivant le format : données.<Guid>. txt (par exemple : : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).

   tooset **folderPath** et **nom de fichier** dynamiquement en fonction de hello **SliceStart** fois, utilisez la propriété de partitionedBy hello. Dans l’exemple suivant de hello, folderPath utilise Year, Month et Day de hello SliceStart (heure de début de la tranche hello en cours de traitement) et nom de fichier utilise l’heure de hello SliceStart. Par exemple, si une tranche est produite pour 2014-10-20T08:00:00, hello nom_dossier est défini toowikidatagateway/wikidatagateway/2014/10/20 et nom de fichier hello too08.csv.

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    Pour plus de détails sur les propriétés JSON, voir [Déplacer des données vers/à partir de Stockage Blob Azure](data-factory-azure-blob-connector.md).
3. Cliquez sur **déployer** sur toodeploy hello dataset de la barre de commandes hello. Vérifiez que vous voyez deux jeux de données dans l’arborescence hello hello.  

## <a name="create-pipeline"></a>Création d’un pipeline
Dans cette étape, vous créez un **pipeline** avec une **activité Copier l’activité** qui utilise **EmpOnPremSQLTable** en tant qu’entrée et **OutputBlobTable** en tant que sortie.

1. Dans Data Factory Editor, cliquez sur **... Plus**, puis sur **Nouveau pipeline**.
2. Remplacez hello JSON dans le volet de droite hello hello suivant du texte :    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > Remplacez la valeur hello hello **Démarrer** propriété hello jour actuel et **fin** valeur avec hello jour suivant.
   >
   >

   Hello Notez les points suivants :

   * Dans la section d’activités hello, il est uniquement les activités dont **type** est défini trop**copie**.
   * **Entrée** d’activité hello est définie trop**EmpOnPremSQLTable** et **sortie** d’activité hello est définie trop**OutputBlobTable**.
   * Bonjour **typeProperties** section, **SqlSource** est spécifié comme hello **type de source de** et ** BlobSink ** est spécifié comme hello **detypederécepteur**.
   * Requête SQL `select * from emp` est spécifié pour hello **sqlReaderQuery** propriété du **SqlSource**.

   Les dates/heures de début et de fin doivent toutes deux être au [format ISO](http://en.wikipedia.org/wiki/ISO_8601). Par exemple : 2014-10-14T16:32:41Z. Hello **fin** temps est facultatif, mais nous l’utilisons dans ce didacticiel.

   Si vous ne spécifiez pas de valeur pour hello **fin** propriété, il est calculé en tant que «**start + 48 heures**». pipeline de hello toorun indéfiniment, spécifiez **9/9/9999** en tant que valeur hello pour hello **fin** propriété.

   Vous définissez hello durée dans le hello tranches de données sont traités en fonction de hello **disponibilité** propriétés qui ont été définies pour chaque jeu de données Azure Data Factory.

   Exemple de hello, sont des tranches de données 24 comme chaque tranche de données est généré toutes les heures.        
3. Cliquez sur **déployer** sur toodeploy hello dataset de la barre de commandes hello (table est un jeu de données rectangulaire). Confirmer ce pipeline hello s’affiche dans l’arborescence hello sous **Pipelines** nœud.  
4. Maintenant, cliquez sur **X** à deux reprises tooclose hello page tooget arrière toohello **Data Factory** page hello **ADFTutorialOnPremDF**.

**Félicitations !** Vous venez de créer une fabrique de données Azure, services liés, jeux de données et un pipeline et le pipeline de hello planifiée.

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>Fabrique de données hello vue dans une vue de diagramme
1. Bonjour **portail Azure**, cliquez sur **diagramme** vignette sur la page d’accueil hello pour hello **ADFTutorialOnPremDF** fabrique de données. :

    ![Lien Diagramme](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. Vous devez voir toohello similaires du diagramme hello suivant image :

    ![Vue du diagramme](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    Vous pouvez faire un zoom, effectuer un zoom arrière, zoom too100 %, toofit de zoom, automatiquement les pipelines de position et jeux de données et afficher les informations de lignage (surligne les éléments en amont et en aval des éléments sélectionnés).  Vous pouvez double-cliquer sur les propriétés de toosee d’un objet (jeu de données d’entrée/sortie ou pipeline) pour celle-ci.

## <a name="monitor-pipeline"></a>Surveillance d’un pipeline
Dans cette étape, vous utilisez hello Azure toomonitor portail, ce qui se passe dans une fabrique de données Azure. Vous pouvez également utiliser des pipelines et les jeux de données toomonitor d’applets de commande PowerShell. Pour plus de détails sur la surveillance, consultez [Surveillance et gestion des pipelines](data-factory-monitor-manage-pipelines.md).

1. Dans le diagramme de hello, double-cliquez sur **EmpOnPremSQLTable**.  

    ![Tranches EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. Notez que toutes les données hello tranches des se trouvent dans **prêt** durée de pipeline hello (heure de début heure tooend) étant Bonjour passées de l’état. Il est également, car vous avez inséré des données de hello dans la base de données SQL Server hello et il n’y figure tout temps hello. Vérifiez qu’aucune tranche n’apparaissent dans hello **tranches de problème** section bas hello. Cliquez sur tous les secteurs de hello, de tooview **consultez plus** bas hello liste hello des tranches.
3. Maintenant, dans hello **Datasets** , cliquez sur **OutputBlobTable**.

    ![Tranches OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. Cliquez sur n’importe quel tranche de données à partir de la liste de hello et vous devez voir hello **tranche de données** page. Vous voyez l’exécution de l’activité de la tranche de hello. Généralement, une seule activité exécutée s’affiche.  

    ![Panneau Tranche de données](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    Si la tranche de hello n’est pas hello **prêt** état, vous pouvez voir les tranches en amont hello qui ne sont pas prêtes et bloquent tranche à partir de l’exécution dans hello hello **tranches en amont qui ne sont pas prêtes** liste.
5. Cliquez sur hello **activité exécuter** à partir de la liste de hello en hello bas toosee **détails d’activité l'exécution**.

   ![Page Détails de l’exécution d’activité](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   Vous constatez des informations telles que le débit, la durée et passerelle de hello tootransfer les données de salutation.
6. Cliquez sur **X** tooclose tous hello pages jusqu'à ce que vous
7. revenir toohello page d’accueil pour hello **ADFTutorialOnPremDF**.
8. (facultatif) Cliquez sur **Pipelines**, sur **ADFTutorialOnPremDF**, puis accédez aux tables d’entrée (**Consommé**) ou aux jeux de données de sortie (**Produit**).
9. Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) tooverify qu’un objet blob/fichier est créé pour chaque heure.

   ![Explorateur de stockage Azure](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>Étapes suivantes
* Consultez [passerelle de gestion des données](data-factory-data-management-gateway.md) de l’article pour tous les hello plus d’informations sur la passerelle de gestion des données de hello.
* Consultez [copier les données d’objets Blob Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn sur comment banque de données récepteur tooa du magasin de données de toomove de l’activité de copie de toouse d’une source de données.
