---
title: aaaManage des comptes Azure Media Services avec PowerShell
description: "Découvrez comment les comptes toomanage Azure Media Services avec les applets de commande PowerShell."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="9bf1d-103">Gérer des comptes Azure Media Services avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bf1d-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9bf1d-104">Portail</span><span class="sxs-lookup"><span data-stu-id="9bf1d-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="9bf1d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bf1d-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="9bf1d-106">REST</span><span class="sxs-lookup"><span data-stu-id="9bf1d-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="9bf1d-107">toocreate en mesure de toobe un compte Azure Media Services, vous devez disposer d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="9bf1d-108">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9bf1d-109">Pour plus d'informations, consultez la page <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Version d'évaluation gratuite d'Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="9bf1d-110">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9bf1d-110">Overview</span></span>
<span data-ttu-id="9bf1d-111">Cet article répertorie des applets de commande PowerShell Azure hello pour Azure Media Services (AMS) dans le cadre d’Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="9bf1d-112">applets de commande Hello existent Bonjour **Microsoft.Azure.Commands.Media** espace de noms.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="9bf1d-113">Versions</span><span class="sxs-lookup"><span data-stu-id="9bf1d-113">Versions</span></span>
<span data-ttu-id="9bf1d-114">**ApiVersion** :   "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="9bf1d-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="9bf1d-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="9bf1d-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="9bf1d-116">Créez un service multimédia.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="9bf1d-117">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9bf1d-117">Syntax</span></span>
<span data-ttu-id="9bf1d-118">Jeu de paramètres : StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="9bf1d-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="9bf1d-119">Jeu de paramètres : StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="9bf1d-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="9bf1d-120">parameters</span><span class="sxs-lookup"><span data-stu-id="9bf1d-120">Parameters</span></span>
<span data-ttu-id="9bf1d-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-122">Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="9bf1d-123">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-123">Aliases</span></span> | <span data-ttu-id="9bf1d-124">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-125">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-125">Required?</span></span> |<span data-ttu-id="9bf1d-126">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-126">true</span></span> |
| <span data-ttu-id="9bf1d-127">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-127">Position?</span></span> |<span data-ttu-id="9bf1d-128">0</span><span class="sxs-lookup"><span data-stu-id="9bf1d-128">0</span></span> |
| <span data-ttu-id="9bf1d-129">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-129">Default value</span></span> |<span data-ttu-id="9bf1d-130">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-130">none</span></span> |
| <span data-ttu-id="9bf1d-131">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-131">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-132">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-133">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-133">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-134">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-134">false</span></span> |

<span data-ttu-id="9bf1d-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-136">Spécifie le nom hello du service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="9bf1d-137">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-137">Aliases</span></span> | <span data-ttu-id="9bf1d-138">Nom</span><span class="sxs-lookup"><span data-stu-id="9bf1d-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-139">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-139">Required?</span></span> |<span data-ttu-id="9bf1d-140">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-140">true</span></span> |
| <span data-ttu-id="9bf1d-141">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-141">Position?</span></span> |<span data-ttu-id="9bf1d-142">1</span><span class="sxs-lookup"><span data-stu-id="9bf1d-142">1</span></span> |
| <span data-ttu-id="9bf1d-143">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-143">Default value</span></span> |<span data-ttu-id="9bf1d-144">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-144">none</span></span> |
| <span data-ttu-id="9bf1d-145">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-145">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-146">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-146">false</span></span> |
| <span data-ttu-id="9bf1d-147">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-147">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-148">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-148">false</span></span> |

<span data-ttu-id="9bf1d-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-150">Spécifie l’emplacement de la ressource du service de support hello hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="9bf1d-151">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-151">Aliases</span></span> | <span data-ttu-id="9bf1d-152">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-153">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-153">Required?</span></span> |<span data-ttu-id="9bf1d-154">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-154">true</span></span> |
| <span data-ttu-id="9bf1d-155">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-155">Position?</span></span> |<span data-ttu-id="9bf1d-156">2</span><span class="sxs-lookup"><span data-stu-id="9bf1d-156">2</span></span> |
| <span data-ttu-id="9bf1d-157">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-157">Default value</span></span> |<span data-ttu-id="9bf1d-158">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-158">none</span></span> |
| <span data-ttu-id="9bf1d-159">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-159">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-160">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-161">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-161">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-162">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-162">false</span></span> |

