---
title: "Création de rapports aaaAccess - Azure RBAC. | Documents Microsoft"
description: "Générer un rapport que répertorie toutes les modifications dans tooyour d’accès abonnements Azure, avec contrôle d’accès basée sur hello 90 derniers jours."
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
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="fff76-103">Créer un rapport d’accès pour le contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="fff76-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="fff76-104">Chaque fois qu’un utilisateur accorde ou révoque l’accès au sein de vos abonnements, les modifications de hello sont consignées dans les événements de Azure.</span><span class="sxs-lookup"><span data-stu-id="fff76-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="fff76-105">Vous pouvez créer accès modifier l’historique des rapports toosee toutes les modifications pour hello 90 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="fff76-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="fff76-106">Créer un rapport avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fff76-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="fff76-107">toocreate un accès à modifier le rapport d’historique dans PowerShell, utilisez hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) commande.</span><span class="sxs-lookup"><span data-stu-id="fff76-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="fff76-108">Lorsque vous appelez cette commande, vous pouvez spécifier la propriété hello aux affectations de répertoriées, y compris les hello suivant :</span><span class="sxs-lookup"><span data-stu-id="fff76-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="fff76-109">Propriété</span><span class="sxs-lookup"><span data-stu-id="fff76-109">Property</span></span> | <span data-ttu-id="fff76-110">Description</span><span class="sxs-lookup"><span data-stu-id="fff76-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fff76-111">**Action**</span><span class="sxs-lookup"><span data-stu-id="fff76-111">**Action**</span></span> |<span data-ttu-id="fff76-112">Si l’accès a été autorisé ou interdit</span><span class="sxs-lookup"><span data-stu-id="fff76-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="fff76-113">**Appelant**</span><span class="sxs-lookup"><span data-stu-id="fff76-113">**Caller**</span></span> |<span data-ttu-id="fff76-114">le propriétaire de Hello responsable de l’accès hello modifier</span><span class="sxs-lookup"><span data-stu-id="fff76-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="fff76-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="fff76-115">**PrincipalId**</span></span> | <span data-ttu-id="fff76-116">Identificateur unique de l’application qui a été attribuée le rôle de hello, groupe ou utilisateur de hello de Hello</span><span class="sxs-lookup"><span data-stu-id="fff76-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="fff76-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="fff76-117">**PrincipalName**</span></span> |<span data-ttu-id="fff76-118">Hello nom d’utilisateur de hello, groupe ou application</span><span class="sxs-lookup"><span data-stu-id="fff76-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="fff76-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="fff76-119">**PrincipalType**</span></span> |<span data-ttu-id="fff76-120">Indique si l’attribution de hello a pour un utilisateur, un groupe ou une application</span><span class="sxs-lookup"><span data-stu-id="fff76-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="fff76-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="fff76-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="fff76-122">Hello GUID du rôle hello qui a été accordé ou révoqué</span><span class="sxs-lookup"><span data-stu-id="fff76-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="fff76-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="fff76-123">**RoleName**</span></span> |<span data-ttu-id="fff76-124">rôle Hello qui a été accordé ou révoqué</span><span class="sxs-lookup"><span data-stu-id="fff76-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="fff76-125">**Portée**</span><span class="sxs-lookup"><span data-stu-id="fff76-125">**Scope**</span></span> | <span data-ttu-id="fff76-126">Identificateur unique de Hello d’abonnement de hello, groupe de ressources ou ressource hello assignation s’applique également</span><span class="sxs-lookup"><span data-stu-id="fff76-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="fff76-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="fff76-127">**ScopeName**</span></span> |<span data-ttu-id="fff76-128">Hello nom d’abonnement de hello, groupe de ressources ou ressource</span><span class="sxs-lookup"><span data-stu-id="fff76-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="fff76-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="fff76-129">**ScopeType**</span></span> |<span data-ttu-id="fff76-130">Indique si l’attribution de hello a à portée de la ressource, groupe de ressources ou abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="fff76-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="fff76-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="fff76-131">**Timestamp**</span></span> |<span data-ttu-id="fff76-132">hello date et l’heure que l’accès a été modifié.</span><span class="sxs-lookup"><span data-stu-id="fff76-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="fff76-133">Cet exemple de commande répertorie toutes les modifications d’accès dans l’abonnement hello pour hello sept derniers jours :</span><span class="sxs-lookup"><span data-stu-id="fff76-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - capture d’écran](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="fff76-135">Créer un rapport avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="fff76-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="fff76-136">toocreate un rapport historique des modifications accès Bonjour Azure interface de ligne de commande (CLI), utilisez hello `azure role assignment changelog list` commande.</span><span class="sxs-lookup"><span data-stu-id="fff76-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="fff76-137">Exporter la feuille de calcul tooa</span><span class="sxs-lookup"><span data-stu-id="fff76-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="fff76-138">toosave hello rapport ou manipuler des données de hello, exportation hello accès se transforme en un fichier .csv.</span><span class="sxs-lookup"><span data-stu-id="fff76-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="fff76-139">Vous pouvez ensuite afficher les rapports hello dans une feuille de calcul pour la révision.</span><span class="sxs-lookup"><span data-stu-id="fff76-139">You can then view hello report in a spreadsheet for review.</span></span>

![ChangeLog affiché en tant que feuille de calcul - capture d’écran](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="fff76-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fff76-141">Next steps</span></span>
* <span data-ttu-id="fff76-142">Utilisation des [rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="fff76-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="fff76-143">Découvrez comment toomanage [RBAC Azure avec powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="fff76-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

