---
title: "aaaDesign votre première base de données SQL Azure | Documents Microsoft"
description: "En savoir plus toodesign votre première base de données SQL Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a>Concevoir votre première base de données SQL Azure

Base de données SQL Azure est un relationnel de base de données comme un service (DBaaS) Bonjour Microsoft Cloud (« Azure »). Dans ce didacticiel, vous apprendrez comment toouse hello portail Azure et [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) pour : 

> [!div class="checklist"]
> * Créer une base de données Bonjour portail Azure
> * Définir une règle de pare-feu de niveau serveur Bonjour portail Azure
> * Connexion de base de données toohello avec SSMS
> * Créer des tables avec SSMS
> * Charger en masse des données avec BCP
> * Interroger ces données avec SSMS
> * Restaurer hello tooa de base de données précédente [point de restauration dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore) Bonjour portail Azure

Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, assurez-vous que vous avez installé :
- version la plus récente de Hello [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).
- version la plus récente de Hello [BCP et SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).

## <a name="log-in-toohello-azure-portal"></a>Ouvrez une session dans toohello portail Azure

Connectez-vous à toohello [portail Azure](https://portal.azure.com/).

## <a name="create-a-blank-sql-database"></a>Créer une base de données SQL vide

Une base de données SQL Azure est créée avec un ensemble défini de [ressources de calcul et de stockage](sql-database-service-tiers.md). base de données Hello est créé dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) et dans un [serveur logique de base de données SQL Azure](sql-database-features.md). 

Suivez ces étapes de toocreate une base de données SQL vide. 

1. Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

2. Sélectionnez **bases de données** de hello **nouveau** page, puis sélectionnez **base de données SQL** de hello **bases de données** page. 

   ![créer une base de données vide](./media/sql-database-design-first-database/create-empty-database.png)

3. Rempliront hello de base de données SQL avec hello suivant d’informations, comme indiqué dans le hello précédant l’image :   

   | Paramètre       | Valeur suggérée | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nom de la base de données** | mySampleDatabase | Pour les noms de base de données valides, consultez [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données). | 
   | **Abonnement** | Votre abonnement  | Pour plus d’informations sur vos abonnements, consultez [Abonnements](https://account.windowsazure.com/Subscriptions). |
   | **Groupe de ressources** | myResourceGroup | Pour les noms de groupe de ressources valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom). |
   | **Sélectionner une source** | Base de données vide | Indique qu’une base de données vide doit être créée. |