<span data-ttu-id="9bf1d-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-164">Spécifie un compte de stockage principal associé au service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="9bf1d-165">Nouveau compte de stockage (créée avec hello API Resource Manager) pris en charge uniquement.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="9bf1d-166">Hello compte de stockage doit exister et a hello même emplacement avec le service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="9bf1d-167">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-167">Aliases</span></span> | <span data-ttu-id="9bf1d-168">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-169">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-169">Required?</span></span> |<span data-ttu-id="9bf1d-170">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-170">true</span></span> |
| <span data-ttu-id="9bf1d-171">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-171">Position?</span></span> |<span data-ttu-id="9bf1d-172">3</span><span class="sxs-lookup"><span data-stu-id="9bf1d-172">3</span></span> |
| <span data-ttu-id="9bf1d-173">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-173">Default value</span></span> |<span data-ttu-id="9bf1d-174">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-174">none</span></span> |
| <span data-ttu-id="9bf1d-175">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-175">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-176">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-177">Nom du jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="9bf1d-177">Parameter set name</span></span> |<span data-ttu-id="9bf1d-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="9bf1d-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="9bf1d-179">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-179">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-180">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-180">false</span></span> |

<span data-ttu-id="9bf1d-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="9bf1d-182">Spécifie les comptes de stockage associé au service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="9bf1d-183">Nouveau compte de stockage (créée avec hello API Resource Manager) pris en charge uniquement.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="9bf1d-184">Hello compte de stockage doit exister et a hello même emplacement avec le service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="9bf1d-185">Un seul compte de stockage peut être spécifié comme compte principal.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="9bf1d-186">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-186">Aliases</span></span> | <span data-ttu-id="9bf1d-187">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-188">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-188">Required?</span></span> |<span data-ttu-id="9bf1d-189">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-189">true</span></span> |
| <span data-ttu-id="9bf1d-190">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-190">Position?</span></span> |<span data-ttu-id="9bf1d-191">3</span><span class="sxs-lookup"><span data-stu-id="9bf1d-191">3</span></span> |
| <span data-ttu-id="9bf1d-192">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-192">Default value</span></span> |<span data-ttu-id="9bf1d-193">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-193">none</span></span> |
| <span data-ttu-id="9bf1d-194">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-194">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-195">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-196">Nom du jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="9bf1d-196">Parameter set name</span></span> |<span data-ttu-id="9bf1d-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="9bf1d-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="9bf1d-198">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-198">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-199">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-199">false</span></span> |

<span data-ttu-id="9bf1d-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="9bf1d-201">Spécifie une table de hachage de balises hello qui sont associés au service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="9bf1d-202">Exemple : @{« balise1 « = » value1 » ; » balise2 » = : value2 »}</span><span class="sxs-lookup"><span data-stu-id="9bf1d-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="9bf1d-203">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-203">Aliases</span></span> | <span data-ttu-id="9bf1d-204">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-205">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-205">Required?</span></span> |<span data-ttu-id="9bf1d-206">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-206">false</span></span> |
| <span data-ttu-id="9bf1d-207">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-207">Position?</span></span> |<span data-ttu-id="9bf1d-208">named</span><span class="sxs-lookup"><span data-stu-id="9bf1d-208">named</span></span> |
| <span data-ttu-id="9bf1d-209">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-209">Default value</span></span> |<span data-ttu-id="9bf1d-210">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-210">none</span></span> |
| <span data-ttu-id="9bf1d-211">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-211">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-212">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-212">false</span></span> |
| <span data-ttu-id="9bf1d-213">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-213">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-214">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-214">false</span></span> |

