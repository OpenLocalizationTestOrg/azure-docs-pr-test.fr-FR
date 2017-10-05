---
title: "Ressources de variables dans Azure Automation | Microsoft Docs"
description: "Les ressources de variables sont des valeurs disponibles pour tous les Runbooks et configurations DSC d’Azure Automation.  Cet article présente les variables de façon détaillée et comment les utiliser dans une création textuelle ou graphique."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: dc00e1e5fa8df5cb55e7e2672137d1df44133773
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="84f88-104">Ressources de variables dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="84f88-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="84f88-105">Les ressources de variables sont des valeurs disponibles pour tous les Runbooks et configurations DSC de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="84f88-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="84f88-106">Elles peuvent être créées, modifiées et récupérées à partir du portail Azure, de Windows PowerShell ou bien d’un Runbook ou d’une configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="84f88-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="84f88-107">Les variables Automation sont utiles pour les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="84f88-107">Automation variables are useful for the following scenarios:</span></span>

- <span data-ttu-id="84f88-108">Partager une valeur entre plusieurs Runbooks ou configurations DSC.</span><span class="sxs-lookup"><span data-stu-id="84f88-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="84f88-109">Partager une valeur entre plusieurs tâches du même Runbook ou de la même configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="84f88-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span></span>

- <span data-ttu-id="84f88-110">Gérer une valeur du portail ou de la ligne de commande Windows PowerShell, qui est utilisée par les Runbooks ou les configurations DSC, par exemple un ensemble d’éléments de configuration communs comme une liste spécifique de noms de machine virtuelle, un groupe de ressources particulier, un nom de domaine Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="84f88-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="84f88-111">Les variables Automation sont conservées afin qu’elles demeurent disponibles même si le Runbook ou la configuration DSC échoue.</span><span class="sxs-lookup"><span data-stu-id="84f88-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span></span>  <span data-ttu-id="84f88-112">Cela permet aussi à une valeur d’être définie par un Runbook ou une configuration DSC, puis utilisée par un autre Runbook ou configuration DSC, ou bien par le même Runbook ou configuration DSC à sa prochaine exécution.</span><span class="sxs-lookup"><span data-stu-id="84f88-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span></span>

<span data-ttu-id="84f88-113">Quand une variable est créée, vous pouvez spécifier qu'elle doit être stockée de manière chiffrée.</span><span class="sxs-lookup"><span data-stu-id="84f88-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="84f88-114">Quand une variable est chiffrée, elle est stockée de manière sécurisée dans Azure Automation. Sa valeur ne peut pas être récupérée à partir de l’applet de commande [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx), fournie dans le cadre du module Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84f88-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of the Azure PowerShell module.</span></span>  <span data-ttu-id="84f88-115">Une valeur chiffrée ne peut être récupérée que d’une seule façon, à partir de l’activité **Get-AutomationVariable** d’un Runbook ou d’une configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="84f88-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="84f88-116">Les ressources sécurisées dans Azure Automation incluent les informations d'identification, les certificats, les connexions et les variables chiffrées.</span><span class="sxs-lookup"><span data-stu-id="84f88-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="84f88-117">Ces ressources sont chiffrées et stockées dans Azure Automation à l'aide d'une clé unique, générée pour chaque compte Automation.</span><span class="sxs-lookup"><span data-stu-id="84f88-117">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="84f88-118">Cette clé est chiffrée par un certificat principal et stockée dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="84f88-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="84f88-119">Avant de stocker une ressource sécurisée, la clé du compte Automation est déchiffrée à l'aide du certificat principal, puis utilisée pour chiffrer la ressource.</span><span class="sxs-lookup"><span data-stu-id="84f88-119">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="84f88-120">Types de variables</span><span class="sxs-lookup"><span data-stu-id="84f88-120">Variable types</span></span>

