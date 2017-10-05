---
title: " Résoudre les alertes de machine virtuelle Azure avec les runbooks Automation | Microsoft Docs"
description: "Cet article montre comment intégrer des alertes de machine virtuelle Azure à des runbooks Azure Automation et corriger automatiquement les problèmes"
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
ms.openlocfilehash: 738959b8e1ee5da989bb996d1ce8148cbf912781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="c3f28-103">Scénario Azure Automation - Résoudre des alertes de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="c3f28-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="c3f28-104">Azure Automation et Azure Virtual Machines disposent d’une nouvelle fonctionnalité qui vous permet de configurer des alertes de machine virtuelle (VM) afin d’exécuter des runbooks Automation.</span><span class="sxs-lookup"><span data-stu-id="c3f28-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span></span> <span data-ttu-id="c3f28-105">Cette nouvelle fonctionnalité vous permet de réaliser automatiquement une correction standard en réponse aux alertes de machine virtuelle, comme le redémarrage ou l’arrêt de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c3f28-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span></span>

<span data-ttu-id="c3f28-106">Auparavant, lors de la création d’une règle d’alerte de machine virtuelle, vous pouviez [spécifier un webhook Automation](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) sur un runbook pour exécuter le runbook dès le déclenchement de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="c3f28-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span></span> <span data-ttu-id="c3f28-107">Toutefois, cela vous oblige à créer le runbook, à créer le webhook pour le runbook, puis à copier et coller le webhook lors de la création de la règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="c3f28-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span></span> <span data-ttu-id="c3f28-108">Cette nouvelle version simplifie davantage le processus, car vous pouvez choisir directement un runbook à partir d’une liste lors de la création d’une règle d’alerte, et un compte Automation qui exécute le runbook ou crée facilement un compte.</span><span class="sxs-lookup"><span data-stu-id="c3f28-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span></span>

<span data-ttu-id="c3f28-109">Dans cet article, nous allons vous montrer à quel point il est simple de configurer une alerte de machine virtuelle Azure et un runbook Automation à exécuter chaque fois que l’alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="c3f28-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span></span> <span data-ttu-id="c3f28-110">Les exemples de scénarios incluent le redémarrage d’une machine virtuelle lorsque l’utilisation de la mémoire dépasse un certain seuil en raison de la fuite de mémoire d’une application de la machine virtuelle, ou l’arrêt d’une machine virtuelle lorsque le temps utilisateur processeur se trouve sous les 1 % pendant plus d’une heure et n’est pas utilisé.</span><span class="sxs-lookup"><span data-stu-id="c3f28-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="c3f28-111">Nous expliquerons également dans quelle mesure la création automatique d’un principal du service dans votre compte Automation simplifie l’utilisation des runbooks pour la correction des alertes Azure.</span><span class="sxs-lookup"><span data-stu-id="c3f28-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="c3f28-112">Créer une alerte sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c3f28-112">Create an alert on a VM</span></span>
<span data-ttu-id="c3f28-113">Procédez comme suit pour configurer une alerte permettant de lancer un runbook lorsque son seuil a été dépassé.</span><span class="sxs-lookup"><span data-stu-id="c3f28-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="c3f28-114">Cette version ne prend en charge que les machines virtuelles V2. La prise en charge des machines virtuelles classiques sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="c3f28-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="c3f28-115">Connectez-vous au portail Azure et cliquez sur **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="c3f28-115">Log in to the Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="c3f28-116">Sélectionnez une de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c3f28-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="c3f28-117">Le panneau du tableau de bord de la machine virtuelle s’affiche, ainsi que le panneau **Paramètres** à sa droite.</span><span class="sxs-lookup"><span data-stu-id="c3f28-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span></span>  
3. <span data-ttu-id="c3f28-118">À partir du panneau **Paramètres**, sous la section Surveillance, sélectionnez **Règles d’alerte**.</span><span class="sxs-lookup"><span data-stu-id="c3f28-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="c3f28-119">Dans le panneau **Règles d’alerte**, cliquez sur **Ajouter une alerte**.</span><span class="sxs-lookup"><span data-stu-id="c3f28-119">On the **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="c3f28-120">Le panneau **Ajouter une règle d’alerte** s’affiche. Vous pouvez y configurer les conditions de l’alerte et choisir l’une des options suivantes : envoyer un e-mail à une personne, utiliser un webhook pour transférer l’alerte vers un autre système et/ou exécuter un runbook Automation dans la tentative de réponse visant à résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="c3f28-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="c3f28-121">Configurer un runbook</span><span class="sxs-lookup"><span data-stu-id="c3f28-121">Configure a runbook</span></span>
<span data-ttu-id="c3f28-122">Pour configurer un runbook à exécuter lorsque le seuil d’alerte de la machine virtuelle est atteint, sélectionnez **Runbook Automation**.</span><span class="sxs-lookup"><span data-stu-id="c3f28-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="c3f28-123">Dans le panneau **Configurer le runbook** , vous pouvez sélectionner le runbook à exécuter et le compte Automation dans lequel exécuter le runbook.</span><span class="sxs-lookup"><span data-stu-id="c3f28-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span></span>

