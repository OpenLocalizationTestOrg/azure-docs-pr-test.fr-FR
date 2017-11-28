---
title: "Surveillance et gestion des travaux Stream Analytics à l’aide de PowerShell | Microsoft Docs"
description: "Découvrez comment utiliser Azure PowerShell et les applets de commande pour surveiller et gérer des travaux Stream Analytics."
keywords: azure powershell, applets de commande azure powershell, commande powershell, scripts powershell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: e3449ee90cc83c5e823e5948a2a2e7e633c454f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="b3cfd-104">Surveillance et gestion des travaux Stream Analytics à l’aide des applets de commande Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3cfd-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="b3cfd-105">Découvrez comment surveiller et gérer les ressources Stream Analytics à l’aide d’applets de commande Azure PowerShell et de scripts PowerShell qui exécutent les tâches Stream Analytics de base.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-105">Learn how to monitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="b3cfd-106">Conditions requises pour l'exécution des applets de commande Azure PowerShell pour Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b3cfd-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="b3cfd-107">Créez un groupe de ressources Azure dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="b3cfd-108">Voici un exemple de script Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-108">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="b3cfd-109">Pour obtenir des informations sur Azure PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3cfd-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="b3cfd-110">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="b3cfd-111">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-111">Azure PowerShell 1.0:</span></span>  

         # Log in to your Azure account
        Login-AzureRmAccount

        # Select the Azure subscription you want to use to create the resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="b3cfd-112">Par défaut, la surveillance n’est pas activée pour les travaux Stream Analytics créés par programme.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="b3cfd-113">Vous pouvez activer manuellement la surveillance dans le portail Azure. Pour cela, accédez à la page de surveillance du travail et cliquez sur le bouton Activer. Vous pouvez également procéder par programme en suivant les étapes décrites dans [Azure Stream Analytics - Surveillance des travaux Stream Analytics par programme](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="b3cfd-113">You can manually enable monitoring in the Azure Portal by navigating to the job’s Monitor page and clicking the Enable button or you can do this programmatically by following the steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="b3cfd-114">Applets de commande Azure PowerShell pour Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b3cfd-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="b3cfd-115">Vous pouvez utiliser les applets de commande Azure PowerShell suivantes pour surveiller et gérer des travaux Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-115">The following Azure PowerShell cmdlets can be used to monitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="b3cfd-116">Notez qu'il existe différentes versions d'Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="b3cfd-117">**Dans les exemples répertoriés, la première commande s'applique à Azure PowerShell 0.9.8, la deuxième commande s'applique à Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-117">**In the examples listed the first command is for Azure PowerShell 0.9.8, the second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="b3cfd-118">Les commandes Azure PowerShell 1.0 contiennent toujours « AzureRM » dans la commande.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-118">The Azure PowerShell 1.0 commands will always have "AzureRM" in the command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="b3cfd-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="b3cfd-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="b3cfd-120">Répertorie tous les travaux Stream Analytics définis dans l’abonnement Azure ou le groupe de ressources spécifié, ou obtient des informations sur un travail spécifique au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-120">Lists all Stream Analytics jobs defined in the Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="b3cfd-121">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-121">**Example 1**</span></span>

<span data-ttu-id="b3cfd-122">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="b3cfd-123">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="b3cfd-124">Cette commande PowerShell retourne des informations sur tous les travaux Stream Analytics dans l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-124">This PowerShell command returns information about all the Stream Analytics jobs in the Azure subscription.</span></span>

<span data-ttu-id="b3cfd-125">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-125">**Example 2**</span></span>

<span data-ttu-id="b3cfd-126">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="b3cfd-127">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="b3cfd-128">Cette commande PowerShell retourne des informations sur tous les travaux Stream Analytics dans le groupe de ressources StreamAnalytics-Default-Central-US.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-128">This PowerShell command returns information about all the Stream Analytics jobs in the resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="b3cfd-129">**Exemple 3**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-129">**Example 3**</span></span>