<span data-ttu-id="84f88-121">Lorsque vous créez une variable avec le portail Azure, vous devez spécifier un type de données dans la liste déroulante afin que le portail puisse afficher le contrôle approprié pour l’entrée de la valeur de la variable.</span><span class="sxs-lookup"><span data-stu-id="84f88-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span></span> <span data-ttu-id="84f88-122">La variable n'est pas limitée à ce type de données, mais vous devez définir la variable à l'aide de Windows PowerShell si vous souhaitez spécifier une valeur d'un type différent.</span><span class="sxs-lookup"><span data-stu-id="84f88-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span></span> <span data-ttu-id="84f88-123">Si vous spécifiez **Non défini**, la variable est définie avec la valeur **$null**, et vous devez définir la valeur avec l’applet de commande [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) ou l’activité **Set-AutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="84f88-123">If you specify **Not defined**, then the value of the variable will be set to **$null**, and you must set the value with the [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="84f88-124">Vous ne pouvez pas créer ou modifier la valeur d'un type de variable complexe dans le portail, mais vous pouvez fournir une valeur de tout type à l'aide de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84f88-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="84f88-125">Les types complexes sont retournés en tant que [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="84f88-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="84f88-126">Vous pouvez stocker plusieurs valeurs dans une seule variable en créant un tableau ou une table de hachage, et en l'enregistrant sur la variable.</span><span class="sxs-lookup"><span data-stu-id="84f88-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span></span>

<span data-ttu-id="84f88-127">Voici la liste des types de variable disponibles dans Automation :</span><span class="sxs-lookup"><span data-stu-id="84f88-127">The following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="84f88-128">String</span><span class="sxs-lookup"><span data-stu-id="84f88-128">String</span></span>
* <span data-ttu-id="84f88-129">Entier </span><span class="sxs-lookup"><span data-stu-id="84f88-129">Integer</span></span>
* <span data-ttu-id="84f88-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="84f88-130">DateTime</span></span>
* <span data-ttu-id="84f88-131">Booléen</span><span class="sxs-lookup"><span data-stu-id="84f88-131">Boolean</span></span>
* <span data-ttu-id="84f88-132">Null</span><span class="sxs-lookup"><span data-stu-id="84f88-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="84f88-133">Applets de commande et activités de workflow</span><span class="sxs-lookup"><span data-stu-id="84f88-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="84f88-134">Les applets de commande du tableau suivant permettent de créer et de gérer les variables Automation avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84f88-134">The cmdlets in the following table are used to create and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="84f88-135">Elles sont fournies dans le cadre du [module Azure PowerShell](../powershell-install-configure.md) , utilisable dans les Runbooks Automation et les configurations DSC.</span><span class="sxs-lookup"><span data-stu-id="84f88-135">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="84f88-136">Applets de commande</span><span class="sxs-lookup"><span data-stu-id="84f88-136">Cmdlets</span></span>|<span data-ttu-id="84f88-137">Description</span><span class="sxs-lookup"><span data-stu-id="84f88-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="84f88-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="84f88-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="84f88-139">Récupère la valeur d'une variable existante.</span><span class="sxs-lookup"><span data-stu-id="84f88-139">Retrieves the value of an existing variable.</span></span>|
|[<span data-ttu-id="84f88-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="84f88-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="84f88-141">Crée une variable et définit sa valeur.</span><span class="sxs-lookup"><span data-stu-id="84f88-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="84f88-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="84f88-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="84f88-143">Supprime une variable existante.</span><span class="sxs-lookup"><span data-stu-id="84f88-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="84f88-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="84f88-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="84f88-145">Définit la valeur d'une variable existante.</span><span class="sxs-lookup"><span data-stu-id="84f88-145">Sets the value for an existing variable.</span></span>|

<span data-ttu-id="84f88-146">Les activités de workflow du tableau suivant sont utilisées pour accéder aux variables Automation d'un Runbook.</span><span class="sxs-lookup"><span data-stu-id="84f88-146">The workflow activities in the following table are used to access Automation variables in a runbook.</span></span> <span data-ttu-id="84f88-147">Elles sont uniquement disponibles pour être utilisées dans un Runbook ou une configuration DSC et ne sont pas fournies dans le cadre du module Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84f88-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of the Azure PowerShell module.</span></span>

|<span data-ttu-id="84f88-148">Activités de workflow</span><span class="sxs-lookup"><span data-stu-id="84f88-148">Workflow Activities</span></span>|<span data-ttu-id="84f88-149">Description</span><span class="sxs-lookup"><span data-stu-id="84f88-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="84f88-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="84f88-150">Get-AutomationVariable</span></span>|<span data-ttu-id="84f88-151">Récupère la valeur d'une variable existante.</span><span class="sxs-lookup"><span data-stu-id="84f88-151">Retrieves the value of an existing variable.</span></span>|
|<span data-ttu-id="84f88-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="84f88-152">Set-AutomationVariable</span></span>|<span data-ttu-id="84f88-153">Définit la valeur d'une variable existante.</span><span class="sxs-lookup"><span data-stu-id="84f88-153">Sets the value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="84f88-154">Évitez d’utiliser des variables dans le paramètre –Name de **Get-AutomationVariable** dans un Runbook ou une configuration DSC, car cela peut compliquer la découverte de dépendances entre les Runbooks ou la configuration DSC et les variables Automation au moment de la conception.</span><span class="sxs-lookup"><span data-stu-id="84f88-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="84f88-155">Création d'une variable Automation</span><span class="sxs-lookup"><span data-stu-id="84f88-155">Creating a new Automation variable</span></span>

### <a name="to-create-a-new-variable-with-the-azure-portal"></a><span data-ttu-id="84f88-156">Création d'une variable avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="84f88-156">To create a new variable with the Azure portal</span></span>

1. <span data-ttu-id="84f88-157">À partir de votre compte Automation, cliquez sur la vignette **Ressources** puis, dans le panneau **Ressources**, sélectionnez **Variables**.</span><span class="sxs-lookup"><span data-stu-id="84f88-157">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="84f88-158">Sur la vignette **Variables**, sélectionnez **Ajouter une variable**.</span><span class="sxs-lookup"><span data-stu-id="84f88-158">On the **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="84f88-159">Définissez les options dans le panneau **Nouvelle variable** et cliquez sur **Créer** pour enregistrer la nouvelle variable.</span><span class="sxs-lookup"><span data-stu-id="84f88-159">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span></span>

### <a name="to-create-a-new-variable-with-windows-powershell"></a><span data-ttu-id="84f88-160">Pour créer une variable avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="84f88-160">To create a new variable with Windows PowerShell</span></span>

<span data-ttu-id="84f88-161">L’applet de commande [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) crée une variable et définit sa valeur initiale.</span><span class="sxs-lookup"><span data-stu-id="84f88-161">The [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="84f88-162">Vous pouvez récupérer la valeur en utilisant [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="84f88-162">You can retrieve the value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="84f88-163">Si la valeur est un type simple, ce même type est retourné.</span><span class="sxs-lookup"><span data-stu-id="84f88-163">If the value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="84f88-164">S'il s'agit d'un type complexe, un **PSCustomObject** est retourné.</span><span class="sxs-lookup"><span data-stu-id="84f88-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="84f88-165">Les exemples de commandes suivants montrent comment créer une variable de type chaîne, puis retourner sa valeur.</span><span class="sxs-lookup"><span data-stu-id="84f88-165">The following sample commands show how to create a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="84f88-166">Les exemples de commandes suivants montrent comment créer une variable de type complexe, puis retourner ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="84f88-166">The following sample commands show how to create a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="84f88-167">Dans ce cas, une machine virtuelle à partir de **Get-AzureRmVm** est utilisée.</span><span class="sxs-lookup"><span data-stu-id="84f88-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="84f88-168">Utilisation d’une variable dans un Runbook ou une configuration DSC</span><span class="sxs-lookup"><span data-stu-id="84f88-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="84f88-169">Utilisez l’activité **Set-AutomationVariable** qui permet de définir la valeur d’une variable Automation dans un Runbook ou dans une configuration DSC, et l’activité **Get-AutomationVariable** pour la récupérer.</span><span class="sxs-lookup"><span data-stu-id="84f88-169">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span></span>  <span data-ttu-id="84f88-170">Vous ne devez pas utiliser les applets de commande **Set-AzureAutomationVariable** ou **Get-AzureAutomationVariable** dans un Runbook ou dans une configuration DSC, car elles sont moins efficaces que les activités de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="84f88-170">You shouldn't use the **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span></span>  <span data-ttu-id="84f88-171">Vous ne pouvez pas non plus récupérer la valeur de variables sécurisées avec **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="84f88-171">You also cannot retrieve the value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="84f88-172">La seule façon de créer une variable à partir d’un Runbook ou d’une configuration DSC consiste à utiliser l’applet de commande [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx).</span><span class="sxs-lookup"><span data-stu-id="84f88-172">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="84f88-173">Exemple de Runbooks textuels</span><span class="sxs-lookup"><span data-stu-id="84f88-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="84f88-174">Définition et récupération d'une valeur simple à partir d'une variable</span><span class="sxs-lookup"><span data-stu-id="84f88-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="84f88-175">Les exemples de commandes suivants montrent comment définir et récupérer une variable dans un Runbook textuel.</span><span class="sxs-lookup"><span data-stu-id="84f88-175">The following sample commands show how to set and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="84f88-176">Dans cet exemple, il est supposé que les variables de type entier nommées *NumberOfIterations* et *NumberOfRunnings* et une variable de type chaîne nommée *SampleMessage* ont déjà été créées.</span><span class="sxs-lookup"><span data-stu-id="84f88-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="84f88-177">Définition et récupération d'un objet complexe dans une variable</span><span class="sxs-lookup"><span data-stu-id="84f88-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="84f88-178">L'exemple de code suivant montre comment mettre à jour une variable avec une valeur complexe dans un Runbook textuel.</span><span class="sxs-lookup"><span data-stu-id="84f88-178">The following sample code shows how to update a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="84f88-179">Dans cet exemple, une machine virtuelle Azure est récupérée avec **Get-AzureVM** et enregistrée dans une variable Automation existante.</span><span class="sxs-lookup"><span data-stu-id="84f88-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="84f88-180">Comme expliqué dans [Types de variables](#variable-types), il est stocké comme PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="84f88-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="84f88-181">Dans le code suivant, la valeur est extraite de la variable et utilisée pour démarrer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84f88-181">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="84f88-182">Définition et récupération d'une collection dans une variable</span><span class="sxs-lookup"><span data-stu-id="84f88-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="84f88-183">L'exemple de code suivant montre comment utiliser une variable avec une collection de valeurs complexes dans un Runbook textuel.</span><span class="sxs-lookup"><span data-stu-id="84f88-183">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="84f88-184">Dans cet exemple, plusieurs machines virtuelles Azure sont récupérées avec **Get-AzureVM** et enregistrées dans une variable Automation existante.</span><span class="sxs-lookup"><span data-stu-id="84f88-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="84f88-185">Comme expliqué dans [Types de variables](#variable-types), elles sont stockées comme collection de PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="84f88-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="84f88-186">Dans le code suivant, la valeur est extraite de la variable et utilisée pour démarrer chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84f88-186">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="84f88-187">Exemples de Runbook graphiques</span><span class="sxs-lookup"><span data-stu-id="84f88-187">Graphical runbook samples</span></span>

<span data-ttu-id="84f88-188">Dans un Runbook graphique, ajoutez l’activité **Get-AutomationVariable** ou **Set-AutomationVariable** en cliquant avec le bouton droit sur la variable dans le volet Bibliothèque de l’éditeur graphique et en sélectionnant l’activité souhaitée.</span><span class="sxs-lookup"><span data-stu-id="84f88-188">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span></span>

![Ajouter une variable à la zone de dessin](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="84f88-190">Définition de valeurs dans une variable</span><span class="sxs-lookup"><span data-stu-id="84f88-190">Setting values in a variable</span></span>
<span data-ttu-id="84f88-191">L'image suivante montre des exemples d'activité pour mettre à jour une variable avec une valeur simple dans un Runbook graphique.</span><span class="sxs-lookup"><span data-stu-id="84f88-191">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="84f88-192">Dans cet exemple, une seule machine virtuelle Azure est récupérée avec **Get-AzureRmVM**, et le nom d’ordinateur est enregistré dans une variable Automation existante avec le type String.</span><span class="sxs-lookup"><span data-stu-id="84f88-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span></span>  <span data-ttu-id="84f88-193">Peu importe si les [lien est un pipeline ou une séquence](automation-graphical-authoring-intro.md#links-and-workflow) , car nous attendons uniquement un objet unique dans la sortie.</span><span class="sxs-lookup"><span data-stu-id="84f88-193">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in the output.</span></span>

![Définir une variable simple](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="84f88-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84f88-195">Next Steps</span></span>

* <span data-ttu-id="84f88-196">Pour en savoir plus sur la connexion d’activités lors de la création graphique, consultez [Liens lors de la création graphique](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="84f88-196">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="84f88-197">Pour une prise en main des Runbooks graphiques, consultez [Mon premier Runbook graphique](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="84f88-197">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

