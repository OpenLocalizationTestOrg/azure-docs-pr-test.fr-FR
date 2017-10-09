---
title: "aaaCopy des données à partir du stockage d’objets Blob tooSQL de base de données - Azure | Documents Microsoft"
description: "Ce didacticiel vous montre comment toouse l’activité de copie dans une fabrique de données Azure pipeline toocopy des données à partir de la base de données tooSQL de stockage Blob."
keywords: "blob sql, blob storage, copie de données"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>Didacticiel : Copier des données à partir du stockage d’objets Blob tooSQL de base de données à l’aide de la fabrique de données
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistant de copie](data-factory-copy-data-wizard-tutorial.md)
> * [Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Dans ce didacticiel, vous créez une fabrique de données comportant des données à partir de la base de données tooSQL de stockage Blob toocopy pipeline.

Activité de copie de Hello effectue le déplacement des données de hello dans Azure Data Factory. Elle est mise en œuvre par un service disponible dans le monde entier, capable de copier des données entre différents magasins de données de façon sécurisée, fiable et évolutive. Consultez [les activités de déplacement des données](data-factory-data-movement-activities.md) article pour plus d’informations sur l’activité de copie de hello.  

> [!NOTE]
> Pour obtenir une présentation détaillée de hello service Data Factory, consultez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) l’article.
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Configuration requise pour le didacticiel de hello
Avant de commencer ce didacticiel, vous devez disposer de hello suivant des conditions préalables :

* **Abonnement Azure**.  Si vous n'êtes pas abonné, vous pouvez créer un compte d'essai gratuit en quelques minutes. Consultez hello [version d’évaluation gratuite](http://azure.microsoft.com/pricing/free-trial/) article pour plus d’informations.
* **Compte Azure Storage**. Vous utilisez le stockage d’objets blob hello comme un **source** stocker des données dans ce didacticiel. Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) toocreate suit un article.
* **Base de données SQL Azure**. Vous allez utiliser une base de données SQL Azure comme magasin de données **cible** dans ce didacticiel. Si vous n’avez pas une base de données SQL Azure que vous pouvez utiliser dans le didacticiel hello, voir [comment toocreate et configurer une base de données SQL Azure](../sql-database/sql-database-get-started.md) toocreate une.
* **SQL Server 2012/2014 ou Visual Studio 2013**. Vous utilisez SQL Server Management Studio ou Visual Studio toocreate une base de données exemple et les données de résultat de salutation tooview dans la base de données hello.  

## <a name="collect-blob-storage-account-name-and-key"></a>Récupération du nom de compte Blob Storage et de la clé d'accès
Vous devez compte hello clé et le nom de votre stockage Azure compte toodo ce didacticiel. Notez le **nom** et la **clé** de votre compte de stockage Azure.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **davantage de services** sur hello gauche menu et sélectionnez **comptes de stockage**.

    ![Parcourir - Comptes de stockage](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. Bonjour **comptes de stockage** panneau, sélectionnez hello **compte de stockage Azure** que vous souhaitez toouse dans ce didacticiel.
4. Sélectionnez le lien **Clés d’accès** sous **PARAMÈTRES**.
5. Cliquez sur **copie** (image) bouton ensuite trop**nom de compte de stockage** texte zone et d’enregistrer/coller il quelque part (par exemple : dans un fichier texte).
6. Répétez hello précédente étape toocopy ou notez hello **key1**.

    ![Clé d’accès de stockage](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. Fermer tous les panneaux de hello en cliquant sur **X**.

## <a name="collect-sql-server-database-user-names"></a>Récupérer les noms de serveur SQL, de base de données et d’utilisateur
Vous devez les noms hello du serveur SQL Azure, de base de données et de toodo de l’utilisateur de ce didacticiel. Notez les noms du **serveur**, de la **base de données** et de **l’utilisateur** pour votre base de données SQL Azure.

1. Bonjour **portail Azure**, cliquez sur **davantage de services** sur hello gauche et sélectionnez **bases de données SQL**.
2. Bonjour **Panneau de bases de données SQL**, sélectionnez hello **base de données** que vous souhaitez toouse dans ce didacticiel. Notez les hello **nom de la base de données**.  
3. Bonjour **base de données SQL** panneau, cliquez sur **propriétés** sous **paramètres**.
4. Notez les valeurs hello pour **nom du serveur** et **ouverture de session de serveur ADMIN**.
5. Fermer tous les panneaux de hello en cliquant sur **X**.

## <a name="allow-azure-services-tooaccess-sql-server"></a>Autoriser les services Azure tooaccess SQL server
Vérifiez que **autoriser l’accès des services de tooAzure** paramètre désactivé **ON** pour votre serveur SQL Azure pour que ce service Data Factory hello peut accéder à votre serveur SQL Azure. tooverify et activer ce paramètre, hello comme suit :

1. Cliquez sur **davantage de services** hub dans hello gauche, cliquez sur **serveurs SQL**.
2. Sélectionnez votre serveur, puis cliquez sur **Pare-feu** sous **PARAMÈTRES**.
3. Bonjour **des paramètres de pare-feu** panneau, cliquez sur **ON** pour **autoriser l’accès des services de tooAzure**.
4. Fermer tous les panneaux de hello en cliquant sur **X**.

## <a name="prepare-blob-storage-and-sql-database"></a>Préparer Blob Storage et la Base de données SQL
À présent, préparer votre stockage d’objets blob Azure et de la base de données SQL Azure hello en effectuant hello comme suit :  

1. Lancez le Bloc-notes. Copier hello après le texte et l’enregistrer en tant que **emp.txt** trop**C:\ADFGetStarted** dossier sur votre disque dur.

    ```
    John, Doe
    Jane, Doe
    ```
2. Utiliser des outils tels que [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** hello conteneur et tooupload **emp.txt** conteneur toohello de fichier.

    ![Azure Storage Explorer. Copier des données à partir de la base de données tooSQL de stockage Blob](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. Hello utilisation suivant hello SQL script toocreate **emp** table dans votre base de données SQL Azure.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **Si vous disposez de SQL Server 2012/2014 installé sur votre ordinateur :** suivez les instructions à partir de [la gestion de Azure SQL Database à l’aide de SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server et exécutez hello SQL script. Cet article utilise hello [portail Azure classic](http://manage.windowsazure.com), pas hello [nouveau portail Azure](https://portal.azure.com), pare-feu tooconfigure pour un serveur SQL Azure.

    Si votre client n’est pas autorisé serveur SQL Azure de hello tooaccess, vous devez tooconfigure pare-feu pour votre accès tooallow du serveur SQL Azure à partir de votre ordinateur (adresse IP). Consultez [cet article](../sql-database/sql-database-configure-firewall-settings.md) pour le pare-feu étapes tooconfigure hello pour votre serveur SQL Azure.

## <a name="create-a-data-factory"></a>Créer une fabrique de données
Vous avez terminé la configuration requise de hello. Vous pouvez créer une fabrique de données à l’aide de hello suivant façons. Cliquez sur une des options de hello dans la liste déroulante de hello au haut de hello ou hello suivant liens tooperform hello didacticiel.     

* [Assistant de copie](data-factory-copy-data-wizard-tutorial.md)
* [Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
* [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa. Il ne transforme pas les données de sortie de données d’entrée tooproduce. Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer vos premières données tootransform de pipeline à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).
> 
> Vous pouvez chaîner les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, voir [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md). 
