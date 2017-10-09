---
title: runbooks aaaRun sur le travail de Runbook hybride Azure Automation | Documents Microsoft
description: "Cet article fournit des informations sur l’exécution des procédures opérationnelles sur des ordinateurs dans votre centre de données local ou d’un fournisseur de cloud avec le rôle de travail de Runbook hybride hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Exécution de Runbooks sur un Runbook Worker hybride 
Il n’existe aucune différence dans la structure de hello des procédures opérationnelles qui s’exécutent dans Azure Automation et celles qui s’exécutent sur un Runbook Worker hybride. Les runbooks que vous utilisez avec chaque très probablement diffèrent considérablement cependant étant donné que les procédures opérationnelles ciblant un Runbook Worker hybride généralement gérer les ressources sur les ordinateur local hello lui-même ou sur des ressources dans l’environnement local de hello où il est déployé, tout en procédures opérationnelles dans Azure Automation généralement gérer les ressources Bonjour cloud Azure.

Vous pouvez modifier un runbook pour un Runbook Worker hybride dans Azure Automation, mais peut avoir des difficultés si vous essayez de runbook de hello tootest dans l’éditeur de hello.  modules PowerShell Hello qui accèdent aux ressources locales de hello ne peuvent pas être installés dans votre environnement Azure Automation dans ce cas, les tests hello échouerait.  Si vous installez hello requis des modules, hello runbook s’exécute, mais il ne sera pas en mesure de tooaccess des ressources locales pour un test complet.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>Démarrage d’un Runbook sur Runbook Worker hybride
[Démarrage d'un Runbook dans Azure Automation](automation-starting-a-runbook.md) décrit différentes méthodes de démarrage d'un Runbook.  Runbook Worker hybride ajoute un **RunOn** option où vous pouvez spécifier le nom de hello d’un groupe de travail de Runbook hybride.  Si un groupe est spécifié, puis hello runbook est récupéré et exécuté par des travailleurs hello dans ce groupe.  Si cette option n'est pas spécifiée, il est exécuté dans Azure Automation comme habituellement.

Lorsque vous démarrez un runbook dans hello portail Azure, vous sont présentées avec un **s’exécutent sur** option dans laquelle vous pouvez sélectionner **Azure** ou **Worker hybride**.  Si vous sélectionnez **Worker hybride**, vous pouvez sélectionner le groupe de hello dans une liste déroulante.

Hello d’utilisation **RunOn** paramètre.  Vous pouvez utiliser hello suivant commande toostart un runbook nommé Test-Runbook sur un groupe de travail de Runbook hybride nommé MyHybridGroup à l’aide de Windows PowerShell.

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> Hello **RunOn** paramètre a été ajouté toohello **Start-AzureAutomationRunbook** applet de commande dans la version 0.9.1 de Microsoft Azure PowerShell.  Vous devez [télécharger la version la plus récente hello](https://azure.microsoft.com/downloads/) si vous avez une ancienne installée.  Vous ne devez tooinstall cette version sur une station de travail où vous démarrez hello runbook à partir de Windows PowerShell.  Vous n’avez pas besoin de tooinstall sur l’ordinateur de traitement hello, sauf si vous avez l’intention de runbooks toostart à partir de cet ordinateur.  Vous ne pouvez pas actuellement démarrer un runbook sur un Runbook Worker hybride à partir d’un autre runbook, car cela nécessiterait plus récent hello toobe Azure Powershell installé dans votre compte Automation.  version la plus récente Hello est automatiquement mis à jour dans Azure Automation et automatiquement poussée vers le bas les travailleurs toohello bientôt.
>
>

## <a name="runbook-permissions"></a>Autorisations de Runbook
Procédures opérationnelles en cours d’exécution sur un Runbook Worker hybride ne peut pas utiliser hello même méthode qui est généralement utilisé pour les procédures opérationnelles de l’authentification des ressources tooAzure, dans la mesure où ils accèdent à des ressources en dehors d’Azure.  Hello runbook peut fournir sa propre authentification toolocal ressources, ou vous pouvez spécifier un tooprovide de compte d’identification un contexte utilisateur pour tous les runbooks.

### <a name="runbook-authentication"></a>Authentification des Runbooks
Par défaut, les procédures opérationnelles s’exécute dans le contexte de hello du compte système local de hello sur l’ordinateur local de hello, pour qu’ils doivent fournir leur propre tooresources de l’authentification d’accès.  

Vous pouvez utiliser [informations d’identification](http://msdn.microsoft.com/library/dn940015.aspx) et [certificat](http://msdn.microsoft.com/library/dn940013.aspx) actifs dans votre runbook avec les applets de commande qui permettent d’informations d’identification toospecify afin de vous authentifier toodifferent ressources.  Hello suivant montre une partie d’un runbook qui redémarre un ordinateur.  Il extrait les informations d’identification à partir d’un nom d’identification de l’élément multimédia et hello d’ordinateur hello à partir d’une ressource de variable et utilise ensuite ces valeurs avec l’applet de commande hello Restart-Computer.

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

Vous pouvez également exploiter [InlineScript](automation-powershell-workflow.md#inlinescript), qui vous permet de toorun des blocs de code sur un autre ordinateur avec les informations d’identification spécifiées par hello [paramètre commun de PSCredential](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="runas-account"></a>Compte RunAs
Au lieu de procédures opérationnelles fournir leur propre authentification toolocal ressources, vous pouvez spécifier un **RunAs** compte pour un groupe de travail hybride.  Vous spécifiez un [actif d’informations d’identification](automation-credentials.md) incluant toolocal d’accéder aux ressources, et tous les runbooks s’exécutent sous ces informations d’identification lors de l’exécution sur un Runbook Worker hybride dans le groupe de hello.  

nom d’utilisateur Hello pour les informations d’identification hello doit être dans un des hello suivant formats :

* domaine\nom d’utilisateur
* username@domain
* nom d’utilisateur (pour l’ordinateur de comptes locaux toohello local)

Utilisez hello suivant la procédure toospecify un compte d’identification pour un groupe de travail hybride :

1. Créer un [actif d’informations d’identification](automation-credentials.md) avec toolocal d’accéder aux ressources.
2. Ouvrez le compte Automation de hello Bonjour portail Azure.
3. Sélectionnez hello **groupes de travail hybride** vignette, puis sélectionnez le groupe de hello.
4. Sélectionnez **Tous les paramètres**, puis **Paramètres du groupe Worker hybride**.
5. Modification **exécuter en tant que** de **par défaut** trop**personnalisé**.
6. Sélectionnez les informations d’identification hello et cliquez sur **enregistrer**.

### <a name="automation-run-as-account"></a>Compte d’identification Automation
Dans le cadre de votre processus de génération automatisé pour le déploiement de ressources dans Azure, vous pouvez avoir besoin toosupport de systèmes de site tooon accès une tâche ou un ensemble d’étapes dans votre séquence de déploiement.  toosupport l’authentification sur Azure à l’aide du compte d’identification hello, vous devez tooinstall hello exécuter en tant que certificat de compte de.  

Hello suivant PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exporte hello exécuter en tant que certificat de votre compte Azure Automation et télécharge et il importe dans le magasin de certificats ordinateur local hello sur un Worker hybride connecté toohello même compte.  Une fois cette étape terminée, il vérifie les processus de travail hello peuvent s’authentifier correctement tooAzure à l’aide du compte d’identification hello.

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

Enregistrer hello *Export-RunAsCertificateToHybridWorker* runbook tooyour équipé d’un `.ps1` extension.  Importer dans votre compte Automation et modifier les runbook hello, la modification de valeur hello de variable de hello `$Password` avec votre mot de passe.  Publier, puis exécutez runbook hello ciblant un groupe Worker hybride hello qui s’exécutent et authentifier des runbooks à l’aide du compte d’identification hello.  Hello travail flux rapports hello tentative tooimport hello certificat dans le magasin de l’ordinateur local hello et suit avec plusieurs lignes, selon le nombre de comptes Automation est défini dans votre abonnement et si l’authentification réussit.  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>Résolution de problèmes de runbooks sur un Runbook Worker hybride
Les journaux sont stockés localement sur chaque Worker hybride à l’emplacement C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Worker hybride enregistre également les erreurs et les événements dans le journal des événements Windows hello sous **d’Application et de Services Logs\Microsoft-SMA\Operational**.  Événements liés toorunbooks exécutées sur le travail de hello sont écrits en trop**d’Application et de Services Logs\Microsoft-Automation\Operational**.  Hello **Microsoft-SMA** journal inclut des nombreux plus événements connexes toohello runbook toohello envoyées hello et travail de traitement de hello runbook.  Lors de hello **Microsoft-Automation** journal des événements n’a pas de nombreux événements avec les détails en aidant hello résolution des problèmes d’exécution de runbook, vous trouverez au moins des résultats de la tâche du runbook hello hello.  

[Runbook de sortie et messages](automation-runbook-output-and-messages.md) sont envoyés tooAzure Automation à partir de workers hybrides simplement que les travaux de runbook s’exécutent dans le cloud de hello.  Vous pouvez également activer hello Verbose et flux de progression hello même façon que vous le feriez pour d’autres runbooks.  

Si vos runbooks ne sont pas correctement terminées et le résumé des tâches hello présente l’état de **Suspended**, passez en revue hello article de résolution des problèmes [Runbook Worker hybride : une tâche de runbook se termine avec l’état Suspendu](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).   

## <a name="next-steps"></a>Étapes suivantes
* toolearn savoir plus sur hello différentes méthodes qui peuvent être utilisé toostart un runbook, consultez [démarrage d’un Runbook dans Azure Automation](automation-starting-a-runbook.md).  
* toounderstand hello différentes procédures pour travailler avec PowerShell et les flux de travail PowerShell runbooks dans Azure Automation à l’aide de l’éditeur de texte hello, consultez [modification d’un Runbook dans Azure Automation](automation-edit-textual-runbook.md)
