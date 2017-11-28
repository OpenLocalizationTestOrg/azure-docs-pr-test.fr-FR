---
title: "aaaManage de la base de données des rôles et les utilisateurs dans Azure Analysis Services | Documents Microsoft"
description: "Découvrez comment toomanage base de données les rôles et les utilisateurs sur un serveur Analysis Services dans Azure."
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="a8733-103">Gérer les rôles et les utilisateurs de base de données</span><span class="sxs-lookup"><span data-stu-id="a8733-103">Manage database roles and users</span></span>

<span data-ttu-id="a8733-104">Au niveau de base de données de modèle hello, tous les utilisateurs doivent appartenir tooa rôle.</span><span class="sxs-lookup"><span data-stu-id="a8733-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="a8733-105">Les rôles définissent les utilisateurs disposant d’autorisations spécifiques pour la base de données model hello.</span><span class="sxs-lookup"><span data-stu-id="a8733-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="a8733-106">N’importe quel utilisateur ou groupe de sécurité ajouté tooa rôle doit avoir un compte dans un locataire Azure AD Bonjour même abonnement que hello serveur.</span><span class="sxs-lookup"><span data-stu-id="a8733-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="a8733-107">Comment définir des rôles est différent selon outil hello que vous utilisez, mais effet de hello est hello identiques.</span><span class="sxs-lookup"><span data-stu-id="a8733-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="a8733-108">Les autorisations des rôles incluent :</span><span class="sxs-lookup"><span data-stu-id="a8733-108">Role permissions include:</span></span>
*  <span data-ttu-id="a8733-109">**Administrateur** -les utilisateurs disposent des autorisations complètes pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="a8733-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="a8733-110">Les rôles de base de données avec des autorisations d’administrateur sont différents des administrateurs de serveur.</span><span class="sxs-lookup"><span data-stu-id="a8733-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="a8733-111">**Processus** -les utilisateurs peuvent se connecter tooand effectuer des opérations de traitement sur la base de données hello et analyser les données de base de données de modèle.</span><span class="sxs-lookup"><span data-stu-id="a8733-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="a8733-112">**Lecture** -les utilisateurs peuvent utiliser un client application tooconnect tooand analyser les données de base de données de modèle.</span><span class="sxs-lookup"><span data-stu-id="a8733-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="a8733-113">Lorsque vous créez un projet de modèle tabulaire, vous créez des rôles et ajoutez des rôles de toothose des utilisateurs ou des groupes à l’aide du Gestionnaire de rôles dans SSDT.</span><span class="sxs-lookup"><span data-stu-id="a8733-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="a8733-114">Lorsque tooa déployé server, vous utilisez SSMS, [applets de commande PowerShell Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx), ou [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd ou supprimer des rôles et des membres de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a8733-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="a8733-115">tooadd ou gérer des rôles et des utilisateurs dans SSDT</span><span class="sxs-lookup"><span data-stu-id="a8733-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="a8733-116">Dans SSDT > **Tabular Model Explorer**, cliquez avec le bouton droit sur **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="a8733-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="a8733-117">Dans le **Gestionnaire de rôles**, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="a8733-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="a8733-118">Tapez un nom pour le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="a8733-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="a8733-119">Par défaut, nom hello de rôle par défaut de hello est numéroté de façon incrémentielle pour chaque nouveau rôle.</span><span class="sxs-lookup"><span data-stu-id="a8733-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="a8733-120">Il est recommandé de que taper un nom qui identifie clairement le type de membre hello, par exemple, directeurs financiers ou responsables des ressources humaines.</span><span class="sxs-lookup"><span data-stu-id="a8733-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="a8733-121">Sélectionnez une des hello les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a8733-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="a8733-122">Autorisation</span><span class="sxs-lookup"><span data-stu-id="a8733-122">Permission</span></span>|<span data-ttu-id="a8733-123">Description</span><span class="sxs-lookup"><span data-stu-id="a8733-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="a8733-124">**Aucun**</span><span class="sxs-lookup"><span data-stu-id="a8733-124">**None**</span></span>|<span data-ttu-id="a8733-125">Les membres ne peuvent pas de modifier le schéma de modèle hello et ne peut pas interroger les données.</span><span class="sxs-lookup"><span data-stu-id="a8733-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="a8733-126">**Lire**</span><span class="sxs-lookup"><span data-stu-id="a8733-126">**Read**</span></span>|<span data-ttu-id="a8733-127">Les membres peuvent interroger des données (selon les filtres de lignes), mais Impossible de modifier le schéma de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="a8733-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="a8733-128">**Lecture et traitement**</span><span class="sxs-lookup"><span data-stu-id="a8733-128">**Read and Process**</span></span>|<span data-ttu-id="a8733-129">Les membres peuvent interroger des données (selon les filtres au niveau des lignes) et l’exécution des opérations traiter et traiter tout, mais Impossible de modifier le schéma de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="a8733-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="a8733-130">**Processus**</span><span class="sxs-lookup"><span data-stu-id="a8733-130">**Process**</span></span>|<span data-ttu-id="a8733-131">Les membres peuvent exécuter des processus et traiter toutes les opérations.</span><span class="sxs-lookup"><span data-stu-id="a8733-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="a8733-132">Impossible de modifier le schéma de modèle hello et ne peut pas interroger les données.</span><span class="sxs-lookup"><span data-stu-id="a8733-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="a8733-133">**Administrateur**</span><span class="sxs-lookup"><span data-stu-id="a8733-133">**Administrator**</span></span>|<span data-ttu-id="a8733-134">Les membres peuvent modifier le schéma de modèle hello et interroger toutes les données.</span><span class="sxs-lookup"><span data-stu-id="a8733-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="a8733-135">Dans le cas des rôles de hello création a lu ou autorisation en lecture et de processus, vous pouvez ajouter des filtres de lignes à l’aide d’une formule DAX.</span><span class="sxs-lookup"><span data-stu-id="a8733-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="a8733-136">Cliquez sur hello **les filtres de lignes** onglet, sélectionnez une table, puis cliquez sur hello **filtre DAX** champ, puis tapez une formule DAX.</span><span class="sxs-lookup"><span data-stu-id="a8733-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="a8733-137">Cliquez sur **Membres** > **Ajouter externe**.</span><span class="sxs-lookup"><span data-stu-id="a8733-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="a8733-138">Dans **Ajouter un membre externe**, entrez les utilisateurs ou groupes dans votre Azure AD client par adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="a8733-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="a8733-139">Une fois que vous avez cliqué sur OK et fermé le Gestionnaire de rôles, les rôles et les membres du rôle s’affichent dans l’Explorateur de modèles tabulaires.</span><span class="sxs-lookup"><span data-stu-id="a8733-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Rôles et les utilisateurs dans l’Explorateur de modèles tabulaires](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="a8733-141">Déployer tooyour Azure Analysis Services serveur.</span><span class="sxs-lookup"><span data-stu-id="a8733-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="a8733-142">tooadd ou gérer des rôles et des utilisateurs dans SSMS</span><span class="sxs-lookup"><span data-stu-id="a8733-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="a8733-143">tooa de rôles et les utilisateurs tooadd déployé la base de données model, vous devez être connecté toohello serveur en tant qu’un administrateur de serveur ou est déjà dans un rôle de base de données avec des autorisations d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a8733-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="a8733-144">Dans Object Exporer, cliquez avec le bouton droit sur **Rôles** > **Nouveau rôle**.</span><span class="sxs-lookup"><span data-stu-id="a8733-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="a8733-145">Dans **Créer un rôle**, entrez un nom de rôle et une description.</span><span class="sxs-lookup"><span data-stu-id="a8733-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="a8733-146">Sélectionnez une autorisation.</span><span class="sxs-lookup"><span data-stu-id="a8733-146">Select a permission.</span></span>
   |<span data-ttu-id="a8733-147">Autorisation</span><span class="sxs-lookup"><span data-stu-id="a8733-147">Permission</span></span>|<span data-ttu-id="a8733-148">Description</span><span class="sxs-lookup"><span data-stu-id="a8733-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="a8733-149">**Contrôle total (administrateur)**</span><span class="sxs-lookup"><span data-stu-id="a8733-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="a8733-150">Les membres peuvent modifier le schéma de modèle hello, traiter et interroger toutes les données.</span><span class="sxs-lookup"><span data-stu-id="a8733-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="a8733-151">**Base de données de processus**</span><span class="sxs-lookup"><span data-stu-id="a8733-151">**Process database**</span></span>|<span data-ttu-id="a8733-152">Les membres peuvent exécuter des processus et traiter toutes les opérations.</span><span class="sxs-lookup"><span data-stu-id="a8733-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="a8733-153">Impossible de modifier le schéma de modèle hello et ne peut pas interroger les données.</span><span class="sxs-lookup"><span data-stu-id="a8733-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="a8733-154">**Lire**</span><span class="sxs-lookup"><span data-stu-id="a8733-154">**Read**</span></span>|<span data-ttu-id="a8733-155">Les membres peuvent interroger des données (selon les filtres de lignes), mais Impossible de modifier le schéma de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="a8733-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="a8733-156">Cliquez sur **Appartenance**, puis entrez un utilisateur ou un groupe dans votre client Azure AD par adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="a8733-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Ajouter un utilisateur](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="a8733-158">Si le rôle que vous créez hello possède une autorisation de lecture, vous pouvez ajouter des filtres de lignes à l’aide d’une formule DAX.</span><span class="sxs-lookup"><span data-stu-id="a8733-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="a8733-159">Cliquez sur **les filtres de lignes**, sélectionnez une table, puis tapez une formule DAX dans hello **filtre DAX** champ.</span><span class="sxs-lookup"><span data-stu-id="a8733-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="a8733-160">tooadd rôles et les utilisateurs à l’aide d’un script TMSL</span><span class="sxs-lookup"><span data-stu-id="a8733-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="a8733-161">Vous pouvez exécuter un script TMSL dans la fenêtre XMLA hello dans SSMS, ou à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8733-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="a8733-162">Hello d’utilisation [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) commande et hello [rôles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) objet.</span><span class="sxs-lookup"><span data-stu-id="a8733-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="a8733-163">**Exemple de script TMSL**</span><span class="sxs-lookup"><span data-stu-id="a8733-163">**Sample TMSL script**</span></span>

