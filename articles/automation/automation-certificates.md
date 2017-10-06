---
title: ressources aaaCertificate dans Azure Automation | Documents Microsoft
description: "Les certificats peuvent être stockées en toute sécurité dans Azure Automation afin qu’ils sont accessibles par les procédures opérationnelles ou tooauthenticate des configurations DSC sur Azure et les ressources tierces.  Cet article explique les détails de hello des certificats et comment toowork avec eux dans textuels et graphiques de création."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Ressources de certificats dans Azure Automation

Les certificats peuvent être stockés en toute sécurité dans Azure Automation afin qu’ils sont accessibles par les procédures opérationnelles ou les configurations DSC à l’aide de hello **Get-AzureRmAutomationRmCertificate** activité pour les ressources Azure Resource Manager. Cela vous permet de toocreate runbooks et les configurations DSC qui utilisent des certificats pour l’authentification ou ajoute les ressources tooAzure ou tiers.

> [!NOTE] 
> Les ressources sécurisées dans Azure Automation incluent les informations d'identification, les certificats, les connexions et les variables chiffrées. Ces ressources sont chiffrées et stockées Bonjour Azure Automation à l’aide d’une clé unique qui est générée pour chaque compte automation. Cette clé est chiffrée par un certificat principal et stockée dans Azure Automation. Avant de stocker une ressource sécurisée, clé hello pour le compte d’automatisation hello est déchiffré à l’aide du certificat master de hello, puis utilisé asset de hello tooencrypt.
> 

## <a name="windows-powershell-cmdlets"></a>Applets de commande Windows PowerShell

applets de commande Hello Bonjour tableau suivant sont utilisée toocreate et gérer des ressources de certificat automation avec Windows PowerShell. Elles font partie de hello [module Azure PowerShell](../powershell-install-configure.md) qui est disponible pour une utilisation dans les runbooks Automation et les configurations DSC.

|Applets de commande|Description|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Récupère des informations sur un toouse de certificat dans un runbook ou la configuration DSC. Vous pouvez uniquement récupérer le certificat hello lui-même à partir de l’activité de Get-AutomationCertificate.|
|[New-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|Crée un nouveau certificat dans Azure Automation.|
[Remove-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Supprime un certificat dans Azure Automation.|Crée un nouveau certificat dans Azure Automation.
|[Set-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|Définit les propriétés hello pour un certificat existant, notamment le téléchargement du fichier de certificat hello et un mot de passe hello paramètre d’un fichier .pfx.|
|[Add-AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Téléchargements d’un service de certificats pour hello spécifié service cloud.|


## <a name="creating-a-new-certificate"></a>Création d’un certificat

Lorsque vous créez un nouveau certificat, vous téléchargez un fichier .cer ou .pfx tooAzure Automation. Si vous marquez le certificat hello comme exportable, vous pouvez également le transférer hors de magasin de certificats Azure Automation hello. Si elle n’est pas exportable, puis il peut uniquement être utilisé pour la signature dans hello runbook ou la configuration DSC.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate un nouveau certificat avec hello portail Azure

1. À partir de votre compte Automation, cliquez sur hello **actifs** vignette tooopen hello **actifs** panneau.
1. Cliquez sur hello **certificats** vignette tooopen hello **certificats** panneau.
1. Cliquez sur **ajouter un certificat** haut hello du Panneau de hello.
2. Tapez un nom pour le certificat de hello Bonjour **nom** boîte.
2. Cliquez sur **sélectionner un fichier** sous **télécharger un fichier de certificat** toobrowse pour un fichier .cer ou .pfx.  Si vous sélectionnez un fichier .pfx, spécifiez un mot de passe et si elle doit être autorisée toobe exporté.
1. Cliquez sur **créer** toosave hello nouveau certificat bien.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>toocreate un nouveau certificat avec Windows PowerShell

Hello exemple suivant montre comment toocreate une Automation de nouveau certificat et marquer exportable. Cette opération importe un fichier pfx existant.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Utilisation d’un certificat

Vous devez utiliser hello **Get-AutomationCertificate** activité toouse un certificat. Vous ne pouvez pas utiliser hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) applet de commande, car elle retourne des informations sur la ressource de certificat hello mais pas les certificats hello lui-même.

### <a name="textual-runbook-sample"></a>Exemple de Runbook textuel

Hello suivant l’exemple de code montre comment tooadd un tooa certificat service de cloud computing dans un runbook. Dans cet exemple, un mot de passe hello est récupérée à partir d’une variable automation chiffrée.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Exemple de Runbook graphique

Vous ajoutez un **Get-AutomationCertificate** tooa des runbook graphique en cliquant sur le certificat hello dans le volet Bibliothèque de hello de l’éditeur graphique de hello et en sélectionnant **ajouter toocanvas**.

![Ajouter la zone de dessin toohello certificat](media/automation-certificates/automation-certificate-add-to-canvas.png)

Hello image suivante montre un exemple d’utilisation d’un certificat dans un runbook graphique.  Il s’agit de hello même exemple ci-dessus pour l’ajout d’un service de cloud de tooa de certificat à partir d’un runbook textuels.

![Exemple de création graphique ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>Étapes suivantes

- toolearn plus sur l’utilisation avec des liens toocontrol hello logique un flux d’activités de votre runbook est conçu tooperform, consultez [liens de création graphique](automation-graphical-authoring-intro.md#links-and-workflow). 
