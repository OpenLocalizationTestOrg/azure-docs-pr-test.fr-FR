---
title: configuration du compte Azure Automation aaaValidate | Documents Microsoft
description: "Cet article décrit la configuration de hello tooconfirm de votre compte Automation est configurée correctement."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a>Test d’authentification du compte d’identification Azure Automation
Une fois un compte Automation est créé avec succès, vous pouvez effectuer un tooconfirm de test simple que vous ne pouvez toosuccessfully s’authentifier dans Azure Resource Manager ou un déploiement classique Azure à l’aide de votre compte Automation exécuter en tant que nouvellement créé ou mis à jour.    

## <a name="automation-run-as-authentication"></a>Authentification d’identification Automation
Utilisez hello exemple de code ci-dessous trop[créer un runbook PowerShell](automation-creating-importing-runbook.md) tooverify l’authentification à l’aide de hello exécuter en tant que compte et également dans votre tooauthenticate runbooks personnalisés et de gérer les ressources du Gestionnaire de ressources avec votre compte Automation.   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

Notez hello applet de commande utilisée pour l’authentification dans hello runbook - **Add-AzureRmAccount**, utilise hello *ServicePrincipalCertificate* jeu de paramètres.  Elle effectue l’authentification à l’aide du certificat du principal du service et non des informations d’identification.  

Lorsque vous [exécuter hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate votre compte d’identification, un [tâche du runbook](automation-runbook-execution.md) est créé, panneau de tâche hello s’affiche, et état de la tâche hello affichée Bonjour **récapitulatif**vignette. état de la tâche Hello démarrera en tant que *en file d’attente* indiquant qu’il est en attente d’un runbook worker dans hello toobecome de cloud disponible. Il passe alors trop*départ* lorsqu’un processus de travail tâche de hello, les revendications, puis *en cours d’exécution* démarrage hello runbook réellement en cours d’exécution.  Lors de la tâche de runbook hello est terminée, nous devons voyez l’état **terminé**.

toosee hello les résultats détaillés de hello runbook, cliquez sur hello **sortie** vignette.  Sur hello **sortie** panneau, vous devez voir qu’il a été authentifié et retourne une liste de toutes les ressources de tous les groupes de ressources dans votre abonnement.  

Rappelez-vous simplement le bloc de hello tooremove de code commençant par le commentaire hello `#Get all ARM resources from all resource groups` lorsque vous réutilisez le code de hello pour les procédures opérationnelles.

## <a name="classic-run-as-authentication"></a>Authentification d’identification Classic
Utilisez hello exemple de code ci-dessous trop[créer un runbook PowerShell](automation-creating-importing-runbook.md) à l’aide de l’authentification tooverify hello classique exécute en tant que compte et également dans votre tooauthenticate runbooks personnalisés et de gérer les ressources dans le modèle de déploiement classique hello.  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

Lorsque vous [exécuter hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate votre compte d’identification, un [tâche du runbook](automation-runbook-execution.md) est créé, panneau de tâche hello s’affiche, et état de la tâche hello affichée Bonjour **récapitulatif**vignette. état de la tâche Hello démarrera en tant que *en file d’attente* indiquant qu’il est en attente d’un runbook worker dans hello toobecome de cloud disponible. Il passe alors trop*départ* lorsqu’un processus de travail tâche de hello, les revendications, puis *en cours d’exécution* démarrage hello runbook réellement en cours d’exécution.  Lors de la tâche de runbook hello est terminée, nous devons voyez l’état **terminé**.

toosee hello les résultats détaillés de hello runbook, cliquez sur hello **sortie** vignette.  Sur hello **sortie** panneau, vous devez voir qu’il a été authentifié et retourne une liste de tous les ordinateurs virtuels de Azure à VMName qui sont déployés dans votre abonnement.  

N’oubliez pas applet de commande hello tooremove **Get-AzureVM** lorsque vous réutilisez le code de hello pour les procédures opérationnelles.

## <a name="next-steps"></a>Étapes suivantes
* tooget main runbook PowerShell, consultez [mon runbook PowerShell premier](automation-first-runbook-textual-powershell.md).
* toolearn plus sur la création de graphiques, consultez [de création graphique dans Azure Automation](automation-graphical-authoring-intro.md).
