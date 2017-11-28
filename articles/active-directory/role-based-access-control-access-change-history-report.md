---
title: "Accès aux rapports - Contrôle d’accès en fonction du rôle Azure | Microsoft Docs"
description: "Générez un rapport qui répertorie toutes les modifications d’accès à vos abonnements Azure avec contrôle d’accès basé sur les rôles au cours des 90 derniers jours."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e8028ab43ed02ef0c0a1374326b07f72f97d9d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="db5b5-103">Créer un rapport d’accès pour le contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="db5b5-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="db5b5-104">Chaque fois qu’un utilisateur autorise ou interdit l’accès dans vos abonnements, les modifications sont consignées dans les événements Azure.</span><span class="sxs-lookup"><span data-stu-id="db5b5-104">Any time someone grants or revokes access within your subscriptions, the changes get logged in Azure events.</span></span> <span data-ttu-id="db5b5-105">Vous pouvez créer des rapports d’historique de modification d’accès pour voir toutes les modifications apportées au cours des 90 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="db5b5-105">You can create access change history reports to see all changes for the past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="db5b5-106">Créer un rapport avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="db5b5-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="db5b5-107">Pour créer un rapport d’historique des modifications d’accès dans PowerShell, utilisez la commande [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog).</span><span class="sxs-lookup"><span data-stu-id="db5b5-107">To create an access change history report in PowerShell, use the [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="db5b5-108">Lorsque vous appelez cette commande, vous pouvez spécifier quelle propriété des affectations répertorier, y compris les suivantes :</span><span class="sxs-lookup"><span data-stu-id="db5b5-108">When you call this command, you can specify which property of the assignments you want listed, including the following:</span></span>

| <span data-ttu-id="db5b5-109">Propriété</span><span class="sxs-lookup"><span data-stu-id="db5b5-109">Property</span></span> | <span data-ttu-id="db5b5-110">Description</span><span class="sxs-lookup"><span data-stu-id="db5b5-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="db5b5-111">**Action**</span><span class="sxs-lookup"><span data-stu-id="db5b5-111">**Action**</span></span> |<span data-ttu-id="db5b5-112">Si l’accès a été autorisé ou interdit</span><span class="sxs-lookup"><span data-stu-id="db5b5-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="db5b5-113">**Appelant**</span><span class="sxs-lookup"><span data-stu-id="db5b5-113">**Caller**</span></span> |<span data-ttu-id="db5b5-114">Le propriétaire responsable de la modification d’accès</span><span class="sxs-lookup"><span data-stu-id="db5b5-114">The owner responsible for the access change</span></span> |
| <span data-ttu-id="db5b5-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="db5b5-115">**PrincipalId**</span></span> | <span data-ttu-id="db5b5-116">L’identificateur unique de l’utilisateur, du groupe ou d’une application auquel ou à laquelle le rôle a été assigné</span><span class="sxs-lookup"><span data-stu-id="db5b5-116">The unique identifier of the user, group, or application that was assigned the role</span></span> |
| <span data-ttu-id="db5b5-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="db5b5-117">**PrincipalName**</span></span> |<span data-ttu-id="db5b5-118">Le nom de l’utilisateur, du groupe ou de l’application</span><span class="sxs-lookup"><span data-stu-id="db5b5-118">The name of the user, group, or application</span></span> |
| <span data-ttu-id="db5b5-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="db5b5-119">**PrincipalType**</span></span> |<span data-ttu-id="db5b5-120">Si l’affectation était pour un utilisateur, un groupe ou une application</span><span class="sxs-lookup"><span data-stu-id="db5b5-120">Whether the assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="db5b5-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="db5b5-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="db5b5-122">Le GUID du rôle qui a été accordé ou refusé</span><span class="sxs-lookup"><span data-stu-id="db5b5-122">The GUID of the role that was granted or revoked</span></span> |
| <span data-ttu-id="db5b5-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="db5b5-123">**RoleName**</span></span> |<span data-ttu-id="db5b5-124">Le rôle qui a été accordé ou refusé</span><span class="sxs-lookup"><span data-stu-id="db5b5-124">The role that was granted or revoked</span></span> |
| <span data-ttu-id="db5b5-125">**Portée**</span><span class="sxs-lookup"><span data-stu-id="db5b5-125">**Scope**</span></span> | <span data-ttu-id="db5b5-126">L’identificateur unique de l’abonnement, du groupe de ressources ou d’une ressource auquel ou à laquelle l’affectation s’applique</span><span class="sxs-lookup"><span data-stu-id="db5b5-126">The unique identifier of the subscription, resource group, or resource that the assignment applies to</span></span> | 
| <span data-ttu-id="db5b5-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="db5b5-127">**ScopeName**</span></span> |<span data-ttu-id="db5b5-128">Le nom de l’abonnement, du groupe de ressources ou de la ressource</span><span class="sxs-lookup"><span data-stu-id="db5b5-128">The name of the subscription, resource group, or resource</span></span> |
| <span data-ttu-id="db5b5-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="db5b5-129">**ScopeType**</span></span> |<span data-ttu-id="db5b5-130">Si l’étendue de l’affectation était au niveau de l’abonnement, du groupe de ressources ou de la ressource</span><span class="sxs-lookup"><span data-stu-id="db5b5-130">Whether the assignment was at the subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="db5b5-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="db5b5-131">**Timestamp**</span></span> |<span data-ttu-id="db5b5-132">La date et l’heure de la modification d’accès</span><span class="sxs-lookup"><span data-stu-id="db5b5-132">The date and time that access was changed</span></span> |

<span data-ttu-id="db5b5-133">Cet exemple de commande répertorie toutes les modifications d’accès de l’abonnement au cours des sept derniers jours :</span><span class="sxs-lookup"><span data-stu-id="db5b5-133">This example command lists all access changes in the subscription for the past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - capture d’écran](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="db5b5-135">Créer un rapport avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="db5b5-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="db5b5-136">Pour créer un rapport d’historique des modifications d’accès dans l’interface de ligne de commande Azure, utilisez la commande `azure role assignment changelog list` .</span><span class="sxs-lookup"><span data-stu-id="db5b5-136">To create an access change history report in the Azure command-line interface (CLI), use the `azure role assignment changelog list` command.</span></span>

## <a name="export-to-a-spreadsheet"></a><span data-ttu-id="db5b5-137">Exporter vers une feuille de calcul</span><span class="sxs-lookup"><span data-stu-id="db5b5-137">Export to a spreadsheet</span></span>
<span data-ttu-id="db5b5-138">Pour enregistrer le rapport ou manipuler les données, exportez les modifications d’accès vers un fichier .csv.</span><span class="sxs-lookup"><span data-stu-id="db5b5-138">To save the report, or manipulate the data, export the access changes into a .csv file.</span></span> <span data-ttu-id="db5b5-139">Vous pouvez ensuite afficher le rapport dans une feuille de calcul pour révision.</span><span class="sxs-lookup"><span data-stu-id="db5b5-139">You can then view the report in a spreadsheet for review.</span></span>

![ChangeLog affiché en tant que feuille de calcul - capture d’écran](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="db5b5-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="db5b5-141">Next steps</span></span>
* <span data-ttu-id="db5b5-142">Utilisation des [rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="db5b5-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="db5b5-143">En savoir plus sur la gestion du [contrôle d’accès en fonction du rôle Azure avec PowerShell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="db5b5-143">Learn how to manage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

