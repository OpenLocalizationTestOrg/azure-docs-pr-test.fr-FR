---
title: configurations aaaCompiling dans Azure Automation DSC | Documents Microsoft
description: "Cet article décrit comment toocompile les configurations de Configuration d’état souhaité (DSC) pour Azure Automation."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Compilation de configurations dans Azure Automation DSC

Vous pouvez compiler des configurations de Configuration d’état souhaité (DSC) de deux manières avec Azure Automation : Bonjour portail Azure et avec Windows PowerShell. Hello tableau suivant vous aide à déterminer quand toouse sur lequel la méthode en fonction des caractéristiques de hello de chacun :

### <a name="azure-portal"></a>Portail Azure

* Méthode la plus simple avec une interface utilisateur interactive
* Valeurs de formulaire tooprovide paramètres simples.
* Suivi aisé de l’état des tâches
* Accès authentifié avec ouverture de session Azure

### <a name="windows-powershell"></a>Windows PowerShell

* Appel à partir de la ligne de commande avec les applets de commande Windows PowerShell
* Possibilité d’inclusion dans une solution automatisée à plusieurs étapes
* Fourniture de valeurs de paramètres simples et complexes
* Suivi de l’état des tâches
* Client requis toosupport applets de commande PowerShell
* Transmission ConfigurationData
* Compilation de configurations utilisant des informations d’identification

Une fois que vous avez choisi une méthode de compilation, vous pouvez suivre les procédures de respectifs de hello ci-dessous toostart la compilation.

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>La compilation d’une Configuration DSC avec hello portail Azure

