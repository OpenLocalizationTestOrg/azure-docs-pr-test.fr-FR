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
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a>Passer d’un runbook Azure Automation de JSON objet tooan

Il peut être utile toostore les données que vous souhaitez runbook de tooa toopass dans un fichier JSON.
Par exemple, vous pouvez créer un fichier JSON qui contient tous les paramètres de hello souhaité toopass tooa runbook.
toodo, vous avez tooconvert hello JSON tooa chaîne, puis la convertir objet PowerShell de hello chaîne tooa avant de les transmettre ses runbook toohello de contenu.

Dans cet exemple, nous allons créer un script PowerShell qui appelle [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook PowerShell, en passant le contenu hello de hello JSON toohello runbook.
Hello PowerShell runbook démarre une machine virtuelle Azure, récupération des paramètres de hello hello machine virtuelle à partir de hello JSON qui a été passé.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant :

* Abonnement Azure. Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[créer un compte gratuit](https://azure.microsoft.com/free/).
* [Compte Automation](automation-sec-configure-azure-runas-account.md) toohold hello runbook et authentifier les ressources tooAzure.  Ce compte doit avoir l’autorisation toostart et arrêter l’ordinateur virtuel de hello.
* Une machine virtuelle Azure. Nous arrêtons et démarrons cette machine afin qu’elle ne soit pas une machine virtuelle de production.
* Azure Powershell installé sur un ordinateur local. Consultez [installer et configurer Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) pour plus d’informations sur la façon tooget Azure PowerShell.

## <a name="create-hello-json-file"></a>Créer le fichier JSON de hello

Tapez ce qui suit hello test dans un fichier texte et enregistrez-le sous `test.json` quelque part sur votre ordinateur local.

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a>Créer des runbook de hello

Créer un nouveau runbook PowerShell nommé « Test-Json » dans Azure Automation.
toolearn toocreate un runbook PowerShell, voir [mon runbook PowerShell premier](automation-first-runbook-textual-powershell.md).

des données JSON tooaccept hello, hello runbook doit prendre un objet comme paramètre d’entrée.

Hello runbook peut ensuite utiliser les propriétés de hello définies dans hello JSON.

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

 Enregistrez et publiez ce runbook dans votre compte Automation.

## <a name="call-hello-runbook-from-powershell"></a>Appelez hello runbook à partir de PowerShell

Vous pouvez maintenant appeler hello runbook à partir de votre ordinateur local à l’aide d’Azure PowerShell.
Exécutez hello suivant de commandes PowerShell :

1. Ouvrez une session dans tooAzure :
   ```powershell
   Login-AzureRmAccount
   ```
    Vous est demandée tooenter vos informations d’identification Azure.
1. Obtenir le contenu de hello du fichier JSON de hello et convertissez-le en tooa chaîne :
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`est le chemin d’accès hello où vous avez enregistré le fichier JSON de hello.
1. Convertir le contenu de la chaîne hello de `$json` tooa PowerShell objet :
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. Créer une table de hachage pour les paramètres de hello pour `Start-AzureRmAutomstionRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   Notez que vous définissez la valeur hello `Parameters` toohello PowerShell objet qui contient les valeurs hello à partir du fichier JSON de hello. 
1. Démarrer hello runbook
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

Hello runbook utilise des valeurs de hello de hello JSON fichier toostart une machine virtuelle.

## <a name="next-steps"></a>Étapes suivantes

* toolearn en savoir plus sur la modification des procédures opérationnelles PowerShell et les flux de travail PowerShell avec un éditeur de texte, consultez [modification textuelles runbooks dans Azure Automation](automation-edit-textual-runbook.md) 
* toolearn en savoir plus sur la création et importation de runbooks, consultez [création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md)


