---
title: ressources aaaVariable dans Azure Automation | Documents Microsoft
description: "Les ressources de variables sont des valeurs qui sont disponibles tooall runbooks et les configurations DSC dans Azure Automation.  Cet article explique les détails de hello de variables et la manière dont toowork avec eux dans textuels et graphiques de création."
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
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="321d4-104">Ressources de variables dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="321d4-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="321d4-105">Les ressources de variables sont des valeurs qui sont disponibles tooall runbooks et les configurations DSC dans votre compte automation.</span><span class="sxs-lookup"><span data-stu-id="321d4-105">Variable assets are values that are available tooall runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="321d4-106">Ils peuvent être créés, modifiés et récupérées à partir de hello portail Azure, Windows PowerShell et à partir d’un runbook ou la configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="321d4-106">They can be created, modified, and retrieved from hello Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="321d4-107">Les variables Automation sont utiles pour hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="321d4-107">Automation variables are useful for hello following scenarios:</span></span>

- <span data-ttu-id="321d4-108">Partager une valeur entre plusieurs Runbooks ou configurations DSC.</span><span class="sxs-lookup"><span data-stu-id="321d4-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="321d4-109">Partager une valeur entre plusieurs travaux hello même runbook ou la configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="321d4-109">Share a value between multiple jobs from hello same runbook or DSC configuration.</span></span>

- <span data-ttu-id="321d4-110">Gérer une valeur à partir du portail de hello ou à partir de la ligne de commande Windows PowerShell hello qui est utilisé par les procédures opérationnelles ou les configurations DSC, comme un ensemble commun d’éléments de configuration comme liste de noms de machine virtuelle, un groupe de ressources spécifique, nom de domaine Active Directory, etc..</span><span class="sxs-lookup"><span data-stu-id="321d4-110">Manage a value from hello portal or from hello Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="321d4-111">Variables Automation sont conservées afin qu’ils continuent toobe disponible même en cas de hello runbook ou la configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="321d4-111">Automation variables are persisted so that they continue toobe available even if hello runbook or DSC configuration fails.</span></span>  <span data-ttu-id="321d4-112">Cela permet également à un toobe de valeur définie par un runbook qui est ensuite utilisé par un autre, ou qui est utilisé par hello même runbook ou hello de configuration DSC prochaine fois qu’elle est exécutée.</span><span class="sxs-lookup"><span data-stu-id="321d4-112">This also allows a value toobe set by one runbook that is then used by another, or is used by hello same runbook or DSC configuration hello next time that it is run.</span></span>

<span data-ttu-id="321d4-113">Quand une variable est créée, vous pouvez spécifier qu'elle doit être stockée de manière chiffrée.</span><span class="sxs-lookup"><span data-stu-id="321d4-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="321d4-114">Lorsqu’une variable est chiffrée, il est stocké en toute sécurité dans Azure Automation, et sa valeur ne peut pas être récupérée à partir de hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) applet de commande qui est fourni en tant que partie du module Azure PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="321d4-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of hello Azure PowerShell module.</span></span>  <span data-ttu-id="321d4-115">Hello uniquement une valeur chiffrée peut être récupérée que consiste à partir de hello **Get-AutomationVariable** activité dans un runbook ou la configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="321d4-115">hello only way that an encrypted value can be retrieved is from hello **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="321d4-116">Les ressources sécurisées dans Azure Automation incluent les informations d'identification, les certificats, les connexions et les variables chiffrées.</span><span class="sxs-lookup"><span data-stu-id="321d4-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="321d4-117">Ces ressources sont chiffrées et stockées Bonjour Azure Automation à l’aide d’une clé unique qui est générée pour chaque compte automation.</span><span class="sxs-lookup"><span data-stu-id="321d4-117">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="321d4-118">Cette clé est chiffrée par un certificat principal et stockée dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="321d4-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="321d4-119">Avant de stocker une ressource sécurisée, clé hello pour le compte d’automatisation hello est déchiffré à l’aide du certificat master de hello, puis utilisé asset de hello tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="321d4-119">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="321d4-120">Types de variables</span><span class="sxs-lookup"><span data-stu-id="321d4-120">Variable types</span></span>

