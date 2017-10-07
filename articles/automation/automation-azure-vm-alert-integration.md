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
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a>Scénario Azure Automation - Résoudre des alertes de machine virtuelle Azure
Azure Automation et les Machines virtuelles Azure ont publié une nouvelle fonctionnalité qui vous runbooks d’automatisation toorun alertes tooconfigure Machine virtuelle (VM). Cette nouvelle fonctionnalité vous permet de tooautomatically effectuer la mise à jour standard dans les alertes tooVM de réponse, telles que le redémarrage ou arrêt hello machine virtuelle.

Auparavant, lors de la création de règle d’alerte de machine virtuelle vous pouviez trop[spécifier un webhook Automation](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) runbook tooa dans l’ordre toorun hello runbook dès que hello alerte déclenchée. Toutefois, cela nécessaire travail hello de toodo de création hello runbook, création webhook hello hello runbook, puis en copiant et collant hello webhook lors de la création d’une règle d’alerte. Avec cette nouvelle version, les processus hello sont beaucoup plus facile, car vous pouvez directement choisir un runbook à partir d’une liste lors de la création d’une règle d’alerte, et vous pouvez choisir un compte Automation qui exécutera hello runbook ou facilement créer un compte.

Dans cet article, nous vous montrer comment il est facile tooset d’une alerte de machine virtuelle Azure et configurer un toorun de runbook Automation chaque fois que hello alerte se déclenche. Exemples de scénarios incluent le redémarrage d’une machine virtuelle lors de l’utilisation de la mémoire hello dépasse un seuil en raison de l’application tooan sur hello machine virtuelle avec une fuite de mémoire ou l’arrêt d’une machine virtuelle lorsque du temps utilisateur hello du processeur est inférieure à 1 % pour la dernière heure et n’est pas en cours d’utilisation. Nous allons également expliquer comment hello automatisé à la création d’un principal de service dans votre automatisation compte simplifie l’utilisation de hello des runbooks dans Azure alerte mise à jour.

## <a name="create-an-alert-on-a-vm"></a>Créer une alerte sur une machine virtuelle
Effectuer hello suivant les étapes tooconfigure une alerte toolaunch un runbook lorsque le seuil a été rencontrée.

> [!NOTE]
> Cette version ne prend en charge que les machines virtuelles V2. La prise en charge des machines virtuelles classiques sera bientôt disponible.  
> 
> 

1. Connectez-vous à toohello portail Azure, puis cliquez sur **virtuels**.  
2. Sélectionnez une de vos machines virtuelles.  Hello Panneau de tableau de bord de machine virtuelle s’affichera et hello **paramètres** droite tooits de panneau.  
3. À partir de hello **paramètres** panneau, sous hello section surveillance, sélectionnez **règles d’alerte**.
4. Sur hello **règles d’alerte** panneau, cliquez sur **ajouter une alerte**.

S’affiche, hello et **ajouter une règle d’alerte** panneau, où vous pouvez configurer des conditions de hello pour l’alerte de hello et choisir entre une ou l’ensemble de ces options : envoyer par courrier électronique toosomeone, utilisez un système webhook tooforward hello alerte tooanother, et/ou problème de réponse tentative tooremediate hello, exécuter un runbook Automation.

## <a name="configure-a-runbook"></a>Configurer un runbook
tooconfigure un toorun runbook lorsque le seuil d’alerte de machine virtuelle hello est remplie, sélectionnez **Runbook Automation**. Bonjour **configurer runbook** panneau, vous pouvez sélectionner hello runbook toorun et runbook hello Automation compte toorun hello dans.

