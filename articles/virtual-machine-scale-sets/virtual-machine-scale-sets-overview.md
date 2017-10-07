---
title: "échelle de machines virtuelles aaaAzure définit la vue d’ensemble | Documents Microsoft"
description: En savoir plus sur les groupes de machines virtuelles identiques Azure
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 788b2d1636e0bf4ef3fbf94aed9b3303c5fafa82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-virtual-machine-scale-sets-in-azure"></a>À quoi correspondent les groupes de machines virtuelles identiques dans Azure ?
Machines virtuelles identiques constituent une ressource de calcul Azure que vous pouvez utiliser toodeploy et gérer un ensemble de machines virtuelles identiques. Avec toutes les machines virtuelles configurées hello même identiques sont true mise à l’échelle de toosupport conçue et aucune configuration anticipée de machines virtuelles n’est nécessaire. Il est donc plus faciles services à grande échelle toobuild qui ciblent des charges de travail big compute et données volumineuses.

Pour les applications qui ont besoin de ressources de calcul tooscale et de mise à l’échelle les opérations sont implicitement équilibrées entre domaines d’erreur et la mise à jour. Pour un tooscale introduction autres jeux, consultez toohello [annonce du blog Azure](https://azure.microsoft.com/blog/azure-virtual-machine-scale-sets-ga/).

Regardez ces vidéos pour en savoir plus sur les groupes identiques :

* [Mark Russinovich parle des groupes identiques Azure](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)  
* [Jeux de mise à l’échelle de machine virtuelle, avec Guy Bowerman](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

## <a name="creating-and-managing-scale-sets"></a>Création et gestion des groupes identiques
Vous pouvez créer une échelle définie dans hello [portail Azure](https://portal.azure.com) en sélectionnant **nouveau** et en tapant **échelle** sur la barre de recherche hello. **Machines virtuelles identiques** est répertorié dans les résultats de hello. À partir de là, vous pouvez renseigner hello requis champs toocustomize et déployer des votre ensemble d’échelle. Vous avez également tooset options des règles de base de mise à l’échelle en fonction de l’utilisation du processeur dans le portail de hello.

Vous pouvez définir et déployer des groupes identiques à l’aide de modèles JSON et d’[API REST](https://msdn.microsoft.com/library/mt589023.aspx), tout comme des machines virtuelles Azure Resource Manager individuelles. Par conséquent, vous pouvez utiliser toute méthode de déploiement standard d’Azure Resource Manager. Pour en savoir plus sur les modèles, consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Vous trouverez un ensemble de modèles d’exemple pour l’échelle de machines virtuelles définit Bonjour [référentiel GitHub de modèles Azure Quickstart](https://github.com/Azure/azure-quickstart-templates). (Recherchez les modèles avec **mise** dans le titre de hello.)

Pour des exemples de modèle de démarrage rapide hello, un bouton « Déployer tooAzure » dans le fichier Lisezmoi de hello pour chaque fonctionnalité de déploiement du portail toohello modèle des liens. mise à l’échelle de toodeploy hello défini, cliquez sur hello, puis renseignez tous les paramètres qui sont requis dans le portail de hello. 

## <a name="scaling-a-scale-set-out-and-in"></a>Mise à l’échelle d’un groupe identique (augmentation et diminution)
Vous pouvez modifier la capacité de hello d’une échelle de définir Bonjour portail Azure en cliquant sur hello **mise à l’échelle** sous **paramètres**. 

ensemble d’échelle de toochange de capacité sur la ligne de commande hello, utilisez hello **échelle** dans [CLI d’Azure](https://github.com/Azure/azure-cli). Par exemple, utilisez cette tooset commande capacité tooa montée en puissance de 10 machines virtuelles :

```bash
az vmss scale -g resourcegroupname -n scalesetname --new-capacity 10 
```

nombre de hello tooset d’ordinateurs virtuels dans une échelle de définie à l’aide de PowerShell, utilisez hello **AzureRmVmss de mise à jour** commande :

```PowerShell
$vmss = Get-AzureRmVmss -ResourceGroupName resourcegroupname -VMScaleSetName scalesetname  
$vmss.Sku.Capacity = 10
Update-AzureRmVmss -ResourceGroupName resourcegroupname -Name scalesetname -VirtualMachineScaleSet $vmss
```

tooincrease ou diminuer nombre de hello d’ordinateurs virtuels dans une échelle définie à l’aide d’un modèle Azure Resource Manager, modifiez hello **capacité** propriété et redéployer le modèle hello. Cette simplicité rend identiques toointegrate facile avec Azure mise à l’échelle ou toowrite que votre propre couche mise à l’échelle personnalisée si vous devez les événements de mise à l’échelle personnalisée toodefine cette échelle automatique Azure ne prend pas en charge. 

Si vous redéployez une capacité de hello de toochange modèle Azure Resource Manager, vous pouvez définir un quantité modèle plus petit qui inclut uniquement hello **SKU** paquet de propriété avec hello mis à jour de capacité. [Voici un exemple](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing).

## <a name="autoscale"></a>Autoscale

Un ensemble d’échelle peut éventuellement être configuré avec les paramètres de mise à l’échelle lorsqu’il est créé dans hello portail Azure. nombre de Hello d’ordinateurs virtuels peut ensuite augmentation ou de diminution selon l’utilisation de la moyenne du processeur. 

Nombreux hello l’échelle le jeu de modèles en hello [modèles de démarrage rapide d’Azure](https://github.com/Azure/azure-quickstart-templates) définir les paramètres de mise à l’échelle. Vous pouvez également ajouter des tooan de paramètres de mise à l’échelle existant d’un ensemble d’échelle. Par exemple, ce script Azure PowerShell ajoute un ensemble d’échelle tooa mise à l’échelle en fonction de l’UC :

```PowerShell

$subid = "yoursubscriptionid"
$rgname = "yourresourcegroup"
$vmssname = "yourscalesetname"
$location = "yourlocation" # e.g. southcentralus

$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Increase -ScaleActionValue 1
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator LessThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Decrease -ScaleActionValue 1
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "autoprofile1"
Add-AzureRmAutoscaleSetting -Location $location -Name "autosetting1" -ResourceGroup $rgname -TargetResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -AutoscaleProfiles $profile1
```

Vous trouverez une liste de métriques valide tooscale sur dans [prise en charge des métriques avec Azure analyse](../monitoring-and-diagnostics/monitoring-supported-metrics.md) sous hello titre « Microsoft.Compute/virtualMachineScaleSets ». Les options de mise à l’échelle plus avancées sont également disponibles, y compris la mise à l’échelle basée sur la planification et à l’aide de webhooks toointegrate avec les systèmes de l’alerte.

## <a name="monitoring-your-scale-set"></a>Surveillance de votre groupe identique
Hello [portail Azure](https://portal.azure.com) listes échelle définit et affiche leurs propriétés. portail de Hello prend également en charge les opérations de gestion. Vous pouvez effectuer des opérations de gestion à la fois sur des groupes identiques, et sur des machines virtuelles individuelles faisant partie d’un groupe identique. portail de Hello fournit également un graphique d’utilisation de ressources personnalisable. 

Si vous devez toosee ou que vous modifiez hello sous-jacent définition JSON d’une ressource Azure, vous pouvez également utiliser [Explorateur de ressources Azure](https://resources.azure.com). Groupes identiques sont une ressource sous hello fournisseur de ressources Microsoft.Compute Azure. À partir de ce site, vous pouvez les voir en développant hello suivant liens :

**Abonnements** > **votre abonnement** > **resourceGroups** > **fournisseurs** > **Microsoft.Compute** > **virtualMachineScaleSets** > **votre groupe identique** &gt; etc.

## <a name="scale-set-scenarios"></a>Scénarios de groupe identique
Cette section répertorie quelques scénarios de groupe identique classiques. Certains services Azure de niveau supérieur (comme Batch, Service Fabric, Container Service) utilisent également ces scénarios.

* **Utilisez le protocole RDP ou SSH tooconnect tooscale définie instances**: un ensemble d’échelle est créé à l’intérieur d’un réseau virtuel, et des ordinateurs virtuels individuels dans un ensemble d’échelle hello ne sont pas alloués des adresses IP publiques par défaut. Cette stratégie permet d’éviter les frais hello et nœuds de hello tooall dans votre grille de calcul des adresses de charge de gestion de l’allocation d’adresse IP publique distincte. Si vous avez besoin de diriger les connexions externes tooscale définie des machines virtuelles, vous pouvez configurer une mise à l’échelle ensemble tooautomatically affecter publique IP adresses toonew machines virtuelles. Vous pouvez également connecter tooVMs d’autres ressources dans votre réseau virtuel qui peut être alloué les adresses IP publiques, par exemple, les équilibreurs de charge et les machines virtuelles autonomes. 
* **Se connecter tooVMs à l’aide de règles NAT**: vous pouvez créer une adresse IP publique, attribuez-lui un équilibreur de charge tooa et définir un pool NAT de trafic entrant. Ces actions mappent les ports sur le port hello IP adresse tooa une machine virtuelle dans un ensemble d’échelle hello. Par exemple :
  
  | Source | Port source | Destination | Port de destination |
  | --- | --- | --- | --- |
  |  Adresse IP publique |Port 50000 |vmss\_0 |Port 22 |
  |  Adresse IP publique |Port 50001 |vmss\_1 |Port 22 |
  |  Adresse IP publique |Port 50002 |vmss\_2 |Port 22 |
  
   Dans [cet exemple](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-nat), des règles NAT sont définie tooenable un tooevery de connexion SSH machine virtuelle dans un ensemble d’échelle, l’utilisation d’une seule adresse IP publique.
  
   [Cet exemple](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-nat) même hello avec RDP et Windows.
* **Se connecter tooVMs à l’aide d’un « jumpbox »**: Si vous créez un ensemble d’échelle et une machine virtuelle autonome dans hello virtuel même réseau, hello autonome machine virtuelle et hello ensemble d’échelle de machine virtuelle peut se connecter à tooone un autre à l’aide de leur adresse IP interne, les adresses, tel que défini par hello virtuel réseau ou sous-réseau. Si vous créez une adresse IP publique et affectez toohello autonome machine virtuelle, vous pouvez utiliser le RDP ou SSH tooconnect toohello machine virtuelle autonome. Vous pouvez ensuite vous connecter à partir de que l’échelle de machine tooyour définie des instances. À ce stade, vous pouvez remarquer qu’un simple groupe identique est intrinsèquement plus sûr qu’une machine virtuelle autonome simple avec une adresse IP publique dans sa configuration par défaut.
  
   Par exemple, [ce modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-jumpbox) déploie une échelle simple avec une machine virtuelle autonome. 
* **Équilibrage des instances de l’ensemble tooscale**: Si vous souhaitez toodeliver travail tooa compute cluster de machines virtuelles à l’aide d’une approche de tourniquet, vous pouvez configurer un équilibreur de charge Azure avec des règles d’équilibrage de charge de couche 4 en conséquence. Vous pouvez définir des sondes tooverify votre application s’exécute par la commande ping ports avec le protocole spécifié, l’intervalle et le chemin d’accès de la demande. [Azure Application Gateway](https://azure.microsoft.com/services/application-gateway/) prend également en charge les groupes identiques de machines virtuelles, ainsi que des scénarios d’équilibrage de charge de couche 7 et plus.
  
   [Cet exemple montre comment](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-web-ssl) crée un ensemble d’échelle qui s’exécute de serveurs web Apache et qu’il utilise un toobalance hello équilibrage de charge que chaque ordinateur virtuel. (Vérifiez VM de type de ressource Microsoft.Network/loadBalancers hello et extensionProfile dans le groupe de VM identiques.)

   [Cet exemple Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-app-gateway) et [cet exemple Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-app-gateway) utilisent Application Gateway.  

* **Déploiement d’un groupe identique en tant que cluster de calcul dans un gestionnaire de cluster PaaS** – Les groupes identiques sont parfois décrits en tant que rôle de travail de la prochaine génération. Si une description valide, elle s’exécute risque hello d’échelle à confusion ensemble de fonctionnalités avec les fonctionnalités des Services de cloud computing Azure. Dans un sens, les groupes identiques correspondent à un rôle de travail ou à une ressource Worker. Ils sont une ressource de calcul généralisée indépendante de la plateforme/du service d’exécution, personnalisable et pouvant être intégrée à l’IaaS Azure Resource Manager.
  
   Un rôle de travail des Services cloud est limité en termes de prise en charge de la plate-forme/du service d’exécution (images de plateforme Windows uniquement). Cependant, il inclut également des services tels que l’échange d’adresses IP virtuelles, la configuration des paramètres de mise à niveau, et les paramètres spécifiques au déploiement du service d’exécution/de l’application. Ces services ne sont pas *encore* disponibles dans les groupes identiques. Ils peuvent être transmis par d’autres services PaaS de niveau supérieur, comme Azure Service Fabric. Vous pouvez envisager les groupes identiques comme une infrastructure prenant en charge PaaS. Les solutions PaaS, telles que [Service Fabric](https://azure.microsoft.com/services/service-fabric/), s’appuient sur cette infrastructure.
  
   Dans [cet exemple](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos) de cette approche, [Azure Container Service](https://azure.microsoft.com/services/container-service/) déploie un cluster basé sur les groupes identiques avec un orchestrateur de conteneur.

## <a name="scale-set-performance-and-scale-guidance"></a>Performance de groupe identique et guide de mise à l’échelle
* Une échelle de jeu prend en charge des too1, 000 machines virtuelles. Si vous créez et téléchargez vos propres images de machine virtuelle personnalisées, la limite de hello est 100. Pour connaître les aspects à prendre en compte en matière d’utilisation de grands groupes identiques, voir [Utilisation de grands groupes de machines virtuelles identiques](virtual-machine-scale-sets-placement-groups.md).
* Vous n’avez pas toopre-créer des jeux de mise à l’échelle de stockage Azure comptes toouse. Jeux de prise en charge Azure géré les disques, exclure des problèmes de performances sur nombre hello de disques par le compte de stockage. Pour plus d’informations, voir [Groupes de machines virtuelles identiques et disques gérés Azure](virtual-machine-scale-sets-managed-disks.md).
* Envisagez d’utiliser Azure Premium Storage plutôt que le stockage Azure afin d’optimiser les temps d’approvisionnement des machines virtuelles et les performances d’E/S.
* quota de cœurs Hello dans la région de hello dans lequel vous déployez limite nombre hello de machines virtuelles que vous pouvez créer. Vous devrez peut-être toocontact clientèle tooincrease votre limite de quota de calcul, même si vous avez une limite haute de cœurs pour une utilisation avec les Services de cloud computing Azure aujourd'hui. tooquery votre quota, exécutez la commande CLI d’Azure : `azure vm list-usage`. Ou bien, exécutez cette commande PowerShell : `Get-AzureRmVMUsage`.

## <a name="frequently-asked-questions-for-scale-sets"></a>Forum Aux Questions (FAQ) pour les groupes identiques
**Q.** Combien de machines virtuelles peut-il y avoir dans un groupe identique ?

**A.** Un ensemble d’échelle peut avoir 0 too1, 000 machines virtuelles basées sur des images de plateforme ou 0 too100 VMs basées sur des images personnalisées. 

**Q.** Les disques de données sont-ils pris en charge dans les groupes identiques ?

**A.** Oui. Un ensemble d’échelle peut définir une configuration de disques de données attachées qui applique des machines virtuelles tooall hello ensemble. Pour plus d’informations, consultez [Groupes identiques Azure et disques de données attachés](virtual-machine-scale-sets-attached-disks.md). Il existe d’autres options pour stocker les données :

* Fichiers Azure (lecteurs SMB partagés)
* Système d’exploitation de lecteur
* Lecteur temp (local, non sauvegardé par le stockage Azure)
* Service de données Azure (par exemple, tables Azure, objets blob Azure)
* Service de données externe (par exemple, base de données distante)

**Q.** Quelles sont les régions Azure qui prennent en charge les groupes identiques ?

**A.** Toutes les régions prennent en charge les groupes identiques.

**Q.** Comment créer un groupe identique à l’aide d’une image personnalisée ?

**A.** Créez un disque géré en fonction de votre image personnalisée de disque dur virtuel et référencez-le dans votre modèle de groupe identique. [Voici un exemple](https://github.com/chagarw/MDPP/tree/master/101-vmss-custom-os).

**Q.** Si vous réduisez mon échelle de définie la capacité de 20 too15, ce qui les machines virtuelles sont supprimées ?

**A.** Machines virtuelles sont supprimés à l’échelle de hello définir uniformément dans les domaines de mise à jour et de la disponibilité de toomaximize de domaines de pannes. Machines virtuelles avec hello Qu'id la plus élevées sont supprimées en premier.

**Q.** Que se passe-t-il si je puis augmenter la capacité de hello de 15 too18 ?

**A.** Si vous augmentez la capacité too18, 3 nouveaux ordinateurs virtuels sont créés. Chaque fois, ID d’instance de machine virtuelle de hello est incrémenté de hello précédente la plus grande (par exemple, 20, 21, 22). Les machines virtuelles sont réparties sur les domaines d’erreur et les domaines de mise à jour.

**Q.** Lorsque j’utilise plusieurs extensions dans un groupe identique, puis-je appliquer une séquence d’exécution ?

**A.** Pas directement, mais pour l’extension customScript de hello, votre script peut attendre qu’une autre extension toofinish. Vous pouvez obtenir plus d’informations sur la mise en séquence d’extension dans le billet de blog hello [séquencement d’Extension dans les ensembles de mise à l’échelle de machine virtuelle Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).

**Q.** Les groupes identiques fonctionnent-ils avec des ensembles haute disponibilité Azure ?

**A.** Oui. Un groupe identique est un ensemble de disponibilité implicite comprenant 5 domaines d’erreur et 5 domaines de mise à jour. Mise à l’échelle les jeux de plus de 100 machines virtuelles sont réparties entre plusieurs *groupes de la sélection élective*, qui sont des groupes à haute disponibilité toomultiple équivalent. Pour plus d’informations sur les groupes de placement, voir [Working with large virtual machine scale sets](virtual-machine-scale-sets-placement-groups.md) (Utilisation de grands groupes de machines virtuelles identiques). Un groupe de disponibilité de machines virtuelles peut exister dans hello même réseau virtuel comme un ensemble d’échelle de machines virtuelles. Une configuration commune est le nœud de contrôle de tooput machines virtuelles (qui nécessitent souvent une configuration unique) d’un groupe défini et placer les nœuds de données dans un ensemble d’échelle hello.

Vous pouvez trouver plus tooquestions réponses sur l’échelle définit Bonjour [mise à l’échelle de machine virtuelle Azure définit FAQ](virtual-machine-scale-sets-faq.md).
