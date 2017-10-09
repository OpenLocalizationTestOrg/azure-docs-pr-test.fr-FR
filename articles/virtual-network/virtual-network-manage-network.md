---
title: "aaaCreate, modifier ou supprimer un réseau virtuel Azure | Documents Microsoft"
description: "Découvrez comment toocreate, modifier ou supprimer un réseau virtuel dans Azure."
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
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>Créer, modifier ou supprimer un réseau virtuel

Découvrez comment toocreate et supprimer un virtuel réseau et modifier les paramètres, comme les serveurs DNS et l’adresse IP des espaces, pour un réseau virtuel existant.

Un réseau virtuel est une représentation de votre propre réseau dans le cloud de hello. Un réseau virtuel est une isolation logique de hello Azure cloud qui est dédié tooyour abonnement Azure. Pour chaque réseau virtuel que vous créez, vous pouvez :
- Choisissez un tooassign d’espace d’adresse. Un espace d’adressage se compose d’une ou plusieurs plages d’adresses qui sont définies à l’aide d’une notation de routage CIDR (Classless InterDomain Routing), telle que 10.0.0.0/16.
- Choisissez toouse hello DNS fourni par Azure serveur, ou utiliser votre propre serveur DNS. Toutes les ressources qui sont connectés toohello des réseaux virtuels sont affectés à ce nom de tooresolve de serveur DNS dans le réseau virtuel de hello.
- Segment hello du réseau virtuel en sous-réseaux, chacune avec sa propre plage d’adresses, au sein de l’espace d’adressage hello du réseau virtuel de hello. toolearn comment toocreate, modification et suppression des sous-réseaux, consultez [ajouter, modifier ou supprimer des sous-réseaux](virtual-network-manage-subnet.md).

Cet article explique comment toocreate, modifier et supprimer des réseaux virtuels à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.

## <a name="before"></a>Avant de commencer

Avant de commencer les tâches hello qui sont décrites dans cet article, terminer hello suivant des conditions préalables :

