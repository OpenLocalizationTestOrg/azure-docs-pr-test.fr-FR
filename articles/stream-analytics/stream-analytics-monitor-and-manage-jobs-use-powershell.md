---
title: "aaaMonitor et gérer des tâches de flux de données Analytique avec PowerShell | Documents Microsoft"
description: "Découvrez comment toomonitor d’Azure PowerShell et les applets de commande toouse et gérer des tâches de flux de données Analytique."
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
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="960b7-104">Surveillance et gestion des travaux Stream Analytics à l’aide des applets de commande Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="960b7-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="960b7-105">Découvrez comment toomonitor et gérer les ressources de flux de données Analytique avec les applets de commande PowerShell de Azure et l’écriture de scripts powershell qui exécutent des tâches de flux de données Analytique base.</span><span class="sxs-lookup"><span data-stu-id="960b7-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="960b7-106">Conditions requises pour l'exécution des applets de commande Azure PowerShell pour Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="960b7-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="960b7-107">Créez un groupe de ressources Azure dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="960b7-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="960b7-108">Hello Voici un exemple de script Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="960b7-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="960b7-109">Pour obtenir des informations sur Azure PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="960b7-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="960b7-110">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="960b7-111">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="960b7-112">Par défaut, la surveillance n’est pas activée pour les travaux Stream Analytics créés par programme.</span><span class="sxs-lookup"><span data-stu-id="960b7-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="960b7-113">Vous pouvez manuellement activer l’analyse dans le portail Azure en parcourant la page de surveillance de la tâche toohello de hello et en cliquant sur le bouton Activer de hello ou vous pouvez le faire par programme en suivant les étapes de hello situés [Analytique de flux de données Azure - analyse de flux de données Analytique des travaux par programmation](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="960b7-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="960b7-114">Applets de commande Azure PowerShell pour Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="960b7-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="960b7-115">Hello suivant d’applets de commande PowerShell de Azure peut être utilisé toomonitor et gérer des tâches d’Analytique de flux de données Azure.</span><span class="sxs-lookup"><span data-stu-id="960b7-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="960b7-116">Notez qu'il existe différentes versions d'Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="960b7-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="960b7-117">**Dans les exemples hello hello répertoriés première commande est de Azure PowerShell 0.9.8, commande deuxième hello est pour Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="960b7-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="960b7-118">commandes Hello Azure PowerShell 1.0 aura toujours « Azure Resource Manager » dans la commande hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="960b7-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="960b7-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="960b7-120">Répertorie toutes les tâches de flux de données Analytique définies dans hello abonnement Azure ou le groupe de ressources spécifié, ou obtient des informations sur une tâche spécifique au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="960b7-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="960b7-121">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-121">**Example 1**</span></span>

<span data-ttu-id="960b7-122">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="960b7-123">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="960b7-124">Cette commande PowerShell retourne des informations sur toutes les tâches de flux de données Analytique hello Bonjour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="960b7-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="960b7-125">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="960b7-125">**Example 2**</span></span>

<span data-ttu-id="960b7-126">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="960b7-127">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="960b7-128">Cette commande PowerShell retourne des informations sur toutes les tâches de flux de données Analytique hello dans le groupe de ressources hello Stream Analytics par défaut-Centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="960b7-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="960b7-129">**Exemple 3**</span><span class="sxs-lookup"><span data-stu-id="960b7-129">**Example 3**</span></span>

<span data-ttu-id="960b7-130">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="960b7-131">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="960b7-132">Cette commande PowerShell retourne des informations sur la tâche de flux de données Analytique hello StreamingJob dans le groupe de ressources hello Stream Analytics par défaut-Centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="960b7-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="960b7-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="960b7-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="960b7-134">Répertorie toutes les entrées de hello qui sont définies dans une tâche de flux de données Analytique spécifiée ou obtient des informations sur une entrée spécifique.</span><span class="sxs-lookup"><span data-stu-id="960b7-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="960b7-135">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-135">**Example 1**</span></span>

<span data-ttu-id="960b7-136">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="960b7-137">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="960b7-138">Cette commande PowerShell retourne des informations sur toutes les entrées de hello définis dans le travail hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="960b7-139">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="960b7-139">**Example 2**</span></span>

<span data-ttu-id="960b7-140">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="960b7-141">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="960b7-142">Cette commande PowerShell retourne des informations sur les entrées hello nommée EntryStream défini dans le travail hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="960b7-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="960b7-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="960b7-144">Répertorie toutes les sorties hello qui sont définies dans une tâche de flux de données Analytique spécifiée ou obtient des informations sur une sortie spécifique.</span><span class="sxs-lookup"><span data-stu-id="960b7-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="960b7-145">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-145">**Example 1**</span></span>

