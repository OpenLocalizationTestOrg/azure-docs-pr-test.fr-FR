---
title: ressources aaaConnection dans Azure Automation | Documents Microsoft
description: "Hello informations requises tooconnect tooan service externe ou une application à partir d’un runbook ou la configuration DSC contiennent des ressources de connexion dans Azure Automation. Cet article explique les détails de hello de connexions et la manière dont toowork avec eux dans textuels et graphiques de création."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Ressources de connexion dans Azure Automation

Une ressource de connexion Automation contient hello informations requises tooconnect tooan service externe ou une application à partir d’un runbook ou la configuration DSC. Cela peut inclure les informations requises pour l’authentification par exemple un nom d’utilisateur et un mot de passe dans plus d’informations tooconnection comme une URL ou un port. valeur Hello d’une connexion conserve toutes les propriétés de hello pour la connexion tooa une application particulière dans une seule ressource comme toocreating opposé plusieurs variables. utilisateur de Hello peut modifier des valeurs hello pour une connexion dans un seul emplacement, et vous pouvez passer le nom hello d’une connexion tooa runbook ou la configuration DSC dans un seul paramètre. Hello des propriétés pour une connexion sont accessibles dans les runbook hello ou la configuration DSC avec hello **Get-AutomationConnection** activité.

Lorsque vous créez une connexion, vous devez spécifier un *type de connexion*. type de connexion Hello est un modèle qui définit un ensemble de propriétés. connexion de Hello définit des valeurs pour chaque propriété définie dans son type de connexion. Types de connexion sont ajoutée tooAzure Automation dans des modules d’intégration ou créé par hello [API Azure Automation](http://msdn.microsoft.com/library/azure/mt163818.aspx) si le module d’intégration hello inclut un type de connexion et qu’il est importé dans votre compte Automation. Dans le cas contraire, vous devez toocreate un toospecify de fichier de métadonnées un type de connexion d’Automation.  Pour plus d’informations à ce sujet, consultez [Modules d’intégration](automation-integration-modules.md).  

>[!NOTE] 
>Les ressources sécurisées dans Azure Automation incluent les informations d'identification, les certificats, les connexions et les variables chiffrées. Ces ressources sont chiffrées et stockées Bonjour Azure Automation à l’aide d’une clé unique qui est générée pour chaque compte automation. Cette clé est chiffrée par un certificat principal et stockée dans Azure Automation. Avant de stocker une ressource sécurisée, clé hello pour le compte d’automatisation hello est déchiffré à l’aide du certificat master de hello, puis utilisé asset de hello tooencrypt.

## <a name="windows-powershell-cmdlets"></a>Applets de commande Windows PowerShell

applets de commande Hello Bonjour tableau suivant sont utilisée toocreate et gérer des connexions Automation avec Windows PowerShell. Elles font partie de hello [module Azure PowerShell](/powershell/azure/overview) qui est disponible pour une utilisation dans les runbooks Automation et les configurations DSC.

|Applet de commande|Description|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Récupère une connexion. Inclut une table de hachage avec les valeurs hello les champs de la connexion hello.|
|[New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Crée une connexion.|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Supprime une connexion existante.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Définit la valeur hello d’un champ particulier pour une connexion existante.|

## <a name="activities"></a>Activités

les activités de Hello Bonjour tableau suivant sont des connexions tooaccess utilisés dans un runbook ou la configuration DSC.

|Activités|Description|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Obtient un toouse de connexion. Retourne une table de hachage avec des propriétés de connexion de hello hello.|

>[!NOTE] 
>Évitez d’utiliser des variables avec hello : paramètre de nom de **Get - AutomationConnection** , car cela complique la découverte des dépendances entre les runbooks ou les configurations DSC et les ressources de connexion au moment du design.

## <a name="creating-a-new-connection"></a>Création d’une connexion

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>toocreate une connexion avec hello portail Azure

1. À partir de votre compte automation, cliquez sur hello **actifs** partie tooopen hello **actifs** panneau.
2. Cliquez sur hello **connexions** partie tooopen hello **connexions** panneau.
3. Cliquez sur **ajouter une connexion** haut hello du Panneau de hello.
4. Bonjour **Type** liste déroulante, le type de sélection hello de connexion vous souhaitez toocreate. formulaire de Hello présente les propriétés hello pour ce type particulier.
5. Complétez le formulaire de hello et cliquez sur **créer** toosave hello nouvelle connexion.

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>toocreate une connexion avec hello portail Azure classic

1. À partir de votre compte automation, cliquez sur **actifs** haut hello de fenêtre hello.
2. Au bas de hello de fenêtre hello, cliquez sur **ajouter un paramètre**.
3. Cliquez sur **Ajouter une connexion**.
4. Bonjour **Type de connexion** liste déroulante, le type de sélection hello de connexion vous souhaitez toocreate.  Assistant de Hello présente les propriétés hello pour ce type particulier.
5. Assistant de hello et cliquez sur Nouvelle connexion hello case à cocher toosave hello.

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>toocreate une connexion avec Windows PowerShell

Créer une nouvelle connexion avec Windows PowerShell à l’aide de hello [New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) applet de commande. Cette applet de commande a un paramètre nommé **ConnectionFieldValues** qui attend un [table de hachage](http://technet.microsoft.com/library/hh847780.aspx) définissant des valeurs pour chacune des propriétés hello définies par le type de connexion hello.

Si vous êtes familiarisé avec hello Automation [exécuter en tant que compte](automation-sec-configure-azure-runas-account.md) runbooks tooauthenticate à l’aide de principal du service hello, hello script PowerShell, fourni en tant qu’une autre toocreating Bonjour Bonjour compte d’identification à partir du portail de hello, Crée une nouvelle ressource de connexion à l’aide de hello suivant des exemples de commandes.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Vous êtes ressource de connexion du script toocreate hello toouse en mesure de hello, car lorsque vous créez votre compte Automation, il inclut automatiquement plusieurs modules globales par défaut, ainsi que le type de connexion hello **AzurServicePrincipal**toocreate hello **AzureRunAsConnection** ressource de connexion.  Il s’agit d’importantes tookeep à l’esprit, car si vous essayez de toocreate un nouveau service de tooa tooconnect de connexion actif ou une application avec une autre méthode d’authentification, l’opération échoue, car le type de connexion hello n’est pas déjà défini dans votre compte Automation.  Pour plus d’informations sur la façon dont toocreate votre propre type de connexion pour votre personnalisé ou un module à partir de hello [PowerShell Gallery](https://www.powershellgallery.com), consultez [Modules d’intégration](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Utilisation d’une connexion dans un Runbook ou une configuration DSC

Récupérer une connexion dans une configuration de DSC avec hello ou un runbook **Get-AutomationConnection** applet de commande.  Vous ne pouvez pas utiliser hello [Get-AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) activité.  Cette activité récupère les valeurs hello de hello différents champs de hello connexion et les retourne comme une [table de hachage](http://go.microsoft.com/fwlink/?LinkID=324844) qui peut ensuite être utilisé avec les commandes appropriées hello dans hello runbook ou la configuration DSC.

### <a name="textual-runbook-sample"></a>Exemple de Runbook textuel

Hello exemples de commandes suivants montrent comment toouse hello exécuter en tant que compte indiqué précédemment, tooauthenticate avec des ressources Azure Resource Manager dans votre runbook.  Il utilise la connexion de hello asset représentant hello exécuter en tant que compte, ce qui fait référence à la principal de service basé sur le certificat hello, informations d’identification pas.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Exemples de Runbook graphiques

Vous ajoutez un **Get-AutomationConnection** activité tooa des runbook graphique en cliquant sur la connexion hello dans le volet Bibliothèque de hello de l’éditeur graphique de hello et en sélectionnant **ajouter toocanvas**.

![](media/automation-connections/connection-add-canvas.png)

Hello image suivante montre un exemple d’utilisation d’une connexion dans un runbook graphique.  Il s’agit de hello même exemple ci-dessus pour l’authentification à l’aide du compte d’identification hello avec un runbook textuels.  Cet exemple utilise hello **valeur constante** jeu de données de hello **obtenir une connexion de RunAs** activité qui utilise un objet de connexion pour l’authentification.  A [lien de pipeline](automation-graphical-authoring-intro.md#links-and-workflow) est utilisé ici car hello jeu de paramètres ServicePrincipalCertificate attend un seul objet.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Étapes suivantes

- Révision [liens dans le graphique de création](automation-graphical-authoring-intro.md#links-and-workflow) toounderstand comment hello toodirect et contrôle le flux de logique dans vos runbook.  

- toolearn en savoir plus sur l’utilisation d’Azure Automation de modules PowerShell et les meilleures pratiques pour la création de votre propre toowork de modules PowerShell en tant que Modules d’intégration dans Azure Automation, consultez [Modules d’intégration](automation-integration-modules.md).  
