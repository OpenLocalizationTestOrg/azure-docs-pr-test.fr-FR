---
title: "aaaWindows vue d’ensemble des Machines virtuelles | Documents Microsoft"
description: "Apprenez à créer et à gérer des machines virtuelles Windows dans Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Vue d’ensemble des machines virtuelles Windows dans Azure

Les Machines Virtuelles Azure sont l’un des nombreux types de [ressources informatiques évolutives et à la demande](../../app-service-web/choose-web-site-cloud-service-vm.md) proposés par Azure. En règle générale, vous choisissez une machine virtuelle lorsque vous avez besoin de plus de contrôle sur l’environnement informatique de hello qu’offre hello autres choix. Cet article vous informe sur les points à prendre en compte avant de créer une machine virtuelle, sur sa création et sur sa gestion.

Une offre Azure VM hello flexibilité de la virtualisation sans avoir toobuy et de maintenir un matériel physique hello qui l’exécute. Toutefois, vous devez toujours toomaintain hello machine virtuelle en effectuant les tâches, telles que la configuration, mise à jour corrective et installation du logiciel hello qui s’exécute sur celui-ci.

Les Machines Virtuelles Azure peuvent être utilisées de différentes manières. Voici quelques exemples :

* **Développement et test** – machines virtuelles Azure offrent une rapide et facilement toocreate un ordinateur avec des configurations spécifiques requis toocode et tester une application.
* **Les applications dans le cloud de hello** – étant donné que la demande pour votre application permettre varier, il peut être économique sens toorun sur une machine virtuelle dans Azure. Vous payez pour des machines virtuelles supplémentaires lorsque vous en avez besoin et vous les arrêtez le reste du temps.
* **Étendue du centre de données** – machines virtuelles dans un réseau virtuel Azure peuvent être facilement le réseau de l’organisation tooyour connecté.

