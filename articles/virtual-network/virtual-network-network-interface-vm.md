---
title: "aaaAdd réseau interfaces tooor supprimer à partir de machines virtuelles | Documents Microsoft"
description: "Découvrez comment tooadd réseau interfaces tooor supprimer des interfaces réseau de machines virtuelles."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: eb564b94932b9242f29bc23234b08b0c76ac23a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-network-interfaces-tooor-remove-from-virtual-machines"></a>Ajoutez les interfaces réseau tooor supprimer des machines virtuelles

Découvrez comment tooadd un réseau existant de l’interface lors de la création d’une machine virtuelle ou ajouter ou supprimer des interfaces réseau à partir d’une machine virtuelle existante Bonjour arrêtée (désallouée) d’état. Une interface réseau active un toocommunicate Azure Virtual Machine (VM) avec Internet, Azure et des ressources locales. Une machine virtuelle peut avoir une ou plusieurs interfaces réseau. 

Si vous avez besoin de tooadd, modifier ou supprimer des adresses IP pour une interface réseau, lire hello [gérer des adresses IP réseau interface](virtual-network-network-interface-addresses.md) l’article. Si vous avez besoin de toocreate, modifier ou supprimer des interfaces réseau, lire hello [gérer les interfaces réseau](virtual-network-network-interface.md) l’article.

## <a name="before"></a>Avant de commencer

Terminer hello tâches suivantes avant d’effectuer l’une des étapes dans une section de cet article :

