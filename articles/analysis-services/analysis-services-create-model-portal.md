---
title: "Créer un modèle tabulaire à l’aide du concepteur web Azure Analysis Services | Microsoft Docs"
description: "Découvrez comment créer un modèle tabulaire Azure Analysis Services à l’aide du concepteur web dans le portail Azure."
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
ms.openlocfilehash: bd58f1845dabf6afb47ce27236d14479677a8808
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="20568-103">Créer un modèle dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="20568-103">Create a model in Azure portal</span></span>

<span data-ttu-id="20568-104">La fonctionnalité de concepteur Web Azure Analysis Services (aperçu) dans le portail Azure fournit un moyen simple et rapide de créer et de modifier des modèles tabulaires et d’interroger les données des modèles directement dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="20568-104">The Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way to create and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="20568-105">N’oubliez pas que le concepteur Web est en **aperçu**.</span><span class="sxs-lookup"><span data-stu-id="20568-105">Keep in mind, the web designer is **preview**.</span></span> <span data-ttu-id="20568-106">Malgré l’ajout permanent de nouvelles fonctionnalités, les fonctionnalités disponibles en préversion sont limitées.</span><span class="sxs-lookup"><span data-stu-id="20568-106">While new functionality is being added all the time, in preview, functionality is limited.</span></span> <span data-ttu-id="20568-107">Pour un développement et un test de modèles plus avancés, utilisez plutôt Visual Studio (SSDT) et SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="20568-107">For more advanced model development and testing, it's best to use Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20568-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="20568-108">Prerequisites</span></span>

- <span data-ttu-id="20568-109">Un serveur Azure Analysis Services au niveau Standard ou Développeur.</span><span class="sxs-lookup"><span data-stu-id="20568-109">An Azure Analysis Services server at the Standard or Developer tier.</span></span> <span data-ttu-id="20568-110">Les modèles créés à l’aide du concepteur web sont en mode DirectQuery, uniquement pris en charge par ces niveaux.</span><span class="sxs-lookup"><span data-stu-id="20568-110">New models created by using the Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="20568-111">Un fichier Azure SQL Database, Azure SQL Data Warehouse ou Power BI Desktop (.pbix) comme source de données.</span><span class="sxs-lookup"><span data-stu-id="20568-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="20568-112">Les modèles créés à partir de fichiers Power BI Desktop prennent en charge les sources de données Azure SQL Database, Azure SQL Data Warehouse, Oracle et Teradata.</span><span class="sxs-lookup"><span data-stu-id="20568-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="20568-113">Un compte et un mot de passe SQL Server pour se connecter aux sources de données Azure SQL Database ou Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="20568-113">A SQL Server account and password for connecting to Azure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="to-create-a-new-tabular-model"></a><span data-ttu-id="20568-114">Pour créer un modèle tabulaire</span><span class="sxs-lookup"><span data-stu-id="20568-114">To create a new tabular model</span></span>

1. <span data-ttu-id="20568-115">Dans le panneau **Vue d’ensemble** > **Concepteur web** de votre serveur, cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="20568-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Créer un modèle dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="20568-117">Dans **Concepteur web** > **Modèles**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="20568-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Créer un modèle dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="20568-119">Dans **Nouveau modèle**, tapez un nom de modèle, puis sélectionnez une source de données.</span><span class="sxs-lookup"><span data-stu-id="20568-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Boîte de dialogue Nouveau modèle dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="20568-121">Dans **Connexion**, entrez les propriétés de connexion.</span><span class="sxs-lookup"><span data-stu-id="20568-121">In **Connect**, enter the connection properties.</span></span> <span data-ttu-id="20568-122">Le nom d’utilisateur et le mot de passe doivent correspondre à un compte SQL Server.</span><span class="sxs-lookup"><span data-stu-id="20568-122">Username and password must be a SQL Server account.</span></span>

     ![Boîte de dialogue Connexion dans le portail Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="20568-124">Dans **Tables et vues**, sélectionnez les tables à inclure dans votre modèle, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="20568-124">In **Tables and views**, select the tables to include in your model, and then click **Create**.</span></span> <span data-ttu-id="20568-125">Les relations sont créées automatiquement entre les tables avec une paire de clés.</span><span class="sxs-lookup"><span data-stu-id="20568-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Sélectionner les tables et les vues](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="20568-127">Votre nouveau modèle s’affiche dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="20568-127">Your new model appears in your browser.</span></span> <span data-ttu-id="20568-128">À ce stade, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="20568-128">From here, you can:</span></span>   

- <span data-ttu-id="20568-129">Interroger les données du modèle en faisant glisser des champs vers le concepteur de requêtes et en ajoutant des filtres.</span><span class="sxs-lookup"><span data-stu-id="20568-129">Query model data by dragging fields to the query designer and adding filters.</span></span>
- <span data-ttu-id="20568-130">Créer des mesures dans les tables.</span><span class="sxs-lookup"><span data-stu-id="20568-130">Create new measures in tables.</span></span>
- <span data-ttu-id="20568-131">Modifier les métadonnées du modèle à l’aide de l’éditeur json.</span><span class="sxs-lookup"><span data-stu-id="20568-131">Edit model metadata by using the json editor.</span></span>
- <span data-ttu-id="20568-132">Ouvrir le modèle dans Visual Studio (SSDT), Power BI Desktop ou Excel.</span><span class="sxs-lookup"><span data-stu-id="20568-132">Open the model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Sélectionner les tables et les vues](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="20568-134">Quand vous modifiez les métadonnées du modèle ou créez des mesures dans votre navigateur, vous enregistrez les modifications apportées à votre modèle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="20568-134">When you edit model metadata or create new measures in your browser, you're saving those changes to your model in Azure.</span></span> <span data-ttu-id="20568-135">Si vous travaillez également sur votre modèle dans SSDT, Power BI Desktop ou Excel, il peut être désynchronisé.</span><span class="sxs-lookup"><span data-stu-id="20568-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="20568-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="20568-136">Next steps</span></span> 
[<span data-ttu-id="20568-137">Gérer les utilisateurs et rôles de bases de données</span><span class="sxs-lookup"><span data-stu-id="20568-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="20568-138">Connexion avec Excel</span><span class="sxs-lookup"><span data-stu-id="20568-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


