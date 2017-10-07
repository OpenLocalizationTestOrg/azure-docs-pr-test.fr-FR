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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="74531-103">Surveiller les passerelles VPN à l’aide de la résolution des problèmes Network Watcher</span><span class="sxs-lookup"><span data-stu-id="74531-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="74531-104">Obtenir des informations détaillées sur les performances de votre réseau est toocustomers de services fiables tooprovide critiques.</span><span class="sxs-lookup"><span data-stu-id="74531-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="74531-105">Il est donc critique toodetect conditions de panne réseau rapidement et prendre la condition de panne d’une action corrective toomitigate hello.</span><span class="sxs-lookup"><span data-stu-id="74531-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="74531-106">Azure Automation vous permet de tooimplement et exécuter une tâche de manière par programmation via des procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="74531-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="74531-107">L’utilisation d’Azure Automation crée un environnement parfait pour l’exécution d’une surveillance réseau proactive et continue et d’alertes.</span><span class="sxs-lookup"><span data-stu-id="74531-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="74531-108">Scénario</span><span class="sxs-lookup"><span data-stu-id="74531-108">Scenario</span></span>

<span data-ttu-id="74531-109">scénario Hello Bonjour suivant l’image est une application multicouche, avec établie à l’aide d’une passerelle VPN et un tunnel de connectivité du site.</span><span class="sxs-lookup"><span data-stu-id="74531-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="74531-110">Assurer hello que passerelle VPN est activé et en cours d’exécution sont performances des applications critiques toohello.</span><span class="sxs-lookup"><span data-stu-id="74531-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="74531-111">Vous pouvez créer un runbook avec un toocheck de script pour l’état de la connexion de tunnel VPN de hello, à l’aide de hello API de résolution des problèmes de ressources toocheck pour l’état de la connexion tunnel.</span><span class="sxs-lookup"><span data-stu-id="74531-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="74531-112">Si l’état de hello n’est pas intègre, un déclencheur de courrier électronique est envoyé à tooadministrators.</span><span class="sxs-lookup"><span data-stu-id="74531-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![Exemple de scénario][scenario]

<span data-ttu-id="74531-114">Ce scénario va :</span><span class="sxs-lookup"><span data-stu-id="74531-114">This scenario will:</span></span>

