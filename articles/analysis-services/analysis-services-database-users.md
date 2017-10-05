---
title: "Gérer les rôles et les utilisateurs dans Azure Analysis Services | Microsoft Docs"
description: "Découvrez comment gérer les rôles et les utilisateurs sur un serveur Analysis Services dans Azure."
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
ms.openlocfilehash: d0bc7d7514f111b4bbde33bd60ae21264bd797fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="f036c-103">Gérer les rôles et les utilisateurs de base de données</span><span class="sxs-lookup"><span data-stu-id="f036c-103">Manage database roles and users</span></span>

<span data-ttu-id="f036c-104">Au niveau de la base de données du modèle, tous les utilisateurs doivent appartenir à un rôle.</span><span class="sxs-lookup"><span data-stu-id="f036c-104">At the model database level, all users must belong to a role.</span></span> <span data-ttu-id="f036c-105">Les rôles définissent les utilisateurs disposant d’autorisations spécifiques pour la base de données du modèle.</span><span class="sxs-lookup"><span data-stu-id="f036c-105">Roles define users with particular permissions for the model database.</span></span> <span data-ttu-id="f036c-106">Tout utilisateur ou groupe de sécurité ajouté à un rôle doit avoir un compte dans un client Azure AD dans le même abonnement que le serveur.</span><span class="sxs-lookup"><span data-stu-id="f036c-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span></span>

<span data-ttu-id="f036c-107">Le mode de définition des rôles est différent selon l’outil utilisé, mais l’effet est le même.</span><span class="sxs-lookup"><span data-stu-id="f036c-107">How you define roles is different depending on the tool you use, but the effect is the same.</span></span>

<span data-ttu-id="f036c-108">Les autorisations des rôles incluent :</span><span class="sxs-lookup"><span data-stu-id="f036c-108">Role permissions include:</span></span>
*  <span data-ttu-id="f036c-109">**Administrateur** : les utilisateurs disposent des autorisations complètes pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="f036c-109">**Administrator** - Users have full permissions for the database.</span></span> <span data-ttu-id="f036c-110">Les rôles de base de données avec des autorisations d’administrateur sont différents des administrateurs de serveur.</span><span class="sxs-lookup"><span data-stu-id="f036c-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="f036c-111">**Processus** : les utilisateurs peuvent se connecter et effectuer des opérations de traitement sur la base de données et analyser les données des bases de données du modèle.</span><span class="sxs-lookup"><span data-stu-id="f036c-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span></span>
*  <span data-ttu-id="f036c-112">**Lecture** : les utilisateurs peuvent utiliser une application cliente pour se connecter et analyser les données des bases de données du modèle.</span><span class="sxs-lookup"><span data-stu-id="f036c-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span></span>

<span data-ttu-id="f036c-113">Lorsque vous créez un projet de modèle tabulaire, vous créez des rôles et ajoutez des utilisateurs ou des groupes à ces rôles à l’aide du Gestionnaire de rôles dans SSDT.</span><span class="sxs-lookup"><span data-stu-id="f036c-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="f036c-114">Lors du déploiement sur un serveur, vous utilisez SSMS, [applets de commande PowerShell Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx) ou [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) pour ajouter ou supprimer des rôles et des membres utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f036c-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span></span>