1. Dans votre compte Automation, cliquez sur **Configurations DSC**.
2. Cliquez sur une configuration tooopen son panneau.
3. Cliquez sur **Compiler**.
4. Si la configuration de hello n’a aucun paramètre, vous serez invité à tooconfirm si vous souhaitez toocompile il. Si la configuration de hello possède des paramètres, hello **compiler la Configuration** panneau afin de pouvoir fournir des valeurs de paramètre. Consultez hello [ **paramètres de base** ](#basic-parameters) section ci-dessous pour plus d’informations sur les paramètres.
5. Hello **tâche de Compilation** panneau est ouvert afin que vous pouvez suivre le statut de la tâche de compilation hello et hello configurations de nœuds (documents MOF de configuration) a provoqué toobe placé sur hello serveur d’extraction Azure Automation DSC.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>Compilation d’une configuration DSC avec Windows PowerShell

Vous pouvez utiliser [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart la compilation avec Windows PowerShell. Hello suivant l’exemple de code démarre la compilation d’une configuration DSC nommée **SampleConfig**.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`objet que vous pouvez utiliser tootrack son état de la tâche retourne une compilation. Vous pouvez ensuite utiliser cet objet de tâche de compilation avec [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) état de hello toodetermine de la tâche de compilation hello, et [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview ses flux (sortie). Hello suivant l’exemple de code démarre la compilation de hello **SampleConfig** configuration, attend qu’il a terminé, puis affiche son flux de données.

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>Paramètres de base
Déclaration de paramètre dans les configurations DSC, y compris les types de paramètres et les propriétés, fonctionne même hello comme dans les runbooks Azure Automation. Consultez [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md) toolearn plus d’informations sur les paramètres du runbook.

Hello exemple suivant utilise deux paramètres appelés **FeatureName** et **IsPresent**, toodetermine les valeurs de hello des propriétés dans hello **ParametersExample.sample** nœud configuration, générée pendant la compilation.

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

Vous pouvez compiler les Configurations DSC qui utilisent les paramètres de base dans le portail d’Azure Automation DSC hello, ou Azure PowerShell :

### <a name="portal"></a>Portail

Dans le portail hello, vous pouvez entrer des valeurs de paramètre après avoir cliqué sur **compiler**.

![alt text](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell requiert des paramètres dans un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) clé de hello correspond au nom du paramètre hello, alors que la valeur du paramètre hello a la valeur hello.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

Pour plus d’informations sur la transmission d’informations d’identification PowerShell en tant que paramètres, voir la section <a href="#credential-assets">**Ressources d’informations d’identification**</a> ci-dessous.

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** vous permet de tooseparate la configuration structurelle à partir de n’importe quel configuration spécifique de l’environnement lors de l’utilisation de DSC PowerShell. Consultez [séparant « ce » qu’à partir de « Where » dans DSC PowerShell](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn plus **ConfigurationData**.

> [!NOTE]
> Vous pouvez utiliser **ConfigurationData** lors de la compilation dans Azure Automation DSC à l’aide d’Azure PowerShell, mais pas dans hello portail Azure.

Hello DSC configuration suivante utilise **ConfigurationData** via hello **$ConfigurationData** et **$AllNodes** mots clés. Vous devez également hello [ **xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) pour cet exemple :

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

Vous pouvez compiler hello DSC la configuration ci-dessus avec PowerShell. Hello sous PowerShell ajoute deux toohello de configurations de nœud serveur de collecteur Azure Automation DSC : **ConfigurationDataSample.MyVM1** et **ConfigurationDataSample.MyVM3**:

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a>Éléments multimédias

Références de l’élément multimédia sont hello même dans les runbooks et les configurations Azure Automation DSC. Consultez les rubriques suivantes de hello pour plus d’informations :

* [Certificats](automation-certificates.md)
* [Connexions](automation-connections.md)
* [Informations d'identification](automation-credentials.md)
* [Variables](automation-variables.md)

### <a name="credential-assets"></a>Ressources d’informations d’identification

Bien que les configurations DSC dans Azure Automation puissent référencer des ressources d’informations d’identification en utilisant **Get-AzureRmAutomationCredential**, vous pouvez également transmettre les ressources d’informations d’identification par le biais de paramètres si vous le souhaitez. Si une configuration prend un paramètre de **PSCredential** de type, vous devez le nom de chaîne hello toopass d’une ressource d’informations d’identification Azure Automation en tant que valeur de ce paramètre, plutôt que sur un objet PSCredential. Coulisses de hello, ressource d’informations d’identification Azure Automation hello portant ce nom sera récupéré et passé toohello configuration.

Conservation des informations d’identification sécurisé dans les configurations de nœuds (documents MOF de configuration) nécessite le chiffrement des informations d’identification hello dans le fichier MOF de configuration de nœud hello. Azure Automation est une étape supplémentaire et chiffre la totalité du fichier MOF hello. Toutefois, actuellement vous devez indiquer à DSC PowerShell c’est OK pour toobe des informations d’identification envoyée en texte brut pendant la génération de fichier MOF de configuration de nœud, parce que PowerShell DSC ne sait pas que les Azure Automation sera chiffrer le fichier MOF entière hello après son génération par une tâche de compilation.

Vous pouvez indiquer à DSC PowerShell qu’il est OK pour toobe des informations d’identification envoyée en texte brut dans la configuration du nœud hello généré MOF à l’aide de [ **ConfigurationData**](#configurationdata). Vous devez passer `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** pour le nom du chaque bloc nœud qui s’affiche dans la configuration de hello DSC et utilise les informations d’identification.

Hello suivant montre une configuration DSC qui utilise une ressource d’informations d’identification Automation.

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

Vous pouvez compiler hello DSC la configuration ci-dessus avec PowerShell. Hello sous PowerShell ajoute deux toohello de configurations de nœud serveur de collecteur Azure Automation DSC : **CredentialSample.MyVM1** et **CredentialSample.MyVM2**.

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a>Importation de configurations de nœuds

Vous pouvez également importer des configurations de nœuds (MOF) que vous avez compilées en dehors d’Azure. Cette configuration de nœuds offre l’avantage de pouvoir être signée.
Une configuration de nœud signé est vérifiée localement sur un nœud géré par agent hello DSC, de s’assurer que la configuration hello étant appliqués toohello nœud proviennent d’une source autorisée.

> [!NOTE]
> Vous pouvez importer des configurations signées dans votre compte Azure Automation, mais Azure Automation ne prend pas en charge la compilation de configurations signées.

> [!NOTE]
> Un fichier de configuration de nœud doit pas être supérieur à 1 Mo tooallow il toobe importé dans Azure Automation.

Vous pouvez apprendre comment toosign des configurations de nœuds à https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>Importation d’une configuration de nœud Bonjour portail Azure

1. Dans votre compte Automation, cliquez sur **Configurations de nœuds DSC**.

    ![Configurations de nœuds DSC](./media/automation-dsc-compile/node-config.png)
2. Bonjour **configurations de nœuds DSC** panneau, cliquez sur **ajouter une NodeConfiguration**.
3. Bonjour **importation** panneau, cliquez sur hello dossier icône suivant toohello **fichier de Configuration de nœud** toobrowse de zone de texte d’un fichier de configuration de nœud (MOF) sur votre ordinateur local.

    ![Rechercher un fichier local](./media/automation-dsc-compile/import-browse.png)
4. Entrez un nom dans hello **nom de la Configuration** zone de texte. Ce nom doit correspondre au nom hello de configuration hello à partir de laquelle la configuration du nœud hello a été compilée.
5. Cliquez sur **OK**.

### <a name="importing-a-node-configuration-with-powershell"></a>Importation d’une configuration de nœuds avec PowerShell

Vous pouvez utiliser hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) tooimport de l’applet de commande une configuration de nœud dans votre compte automation.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