4. Cliquez sur **Server** toocreate et configurer un nouveau serveur pour votre nouvelle base de données. Remplir hello **nouveau formulaire serveur** avec hello informations suivantes : 

   | Paramètre       | Valeur suggérée | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nom du serveur** | Nom globalement unique | Pour les noms de serveur valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom). | 
   | **Connexion d’administrateur du serveur** | Nom valide | Pour les noms de connexion valides, consultez [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données).|
   | **Mot de passe** | Mot de passe valide | Votre mot de passe doit comporter au moins 8 caractères et contenir des caractères appartenant à trois des hello suivant catégories : les caractères majuscules, caractères en minuscules, des chiffres et des caractères non alphanumériques. |
   | **Emplacement** | Emplacement valide | Pour plus d’informations sur les régions, consultez [Régions Azure](https://azure.microsoft.com/regions/). |

   ![create database-server](./media//sql-database-design-first-database/create-database-server.png)

5. Cliquez sur **Sélectionner**.

6. Cliquez sur **niveau tarifaire** toospecify hello performances et la couche de niveau de service pour votre nouvelle base de données. Pour ce didacticiel, sélectionnez **20 DTU** et **250** Go de stockage.

   ![create database-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Cliquez sur **Apply**.  

8. Sélectionnez un **classement** pour la base de données vide hello (pour ce didacticiel, utiliser la valeur par défaut hello). Pour en savoir plus sur les classements, voir [Classements](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Cliquez sur **créer** base de données tooprovision hello. Approvisionnement prend sur un toocomplete une minute et demie. 

10. Dans la barre d’outils de hello, cliquez sur **Notifications** processus de déploiement toomonitor hello.

   ![notification](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>créer une règle de pare-feu au niveau du serveur ;

Hello service de base de données SQL crée un pare-feu à hello au niveau du serveur qui empêche des applications externes et des outils de se connecter toohello server ou des bases de données sur le serveur de hello, sauf si une règle de pare-feu est créée le pare-feu tooopen hello pour des adresses IP spécifiques. Suivez ces étapes toocreate un [règle de pare-feu de niveau serveur de base de données SQL](sql-database-firewall-configure.md) pour l’adressage IP de votre client et activer la connectivité externe via le pare-feu de base de données SQL hello pour votre adresse IP uniquement. 

> [!NOTE]
> SQL Database communique par le biais du port 1433. Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau. Dans ce cas, serveur de base de données SQL Azure tooyour ne peut pas se connecter à moins que votre service informatique s’ouvre le port 1433.
>

1. Une fois le déploiement de hello terminé, cliquez sur **bases de données SQL** de menu à gauche hello, puis cliquez sur **mySampleDatabase** sur hello **bases de données SQL** page. nom de serveur complet Hello page Vue d’ensemble de votre base de données ouvre, affichant vous hello entièrement (tel que **mynewserver20170313.database.windows.net**) et fournit des options de configuration supplémentaire. Copiez ce nom de serveur complet pour une utilisation ultérieure.

   > [!IMPORTANT]
   > Vous avez besoin de ce serveur complet nom tooconnect tooyour ses bases de données et dans les Démarrages rapides suivants.
   > 

   ![nom du serveur](./media/sql-database-connect-query-dotnet/server-name.png) 

2. Cliquez sur **définir serveur pare-feu** barre d’outils hello comme indiqué dans l’image précédente de hello. Hello **des paramètres de pare-feu** page serveur de base de données SQL hello s’ouvre. 

   ![règle de pare-feu de serveur](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Cliquez sur **ajouter l’adresse IP du client** sur tooadd de barre d’outils hello votre adresse IP actuelle d’adresses tooa nouvelle règle de pare-feu. Une règle de pare-feu peut ouvrir le port 1433 pour une seule adresse IP ou une plage d’adresses IP.

4. Cliquez sur **Enregistrer**. Une règle de pare-feu de niveau serveur est créée pour votre adresse IP actuelle, ouvrir le port 1433 sur le serveur logique de hello.

   ![définir la règle de pare-feu de serveur](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Cliquez sur **OK** , puis fermez hello **des paramètres de pare-feu** page.

Vous pouvez désormais connecter le serveur de base de données SQL toohello et ses bases de données à l’aide de SQL Server Management Studio ou un autre outil de votre choix à partir de cette adresse IP à l’aide du compte d’administrateur de serveur hello créé précédemment.

> [!IMPORTANT]
> Par défaut, l’accès via le pare-feu de base de données SQL hello est activé pour tous les services Azure. Cliquez sur **OFF** sur toodisable de cette page pour tous les services Azure.

## <a name="sql-server-connection-information"></a>Informations de connexion SQL Server

Obtenir le nom du serveur complet hello pour votre serveur de base de données SQL Azure Bonjour portail Azure. Vous utilisez hello complet nom tooconnect tooyour serveur à l’aide de SQL Server Management Studio.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page. 
3. Bonjour **Essentials** volet Bonjour page du portail Azure pour votre base de données, recherchez et copiez hello **nom du serveur**.

   ![informations de connexion](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a>Connexion de base de données toohello avec SSMS

Utilisez [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish un serveur de base de données SQL Azure de tooyour de connexion.

1. Ouvrez SQL Server Management Studio.

2. Bonjour **connecter tooServer** boîte de dialogue, entrez hello informations suivantes :

   | Paramètre       | Valeur suggérée | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | Type de serveur | Moteur de base de données | Cette valeur est obligatoire |
   | Nom du serveur | nom du serveur complet Hello | Hello nom doit être semblable à celui-ci : **mynewserver20170313.database.windows.net**. |
   | Authentification | l’authentification SQL Server | L’authentification SQL est hello seul type d’authentification que nous avons configuré dans ce didacticiel. |
   | Connexion | compte d’administrateur serveur Hello | Il s’agit de compte hello que vous avez spécifié lors de la création du serveur de hello. |
   | Mot de passe | mot de passe Hello pour votre compte d’administrateur de serveur | Il s’agit d’un mot de passe hello que vous avez spécifié lors de la création du serveur de hello. |

   ![se connecter tooserver](./media/sql-database-connect-query-ssms/connect.png)

3. Cliquez sur **Options** Bonjour **connecter tooserver** boîte de dialogue. Bonjour **connecter toodatabase** section, entrez **mySampleDatabase** tooconnect toothis base de données.

   ![se connecter toodb sur le serveur](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Cliquez sur **Connecter**. Ouvre la fenêtre de l’Explorateur d’objets Hello dans SSMS. 

5. Dans l’Explorateur d’objets, développez **bases de données** , puis **mySampleDatabase** tooview des objets de hello dans la base de données exemple hello.

   ![objets de base de données](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a>Créer des tables dans la base de données hello 

Créez un schéma de base de données avec quatre tables qui modélisent un système de gestion des étudiants pour les universités à l’aide de [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference) :

- Personne
- Cours
- Étudiant
- Attribuez à ce modèle un système de gestion des étudiants pour les universités

Hello diagramme suivant montre comment ces tables sont associée tooeach autres. Certaines de ces tables référencent des colonnes d’autres tables. Par exemple, table de Student hello référence hello **PersonId** colonne Hello **personne** table. Étude hello diagramme toounderstand comment hello tables dans ce didacticiel sont associée tooone une autre. Pour des explications approfondies sur la façon de tables de base de données efficace toocreate, consultez [créer des tables de base de données efficace](https://msdn.microsoft.com/library/cc505842.aspx). Pour plus d’informations sur le choix des types de données, consultez [Types de données](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).

> [!NOTE]
> Vous pouvez également utiliser hello [Concepteur de tables dans SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate et concevoir vos tables. 

![Relations entre les tables](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. Dans l’Explorateur d’objets, cliquez avec le bouton droit sur **mySampleDatabase**, puis cliquez sur **Nouvelle requête**. Une fenêtre de requête vide s’ouvre tooyour connecté de base de données.

2. Dans la fenêtre de requête hello, exécutez hello requête toocreate quatre tables suivantes dans votre base de données : 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![créez des tables](./media/sql-database-design-first-database/create-tables.png)

3. Développez le nœud de « tables » de hello dans les tables hello hello SQL Server Management Studio Object explorer toosee que vous avez créé.

   ![tables ssms-créées](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a>Charger des données dans les tables de hello

1. Créez un dossier appelé **SampleTableData** dans vos données d’exemple toostore dossier Téléchargements pour votre base de données. 

2. Suivant de hello avec le bouton des liens et les enregistrer dans hello **SampleTableData** dossier. 

   - [SampleCourseData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [SamplePersonData](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [SampleStudentData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [SampleCreditData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. Ouvrez une fenêtre d’invite de commandes et accédez toohello SampleTableData dossier.

4. Exécutez hello suivant des données d’exemple tooinsert commandes dans des tables hello en remplaçant les valeurs hello pour **nom_serveur**, **DatabaseName**, **nom d’utilisateur**et **Mot de passe** avec les valeurs hello pour votre environnement.
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

Vous avez maintenant chargé des exemples de données dans des tables hello que vous avez créé précédemment.

## <a name="query-data"></a>Données de requête

Exécutez hello suivant informations tooretrieve de requêtes à partir des tables de base de données hello. Consultez [l’écriture des requêtes SQL](https://technet.microsoft.com/library/bb264565.aspx) toolearn plus d’informations sur l’écriture de requêtes SQL. requête de première Hello joint toutes les quatre tables toofind tous les étudiants hello traités par ' Dominick ce protocole » qui ont un niveau supérieur à 75 % de sa classe. requête de deuxième Hello joint les quatre tables et recherche tous les cours dans lequel 'Noe Coleman' a déjà inscrit.

1. Dans une fenêtre de requête SQL Server Management Studio, exécutez hello suivant la requête :

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. Dans une fenêtre de requête SQL Server Management Studio, exécutez la requête suivante :

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurer un état antérieur de tooa de base de données dans le temps

Imaginez que vous avez supprimé une table par inadvertance. Il s’agit de quelque chose que vous ne pouvez pas récupérer facilement. Base de données SQL Azure vous permet de toogo tooany précédent point dans le temps dans hello dernière too35 jours et de restauration ce point dans le temps tooa nouvelle base de données. Vous pouvez utiliser cette base de données toorecover les données supprimées. Hello suit point de restauration hello exemple de base de données tooa avant l’ajout de tables de hello.

1. Dans la page de base de données SQL hello pour votre base de données, cliquez sur **restaurer** sur la barre d’outils hello. Hello **restaurer** ouvrir la page.

   ![restauration](./media/sql-database-design-first-database/restore.png)

2. Remplir hello **restaurer** formulaire avec les informations de hello requis :
    * Nom de la base de données : entrez un nom pour la base de données 
    * Point-à-temps : Hello Select **Point-à-temps** onglet sur le formulaire de restauration hello 
    * Point de restauration : sélectionnez une heure qui se produit avant la modification de la base de données hello
    * Serveur cible : Vous ne pouvez pas modifier cette valeur lors de la restauration d’une base de données 
    * Pool de base de données élastique : sélectionnez **Aucun**  
    * Niveau tarifaire : sélectionnez **20 DTU** et **250 Go** de stockage.

   ![point de restauration](./media/sql-database-design-first-database/restore-point.png)

3. Cliquez sur **OK** toorestore hello de base de données trop[restaurer tooa point dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore) avant l’ajout de tables de hello. Restauration d’un point différent de tooa de base de données dans le temps crée une base de données en double dans hello même serveur que la base de données d’origine hello as of point hello dans le temps que vous spécifiez, tant qu’elle se trouve dans la période de rétention hello pour votre [niveau de service](sql-database-service-tiers.md).

## <a name="next-steps"></a>Étapes suivantes 
Dans ce didacticiel, vous avez appris les tâches de base de données telles que la création une base de données et les tables, charger et interroger des données et restaurer le point précédent du tooa hello de base de données dans le temps. Vous avez appris à effectuer les actions suivantes :
> [!div class="checklist"]
> * Créer une base de données
> * Configurer une règle de pare-feu
> * Se connecter à base de données toohello avec [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)
> * créez des tables
> * Charger des données en bloc
> * Interroger ces données
> * Restaurer le point précédent du tooa hello de base de données dans le temps à l’aide de la base de données SQL [point de restauration dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore) fonctionnalités

Avance toohello toolearn de didacticiel suivant sur la conception d’une base de données à l’aide de Visual Studio et c#.

> [!div class="nextstepaction"]
>[Concevoir une base de données SQL Azure et se connecter avec C# et ADO.NET](sql-database-design-first-database-csharp.md)
