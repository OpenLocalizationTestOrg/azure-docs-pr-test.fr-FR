---
title: "aaaVertically groupes identiques de mise à l’échelle de machine virtuelle Azure | Documents Microsoft"
description: "Comment toovertically l’échelle d’un ordinateur virtuel dans les alertes de réponse de toomonitoring avec Azure Automation"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>Mise à l’échelle verticale avec des jeux de mise à l’échelle de machine virtuelle
Cet article décrit comment toovertically l’échelle Azure [machines virtuelles identiques](https://azure.microsoft.com/services/virtual-machine-scale-sets/) avec ou sans la préparation. Vertical mise à l’échelle de machines virtuelles qui ne sont pas identiques, consultez trop[évolution verticale de machine virtuelle Azure avec Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Échelle verticale, également appelé *montée en puissance* et *à l’échelle*, moyens en augmentant ou en réduisant les tailles de machine virtuelle (VM) dans la charge de travail de réponse tooa. Comparez cela avec [mise à l’échelle horizontale](virtual-machine-scale-sets-autoscale-overview.md), également appelée tooas *montée en puissance parallèle* et *l’échelle en*, où le nombre hello d’ordinateurs virtuels est modifiée en fonction de la charge de travail hello.

Le terme « réapprovisionner » signifie supprimer une machine virtuelle et la remplacer par une autre. Lorsque vous augmentez ou réduisez la taille des machines virtuelles sur un ensemble d’échelle de machines virtuelles de hello, dans certains cas vous souhaitez tooresize existant de machines virtuelles et conserver vos données, alors que dans d’autres cas, vous devez toodeploy nouvelles machines virtuelles de taille de nouveau hello. Ce document couvre les deux cas de figure.

La mise à l’échelle verticale peut être utile dans les cas suivants :

* Sous-utilisation d’un service résidant sur des machines virtuelles (par exemple, le week-end). La réduction de taille de machine virtuelle hello peut réduire les coûts mensuels.
* Augmentation toocope taille de machine virtuelle avec la plus grande à la demande sans créer des machines virtuelles supplémentaires.

Vous pouvez configurer vertical mise à l’échelle toobe déclenchée selon des métriques alertes en fonction de votre jeu de mise à l’échelle de machine virtuelle. Alerte de hello est activé se déclenche un webhook déclenchant un runbook qui peut s’ajuster votre échelle défini vers le haut ou vers le bas. La mise à l’échelle verticale peut être configurée comme suit :

1. Créez un compte Azure Automation avec fonctionnalité d’identification.
2. Importez les runbooks de mise à l’échelle verticale Azure Automation dans votre abonnement.
3. Ajouter un runbook de tooyour webhook.
4. Ajouter une alerte tooyour ensemble d’échelle de machine virtuelle à l’aide d’une notification de webhook.

> [!NOTE]
> La mise à l’échelle verticale ne peut s’effectuer que sur des machines virtuelles d’une certaine taille. Comparer les spécifications de hello de chaque taille avant de décider de tooscale à partir d’un tooanother (nombre plus élevé n’indique pas toujours plus grande taille de machine virtuelle). Vous pouvez choisir tooscale entre hello suivant des paires de taille :
> 
> | Paires de mise à l’échelle des machines virtuelles |  |
> | --- | --- |
> | Standard_A0 |Standard_A11 |
> | D1 standard |D14 standard |
> | Standard_DS1 |Standard_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>Créer un compte Azure Automation avec fonctionnalité d’identification
Hello première chose toodo consiste à créer un compte Azure Automation qui hébergera hello procédures opérationnelles utilisé tooscale hello instances ensemble d’échelle de machine virtuelle. Récemment [Azure Automation](https://azure.microsoft.com/services/automation/) a introduit la fonctionnalité « Exécuter en tant que compte » hello qui rend la hello Principal du Service pour en exécutant automatiquement les runbooks hello au nom d’un utilisateur très facile. Vous pouvez en savoir plus à ce sujet dans l’article hello ci-dessous :

* [Authentifier des Runbooks avec un compte d’identification Azure](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importer les runbooks de mise à l’échelle verticale Azure Automation dans votre abonnement
les runbooks Hello nécessaire échelle toovertically que vos jeux de mise à l’échelle de machine virtuelle sont déjà publiés dans hello galerie de runbooks Azure Automation. les étapes tooimport dans votre abonnement suivent hello dans cet article :

* [Galeries de runbooks et de modules pour Azure Automation](../automation/automation-runbook-gallery.md)

Choisissez option Parcourir la galerie de hello hello procédures opérationnelles :

![Toobe runbooks importé][runbooks]

procédures opérationnelles Hello nécessitant toobe importé sont affichés. Sélectionnez le runbook hello selon si vous souhaitez que verticales mise à l’échelle avec ou sans la préparation :

![Galerie de runbooks][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>Ajouter un runbook de tooyour webhook
Une fois que vous avez importé les runbooks hello, vous devez tooadd un runbook de toohello webhook afin qu’elle peut être déclenchée par une alerte à partir d’un ensemble d’échelle de machine virtuelle. Détails de Hello de création d’un webhook pour votre Runbook sont décrites dans cet article :

* [Webhooks Azure Automation](../automation/automation-webhooks.md)

> [!NOTE]
> Assurez-vous que vous copiez hello webhook URI avant de fermer la boîte de dialogue hello webhook car vous en aurez besoin dans la section suivante de hello.
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>Ajouter une alerte tooyour ensemble d’échelle de machine virtuelle
Voici un PowerShell script qui montre comment tooadd une alerte tooa ensemble d’échelle de machine virtuelle. Consultez toohello suivant le nom de hello article tooget d’alerte de hello hello toofire métrique de : [mesures courantes de moniteur Azure échelle](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> Il est recommandé de tooconfigure une fenêtre de temps raisonnable pour l’alerte hello dans tooavoid commande déclencher la mise à l’échelle verticale, et les associés interruption de service, trop souvent. Envisagez une période d’au moins 20 à 30 minutes. Envisagez horizontal mise à l’échelle si vous avez besoin tooavoid toute interruption.
> 
> 

Pour plus d’informations sur comment toocreate alertes référence toohello suivant des articles :

* [Exemples de démarrage rapide Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [Exemple de démarrage rapide de l’interface CLI multiplateforme Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a>Résumé
Cet article vous a montré des exemples simples de mise à l’échelle verticale. Grâce à ces éléments (compte Automation, runbooks, webhooks et alertes), vous pouvez connecter des événements très différents à un jeu d’actions personnalisé.

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