<span data-ttu-id="b3cfd-130">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="b3cfd-131">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="b3cfd-132">Cette commande PowerShell retourne des informations sur le travail Stream Analytics StreamingJob dans le groupe de ressources StreamAnalytics-Default-Central-US.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-132">This PowerShell command returns information about the Stream Analytics job StreamingJob in the resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="b3cfd-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="b3cfd-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="b3cfd-134">Répertorie toutes les entrées qui sont définies dans un travail Stream Analytics spécifié ou obtient des informations sur une entrée spécifique.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-134">Lists all of the inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="b3cfd-135">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-135">**Example 1**</span></span>

<span data-ttu-id="b3cfd-136">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="b3cfd-137">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="b3cfd-138">Cette commande PowerShell retourne des informations sur toutes les entrées définies dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-138">This PowerShell command returns information about all the inputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="b3cfd-139">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-139">**Example 2**</span></span>

<span data-ttu-id="b3cfd-140">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="b3cfd-141">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="b3cfd-142">Cette commande PowerShell retourne des informations sur l’entrée nommée EntryStream définie dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-142">This PowerShell command returns information about the input named EntryStream defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="b3cfd-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="b3cfd-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="b3cfd-144">Répertorie toutes les sorties qui sont définies dans un travail Stream Analytics spécifié ou obtient des informations sur une sortie spécifique.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-144">Lists all of the outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="b3cfd-145">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-145">**Example 1**</span></span>

<span data-ttu-id="b3cfd-146">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="b3cfd-147">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="b3cfd-148">Cette commande PowerShell retourne des informations sur les sorties définies dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-148">This PowerShell command returns information about the outputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="b3cfd-149">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-149">**Example 2**</span></span>

<span data-ttu-id="b3cfd-150">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="b3cfd-151">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="b3cfd-152">Cette commande PowerShell retourne des informations sur la sortie nommée Output définie dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-152">This PowerShell command returns information about the output named Output defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="b3cfd-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="b3cfd-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="b3cfd-154">Obtient des informations sur le quota des unités de diffusion en continu d'une région spécifiée.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-154">Gets information about the quota of streaming units in a specified region.</span></span>

<span data-ttu-id="b3cfd-155">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-155">**Example 1**</span></span>

<span data-ttu-id="b3cfd-156">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="b3cfd-157">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="b3cfd-158">Cette commande PowerShell retourne des informations sur le quota et l’utilisation des unités de diffusion en continu dans la région Centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-158">This PowerShell command returns information about the quota and usage of streaming units in the Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="b3cfd-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="b3cfd-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="b3cfd-160">Obtient des informations sur une transformation spécifique définie dans un travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="b3cfd-161">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-161">**Example 1**</span></span>

<span data-ttu-id="b3cfd-162">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="b3cfd-163">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="b3cfd-164">Cette commande PowerShell retourne des informations sur la transformation nommée StreamingJob dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-164">This PowerShell command returns information about the transformation called StreamingJob in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="b3cfd-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="b3cfd-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="b3cfd-166">Crée une entrée dans un travail Stream Analytics ou met à jour une entrée spécifiée existante.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="b3cfd-167">Vous pouvez spécifier le nom de l'entrée dans le fichier .json ou sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-167">The name of the input can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="b3cfd-168">Si vous spécifiez les deux, le nom indiqué sur la ligne de commande doit être identique à celui contenu dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-168">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="b3cfd-169">Si vous spécifiez une entrée qui existe déjà et que vous ne spécifiez pas le paramètre -Force, l'applet de commande vous demande s'il faut remplacer l'entrée existante.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-169">If you specify an input that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing input.</span></span>

<span data-ttu-id="b3cfd-170">Si vous spécifiez le paramètre -Force et un nom d'entrée existant, l'entrée est remplacée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-170">If you specify the –Force parameter and specify an existing input name, the input will be replaced without confirmation.</span></span>

