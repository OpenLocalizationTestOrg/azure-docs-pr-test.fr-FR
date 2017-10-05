---
title: "Leçon 12 du didacticiel Azure Analysis Services : Analyser dans Excel | Microsoft Docs"
description: "Explique comment utiliser la fonctionnalité Analyser dans Excel dans le projet du didacticiel Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 6f47de43ff8d94de22f8b7c12fa0707a8d7ffbbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-12-analyze-in-excel"></a><span data-ttu-id="69eb9-103">Leçon 12 : Analyser dans Excel</span><span class="sxs-lookup"><span data-stu-id="69eb9-103">Lesson 12: Analyze in Excel</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="69eb9-104">Dans cette leçon, vous utilisez la fonctionnalité Analyser dans Excel pour ouvrir Microsoft Excel, créer automatiquement une connexion à l’espace de travail du modèle et ajouter automatiquement un tableau croisé dynamique à la feuille de calcul.</span><span class="sxs-lookup"><span data-stu-id="69eb9-104">In this lesson, you use the Analyze in Excel feature to open Microsoft Excel, automatically create a connection to the model workspace, and automatically add a PivotTable to the worksheet.</span></span> <span data-ttu-id="69eb9-105">La fonctionnalité Analyser dans Excel est destinée à fournir un moyen simple et rapide de tester l’efficacité de la conception de votre modèle avant de déployer ce dernier.</span><span class="sxs-lookup"><span data-stu-id="69eb9-105">The Analyze in Excel feature is meant to provide a quick and easy way to test the efficacy of your model design prior to deploying your model.</span></span> <span data-ttu-id="69eb9-106">Vous n’exécutez aucune analyse de données dans cette leçon.</span><span class="sxs-lookup"><span data-stu-id="69eb9-106">You do not perform any data analysis in this lesson.</span></span> <span data-ttu-id="69eb9-107">L’objectif de cette leçon est de vous familiariser, en tant qu’auteur de modèle, avec les outils que vous pouvez utiliser pour tester la conception de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="69eb9-107">The purpose of this lesson is to familiarize you, the model author, with the tools you can use to test your model design.</span></span>   
  
<span data-ttu-id="69eb9-108">Pour que vous puissiez suivre cette leçon, Excel doit être installé sur le même ordinateur que SSDT.</span><span class="sxs-lookup"><span data-stu-id="69eb9-108">To complete this lesson, Excel must be installed on the same computer as SSDT.</span></span>
  
<span data-ttu-id="69eb9-109">Durée estimée pour suivre cette leçon : **5 minutes**</span><span class="sxs-lookup"><span data-stu-id="69eb9-109">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="69eb9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="69eb9-110">Prerequisites</span></span>  
<span data-ttu-id="69eb9-111">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="69eb9-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="69eb9-112">Avant d’effectuer les tâches de cette leçon, vous devez avoir suivi la leçon précédente : [Leçon 11 : Créer des rôles](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="69eb9-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span></span>  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a><span data-ttu-id="69eb9-113">Parcourir des données à l’aide des perspectives par défaut et Internet Sales</span><span class="sxs-lookup"><span data-stu-id="69eb9-113">Browse using the Default and Internet Sales perspectives</span></span>  
<span data-ttu-id="69eb9-114">Dans ces premières tâches, vous aller parcourir votre modèle en utilisant à la fois la perspective par défaut, qui inclut tous les objets du modèle, et la perspective Internet Sales créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="69eb9-114">In these first tasks, you browse your model by using both the default perspective, which includes all model objects, and also by using the Internet Sales perspective you earlier.</span></span> <span data-ttu-id="69eb9-115">La perspective Internet Sales exclut l’objet table Customer.</span><span class="sxs-lookup"><span data-stu-id="69eb9-115">The Internet Sales perspective excludes the Customer table object.</span></span>  
  
#### <a name="to-browse-by-using-the-default-perspective"></a><span data-ttu-id="69eb9-116">Pour parcourir des données à l’aide de la perspective par défaut</span><span class="sxs-lookup"><span data-stu-id="69eb9-116">To browse by using the Default perspective</span></span>  
  
1.  <span data-ttu-id="69eb9-117">Cliquez sur le menu **Modèle** > **Analyser dans Excel**.</span><span class="sxs-lookup"><span data-stu-id="69eb9-117">Click the **Model** menu > **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="69eb9-118">Dans la boîte de dialogue **Analyser dans Excel**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="69eb9-118">In the **Analyze in Excel** dialog box, click **OK**.</span></span>  
  
    <span data-ttu-id="69eb9-119">Excel s’ouvre avec un nouveau classeur.</span><span class="sxs-lookup"><span data-stu-id="69eb9-119">Excel opens with a new workbook.</span></span> <span data-ttu-id="69eb9-120">Une connexion de source de données est créée à l’aide du compte d’utilisateur actuel et la perspective par défaut est utilisée pour définir les champs visibles.</span><span class="sxs-lookup"><span data-stu-id="69eb9-120">A data source connection is created using the current user account and the Default perspective is used to define viewable fields.</span></span> <span data-ttu-id="69eb9-121">Un tableau croisé dynamique est automatiquement ajouté à la feuille de calcul.</span><span class="sxs-lookup"><span data-stu-id="69eb9-121">A PivotTable is automatically added to the worksheet.</span></span>  
  