<span data-ttu-id="960b7-146">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="960b7-147">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="960b7-148">Cette commande PowerShell retourne des informations sur les sorties hello définies dans la tâche de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="960b7-149">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="960b7-149">**Example 2**</span></span>

<span data-ttu-id="960b7-150">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="960b7-151">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="960b7-152">Cette commande PowerShell retourne des informations sur la sortie hello nommé défini dans le travail hello StreamingJob de sortie.</span><span class="sxs-lookup"><span data-stu-id="960b7-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="960b7-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="960b7-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="960b7-154">Obtient les informations de quota de hello de diffusion en continu les unités dans la région spécifiée.</span><span class="sxs-lookup"><span data-stu-id="960b7-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="960b7-155">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-155">**Example 1**</span></span>

<span data-ttu-id="960b7-156">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="960b7-157">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="960b7-158">Cette commande PowerShell retourne des informations sur le quota de hello et de l’utilisation des unités de diffusion en continu dans la région du centre des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="960b7-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="960b7-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="960b7-160">Obtient des informations sur une transformation spécifique définie dans un travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="960b7-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="960b7-161">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-161">**Example 1**</span></span>

<span data-ttu-id="960b7-162">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="960b7-163">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="960b7-164">Cette commande PowerShell retourne des informations sur la transformation hello appelée StreamingJob dans la tâche de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="960b7-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="960b7-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="960b7-166">Crée une entrée dans un travail Stream Analytics ou met à jour une entrée spécifiée existante.</span><span class="sxs-lookup"><span data-stu-id="960b7-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="960b7-167">Hello nom de l’entrée de hello peut être spécifié dans le fichier .json de hello ou sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="960b7-168">Si les deux sont spécifiées, nom hello sur la ligne de commande hello doit hello identique hello un fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="960b7-169">Si vous spécifiez une entrée existe déjà et que vous ne spécifiez pas hello – paramètre Force, applet de commande hello demandera ou non tooreplace hello entrée existante.</span><span class="sxs-lookup"><span data-stu-id="960b7-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="960b7-170">Si vous spécifiez hello – paramètre Force et spécifiez un existant, nom d’entrée, hello entrée sera remplacée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="960b7-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="960b7-171">Pour plus d’informations sur la structure du fichier JSON hello et de contenu, consultez toohello [créer une entrée (Analytique de flux de données Azure)] [ msdn-rest-api-create-stream-analytics-input] section Hello [API REST de gestion des flux de données Analytique Bibliothèque de référence][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="960b7-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="960b7-172">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-172">**Example 1**</span></span>

<span data-ttu-id="960b7-173">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="960b7-174">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="960b7-175">Cette commande PowerShell crée une nouvelle entrée à partir du fichier de hello Input.json.</span><span class="sxs-lookup"><span data-stu-id="960b7-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="960b7-176">Si une entrée existante avec le nom hello spécifié dans le fichier de définition d’entrée de hello est déjà définie, l’applet de commande hello vous demande ou non tooreplace il.</span><span class="sxs-lookup"><span data-stu-id="960b7-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="960b7-177">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="960b7-177">**Example 2**</span></span>

<span data-ttu-id="960b7-178">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="960b7-179">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="960b7-180">Cette commande PowerShell crée une entrée dans la tâche hello appelé EntryStream.</span><span class="sxs-lookup"><span data-stu-id="960b7-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="960b7-181">Si une entrée existante portant ce nom est déjà définie, l’applet de commande hello vous demande ou non tooreplace il.</span><span class="sxs-lookup"><span data-stu-id="960b7-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="960b7-182">**Exemple 3**</span><span class="sxs-lookup"><span data-stu-id="960b7-182">**Example 3**</span></span>

<span data-ttu-id="960b7-183">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="960b7-184">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="960b7-185">Cette commande PowerShell remplace la définition de hello de source d’entrée existante hello appelé EntryStream avec définition hello à partir du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="960b7-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="960b7-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="960b7-187">Crée une tâche de flux de données Analytique dans Microsoft Azure, ou met à jour de définition de hello d’une tâche spécifiée existante.</span><span class="sxs-lookup"><span data-stu-id="960b7-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="960b7-188">nom de Hello du travail de hello peut être spécifié dans le fichier .json de hello ou sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="960b7-189">Si les deux sont spécifiées, nom hello sur la ligne de commande hello doit hello identique hello un fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="960b7-190">Si vous spécifiez un nom de tâche existe déjà et que vous ne spécifiez pas hello – paramètre Force, applet de commande hello demandera ou non tooreplace hello travail existant.</span><span class="sxs-lookup"><span data-stu-id="960b7-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="960b7-191">Si vous spécifiez hello – paramètre Force et spécifiez un nom de travail existant, définition de la tâche hello est remplacée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="960b7-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="960b7-192">Pour plus d’informations sur la structure du fichier JSON hello et de contenu, consultez toohello [créer une tâche de flux de données Analytique] [ msdn-rest-api-create-stream-analytics-job] section Hello [référence d’API REST gestion des flux de données Analytique Bibliothèque][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="960b7-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="960b7-193">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-193">**Example 1**</span></span>

