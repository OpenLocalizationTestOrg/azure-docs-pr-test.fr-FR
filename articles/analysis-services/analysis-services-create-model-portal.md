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
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="b6707-103">Créer un modèle dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b6707-103">Create a model in Azure portal</span></span>

<span data-ttu-id="b6707-104">fonctionnalité de concepteur (version préliminaire) Hello Azure Analysis Services web dans le portail Azure fournit un moyen simple et rapide de toocreate et modifier les modèles tabulaires et droite de données de modèle de requête dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="b6707-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="b6707-105">N’oubliez pas, le concepteur web hello est **aperçu**.</span><span class="sxs-lookup"><span data-stu-id="b6707-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="b6707-106">Lors de la nouvelle fonctionnalité est ajoutée toutes les périodes de hello, dans l’aperçu, la fonctionnalité est limitée.</span><span class="sxs-lookup"><span data-stu-id="b6707-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="b6707-107">Pour plus avancées développement de modèles et de test, il est meilleure toouse Visual Studio (SSDT) et SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="b6707-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6707-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b6707-108">Prerequisites</span></span>

- <span data-ttu-id="b6707-109">Un serveur Azure Analysis Services au niveau Standard ou Developer de hello.</span><span class="sxs-lookup"><span data-stu-id="b6707-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="b6707-110">Nouveaux modèles créés à l’aide du Concepteur de sites Web hello sont DirectQuery, pris en charge uniquement par ces couches.</span><span class="sxs-lookup"><span data-stu-id="b6707-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="b6707-111">Un fichier Azure SQL Database, Azure SQL Data Warehouse ou Power BI Desktop (.pbix) comme source de données.</span><span class="sxs-lookup"><span data-stu-id="b6707-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="b6707-112">Les modèles créés à partir de fichiers Power BI Desktop prennent en charge les sources de données Azure SQL Database, Azure SQL Data Warehouse, Oracle et Teradata.</span><span class="sxs-lookup"><span data-stu-id="b6707-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="b6707-113">Un compte SQL Server et le mot de passe pour la connexion des sources de données de base de données SQL ou Azure SQL Data Warehouse tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b6707-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="b6707-114">toocreate un nouveau modèle tabulaire</span><span class="sxs-lookup"><span data-stu-id="b6707-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="b6707-115">Dans le panneau **Vue d’ensemble** > **Concepteur web** de votre serveur, cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="b6707-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Créer un modèle dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="b6707-117">Dans **Concepteur web** > **Modèles**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b6707-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Créer un modèle dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="b6707-119">Dans **Nouveau modèle**, tapez un nom de modèle, puis sélectionnez une source de données.</span><span class="sxs-lookup"><span data-stu-id="b6707-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Boîte de dialogue Nouveau modèle dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="b6707-121">Dans **connexion**, entrez les propriétés de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="b6707-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="b6707-122">Le nom d’utilisateur et le mot de passe doivent correspondre à un compte SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b6707-122">Username and password must be a SQL Server account.</span></span>

     ![Boîte de dialogue Connexion dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="b6707-124">Dans **Tables et vues**, sélectionnez hello tables tooinclude dans votre modèle, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="b6707-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="b6707-125">Les relations sont créées automatiquement entre les tables avec une paire de clés.</span><span class="sxs-lookup"><span data-stu-id="b6707-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Sélectionner les tables et les vues](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="b6707-127">Votre nouveau modèle s’affiche dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="b6707-127">Your new model appears in your browser.</span></span> <span data-ttu-id="b6707-128">À ce stade, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="b6707-128">From here, you can:</span></span>   

- <span data-ttu-id="b6707-129">Données de modèle de requête en faisant glisser le Concepteur de requêtes toohello de champs et en ajoutant des filtres.</span><span class="sxs-lookup"><span data-stu-id="b6707-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="b6707-130">Créer des mesures dans les tables.</span><span class="sxs-lookup"><span data-stu-id="b6707-130">Create new measures in tables.</span></span>
- <span data-ttu-id="b6707-131">Modifier les métadonnées du modèle à l’aide de l’éditeur json hello.</span><span class="sxs-lookup"><span data-stu-id="b6707-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="b6707-132">Ouvrez le modèle de hello dans Visual Studio (SSDT), Power BI Desktop ou Excel.</span><span class="sxs-lookup"><span data-stu-id="b6707-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Sélectionner les tables et les vues](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="b6707-134">Lorsque vous modifiez les métadonnées du modèle ou créez de nouvelles mesures dans votre navigateur, vous enregistrez ces modèle tooyour de modifications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b6707-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="b6707-135">Si vous travaillez également sur votre modèle dans SSDT, Power BI Desktop ou Excel, il peut être désynchronisé.</span><span class="sxs-lookup"><span data-stu-id="b6707-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b6707-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6707-136">Next steps</span></span> 
[<span data-ttu-id="b6707-137">Gérer les utilisateurs et rôles de bases de données</span><span class="sxs-lookup"><span data-stu-id="b6707-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="b6707-138">Connexion avec Excel</span><span class="sxs-lookup"><span data-stu-id="b6707-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