<span data-ttu-id="9bf1d-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="9bf1d-216">Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="9bf1d-217">Entrées</span><span class="sxs-lookup"><span data-stu-id="9bf1d-217">Inputs</span></span>
<span data-ttu-id="9bf1d-218">type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="9bf1d-219">outputs</span><span class="sxs-lookup"><span data-stu-id="9bf1d-219">Outputs</span></span>
<span data-ttu-id="9bf1d-220">type de sortie Hello est de type hello d’objets hello hello applet de commande émet.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="9bf1d-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="9bf1d-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="9bf1d-222">Met à jour un service multimédia.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="9bf1d-223">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9bf1d-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="9bf1d-224">parameters</span><span class="sxs-lookup"><span data-stu-id="9bf1d-224">Parameters</span></span>
<span data-ttu-id="9bf1d-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-226">Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="9bf1d-227">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-227">Aliases</span></span> | <span data-ttu-id="9bf1d-228">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-229">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-229">Required?</span></span> |<span data-ttu-id="9bf1d-230">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-230">true</span></span> |
| <span data-ttu-id="9bf1d-231">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-231">Position?</span></span> |<span data-ttu-id="9bf1d-232">0</span><span class="sxs-lookup"><span data-stu-id="9bf1d-232">0</span></span> |
| <span data-ttu-id="9bf1d-233">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-233">Default Value</span></span> |<span data-ttu-id="9bf1d-234">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-234">none</span></span> |
| <span data-ttu-id="9bf1d-235">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="9bf1d-236">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-237">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-237">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-238">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-238">false</span></span> |

<span data-ttu-id="9bf1d-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-240">Spécifie le nom hello du service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="9bf1d-241">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-241">Aliases</span></span> | <span data-ttu-id="9bf1d-242">Nom</span><span class="sxs-lookup"><span data-stu-id="9bf1d-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-243">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-243">Required?</span></span> |<span data-ttu-id="9bf1d-244">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-244">True</span></span> |
| <span data-ttu-id="9bf1d-245">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-245">Position?</span></span> |<span data-ttu-id="9bf1d-246">1</span><span class="sxs-lookup"><span data-stu-id="9bf1d-246">1</span></span> |
| <span data-ttu-id="9bf1d-247">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-247">Default value</span></span> |<span data-ttu-id="9bf1d-248">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-248">None</span></span> |
| <span data-ttu-id="9bf1d-249">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-249">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-250">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-251">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-251">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-252">False</span><span class="sxs-lookup"><span data-stu-id="9bf1d-252">False</span></span> |

<span data-ttu-id="9bf1d-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="9bf1d-254">Spécifie les comptes de stockage associé au service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="9bf1d-255">Nouveau compte de stockage (créée avec hello API Resource Manager) pris en charge uniquement.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="9bf1d-256">Hello compte de stockage doit exister et a hello même emplacement avec le service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="9bf1d-257">Un seul compte de stockage peut être spécifié comme compte principal.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="9bf1d-258">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-258">Aliases</span></span> | <span data-ttu-id="9bf1d-259">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-260">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-260">Required?</span></span> |<span data-ttu-id="9bf1d-261">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-261">false</span></span> |
| <span data-ttu-id="9bf1d-262">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-262">Position?</span></span> |<span data-ttu-id="9bf1d-263">named</span><span class="sxs-lookup"><span data-stu-id="9bf1d-263">Named</span></span> |
| <span data-ttu-id="9bf1d-264">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-264">Default value</span></span> |<span data-ttu-id="9bf1d-265">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-265">none</span></span> |
| <span data-ttu-id="9bf1d-266">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-266">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-267">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-268">Nom du jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="9bf1d-268">Parameter set name</span></span> |<span data-ttu-id="9bf1d-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="9bf1d-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="9bf1d-270">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-270">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-271">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-271">false</span></span> |

<span data-ttu-id="9bf1d-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="9bf1d-273">Spécifie une table de hachage de balises hello qui sont associés à ce service de support.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="9bf1d-274">balises Hello qui sont associés au service de support hello sont remplacés par la valeur spécifiée par le client de hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="9bf1d-275">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-275">Aliases</span></span> | <span data-ttu-id="9bf1d-276">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-277">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-277">Required?</span></span> |<span data-ttu-id="9bf1d-278">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-278">False</span></span> |
| <span data-ttu-id="9bf1d-279">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-279">Position?</span></span> |<span data-ttu-id="9bf1d-280">named</span><span class="sxs-lookup"><span data-stu-id="9bf1d-280">Named</span></span> |
| <span data-ttu-id="9bf1d-281">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-281">Default value</span></span> |<span data-ttu-id="9bf1d-282">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-282">None</span></span> |
| <span data-ttu-id="9bf1d-283">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-283">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-284">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-285">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-285">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-286">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-286">false</span></span> |