- <span data-ttu-id="74531-115">Créer un hello appelant runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` état de la connexion tootroubleshoot applet de commande</span><span class="sxs-lookup"><span data-stu-id="74531-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="74531-116">Liez un runbook toohello de planification</span><span class="sxs-lookup"><span data-stu-id="74531-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="74531-117">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="74531-117">Before you begin</span></span>

<span data-ttu-id="74531-118">Avant de commencer ce scénario, vous devez disposer de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="74531-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="74531-119">Un compte Azure Automation dans Azure.</span><span class="sxs-lookup"><span data-stu-id="74531-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="74531-120">Assurez-vous que le compte d’automatisation hello a des modules de dernière hello et a également le module de AzureRM.Network hello.</span><span class="sxs-lookup"><span data-stu-id="74531-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="74531-121">module de AzureRM.Network Hello n’est disponible dans la galerie des modules hello si vous avez besoin de tooadd il compte automation de tooyour.</span><span class="sxs-lookup"><span data-stu-id="74531-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="74531-122">Vous devez avoir configuré des informations d’identification dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="74531-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="74531-123">Pour en savoir plus, consultez l’article [Sécurité dans Azure Automation](../automation/automation-security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74531-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="74531-124">Un serveur SMTP valide (Office 365, votre messagerie locale ou une autre) et les informations d’identification définies dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="74531-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="74531-125">Une passerelle de réseau virtuel configurée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="74531-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="74531-126">Un compte de stockage existant avec un hello toostore de conteneur existant se connecte.</span><span class="sxs-lookup"><span data-stu-id="74531-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="74531-127">infrastructure Hello mentionné dans hello précédant l’image est à titre d’illustration et ne sont pas créés aux étapes hello contenues dans cet article.</span><span class="sxs-lookup"><span data-stu-id="74531-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="74531-128">Créer des runbook de hello</span><span class="sxs-lookup"><span data-stu-id="74531-128">Create hello runbook</span></span>

<span data-ttu-id="74531-129">exemple de Hello première étape tooconfiguring hello est toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="74531-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="74531-130">Cet exemple utilise un compte d’identification.</span><span class="sxs-lookup"><span data-stu-id="74531-130">This example uses a run-as account.</span></span> <span data-ttu-id="74531-131">toolearn sur les comptes d’identification, visitez [Runbooks de s’authentifier avec un compte d’identification Azure](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="74531-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="74531-132">Étape 1</span><span class="sxs-lookup"><span data-stu-id="74531-132">Step 1</span></span>

<span data-ttu-id="74531-133">Accédez tooAzure Automation Bonjour [portail Azure](https://portal.azure.com) et cliquez sur **Runbooks**</span><span class="sxs-lookup"><span data-stu-id="74531-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![présentation du compte Automation][1]

### <a name="step-2"></a><span data-ttu-id="74531-135">Étape 2</span><span class="sxs-lookup"><span data-stu-id="74531-135">Step 2</span></span>

<span data-ttu-id="74531-136">Cliquez sur **ajouter un runbook** toostart des processus de création de hello de hello runbook.</span><span class="sxs-lookup"><span data-stu-id="74531-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![panneau de runbooks][2]

### <a name="step-3"></a><span data-ttu-id="74531-138">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="74531-138">Step 3</span></span>

<span data-ttu-id="74531-139">Sous **création rapide**, cliquez sur **créer un runbook** toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="74531-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![panneau ajouter un runbook][3]

### <a name="step-4"></a><span data-ttu-id="74531-141">Étape 4</span><span class="sxs-lookup"><span data-stu-id="74531-141">Step 4</span></span>

<span data-ttu-id="74531-142">Dans cette étape, nous nommez les runbook hello, dans l’exemple de hello, il est appelé **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="74531-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="74531-143">Il est important de toogive hello runbook un nom descriptif et recommandé de lui donner un nom qui suit les normes d’affectation de noms standards PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74531-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="74531-144">type de runbook Hello pour cet exemple est **PowerShell**, hello sont les autres options du graphique, flux de travail PowerShell et les flux de travail PowerShell graphique.</span><span class="sxs-lookup"><span data-stu-id="74531-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![panneau runbook][4]

### <a name="step-5"></a><span data-ttu-id="74531-146">Étape 5</span><span class="sxs-lookup"><span data-stu-id="74531-146">Step 5</span></span>

<span data-ttu-id="74531-147">Dans cette étape hello runbook est créé, hello, exemple de code suivant fournit que toutes les hello code nécessaire pour l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="74531-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="74531-148">Hello d’éléments dans le code hello contenant \<valeur\> devez toobe remplacé par des valeurs hello à partir de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="74531-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="74531-149">Suivant de hello d’utilisation de code comme **enregistrer**</span><span class="sxs-lookup"><span data-stu-id="74531-149">Use hello following code as click **Save**</span></span>

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

### <a name="step-6"></a><span data-ttu-id="74531-150">Étape 6</span><span class="sxs-lookup"><span data-stu-id="74531-150">Step 6</span></span>

<span data-ttu-id="74531-151">Une fois les runbook hello est enregistré, une planification doit être lié de début de hello tooit tooautomate de runbook de hello.</span><span class="sxs-lookup"><span data-stu-id="74531-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="74531-152">processus de hello toostart, cliquez sur **planification**.</span><span class="sxs-lookup"><span data-stu-id="74531-152">toostart hello process, click **Schedule**.</span></span>

![Étape 6][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="74531-154">Liez un runbook toohello de planification</span><span class="sxs-lookup"><span data-stu-id="74531-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="74531-155">Vous devez créer une planification.</span><span class="sxs-lookup"><span data-stu-id="74531-155">A new schedule must be created.</span></span> <span data-ttu-id="74531-156">Cliquez sur **liez un runbook de tooyour planification**.</span><span class="sxs-lookup"><span data-stu-id="74531-156">Click **Link a schedule tooyour runbook**.</span></span>

![Étape 7][7]

### <a name="step-1"></a><span data-ttu-id="74531-158">Étape 1</span><span class="sxs-lookup"><span data-stu-id="74531-158">Step 1</span></span>

<span data-ttu-id="74531-159">Sur hello **planification** panneau, cliquez sur **créer une planification**</span><span class="sxs-lookup"><span data-stu-id="74531-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![Étape 8][8]

### <a name="step-2"></a><span data-ttu-id="74531-161">Étape 2</span><span class="sxs-lookup"><span data-stu-id="74531-161">Step 2</span></span>

<span data-ttu-id="74531-162">Sur hello **nouvelle planification** panneau remplissez les informations de planification hello.</span><span class="sxs-lookup"><span data-stu-id="74531-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="74531-163">les valeurs Hello qui peuvent être définies sont Bonjour suivant liste :</span><span class="sxs-lookup"><span data-stu-id="74531-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="74531-164">**Nom** -nom convivial de hello de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="74531-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="74531-165">**Description** -obtenir une description de la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="74531-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="74531-166">**Démarre** -cette valeur est une combinaison de date et d’heure fuseau horaire qui composent les déclencheurs de planification hello temps hello.</span><span class="sxs-lookup"><span data-stu-id="74531-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="74531-167">**Périodicité** -cette valeur détermine la répétition de planifications hello.</span><span class="sxs-lookup"><span data-stu-id="74531-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="74531-168">Les valeurs valides sont **Une fois** ou **Périodique**.</span><span class="sxs-lookup"><span data-stu-id="74531-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="74531-169">**Répéter chaque** -intervalle de périodicité hello de planification hello en heures, jours, semaines ou mois.</span><span class="sxs-lookup"><span data-stu-id="74531-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="74531-170">**Expiration du jeu de** -valeur de hello détermine si la planification de hello doit expirer ou non.</span><span class="sxs-lookup"><span data-stu-id="74531-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="74531-171">Peut être défini trop**Oui** ou **non**.</span><span class="sxs-lookup"><span data-stu-id="74531-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="74531-172">Une date et heure valides sont toobe fourni si vous choisissez Oui.</span><span class="sxs-lookup"><span data-stu-id="74531-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="74531-173">Si vous devez toohave un runbook à exécuter plus souvent que toutes les heures, plusieurs planifications doivent être créées à des intervalles différents (autrement dit, 15, 30, 45 minutes après l’heure de hello)</span><span class="sxs-lookup"><span data-stu-id="74531-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![Étape 9][9]

### <a name="step-3"></a><span data-ttu-id="74531-175">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="74531-175">Step 3</span></span>

<span data-ttu-id="74531-176">Cliquez sur Enregistrer toosave hello planification toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="74531-176">Click Save toosave hello schedule toohello runbook.</span></span>

![Étape 10][10]

## <a name="next-steps"></a><span data-ttu-id="74531-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74531-178">Next steps</span></span>

<span data-ttu-id="74531-179">Maintenant que vous possédez des connaissances sur la façon de dépannage de l’Observateur réseau toointegrate avec Azure Automation, découvrez comment de captures de paquets de tootrigger sur les alertes de la machine virtuelle en vous rendant sur [créer une capture de paquets déclenchées alerte avec Azuredel’Observateurréseau](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="74531-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