- Si vous êtes nouveau tooworking avec des réseaux virtuels, nous vous recommandons de consulter exercice hello dans [créer votre premier réseau virtuel Azure](virtual-network-get-started-vnet-subnet.md). Cet exercice peut vous aider à vous familiariser avec les réseaux virtuels.
- toolearn sur les limites pour les réseaux virtuels, consultez [limite Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Connectez-vous à toohello portail Azure, hello Azure outil de ligne de commande (CLI d’Azure), ou Azure PowerShell à l’aide de votre compte Azure. Si vous n’avez pas encore de compte Azure, inscrivez-vous pour bénéficier d’un [compte d’essai gratuit](https://azure.microsoft.com/free).
- Si vous envisagez toouse toocomplete hello tâches décrites dans cet article de commandes PowerShell, vous devez d’abord [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Assurez-vous que vous disposez de version la plus récente hello Hello applets de commande PowerShell Azure installé. aide tooget pour les commandes PowerShell dans les exemples hello, entrez `get-help <command> -full`.
- Si vous envisagez toouse toocomplete hello tâches décrites dans cet article des commandes CLI d’Azure, vous devez d’abord [installer et configurer Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Assurez-vous que vous disposez de version la plus récente hello de CLI Azure installé. aide tooget avec les commandes CLI d’Azure, entrez `az <command> --help`.


## <a name="create-vnet"></a>Créer un réseau virtuel

toocreate un réseau virtuel :

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui a des autorisations pour le rôle de collaborateur de réseau hello (au minimum) pour votre abonnement. toolearn plus sur l’attribution tooaccounts de rôles et les autorisations, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Cliquez sur **Nouveau** > **Mise en réseau** > **Réseau virtuel**.
3. Sur hello **réseau virtuel** panneau, Bonjour **sélectionner un modèle de déploiement** conservez **le Gestionnaire de ressources** sélectionné, puis cliquez sur **créer**.
4. Sur hello **créer un réseau virtuel** panneau, entrez ou sélectionnez les valeurs pour hello suivant les paramètres, puis cliquez sur **créer**:
    - **Nom**: hello doit être unique dans hello [groupe de ressources](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) que vous sélectionnez toocreate hello réseau virtuel. Vous ne pouvez pas modifier le nom de hello après la création du réseau virtuel hello. Vous pouvez créer plusieurs réseaux virtuels au fil du temps. Pour des suggestions de dénomination, voir [Conventions d’affectation de noms](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions). Suivant une convention d’affectation de noms peut aider à rendre plus facile toomanage plusieurs réseaux virtuels.
    - **L’espace d’adressage**: spécifiez l’espace d’adressage hello en notation CIDR. vous définissez l’espace d’adressage Hello peut être public ou privé (RFC 1918). Si vous définissez un espace d’adressage hello comme public ou privé, l’espace d’adressage hello est accessible uniquement à partir de réseau virtuel hello, à partir de réseaux virtuels interconnectés et à partir de n’importe quel sur des réseaux locaux que vous avez connecté les réseaux virtuels toohello. Vous ne pouvez pas ajouter hello suivant des espaces d’adressage :
        - 224.0.0.0/4 (multidiffusion)
        - 255.255.255.255/32 (diffusion)
        - 127.0.0.0/8 (bouclage)
        - 169.254.0.0/16 (lien-local)
        - 168.63.129.16/32 (DNS interne)

      Bien que vous pouvez définir qu’un seul espace d’adressage lorsque vous créez le réseau virtuel de hello, vous pouvez ajouter des espaces d’adressage plus après la création du réseau virtuel hello. toolearn l’espace de tooadd une adresse tooan de réseau virtuel existant, consultez [ajouter ou supprimer un espace d’adressage](#add-address-spaces) dans cet article.

      >[!WARNING]
      >Si un réseau virtuel comporte des espaces d’adressage qui se chevauchent avec un autre réseau local ou de réseau virtuel, les réseaux hello deux ne peut pas être connectés. Avant de définir un espace d’adressage, réfléchissez peut décider les réseaux virtuels tooconnect hello réseau virtuel tooother ou sur des réseaux locaux dans hello futures.
      >
      >

    - **Nom du sous-réseau**: nom du sous-réseau hello doit être unique au sein du réseau virtuel de hello. Vous ne pouvez pas modifier le nom du sous-réseau hello après que hello sous-réseau est créé. portail de Hello nécessite que vous définissiez un sous-réseau lorsque vous créez un réseau virtuel, même si un réseau virtuel n’est pas nécessaire de toohave tous les sous-réseaux. Dans le portail hello, vous pouvez définir un seul sous-réseau lorsque vous créez un réseau virtuel. Vous pouvez ajouter plusieurs sous-réseaux toohello réseaux ultérieurement, après la création du réseau virtuel hello. tooadd un réseau virtuel tooa de sous-réseau, consultez [créer un sous-réseau](virtual-network-manage-subnet.md#create-subnet) dans [créer, modifier ou supprimer des sous-réseaux](virtual-network-manage-subnet.md). Vous pouvez créer un réseau virtuel comprenant plusieurs sous-réseaux en utilisant PowerShell ou Azure CLI.

      >[!TIP]
      >Parfois, administrateurs de créent des sous-réseaux différents toofilter ou contrôle un routage du trafic entre les sous-réseaux de hello. Avant de définir des sous-réseaux, pensez comment vous souhaitez toofilter et acheminer le trafic entre les sous-réseaux. toolearn en savoir plus sur le filtrage du trafic entre sous-réseaux, consultez [groupes de sécurité réseau](virtual-networks-nsg.md). Azure route automatiquement le trafic entre sous-réseaux, mais vous pouvez remplacer les itinéraires par défaut d’Azure. toolearn toooverride Azure par défaut le routage du trafic sous-réseau, voir [itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md).
      >

    - **Plage d’adresses de sous-réseau**: hello doivent être compris dans l’espace d’adressage hello vous avez entré pour le réseau virtuel de hello. Hello plus petite plage que vous pouvez spécifier est à/29, de qui fournit huit adresses IP pour le sous-réseau de hello. Les réserves de ressources Azure hello tout d’abord et dernière d’adresses dans chaque sous-réseau pour la conformité du protocole. Trois adresses supplémentaires sont réservées à l’usage du service Azure. Par conséquent, un réseau virtuel dont la plage d’adresses de sous-réseau est /29 ne comprend que trois adresses IP utilisables. Si vous envisagez tooconnect passerelle VPN tooa de réseau virtuel, vous devez créer un sous-réseau de passerelle. Pour en savoir plus, voir [Sous-réseau de passerelle](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Vous pouvez modifier la plage d’adresses hello après la création du sous-réseau de hello, dans des conditions spécifiques. toolearn toochange une plage d’adresses de sous-réseau, voir [modifier les paramètres de sous-réseau](#change-subnet) dans [ajouter, modifier ou supprimer des sous-réseaux](virtual-network-manage-subnet.md).
    - **Abonnement :** sélectionnez un [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). Vous ne pouvez pas utiliser hello même réseau virtuel dans plus d’un abonnement Azure. Toutefois, vous pouvez connecter un réseau virtuel dans les réseaux de toovirtual un abonnement dans les autres abonnements. tooconnect des réseaux virtuels dans différents abonnements, utilisez la passerelle VPN à Azure ou réseau virtuel d’homologation. N’importe quelle ressource Azure que vous vous connectez de réseau virtuel de toohello doit être Bonjour même abonnement que le réseau virtuel de hello.
    - **Groupe de ressources** : sélectionnez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) existant ou créez-en un. Une ressource Azure que vous vous connectez toohello des réseaux virtuels peut être Bonjour même groupe de ressources en tant que réseau virtuel de hello ou dans un autre groupe de ressources.
    - **Emplacement** : sélectionnez un [emplacement](https://azure.microsoft.com/regions/) Azure (également appelé région). Un réseau virtuel peut figurer que dans un seul emplacement d’Azure. Toutefois, vous pouvez vous connecter à un réseau virtuel dans un réseau virtuel emplacement tooa dans un autre emplacement à l’aide d’une passerelle VPN. N’importe quelle ressource Azure que vous vous connectez de réseau virtuel de toohello doit être Bonjour même emplacement que le réseau virtuel de hello.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande Azure|[az network vnet create](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>Afficher des réseaux virtuels et des paramètres

tooview des réseaux virtuels et des paramètres :

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui a des autorisations pour le rôle de collaborateur de réseau hello (au minimum) pour votre abonnement. toolearn plus sur l’attribution tooaccounts de rôles et les autorisations, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Dans la zone de recherche du portail hello, entrez **réseaux virtuels**. Dans les résultats de recherche de hello, cliquez sur **réseaux virtuels**.
3. Sur hello **réseaux virtuels** panneau, cliquez sur le réseau virtuel hello que vous souhaitez que les paramètres de tooview pour.
4. Hello paramètres suivants sont répertoriés sur le panneau hello pour le réseau virtuel de hello sélectionné :
    - **Vue d’ensemble**: fournit des informations sur le réseau virtuel hello, y compris l’espace d’adressage et les serveurs DNS. Hello capture d’écran suivante montre les paramètres de vue d’ensemble de hello pour un réseau virtuel nommé **MyVNet**:

        ![Vue d’ensemble de l’interface réseau](./media/virtual-network-manage-network/vnet-overview.png)

      Sur hello **vue d’ensemble** panneau, vous pouvez déplacer un réseau virtuel tooa autre abonnement ou la ressource de groupe. toolearn toomove un réseau virtuel, voir [déplacer des ressources tooa autre groupe de ressources ou d’un abonnement](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json). article de Hello répertorie les conditions préalables requises, et comment les ressources toomove à l’aide de hello portail Azure, PowerShell et CLI d’Azure. Toutes les ressources qui sont des réseaux connectés toohello doivent déplacer avec le réseau virtuel hello.
    - **L’espace d’adressage**: espaces d’adressage hello assignés toohello des réseaux virtuels sont répertoriés. toolearn comment tooadd et supprimer un espace d’adressage, terminer hello étapes dans [ajouter ou supprimer un espace d’adressage](#address-spaces) dans cet article.
    - **Les unités connectées**: toutes les ressources qui sont connectés toohello des réseaux virtuels sont répertoriés. Bonjour précédant la capture d’écran, trois interfaces réseau et un équilibrage de charge sont les réseaux virtuels connectés toohello. Toute nouvelle ressource que vous créez et connectez le réseau virtuel de toohello est répertoriés. Si vous supprimez une ressource qui a été toohello connecté les réseaux virtuels, il n’apparaît plus dans la liste de hello.
    - **Sous-réseaux**: liste des sous-réseaux qui existent dans le réseau virtuel de hello est indiquée. toolearn voir tooadd et supprimer un sous-réseau, [créer un sous-réseau](virtual-network-manage-subnet.md#create-subnet) et [supprimer un sous-réseau](virtual-network-manage-subnet.md#delete-subnet) dans [ajouter, modifier ou supprimer des sous-réseaux](virtual-network-manage-subnet.md).
    - **Serveurs DNS**: vous pouvez spécifier si hello Azure interne au serveur DNS ou un serveur DNS personnalisé fournit la résolution de noms pour les périphériques qui sont connectés toohello des réseaux virtuels. Lorsque vous créez un réseau virtuel à l’aide de hello portail Azure, les serveurs DNS de Azure sont utilisés pour la résolution de nom au sein d’un réseau virtuel, par défaut. les serveurs DNS toomodify hello, hello complète des étapes dans [ajouter, modifier ou supprimer un serveur DNS](#dns-servers) dans cet article.
    - **Homologations**: s’il existe des homologations existantes dans l’abonnement de hello, elles sont répertoriées ici. Vous pouvez afficher les paramètres des homologations existantes, ou créer, modifier ou supprimer des homologations. toolearn en savoir plus sur les homologations, consultez [d’homologation de réseau virtuel](virtual-network-peering-overview.md).
    - **Propriétés**: affiche les paramètres sur les hello réseau virtuel, y compris l’ID de ressource du réseau virtuel hello et hello abonnement Azure, il se trouve dans.
    - **Diagramme**: diagramme de hello fournit une représentation visuelle de tous les périphériques qui sont connectés toohello des réseaux virtuels. diagramme de Hello possède certaines informations clés sur les périphériques de hello. toomanage un périphérique dans cette vue, dans le diagramme de hello, cliquez sur l’appareil de hello.
    - **Paramètres communs des Azure**: toolearn plus à propos des paramètres communs d’Azure, consultez hello informations suivantes :
        *   [Journal d’activité](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [Contrôle d’accès (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [Balises](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [Verrous](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [Script Automation](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande Azure|[az network vnet show](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>Ajouter ou supprimer un espace d’adressage

Vous pouvez ajouter et supprimer des espaces d’adressage pour un réseau virtuel. Un espace d’adressage doit être spécifié dans la notation CIDR et ne peut pas se chevaucher avec d’autres espaces d’adressage dans hello même réseau virtuel. vous définissez des espaces d’adressage Hello peuvent être public ou privé (RFC 1918). Si vous définissez un espace d’adressage hello comme public ou privé, l’espace d’adressage hello est accessible uniquement à partir de réseau virtuel hello, à partir de réseaux virtuels interconnectés et à partir de n’importe quel sur des réseaux locaux que vous avez connecté les réseaux virtuels toohello. Vous ne pouvez pas ajouter hello suivant des espaces d’adressage :

- 224.0.0.0/4 (multidiffusion)
- 255.255.255.255/32 (diffusion)
- 127.0.0.0/8 (bouclage)
- 169.254.0.0/16 (lien-local)
- 168.63.129.16/32 (DNS interne)

tooadd ou supprimer un espace d’adressage :

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui a des autorisations pour le rôle de collaborateur de réseau hello (au minimum) pour votre abonnement. toolearn plus sur l’attribution tooaccounts de rôles et les autorisations, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Dans la zone de recherche du portail hello, entrez **réseaux virtuels**. Dans les résultats de recherche de hello, sélectionnez **réseaux virtuels**.
3. Sur hello **réseaux virtuels** panneau, cliquez sur le réseau virtuel hello pour lequel vous voulez tooadd ou supprimez un espace d’adressage.
4. Sur hello virtuel réseau panneau, sous **paramètres**, cliquez sur **l’espace d’adressage**.
5. Dans Panneau de hello pour l’espace d’adressage hello, effectuez une des options suivantes de hello :
    - **Ajouter un espace d’adressage**: entrez le nouvel espace d’adressage hello. espace d’adressage Hello ne peuvent pas chevaucher un espace d’adressage existant qui est défini pour le réseau virtuel de hello.
    - **Supprimer un espace d’adressage** : cliquez avec le bouton droit sur un espace d’adressage, puis cliquez sur **Supprimer**. Si un sous-réseau existe dans l’espace d’adressage hello, vous ne pouvez pas supprimer l’espace d’adressage hello. tooremove un espace d’adressage, vous devez d’abord supprimer tous les sous-réseaux (et toutes les ressources qui sont les sous-réseaux connectés toohello) qui existe dans l’espace d’adressage hello.
6. Cliquez sur **Enregistrer**.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande Azure|Resource Manager uniquement|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>Ajouter, modifier ou supprimer un serveur DNS

Tous les ordinateurs virtuels qui sont des réseaux connectés toohello auprès des serveurs DNS hello que vous spécifiez pour le réseau virtuel de hello. Elles utilisent également hello spécifié serveur DNS pour la résolution de noms. Chaque carte réseau (NIC) sur un ordinateur virtuel peut avoir ses propres paramètres de serveur DNS. Si une carte réseau possède ses propres paramètres de serveur DNS, elles remplacent les paramètres du serveur DNS hello pour le réseau virtuel de hello. toolearn savoir plus sur les paramètres NIC DNS, consultez [tâches de l’interface et les paramètres réseau](virtual-network-network-interface.md#change-dns-servers). toolearn savoir plus sur la résolution de noms pour les machines virtuelles et instances de rôle dans Azure Cloud Services, consultez [la résolution de noms pour les machines virtuelles et instances de rôle](virtual-networks-name-resolution-for-vms-and-role-instances.md). tooadd, modifier ou supprimer un serveur DNS :

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui a des autorisations pour le rôle de collaborateur de réseau hello (au minimum) pour votre abonnement. toolearn plus sur l’attribution tooaccounts de rôles et les autorisations, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Dans la zone de recherche du portail hello, tapez **réseaux virtuels**. Dans les résultats de recherche de hello, sélectionnez **réseaux virtuels**.
3. Sur hello **réseaux virtuels** panneau, cliquez sur hello vous souhaitez toochange les paramètres DNS pour le réseau virtuel.
4. Sur hello virtuel réseau panneau, sous **paramètres**, cliquez sur **serveurs DNS**.
5. Sélectionnez une des hello options panneau hello qui répertorie les serveurs DNS suivantes :
    - **Par défaut (fourni par Azure)**: tous les noms de ressources et des adresses IP privées sont les serveurs DNS de Azure toohello inscrit automatiquement. Vous pouvez résoudre les noms entre toutes les ressources qui sont connecté toohello même réseau virtuel. Vous ne pouvez pas utiliser les noms de tooresolve de cette option sur plusieurs réseaux virtuels. noms tooresolve sur plusieurs réseaux virtuels, vous devez utiliser un serveur DNS personnalisé.
    - **Personnalisé**: vous pouvez ajouter un ou plusieurs serveurs, des toohello Azure limite pour un réseau virtuel. toolearn savoir plus sur les limites du serveur DNS, consultez [limite Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic). Vous avez hello options suivantes :
        - **Ajouter une adresse**: ajoute la liste des serveurs DNS hello server tooyour réseau virtuel. Cette option enregistre également le serveur DNS de hello avec Azure. Si vous avez déjà inscrit un serveur DNS avec Azure, vous pouvez sélectionner ce serveur DNS dans la liste de hello.
        - **Supprimer une adresse**: cliquez sur le serveur toohello suivant que vous souhaitez tooremove, **X**. Suppression du serveur hello supprime le serveur de hello uniquement à partir de cette liste de réseau virtuel. serveur DNS de Hello reste inscrit dans Azure pour vos autres toouse de réseaux virtuels.
        - **Réorganiser les adresses de serveur DNS**: il est important de tooverify que vous répertoriez vos serveurs DNS Bonjour corriger afin que votre environnement. Listes de serveurs DNS sont utilisés dans l’ordre de hello qu’ils sont spécifiés. Ils ne fonctionnent pas comme un tourniquet (round robin). Si hello premier serveur DNS de hello liste est joignable, hello utilise ce serveur DNS, indépendamment de si hello DNS serveur fonctionne correctement. Supprimez tous les serveurs DNS hello répertoriés et ajoutez-les dans l’ordre hello que vous souhaitez.
        - **Modifier une adresse**: mettez en surbrillance le serveur DNS de hello dans la liste de hello, puis entrez le nouveau nom de hello.
6. Cliquez sur **Enregistrer**.
7. Redémarrez les ordinateurs virtuels de hello qui sont connectés toohello réseau virtuel, afin qu’ils sont affectés des nouveaux paramètres de serveur DNS hello. Machines virtuelles continuer toouse à leurs paramètres DNS en cours jusqu'à ce qu’ils sont redémarrés.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande Azure|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>Supprimer un réseau virtuel

Vous pouvez supprimer un réseau virtuel uniquement s’il n’existe aucun tooit connecté de ressources. S’il existe de sous-réseau connecté tooany de ressources au sein du réseau virtuel de hello, vous devez d’abord supprimer les ressources hello qui sont connectés tooall des sous-réseaux au sein du réseau virtuel de hello. étapes Hello toodelete une ressource varient selon les ressources hello. toolearn comment lire les ressources toodelete toosubnets connecté, hello documentation pour chaque type de ressource, vous souhaitez toodelete. toodelete un réseau virtuel :

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. toolearn plus sur l’attribution tooaccounts de rôles et les autorisations, consultez [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Dans la zone de recherche du portail hello, entrez **réseaux virtuels**. Dans les résultats de recherche de hello, cliquez sur **réseaux virtuels**.
3. Sur hello **réseaux virtuels** panneau, sélectionnez hello virtuel réseau toodelete.
4. Sur le panneau de réseau virtuel hello, tooconfirm qu’il n’y a aucun périphérique connecté toohello de réseau virtuel, sous **paramètres**, cliquez sur **périphériques connectés**. S’il existe des périphériques connectés, vous devez les supprimer avant de pouvoir supprimer les réseaux virtuels hello. Si aucun appareil n’est connecté, cliquez sur **Vue d’ensemble**.
5. Haut hello du Panneau de hello, cliquez sur hello **supprimer** icône.
6. suppression de hello tooconfirm de réseau virtuel de hello, cliquez sur **Oui**.


**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande Azure|[azure network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>Étapes suivantes

- toocreate une machine virtuelle et connectez-la tooa des réseaux virtuels, consultez [créer un réseau virtuel et connecter les machines virtuelles](virtual-network-get-started-vnet-subnet.md#create-vms).
- le trafic réseau de toofilter entre sous-réseaux au sein d’un réseau virtuel, consultez [créer des groupes de sécurité réseau](virtual-networks-create-nsg-arm-pportal.md).
- toopeer un réseau virtuel tooanother du réseau virtuel, consultez [créer un réseau virtuel d’homologation](virtual-network-create-peering.md#portal).
- toolearn sur les options pour la connexion d’un réseau local de tooan de réseau virtuel, consultez [sur la passerelle du VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams).