<span data-ttu-id="9bf1d-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="9bf1d-288">Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="9bf1d-289">Entrées</span><span class="sxs-lookup"><span data-stu-id="9bf1d-289">Inputs</span></span>
<span data-ttu-id="9bf1d-290">type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="9bf1d-291">outputs</span><span class="sxs-lookup"><span data-stu-id="9bf1d-291">Outputs</span></span>
<span data-ttu-id="9bf1d-292">type de sortie Hello est de type hello d’objets hello hello applet de commande émet.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="9bf1d-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="9bf1d-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="9bf1d-294">Supprime un service multimédia.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="9bf1d-295">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9bf1d-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="9bf1d-296">parameters</span><span class="sxs-lookup"><span data-stu-id="9bf1d-296">Parameters</span></span>
<span data-ttu-id="9bf1d-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-298">Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="9bf1d-299">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-299">Aliases</span></span> | <span data-ttu-id="9bf1d-300">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-301">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-301">Required?</span></span> |<span data-ttu-id="9bf1d-302">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-302">true</span></span> |
| <span data-ttu-id="9bf1d-303">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-303">Position?</span></span> |<span data-ttu-id="9bf1d-304">0</span><span class="sxs-lookup"><span data-stu-id="9bf1d-304">0</span></span> |
| <span data-ttu-id="9bf1d-305">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-305">Default value</span></span> |<span data-ttu-id="9bf1d-306">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-306">none</span></span> |
| <span data-ttu-id="9bf1d-307">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-307">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-308">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-309">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-309">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-310">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-310">false</span></span> |

<span data-ttu-id="9bf1d-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-312">Spécifie le nom hello du service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="9bf1d-313">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-313">Aliases</span></span> | <span data-ttu-id="9bf1d-314">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-315">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-315">Required?</span></span> |<span data-ttu-id="9bf1d-316">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-316">true</span></span> |
| <span data-ttu-id="9bf1d-317">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-317">Position?</span></span> |<span data-ttu-id="9bf1d-318">2</span><span class="sxs-lookup"><span data-stu-id="9bf1d-318">2</span></span> |
| <span data-ttu-id="9bf1d-319">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-319">Default value</span></span> |<span data-ttu-id="9bf1d-320">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-320">None</span></span> |
| <span data-ttu-id="9bf1d-321">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-321">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-322">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-323">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-323">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-324">False</span><span class="sxs-lookup"><span data-stu-id="9bf1d-324">False</span></span> |

<span data-ttu-id="9bf1d-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="9bf1d-326">Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="9bf1d-327">Entrées</span><span class="sxs-lookup"><span data-stu-id="9bf1d-327">Inputs</span></span>
<span data-ttu-id="9bf1d-328">type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="9bf1d-329">outputs</span><span class="sxs-lookup"><span data-stu-id="9bf1d-329">Outputs</span></span>
<span data-ttu-id="9bf1d-330">type de sortie Hello est de type hello d’objets hello hello applet de commande émet.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="9bf1d-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="9bf1d-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="9bf1d-332">Obtient tous les services multimédia d'un groupe de ressources ou un service multimédia avec un nom donné.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="9bf1d-333">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9bf1d-333">Syntax</span></span>
<span data-ttu-id="9bf1d-334">Jeu de paramètres : ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="9bf1d-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="9bf1d-335">Jeu de paramètres : AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="9bf1d-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="9bf1d-336">parameters</span><span class="sxs-lookup"><span data-stu-id="9bf1d-336">Parameters</span></span>
<span data-ttu-id="9bf1d-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-338">Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="9bf1d-339">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-339">Aliases</span></span> | <span data-ttu-id="9bf1d-340">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-341">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-341">Required?</span></span> |<span data-ttu-id="9bf1d-342">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-342">true</span></span> |
| <span data-ttu-id="9bf1d-343">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-343">Position?</span></span> |<span data-ttu-id="9bf1d-344">0</span><span class="sxs-lookup"><span data-stu-id="9bf1d-344">0</span></span> |
| <span data-ttu-id="9bf1d-345">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-345">Default value</span></span> |<span data-ttu-id="9bf1d-346">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-346">none</span></span> |
| <span data-ttu-id="9bf1d-347">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-347">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-348">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-349">Nom du jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="9bf1d-349">Parameter set name</span></span> |<span data-ttu-id="9bf1d-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="9bf1d-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="9bf1d-351">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-351">Accept wildcard characters?</span></span>   <span data-ttu-id="9bf1d-352">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-352">false</span></span>

