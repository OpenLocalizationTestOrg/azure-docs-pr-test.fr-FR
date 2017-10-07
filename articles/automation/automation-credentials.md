---
title: ressources aaaCredential dans Azure Automation | Documents Microsoft
description: "Ressources d’informations d’identification dans Azure Automation contiennent des informations d’identification de sécurité qui peuvent être tooresources tooauthenticate utilisé accessibles par hello runbook ou la configuration DSC. Cet article décrit comment toocreate actifs des informations d’identification et les utiliser dans un runbook ou la configuration DSC."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Ressources d’informations d’identification dans Azure Automation
Une ressource d’informations d’identification Automation conserve un objet [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) qui contient les informations d’identification de sécurité comme un nom d’utilisateur et un mot de passe. Configurations DSC et de procédures opérationnelles peuvent utiliser les applets de commande qui acceptent un objet PSCredential pour l’authentification, ou ils peuvent extraire le nom d’utilisateur hello et le mot Hello application de toosome tooprovide PSCredential objet ou service qui requiert l’authentification. propriétés de Hello pour les informations d’identification sont stockées de manière sécurisée dans Azure Automation et sont accessibles dans les runbook hello ou la configuration DSC avec hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) activité.

> [!NOTE]
> Les ressources sécurisées dans Azure Automation incluent les informations d'identification, les certificats, les connexions et les variables chiffrées. Ces ressources sont chiffrées et stockées Bonjour Azure Automation à l’aide d’une clé unique qui est générée pour chaque compte automation. Cette clé est chiffrée par un certificat principal et stockée dans Azure Automation. Avant de stocker une ressource sécurisée, clé hello pour le compte d’automatisation hello est déchiffré à l’aide du certificat master de hello, puis utilisé asset de hello tooencrypt.  

## <a name="windows-powershell-cmdlets"></a>Applets de commande Windows PowerShell
applets de commande Hello Bonjour tableau suivant sont utilisée toocreate et gérer des ressources d’informations d’identification automation avec Windows PowerShell.  Elles font partie de hello [module Azure PowerShell](/powershell/azure/overview) qui est disponible pour une utilisation dans les runbooks Automation et les configurations DSC.