<span data-ttu-id="b3cfd-171">Pour plus d’informations sur la structure et le contenu du fichier JSON, reportez-vous à la section [Création d’une entrée (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] de la [bibliothèque de référence des API REST de gestion de Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="b3cfd-171">For detailed information on the JSON file structure and contents, refer to the [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="b3cfd-172">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-172">**Example 1**</span></span>

<span data-ttu-id="b3cfd-173">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="b3cfd-174">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="b3cfd-175">Cette commande PowerShell crée une entrée à partir du fichier Input.json.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-175">This PowerShell command creates a new input from the file Input.json.</span></span> <span data-ttu-id="b3cfd-176">Si une entrée existante avec le nom spécifié dans le fichier de définition d'entrée est déjà définie, l'applet de commande vous demande s'il faut la remplacer.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-176">If an existing input with the name specified in the input definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="b3cfd-177">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-177">**Example 2**</span></span>

<span data-ttu-id="b3cfd-178">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="b3cfd-179">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="b3cfd-180">Cette commande PowerShell crée une entrée dans le travail nommé EntryStream.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-180">This PowerShell command creates a new input in the job called EntryStream.</span></span> <span data-ttu-id="b3cfd-181">Si une entrée existante portant ce nom est déjà définie, l'applet de commande vous demande s'il faut la remplacer.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-181">If an existing input with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="b3cfd-182">**Exemple 3**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-182">**Example 3**</span></span>

<span data-ttu-id="b3cfd-183">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="b3cfd-184">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="b3cfd-185">Cette commande PowerShell remplace la définition de la source d’entrée existante nommée EntryStream par la définition qui se trouve dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-185">This PowerShell command replaces the definition of the existing input source called EntryStream with the definition from the file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="b3cfd-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="b3cfd-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="b3cfd-187">Crée un travail Stream Analytics dans Microsoft Azure ou met à jour la définition d'un travail existant spécifié.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-187">Creates a new Stream Analytics job in Microsoft Azure, or updates the definition of an existing specified job.</span></span>

<span data-ttu-id="b3cfd-188">Vous pouvez spécifier le nom du travail dans le fichier .json ou sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-188">The name of the job can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="b3cfd-189">Si vous spécifiez les deux, le nom indiqué sur la ligne de commande doit être identique à celui contenu dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-189">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="b3cfd-190">Si vous spécifiez un nom de travail qui existe déjà et que vous ne spécifiez pas le paramètre -Force, l'applet de commande vous demande s'il faut remplacer le travail existant.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-190">If you specify a job name that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing job.</span></span>

<span data-ttu-id="b3cfd-191">Si vous spécifiez le paramètre -Force et un nom de travail existant, la définition de travail est remplacée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-191">If you specify the –Force parameter and specify an existing job name, the job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="b3cfd-192">Pour plus d’informations sur la structure et le contenu du fichier JSON, reportez-vous à la section [Création d’un travail Stream Analytics][msdn-rest-api-create-stream-analytics-job] de la [bibliothèque de référence des API REST de gestion de Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="b3cfd-192">For detailed information on the JSON file structure and contents, refer to the [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="b3cfd-193">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-193">**Example 1**</span></span>

<span data-ttu-id="b3cfd-194">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="b3cfd-195">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="b3cfd-196">Cette commande PowerShell crée un travail à partir de la définition qui se trouve dans JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-196">This PowerShell command creates a new job from the definition in JobDefinition.json.</span></span> <span data-ttu-id="b3cfd-197">Si un travail existant avec le nom spécifié dans le fichier de définition de travail est déjà défini, l'applet de commande vous demande s'il faut le remplacer.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-197">If an existing job with the name specified in the job definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="b3cfd-198">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-198">**Example 2**</span></span>

<span data-ttu-id="b3cfd-199">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="b3cfd-200">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="b3cfd-201">Cette commande PowerShell remplace la définition du travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-201">This PowerShell command replaces the job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="b3cfd-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="b3cfd-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="b3cfd-203">Crée une sortie dans un travail Stream Analytics ou met à jour une sortie existante.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="b3cfd-204">Vous pouvez spécifier le nom de la sortie dans le fichier .json ou sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-204">The name of the output can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="b3cfd-205">Si vous spécifiez les deux, le nom indiqué sur la ligne de commande doit être identique à celui contenu dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-205">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="b3cfd-206">Si vous spécifiez une sortie qui existe déjà et que vous ne spécifiez pas le paramètre -Force, l'applet de commande vous demande s'il faut remplacer la sortie existante.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-206">If you specify an output that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing output.</span></span>

<span data-ttu-id="b3cfd-207">Si vous spécifiez le paramètre -Force et un nom de sortie existant, la sortie est remplacée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-207">If you specify the –Force parameter and specify an existing output name, the output will be replaced without confirmation.</span></span>

<span data-ttu-id="b3cfd-208">Pour plus d’informations sur la structure et le contenu du fichier JSON, reportez-vous à la section [Création d’une sortie (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] de la[ bibliothèque de référence des API REST de gestion de Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="b3cfd-208">For detailed information on the JSON file structure and contents, refer to the [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="b3cfd-209">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-209">**Example 1**</span></span>

<span data-ttu-id="b3cfd-210">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="b3cfd-211">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="b3cfd-212">Cette commande PowerShell crée une sortie nommée « output » dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-212">This PowerShell command creates a new output called "output" in the job StreamingJob.</span></span> <span data-ttu-id="b3cfd-213">Si une sortie existante portant ce nom est déjà définie, l'applet de commande vous demande s'il faut la remplacer.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-213">If an existing output with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="b3cfd-214">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-214">**Example 2**</span></span>

<span data-ttu-id="b3cfd-215">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="b3cfd-216">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="b3cfd-217">Cette commande PowerShell remplace la définition de la sortie « output » dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-217">This PowerShell command replaces the definition for "output" in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="b3cfd-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="b3cfd-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="b3cfd-219">Crée une transformation dans un travail Stream Analytics ou met à jour la transformation existante.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-219">Creates a new transformation within a Stream Analytics job, or updates the existing transformation.</span></span>

<span data-ttu-id="b3cfd-220">Vous pouvez spécifier le nom de la transformation dans le fichier .json ou sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-220">The name of the transformation can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="b3cfd-221">Si vous spécifiez les deux, le nom indiqué sur la ligne de commande doit être identique à celui contenu dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-221">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="b3cfd-222">Si vous spécifiez une transformation qui existe déjà et que vous ne spécifiez pas le paramètre -Force, l'applet de commande vous demande s'il faut remplacer la transformation existante.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-222">If you specify a transformation that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing transformation.</span></span>

<span data-ttu-id="b3cfd-223">Si vous spécifiez le paramètre -Force et un nom de transformation existant, la transformation est remplacée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-223">If you specify the –Force parameter and specify an existing transformation name, the transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="b3cfd-224">Pour plus d’informations sur la structure et le contenu du fichier JSON, reportez-vous à la section [Création d’une transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] de la [bibliothèque de référence des API REST de gestion de Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="b3cfd-224">For detailed information on the JSON file structure and contents, refer to the [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="b3cfd-225">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-225">**Example 1**</span></span>

<span data-ttu-id="b3cfd-226">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="b3cfd-227">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="b3cfd-228">Cette commande PowerShell crée une transformation nommée StreamingJobTransform dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-228">This PowerShell command creates a new transformation called StreamingJobTransform in the job StreamingJob.</span></span> <span data-ttu-id="b3cfd-229">Si une transformation existante est déjà définie avec ce nom, l'applet de commande vous demande s'il faut la remplacer.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-229">If an existing transformation is already defined with this name, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="b3cfd-230">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-230">**Example 2**</span></span>

<span data-ttu-id="b3cfd-231">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="b3cfd-232">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="b3cfd-233">Cette commande PowerShell remplace la définition de StreamingJobTransform dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-233">This PowerShell command replaces the definition of StreamingJobTransform in the job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="b3cfd-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="b3cfd-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="b3cfd-235">Supprime de manière asynchrone une entrée spécifique d'un travail Stream Analytics dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="b3cfd-236">Si vous spécifiez le paramètre -Force, l'entrée est supprimée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-236">If you specify the –Force parameter, the input will be deleted without confirmation.</span></span>

<span data-ttu-id="b3cfd-237">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-237">**Example 1**</span></span>

<span data-ttu-id="b3cfd-238">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="b3cfd-239">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="b3cfd-240">Cette commande PowerShell supprime l’entrée EventStream dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-240">This PowerShell command removes the input EventStream in the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="b3cfd-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="b3cfd-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="b3cfd-242">Supprime de manière asynchrone un travail Stream Analytics spécifique dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="b3cfd-243">Si vous spécifiez le paramètre -Force, le travail est supprimé sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-243">If you specify the –Force parameter, the job will be deleted without confirmation.</span></span>

<span data-ttu-id="b3cfd-244">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-244">**Example 1**</span></span>

<span data-ttu-id="b3cfd-245">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="b3cfd-246">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="b3cfd-247">Cette commande PowerShell supprime le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-247">This PowerShell command removes the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="b3cfd-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="b3cfd-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="b3cfd-249">Supprime de manière asynchrone une sortie spécifique d'un travail Stream Analytics dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="b3cfd-250">Si vous spécifiez le paramètre -Force, la sortie est supprimée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-250">If you specify the –Force parameter, the output will be deleted without confirmation.</span></span>

<span data-ttu-id="b3cfd-251">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-251">**Example 1**</span></span>

<span data-ttu-id="b3cfd-252">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="b3cfd-253">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="b3cfd-254">Cette commande PowerShell supprime la sortie Output dans le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-254">This PowerShell command removes the output Output in the job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="b3cfd-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="b3cfd-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="b3cfd-256">Déploie et démarre un travail Stream Analytics dans Microsoft Azure de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="b3cfd-257">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-257">**Example 1**</span></span>

<span data-ttu-id="b3cfd-258">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="b3cfd-259">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="b3cfd-260">Cette commande PowerShell démarre le travail StreamingJob avec une heure de début de sortie personnalisée définie sur le 12 décembre 2012, 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-260">This PowerShell command starts the job StreamingJob with a custom output start time set to December 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="b3cfd-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="b3cfd-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="b3cfd-262">Arrête l'exécution d'un travail Stream Analytics dans Microsoft Azure de façon asynchrone et libère les ressources qui étaient utilisées.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="b3cfd-263">La définition du travail et les métadonnées restent disponibles dans votre abonnement par le biais du Portail Azure et des API de gestion ; ainsi, le travail peut être modifié et redémarré.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-263">The job definition and metadata will remain available within your subscription through both the Azure portal and management APIs, such that the job can be edited and restarted.</span></span> <span data-ttu-id="b3cfd-264">Un travail à l'état Arrêté ne vous sera pas facturé.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-264">You will not be charged for a job in the stopped state.</span></span>

<span data-ttu-id="b3cfd-265">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-265">**Example 1**</span></span>

<span data-ttu-id="b3cfd-266">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="b3cfd-267">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="b3cfd-268">Cette commande PowerShell arrête le travail StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-268">This PowerShell command stops the job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="b3cfd-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="b3cfd-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="b3cfd-270">Teste la capacité de Stream Analytics à se connecter à une entrée spécifiée.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-270">Tests the ability of Stream Analytics to connect to a specified input.</span></span>

<span data-ttu-id="b3cfd-271">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-271">**Example 1**</span></span>

<span data-ttu-id="b3cfd-272">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="b3cfd-273">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="b3cfd-274">Cette commande PowerShell teste l’état de la connexion de l’entrée EntryStream dans StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-274">This PowerShell command tests the connection status of the input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="b3cfd-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="b3cfd-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="b3cfd-276">Teste la capacité de Stream Analytics à se connecter à une sortie spécifiée.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-276">Tests the ability of Stream Analytics to connect to a specified output.</span></span>

<span data-ttu-id="b3cfd-277">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="b3cfd-277">**Example 1**</span></span>

<span data-ttu-id="b3cfd-278">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="b3cfd-279">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="b3cfd-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="b3cfd-280">Cette commande PowerShell teste l’état de la connexion de la sortie Output dans StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="b3cfd-280">This PowerShell command tests the connection status of the output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="b3cfd-281">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="b3cfd-281">Get support</span></span>
<span data-ttu-id="b3cfd-282">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="b3cfd-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b3cfd-283">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3cfd-283">Next steps</span></span>
* [<span data-ttu-id="b3cfd-284">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b3cfd-284">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b3cfd-285">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b3cfd-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b3cfd-286">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b3cfd-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b3cfd-287">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b3cfd-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b3cfd-288">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b3cfd-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