<span data-ttu-id="9bf1d-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-354">Spécifie le nom hello du service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="9bf1d-355">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-355">Aliases</span></span> | <span data-ttu-id="9bf1d-356">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-357">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-357">Required?</span></span> |<span data-ttu-id="9bf1d-358">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-358">true</span></span> |
| <span data-ttu-id="9bf1d-359">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-359">Position?</span></span> |<span data-ttu-id="9bf1d-360">1</span><span class="sxs-lookup"><span data-stu-id="9bf1d-360">1</span></span> |
| <span data-ttu-id="9bf1d-361">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-361">Default value</span></span> |<span data-ttu-id="9bf1d-362">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-362">none</span></span> |
| <span data-ttu-id="9bf1d-363">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-363">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-364">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-365">Nom du jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="9bf1d-365">Parameter set name</span></span> |<span data-ttu-id="9bf1d-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="9bf1d-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="9bf1d-367">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-367">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-368">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-368">false</span></span> |

<span data-ttu-id="9bf1d-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="9bf1d-370">Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="9bf1d-371">Entrées</span><span class="sxs-lookup"><span data-stu-id="9bf1d-371">Inputs</span></span>
<span data-ttu-id="9bf1d-372">type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="9bf1d-373">outputs</span><span class="sxs-lookup"><span data-stu-id="9bf1d-373">Outputs</span></span>
<span data-ttu-id="9bf1d-374">type de sortie Hello est de type hello d’objets hello hello applet de commande émet.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="9bf1d-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="9bf1d-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="9bf1d-376">Obtient les clés d’un service multimédia.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="9bf1d-377">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9bf1d-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="9bf1d-378">parameters</span><span class="sxs-lookup"><span data-stu-id="9bf1d-378">Parameters</span></span>
<span data-ttu-id="9bf1d-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-380">Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="9bf1d-381">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-381">Aliases</span></span> | <span data-ttu-id="9bf1d-382">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-383">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-383">Required?</span></span> |<span data-ttu-id="9bf1d-384">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-384">true</span></span> |
| <span data-ttu-id="9bf1d-385">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-385">Position?</span></span> |<span data-ttu-id="9bf1d-386">0</span><span class="sxs-lookup"><span data-stu-id="9bf1d-386">0</span></span> |
| <span data-ttu-id="9bf1d-387">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-387">Default value</span></span> |<span data-ttu-id="9bf1d-388">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-388">none</span></span> |
| <span data-ttu-id="9bf1d-389">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-389">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-390">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-391">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-391">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-392">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-392">false</span></span> |

<span data-ttu-id="9bf1d-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-394">Spécifie le nom hello du service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="9bf1d-395">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-395">Aliases</span></span> | <span data-ttu-id="9bf1d-396">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-397">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-397">Required?</span></span> |<span data-ttu-id="9bf1d-398">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-398">true</span></span> |
| <span data-ttu-id="9bf1d-399">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-399">Position?</span></span> |<span data-ttu-id="9bf1d-400">1</span><span class="sxs-lookup"><span data-stu-id="9bf1d-400">1</span></span> |
| <span data-ttu-id="9bf1d-401">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-401">Default value</span></span> |<span data-ttu-id="9bf1d-402">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-402">none</span></span> |
| <span data-ttu-id="9bf1d-403">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-403">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-404">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-405">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-405">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-406">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-406">false</span></span> |