| Applets de commande | Description |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |Récupère des informations sur une ressource d’informations d’identification. Vous pouvez uniquement récupérer des informations d’identification hello lui-même à partir de **Get-AutomationPSCredential** activité. |
| [New-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Crée de nouvelles informations d’identification Automation. |
| [Remove- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Supprime des informations d’identification Automation. |
| [Set- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Jeux de hello des propriétés pour les informations d’identification Automation existantes. |

## <a name="runbook-activities"></a>Activités de Runbook
activités Hello Bonjour tableau suivant sont des informations d’identification de tooaccess utilisés dans un runbook et les configurations DSC.

| Activités | Description |
|:--- |:--- |
| Get-AutomationPSCredential |Obtient un toouse d’informations d’identification dans un runbook ou la configuration DSC. Renvoie un objet [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) . |

> [!NOTE]
> Vous devez éviter d’utiliser des variables dans hello – paramètre Name de Get-AutomationPSCredential car cela peut compliquer la découverte des dépendances entre les runbooks et les configurations DSC et ressources des informations d’identification au moment du design.
> 
> 

## <a name="creating-a-new-credential-asset"></a>Création d’une ressource d’informations d’identification

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>toocreate un élément multimédia d’informations d’identification avec hello portail Azure
1. À partir de votre compte automation, cliquez sur hello **actifs** partie tooopen hello **actifs** panneau.
2. Cliquez sur hello **informations d’identification** partie tooopen hello **informations d’identification** panneau.
3. Cliquez sur **ajouter les informations d’identification** haut hello du Panneau de hello.
4. Complétez le formulaire de hello et cliquez sur **créer** toosave hello de nouvelles informations d’identification.

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>toocreate un élément multimédia d’informations d’identification avec Windows PowerShell
Hello exemples de commandes suivants montrent comment toocreate une automation de nouvelles informations d’identification. Un objet PSCredential est d’abord créé avec un mot de passe et nom de hello et ensuite utilisé actif d’informations d’identification toocreate hello. Vous pouvez également utiliser hello **Get-Credential** toobe de l’applet de commande invité tootype dans un nom et un mot de passe.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>toocreate un élément multimédia d’informations d’identification avec hello portail Azure classic
1. À partir de votre compte automation, cliquez sur **actifs** haut hello de fenêtre hello.
2. Au bas de hello de fenêtre hello, cliquez sur **ajouter un paramètre**.
3. Cliquez sur **Ajouter les informations d’identification**.
4. Bonjour **Type d’informations d’identification** liste déroulante, sélectionnez **informations d’identification PowerShell**.
5. Assistant de hello et cliquez sur hello case à cocher toosave hello nouvelles informations d’identification.

## <a name="using-a-powershell-credential"></a>Utilisation des informations d’identification PowerShell
Vous récupérez une ressource d’informations d’identification dans un runbook ou la configuration DSC hello **Get-AutomationPSCredential** activité. Cette propriété renvoie un [objet PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) que vous pouvez utiliser avec une activité ou une applet de commande nécessitant un paramètre PSCredential. Vous pouvez également récupérer des propriétés hello de hello d’informations d’identification objet toouse individuellement. objet Hello possède une propriété de nom d’utilisateur hello et le mot de passe sécurisé hello, ou vous pouvez utiliser hello **GetNetworkCredential** méthode tooreturn un [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) objet qui fournira un non sécurisé version du mot de passe hello.

### <a name="textual-runbook-sample"></a>Exemple de Runbook textuel
Hello exemples de commandes suivants montrent comment toouse un PowerShell des informations d’identification dans un runbook. Dans cet exemple, informations d’identification hello sont récupérée et son nom d’utilisateur et un mot de passe assigné toovariables.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>Exemple de Runbook graphique
Vous ajoutez un **Get-AutomationPSCredential** activité tooa des runbook graphique en cliquant sur les informations d’identification hello dans le volet Bibliothèque de hello de l’éditeur graphique de hello et en sélectionnant **ajouter toocanvas**.

![Ajouter des informations d’identification toocanvas](media/automation-credentials/credential-add-canvas.png)

Hello image suivante montre un exemple d’utilisation des informations d’identification dans un runbook graphique.  Dans ce cas, il est en cours tooprovide utilisé l’authentification pour un runbook des ressources tooAzure comme décrit dans [Runbooks de s’authentifier avec un compte d’utilisateur Active Directory de Azure](automation-create-aduser-account.md).  la première activité Hello récupère les informations d’identification hello qui a accès toohello abonnement Azure.  Hello **Add-AzureAccount** activité utilise ensuite cette authentification de tooprovide d’informations d’identification pour toutes les activités qui viennent après lui.  C’est un [lien pipeline](automation-graphical-authoring-intro.md#links-and-workflow) , étant donné que **Get-AutomationPSCredential** attend un objet unique.  

![Ajouter des informations d’identification toocanvas](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>Utilisation des informations d’identification PowerShell dans une configuration DSC
Bien que les configurations DSC dans Azure Automation puissent se rapporter à des ressources d’informations d’identification utilisant **Get-AutomationPSCredential**, les ressources d’information d’identification peuvent également transmises via des paramètres, si vous le souhaitez. Pour plus d’informations, consultez [Compilation de configurations dans Azure Automation DSC](automation-dsc-compile.md#credential-assets).

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur les liens dans le graphique de création, consultez [liens dans le graphique de création](automation-graphical-authoring-intro.md#links-and-workflow)
* toounderstand hello différentes méthodes d’authentification avec l’Automation, consultez [de sécurité Azure Automation](automation-security-overview.md)
* tooget main runbooks graphiques, consultez [mon premier runbook graphique](automation-first-runbook-graphical.md)
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md) 