nombre de Hello de machines virtuelles utilisées par votre application capable d’évoluer et toowhatever est requis toomeet vos besoins.

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>De quoi ai-je besoin toothink sur avant de créer une machine virtuelle ?
Il existe toujours une multitude de [considérations liées à la conception](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lorsque vous générez une infrastructure d’application dans Azure. Ces aspects d’une machine virtuelle sont toothink important avant de commencer :

* noms de Hello vos ressources d’application
* emplacement Hello où sont stockés les ressources de hello
* taille de Hello Hello machine virtuelle
* nombre maximal de Hello de machines virtuelles qui peuvent être créés
* système d’exploitation Hello hello machine virtuelle s’exécute.
* configuration de Hello Hello machine virtuelle après son démarrage
* Hello les ressources associées qui hello que machine virtuelle doit

### <a name="naming"></a>Dénomination
Un ordinateur virtuel possède un [nom](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooit attribué et qu’il a un nom d’ordinateur configuré en tant que partie du système d’exploitation de hello. nom de Hello d’une machine virtuelle peut être too15 caractères.

Si vous utilisez le disque de système d’exploitation toocreate Azure hello, Nom_Ordinateur hello et le nom de machine virtuelle hello sont hello identiques. Si vous [télécharger et utiliser votre propre image](upload-generalized-managed.md) qui contient un système d’exploitation précédemment configuré et l’utiliser toocreate une machine virtuelle, les noms de hello peuvent être différentes. Nous recommandons que lorsque vous téléchargez votre propre fichier image, vous nom de l’ordinateur dans le système d’exploitation de hello hello et nom d’ordinateur virtuel hello hello même.

### <a name="locations"></a>Emplacements
Toutes les ressources créées dans Azure sont distribués sur plusieurs [des régions géographiques](https://azure.microsoft.com/regions/) monde hello. En règle générale, la région de hello est appelée **emplacement** lorsque vous créez une machine virtuelle. Pour une machine virtuelle, emplacement de hello spécifie où se trouvent les disques durs virtuels hello.

Ce tableau présente quelques-unes des utilisations hello que vous pouvez obtenir une liste des emplacements disponibles.

| Méthode | Description |
| --- | --- |
| Portail Azure |Sélectionnez un emplacement à partir de la liste de hello lorsque vous créez une machine virtuelle. |
| Azure PowerShell |Hello d’utilisation [Get-AzureRmLocation](/powershell/module/azurerm.resources/get-azurermlocation) commande. |
| API REST |Hello d’utilisation [liste d’emplacements](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations) opération. |

### <a name="vm-size"></a>Taille de la machine virtuelle
Hello [taille](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Hello machine virtuelle que vous utilisez est déterminé par la charge de travail hello que vous souhaitez toorun. taille Hello que vous choisissez détermine ensuite des facteurs tels que la capacité d’alimentation, la mémoire et le stockage, de traitement. Azure propose un large éventail de tailles toosupport de nombreux types d’utilisations.

Azure facture un [tarif horaire](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) en fonction de la taille et le système d’exploitation de machine virtuelle hello. Pour les heures entamées, Azure facture uniquement pour les minutes hello utilisés. Le stockage est facturé séparément.

### <a name="vm-limits"></a>Limites des machines virtuelles
Votre abonnement a la valeur par défaut [des limites de quota](../../azure-subscription-service-limits.md) en place qui pourrait avoir un impact sur déploiement hello de nombreux ordinateurs virtuels pour votre projet. limite actuelle de Hello par abonnement est 20 ordinateurs virtuels par région. Les limites peuvent être augmentées en soumettant un ticket de support demandant leur hausse.

### <a name="operating-system-disks-and-images"></a>Images et disques du système d’exploitation
Utiliser des machines virtuelles [les disques durs virtuels (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore leur système d’exploitation (OS) et les données. Disques durs virtuels sont également utilisés pour les images hello que vous pouvez choisir parmi tooinstall un système d’exploitation. 

Azure propose de nombreuses [les images marketplace](https://azure.microsoft.com/marketplace/virtual-machines/) toouse avec différentes versions et les types de systèmes d’exploitation Windows Server. Les images Marketplace sont identifiées par l’éditeur d’images, l’offre, la référence (SKU) et la version (la version est généralement spécifiée en dernier). 

Ce tableau présente quelques méthodes que vous pouvez trouver des informations hello pour une image.

| Méthode | Description |
| --- | --- |
| Portail Azure |les valeurs Hello sont automatiquement spécifiées pour vous lorsque vous sélectionnez une image toouse. |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher) -Location "emplacement"<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer) -Location "emplacement" -Publisher "nomÉditeur"<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) -Location "emplacement" -Publisher "nomÉditeur" -Offer "nomOffre" |
| API REST |[Lister les éditeurs d’images](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<BR>[Lister les offres d’images](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<BR>[Lister les références d’images](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) |

Vous pouvez choisir trop[télécharger et utiliser votre propre image](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account) et lorsque vous procédez ainsi, le nom du serveur de publication hello offre et la référence (SKU) ne sont pas utilisés.

### <a name="extensions"></a>Extensions
Les [extensions](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) de machines virtuelles étendent les fonctionnalités de votre machine virtuelle par le biais de la configuration post-déploiement et de tâches automatisées.

Ces tâches courantes peuvent être accomplies à l’aide des extensions :

* **Exécuter des scripts personnalisés** : hello [Extension de Script personnalisé](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) vous permet de configurer des charges de travail sur hello machine virtuelle en exécutant le script lorsque hello machine virtuelle est configurée.
* **Déployer et gérer des configurations** : hello [Extension de Configuration d’état souhaité (DSC) PowerShell](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) vous permet de configurer DSC sur une machine virtuelle toomanage environnements et des configurations.
* **Collecter les données de diagnostic** : hello [Extension des Diagnostics Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) vous permet de configurer les données de diagnostic hello VM toocollect qui peuvent être utilisé toomonitor hello d’intégrité de votre application.

### <a name="related-resources"></a>Ressources associées
ressources Hello dans cette table sont utilisés par hello VM et doivent tooexist ou être créées lorsque hello machine virtuelle est créée.

| Ressource | Requis | Description |
| --- | --- | --- |
| [Groupe de ressources](../../azure-resource-manager/resource-group-overview.md) |Oui |Hello machine virtuelle doit être contenu dans un groupe de ressources. |
| [Compte de stockage](../../storage/common/storage-create-storage-account.md) |Oui |Hello machine virtuelle doit toostore de compte de stockage hello ses disques durs virtuels. |
| [Réseau virtuel](../../virtual-network/virtual-networks-overview.md) |Oui |Hello machine virtuelle doit être un membre d’un réseau virtuel. |
| [Adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |Non |Hello machine virtuelle peut avoir un tooremotely de tooit adresse IP publique à y accéder. |
| [Interface réseau](../../virtual-network/virtual-network-network-interface.md) |Oui |Hello machine virtuelle doit hello réseau interface toocommunicate dans le réseau de hello. |
| [Disques de données](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |Non |Hello VM peut inclure des fonctionnalités de stockage de tooexpand de disques de données. |

## <a name="how-do-i-create-my-first-vm"></a>Comment créer sa première machine virtuelle ?
Vous avez plusieurs possibilités pour la création de votre machine virtuelle. les choix de Hello que vous effectuez dépend de l’environnement hello dans. 

Ce tableau fournit tooget informations que vous aider à créer votre machine virtuelle.

| Méthode | Article |
| --- | --- |
| Portail Azure |[Créer une machine virtuelle exécutant Windows à l’aide du portail de hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Modèles |[Création d’une machine virtuelle Windows avec un modèle du Gestionnaire de ressources](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[Créer une machine virtuelle Windows à l’aide de PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Kits de développement logiciel (SDK) client |[Déployer des ressources Azure en C#](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| API REST |[Créer ou mettre à jour une machine virtuelle](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) |

Même si l’on souhaite que cela ne se produise jamais, des problèmes peuvent survenir. Si cette situation produit tooyou, voir informations hello [Gestionnaire de ressources de dépannage des problèmes de déploiement avec la création d’une machine virtuelle Windows dans Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>Comment gérer les hello VM que j’ai créé ?
Les machines virtuelles peuvent être gérées à l’aide d’un portail sur navigateur, d’outils de ligne de commande avec prise en charge des scripts ou directement au moyen des API. Certaines tâches de gestion classiques que vous pouvez exécuter obtenez plus d’informations sur une machine virtuelle, ouverture de session tooa machine virtuelle, gestion de la disponibilité et les sauvegardes.

### <a name="get-information-about-a-vm"></a>Obtenir des informations sur une machine virtuelle
Cette table montre quelques-unes des utilisations hello que vous pouvez obtenir plus d’informations sur une machine virtuelle.

| Méthode | Description |
| --- | --- |
| Portail Azure |Dans le menu du hub hello, cliquez sur **virtuels** , puis sélectionnez hello machine virtuelle à partir de la liste de hello. Panneau hello pour hello machine virtuelle, vous avez accès toooverview d’informations, les valeurs de paramètre et métriques de surveillance. |
| Azure PowerShell |Pour plus d’informations sur l’utilisation de machines virtuelles toomanage de PowerShell, consultez [créer et gérer des machines virtuelles Windows avec module d’Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| API REST |Hello d’utilisation [informations d’obtenir un ordinateur virtuel](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) informations tooget d’opération sur une machine virtuelle. |
| Kits de développement logiciel (SDK) client |Pour plus d’informations sur l’utilisation de machines virtuelles de toomanage c#, consultez [gérer des Machines virtuelles Azure à l’aide du Gestionnaire de ressources Azure et c#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |

### <a name="log-on-toohello-vm"></a>Ouvrez une session toohello machine virtuelle
Vous utilisez trop le bouton de connexion de hello Bonjour Azure portal[démarrer une session Bureau à distance (RDP)](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Incidents peuvent parfois se produire lors de la tentative de toouse une connexion à distance. Si cette situation produit tooyou, extraire des informations d’aide hello dans [tooan de connexions de résoudre les problèmes de bureau à distance Azure machine virtuelle exécutant Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="manage-availability"></a>Gérer la disponibilité
Il est important pour vous toounderstand comment trop[garantir une haute disponibilité](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour votre application. Cette configuration implique la création de plusieurs tooensure de machines virtuelles au moins est en cours d’exécution.

Pour votre tooqualify de déploiement pour notre 99.95 contrat de niveau de Service de machine virtuelle, vous devez toodeploy deux ou plusieurs ordinateurs virtuels sont en cours d’exécution à l’intérieur de votre charge de travail un [à haute disponibilité](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Grâce à cette configuration, vos machines virtuelles sont réparties sur plusieurs domaines d’erreur et déployées sur des hôtes ayant des fenêtres de maintenance distinctes. Hello complète [contrat SLA Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) explique hello garantie de disponibilité de Azure dans sa globalité.

### <a name="back-up-hello-vm"></a>Sauvegarder hello machine virtuelle
A [de coffre Recovery Services](../../backup/backup-introduction-to-azure-backup.md) est utilisé tooprotect données et des ressources dans Azure Backup et Azure Site Recovery services. Vous pouvez utiliser un coffre Recovery Services trop[déployer et gérer des sauvegardes pour les machines virtuelles déployées par le Gestionnaire de ressources à l’aide de PowerShell](../../backup/backup-azure-vms-automation.md). 

## <a name="next-steps"></a>Étapes suivantes
* Si votre objectif est toowork avec les machines virtuelles Linux, consultez [Azure et Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* En savoir plus sur les instructions de hello autour de la configuration de votre infrastructure Bonjour [procédure pas à pas d’exemple Azure infrastructure](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
