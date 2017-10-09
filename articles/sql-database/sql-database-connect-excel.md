---
title: "aaaConnect Excel tooSQL de base de données | Documents Microsoft"
description: "Découvrez comment tooconnect Microsoft Excel tooAzure SQL de base de données dans le cloud de hello. Importez des données dans Excel pour les rapports et l’exploration des données."
services: sql-database
keywords: "connecter excel toosql, importer des données tooexcel"
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>Connexion de base de données SQL Azure Excel tooan et créer un rapport

Connexion de base de données SQL de tooa Excel dans le cloud de hello et importer des données et créer des tables et des graphiques basés sur des valeurs dans la base de données hello. Dans ce didacticiel, que vous allez configurer la connexion hello entre Excel et une table de base de données, enregistrez le fichier hello qui stocke les informations de connexion de données et hello pour Excel et puis créer un graphique croisé dynamique à partir de hello les valeurs de base de données.

Vous avez besoin d’une base de données SQL dans Azure avant de commencer. Si vous n’en avez pas, consultez [créer votre première base de données SQL](sql-database-get-started-portal.md) tooget une base de données avec des exemples de données opérationnel en quelques minutes. Dans cet article, vous allez importer des données d’exemple dans Excel à partir de cet article, mais vous pouvez suivre les mêmes étapes avec vos propres données.

Vous aurez besoin d’une copie d’Excel. Cet article utilise [Microsoft Excel 2016](https://products.office.com/).

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>Connexion de base de données Excel tooa SQL et créer un fichier odc
1. base de données tooconnect Excel tooSQL, ouvrez Excel et créer un nouveau classeur ou ouvrir un classeur Excel existant.
2. Dans la barre de menus de hello en hello haut hello cliquez sur **données**, cliquez sur **à partir d’autres Sources**, puis cliquez sur **à partir de SQL Server**.
   
   ![Sélectionner les données source : connecter Excel tooSQL base de données.](./media/sql-database-connect-excel/excel_data_source.png)
   
   Hello Assistant connexion de données s’ouvre.
3. Bonjour **connecter tooDatabase Server** boîte de dialogue, hello du type de base de données SQL **nom du serveur** tooconnect tooin hello formulaire <*nom_serveur* > **. database.windows.net**. Par exemple, **adworkserver.database.windows.net**.
4. Sous **références de connexion**, cliquez sur **hello utilisation après le nom d’utilisateur et mot de passe**, hello de type **nom d’utilisateur** et **mot de passe** configurez pour Hello le serveur de base de données SQL lors de sa création, puis cliquez sur **suivant**.
   
   ![Tapez les informations d’identification nom et la connexion de serveur hello](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > Selon votre environnement réseau, vous n’êtes peut-être pas en mesure de tooconnect ou vous risquez de perdre les connexions hello si le serveur de base de données SQL hello n’autorise pas le trafic à partir de votre adresse IP du client. Accédez toohello [portail Azure](https://portal.azure.com/)et cliquez sur serveurs SQL Server, cliquez sur votre serveur, cliquez sur pare-feu sous paramètres ajouter votre adresse IP du client. Consultez [comment les paramètres de pare-feu de tooconfigure](sql-database-configure-firewall-settings.md) pour plus d’informations.
   > 
   > 
5. Bonjour **sélectionner une base de données et de Table** boîte de dialogue, base de données Sélectionnez hello vous souhaitez toowork avec à partir de la liste de hello, puis cliquez sur les tables de hello ou des vues que vous souhaitez toowork avec (nous avons choisi **vGetAllCategories**), puis Cliquez sur **suivant**.
   
    ![Sélectionner une base de données et une table](./media/sql-database-connect-excel/select-database-and-table.png)
   
    Hello **enregistrer un fichier de connexion de données et fin** boîte de dialogue s’ouvre, où vous fournissez des informations sur hello Office de base de données (*.odc) fichier de connexion utilisé par Excel. Vous pouvez laisser les valeurs par défaut hello ou personnaliser vos sélections.
6. Vous pouvez laisser les valeurs par défaut de hello, mais les hello Remarque **nom de fichier** en particulier. A **Description**, un **nom convivial**, et **mots clés de recherche** vous aider à et d’autres utilisateurs n’oubliez pas que vous vous connectez tooand de trouver la connexion de hello. Cliquez sur **toujours tentez toouse ce fichier de données de toorefresh** si vous souhaitez que les informations de connexion stockées dans un fichier odc de hello peut mettre à jour lorsque vous connectez tooit, puis cliquez sur **Terminer**.
   
    ![Enregistrement d’un fichier odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    Hello **importer des données** boîte de dialogue s’affiche.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Importer des données de hello dans Excel et créer un graphique croisé dynamique
Maintenant que vous avez établi la connexion de hello et hello créé avec les informations de connexion et les données, vous lisez les données de salutation tooimport.

1. Bonjour **importer des données** boîte de dialogue, cliquez sur hello voulue pour la présentation de vos données dans la feuille de calcul hello **OK**. Nous avons choisi **Graphique croisé dynamique**. Vous pouvez également choisir toocreate un **nouvelle feuille de calcul** ou trop**ajouter ce modèle de données de tooa données**. Pour plus d’informations sur les modèles de données, consultez la page [Créer un modèle de données dans Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B). Cliquez sur **propriétés** tooexplore informations hello odc fichier vous avez créé dans hello étape et toochoose options précédentes pour l’actualisation des données de salutation.
   
    ![En choisissant l’option format hello pour les données dans Excel](./media/sql-database-connect-excel/import-data.png)
   
    feuille de calcul Hello dispose maintenant d’un tableau croisé dynamique vide et graphique.
2. Sous **PivotTable Fields**, sélectionnez tous les hello des cases à cocher pour hello champs tooview.
   
    ![Configurez le rapport de base de données.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> Si vous souhaitez tooconnect autres classeurs et des feuilles de calcul toohello base de données Excel, cliquez sur **données**, cliquez sur **connexions**, cliquez sur **ajouter**, choisissez la connexion hello vous avez créé dans la liste de hello, puis cliquez sur **ouvrir**.
> ![Ouvrir une connexion à partir d’un autre classeur](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[connecter tooSQL de base de données avec SQL Server Management Studio](sql-database-connect-query-ssms.md) avancés d’analyse et interrogation.
* En savoir plus sur les avantages de hello de [pools élastiques](sql-database-elastic-pool.md).
* Découvrez comment trop[créer une application web qui se connecte tooSQL de base de données sur les principaux hello](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).