<span data-ttu-id="a8733-164">Dans cet exemple, un utilisateur externe B2B et un groupe sont ajoutés rôle d’analyste toohello avec les autorisations de lecture pour la base de données SalesBI hello.</span><span class="sxs-lookup"><span data-stu-id="a8733-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="a8733-165">Les deux hello utilisateur externe et de groupe doit être dans le même client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8733-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="a8733-166">tooadd rôles et les utilisateurs à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8733-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="a8733-167">Hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module fournit spécifiques à une tâche de base de données Gestion des applets de commande et hello à usage général Invoke-ASCmd applet de commande qui accepte une requête d’écriture de scripts langage TMSL (Tabular Model) ou un script.</span><span class="sxs-lookup"><span data-stu-id="a8733-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="a8733-168">Hello suivant d’applets de commande est utilisé pour la gestion des utilisateurs et des rôles de base de données.</span><span class="sxs-lookup"><span data-stu-id="a8733-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="a8733-169">Applet de commande</span><span class="sxs-lookup"><span data-stu-id="a8733-169">Cmdlet</span></span>|<span data-ttu-id="a8733-170">Description</span><span class="sxs-lookup"><span data-stu-id="a8733-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="a8733-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="a8733-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="a8733-172">Ajouter un rôle de base de données de membre tooa.</span><span class="sxs-lookup"><span data-stu-id="a8733-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="a8733-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="a8733-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="a8733-174">Supprime un membre d’un rôle de base de données.</span><span class="sxs-lookup"><span data-stu-id="a8733-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="a8733-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="a8733-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="a8733-176">Exécute un script TMSL.</span><span class="sxs-lookup"><span data-stu-id="a8733-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="a8733-177">Filtres de lignes</span><span class="sxs-lookup"><span data-stu-id="a8733-177">Row filters</span></span>  
<span data-ttu-id="a8733-178">Les filtres de lignes définissent les lignes d’une table qui peuvent être interrogées par les membres d’un rôle donné.</span><span class="sxs-lookup"><span data-stu-id="a8733-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="a8733-179">Les filtres de lignes sont définis pour chaque table dans un modèle à l’aide de formules DAX.</span><span class="sxs-lookup"><span data-stu-id="a8733-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="a8733-180">Les filtres de lignes peuvent être définis uniquement pour les rôles avec des autorisations de Lecture et de Lecture et processus.</span><span class="sxs-lookup"><span data-stu-id="a8733-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="a8733-181">Par défaut, si un filtre de lignes n’est pas défini pour une table particulière, les membres peuvent interroger toutes les lignes de la table de hello, sauf si le filtrage croisé s’applique à partir d’une autre table.</span><span class="sxs-lookup"><span data-stu-id="a8733-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="a8733-182">Les filtres de lignes nécessitent une formule DAX, qui doit prendre la valeur TRUE/FALSE, les lignes de hello toodefine qui peuvent être interrogées par les membres de ce rôle particulier de tooa.</span><span class="sxs-lookup"><span data-stu-id="a8733-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="a8733-183">Les lignes non incluses dans hello formule DAX ne peut pas être interrogés.</span><span class="sxs-lookup"><span data-stu-id="a8733-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="a8733-184">Par exemple, hello table Customers avec hello suivant l’expression de filtres de lignes, *= clients [pays] = « France »*, les membres du rôle Sales de hello peuvent visualiser uniquement les clients Bonjour USA.</span><span class="sxs-lookup"><span data-stu-id="a8733-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="a8733-185">Les filtres de lignes s’appliquent toohello spécifié lignes et les lignes associées.</span><span class="sxs-lookup"><span data-stu-id="a8733-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="a8733-186">Lorsqu’une table possède plusieurs relations, filtres appliquent la sécurité pour la relation de hello est active.</span><span class="sxs-lookup"><span data-stu-id="a8733-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="a8733-187">Les filtres de lignes sont croisés avec d’autres filtres de lignes définis pour les tables associées, par exemple :</span><span class="sxs-lookup"><span data-stu-id="a8733-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="a8733-188">Table</span><span class="sxs-lookup"><span data-stu-id="a8733-188">Table</span></span>|<span data-ttu-id="a8733-189">Expression DAX</span><span class="sxs-lookup"><span data-stu-id="a8733-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="a8733-190">Région</span><span class="sxs-lookup"><span data-stu-id="a8733-190">Region</span></span>|<span data-ttu-id="a8733-191">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="a8733-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="a8733-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="a8733-192">ProductCategory</span></span>|<span data-ttu-id="a8733-193">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="a8733-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="a8733-194">Transactions</span><span class="sxs-lookup"><span data-stu-id="a8733-194">Transactions</span></span>|<span data-ttu-id="a8733-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="a8733-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="a8733-196">effet net de Hello est membres peuvent interroger les lignes de données où client de hello réside aux États-Unis de hello, catégorie de produit hello correspond à des bicyclettes et l’année hello est 2016.</span><span class="sxs-lookup"><span data-stu-id="a8733-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="a8733-197">Les utilisateurs ne peuvent pas interroger les transactions en dehors des États-Unis de hello, qui ne sont pas bicyclettes ou transactions pas de 2016, sauf si elles sont membres d’un autre rôle qui accorde ces autorisations.</span><span class="sxs-lookup"><span data-stu-id="a8733-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="a8733-198">Vous pouvez utiliser le filtre de hello, *= False()*, les lignes tooall toodeny accès pour une table entière.</span><span class="sxs-lookup"><span data-stu-id="a8733-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8733-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a8733-199">Next steps</span></span>
  <span data-ttu-id="a8733-200">[Gérer les administrateurs de serveur](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="a8733-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="a8733-201">Gérer Azure Analysis Services avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8733-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="a8733-202">Langage TMSL (Tabular Model Scripting Language)</span><span class="sxs-lookup"><span data-stu-id="a8733-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