![Configurer un runbook Automation et créer un nouveau compte Automation](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> Pour cette version, vous pouvez choisir parmi trois procédures opérationnelles qui fournit des services de hello – redémarrer la machine virtuelle, arrêtez la machine virtuelle ou supprimer la machine virtuelle (supprimer).  Hello capacité tooselect autres runbooks ou un de vos propres runbooks sera disponible dans une version ultérieure.
> 
> 

![Toochoose de runbooks à partir de](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

Une fois que vous sélectionnez une des procédures opérationnelles disponibles de hello trois, hello **compte Automation** liste déroulante s’affiche et vous pouvez sélectionner un objet automation compte hello runbook s’exécutera en tant que. Procédures opérationnelles doivent toorun dans le contexte de hello d’un [compte Automation](automation-security-overview.md) qui se trouve dans votre abonnement Azure. Vous pouvez sélectionner un compte Automation que vous avez déjà créé, ou avoir un nouveau compte Automation créé pour vous.

procédures opérationnelles Hello fournis authentifient tooAzure à l’aide d’un principal de service. Si vous choisissez toorun hello runbook dans un de vos comptes Automation existants, nous crée automatiquement le service de hello principal pour vous. Si vous choisissez un compte Automation à toocreate, puis nous crée automatiquement le compte de hello et principal du service hello. Dans les deux cas, les deux éléments multimédias seront également créées hello compte Automation – une ressource de certificat nommée **AzureRunAsCertificate** et une ressource de connexion nommée **AzureRunAsConnection**. les runbooks Hello utilisera **AzureRunAsConnection** tooauthenticate avec Azure dans l’action de gestion ordre tooperform hello contre hello machine virtuelle.

> [!NOTE]
> principal du service Hello est créé dans l’étendue de l’abonnement hello et rôle de collaborateur hello est attribué. Ce rôle est nécessaire pour l’autorisation hello compte toohave toorun Automation runbooks toomanage machines virtuelles Azure.  Hello la création d’un compte de l’automate et/ou d’un principal de service est un événement unique. Une fois qu’elles sont créées, vous pouvez utiliser que le compte toorun runbook d’autres alertes de la machine virtuelle Azure.
> 
> 

Lorsque vous cliquez sur **OK** hello alerte est configurée et si vous avez sélectionné hello option toocreate un compte Automation, il est créé en même temps que le principal du service hello.  Cette opération peut prendre quelques secondes toocomplete.  

![Runbook en cours de configuration](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

Après la configuration de hello nom hello de hello runbook s’affiche s’affichent dans hello **ajouter une règle d’alerte** panneau.

![Runbook configuré](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

Cliquez sur **OK** Bonjour **ajouter une règle d’alerte** lame et hello règle d’alerte est créé et l’activer si l’ordinateur virtuel de hello est en cours d’exécution.

### <a name="enable-or-disable-a-runbook"></a>Activer ou désactiver un runbook
Si vous disposez d’un runbook configuré pour une alerte, vous pouvez le désactiver sans supprimer la configuration du runbook hello. Cela vous permet d’alerte de hello tookeep en cours d’exécution et peut-être tester certaines des règles d’alerte hello et alors réactiver ultérieurement hello runbook.

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a>Créer un runbook fonctionnant avec une alerte Azure
Lorsque vous choisissez un runbook dans le cadre d’une règle d’alerte Azure, hello runbook doit logique toohave toomanage hello données d’alerte qui sont passées à tooit.  Lorsqu’un runbook est configuré dans une règle d’alerte, un webhook est créé pour hello runbook ; Ce webhook est ensuite utilisé toostart hello runbook chaque heure hello alerte les déclencheurs.  Hello appel réel toostart hello runbook est une demande HTTP POST toohello l’URL du webhook. corps Hello de requête de publication hello contient un objet JSON-formatée qui contient l’alerte connexe toohello de propriétés utiles.  Comme vous pouvez le voir ci-dessous, les données d’alerte hello contient des détails tels que l’ID d’abonnement, resourceGroupName, resourceName et resourceType.

### <a name="example-of-alert-data"></a>Exemple de données d’alerte
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

Lorsque hello service d’automatisation de webhook reçoit hello HTTP POST il extrait les données d’alerte hello et transmet toohello runbook dans le paramètre d’entrée du runbook WebhookData hello.  Voici un exemple de runbook qui montre comment toouse hello WebhookData paramètre et extraire des données d’alerte hello et utilisez-le toomanage hello ressource Azure qui a déclenché l’alerte de hello.

### <a name="example-runbook"></a>Exemple de runbook
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

## <a name="summary"></a>Résumé
Lorsque vous configurez une alerte sur une machine virtuelle Azure, vous pouvez désormais hello capacité tooeasily configurer un objet Automation runbook tooautomatically effectuer des mesures correctives lorsque hello alerte se déclenche. Pour cette version, vous pouvez choisir parmi les runbooks toorestart, arrêter ou supprimer une machine virtuelle en fonction de votre scénario d’alerte. Il s’agit de début hello simplement d’activer des scénarios où vous contrôlez les actions de hello (notification, dépannage, mise à jour) qui seront entreprises automatiquement lorsqu’une alerte se déclenche.

## <a name="next-steps"></a>Étapes suivantes
* tooget main runbooks graphiques, consultez [mon premier runbook graphique](automation-first-runbook-graphical.md)
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md)
* toolearn en savoir plus sur les types de runbook, leurs avantages et les limitations, consultez [types de runbook Azure Automation](automation-runbook-types.md)

