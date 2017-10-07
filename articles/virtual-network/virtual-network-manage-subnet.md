---
title: "aaaAdd, modifier ou supprimer un sous-réseau de réseau virtuel Azure | Documents Microsoft"
description: "Découvrez comment tooadd, modifier ou supprimer un sous-réseau de réseau virtuel dans Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>Ajouter, modifier ou supprimer un sous-réseau de réseau virtuel

Découvrez comment tooadd, modifier ou supprimer un sous-réseau de réseau virtuel. 

Si vous n’êtes pas familiarisé avec les réseaux virtuels, nous vous recommandons de lire [Vue d’ensemble des réseaux virtuels Azure](virtual-networks-overview.md) et [Créer, modifier ou supprimer un réseau virtuel](virtual-network-manage-network.md) avant d’ajouter, modifier ou supprimer un sous-réseau. Toutes les ressources Azure déployées dans un réseau virtuel sont déployées dans un sous-réseau au sein d’un réseau virtuel. Plusieurs sous-réseaux sont généralement créés au sein d’un réseau virtuel pour :
- **Filtrer le trafic entre sous-réseaux**. Vous pouvez appliquer toofilter toosubnets groupes réseau de sécurité entrant et sortant du trafic réseau de toutes les ressources (telles que les ordinateurs virtuels) qui se trouvent dans le réseau virtuel de hello. toolearn savoir plus sur toocreate un groupe de sécurité réseau, voir [créer des groupes de sécurité réseau](virtual-networks-create-nsg-arm-pportal.md).
- **Contrôler le routage entre les sous-réseaux**. Azure crée des itinéraires par défaut de façon à ce que le trafic soit automatiquement routé entre les sous-réseaux. Vous pouvez substituer les itinéraires Azure par défaut en créant des itinéraires définis par l’utilisateur. toolearn savoir plus sur les itinéraires définis par l’utilisateur, consultez [créer des itinéraires définis par l’utilisateur](virtual-network-create-udr-arm-ps.md). 

Cet article explique comment tooadd, modifier et supprimer un sous-réseau pour les réseaux virtuels qui ont été créés à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.
 
## <a name="before"></a>Avant de commencer

Avant de commencer les tâches hello qui sont décrites dans cet article, terminer hello suivant des conditions préalables :

