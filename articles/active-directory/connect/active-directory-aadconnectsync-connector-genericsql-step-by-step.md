---
title: "aaaGeneric étape par le connecteur SQL étape | Documents Microsoft"
description: "Cet article est en marche vous via un système de ressources humaines simple à l’aide de pas à pas hello connecteur SQL générique."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>Connecteur SQL générique - Guide pas à pas
Cette rubrique est un guide pas à pas. Elle explique comment créer un simple exemple de base de données Ressources humaines et l’utiliser pour importer certains utilisateurs et leur appartenance à un groupe.

## <a name="prepare-hello-sample-database"></a>Préparer la base de données exemple hello
Sur un serveur exécutant SQL Server, exécuter un script SQL hello trouvé dans [annexe A](#appendix-a). Ce script crée une base de données portant le nom hello GSQLDEMO. modèle d’objet Hello pour hello créé ressemble de base de données de cette image :  
![Modèle objet](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

Également créer un utilisateur de base de données de toouse tooconnect toohello. Dans cette procédure pas à pas, hello utilisateur appelée FABRIKAM\SQLUser et situé dans le domaine de hello.

## <a name="create-hello-odbc-connection-file"></a>Créer le fichier de connexion ODBC hello
Hello connecteur SQL générique à l’aide de ODBC tooconnect toohello à distance. Tout d’abord, nous devons toocreate un fichier avec les informations de connexion ODBC de hello.

1. Démarrer l’utilitaire de gestion hello ODBC sur votre serveur :  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. Onglet de hello sélectionnez **DSN de fichier**. Cliquez sur **Ajouter...**.  
   ![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. Hello out-of-box pilote fonctionne fine, par conséquent, sélectionnez-le, puis cliquez sur **suivante >**.  
   ![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. Nommez le fichier de hello, tel que **GenericSQL**.  
   ![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. Cliquez sur **Terminer**.  
   ![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. Connexion au moment tooconfigure hello. Donner de source de données hello une bonne description et fournir le nom hello du serveur hello exécutant SQL Server.  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. Sélectionnez la façon dont tooauthenticate avec SQL. Dans ce cas, nous utilisons l’authentification Windows.  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. Fournir le nom hello de base de données exemple hello **GSQLDEMO**.  
   ![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. Conservez toutes les valeurs par défaut sur cet écran. Cliquez sur **Terminer**.  
   ![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. tooverify que tout fonctionne comme prévu, cliquez sur **Source de données de Test**.  
    ![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. Vérifiez que hello test est réussi.  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. fichier de configuration Hello ODBC doit maintenant être visible dans le fichier DSN.  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

Nous disposons de fichier hello vous avez besoin et que vous pouvez commencer à créer hello connecteur.

## <a name="create-hello-generic-sql-connector"></a>Créer hello connecteur SQL générique
1. Dans le Gestionnaire de Service de synchronisation UI de hello, sélectionnez **connecteurs** et **créer**. Sélectionnez **SQL générique (Microsoft)** et donnez-lui un nom descriptif.  
   ![Connecteur1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. Trouver le fichier de source de données hello que vous avez créé dans la section précédente de hello et téléchargez-le toohello server. Fournir de base de données toohello tooconnect des informations d’identification hello.  
   ![Connecteur2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. Pour simplifier cette procédure pas à pas, disons qu’il existe deux types d’objet : **Utilisateur** et **Groupe**.
   ![Connecteur3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. attributs de hello toofind, nous souhaitons hello connecteur toodetect ces attributs en examinant la table hello elle-même. Étant donné que **utilisateurs** est un mot réservé dans SQL, nous devons tooprovide dans le carré des crochets [].  
   ![Connecteur4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. Attribut d’ancrage temps toodefine hello et attribut DN de hello. Pour **utilisateurs**, nous utilisons la combinaison de hello de hello deux attributs username et EmployeeID. Pour **Groupe**, nous utilisons GroupName (rappelons qu’il ne s’agit ici que d’un exemple).
   ![Connecteur5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. Tous les types d’attribut ne peuvent pas être détectés dans une base de données SQL, type d’attribut de référence de Hello en particulier ne peut pas. Pour le type d’objet groupe de hello, nous devons toochange hello OwnerID et MemberID tooreference.  
   ![Connecteur6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. attributs de Hello que nous avons sélectionné comme attributs de référence à l’étape précédente de hello nécessitent le type d’objet hello à que ces valeurs sont une référence. Dans notre cas, hello type d’objet utilisateur.  
   ![Connecteur7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. Sur la page de paramètres globaux de hello, sélectionnez **filigrane** en tant que stratégie de delta hello. Tapez également dans le format de date/heure hello **AAAA-MM-JJ HH : mm :**.
   ![Connecteur8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. Sur hello **configurer des Partitions et des hiérarchies** , sélectionnez les deux types d’objets.
   ![Connecteur9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. Sur hello **sélectionner les Types d’objet** et **sélectionner les attributs**, sélectionnez les types d’objet et tous les attributs. Sur hello **configurer des points d’ancrage** , cliquez sur **Terminer**.

## <a name="create-run-profiles"></a>Créer les profils d’exécution
1. Dans le Gestionnaire de Service de synchronisation UI de hello, sélectionnez **connecteurs**, et **configurer des profils d’exécution**. Cliquez sur **Nouveau profil**. Nous commençons par **Importation intégrale**.  
   ![ProfilExecution1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. Sélectionnez le type de hello **importation intégrale (phase uniquement)**.  
   ![ProfilExecution2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. Sélectionnez la partition de hello **objet = utilisateur**.  
   ![ProfilExecution3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. Sélectionnez **Table** et tapez **[USERS]**. Défiler vers le bas la section de type d’objet à valeurs multiples toohello et entrer des données hello comme hello illustration suivante. Sélectionnez **Terminer** étape de hello toosave.  
   ![ProfilExecution4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![ProfilExecution4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. Sélectionnez **Nouvelle étape**. Cette fois, sélectionnez **OBJECT=Group**. Sur la dernière page de hello, utilisez la configuration hello comme hello illustration suivante. Cliquez sur **Terminer**.  
   ![ProfilExecution5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![ProfilExecution5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. Facultatif : si vous le souhaitez, vous pouvez configurer des profils d’exécution supplémentaires. Pour cette procédure pas à pas, uniquement hello importation intégrale est utilisé.
7. Cliquez sur **OK** toofinish modification de profils d’exécution.

## <a name="add-some-test-data-and-test-hello-import"></a>Ajouter des test d’importation hello données et de test
Remplissez quelques données de test dans votre exemple de base de données. Lorsque vous êtes prêt, sélectionnez **Exécuter** et **Importation intégrale**.

Voici un utilisateur avec deux numéros de téléphone et un groupe avec quelques membres.  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>Annexe A
**Base de données SQL script toocreate hello exemple**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