## <a name="to-add-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="f036c-115">Pour ajouter ou gérer des rôles et des utilisateurs dans SSDT</span><span class="sxs-lookup"><span data-stu-id="f036c-115">To add or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="f036c-116">Dans SSDT > **Tabular Model Explorer**, cliquez avec le bouton droit sur **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="f036c-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="f036c-117">Dans le **Gestionnaire de rôles**, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="f036c-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="f036c-118">Entrez ensuite le nom du rôle.</span><span class="sxs-lookup"><span data-stu-id="f036c-118">Type a name for the role.</span></span>  
  
     <span data-ttu-id="f036c-119">Par défaut, le nom de rôle par défaut est numéroté de façon incrémentielle pour chaque nouveau rôle.</span><span class="sxs-lookup"><span data-stu-id="f036c-119">By default, the name of the default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="f036c-120">Il est recommandé de saisir un nom qui identifie clairement le type de membre, par exemple, directeurs financiers ou spécialistes des ressources humaines.</span><span class="sxs-lookup"><span data-stu-id="f036c-120">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="f036c-121">Sélectionnez l’une des autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f036c-121">Select one of the following permissions:</span></span>  
  
    |<span data-ttu-id="f036c-122">Autorisation</span><span class="sxs-lookup"><span data-stu-id="f036c-122">Permission</span></span>|<span data-ttu-id="f036c-123">Description</span><span class="sxs-lookup"><span data-stu-id="f036c-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="f036c-124">**Aucun**</span><span class="sxs-lookup"><span data-stu-id="f036c-124">**None**</span></span>|<span data-ttu-id="f036c-125">Les membres ne peuvent pas modifier le schéma de modèle et ne peuvent pas interroger les données.</span><span class="sxs-lookup"><span data-stu-id="f036c-125">Members cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="f036c-126">**Lire**</span><span class="sxs-lookup"><span data-stu-id="f036c-126">**Read**</span></span>|<span data-ttu-id="f036c-127">Les membres peuvent interroger des données (selon les filtres de lignes) mais ne peuvent pas modifier le schéma de modèle.</span><span class="sxs-lookup"><span data-stu-id="f036c-127">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="f036c-128">**Lecture et traitement**</span><span class="sxs-lookup"><span data-stu-id="f036c-128">**Read and Process**</span></span>|<span data-ttu-id="f036c-129">Les membres peuvent interroger des données (selon les filtres au niveau des lignes) et exécuter des processus et traiter toutes les opérations, mais ne peuvent pas modifier le schéma de modèle.</span><span class="sxs-lookup"><span data-stu-id="f036c-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="f036c-130">**Processus**</span><span class="sxs-lookup"><span data-stu-id="f036c-130">**Process**</span></span>|<span data-ttu-id="f036c-131">Les membres peuvent exécuter des processus et traiter toutes les opérations.</span><span class="sxs-lookup"><span data-stu-id="f036c-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="f036c-132">Ils ne peuvent pas modifier le schéma de modèle et ne peuvent pas interroger les données.</span><span class="sxs-lookup"><span data-stu-id="f036c-132">Cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="f036c-133">**Administrateur**</span><span class="sxs-lookup"><span data-stu-id="f036c-133">**Administrator**</span></span>|<span data-ttu-id="f036c-134">Les membres peuvent modifier le schéma de modèle et interroger toutes les données.</span><span class="sxs-lookup"><span data-stu-id="f036c-134">Members can modify the model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="f036c-135">Si le rôle que vous créez a l’autorisation de Lecture ou de Lecture et processus, vous pouvez ajouter des filtres de lignes à l’aide d’une formule DAX.</span><span class="sxs-lookup"><span data-stu-id="f036c-135">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="f036c-136">Cliquez sur l’onglet **Filtres de lignes**, sélectionnez une table, puis cliquez sur le champ **Filtre DAX**, puis tapez une formule DAX.</span><span class="sxs-lookup"><span data-stu-id="f036c-136">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="f036c-137">Cliquez sur **Membres** > **Ajouter externe**.</span><span class="sxs-lookup"><span data-stu-id="f036c-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="f036c-138">Dans **Ajouter un membre externe**, entrez les utilisateurs ou groupes dans votre Azure AD client par adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="f036c-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="f036c-139">Une fois que vous avez cliqué sur OK et fermé le Gestionnaire de rôles, les rôles et les membres du rôle s’affichent dans l’Explorateur de modèles tabulaires.</span><span class="sxs-lookup"><span data-stu-id="f036c-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Rôles et les utilisateurs dans l’Explorateur de modèles tabulaires](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="f036c-141">Déployez votre serveur Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="f036c-141">Deploy to your Azure Analysis Services server.</span></span>


## <a name="to-add-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="f036c-142">Pour ajouter ou gérer des rôles et des utilisateurs dans SSMS</span><span class="sxs-lookup"><span data-stu-id="f036c-142">To add or manage roles and users in SSMS</span></span>
<span data-ttu-id="f036c-143">Pour ajouter des rôles et des utilisateurs à une base de données du modèle déployée, vous devez être connecté au serveur en tant qu’administrateur de serveur ou déjà dans un rôle de base de données avec des autorisations d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f036c-143">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="f036c-144">Dans Object Exporer, cliquez avec le bouton droit sur **Rôles** > **Nouveau rôle**.</span><span class="sxs-lookup"><span data-stu-id="f036c-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="f036c-145">Dans **Créer un rôle**, entrez un nom de rôle et une description.</span><span class="sxs-lookup"><span data-stu-id="f036c-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="f036c-146">Sélectionnez une autorisation.</span><span class="sxs-lookup"><span data-stu-id="f036c-146">Select a permission.</span></span>
   |<span data-ttu-id="f036c-147">Autorisation</span><span class="sxs-lookup"><span data-stu-id="f036c-147">Permission</span></span>|<span data-ttu-id="f036c-148">Description</span><span class="sxs-lookup"><span data-stu-id="f036c-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="f036c-149">**Contrôle total (administrateur)**</span><span class="sxs-lookup"><span data-stu-id="f036c-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="f036c-150">Les membres peuvent modifier le schéma de modèle, le processus et interroger toutes les données.</span><span class="sxs-lookup"><span data-stu-id="f036c-150">Members can modify the model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="f036c-151">**Base de données de processus**</span><span class="sxs-lookup"><span data-stu-id="f036c-151">**Process database**</span></span>|<span data-ttu-id="f036c-152">Les membres peuvent exécuter des processus et traiter toutes les opérations.</span><span class="sxs-lookup"><span data-stu-id="f036c-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="f036c-153">Ils ne peuvent pas modifier le schéma de modèle et ne peuvent pas interroger les données.</span><span class="sxs-lookup"><span data-stu-id="f036c-153">Cannot modify the model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="f036c-154">**Lire**</span><span class="sxs-lookup"><span data-stu-id="f036c-154">**Read**</span></span>|<span data-ttu-id="f036c-155">Les membres peuvent interroger des données (selon les filtres de lignes) mais ne peuvent pas modifier le schéma de modèle.</span><span class="sxs-lookup"><span data-stu-id="f036c-155">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
  
4. <span data-ttu-id="f036c-156">Cliquez sur **Appartenance**, puis entrez un utilisateur ou un groupe dans votre client Azure AD par adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="f036c-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Ajouter un utilisateur](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="f036c-158">Si le rôle que vous créez a l’autorisation de Lecture, vous pouvez ajouter des filtres de lignes à l’aide d’une formule DAX.</span><span class="sxs-lookup"><span data-stu-id="f036c-158">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="f036c-159">Cliquez sur **Filtres de lignes**, sélectionnez une table, puis tapez une formule DAX dans le champ **Filtre DAX**.</span><span class="sxs-lookup"><span data-stu-id="f036c-159">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span></span> 

## <a name="to-add-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="f036c-160">Pour ajouter des rôles et des utilisateurs à l’aide d’un script TMSL</span><span class="sxs-lookup"><span data-stu-id="f036c-160">To add roles and users by using a TMSL script</span></span>
<span data-ttu-id="f036c-161">Vous pouvez exécuter un script TMSL dans la fenêtre XMLA dans SSMS ou à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f036c-161">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="f036c-162">Utilisez la commande [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) et l’objet [Rôles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl).</span><span class="sxs-lookup"><span data-stu-id="f036c-162">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="f036c-163">**Exemple de script TMSL**</span><span class="sxs-lookup"><span data-stu-id="f036c-163">**Sample TMSL script**</span></span>

<span data-ttu-id="f036c-164">Dans cet exemple, un utilisateur externe B2B et un groupe sont ajoutés au rôle d’analyste avec des autorisations de Lecture pour la base de données SalesBI.</span><span class="sxs-lookup"><span data-stu-id="f036c-164">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span></span> <span data-ttu-id="f036c-165">L’utilisateur externe et le groupe doivent être dans le même client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f036c-165">Both the external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users to query the model",
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

## <a name="to-add-roles-and-users-by-using-powershell"></a><span data-ttu-id="f036c-166">Pour ajouter des rôles et des utilisateurs à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="f036c-166">To add roles and users by using PowerShell</span></span>
<span data-ttu-id="f036c-167">Le module [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) fournit des applets de commande de gestion de bases de données spécifiques à chaque tâche, ainsi que l’applet de commande Invoke-ASCmd à usage général, qui accepte un script ou une requête utilisant le langage de script de modèle tabulaire (TMSL).</span><span class="sxs-lookup"><span data-stu-id="f036c-167">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="f036c-168">Les applets de commande suivantes sont utilisées pour la gestion des utilisateurs et des rôles de bases de données.</span><span class="sxs-lookup"><span data-stu-id="f036c-168">The following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="f036c-169">Applet de commande</span><span class="sxs-lookup"><span data-stu-id="f036c-169">Cmdlet</span></span>|<span data-ttu-id="f036c-170">Description</span><span class="sxs-lookup"><span data-stu-id="f036c-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="f036c-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="f036c-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="f036c-172">Ajoute un membre à un rôle de base de données.</span><span class="sxs-lookup"><span data-stu-id="f036c-172">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="f036c-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="f036c-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="f036c-174">Supprime un membre d’un rôle de base de données.</span><span class="sxs-lookup"><span data-stu-id="f036c-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="f036c-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="f036c-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="f036c-176">Exécute un script TMSL.</span><span class="sxs-lookup"><span data-stu-id="f036c-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="f036c-177">Filtres de lignes</span><span class="sxs-lookup"><span data-stu-id="f036c-177">Row filters</span></span>  
<span data-ttu-id="f036c-178">Les filtres de lignes définissent les lignes d’une table qui peuvent être interrogées par les membres d’un rôle donné.</span><span class="sxs-lookup"><span data-stu-id="f036c-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="f036c-179">Les filtres de lignes sont définis pour chaque table dans un modèle à l’aide de formules DAX.</span><span class="sxs-lookup"><span data-stu-id="f036c-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="f036c-180">Les filtres de lignes peuvent être définis uniquement pour les rôles avec des autorisations de Lecture et de Lecture et processus.</span><span class="sxs-lookup"><span data-stu-id="f036c-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="f036c-181">Par défaut, si un filtre de lignes n’est pas défini pour une table en particulier, les membres peuvent interroger toutes les lignes de la table, sauf si le filtrage croisé s’applique à partir d’une autre table.</span><span class="sxs-lookup"><span data-stu-id="f036c-181">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="f036c-182">Les filtres de lignes nécessitent une formule DAX, qui doit correspondre à une valeur TRUE/FALSE, pour définir les lignes qui peuvent être interrogées par les membres de ce rôle en particulier.</span><span class="sxs-lookup"><span data-stu-id="f036c-182">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="f036c-183">Les lignes non incluses dans la formule DAX ne peuvent pas être interrogées.</span><span class="sxs-lookup"><span data-stu-id="f036c-183">Rows not included in the DAX formula cannot be queried.</span></span> <span data-ttu-id="f036c-184">Par exemple, la table Clients avec l’expression de filtres de la ligne suivante, *=Customers [Country] = “USA”*, les membres du rôle Ventes peuvent voir uniquement les clients aux États-Unis.</span><span class="sxs-lookup"><span data-stu-id="f036c-184">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span></span>  
  
<span data-ttu-id="f036c-185">Les filtres de lignes s’appliquent aux lignes spécifiées et aux lignes connexes.</span><span class="sxs-lookup"><span data-stu-id="f036c-185">Row filters apply to the specified rows and related rows.</span></span> <span data-ttu-id="f036c-186">Lorsqu’une table possède plusieurs relations, les filtres appliquent la sécurité de la relation qui est active.</span><span class="sxs-lookup"><span data-stu-id="f036c-186">When a table has multiple relationships, filters apply security for the relationship that is active.</span></span> <span data-ttu-id="f036c-187">Les filtres de lignes sont croisés avec d’autres filtres de lignes définis pour les tables associées, par exemple :</span><span class="sxs-lookup"><span data-stu-id="f036c-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="f036c-188">Table</span><span class="sxs-lookup"><span data-stu-id="f036c-188">Table</span></span>|<span data-ttu-id="f036c-189">Expression DAX</span><span class="sxs-lookup"><span data-stu-id="f036c-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="f036c-190">Région</span><span class="sxs-lookup"><span data-stu-id="f036c-190">Region</span></span>|<span data-ttu-id="f036c-191">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="f036c-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="f036c-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="f036c-192">ProductCategory</span></span>|<span data-ttu-id="f036c-193">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="f036c-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="f036c-194">Transactions</span><span class="sxs-lookup"><span data-stu-id="f036c-194">Transactions</span></span>|<span data-ttu-id="f036c-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="f036c-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="f036c-196">L’effet net est que les membres peuvent interroger les lignes de données pour lesquelles le client réside aux États-Unis, la catégorie de produits est bicyclettes et l’année est 2016.</span><span class="sxs-lookup"><span data-stu-id="f036c-196">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span></span> <span data-ttu-id="f036c-197">Les utilisateurs ne peuvent pas interroger les transactions en dehors des États-Unis, qui ne sont pas des bicyclettes ou les transactions hors de 2016, sauf si ils sont membres d’un autre rôle qui accorde ces autorisations.</span><span class="sxs-lookup"><span data-stu-id="f036c-197">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="f036c-198">Vous pouvez utiliser le filtre, *= FALSE()*, pour refuser l’accès à toutes les lignes pour une table entière.</span><span class="sxs-lookup"><span data-stu-id="f036c-198">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f036c-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f036c-199">Next steps</span></span>
  <span data-ttu-id="f036c-200">[Gérer les administrateurs de serveur](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="f036c-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="f036c-201">Gérer Azure Analysis Services avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="f036c-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="f036c-202">Langage TMSL (Tabular Model Scripting Language)</span><span class="sxs-lookup"><span data-stu-id="f036c-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

