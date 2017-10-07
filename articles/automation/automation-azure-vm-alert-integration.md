---
title: "Corriger les alertes de machine virtuelle Azure avec des Runbooks Automation aaa » | Documents Microsoft »"
description: "Cet article montre comment les alertes toointegrate Machine virtuelle Azure avec des runbooks Azure Automation et corriger automatiquement les problèmes"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="39b14-103">Scénario Azure Automation - Résoudre des alertes de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="39b14-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="39b14-104">Azure Automation et les Machines virtuelles Azure ont publié une nouvelle fonctionnalité qui vous runbooks d’automatisation toorun alertes tooconfigure Machine virtuelle (VM).</span><span class="sxs-lookup"><span data-stu-id="39b14-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="39b14-105">Cette nouvelle fonctionnalité vous permet de tooautomatically effectuer la mise à jour standard dans les alertes tooVM de réponse, telles que le redémarrage ou arrêt hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="39b14-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="39b14-106">Auparavant, lors de la création de règle d’alerte de machine virtuelle vous pouviez trop[spécifier un webhook Automation](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) runbook tooa dans l’ordre toorun hello runbook dès que hello alerte déclenchée.</span><span class="sxs-lookup"><span data-stu-id="39b14-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="39b14-107">Toutefois, cela nécessaire travail hello de toodo de création hello runbook, création webhook hello hello runbook, puis en copiant et collant hello webhook lors de la création d’une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="39b14-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="39b14-108">Avec cette nouvelle version, les processus hello sont beaucoup plus facile, car vous pouvez directement choisir un runbook à partir d’une liste lors de la création d’une règle d’alerte, et vous pouvez choisir un compte Automation qui exécutera hello runbook ou facilement créer un compte.</span><span class="sxs-lookup"><span data-stu-id="39b14-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="39b14-109">Dans cet article, nous vous montrer comment il est facile tooset d’une alerte de machine virtuelle Azure et configurer un toorun de runbook Automation chaque fois que hello alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="39b14-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="39b14-110">Exemples de scénarios incluent le redémarrage d’une machine virtuelle lors de l’utilisation de la mémoire hello dépasse un seuil en raison de l’application tooan sur hello machine virtuelle avec une fuite de mémoire ou l’arrêt d’une machine virtuelle lorsque du temps utilisateur hello du processeur est inférieure à 1 % pour la dernière heure et n’est pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="39b14-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="39b14-111">Nous allons également expliquer comment hello automatisé à la création d’un principal de service dans votre automatisation compte simplifie l’utilisation de hello des runbooks dans Azure alerte mise à jour.</span><span class="sxs-lookup"><span data-stu-id="39b14-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="39b14-112">Créer une alerte sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="39b14-112">Create an alert on a VM</span></span>
<span data-ttu-id="39b14-113">Effectuer hello suivant les étapes tooconfigure une alerte toolaunch un runbook lorsque le seuil a été rencontrée.</span><span class="sxs-lookup"><span data-stu-id="39b14-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="39b14-114">Cette version ne prend en charge que les machines virtuelles V2. La prise en charge des machines virtuelles classiques sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="39b14-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="39b14-115">Connectez-vous à toohello portail Azure, puis cliquez sur **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="39b14-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="39b14-116">Sélectionnez une de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="39b14-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="39b14-117">Hello Panneau de tableau de bord de machine virtuelle s’affichera et hello **paramètres** droite tooits de panneau.</span><span class="sxs-lookup"><span data-stu-id="39b14-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="39b14-118">À partir de hello **paramètres** panneau, sous hello section surveillance, sélectionnez **règles d’alerte**.</span><span class="sxs-lookup"><span data-stu-id="39b14-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="39b14-119">Sur hello **règles d’alerte** panneau, cliquez sur **ajouter une alerte**.</span><span class="sxs-lookup"><span data-stu-id="39b14-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="39b14-120">S’affiche, hello et **ajouter une règle d’alerte** panneau, où vous pouvez configurer des conditions de hello pour l’alerte de hello et choisir entre une ou l’ensemble de ces options : envoyer par courrier électronique toosomeone, utilisez un système webhook tooforward hello alerte tooanother, et/ou problème de réponse tentative tooremediate hello, exécuter un runbook Automation.</span><span class="sxs-lookup"><span data-stu-id="39b14-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="39b14-121">Configurer un runbook</span><span class="sxs-lookup"><span data-stu-id="39b14-121">Configure a runbook</span></span>
<span data-ttu-id="39b14-122">tooconfigure un toorun runbook lorsque le seuil d’alerte de machine virtuelle hello est remplie, sélectionnez **Runbook Automation**.</span><span class="sxs-lookup"><span data-stu-id="39b14-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="39b14-123">Bonjour **configurer runbook** panneau, vous pouvez sélectionner hello runbook toorun et runbook hello Automation compte toorun hello dans.</span><span class="sxs-lookup"><span data-stu-id="39b14-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![Configurer un runbook Automation et créer un nouveau compte Automation](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="39b14-125">Pour cette version, vous pouvez choisir parmi trois procédures opérationnelles qui fournit des services de hello – redémarrer la machine virtuelle, arrêtez la machine virtuelle ou supprimer la machine virtuelle (supprimer).</span><span class="sxs-lookup"><span data-stu-id="39b14-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="39b14-126">Hello capacité tooselect autres runbooks ou un de vos propres runbooks sera disponible dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="39b14-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Toochoose de runbooks à partir de](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="39b14-128">Une fois que vous sélectionnez une des procédures opérationnelles disponibles de hello trois, hello **compte Automation** liste déroulante s’affiche et vous pouvez sélectionner un objet automation compte hello runbook s’exécutera en tant que.</span><span class="sxs-lookup"><span data-stu-id="39b14-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="39b14-129">Procédures opérationnelles doivent toorun dans le contexte de hello d’un [compte Automation](automation-security-overview.md) qui se trouve dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="39b14-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="39b14-130">Vous pouvez sélectionner un compte Automation que vous avez déjà créé, ou avoir un nouveau compte Automation créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="39b14-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="39b14-131">procédures opérationnelles Hello fournis authentifient tooAzure à l’aide d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="39b14-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="39b14-132">Si vous choisissez toorun hello runbook dans un de vos comptes Automation existants, nous crée automatiquement le service de hello principal pour vous.</span><span class="sxs-lookup"><span data-stu-id="39b14-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="39b14-133">Si vous choisissez un compte Automation à toocreate, puis nous crée automatiquement le compte de hello et principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="39b14-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="39b14-134">Dans les deux cas, les deux éléments multimédias seront également créées hello compte Automation – une ressource de certificat nommée **AzureRunAsCertificate** et une ressource de connexion nommée **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="39b14-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="39b14-135">les runbooks Hello utilisera **AzureRunAsConnection** tooauthenticate avec Azure dans l’action de gestion ordre tooperform hello contre hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="39b14-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="39b14-136">principal du service Hello est créé dans l’étendue de l’abonnement hello et rôle de collaborateur hello est attribué.</span><span class="sxs-lookup"><span data-stu-id="39b14-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="39b14-137">Ce rôle est nécessaire pour l’autorisation hello compte toohave toorun Automation runbooks toomanage machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="39b14-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="39b14-138">Hello la création d’un compte de l’automate et/ou d’un principal de service est un événement unique.</span><span class="sxs-lookup"><span data-stu-id="39b14-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="39b14-139">Une fois qu’elles sont créées, vous pouvez utiliser que le compte toorun runbook d’autres alertes de la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="39b14-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="39b14-140">Lorsque vous cliquez sur **OK** hello alerte est configurée et si vous avez sélectionné hello option toocreate un compte Automation, il est créé en même temps que le principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="39b14-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="39b14-141">Cette opération peut prendre quelques secondes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="39b14-141">This can take a few seconds toocomplete.</span></span>  

![Runbook en cours de configuration](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="39b14-143">Après la configuration de hello nom hello de hello runbook s’affiche s’affichent dans hello **ajouter une règle d’alerte** panneau.</span><span class="sxs-lookup"><span data-stu-id="39b14-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![Runbook configuré](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="39b14-145">Cliquez sur **OK** Bonjour **ajouter une règle d’alerte** lame et hello règle d’alerte est créé et l’activer si l’ordinateur virtuel de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="39b14-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="39b14-146">Activer ou désactiver un runbook</span><span class="sxs-lookup"><span data-stu-id="39b14-146">Enable or disable a runbook</span></span>
<span data-ttu-id="39b14-147">Si vous disposez d’un runbook configuré pour une alerte, vous pouvez le désactiver sans supprimer la configuration du runbook hello.</span><span class="sxs-lookup"><span data-stu-id="39b14-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="39b14-148">Cela vous permet d’alerte de hello tookeep en cours d’exécution et peut-être tester certaines des règles d’alerte hello et alors réactiver ultérieurement hello runbook.</span><span class="sxs-lookup"><span data-stu-id="39b14-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="39b14-149">Créer un runbook fonctionnant avec une alerte Azure</span><span class="sxs-lookup"><span data-stu-id="39b14-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="39b14-150">Lorsque vous choisissez un runbook dans le cadre d’une règle d’alerte Azure, hello runbook doit logique toohave toomanage hello données d’alerte qui sont passées à tooit.</span><span class="sxs-lookup"><span data-stu-id="39b14-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="39b14-151">Lorsqu’un runbook est configuré dans une règle d’alerte, un webhook est créé pour hello runbook ; Ce webhook est ensuite utilisé toostart hello runbook chaque heure hello alerte les déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="39b14-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="39b14-152">Hello appel réel toostart hello runbook est une demande HTTP POST toohello l’URL du webhook.</span><span class="sxs-lookup"><span data-stu-id="39b14-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="39b14-153">corps Hello de requête de publication hello contient un objet JSON-formatée qui contient l’alerte connexe toohello de propriétés utiles.</span><span class="sxs-lookup"><span data-stu-id="39b14-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="39b14-154">Comme vous pouvez le voir ci-dessous, les données d’alerte hello contient des détails tels que l’ID d’abonnement, resourceGroupName, resourceName et resourceType.</span><span class="sxs-lookup"><span data-stu-id="39b14-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="39b14-155">Exemple de données d’alerte</span><span class="sxs-lookup"><span data-stu-id="39b14-155">Example of Alert data</span></span>
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

<span data-ttu-id="39b14-156">Lorsque hello service d’automatisation de webhook reçoit hello HTTP POST il extrait les données d’alerte hello et transmet toohello runbook dans le paramètre d’entrée du runbook WebhookData hello.</span><span class="sxs-lookup"><span data-stu-id="39b14-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="39b14-157">Voici un exemple de runbook qui montre comment toouse hello WebhookData paramètre et extraire des données d’alerte hello et utilisez-le toomanage hello ressource Azure qui a déclenché l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="39b14-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="39b14-158">Exemple de runbook</span><span class="sxs-lookup"><span data-stu-id="39b14-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="39b14-159">Résumé</span><span class="sxs-lookup"><span data-stu-id="39b14-159">Summary</span></span>
<span data-ttu-id="39b14-160">Lorsque vous configurez une alerte sur une machine virtuelle Azure, vous pouvez désormais hello capacité tooeasily configurer un objet Automation runbook tooautomatically effectuer des mesures correctives lorsque hello alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="39b14-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="39b14-161">Pour cette version, vous pouvez choisir parmi les runbooks toorestart, arrêter ou supprimer une machine virtuelle en fonction de votre scénario d’alerte.</span><span class="sxs-lookup"><span data-stu-id="39b14-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="39b14-162">Il s’agit de début hello simplement d’activer des scénarios où vous contrôlez les actions de hello (notification, dépannage, mise à jour) qui seront entreprises automatiquement lorsqu’une alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="39b14-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39b14-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39b14-163">Next Steps</span></span>
* <span data-ttu-id="39b14-164">tooget main runbooks graphiques, consultez [mon premier runbook graphique](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="39b14-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="39b14-165">tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="39b14-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="39b14-166">toolearn en savoir plus sur les types de runbook, leurs avantages et les limitations, consultez [types de runbook Azure Automation](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="39b14-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