<span data-ttu-id="960b7-194">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="960b7-195">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="960b7-196">Cette commande PowerShell crée une nouvelle tâche à partir de la définition de hello dans JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="960b7-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="960b7-197">Si un travail existant avec le nom hello spécifié dans le fichier de définition de tâche hello est déjà défini, l’applet de commande hello vous demande ou non tooreplace il.</span><span class="sxs-lookup"><span data-stu-id="960b7-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="960b7-198">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="960b7-198">**Example 2**</span></span>

<span data-ttu-id="960b7-199">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="960b7-200">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="960b7-201">Cette commande PowerShell remplace la définition de tâche hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="960b7-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="960b7-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="960b7-203">Crée une sortie dans un travail Stream Analytics ou met à jour une sortie existante.</span><span class="sxs-lookup"><span data-stu-id="960b7-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="960b7-204">nom de Hello de sortie de hello peut être spécifié dans le fichier .json de hello ou sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="960b7-205">Si les deux sont spécifiées, nom hello sur la ligne de commande hello doit hello identique hello un fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="960b7-206">Si vous spécifiez une sortie qui existe déjà et que vous ne spécifiez pas hello – paramètre Force, applet de commande hello demandera ou non tooreplace hello sortie existant.</span><span class="sxs-lookup"><span data-stu-id="960b7-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="960b7-207">Si vous spécifiez hello – paramètre Force et spécifiez le nom de sortie existant, la sortie de hello est remplacé sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="960b7-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="960b7-208">Pour plus d’informations sur la structure du fichier JSON hello et de contenu, consultez toohello [créer une sortie (Analytique de flux de données Azure)] [ msdn-rest-api-create-stream-analytics-output] section Hello [API REST de gestion des flux de données Analytique Bibliothèque de référence][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="960b7-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="960b7-209">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-209">**Example 1**</span></span>

<span data-ttu-id="960b7-210">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="960b7-211">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="960b7-212">Cette commande PowerShell crée une sortie appelée « sortie » dans la tâche de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="960b7-213">Si une sortie existante portant ce nom est déjà définie, l’applet de commande hello vous demande ou non tooreplace il.</span><span class="sxs-lookup"><span data-stu-id="960b7-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="960b7-214">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="960b7-214">**Example 2**</span></span>