- Si vous êtes nouveau tooworking avec des réseaux virtuels, nous vous recommandons de consulter exercice hello dans [créer votre premier réseau virtuel Azure](virtual-network-get-started-vnet-subnet.md). Cet exercice peut vous aider à vous familiariser avec les réseaux virtuels.
- toolearn sur les limites pour les réseaux virtuels, consultez [limite Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Connectez-vous à toohello portail Azure, hello Azure outil de ligne de commande (CLI d’Azure), ou Azure PowerShell à l’aide de votre compte Azure. Si vous n’avez pas encore de compte Azure, inscrivez-vous pour bénéficier d’un [compte d’essai gratuit](https://azure.microsoft.com/free).
- Si vous envisagez toouse toocomplete hello tâches décrites dans cet article de commandes PowerShell, vous devez d’abord [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Assurez-vous que vous disposez de version la plus récente hello Hello applets de commande PowerShell Azure installé. aide tooget pour les commandes PowerShell dans les exemples hello, entrez `get-help <command> -full`.
- Si vous envisagez toouse que toocomplete hello tâches décrites dans cet article des commandes CLI d’Azure, vous devez :
    - [Installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Assurez-vous que vous disposez de version la plus récente hello de CLI Azure installé.
    - Utilisez hello Azure Cloud Shell. Au lieu d’installer hello CLI et ses dépendances, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. toouse hello Cloud interpréteur de commandes, cliquez sur hello Cloud Shell (**> _**) icône haut hello hello portail Azure. 

  aide tooget avec les commandes CLI d’Azure, entrez `az <command> --help`.

## <a name="create-subnet"></a>Ajouter un sous-réseau

tooadd un sous-réseau :

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui a des autorisations pour le rôle de collaborateur de réseau hello (au minimum) pour votre abonnement. toolearn plus sur l’attribution tooaccounts de rôles et les autorisations, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Dans la zone de recherche du portail hello, entrez **réseaux virtuels**. Dans les résultats de recherche de hello, cliquez sur **réseaux virtuels**.
3. Sur hello **réseaux virtuels** panneau, cliquez sur le réseau virtuel hello souhaité tooadd un sous-réseau.
4. Dans le panneau de réseau virtuel hello, cliquez sur **sous-réseaux**.
5. Cliquez sur **+Sous-réseau**.
6. Sur hello **ajouter un sous-réseau** panneau, entrez des valeurs pour hello paramètres suivants :
    - **Nom**: nom de hello doit être unique au sein du réseau virtuel de hello.
    - **Plage d’adresses**: plage de hello doit être unique au sein de l’espace d’adressage hello pour le réseau virtuel de hello. plage de Hello ne peuvent pas chevaucher d’autres plages d’adresses de sous-réseau au sein du réseau virtuel de hello. espace d’adressage Hello doit être spécifié en utilisant la notation de routage inter-domaines sans classe (CIDR). Par exemple, dans un réseau virtuel avec l’espace d’adressage 10.0.0.0/16, vous pouvez définir l’espace d’adressage de sous-réseau 10.0.0.0/24. Hello plus petite plage que vous pouvez spécifier est à/29, de qui fournit huit adresses IP pour le sous-réseau de hello. Les réserves de ressources Azure hello tout d’abord et dernière d’adresses dans chaque sous-réseau pour la conformité du protocole. Trois adresses supplémentaires sont réservées à l’usage du service Azure. Par conséquent, en définissant un sous-réseau avec/29 résoudre les résultats de la plage dans les trois adresses IP utilisables dans un sous-réseau de hello. Si vous envisagez tooconnect passerelle VPN tooa de réseau virtuel, vous devez créer un sous-réseau de passerelle. Pour en savoir plus, voir [Sous-réseau de passerelle](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Vous pouvez modifier la plage d’adresses hello après l’ajout du sous-réseau de hello, dans des conditions spécifiques. toolearn toochange une plage d’adresses de sous-réseau, voir [modifier les paramètres de sous-réseau](#change-subnet) dans cet article.
    - **Groupe de sécurité réseau**: Si vous le souhaitez, vous pouvez associer un groupe de sécurité réseau existant hello sous-réseau toocontrol le trafic réseau entrant et sortant de filtrage pour le sous-réseau de hello. Hello groupe de sécurité réseau doit exister dans hello même abonnement et l’emplacement en tant que réseau virtuel de hello. Il doit également être créé à l’aide du modèle de déploiement du Gestionnaire de ressources hello. toolearn savoir plus sur toocreate un groupe de sécurité réseau, voir [groupes de sécurité réseau](virtual-networks-create-nsg-arm-pportal.md).
    - **Table d’itinéraires**: Si vous le souhaitez, vous pouvez associer une table d’itinéraires existante hello sous-réseau toocontrol le trafic réseau des réseaux tooother de routage. Hello itinéraire table doit exister dans hello même abonnement et l’emplacement en tant que réseau virtuel de hello. Il doit également être créé à l’aide du modèle de déploiement du Gestionnaire de ressources hello. toolearn savoir plus sur les tables d’itinéraires toocreate, voir [itinéraires définis par l’utilisateur](virtual-network-create-udr-arm-ps.md).
    - **Les utilisateurs**: vous pouvez contrôler l’accès toohello sous-réseau à l’aide de rôles intégrés ou vos propres rôles personnalisés. toolearn plus sur l’attribution de rôles et les utilisateurs sous-réseau hello tooaccess, consultez [utiliser rôle affectation toomanage accès tooyour Azure ressources](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access).
7. tooadd hello sous-réseau toohello réseau virtuel que vous avez sélectionné, cliquez sur **OK**.

**Commandes**

|Outil|Commande|
|---|---|
|Azure CLI|[az network vnet subnet create](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>Changer les paramètres de sous-réseau

Vous pouvez modifier les groupes de sécurité réseau, tables d’itinéraires et sous-réseaux de tooa d’accès utilisateur par la gestion des ressources qui sont dans un sous-réseau. toolearn sur ces paramètres, dans [ajouter un sous-réseau](#create-subnet), consultez l’étape 6. Si vous souhaitez espace d’adressage toochange hello d’un sous-réseau, vous devez d’abord supprimer toutes les ressources qui sont dans un sous-réseau de hello. étapes Hello toodelete une ressource varient selon les ressources hello. toolearn comment toodelete les ressources qui se trouvent dans des sous-réseaux, documentation hello lecture pour chaque ressource de type de toodelete. plage d’adresses toochange hello pour un sous-réseau :

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui a des autorisations pour le rôle de collaborateur de réseau hello (au minimum) pour votre abonnement. toolearn plus sur l’attribution tooaccounts de rôles et les autorisations, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Dans la zone de recherche du portail hello, entrez **réseaux virtuels**. Dans les résultats de recherche de hello, cliquez sur **réseaux virtuels**.
3. Sur hello **réseaux virtuels** panneau, cliquez sur le réseau virtuel hello pour lequel vous souhaitez toochange une plage d’adresses de sous-réseau.
4. Cliquez sur le sous-réseau hello pour lequel vous souhaitez la plage d’adresses toochange hello.
5. Dans Panneau de sous-réseau hello, Bonjour **plage d’adresses** , entrez la nouvelle plage d’adresses hello. plage de Hello doit être unique au sein de l’espace d’adressage hello pour le réseau virtuel de hello. plage de Hello ne peuvent pas chevaucher d’autres plages d’adresses de sous-réseau au sein du réseau virtuel de hello. espace d’adressage Hello doit être spécifié à l’aide de la notation CIDR. Par exemple, dans un réseau virtuel avec l’espace d’adressage 10.0.0.0/16, vous pouvez définir l’espace d’adressage de sous-réseau 10.0.0.0/24. Hello plus petite plage que vous pouvez spécifier est à/29, de qui fournit huit adresses IP pour le sous-réseau de hello. Les réserves de ressources Azure hello tout d’abord et dernière d’adresses dans chaque sous-réseau pour la conformité du protocole. Trois adresses supplémentaires sont réservées à l’usage du service Azure. Par conséquent, un sous-réseau avec une plage d’adresses /29 compte trois adresses IP utilisables. Si vous envisagez tooconnect passerelle VPN tooa de réseau virtuel, vous devez créer un sous-réseau de passerelle. Pour en savoir plus, voir [Sous-réseau de passerelle](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Vous pouvez modifier la plage d’adresses hello après la création du sous-réseau de hello, dans des conditions spécifiques. toolearn toochange une plage d’adresses de sous-réseau, voir [modifier les paramètres de sous-réseau](#change-subnet) dans cet article.
6. Cliquez sur **Enregistrer**.

**Commandes**

|Outil|Commande|
|---|---|
|Azure CLI|[az network vnet subnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>Supprimer un sous-réseau

Vous pouvez supprimer un sous-réseau uniquement s’il en existe aucune ressource dans un sous-réseau de hello. S’il existe des ressources dans un sous-réseau de hello, vous devez supprimer les ressources hello qui se trouvent dans le sous-réseau de hello avant de pouvoir supprimer les sous-réseaux hello. étapes Hello toodelete une ressource varient selon les ressources hello. toolearn comment toodelete les ressources qui se trouvent dans des sous-réseaux, documentation hello lecture pour chaque ressource de type de toodelete. toodelete un sous-réseau :

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui a des autorisations pour le rôle de collaborateur de réseau hello (au minimum) pour votre abonnement. toolearn plus sur l’attribution tooaccounts de rôles et les autorisations, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Dans la zone de recherche du portail hello, entrez **réseaux virtuels**. Dans les résultats de recherche de hello, cliquez sur **réseaux virtuels**.
3. Sur hello **réseaux virtuels** panneau, cliquez sur le réseau virtuel hello souhaité toodelete un sous-réseau.
4. Sur hello virtuel réseau panneau, sous **paramètres**, cliquez sur **sous-réseaux**.
5. Dans la liste hello des sous-réseaux qui s’affiche sur le panneau de sous-réseaux hello, sous-réseau de hello avec le bouton droit, vous souhaitez toodelete, cliquez sur **supprimer**, puis cliquez sur **Oui** sous-réseau de hello toodelete.

**Commandes**

|Outil|Commande|
|---|---|
|Azure CLI|[az network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Étapes suivantes

toocreate une machine virtuelle dans un sous-réseau, consultez [créer un réseau virtuel et de déployer des machines virtuelles dans un sous-réseau de hello](virtual-network-get-started-vnet-subnet.md#create-vms).