<span data-ttu-id="9bf1d-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="9bf1d-408">Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="9bf1d-409">Entrées</span><span class="sxs-lookup"><span data-stu-id="9bf1d-409">Inputs</span></span>
<span data-ttu-id="9bf1d-410">type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="9bf1d-411">outputs</span><span class="sxs-lookup"><span data-stu-id="9bf1d-411">Outputs</span></span>
<span data-ttu-id="9bf1d-412">type de sortie Hello est de type hello d’objets hello hello applet de commande émet.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="9bf1d-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="9bf1d-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="9bf1d-414">Régénère une clé primaire ou secondaire d’un service multimédia.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="9bf1d-415">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9bf1d-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="9bf1d-416">parameters</span><span class="sxs-lookup"><span data-stu-id="9bf1d-416">Parameters</span></span>
<span data-ttu-id="9bf1d-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-418">Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="9bf1d-419">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-419">Aliases</span></span> | <span data-ttu-id="9bf1d-420">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-421">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-421">Required?</span></span> |<span data-ttu-id="9bf1d-422">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-422">true</span></span> |
| <span data-ttu-id="9bf1d-423">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-423">Position?</span></span> |<span data-ttu-id="9bf1d-424">0</span><span class="sxs-lookup"><span data-stu-id="9bf1d-424">0</span></span> |
| <span data-ttu-id="9bf1d-425">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-425">Default value</span></span> |<span data-ttu-id="9bf1d-426">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-426">none</span></span> |
| <span data-ttu-id="9bf1d-427">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-427">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-428">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-429">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-429">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-430">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-430">false</span></span> |

<span data-ttu-id="9bf1d-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-432">Spécifie le nom hello du service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="9bf1d-433">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-433">Aliases</span></span> | <span data-ttu-id="9bf1d-434">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-435">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-435">Required?</span></span> |<span data-ttu-id="9bf1d-436">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-436">true</span></span> |
| <span data-ttu-id="9bf1d-437">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-437">Position?</span></span> |<span data-ttu-id="9bf1d-438">1</span><span class="sxs-lookup"><span data-stu-id="9bf1d-438">1</span></span> |
| <span data-ttu-id="9bf1d-439">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-439">Default value</span></span> |<span data-ttu-id="9bf1d-440">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-440">none</span></span> |
| <span data-ttu-id="9bf1d-441">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-441">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-442">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-443">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-443">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-444">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-444">false</span></span> |

<span data-ttu-id="9bf1d-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="9bf1d-446">Spécifie le type de clé hello du service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="9bf1d-447">Principal ou secondaire</span><span class="sxs-lookup"><span data-stu-id="9bf1d-447">Primary or Secondary</span></span>

| <span data-ttu-id="9bf1d-448">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-448">Aliases</span></span> | <span data-ttu-id="9bf1d-449">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-450">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-450">Required?</span></span> |<span data-ttu-id="9bf1d-451">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-451">true</span></span> |
| <span data-ttu-id="9bf1d-452">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-452">Position?</span></span> |<span data-ttu-id="9bf1d-453">2</span><span class="sxs-lookup"><span data-stu-id="9bf1d-453">2</span></span> |
| <span data-ttu-id="9bf1d-454">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-454">Default value</span></span> |<span data-ttu-id="9bf1d-455">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-455">none</span></span> |
| <span data-ttu-id="9bf1d-456">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-456">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-457">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-457">false</span></span> |
| <span data-ttu-id="9bf1d-458">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-458">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-459">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-459">false</span></span> |