<span data-ttu-id="960b7-215">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="960b7-216">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="960b7-217">Cette commande PowerShell remplace la définition de hello de « sortie » dans la tâche de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="960b7-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="960b7-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="960b7-219">Crée une nouvelle transformation au sein d’une tâche de flux de données Analytique ou met à jour de la transformation de hello existant.</span><span class="sxs-lookup"><span data-stu-id="960b7-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="960b7-220">nom de Hello de transformation de hello peut être spécifié dans le fichier .json de hello ou sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="960b7-221">Si les deux sont spécifiées, nom hello sur la ligne de commande hello doit hello identique hello un fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="960b7-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="960b7-222">Si vous spécifiez une transformation qui existe déjà et que vous ne spécifiez pas hello – paramètre Force, applet de commande hello demandera ou non tooreplace hello transformation existante.</span><span class="sxs-lookup"><span data-stu-id="960b7-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="960b7-223">Si vous spécifiez hello – paramètre Force et spécifiez un nom existant de la transformation, la transformation de hello est remplacée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="960b7-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="960b7-224">Pour plus d’informations sur la structure du fichier JSON hello et de contenu, consultez toohello [créer une Transformation (Analytique de flux de données Azure)] [ msdn-rest-api-create-stream-analytics-transformation] section Hello [gestion des flux de données Analytique Bibliothèque de référence d’API REST][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="960b7-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="960b7-225">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-225">**Example 1**</span></span>

<span data-ttu-id="960b7-226">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="960b7-227">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="960b7-228">Cette commande PowerShell crée une nouvelle transformation appelée StreamingJobTransform dans la tâche de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="960b7-229">Si une transformation existante est déjà définie avec ce nom, l’applet de commande hello vous demande ou non tooreplace il.</span><span class="sxs-lookup"><span data-stu-id="960b7-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="960b7-230">**Exemple 2**</span><span class="sxs-lookup"><span data-stu-id="960b7-230">**Example 2**</span></span>

<span data-ttu-id="960b7-231">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="960b7-232">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="960b7-233">Cette commande PowerShell remplace la définition de hello de StreamingJobTransform dans la tâche de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="960b7-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="960b7-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="960b7-235">Supprime de manière asynchrone une entrée spécifique d'un travail Stream Analytics dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="960b7-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="960b7-236">Si vous spécifiez hello – paramètre Force, hello d’entrée est supprimée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="960b7-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="960b7-237">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-237">**Example 1**</span></span>

<span data-ttu-id="960b7-238">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="960b7-239">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="960b7-240">Cette commande PowerShell supprime hello EventStream d’entrée dans la tâche de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="960b7-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="960b7-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="960b7-242">Supprime de manière asynchrone un travail Stream Analytics spécifique dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="960b7-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="960b7-243">Si vous spécifiez hello – paramètre Force, hello travail sera supprimée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="960b7-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="960b7-244">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-244">**Example 1**</span></span>

<span data-ttu-id="960b7-245">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="960b7-246">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="960b7-247">Cette commande PowerShell supprime le travail de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="960b7-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="960b7-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="960b7-249">Supprime de manière asynchrone une sortie spécifique d'un travail Stream Analytics dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="960b7-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="960b7-250">Si vous spécifiez hello – paramètre Force, hello sortie sera supprimée sans confirmation.</span><span class="sxs-lookup"><span data-stu-id="960b7-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="960b7-251">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-251">**Example 1**</span></span>

<span data-ttu-id="960b7-252">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="960b7-253">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="960b7-254">Sortie de sortie de cette commande supprime hello de PowerShell dans la tâche de hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="960b7-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="960b7-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="960b7-256">Déploie et démarre un travail Stream Analytics dans Microsoft Azure de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="960b7-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="960b7-257">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-257">**Example 1**</span></span>

<span data-ttu-id="960b7-258">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="960b7-259">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="960b7-260">Cette commande PowerShell démarre hello travail StreamingJob avec une heure de début de sortie personnalisée définie tooDecember 12, 2012, 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="960b7-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="960b7-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="960b7-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="960b7-262">Arrête l'exécution d'un travail Stream Analytics dans Microsoft Azure de façon asynchrone et libère les ressources qui étaient utilisées.</span><span class="sxs-lookup"><span data-stu-id="960b7-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="960b7-263">Hello métadonnées et la définition de la tâche reste disponibles au sein de votre abonnement via hello portail Azure et les API de gestion, telles que hello travail peut être modifié et redémarré.</span><span class="sxs-lookup"><span data-stu-id="960b7-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="960b7-264">Vous ne serez pas facturé pour une tâche dans l’état de hello s’est arrêté.</span><span class="sxs-lookup"><span data-stu-id="960b7-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="960b7-265">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-265">**Example 1**</span></span>

<span data-ttu-id="960b7-266">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="960b7-267">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="960b7-268">Cette commande PowerShell arrête le travail hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="960b7-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="960b7-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="960b7-270">Possibilité de hello de tests de flux de données Analytique tooconnect tooa spécifié d’entrée.</span><span class="sxs-lookup"><span data-stu-id="960b7-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="960b7-271">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-271">**Example 1**</span></span>

<span data-ttu-id="960b7-272">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="960b7-273">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="960b7-274">Cet état connexion hello de tests de commande PowerShell de hello entrée EntryStream dans StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="960b7-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="960b7-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="960b7-276">Possibilité de hello de tests de flux de données Analytique tooconnect tooa spécifié de sortie.</span><span class="sxs-lookup"><span data-stu-id="960b7-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="960b7-277">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="960b7-277">**Example 1**</span></span>

<span data-ttu-id="960b7-278">Azure PowerShell 0.9.8 :</span><span class="sxs-lookup"><span data-stu-id="960b7-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="960b7-279">Azure PowerShell 1.0 :</span><span class="sxs-lookup"><span data-stu-id="960b7-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="960b7-280">Cet état connexion hello de tests de commande PowerShell de hello output sortie dans StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="960b7-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="960b7-281">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="960b7-281">Get support</span></span>
<span data-ttu-id="960b7-282">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="960b7-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="960b7-283">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="960b7-283">Next steps</span></span>
* [<span data-ttu-id="960b7-284">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="960b7-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="960b7-285">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="960b7-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="960b7-286">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="960b7-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="960b7-287">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="960b7-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="960b7-288">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="960b7-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