3.  <span data-ttu-id="69eb9-122">Dans Excel, dans la **liste des champs de tableau croisé dynamique**, les groupes de mesures **DimDate** et **FactInternetSales** sont affichés.</span><span class="sxs-lookup"><span data-stu-id="69eb9-122">In Excel, in the **PivotTable Field List**, notice the **DimDate** and **FactInternetSales** measure groups appear.</span></span> <span data-ttu-id="69eb9-123">Vous voyez également les tables **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** et **FactInternetSales**, avec leurs colonnes respectives.</span><span class="sxs-lookup"><span data-stu-id="69eb9-123">The **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span></span>  
  
4.  <span data-ttu-id="69eb9-124">Fermez Excel sans enregistrer le classeur.</span><span class="sxs-lookup"><span data-stu-id="69eb9-124">Close Excel without saving the workbook.</span></span>  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a><span data-ttu-id="69eb9-125">Pour parcourir les données à l’aide de perspective Internet Sales</span><span class="sxs-lookup"><span data-stu-id="69eb9-125">To browse by using the Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="69eb9-126">Cliquez sur le menu **Modèle**, puis sur **Analyser dans Excel**.</span><span class="sxs-lookup"><span data-stu-id="69eb9-126">Click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="69eb9-127">Dans la boîte de dialogue **Analyser dans Excel**, laissez **Utilisateur Windows actuel** sélectionné, puis dans la zone de liste déroulante **Perspective**, sélectionnez **Internet Sales**. Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="69eb9-127">In the **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in the **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span></span> 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  <span data-ttu-id="69eb9-129">Dans Excel, dans **Champs de tableau croisé dynamique**, notez que la table DimCustomer est exclue de la liste des champs.</span><span class="sxs-lookup"><span data-stu-id="69eb9-129">In Excel, in **PivotTable Fields**, notice the DimCustomer table is excluded from the field list.</span></span>  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  <span data-ttu-id="69eb9-131">Fermez Excel sans enregistrer le classeur.</span><span class="sxs-lookup"><span data-stu-id="69eb9-131">Close Excel without saving the workbook.</span></span>  
  
## <a name="browse-by-using-roles"></a><span data-ttu-id="69eb9-132">Parcourir les données à l’aide de rôles</span><span class="sxs-lookup"><span data-stu-id="69eb9-132">Browse by using roles</span></span>  
<span data-ttu-id="69eb9-133">Les rôles sont importants dans n’importe quel modèle tabulaire.</span><span class="sxs-lookup"><span data-stu-id="69eb9-133">Roles are an important part of any tabular model.</span></span> <span data-ttu-id="69eb9-134">Si les utilisateurs ne disposent pas d’au moins un rôle auquel ils sont ajoutés en tant que membres, ils ne peuvent pas accéder aux données ni les analyser à l’aide de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="69eb9-134">Without at least one role to which users are added as members, users cannot access and analyze data using your model.</span></span> <span data-ttu-id="69eb9-135">La fonctionnalité Analyser dans Excel fournit un moyen de tester les rôles que vous avez définis.</span><span class="sxs-lookup"><span data-stu-id="69eb9-135">The Analyze in Excel feature provides a way for you to test the roles you have defined.</span></span>  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a><span data-ttu-id="69eb9-136">Pour parcourir les données à l’aide du rôle utilisateur Sales Manager</span><span class="sxs-lookup"><span data-stu-id="69eb9-136">To browse by using the Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="69eb9-137">Dans SSDT, cliquez sur le menu **Modèle**, puis sur **Analyser dans Excel**.</span><span class="sxs-lookup"><span data-stu-id="69eb9-137">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="69eb9-138">Dans **Spécifier le nom d’utilisateur ou le rôle à utiliser pour se connecter au modèle**, sélectionnez **Rôle**, puis dans la zone de liste déroulante, sélectionnez **Sales Manager**. Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="69eb9-138">In **Specify the user name or role to use to connect to the model**, select **Role**, and then in the drop-down listbox, select **Sales Manager**, and then click **OK**.</span></span>  
  
    <span data-ttu-id="69eb9-139">Excel s’ouvre avec un nouveau classeur.</span><span class="sxs-lookup"><span data-stu-id="69eb9-139">Excel opens with a new workbook.</span></span> <span data-ttu-id="69eb9-140">Un tableau croisé dynamique est automatiquement créé.</span><span class="sxs-lookup"><span data-stu-id="69eb9-140">A PivotTable is automatically created.</span></span> <span data-ttu-id="69eb9-141">La liste des champs du tableau croisé dynamique inclut tous les champs de données disponibles dans votre nouveau modèle.</span><span class="sxs-lookup"><span data-stu-id="69eb9-141">The Pivot Table Field List includes all the data fields available in your new model.</span></span>  
      
3.  <span data-ttu-id="69eb9-142">Fermez Excel sans enregistrer le classeur.</span><span class="sxs-lookup"><span data-stu-id="69eb9-142">Close Excel without saving the workbook.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="69eb9-143">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="69eb9-143">What's next?</span></span>
<span data-ttu-id="69eb9-144">Accédez à la leçon suivante : [Leçon 13 : Déployer](../tutorials/aas-lesson-13-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="69eb9-144">Go to the next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span></span>

  
  
  
