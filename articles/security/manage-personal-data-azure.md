---
title: "aaaManage des données personnelles dans Microsoft Azure | Documents Microsoft"
description: "obtenir des conseils sur la façon dont toocorrect, mettre à jour, supprimer et exporter des données personnelles dans Azure Active Directory et de la base de données SQL Azure"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a>Gérer les données personnelles dans Microsoft Azure

Cet article fournit des conseils sur la façon dont toocorrect, mettre à jour, supprimer et exporter des données personnelles dans Azure Active Directory et de la base de données SQL Azure.

## <a name="scenario"></a>Scénario

Une société de Dublin fournit guichet unique pour mariage de destination haut de gamme en Irlande et autour Bonjour pour à la fois une base de client local et international. Ils ont des bureaux, clients, employés et fournisseurs situés dans des lieux hello hello world toofully service qu’elles proposent.

Parmi les nombreux autres éléments, société de hello effectue le suivi de RSVP qui incluent des allergies alimentaires et préférences alimentaires. Les invités mariage enregistrez pour diverses activités telles que horseback riding, de navigation, bateau trajets, etc. et même interagissent entre eux sur une page web central au cours des mois hello mènent toohello événement. société de Hello recueille des informations personnelles à partir des employés, les fournisseurs, les clients et les invités de mariage. En raison de hello nature internationale de hello hello société doit être conforme à plusieurs niveaux du règlement.

## <a name="problem-statement"></a>Définition du problème

- Admins de données doit être toocorrect en mesure d’inexactes mise à jour et des informations incomplètes ou modifiées personnelles informations personnelles.

- Nécessité d’administrateurs de données doit être en mesure de toodelete des informations personnelles à la demande de hello d’un objet de données.

- Admins de données besoin tooexport de données et fournir tooa concernée dans un format commun et structurée sur sa demande.

## <a name="company-goals"></a>Objectifs de la société

- Les informations inexactes ou incomplètes sur les clients, les invités du mariage, les employés et les fournisseurs doivent être corrigées ou mises à jour dans Azure Active Directory et Azure SQL Database.

- Les informations personnelles doivent être supprimées dans Azure Active Directory et de la base de données SQL Azure à la demande de hello d’un objet de données.

- Les données personnelles doivent être exportées dans un format commun et structuré sur demande hello d’un objet de données.

## <a name="solutions"></a>Solutions

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a>Azure Active Directory : rectifier/corriger des données personnelles inexactes ou incomplètes et effacer/supprimer des données personnelles/profils utilisateur

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) est le service Microsoft de gestion d’annuaires et d’identités multilocataire basé sur le cloud.
Vous pouvez corriger, mettre à jour ou supprimer des profils utilisateur clients et des employés et les informations de travail utilisateur qui contiennent des données personnelles, telles que le nom, titre de travail, adresse ou numéro de téléphone d’un utilisateur dans votre [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (DAS) environnement à l’aide de hello [portail Azure](https://portal.azure.com/).

Vous devez vous connecter avec un compte qui est un administrateur global pour le répertoire de hello.

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a>Comment corriger ou mettre à jour des informations professionnelles et de profil utilisateur dans Azure Active Directory ?

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.

2. Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **utilisateurs**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. Sur hello **les utilisateurs et groupes d’utilisateurs -** panneau, sélectionnez un utilisateur à partir de la liste de hello, puis, dans Panneau de hello pour l’utilisateur sélectionné de hello, **profil** informations de profil tooview hello utilisateur nécessitant toobe corrigé ou mis à jour.

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. Corriger ou mettre à jour les informations de hello et, dans la barre de commandes hello, sélectionnez **enregistrer.**

6.  Dans le panneau hello pour l’utilisateur sélectionné de hello, sélectionnez **Info de travail** tooview utilisateur travail informations dont a besoin toobe corrigée ou mis à jour.

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. Corriger ou mettre à jour les informations de travail utilisateur hello et, dans la barre de commandes hello, sélectionnez **enregistrer.**

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a>Comment supprimer un profil utilisateur dans Azure Active Directory ?

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.

2. Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.

    ![](media/manage-personal-data-azure/image001.png)

3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **utilisateurs**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. Sur hello **les utilisateurs et groupes d’utilisateurs -** panneau, sélectionnez un utilisateur à partir de la liste de hello.

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. Dans le panneau hello pour l’utilisateur sélectionné de hello, sélectionnez **vue d’ensemble**, puis, dans la barre de commandes hello, sélectionnez **supprimer**.

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a>SQL Database : rectifier/corriger des données personnelles inexactes ou incomplètes ; effacer/supprimer des données personnelles ; exporter des données personnelles 

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) est une base de données cloud qui permet aux développeurs de créer et tenir à jour des applications.

Les données personnelles peuvent être mises à jour dans [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) à l’aide de requêtes SQL standard et peuvent aussi être supprimées. En outre, les données personnelles peuvent être exportées à partir de la base de données SQL à l’aide de plusieurs méthodes, y compris hello import Azure SQL Server et l’Assistant Exportation et dans divers formats, y compris un fichier BACPAC.

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a>Comment corriger, mettre à jour ou supprimer des données personnelles dans SQL Database ?

toolearn comment toocorrect ou mise à jour des données personnelles dans la base de données SQL, visitez hello [mise à jour (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [mettre à jour le texte](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [mettre à jour avec l’Expression de Table commune](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), ou [ Mettre à jour écrire le texte](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.

toolearn comment toodelete des données personnelles dans la base de données SQL, visitez hello [supprimer (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a>Comment exporter le fichier BACPAC tooa de données personnelles dans la base de données SQL ?

Un fichier BACPAC inclut les métadonnées et les données de base de données SQL hello et est un fichier zip avec une extension de fichier BACPAC. Cela est possible à l’aide de hello [portail Azure](https://portal.azure.com/), hello SQLPackage utilitaire de ligne de commande, SQL Server Management Studio (SSMS) ou PowerShell.

toolearn comment tooexport tooa BACPAC fichier, visitez hello [exporter un fichier BACPAC de tooa de base de données SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, ce qui inclut des instructions détaillées pour chaque méthode répertoriés ci-dessus.

Comment exporter des données personnelles à partir de la base de données SQL hello SQL Server Import et l’Assistant Exportation ?

Cet Assistant vous permet de copier des données à partir d’une source de destination tooa. Pour un Assistant toohello introduction, y compris comment tooget, informations sur les autorisations et comment aider à tooget avec l’outil de hello, visitez hello [et exporter des données avec SQL Server Import de hello Assistant Importation et exportation](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) page web.

Pour une vue d’ensemble des étapes de l’Assistant de hello, visitez hello [étapes hello SQL Server Import et Assistant Exportation](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) page web.

## <a name="next-steps"></a>Étapes suivantes :

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

