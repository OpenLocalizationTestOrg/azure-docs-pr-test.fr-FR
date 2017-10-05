---
title: "Leçon 11 du didacticiel Azure Analysis Services : Créer des rôles | Microsoft Docs"
description: "Explique comment créer des rôles dans le projet du didacticiel Azure Analysis Services."
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
ms.openlocfilehash: 085a36edd2a0e80123ac8754b438bceadfa6c0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="827d9-103">Leçon 11 : Créer des rôles</span><span class="sxs-lookup"><span data-stu-id="827d9-103">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="827d9-104">Dans cette leçon, vous allez créer des rôles.</span><span class="sxs-lookup"><span data-stu-id="827d9-104">In this lesson, you create roles.</span></span> <span data-ttu-id="827d9-105">Les rôles fournissent la sécurité des données et des objets d’une base de données de modèles en limitant l’accès aux utilisateurs qui en sont membres.</span><span class="sxs-lookup"><span data-stu-id="827d9-105">Roles provide model database object and data security by limiting access to only those users that are role members.</span></span> <span data-ttu-id="827d9-106">Chaque rôle est défini avec une autorisation unique : aucune autorisation, autorisation de lecture, autorisation de lecture et de traitement, autorisation de traitement ou autorisation d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="827d9-106">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="827d9-107">Les rôles peuvent être définis lors de la création des modèles à l’aide du Gestionnaire de rôles.</span><span class="sxs-lookup"><span data-stu-id="827d9-107">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="827d9-108">Une fois un modèle déployé, vous pouvez gérer des rôles à l’aide de SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="827d9-108">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="827d9-109">Pour plus d’informations, consultez la rubrique [Rôles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="827d9-109">To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="827d9-110">Il n’est pas nécessaire de créer des rôles pour suivre ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="827d9-110">Creating roles is not necessary to complete this tutorial.</span></span> <span data-ttu-id="827d9-111">Par défaut, le compte avec lequel vous êtes actuellement connecté dispose de privilèges Administrateur sur le modèle.</span><span class="sxs-lookup"><span data-stu-id="827d9-111">By default, the account you are currently logged in with has Administrator privileges on the model.</span></span> <span data-ttu-id="827d9-112">Toutefois, pour permettre à d’autres utilisateurs de votre organisation de parcourir le modèle à l’aide d’un client de création de rapports, vous devez créer au moins un rôle avec des autorisations de lecture et ajouter ces utilisateurs comme membres.</span><span class="sxs-lookup"><span data-stu-id="827d9-112">However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="827d9-113">Vous devez créer trois rôles :</span><span class="sxs-lookup"><span data-stu-id="827d9-113">You create three roles:</span></span>  
  
-   <span data-ttu-id="827d9-114">**Sales Manager (Responsable des ventes)** – Ce rôle peut inclure les utilisateurs de votre organisation auxquels vous souhaitez donner un accès en lecture à l’ensemble des objets et données du modèle.</span><span class="sxs-lookup"><span data-stu-id="827d9-114">**Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.</span></span>  
  
-   <span data-ttu-id="827d9-115">**Sales Analyst US (Analyste en ventes aux États-Unis)** – Ce rôle peut inclure les utilisateurs de votre organisation que vous souhaitez autoriser à parcourir uniquement les données relatives aux ventes aux États-Unis.</span><span class="sxs-lookup"><span data-stu-id="827d9-115">**Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States.</span></span> <span data-ttu-id="827d9-116">Pour ce rôle, vous utilisez une formule DAX de façon à définir un *filtre de lignes*, qui limite les membres à parcourir uniquement les données concernant les États-Unis.</span><span class="sxs-lookup"><span data-stu-id="827d9-116">For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.</span></span>  
  
-   <span data-ttu-id="827d9-117">**Administrator (Administrateur)** – Ce rôle peut inclure des utilisateurs auxquels vous souhaitez fournir une autorisation d’administrateur, ce qui permet un accès et des autorisations illimités pour effectuer des tâches administratives sur la base de données de modèles.</span><span class="sxs-lookup"><span data-stu-id="827d9-117">**Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.</span></span>  
  
<span data-ttu-id="827d9-118">Étant donné que les comptes d’utilisateurs et de groupes Windows de votre organisation sont uniques, vous pouvez ajouter des comptes de votre organisation spécifique aux membres.</span><span class="sxs-lookup"><span data-stu-id="827d9-118">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members.</span></span> <span data-ttu-id="827d9-119">Toutefois, pour ce didacticiel, vous pouvez également laisser les membres vides.</span><span class="sxs-lookup"><span data-stu-id="827d9-119">However, for this tutorial, you can also leave the members blank.</span></span> <span data-ttu-id="827d9-120">Vous allez tester l’effet de chaque rôle ultérieurement dans la leçon 12 : Analyser dans Excel.</span><span class="sxs-lookup"><span data-stu-id="827d9-120">You test the effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="827d9-121">Durée estimée pour suivre cette leçon : **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="827d9-121">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="827d9-122">Prérequis</span><span class="sxs-lookup"><span data-stu-id="827d9-122">Prerequisites</span></span>  
<span data-ttu-id="827d9-123">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="827d9-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="827d9-124">Avant d’effectuer les tâches de cette leçon, vous devez avoir suivi la leçon précédente : [Leçon 10 : Créer des partitions](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="827d9-124">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="827d9-125">Créer des rôles</span><span class="sxs-lookup"><span data-stu-id="827d9-125">Create roles</span></span>  
  
#### <a name="to-create-a-sales-manager-user-role"></a><span data-ttu-id="827d9-126">Pour créer un rôle d’utilisateur Sales Manager (Responsable des ventes)</span><span class="sxs-lookup"><span data-stu-id="827d9-126">To create a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="827d9-127">Dans l’Explorateur de modèle tabulaire, cliquez avec le bouton droit sur **Rôles** > **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="827d9-127">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="827d9-128">Dans le Gestionnaire de rôles, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="827d9-128">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="827d9-129">Cliquez sur le nouveau rôle, puis dans la colonne **Nom**, renommez le rôle en **Sales Manager**.</span><span class="sxs-lookup"><span data-stu-id="827d9-129">Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="827d9-130">Dans la colonne **Autorisations**, cliquez sur la liste déroulante et sélectionnez l’autorisation **Lecture**.</span><span class="sxs-lookup"><span data-stu-id="827d9-130">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="827d9-132">Facultatif : Cliquez sur l’onglet **Membres**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="827d9-132">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="827d9-133">Dans la boîte de dialogue **Sélectionner des utilisateurs ou des groupes**, entrez les utilisateurs ou les groupes Windows de votre organisation à inclure dans le rôle.</span><span class="sxs-lookup"><span data-stu-id="827d9-133">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a><span data-ttu-id="827d9-134">Pour créer un rôle d’utilisateur Sales Analyst US (Analyste en ventes aux États-Unis)</span><span class="sxs-lookup"><span data-stu-id="827d9-134">To create a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="827d9-135">Dans le Gestionnaire de rôles, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="827d9-135">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="827d9-136">Renommez le rôle en **Sales Analyst US**.</span><span class="sxs-lookup"><span data-stu-id="827d9-136">Rename the role to **Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="827d9-137">Attribuez à ce rôle l’autorisation **Lecture**.</span><span class="sxs-lookup"><span data-stu-id="827d9-137">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="827d9-138">Cliquez sur l’onglet Filtres de lignes, puis uniquement pour la table **DimGeography**, dans la colonne Filtre DAX, tapez la formule suivante :</span><span class="sxs-lookup"><span data-stu-id="827d9-138">Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="827d9-139">Une formule de filtre de lignes doit être résolue en une valeur booléenne (TRUE/FALSE).</span><span class="sxs-lookup"><span data-stu-id="827d9-139">A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="827d9-140">Avec cette formule, vous spécifiez que l’utilisateur doit voir uniquement les lignes dont la valeur Code pays/région est « US ».</span><span class="sxs-lookup"><span data-stu-id="827d9-140">With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="827d9-142">Facultatif : Cliquez sur l’onglet **Membres**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="827d9-142">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="827d9-143">Dans la boîte de dialogue **Sélectionner des utilisateurs ou des groupes**, entrez les utilisateurs ou les groupes Windows de votre organisation à inclure dans le rôle.</span><span class="sxs-lookup"><span data-stu-id="827d9-143">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-an-administrator-user-role"></a><span data-ttu-id="827d9-144">Pour créer un rôle d’utilisateur Administrator</span><span class="sxs-lookup"><span data-stu-id="827d9-144">To create an Administrator user role</span></span>  
  
1.  <span data-ttu-id="827d9-145">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="827d9-145">Click **New**.</span></span>  
  
2.  <span data-ttu-id="827d9-146">Renommez le rôle en **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="827d9-146">Rename the role to **Administrator**.</span></span>  
  
3.  <span data-ttu-id="827d9-147">Attribuez à ce rôle l’autorisation **Administrateur**.</span><span class="sxs-lookup"><span data-stu-id="827d9-147">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="827d9-148">Facultatif : Cliquez sur l’onglet **Membres**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="827d9-148">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="827d9-149">Dans la boîte de dialogue **Sélectionner des utilisateurs ou des groupes**, entrez les utilisateurs ou les groupes Windows de votre organisation à inclure dans le rôle.</span><span class="sxs-lookup"><span data-stu-id="827d9-149">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="827d9-150">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="827d9-150">What's next?</span></span>
<span data-ttu-id="827d9-151">[Leçon 12 : Analyser dans Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="827d9-151">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