<span data-ttu-id="9bf1d-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="9bf1d-461">Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="9bf1d-462">Entrées</span><span class="sxs-lookup"><span data-stu-id="9bf1d-462">Inputs</span></span>
<span data-ttu-id="9bf1d-463">type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toothe applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="9bf1d-464">outputs</span><span class="sxs-lookup"><span data-stu-id="9bf1d-464">Outputs</span></span>
<span data-ttu-id="9bf1d-465">type de sortie Hello est de type hello d’objets hello hello applet de commande émet.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="9bf1d-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="9bf1d-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="9bf1d-467">Synchronise les clés de compte de stockage pour un compte de stockage associé au service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="9bf1d-468">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9bf1d-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="9bf1d-469">parameters</span><span class="sxs-lookup"><span data-stu-id="9bf1d-469">Parameters</span></span>
<span data-ttu-id="9bf1d-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-471">Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="9bf1d-472">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-472">Aliases</span></span> | <span data-ttu-id="9bf1d-473">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-474">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-474">Required?</span></span> |<span data-ttu-id="9bf1d-475">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-475">true</span></span> |
| <span data-ttu-id="9bf1d-476">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-476">Position?</span></span> |<span data-ttu-id="9bf1d-477">0</span><span class="sxs-lookup"><span data-stu-id="9bf1d-477">0</span></span> |
| <span data-ttu-id="9bf1d-478">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-478">Default value</span></span> |<span data-ttu-id="9bf1d-479">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-479">none</span></span> |
| <span data-ttu-id="9bf1d-480">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-480">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-481">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-482">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-482">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-483">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-483">false</span></span> |

<span data-ttu-id="9bf1d-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-485">Spécifie le nom hello du service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="9bf1d-486">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-486">Aliases</span></span> | <span data-ttu-id="9bf1d-487">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-488">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-488">Required?</span></span> |<span data-ttu-id="9bf1d-489">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-489">true</span></span> |
| <span data-ttu-id="9bf1d-490">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-490">Position?</span></span> |<span data-ttu-id="9bf1d-491">1</span><span class="sxs-lookup"><span data-stu-id="9bf1d-491">1</span></span> |
| <span data-ttu-id="9bf1d-492">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-492">Default value</span></span> |<span data-ttu-id="9bf1d-493">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-493">none</span></span> |
| <span data-ttu-id="9bf1d-494">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-494">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-495">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-496">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-496">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-497">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-497">false</span></span> |

<span data-ttu-id="9bf1d-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="9bf1d-499">Spécifie le compte de stockage hello associé au service de support hello.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="9bf1d-500">Alias</span><span class="sxs-lookup"><span data-stu-id="9bf1d-500">Aliases</span></span> | <span data-ttu-id="9bf1d-501">ID</span><span class="sxs-lookup"><span data-stu-id="9bf1d-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="9bf1d-502">Requis ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-502">Required?</span></span> |<span data-ttu-id="9bf1d-503">true</span><span class="sxs-lookup"><span data-stu-id="9bf1d-503">true</span></span> |
| <span data-ttu-id="9bf1d-504">Position ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-504">Position?</span></span> |<span data-ttu-id="9bf1d-505">2</span><span class="sxs-lookup"><span data-stu-id="9bf1d-505">2</span></span> |
| <span data-ttu-id="9bf1d-506">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9bf1d-506">Default value</span></span> |<span data-ttu-id="9bf1d-507">(aucun)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-507">none</span></span> |
| <span data-ttu-id="9bf1d-508">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-508">Accept pipeline input?</span></span> |<span data-ttu-id="9bf1d-509">True(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9bf1d-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="9bf1d-510">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="9bf1d-510">Accept wildcard characters?</span></span> |<span data-ttu-id="9bf1d-511">false</span><span class="sxs-lookup"><span data-stu-id="9bf1d-511">false</span></span> |

<span data-ttu-id="9bf1d-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="9bf1d-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="9bf1d-513">Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="9bf1d-514">Entrées</span><span class="sxs-lookup"><span data-stu-id="9bf1d-514">Inputs</span></span>
<span data-ttu-id="9bf1d-515">type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="9bf1d-516">outputs</span><span class="sxs-lookup"><span data-stu-id="9bf1d-516">Outputs</span></span>
<span data-ttu-id="9bf1d-517">type de sortie Hello est de type hello d’objets hello hello applet de commande émet.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="9bf1d-518">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="9bf1d-518">Next step</span></span>
<span data-ttu-id="9bf1d-519">Consultez les chemins d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="9bf1d-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9bf1d-520">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="9bf1d-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