![Configurer un runbook Automation et créer un nouveau compte Automation](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="c3f28-125">Pour cette version, vous pouvez choisir un des trois runbooks fournis par le service : redémarrage, arrêt ou suppression de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c3f28-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="c3f28-126">La possibilité de sélectionner d’autres runbooks ou un de vos propres runbooks sera disponible dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c3f28-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Runbooks à sélectionner](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="c3f28-128">Après avoir sélectionné un des trois runbook disponibles, la liste déroulante **Compte Automation** à partir de laquelle vous pouvez sélectionner un compte Automation dans le contexte duquel le runbook s’exécutera, s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c3f28-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span></span> <span data-ttu-id="c3f28-129">Les runbooks doivent s’exécuter dans le contexte d’un [compte Automation](automation-security-overview.md) qui se trouve dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c3f28-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="c3f28-130">Vous pouvez sélectionner un compte Automation que vous avez déjà créé, ou avoir un nouveau compte Automation créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="c3f28-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="c3f28-131">Les runbooks fournis s’authentifient sur Azure à l’aide d’un principal du service.</span><span class="sxs-lookup"><span data-stu-id="c3f28-131">The runbooks that are provided authenticate to Azure using a service principal.</span></span> <span data-ttu-id="c3f28-132">Si vous choisissez d’exécuter le runbook dans un de vos comptes Automation existants, nous créerons automatiquement le principal du service pour vous.</span><span class="sxs-lookup"><span data-stu-id="c3f28-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span></span> <span data-ttu-id="c3f28-133">Si vous choisissez de créer un nouveau compte Automation, nous créerons automatiquement le compte et le principal du service.</span><span class="sxs-lookup"><span data-stu-id="c3f28-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span></span> <span data-ttu-id="c3f28-134">Dans les deux cas, deux ressources seront créées dans le compte Automation : une ressource de certificat nommée **AzureRunAsCertificate** et une ressource de connexion nommée **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="c3f28-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="c3f28-135">Les runbooks utiliseront **AzureRunAsConnection** pour s’authentifier avec Azure afin d’effectuer l’action de gestion par rapport à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c3f28-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c3f28-136">Le principal du service est créé dans le cadre de l’abonnement et attribué au rôle Collaborateur.</span><span class="sxs-lookup"><span data-stu-id="c3f28-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span></span> <span data-ttu-id="c3f28-137">Ce rôle est nécessaire pour que le compte soit autorisé à exécuter des runbooks Automation pour gérer les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="c3f28-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span></span>  <span data-ttu-id="c3f28-138">La création d’un compte Automation et/ou du principal du service est un événement unique.</span><span class="sxs-lookup"><span data-stu-id="c3f28-138">The creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="c3f28-139">Une fois qu’ils sont créés, vous pouvez utiliser ce compte pour exécuter des runbooks pour d’autres alertes de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="c3f28-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="c3f28-140">Quand vous cliquez sur **OK**, l’alerte est configurée. Si vous avez sélectionné l’option pour créer un nouveau compte Automation, celui-ci est créé avec le principal du service.</span><span class="sxs-lookup"><span data-stu-id="c3f28-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span></span>  <span data-ttu-id="c3f28-141">Cette opération peut prendre quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="c3f28-141">This can take a few seconds to complete.</span></span>  

![Runbook en cours de configuration](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="c3f28-143">Une fois la configuration terminée vous verrez le nom du runbook s’afficher dans le panneau **Ajouter une règle d’alerte** .</span><span class="sxs-lookup"><span data-stu-id="c3f28-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span></span>

![Runbook configuré](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="c3f28-145">Cliquez sur **OK** dans le panneau **Ajouter une règle d’alerte**. La règle d’alerte sera alors créée et activée si la machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c3f28-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="c3f28-146">Activer ou désactiver un runbook</span><span class="sxs-lookup"><span data-stu-id="c3f28-146">Enable or disable a runbook</span></span>
<span data-ttu-id="c3f28-147">Si un runbook est configuré pour une alerte, vous pouvez le désactiver sans supprimer la configuration du runbook.</span><span class="sxs-lookup"><span data-stu-id="c3f28-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span></span> <span data-ttu-id="c3f28-148">Cela permet de laisser l’alerte s’exécuter et peut-être de tester certaines des règles d’alerte, puis de réactiver ultérieurement le runbook.</span><span class="sxs-lookup"><span data-stu-id="c3f28-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="c3f28-149">Créer un runbook fonctionnant avec une alerte Azure</span><span class="sxs-lookup"><span data-stu-id="c3f28-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="c3f28-150">Lorsque vous choisissez un runbook dans le cadre d’une règle d’alerte Azure, le runbook doit contenir une logique pour gérer les données d’alerte qui lui sont transmises.</span><span class="sxs-lookup"><span data-stu-id="c3f28-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span></span>  <span data-ttu-id="c3f28-151">Lorsqu’un runbook est configuré dans une règle d’alerte, un webhook est créé pour le runbook : ce webhook est ensuite utilisé pour démarrer le runbook chaque fois que l’alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="c3f28-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span></span>  <span data-ttu-id="c3f28-152">L’appel réel pour démarrer le runbook est une demande HTTP POST vers l’URL du webhook.</span><span class="sxs-lookup"><span data-stu-id="c3f28-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span></span> <span data-ttu-id="c3f28-153">Le corps de la demande POST contient un objet au format JSON qui contient les propriétés utiles relatives à l’alerte.</span><span class="sxs-lookup"><span data-stu-id="c3f28-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span></span>  <span data-ttu-id="c3f28-154">Comme vous pouvez le voir ci-dessous, les données d’alerte contiennent des détails comme subscriptionID, resourceGroupName, resourceName, et resourceType.</span><span class="sxs-lookup"><span data-stu-id="c3f28-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="c3f28-155">Exemple de données d’alerte</span><span class="sxs-lookup"><span data-stu-id="c3f28-155">Example of Alert data</span></span>
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

<span data-ttu-id="c3f28-156">Lorsque le service webhook Automation reçoit la requête HTTP POST, il extrait les données d’alerte et les transmet au runbook dans le paramètre d’entrée WebhookData du runbook.</span><span class="sxs-lookup"><span data-stu-id="c3f28-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span></span>  <span data-ttu-id="c3f28-157">Voici un exemple de runbook qui montre comment utiliser le paramètre WebhookData et extraire les données d’alerte et les utiliser pour gérer la ressource Azure qui a déclenché l’alerte.</span><span class="sxs-lookup"><span data-stu-id="c3f28-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="c3f28-158">Exemple de runbook</span><span class="sxs-lookup"><span data-stu-id="c3f28-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response to an Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get the data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that the alert status is 'Activated' (alert condition went from false to true)
    # and not 'Resolved' (alert condition went from true to false)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get the info needed to identify the VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is the expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate to Azure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart the VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # The alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant to be started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="c3f28-159">Résumé</span><span class="sxs-lookup"><span data-stu-id="c3f28-159">Summary</span></span>
<span data-ttu-id="c3f28-160">Lorsque vous configurez une alerte sur une machine virtuelle Azure, vous avez maintenant la possibilité de configurer facilement un runbook Automation pour qu’il effectue automatiquement une action corrective au déclenchement de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="c3f28-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span></span> <span data-ttu-id="c3f28-161">Pour cette version, vous pouvez choisir à partir des runbooks, de redémarrer, d’arrêter ou de supprimer une machine virtuelle en fonction de votre scénario d’alerte.</span><span class="sxs-lookup"><span data-stu-id="c3f28-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="c3f28-162">Ceci n’est qu’un avant-goût des scénarios d’activation dans lesquels vous contrôlez les actions (notification, dépannage, correction) qui seront entreprises automatiquement au déclenchement d’une alerte.</span><span class="sxs-lookup"><span data-stu-id="c3f28-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3f28-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3f28-163">Next Steps</span></span>
* <span data-ttu-id="c3f28-164">Pour une prise en main des Runbooks graphiques, consultez [Mon premier Runbook graphique](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="c3f28-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="c3f28-165">Pour une prise en main des Runbooks de workflow PowerShell, consultez [Mon premier Runbook PowerShell Workflow](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="c3f28-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="c3f28-166">Pour en savoir plus sur les types de Runbook, leurs avantages et leurs limites, consultez [Types de Runbooks Azure Automation](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="c3f28-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

