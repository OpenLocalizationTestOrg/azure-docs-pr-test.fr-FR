---
title: "les passerelles VPN aaaMonitor la résolution des problèmes de l’Observateur réseau Azure | Documents Microsoft"
description: "Cet article explique comment diagnostiquer la connectivité locale avec Azure Automation et Network Watcher."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Surveiller les passerelles VPN à l’aide de la résolution des problèmes Network Watcher

Obtenir des informations détaillées sur les performances de votre réseau est toocustomers de services fiables tooprovide critiques. Il est donc critique toodetect conditions de panne réseau rapidement et prendre la condition de panne d’une action corrective toomitigate hello. Azure Automation vous permet de tooimplement et exécuter une tâche de manière par programmation via des procédures opérationnelles. L’utilisation d’Azure Automation crée un environnement parfait pour l’exécution d’une surveillance réseau proactive et continue et d’alertes.

## <a name="scenario"></a>Scénario

scénario Hello Bonjour suivant l’image est une application multicouche, avec établie à l’aide d’une passerelle VPN et un tunnel de connectivité du site. Assurer hello que passerelle VPN est activé et en cours d’exécution sont performances des applications critiques toohello.

Vous pouvez créer un runbook avec un toocheck de script pour l’état de la connexion de tunnel VPN de hello, à l’aide de hello API de résolution des problèmes de ressources toocheck pour l’état de la connexion tunnel. Si l’état de hello n’est pas intègre, un déclencheur de courrier électronique est envoyé à tooadministrators.

![Exemple de scénario][scenario]

Ce scénario va :

- Créer un hello appelant runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` état de la connexion tootroubleshoot applet de commande
- Liez un runbook toohello de planification

## <a name="before-you-begin"></a>Avant de commencer

Avant de commencer ce scénario, vous devez disposer de hello suivant des conditions préalables :

- Un compte Azure Automation dans Azure. Assurez-vous que le compte d’automatisation hello a des modules de dernière hello et a également le module de AzureRM.Network hello. module de AzureRM.Network Hello n’est disponible dans la galerie des modules hello si vous avez besoin de tooadd il compte automation de tooyour.
- Vous devez avoir configuré des informations d’identification dans Azure Automation. Pour en savoir plus, consultez l’article [Sécurité dans Azure Automation](../automation/automation-security-overview.md).
- Un serveur SMTP valide (Office 365, votre messagerie locale ou une autre) et les informations d’identification définies dans Azure Automation.
- Une passerelle de réseau virtuel configurée dans Azure.
- Un compte de stockage existant avec un hello toostore de conteneur existant se connecte.

> [!NOTE]
> infrastructure Hello mentionné dans hello précédant l’image est à titre d’illustration et ne sont pas créés aux étapes hello contenues dans cet article.

### <a name="create-hello-runbook"></a>Créer des runbook de hello

exemple de Hello première étape tooconfiguring hello est toocreate hello runbook. Cet exemple utilise un compte d’identification. toolearn sur les comptes d’identification, visitez [Runbooks de s’authentifier avec un compte d’identification Azure](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>Étape 1

Accédez tooAzure Automation Bonjour [portail Azure](https://portal.azure.com) et cliquez sur **Runbooks**

![présentation du compte Automation][1]

### <a name="step-2"></a>Étape 2

Cliquez sur **ajouter un runbook** toostart des processus de création de hello de hello runbook.

![panneau de runbooks][2]

### <a name="step-3"></a>Étape 3 :

Sous **création rapide**, cliquez sur **créer un runbook** toocreate hello runbook.

![panneau ajouter un runbook][3]

### <a name="step-4"></a>Étape 4

Dans cette étape, nous nommez les runbook hello, dans l’exemple de hello, il est appelé **Get-VPNGatewayStatus**. Il est important de toogive hello runbook un nom descriptif et recommandé de lui donner un nom qui suit les normes d’affectation de noms standards PowerShell. type de runbook Hello pour cet exemple est **PowerShell**, hello sont les autres options du graphique, flux de travail PowerShell et les flux de travail PowerShell graphique.

![panneau runbook][4]

### <a name="step-5"></a>Étape 5

Dans cette étape hello runbook est créé, hello, exemple de code suivant fournit que toutes les hello code nécessaire pour l’exemple hello. Hello d’éléments dans le code hello contenant \<valeur\> devez toobe remplacé par des valeurs hello à partir de votre abonnement.

Suivant de hello d’utilisation de code comme **enregistrer**

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a>Étape 6

Une fois les runbook hello est enregistré, une planification doit être lié de début de hello tooit tooautomate de runbook de hello. processus de hello toostart, cliquez sur **planification**.

![Étape 6][6]

## <a name="link-a-schedule-toohello-runbook"></a>Liez un runbook toohello de planification

Vous devez créer une planification. Cliquez sur **liez un runbook de tooyour planification**.

![Étape 7][7]

### <a name="step-1"></a>Étape 1

Sur hello **planification** panneau, cliquez sur **créer une planification**

![Étape 8][8]

### <a name="step-2"></a>Étape 2

Sur hello **nouvelle planification** panneau remplissez les informations de planification hello. les valeurs Hello qui peuvent être définies sont Bonjour suivant liste :

- **Nom** -nom convivial de hello de planification de hello.
- **Description** -obtenir une description de la planification de hello.
- **Démarre** -cette valeur est une combinaison de date et d’heure fuseau horaire qui composent les déclencheurs de planification hello temps hello.
- **Périodicité** -cette valeur détermine la répétition de planifications hello.  Les valeurs valides sont **Une fois** ou **Périodique**.
- **Répéter chaque** -intervalle de périodicité hello de planification hello en heures, jours, semaines ou mois.
- **Expiration du jeu de** -valeur de hello détermine si la planification de hello doit expirer ou non. Peut être défini trop**Oui** ou **non**. Une date et heure valides sont toobe fourni si vous choisissez Oui.

> [!NOTE]
> Si vous devez toohave un runbook à exécuter plus souvent que toutes les heures, plusieurs planifications doivent être créées à des intervalles différents (autrement dit, 15, 30, 45 minutes après l’heure de hello)

![Étape 9][9]

### <a name="step-3"></a>Étape 3 :

Cliquez sur Enregistrer toosave hello planification toohello runbook.

![Étape 10][10]

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous possédez des connaissances sur la façon de dépannage de l’Observateur réseau toointegrate avec Azure Automation, découvrez comment de captures de paquets de tootrigger sur les alertes de la machine virtuelle en vous rendant sur [créer une capture de paquets déclenchées alerte avec Azuredel’Observateurréseau](network-watcher-alert-triggered-packet-capture.md).

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