- En savoir sur le nombre d’interfaces réseau chaque taille de Linux et de la machine virtuelle Windows prend en charge en consultant hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articles des tailles de machine virtuelle.
- Connectez-vous à Azure de toohello [portal](https://portal.azure.com), Azure interface de ligne de commande (CLI), ou Azure PowerShell avec un compte Azure. Si vous n’avez pas encore de compte, inscrivez-vous pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/free).
- Si les tâches toocomplete dans cet article, les commandes à l’aide de PowerShell [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente des applets de commande PowerShell Azure hello installé hello. aide tooget pour les commandes PowerShell, des exemples, tapez `get-help <command> -full`.
- Si les tâches toocomplete dans cet article, les commandes à l’aide d’Azure interface de ligne de commande (CLI) [installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente hello Hello CLI d’Azure installé. aide tooget pour les commandes CLI, tapez `az <command> --help`. Au lieu de hello lors de l’installation CLI et les logiciels requis, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. toouse hello Cloud interpréteur de commandes, cliquez sur hello Cloud Shell **> _** bouton haut hello hello [portal](https://portal.azure.com).

## <a name="about"></a>À propos des interfaces réseau et des machines virtuelles

Vous pouvez ajouter (joindre) un tooa d’interface réseau existante machine virtuelle lorsque vous créez hello machine virtuelle, autant de l’interface de réseau hello n’est pas actuellement attaché tooanother machine virtuelle. Vous pouvez ajouter une interface réseau à ou supprimer (détacher) un réseau de l’interface toofrom une machine virtuelle existante, condition hello machine virtuelle est arrêtée dans hello état (libéré). Si vous créez une machine virtuelle à l’aide de hello portail Azure, le portail de hello crée une interface réseau pour vous avec les paramètres par défaut. portail de Hello ne vous autorise pas à :

- Spécifiez un tooadd d’interface réseau existante lors de la création de hello machine virtuelle
- Créer une machine virtuelle avec plusieurs interfaces réseau
- Spécifiez un nom pour l’interface de réseau hello (portail de hello crée interface de réseau hello avec un nom par défaut)

Vous pouvez utiliser Azure PowerShell ou hello CLI toocreate une interface réseau ou la machine virtuelle avec tous les attributs précédents hello que vous ne pouvez pas utiliser le portail hello pour. Avant d’effectuer les tâches hello dans les sections suivantes de hello, tenez compte hello qui suit les contraintes et les comportements :

- Toutes les tailles de machine virtuelle prennent en charge au moins deux interfaces réseau, mais certaines en prennent en charge plus de deux. Bonjour au-delà de certains ordinateurs virtuels, les tailles prises en charge uniquement une seule interface réseau. toolearn le nombre d’interfaces réseau prend en charge la taille de chaque machine virtuelle, lire hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articles des tailles de machine virtuelle. 
- Bonjour précédentes, les interfaces réseau ne serait ajouté tooVMs pris en charge de plusieurs interfaces réseau qui ont été créées avec au moins deux interfaces réseau. Vous ne pouvez pas ajouter un tooa d’interface réseau virtuelle qui a été créé avec une interface réseau, même si la taille de machine virtuelle de hello pris en charge plusieurs interfaces réseau. À l’inverse, vous pouvez supprimer uniquement les interfaces réseau à partir d’une machine virtuelle avec au moins trois interfaces réseau, car les machines virtuelles créées avec au moins deux interfaces réseau toujours avaient toohave au moins deux interfaces réseau. Ces contraintes sont aujourd’hui obsolètes. Vous pouvez maintenant créer une machine virtuelle avec un nombre quelconque d’interfaces réseau (haut numéro toohello pris en charge par la taille de machine virtuelle de hello) et ajouter ou supprimer n’importe quel nombre d’interfaces réseau (à partir de l’état des machines virtuelles dans hello arrêté (désalloués)), tant que hello machine virtuelle a toujours au moins une interface réseau.
- Par défaut, hello première interface réseau dans un ordinateur virtuel est défini comme hello *principal* interface réseau. Toutes les autres interfaces réseau Bonjour machine virtuelle sont *secondaire* interfaces réseau.
- Interfaces réseau principales sont affectés à une passerelle par défaut par les serveurs DHCP Azure hello, mais les interfaces réseau secondaires ne sont pas. Étant donné qu’aucune passerelle par défaut n’est affectée aux interfaces réseau secondaires, par défaut, celles-ci ne peuvent pas communiquer avec des ressources situées hors de leur sous-réseau. interfaces réseau secondaires de tooenable dans un toocommunicate de machine virtuelle Windows avec des ressources en dehors de leur sous-réseau, ajouter des itinéraires toohello système d’exploitation hello `route add` commande à partir d’une ligne de commande Windows. Pour les machines virtuelles Linux, car par défaut hello utilise hôte faible routage, nous vous recommandons restriction du trafic de sous-réseau unique du tooa interfaces réseau secondaires. Si vous avez besoin de connectivité en dehors du sous-réseau de hello pour les interfaces réseau secondaires, activer basée routage tooensure cette entrée et le trafic sortant utilise hello même interface de réseau.
- Par défaut, tout le trafic sortant à partir de la machine virtuelle est envoyé à l’adresse IP de hello de hello assigné toohello principal de configuration IP de l’interface réseau principale de hello. Vous contrôlez l’adresse IP qui est utilisée pour le trafic sortant système du hello machine virtuelle d’exploitation, mais par défaut, il est via l’interface réseau principale de hello.
- Bonjour passé, toutes les machines virtuelles au sein de hello même ensemble de disponibilité ont été toohave requis un réseau unique ou plusieurs interfaces. Machines virtuelles avec un nombre quelconque de réseau interfaces peuvent existent maintenant dans hello même ensemble de disponibilité, le numéro de toohello pris en charge par hello taille de machine virtuelle. Vous pouvez uniquement ajouter une machine virtuelle tooan groupe à haute disponibilité lorsqu’il est créé si. toolearn plus d’informations sur les groupes à haute disponibilité, lire hello [gérer la disponibilité hello de machines virtuelles dans Azure](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) l’article.
- Tandis que les interfaces réseau dans hello même machine virtuelle peut être connecté toodifferent des sous-réseaux au sein d’un réseau virtuel, les interfaces réseau hello doivent tous être connecté toohello même réseau virtuel.
- Vous pouvez ajouter n’importe quelle adresse IP pour toute configuration IP de n’importe quel pool tooan équilibrage de charge Azure principal de l’interface réseau principal ou secondaire. Bonjour passées, uniquement hello adresse IP principale pour l’interface réseau principale de hello pu être ajouté pool principal de tooa. toolearn plus d’informations sur les adresses IP et des configurations, lire hello [ajouter, modifier ou supprimer des adresses IP](virtual-network-network-interface-addresses.md) l’article.
- Supprimer une machine virtuelle ne supprime pas les interfaces réseau hello tooit attaché. Lorsqu’une machine virtuelle est supprimée, les interfaces réseau de hello sont détachées de hello machine virtuelle. Vous pouvez ajouter hello réseau interfaces toodifferent machines virtuelles ou les supprimer.
- Si une interface réseau a un tooit d’adresse IPv6 privé, vous pouvez attacher il tooa machine virtuelle lors de la création de hello machine virtuelle. Impossible d’attacher une interface réseau avec un tooa d’adresse IPv6 attribué machine virtuelle une fois hello machine virtuelle est créée. Si vous attachez une interface réseau avec une adresse IPv6 privée lors de la création d’un ordinateur virtuel, vous pouvez uniquement joindre cet ordinateur virtuel de réseau interface toohello, quel que soit le nombre d’interfaces réseau prend en charge la taille de machine virtuelle hello. Consultez [réseau des adresses IP d’interface](virtual-network-network-interface-addresses.md) toolearn plus sur l’affectation IP adresses toonetwork interfaces.

## <a name="vm-create"></a>Ajouter existant tooa d’interfaces réseau nouvelle machine virtuelle

Lorsque vous créez une machine virtuelle via le portail de hello, portail de hello crée une interface réseau avec les paramètres par défaut et l’attache toohello machine virtuelle pour vous. Vous ne pouvez pas ajouter existant tooa d’interfaces réseau nouvelle machine virtuelle, ou créer une machine virtuelle avec plusieurs interfaces réseau à l’aide de hello portail Azure. Vous pouvez effectuer à la fois à l’aide de hello CLI ou PowerShell. Vous pouvez ajouter plusieurs interfaces tooa machine virtuelle du réseau comme hello taille de machine virtuelle que vous créez prend en charge. toolearn en savoir plus sur le réseau combien interfaces chaque prend en charge taille machine virtuelle, lire hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articles des tailles de machine virtuelle. interfaces réseau de Hello vous ajoutez tooa machine virtuelle ne peut pas être actuellement attaché tooanother machine virtuelle. toolearn plus d’informations sur la création d’interfaces réseau, lire hello [gérer les interfaces réseau](virtual-network-network-interface.md#create-a-network-interface) l’article.

> [!WARNING]
> Si une interface réseau possède une adresse IPv6 privée affectée tooit, vous pouvez uniquement ajouter hello réseau interface toohello virtual machine lors de la création d’ordinateur virtuel de hello. Vous ne peut pas joindre plus d’une machine virtuelle de réseau interface toohello lorsque vous créez la machine virtuelle de hello, ou après hello machine virtuelle est créée, tant qu’une adresse IPv6 est affectée tooa réseau interface attaché tooa virtual machine. Consultez [réseau des adresses IP d’interface](virtual-network-network-interface-addresses.md) toolearn plus sur l’affectation IP adresses toonetwork interfaces.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az vm create](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>Ajouter un tooan d’interface réseau existante existante de machine virtuelle

Vous pouvez ajouter plusieurs interfaces tooa machine virtuelle du réseau comme hello taille de machine virtuelle que vous ajoutez toosupports des interfaces réseau. toolearn le nombre d’interfaces réseau prend en charge la taille de chaque machine virtuelle, lire hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articles des tailles de machine virtuelle. Hello machine virtuelle que vous voulez tooadd un toomust d’interface réseau prennent en charge hello d’interfaces réseau tooadd et doit être Bonjour s’est arrêté (désalloué) état. interfaces réseau de Hello souhaité tooadd ne peut pas être actuellement attaché tooanother machine virtuelle. Vous ne pouvez pas ajouter tooan d’interfaces réseau existant de machine virtuelle à l’aide de hello portail Azure. tooadd réseau interfaces tooan existant de machine virtuelle, vous devez utiliser hello CLI ou PowerShell. 

> [!WARNING]
> Si une interface réseau possède une adresse IPv6 privée affectée tooit, il ne peut pas ajouté tooan les ordinateur virtuel existant. Vous pouvez uniquement ajouter une interface réseau avec une attribué privé IPv6 adresse tooa machine virtuelle lorsque vous créez une machine virtuelle. Consultez [réseau des adresses IP d’interface](virtual-network-network-interface-addresses.md) toolearn plus sur l’affectation IP adresses toonetwork interfaces.

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az vm nic add](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (référence) ou [procédure détaillée](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (référence) ou [procédure détaillée](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a> Afficher les interfaces réseau d’une machine virtuelle

Vous pouvez afficher hello réseau interfaces actuellement connectées tooa VM toolearn sur la configuration de chaque interface réseau, et des adresses IP hello affecté l’interface de réseau tooeach. 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribué hello un rôle propriétaire, collaborateur ou les collaborateurs de réseau pour votre abonnement. toolearn plus sur l’affectation des rôles tooaccounts, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *virtuels*. Lorsque **virtuels** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **virtuels** panneau qui s’affiche, cliquez sur le nom hello Hello machine virtuelle que vous souhaitez tooview des interfaces réseau pour.
4. Bonjour **paramètres** section du Panneau de machine virtuelle hello qui s’affiche pour hello machine virtuelle que vous avez sélectionné, cliquez sur **interfaces réseau**. toolearn sur les paramètres d’interface réseau et comment toochange les, consultez l’article hello [gérer les interfaces réseau](virtual-network-network-interface.md) l’article. toolearn sur l’ajout, modification ou suppression d’adresses IP attribuées tooa interface de réseau, consultez [les adresses IP de gérer](virtual-network-network-interface-addresses.md).

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az vm show](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a> Supprimer une interface réseau d’une machine virtuelle

Hello machine virtuelle, vous souhaitez tooremove (ou détachez) une interface réseau à partir de doit être hello arrêté (désallouée) et doit avoir actuellement réseau au moins deux interfaces connectées tooit. Vous pouvez supprimer n’importe quelle interface réseau, mais hello machine virtuelle doit toujours avoir au moins un tooit d’interface attaché réseau. Si vous supprimez une interface réseau principale, Azure affecte hello attribut principal toohello interface réseau qui a été attaché toohello hello de machine virtuelle plus longue. 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribué hello un rôle propriétaire, collaborateur ou les collaborateurs de réseau pour votre abonnement. toolearn plus sur l’affectation des rôles tooaccounts, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *virtuels*. Lorsque **virtuels** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **virtuels** panneau qui s’affiche, cliquez sur le nom hello Hello machine virtuelle tooremove une interface réseau pour.
4. Bonjour **paramètres** section du Panneau de machine virtuelle hello qui s’affiche pour hello machine virtuelle que vous avez sélectionné, cliquez sur **interfaces réseau**. toolearn sur les paramètres d’interface réseau et comment toochange les, consultez l’article hello [gérer les interfaces réseau](virtual-network-network-interface.md) l’article. toolearn sur l’ajout, modification ou suppression d’adresses IP attribuées tooa interface de réseau, consultez [les adresses IP de gérer](virtual-network-network-interface-addresses.md).
5. Dans hello panneau des interfaces réseau qui s’affiche, cliquez sur hello **...**  toohello à droite de l’interface de réseau hello que vous souhaitez toodetach.
6. Cliquez sur **Dissocier**. S’il n'existe qu’un seul ordinateur virtuel de réseau interface attaché toohello, hello **détachement** option n’est pas disponible. Cliquez sur **Oui** dans hello de confirmation qui s’affiche.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az vm nic remove](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (référence) ou [procédure détaillée](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Remove-AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (référence) ou [procédure détaillée](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>Étapes suivantes
toocreate une machine virtuelle avec plusieurs interfaces réseau ou des adresses IP, de lire hello suivant des articles :

**Commandes**

|Tâche|Outil|
|---|---|
|Créer une machine virtuelle avec plusieurs cartes d’interface réseau|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Créer une machine virtuelle à carte réseau unique avec plusieurs adresses IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Créer une machine virtuelle à carte réseau unique avec une adresse IPv6 privée (derrière Azure Load Balancer)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [modèle Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
