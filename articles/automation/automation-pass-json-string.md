---
title: "Passer un objet JSON dans un runbook Azure Automation | Documents Microsoft"
description: "Comment passer des paramètres dans un runbook en tant qu’objet JSON"
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
ms.openlocfilehash: eac0e95a46731b9d396ea0590e629d61ca6a7d70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a><span data-ttu-id="21df6-104">Passer un objet JSON dans un runbook Azure Automation</span><span class="sxs-lookup"><span data-stu-id="21df6-104">Pass a JSON object to an Azure Automation runbook</span></span>

<span data-ttu-id="21df6-105">Il peut être utile stocker les données à passer dans un runbook dans un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="21df6-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span></span>
<span data-ttu-id="21df6-106">Par exemple, vous pouvez créer un fichier JSON qui contient tous les paramètres que vous souhaitez passer dans un runbook.</span><span class="sxs-lookup"><span data-stu-id="21df6-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span></span>
<span data-ttu-id="21df6-107">Pour ce faire, vous devez convertir le fichier JSON en une chaîne, puis convertir la chaîne en un objet PowerShell avant de passer son contenu dans le runbook.</span><span class="sxs-lookup"><span data-stu-id="21df6-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span></span>

<span data-ttu-id="21df6-108">Dans cet exemple, nous allons créer un script PowerShell qui appelle [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) pour démarrer un runbook PowerShell, en passant le contenu de l’objet JSON dans le runbook.</span><span class="sxs-lookup"><span data-stu-id="21df6-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span></span>
<span data-ttu-id="21df6-109">Le runbook PowerShell démarre une machine virtuelle Azure, en obtenant les paramètres pour la machine virtuelle à partir de l’objet JSON qui a été passé.</span><span class="sxs-lookup"><span data-stu-id="21df6-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21df6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="21df6-110">Prerequisites</span></span>
<span data-ttu-id="21df6-111">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="21df6-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="21df6-112">Abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="21df6-112">Azure subscription.</span></span> <span data-ttu-id="21df6-113">Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[créer un compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="21df6-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="21df6-114">[compte Automation](automation-sec-configure-azure-runas-account.md) pour le stockage du Runbook et l’authentification auprès des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="21df6-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="21df6-115">Ce compte doit avoir l’autorisation de démarrer et d’arrêter la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21df6-115">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="21df6-116">Une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="21df6-116">An Azure virtual machine.</span></span> <span data-ttu-id="21df6-117">Nous arrêtons et démarrons cette machine afin qu’elle ne soit pas une machine virtuelle de production.</span><span class="sxs-lookup"><span data-stu-id="21df6-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="21df6-118">Azure Powershell installé sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="21df6-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="21df6-119">Pour plus d'informations sur l’obtention d’Azure PowerShell, consultez la section [Installation et configuration d'Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="21df6-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-json-file"></a><span data-ttu-id="21df6-120">Créer le fichier JSON</span><span class="sxs-lookup"><span data-stu-id="21df6-120">Create the JSON file</span></span>

<span data-ttu-id="21df6-121">Tapez le test suivant dans un fichier texte et enregistrez-le sous `test.json` quelque part sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="21df6-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a><span data-ttu-id="21df6-122">Créer le runbook</span><span class="sxs-lookup"><span data-stu-id="21df6-122">Create the runbook</span></span>

<span data-ttu-id="21df6-123">Créer un nouveau runbook PowerShell nommé « Test-Json » dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="21df6-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="21df6-124">Pour savoir comment créer un nouveau runbook PowerShell, consultez [Mon premier runbook PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="21df6-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="21df6-125">Pour accepter les données JSON, le runbook doit prendre un objet comme paramètre d’entrée.</span><span class="sxs-lookup"><span data-stu-id="21df6-125">To accept the JSON data, the runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="21df6-126">Le runbook peut utiliser ensuite les propriétés définies dans le JSON.</span><span class="sxs-lookup"><span data-stu-id="21df6-126">The runbook can then use the properties defined in the JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="21df6-127">Enregistrez et publiez ce runbook dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="21df6-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-the-runbook-from-powershell"></a><span data-ttu-id="21df6-128">Appeler le runbook à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="21df6-128">Call the runbook from PowerShell</span></span>

<span data-ttu-id="21df6-129">Vous pouvez maintenant appeler le runbook à partir de votre ordinateur local à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21df6-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="21df6-130">Lancer les commandes PowerShell suivantes :</span><span class="sxs-lookup"><span data-stu-id="21df6-130">Run the following PowerShell commands:</span></span>

1. <span data-ttu-id="21df6-131">Connexion à Azure :</span><span class="sxs-lookup"><span data-stu-id="21df6-131">Log in to Azure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="21df6-132">Vous êtes invité à entrer vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="21df6-132">You are prompted to enter your Azure credentials.</span></span>
1. <span data-ttu-id="21df6-133">Obtenir le contenu du fichier JSON et les convertir en une chaîne :</span><span class="sxs-lookup"><span data-stu-id="21df6-133">Get the contents of the JSON file and convert it to a string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="21df6-134">`JsonPath` est le chemin d’accès où vous avez enregistré le fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="21df6-134">`JsonPath` is the path where you saved the JSON file.</span></span>
1. <span data-ttu-id="21df6-135">Convertir le contenu de la chaîne de `$json` dans un objet PowerShell :</span><span class="sxs-lookup"><span data-stu-id="21df6-135">Convert the string contents of `$json` to a PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="21df6-136">Créer une table de hachage pour les paramètres pour `Start-AzureRmAutomstionRunbook` :</span><span class="sxs-lookup"><span data-stu-id="21df6-136">Create a hashtable for the parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="21df6-137">Notez que vous définissez la valeur de `Parameters` sur l’objet PowerShell qui contient les valeurs à partir du fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="21df6-137">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span></span> 
1. <span data-ttu-id="21df6-138">Démarrer le runbook</span><span class="sxs-lookup"><span data-stu-id="21df6-138">Start the runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="21df6-139">Le runbook utilise les valeurs du fichier JSON pour démarrer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21df6-139">The runbook uses the values from the JSON file to start a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21df6-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21df6-140">Next steps</span></span>

* <span data-ttu-id="21df6-141">Pour en savoir plus sur la modification des runbooks PowerShell et de workflow PowerShell avec un éditeur de texte, consultez [Modifier des runbooks textuels dans Azure Automation](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="21df6-141">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="21df6-142">Pour savoir comment créer et importer des runbooks, consultez [Création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="21df6-142">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


