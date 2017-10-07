---
title: aaaAzure analyse et les Machines virtuelles Windows | Documents Microsoft
description: Didacticiel - Surveiller une machine virtuelle Windows avec Azure PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a>Surveiller une machine virtuelle Windows avec Azure PowerShell

Surveillance Azure utilise des agents de démarrage de toocollect et les données de performances à partir de machines virtuelles Azure, stocker ces données dans le stockage Azure et le rendre accessible via le portail, module Azure PowerShell de hello et hello CLI d’Azure. Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Activer les diagnostics de démarrage sur une machine virtuelle
> * Afficher les diagnostics de démarrage
> * Afficher les métriques de l’hôte de machine virtuelle
> * Installer l’extension de diagnostics hello
> * Afficher les métriques de la machine virtuelle
> * Créer une alerte
> * Configurer la surveillance avancée

Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).

exemple de hello toocomplete dans ce didacticiel, vous devez disposer d’un ordinateur virtuel existant. Si nécessaire, cet [exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) peut en créer une pour vous. Lors de l’utilisation de didacticiel de hello, remplacez le groupe de ressources hello, nom de la machine virtuelle et l’emplacement si nécessaire.

## <a name="view-boot-diagnostics"></a>Afficher les diagnostics de démarrage

Comme les machines virtuelles Windows démarre, agent de Diagnostics de démarrage hello capture de texte qui peut être utilisé pour la résolution des problèmes d’objectif. Cette fonctionnalité est activée par défaut. Hello capturées écran captures sont stockés dans un compte de stockage Azure, qui est également créé par défaut. 

Vous pouvez obtenir des données de diagnostic de démarrage hello avec hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) commande. Bonjour l’exemple suivant, les diagnostics de démarrage sont téléchargés toohello racine hello * c:\* lecteur. 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a>Afficher les métriques de l’hôte

Une machine virtuelle Windows possède une machine virtuelle hôte dédiée dans Azure, avec qui elle interagit. Métriques sont automatiquement collectées pour hello hôte et peuvent être consultées dans hello portail Azure.

1. Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.
2. Cliquez sur **métriques** sur hello Panneau de machine virtuelle, puis sélectionnez une des métriques d’hôte hello sous **métriques disponibles** toosee fonctionne hello machine virtuelle d’hôte.

    ![Afficher les métriques de l’hôte](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a>Installer l’extension Diagnostics

métriques de base hôte Hello sont disponibles, mais toosee plus précis et des mesures spécifiques à la machine virtuelle, vous tooneed tooinstall hello extension Azure diagnostics sur hello machine virtuelle. Hello extension Azure diagnostics permet une analyse supplémentaire et diagnostics toobe de données récupérées à partir de la machine virtuelle de hello. Vous pouvez afficher ces métriques de performances et créer des alertes basées sur le fonctionnement de hello machine virtuelle. extension de diagnostic Hello est installée via hello portail Azure comme suit :

1. Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.
2. Cliquez sur **Paramètres de diagnostic**. liste de Hello montre que *diagnostics de démarrage* sont déjà activés à partir de la section précédente de hello. Cliquez sur la case à cocher pour hello *les audits de base*.
3. Cliquez sur hello **activer l’analyse au niveau invité** bouton.

    ![Afficher les métriques de diagnostic](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a>Afficher les métriques de la machine virtuelle

Vous pouvez afficher les métriques de machine virtuelle hello Bonjour même façon que vous avez affiché les métriques de machine virtuelle hôte hello :

1. Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.
2. toosee effectue hello machine virtuelle, cliquez sur **métriques** sur hello Panneau de machine virtuelle, puis sélectionnez une des métriques de diagnostic hello sous **métriques disponibles**.

    ![Afficher les métriques de la machine virtuelle](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a>Créez des alertes

Vous pouvez créer des alertes en fonction de métriques de performances spécifiques. Les alertes peuvent être utilisé toonotify vous lors de l’utilisation moyenne du processeur dépasse un seuil ou une espace disque disponible devient inférieur à un certain montant, par exemple. Les alertes sont affichent dans hello portail Azure ou peuvent être envoyés par courrier électronique. Vous pouvez également déclencher des runbooks Azure Automation ou Azure Logic Apps dans tooalerts de réponse en cours de génération.

Hello exemple suivant crée une alerte pour l’utilisation moyenne du processeur.

1. Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.
2. Cliquez sur **règles d’alerte** sur le panneau de la machine virtuelle hello, puis cliquez sur **ajouter une alerte métrique** haut hello du panneau des alertes hello.
4. Spécifiez un **Nom** pour votre alerte, comme *myAlertRule*
5. tootrigger une alerte lorsque le pourcentage de l’UC dépasse 1.0 pendant cinq minutes, laissez hello toutes les autres valeurs par défaut sélectionnées.
6. Si vous le souhaitez, case hello pour *propriétaires, collaborateurs et les lecteurs de messagerie* toosend la notification par e-mail. action par défaut de Hello est toopresent une notification dans le portail de hello.
7. Cliquez sur hello **OK** bouton.

## <a name="advanced-monitoring"></a>Surveillance avancée 

Vous pouvez faire une surveillance plus avancée de votre machine virtuelle en utilisant [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Si vous ne l’avez pas déjà fait, vous pouvez vous inscrire pour une [version d’évaluation gratuite](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) d’Operations Management Suite.

Lorsque vous avez accès toohello OMS portail, vous pouvez trouver l’identificateur de clé et l’espace de travail du espace de travail hello sur le panneau des paramètres hello. Hello d’utilisation [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) commande tootooadd hello OMS extension toohello machine virtuelle. Mise à jour hello valeurs Bonjour ci-dessous exemple tooreflect vous clé d’espace de travail OMS et l’ID de l’espace de travail  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

Après quelques minutes, vous devez voir hello nouvelle machine virtuelle dans l’espace de travail OMS hello. 

![Panneau OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez configuré et examiné des machines virtuelles avec Azure Security Center. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créez un réseau virtuel
> * Créer un groupe de ressources et une machine virtuelle 
> * Activer les diagnostics de démarrage sur hello machine virtuelle
> * Afficher les diagnostics de démarrage
> * Afficher les métriques de l’hôte
> * Installer l’extension de diagnostics hello
> * Afficher les métriques de la machine virtuelle
> * Créer une alerte
> * Configurer la surveillance avancée

Avance toohello toolearn de didacticiel suivant sur le centre de sécurité Azure.

> [!div class="nextstepaction"]
> [Gérer la sécurité des machines virtuelles](./tutorial-azure-security.md)