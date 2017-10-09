---
title: "aaaPass JSON de l’objet runbook Azure Automation de tooan | Documents Microsoft"
description: "Comment toopass paramètres tooa runbook en tant qu’objet JSON"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powerShell, runbook, json, azure automation
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="329e9-104">Passer d’un runbook Azure Automation de JSON objet tooan</span><span class="sxs-lookup"><span data-stu-id="329e9-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="329e9-105">Il peut être utile toostore les données que vous souhaitez runbook de tooa toopass dans un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="329e9-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="329e9-106">Par exemple, vous pouvez créer un fichier JSON qui contient tous les paramètres de hello souhaité toopass tooa runbook.</span><span class="sxs-lookup"><span data-stu-id="329e9-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="329e9-107">toodo, vous avez tooconvert hello JSON tooa chaîne, puis la convertir objet PowerShell de hello chaîne tooa avant de les transmettre ses runbook toohello de contenu.</span><span class="sxs-lookup"><span data-stu-id="329e9-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="329e9-108">Dans cet exemple, nous allons créer un script PowerShell qui appelle [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook PowerShell, en passant le contenu hello de hello JSON toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="329e9-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="329e9-109">Hello PowerShell runbook démarre une machine virtuelle Azure, récupération des paramètres de hello hello machine virtuelle à partir de hello JSON qui a été passé.</span><span class="sxs-lookup"><span data-stu-id="329e9-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="329e9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="329e9-110">Prerequisites</span></span>
<span data-ttu-id="329e9-111">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="329e9-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="329e9-112">Abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="329e9-112">Azure subscription.</span></span> <span data-ttu-id="329e9-113">Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[créer un compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="329e9-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="329e9-114">[Compte Automation](automation-sec-configure-azure-runas-account.md) toohold hello runbook et authentifier les ressources tooAzure.</span><span class="sxs-lookup"><span data-stu-id="329e9-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="329e9-115">Ce compte doit avoir l’autorisation toostart et arrêter l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="329e9-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="329e9-116">Une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="329e9-116">An Azure virtual machine.</span></span> <span data-ttu-id="329e9-117">Nous arrêtons et démarrons cette machine afin qu’elle ne soit pas une machine virtuelle de production.</span><span class="sxs-lookup"><span data-stu-id="329e9-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="329e9-118">Azure Powershell installé sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="329e9-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="329e9-119">Consultez [installer et configurer Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) pour plus d’informations sur la façon tooget Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="329e9-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="329e9-120">Créer le fichier JSON de hello</span><span class="sxs-lookup"><span data-stu-id="329e9-120">Create hello JSON file</span></span>

<span data-ttu-id="329e9-121">Tapez ce qui suit hello test dans un fichier texte et enregistrez-le sous `test.json` quelque part sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="329e9-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="329e9-122">Créer des runbook de hello</span><span class="sxs-lookup"><span data-stu-id="329e9-122">Create hello runbook</span></span>

<span data-ttu-id="329e9-123">Créer un nouveau runbook PowerShell nommé « Test-Json » dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="329e9-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="329e9-124">toolearn toocreate un runbook PowerShell, voir [mon runbook PowerShell premier](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="329e9-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="329e9-125">des données JSON tooaccept hello, hello runbook doit prendre un objet comme paramètre d’entrée.</span><span class="sxs-lookup"><span data-stu-id="329e9-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="329e9-126">Hello runbook peut ensuite utiliser les propriétés de hello définies dans hello JSON.</span><span class="sxs-lookup"><span data-stu-id="329e9-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="329e9-127">Enregistrez et publiez ce runbook dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="329e9-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="329e9-128">Appelez hello runbook à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="329e9-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="329e9-129">Vous pouvez maintenant appeler hello runbook à partir de votre ordinateur local à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="329e9-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="329e9-130">Exécutez hello suivant de commandes PowerShell :</span><span class="sxs-lookup"><span data-stu-id="329e9-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="329e9-131">Ouvrez une session dans tooAzure :</span><span class="sxs-lookup"><span data-stu-id="329e9-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="329e9-132">Vous est demandée tooenter vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="329e9-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="329e9-133">Obtenir le contenu de hello du fichier JSON de hello et convertissez-le en tooa chaîne :</span><span class="sxs-lookup"><span data-stu-id="329e9-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="329e9-134">`JsonPath`est le chemin d’accès hello où vous avez enregistré le fichier JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="329e9-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="329e9-135">Convertir le contenu de la chaîne hello de `$json` tooa PowerShell objet :</span><span class="sxs-lookup"><span data-stu-id="329e9-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="329e9-136">Créer une table de hachage pour les paramètres de hello pour `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="329e9-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="329e9-137">Notez que vous définissez la valeur hello `Parameters` toohello PowerShell objet qui contient les valeurs hello à partir du fichier JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="329e9-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="329e9-138">Démarrer hello runbook</span><span class="sxs-lookup"><span data-stu-id="329e9-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="329e9-139">Hello runbook utilise des valeurs de hello de hello JSON fichier toostart une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="329e9-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="329e9-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="329e9-140">Next steps</span></span>

* <span data-ttu-id="329e9-141">toolearn en savoir plus sur la modification des procédures opérationnelles PowerShell et les flux de travail PowerShell avec un éditeur de texte, consultez [modification textuelles runbooks dans Azure Automation](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="329e9-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="329e9-142">toolearn en savoir plus sur la création et importation de runbooks, consultez [création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="329e9-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


