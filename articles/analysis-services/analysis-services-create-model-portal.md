---
title: "aaaCreate un modèle tabulaire à l’aide du Concepteur Web Azure Analysis Services de hello | Documents Microsoft"
description: "Découvrez comment toocreate un modèle tabulaire Azure Analysis Services à l’aide de hello Concepteur Web dans le portail Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a>Créer un modèle dans le portail Azure

fonctionnalité de concepteur (version préliminaire) Hello Azure Analysis Services web dans le portail Azure fournit un moyen simple et rapide de toocreate et modifier les modèles tabulaires et droite de données de modèle de requête dans votre navigateur. 

N’oubliez pas, le concepteur web hello est **aperçu**. Lors de la nouvelle fonctionnalité est ajoutée toutes les périodes de hello, dans l’aperçu, la fonctionnalité est limitée. Pour plus avancées développement de modèles et de test, il est meilleure toouse Visual Studio (SSDT) et SQL Server Management Studio (SSMS).

## <a name="prerequisites"></a>Composants requis

- Un serveur Azure Analysis Services au niveau Standard ou Developer de hello. Nouveaux modèles créés à l’aide du Concepteur de sites Web hello sont DirectQuery, pris en charge uniquement par ces couches.
- Un fichier Azure SQL Database, Azure SQL Data Warehouse ou Power BI Desktop (.pbix) comme source de données. Les modèles créés à partir de fichiers Power BI Desktop prennent en charge les sources de données Azure SQL Database, Azure SQL Data Warehouse, Oracle et Teradata.
- Un compte SQL Server et le mot de passe pour la connexion des sources de données de base de données SQL ou Azure SQL Data Warehouse tooAzure.

## <a name="toocreate-a-new-tabular-model"></a>toocreate un nouveau modèle tabulaire

1. Dans le panneau **Vue d’ensemble** > **Concepteur web** de votre serveur, cliquez sur **Ouvrir**.

    ![Créer un modèle dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. Dans **Concepteur web** > **Modèles**, cliquez sur **Ajouter**.

    ![Créer un modèle dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. Dans **Nouveau modèle**, tapez un nom de modèle, puis sélectionnez une source de données.

    ![Boîte de dialogue Nouveau modèle dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. Dans **connexion**, entrez les propriétés de connexion hello. Le nom d’utilisateur et le mot de passe doivent correspondre à un compte SQL Server.

     ![Boîte de dialogue Connexion dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. Dans **Tables et vues**, sélectionnez hello tables tooinclude dans votre modèle, puis cliquez sur **créer**. Les relations sont créées automatiquement entre les tables avec une paire de clés.

     ![Sélectionner les tables et les vues](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

Votre nouveau modèle s’affiche dans votre navigateur. À ce stade, vous pouvez :   

- Données de modèle de requête en faisant glisser le Concepteur de requêtes toohello de champs et en ajoutant des filtres.
- Créer des mesures dans les tables.
- Modifier les métadonnées du modèle à l’aide de l’éditeur json hello.
- Ouvrez le modèle de hello dans Visual Studio (SSDT), Power BI Desktop ou Excel.

![Sélectionner les tables et les vues](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> Lorsque vous modifiez les métadonnées du modèle ou créez de nouvelles mesures dans votre navigateur, vous enregistrez ces modèle tooyour de modifications dans Azure. Si vous travaillez également sur votre modèle dans SSDT, Power BI Desktop ou Excel, il peut être désynchronisé.


## <a name="next-steps"></a>Étapes suivantes 
[Gérer les utilisateurs et rôles de bases de données](analysis-services-database-users.md)  
[Connexion avec Excel](analysis-services-connect-excel.md)  