<span data-ttu-id="321d4-121">Lorsque vous créez une variable avec hello portail Azure, vous devez spécifier un type de données à partir de la liste déroulante de hello pour le portail de hello peut afficher le contrôle approprié de hello pour entrer la valeur de la variable hello.</span><span class="sxs-lookup"><span data-stu-id="321d4-121">When you create a variable with hello Azure portal, you must specify a data type from hello drop-down list so hello portal can display hello appropriate control for entering hello variable value.</span></span> <span data-ttu-id="321d4-122">variable de Hello n’est pas restreinte toothis données type, mais vous devez définir variable hello à l’aide de Windows PowerShell si vous souhaitez toospecify une valeur d’un type différent.</span><span class="sxs-lookup"><span data-stu-id="321d4-122">hello variable is not restricted toothis data type, but you must set hello variable using Windows PowerShell if you want toospecify a value of a different type.</span></span> <span data-ttu-id="321d4-123">Si vous spécifiez **non défini**, puis hello la valeur de variable de hello sera définie trop**$null**, et vous devez affecter la valeur hello avec hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) applet de commande ou **Set-AutomationVariable** activité.</span><span class="sxs-lookup"><span data-stu-id="321d4-123">If you specify **Not defined**, then hello value of hello variable will be set too**$null**, and you must set hello value with hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="321d4-124">Impossible de créer ou de modifier la valeur hello pour un type de variable complexe dans le portail de hello, mais vous pouvez fournir une valeur de tout type à l’aide de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="321d4-124">You cannot create or change hello value for a complex variable type in hello portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="321d4-125">Les types complexes sont retournés en tant que [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="321d4-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="321d4-126">Vous pouvez stocker plusieurs variable unique tooa de valeurs en créant un tableau ou une table de hachage et de l’enregistrement de toohello variable.</span><span class="sxs-lookup"><span data-stu-id="321d4-126">You can store multiple values tooa single variable by creating an array or hashtable and saving it toohello variable.</span></span>

<span data-ttu-id="321d4-127">Hello Voici une liste des types de variables disponibles dans Automation :</span><span class="sxs-lookup"><span data-stu-id="321d4-127">hello following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="321d4-128">String</span><span class="sxs-lookup"><span data-stu-id="321d4-128">String</span></span>
* <span data-ttu-id="321d4-129">Entier </span><span class="sxs-lookup"><span data-stu-id="321d4-129">Integer</span></span>
* <span data-ttu-id="321d4-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="321d4-130">DateTime</span></span>
* <span data-ttu-id="321d4-131">Booléen</span><span class="sxs-lookup"><span data-stu-id="321d4-131">Boolean</span></span>
* <span data-ttu-id="321d4-132">Null</span><span class="sxs-lookup"><span data-stu-id="321d4-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="321d4-133">Applets de commande et activités de workflow</span><span class="sxs-lookup"><span data-stu-id="321d4-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="321d4-134">applets de commande Hello Bonjour tableau suivant sont utilisée toocreate et gérer les variables Automation avec Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="321d4-134">hello cmdlets in hello following table are used toocreate and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="321d4-135">Elles font partie de hello [module Azure PowerShell](../powershell-install-configure.md) qui est disponible pour une utilisation dans les runbooks d’automatisation et de configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="321d4-135">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="321d4-136">Applets de commande</span><span class="sxs-lookup"><span data-stu-id="321d4-136">Cmdlets</span></span>|<span data-ttu-id="321d4-137">Description</span><span class="sxs-lookup"><span data-stu-id="321d4-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="321d4-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="321d4-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="321d4-139">Récupère la valeur hello d’une variable existante.</span><span class="sxs-lookup"><span data-stu-id="321d4-139">Retrieves hello value of an existing variable.</span></span>|
|[<span data-ttu-id="321d4-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="321d4-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="321d4-141">Crée une variable et définit sa valeur.</span><span class="sxs-lookup"><span data-stu-id="321d4-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="321d4-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="321d4-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="321d4-143">Supprime une variable existante.</span><span class="sxs-lookup"><span data-stu-id="321d4-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="321d4-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="321d4-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="321d4-145">Définit la valeur hello d’une variable existante.</span><span class="sxs-lookup"><span data-stu-id="321d4-145">Sets hello value for an existing variable.</span></span>|

<span data-ttu-id="321d4-146">activités de flux de travail Hello Bonjour tableau suivant sont utilisées tooaccess variables Automation dans un runbook.</span><span class="sxs-lookup"><span data-stu-id="321d4-146">hello workflow activities in hello following table are used tooaccess Automation variables in a runbook.</span></span> <span data-ttu-id="321d4-147">Ils sont uniquement disponibles pour une utilisation dans un runbook ou la configuration DSC et ne sont pas fournis dans le cadre du module Azure PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="321d4-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of hello Azure PowerShell module.</span></span>

|<span data-ttu-id="321d4-148">Activités de workflow</span><span class="sxs-lookup"><span data-stu-id="321d4-148">Workflow Activities</span></span>|<span data-ttu-id="321d4-149">Description</span><span class="sxs-lookup"><span data-stu-id="321d4-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="321d4-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="321d4-150">Get-AutomationVariable</span></span>|<span data-ttu-id="321d4-151">Récupère la valeur hello d’une variable existante.</span><span class="sxs-lookup"><span data-stu-id="321d4-151">Retrieves hello value of an existing variable.</span></span>|
|<span data-ttu-id="321d4-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="321d4-152">Set-AutomationVariable</span></span>|<span data-ttu-id="321d4-153">Définit la valeur hello d’une variable existante.</span><span class="sxs-lookup"><span data-stu-id="321d4-153">Sets hello value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="321d4-154">Vous devez éviter d’utiliser des variables dans hello : paramètre de nom de **Get-AutomationVariable** dans un runbook ou la configuration DSC, car cela complique la découverte des dépendances entre les procédures opérationnelles ou d’automatisation et de configuration DSC variables au moment du design.</span><span class="sxs-lookup"><span data-stu-id="321d4-154">You should avoid using variables in hello –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="321d4-155">Création d'une variable Automation</span><span class="sxs-lookup"><span data-stu-id="321d4-155">Creating a new Automation variable</span></span>

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a><span data-ttu-id="321d4-156">toocreate une nouvelle variable avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="321d4-156">toocreate a new variable with hello Azure portal</span></span>

1. <span data-ttu-id="321d4-157">À partir de votre compte Automation, cliquez sur hello **actifs** vignette et puis sur hello **actifs** panneau, sélectionnez **Variables**.</span><span class="sxs-lookup"><span data-stu-id="321d4-157">From your Automation account, click hello **Assets** tile and then on hello **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="321d4-158">Sur hello **Variables** vignette, sélectionnez **ajouter une variable**.</span><span class="sxs-lookup"><span data-stu-id="321d4-158">On hello **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="321d4-159">Choisissez les options de hello sur hello **nouvelle Variable** panneau, cliquez sur **créer** enregistrer hello nouvelle variable.</span><span class="sxs-lookup"><span data-stu-id="321d4-159">Complete hello options on hello **New Variable** blade and click **Create** save hello new variable.</span></span>

### <a name="toocreate-a-new-variable-with-windows-powershell"></a><span data-ttu-id="321d4-160">toocreate une nouvelle variable avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="321d4-160">toocreate a new variable with Windows PowerShell</span></span>

<span data-ttu-id="321d4-161">Hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) applet de commande crée une variable et définit sa valeur initiale.</span><span class="sxs-lookup"><span data-stu-id="321d4-161">hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="321d4-162">Vous pouvez récupérer à l’aide de valeur hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="321d4-162">You can retrieve hello value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="321d4-163">Si la valeur de hello est un type simple, ce même type est retourné.</span><span class="sxs-lookup"><span data-stu-id="321d4-163">If hello value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="321d4-164">S'il s'agit d'un type complexe, un **PSCustomObject** est retourné.</span><span class="sxs-lookup"><span data-stu-id="321d4-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="321d4-165">exemple de Hello suivant commandes indiquent comment toocreate une variable de type chaîne et puis de retourner sa valeur.</span><span class="sxs-lookup"><span data-stu-id="321d4-165">hello following sample commands show how toocreate a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="321d4-166">exemple de Hello suivant commandes indiquent comment toocreate une variable avec un type complexe de type, puis retourner ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="321d4-166">hello following sample commands show how toocreate a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="321d4-167">Dans ce cas, une machine virtuelle à partir de **Get-AzureRmVm** est utilisée.</span><span class="sxs-lookup"><span data-stu-id="321d4-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="321d4-168">Utilisation d’une variable dans un Runbook ou une configuration DSC</span><span class="sxs-lookup"><span data-stu-id="321d4-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="321d4-169">Hello d’utilisation **Set-AutomationVariable** valeur hello de tooset l’activité d’une variable Automation dans un runbook ou la configuration DSC et le hello **Get-AutomationVariable** tooretrieve il.</span><span class="sxs-lookup"><span data-stu-id="321d4-169">Use hello **Set-AutomationVariable** activity tooset hello value of an Automation variable in a runbook or DSC configuration, and hello **Get-AutomationVariable** tooretrieve it.</span></span>  <span data-ttu-id="321d4-170">Vous ne devez pas utiliser hello **Set-AzureAutomationVariable** ou **Get-AzureAutomationVariable** applets de commande dans un runbook ou la configuration DSC, car elles sont moins efficaces que les activités de flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="321d4-170">You shouldn't use hello **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than hello workflow activities.</span></span>  <span data-ttu-id="321d4-171">Vous ne peut pas également récupérer la valeur hello de variables sécurisées avec **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="321d4-171">You also cannot retrieve hello value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="321d4-172">Hello uniquement moyen toocreate une variable à partir d’un runbook ou la configuration DSC est toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="321d4-172">hello only way toocreate a new variable from within a runbook or DSC configuration is toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="321d4-173">Exemple de Runbooks textuels</span><span class="sxs-lookup"><span data-stu-id="321d4-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="321d4-174">Définition et récupération d'une valeur simple à partir d'une variable</span><span class="sxs-lookup"><span data-stu-id="321d4-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="321d4-175">exemple de Hello suivant commandes indiquent comment tooset et récupérer une variable dans un runbook textuelle.</span><span class="sxs-lookup"><span data-stu-id="321d4-175">hello following sample commands show how tooset and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="321d4-176">Dans cet exemple, il est supposé que les variables de type entier nommées *NumberOfIterations* et *NumberOfRunnings* et une variable de type chaîne nommée *SampleMessage* ont déjà été créées.</span><span class="sxs-lookup"><span data-stu-id="321d4-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="321d4-177">Définition et récupération d'un objet complexe dans une variable</span><span class="sxs-lookup"><span data-stu-id="321d4-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="321d4-178">exemple de Hello suivant de code montre comment tooupdate une variable avec une valeur complexe dans un runbook textuelle.</span><span class="sxs-lookup"><span data-stu-id="321d4-178">hello following sample code shows how tooupdate a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="321d4-179">Dans cet exemple, une machine virtuelle Azure est récupérée avec **Get-AzureVM** et tooan enregistré les variable Automation existante.</span><span class="sxs-lookup"><span data-stu-id="321d4-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="321d4-180">Comme expliqué dans [Types de variables](#variable-types), il est stocké comme PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="321d4-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="321d4-181">Bonjour suivant de code, les valeur de hello est extraite de la machine virtuelle de hello toostart variable et utilisé hello.</span><span class="sxs-lookup"><span data-stu-id="321d4-181">In hello following code, hello value is retrieved from hello variable and used toostart hello virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="321d4-182">Définition et récupération d'une collection dans une variable</span><span class="sxs-lookup"><span data-stu-id="321d4-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="321d4-183">exemple de Hello suivant de code montre comment toouse une variable avec une collection de valeurs complexes dans un runbook textuels.</span><span class="sxs-lookup"><span data-stu-id="321d4-183">hello following sample code shows how toouse a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="321d4-184">Dans cet exemple, plusieurs machines virtuelles Azure sont récupérés avec **Get-AzureVM** et tooan enregistré les variable Automation existante.</span><span class="sxs-lookup"><span data-stu-id="321d4-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="321d4-185">Comme expliqué dans [Types de variables](#variable-types), elles sont stockées comme collection de PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="321d4-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="321d4-186">Bonjour suivant de code, collection de hello est extraite de la variable de hello et utilisé toostart chaque ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="321d4-186">In hello following code, hello collection is retrieved from hello variable and used toostart each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="321d4-187">Exemples de Runbook graphiques</span><span class="sxs-lookup"><span data-stu-id="321d4-187">Graphical runbook samples</span></span>

<span data-ttu-id="321d4-188">Dans un runbook graphique, vous ajoutez hello **Get-AutomationVariable** ou **Set-AutomationVariable** en cliquant sur variable hello dans le volet Bibliothèque de hello de l’éditeur graphique de hello et en sélectionnant hello activité de que votre choix.</span><span class="sxs-lookup"><span data-stu-id="321d4-188">In a graphical runbook, you add hello **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on hello variable in hello Library pane of hello graphical editor and selecting hello activity you want.</span></span>

![Ajoutez la variable toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="321d4-190">Définition de valeurs dans une variable</span><span class="sxs-lookup"><span data-stu-id="321d4-190">Setting values in a variable</span></span>
<span data-ttu-id="321d4-191">Hello image suivante montre exemple activités tooupdate une variable avec une valeur simple dans un runbook graphique.</span><span class="sxs-lookup"><span data-stu-id="321d4-191">hello following image shows sample activities tooupdate a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="321d4-192">Dans cet exemple, une seule machine virtuelle Azure est récupérée avec **Get-AzureRmVM** et nom de l’ordinateur hello est enregistrée variable Automation existante de tooan avec un type de chaîne.</span><span class="sxs-lookup"><span data-stu-id="321d4-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and hello computer name is saved tooan existing Automation variable with a type of String.</span></span>  <span data-ttu-id="321d4-193">Peu importe si hello [lien est un pipeline ou une séquence](automation-graphical-authoring-intro.md#links-and-workflow) étant donné que nous n'espérons qu’un seul objet dans la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="321d4-193">It doesn't matter whether hello [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in hello output.</span></span>

![Définir une variable simple](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="321d4-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="321d4-195">Next Steps</span></span>

* <span data-ttu-id="321d4-196">toolearn en savoir plus sur les reliant les activités de création graphique, consultez [liens dans le graphique de création](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="321d4-196">toolearn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="321d4-197">tooget main runbooks graphiques, consultez [mon premier runbook graphique](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="321d4-197">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

