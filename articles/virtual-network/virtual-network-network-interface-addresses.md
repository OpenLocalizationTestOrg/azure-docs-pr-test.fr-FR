---
title: "aaaConfigure des adresses IP pour une interface réseau Azure | Documents Microsoft"
description: "Découvrez comment tooadd, modifier et supprimer des adresses IP privées et publiques pour une interface réseau."
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
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>Ajouter, modifier ou supprimer des adresses IP pour une interface réseau Azure

Découvrez comment tooadd, modifier et supprimer des adresses IP privées et publiques pour une interface réseau. Les adresses IP privées affectés l’interface de réseau tooa activer un toocommunicate de l’ordinateur virtuel avec d’autres ressources dans un réseau virtuel Azure et des réseaux connectés. Une adresse IP privée permet également aux communications sortantes toohello Internet à l’aide d’une adresse IP imprévisible. A [adresse IP publique](virtual-network-public-ip-address.md) affecté tooa interface réseau permet les communications entrantes tooa virtual machine à partir de hello Internet. adresse de Hello permet également la communication sortante à partir de l’ordinateur virtuel de hello toohello Internet à l’aide d’une adresse IP prévisible. Pour en savoir plus, consultez [Comprendre les connexions sortantes dans Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Si vous avez besoin de toocreate, modifier ou supprimer une interface réseau, lire hello [gérer une interface réseau](virtual-network-network-interface.md) l’article. Si vous devez tooadd réseau interfaces tooor supprimer les interfaces réseau à partir d’un ordinateur virtuel, lisez hello [ajouter ou supprimer les interfaces réseau](virtual-network-network-interface-vm.md) l’article. 


## <a name="before-you-begin"></a>Avant de commencer

Terminer hello tâches suivantes avant d’effectuer l’une des étapes dans une section de cet article :

- Hello de révision [Azure limite](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn l’article sur les limites pour les adresses IP privées et publiques.
- Connectez-vous à Azure de toohello [portal](https://portal.azure.com), Azure interface de ligne de commande (CLI), ou Azure PowerShell avec un compte Azure. Si vous n’avez pas encore de compte, inscrivez-vous pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/free).
- Si les tâches toocomplete dans cet article, les commandes à l’aide de PowerShell [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente des applets de commande PowerShell Azure hello installé hello. aide tooget pour les commandes PowerShell, des exemples, tapez `get-help <command> -full`.
- Si les tâches toocomplete dans cet article, les commandes à l’aide d’Azure interface de ligne de commande (CLI) [installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente hello Hello CLI d’Azure installé. aide tooget pour les commandes CLI, tapez `az <command> --help`. Au lieu de hello lors de l’installation CLI et les logiciels requis, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. toouse hello Cloud interpréteur de commandes, cliquez sur hello Cloud Shell **> _** bouton haut hello hello [portal](https://portal.azure.com).

## <a name="add-ip-addresses"></a>Ajouter des adresses IP

Vous pouvez ajouter autant [privé](#private) et [public](#public) [IPv4](#ipv4) adresses en tant qu’interface réseau tooa nécessaire, dans les limites de hello répertoriées Bonjour [limites d’Azure ](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) l’article. Vous ne pouvez pas utiliser tooadd de portail hello une interface réseau IPv6 adresse tooan existante (même si vous pouvez utiliser tooadd de portail hello une interface de réseau IPv6 adresse tooa privée lorsque vous créez l’interface de réseau hello). Vous pouvez utiliser PowerShell ou hello CLI tooadd un privée IPv6 adresse tooone [configuration IP secondaire](#secondary) (comme qu’il n’y a aucune des configurations IP secondaires existantes), pour un réseau existant, interface qui n’est pas attachée tooa virtuel ordinateur. Vous ne pouvez pas utiliser n’importe quel outil de tooadd une interface de réseau IPv6 adresse tooa publique. Consultez [IPv6](#ipv6) pour plus d’informations sur l’utilisation des adresses IPv6. 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *interfaces réseau*. Lorsque **interfaces réseau** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **interfaces réseau** panneau qui s’affiche, cliquez sur hello network interface adresse tooadd d’IPv4.
4. Cliquez sur **configurations IP** Bonjour **paramètres** section du panneau hello pour l’interface de réseau hello vous avez sélectionné.
5. Cliquez sur **+ ajouter** dans le panneau de hello qui s’ouvre pour les configurations IP.
6. Spécifiez hello qui suit, puis cliquez sur **OK** tooclose hello **configuration d’ajouter une adresse IP** panneau :

    |Paramètre|Requis ?|Détails|
    |---|---|---|
    |Nom|Oui|Doit être unique pour l’interface de réseau hello|
    |Type|Oui|Étant donné que vous ajoutez une interface réseau IP configuration tooan existante, et chaque interface réseau doit avoir un [principal](#primary) votre seule option de configuration IP, est **secondaire**.|
    |Méthode d’affectation d’adresses IP privées|Oui|[**Dynamique** ](#dynamic) les adresses peuvent changer si l’ordinateur virtuel de hello est redémarré après avoir été Bonjour arrêtée (désallouée) état. Azure affecte une adresse disponible à partir de l’espace d’adressage hello d’interface réseau de hello sous-réseau hello est connectée à. [**Statique** ](#static) adresses ne sont pas libérées tant que l’interface de réseau hello est supprimé. Spécifiez une adresse IP à partir de la plage d’espace hello sous-réseau adresse qui n’est pas actuellement en cours d’utilisation par une autre configuration IP.|
    |Adresse IP publique|Non|**Désactivé :** aucune ressource d’adresse IP publique n’est la configuration d’adresse IP toohello actuellement associé. **Activée :** sélectionnez une adresse IPv4 publique existante ou créez-en une. toolearn comment toocreate une adresse IP publique, lire hello [des adresses IP publiques](virtual-network-public-ip-address.md#create-a-public-ip-address) l’article.|
7. Ajouter manuellement des secondaire privé IP adresses toohello machine virtuelle système d’exploitation en suivant les instructions hello Bonjour [affecter plusieurs adresses IP des systèmes d’exploitation de machine toovirtual](virtual-network-multiple-ip-addresses-portal.md#os-config) l’article. Consultez [privé](#private) les adresses IP pour connaître les considérations avant d’ajouter manuellement le système d’exploitation IP adresses tooa machine virtuelle. N’ajoutez pas de n’importe quel système d’exploitation ordinateur virtuel de publique IP adresses toohello.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network nic ip-config create](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>Modifier les paramètres d’adresse IP

Vous devrez peut-être la méthode d’affectation hello toochange d’une adresse IPv4, la modification hello adresse IPv4 statique, ou modifier hello l’adresse IP publique affectée interface de réseau tooa. Si vous changez d’adresse IPv4 privée de hello d’une configuration IP secondaire associée à une interface réseau secondaire dans une machine virtuelle (en savoir plus sur [interfaces réseau principal et secondaire](virtual-network-network-interface-vm.md#about)), hello place virtuel machine dans hello arrêtée (désallouée) état avant la fin de hello comme suit : 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *interfaces réseau*. Lorsque **interfaces réseau** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **interfaces réseau** panneau qui s’affiche, cliquez sur l’interface réseau hello vous souhaitez tooview ou modifiez les paramètres d’adresse IP pour.
4. Cliquez sur **configurations IP** Bonjour **paramètres** section du panneau hello pour l’interface de réseau hello vous avez sélectionné.
5. Cliquez sur configuration IP de hello souhaité toomodify à partir de la liste hello dans le panneau de hello qui s’ouvre pour les configurations IP.
6. Modifier les paramètres de hello, comme vous le souhaitez, à l’aide de hello plus d’informations sur les paramètres hello à l’étape 6 de hello [ajouter une configuration IP](#create-ip-config) section de cet article. Cliquez sur **enregistrer** Panneau de hello tooclose pour la configuration IP de hello vous avez modifié.

>[!NOTE]
>Si l’interface réseau principale de hello a plusieurs configurations IP et modifiez hello adresse IP privée du principal de configuration IP hello, vous devez réattribuer manuellement hello principaux et secondaire IP adresses toohello interface réseau dans Windows (pas obligatoire pour Linux). toomanually affecter l’interface de réseau IP adresses tooa au sein d’un système d’exploitation, lire hello [affecter plusieurs adresses IP toovirtual machines](virtual-network-multiple-ip-addresses-portal.md#os-config) l’article. Consultez [privé](#private) les adresses IP pour connaître les considérations avant d’ajouter manuellement le système d’exploitation IP adresses tooa machine virtuelle. N’ajoutez pas de n’importe quel système d’exploitation ordinateur virtuel de publique IP adresses toohello.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>Supprimer des adresses IP

Vous pouvez supprimer [privé](#private) et [public](#public) les adresses IP à partir d’une interface réseau, mais une interface réseau doit toujours avoir au moins un tooit d’adresse IPv4 privée.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *interfaces réseau*. Lorsque **interfaces réseau** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **interfaces réseau** panneau qui s’affiche, cliquez sur hello réseau interface tooremove les adresses IP.
4. Cliquez sur **configurations IP** Bonjour **paramètres** section du panneau hello pour l’interface de réseau hello vous avez sélectionné.
5. Avec le bouton droit une [secondaire](#secondary) configuration IP (vous ne pouvez pas supprimer hello [principal](#primary) configuration) vous voulez toodelete, cliquez sur **supprimer**, puis cliquez sur **Oui**  suppression de hello tooconfirm. Si la configuration de hello contient une ressource d’adresse IP publique associée tooit, les ressources hello sont dissociée de la configuration d’adresse IP hello, mais les ressources hello ne sont pas supprimé.
6. Fermer hello **configurations IP** panneau.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network nic ip-config delete](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>Configurations IP

[Privé](#private) et (facultativement) [public](#public) tooone les adresses IP sont affectées ou davantage de configurations IP affectée interface de réseau tooa. Il existe deux types de configuration IP :

### <a name="primary"></a>Primaire

Une configuration IP principale est assignée à chaque interface réseau. Une configuration IP principale :

- A un [privé](#private) [IPv4](#ipv4) tooit de l’adresse attribuée. Vous ne pouvez pas attribuer privé [IPv6](#ipv6) configuration IP principale de l’adresse tooa.
- Peut également avoir un [public](#public) tooit d’adresse IPv4. Vous ne pouvez pas affecter une public tooa principale ou secondaire IP configuration d’adresse IPv6. Vous pouvez cependant, affecter un public IPv6 adresse équilibrage de charge Azure tooan, qui peut charger solde adresse IPv6 privée de l’ordinateur de le virtuel trafic tooa. Pour en savoir plus, consultez les [informations et limitations relatives à IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations).

### <a name="secondary"></a>Secondaire

En outre tooa principal de configuration IP, une interface réseau peut-être avoir zéro ou plusieurs configurations IP secondaires affectées tooit. Une configuration IP secondaire :

- Doit avoir un tooit d’adresse IPv4 ou IPv6 privé. Si l’adresse de hello est IPv6, interface de réseau de hello ne peut avoir qu’une seule configuration IP secondaire. Si l’adresse hello est IPv4, interface de réseau hello peut avoir plusieurs configurations IP secondaires affectées tooit. toolearn en savoir plus sur le nombre d’adresses IPv4 privé et publique peut avoir des tooa interface de réseau, consultez hello [Azure limite](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) l’article.  
- Peut également avoir un tooit d’adresse IPv4 publique, si l’adresse IP privée de hello est IPv4. Si l’adresse IP privée de hello est IPv6, vous ne pouvez attribuer un IPv4 ou IPv6 adresse toohello IP configuration publique. Affectation d’interface réseau de plusieurs IP adresses tooa est tel qu’utile dans les scénarios :
    - D’héberger plusieurs sites web ou services avec des adresses IP différentes et des certificats SSL sur un serveur unique.
    - Une machine virtuelle joue le rôle d’appliance virtuelle réseau, comme un pare-feu ou un équilibreur de charge.
    - Bonjour tooadd de capacité des hello des adresses IPv4 privées pour une des interfaces tooan équilibrage de charge Azure principal pool de hello réseau. Bonjour passées, uniquement hello principal adresse IPv4 pour l’interface réseau principale de hello peut être ajouté par pool principal de tooa. toolearn en savoir plus sur comment tooload équilibrer plusieurs configurations d’IPv4, consultez hello [plusieurs configurations IP d’équilibrage de la charge](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article. 
    - Bonjour capacité tooload solde IPv6 adresse affectée tooa interface réseau. toolearn en savoir plus sur comment tooload équilibrer les adresses IPv6 privées tooa, consultez hello [d’équilibrer les adresses IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.


## <a name="address-types"></a>Types d’adresse

Vous pouvez affecter hello les types de tooan d’adresses IP suivants [configuration IP](#ip-configurations):

### <a name="private"></a>Privé

Privé [IPv4](#ipv4) adresses activer un toocommunicate de l’ordinateur virtuel avec d’autres ressources dans un réseau virtuel ou d’autres réseaux connectés. Un ordinateur virtuel ne peut pas être communiqué entrant vers ni hello virtuels peuvent communiquer sortant avec privé [IPv6](#ipv6) adresse, avec une exception. Un ordinateur virtuel peuvent communiquer avec équilibrage de charge Azure hello à l’aide d’une adresse IPv6. Pour en savoir plus, consultez les [informations et limitations relatives à IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations). 

Par défaut, les serveurs DHCP Azure hello attribuer les adresses IPv4 privées hello pour hello [configuration IP principale](#primary) de hello interface toohello interface réseau du réseau au sein du système d’exploitation de machine virtuelle hello. Sauf si nécessaire, vous devez jamais affecter la valeur adresse hello d’une interface réseau au sein du système d’exploitation de l’ordinateur virtuel de hello. 

> [!WARNING]
> Si l’adresse IPv4 de hello définie comme adresse IP principale de hello d’une interface réseau au sein du système d’exploitation de l’ordinateur virtuel est jamais différent de celui de l’adresse IPv4 privée hello affecté toohello principal de configuration IP de l’interface réseau principale de hello attaché tooa machine virtuelle dans Azure, vous perdez connectivité toohello virtual machine.

Il existe des scénarios où il est nécessaire toomanually définir hello une adresse IP d’une interface réseau au sein du système d’exploitation de l’ordinateur virtuel de hello. Par exemple, vous devez définir manuellement un système d’exploitation Windows dans les adresses IP de principal et secondaires hello lors de l’ajout de plusieurs tooan d’adresses IP machine virtuelle Azure. Pour une machine virtuelle Linux, vous devrez uniquement des adresses IP secondaires de toomanually ensemble hello. Consultez [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](virtual-network-multiple-ip-addresses-portal.md#os-config) pour plus d’informations. Lorsque vous définissez manuellement les adresses IP de hello hello système d’exploitation, il est recommandé que vous attribuez toujours configuration de hello adresses toohello IP pour une interface réseau à l’aide de la méthode d’affectation statique (plutôt que dynamique) hello. Affectation d’adresse hello à l’aide de la méthode statique hello garantit que l’adresse de hello ne change pas dans Azure. Si vous avez besoin toochange hello adresse tooan configuration d’adresse IP, il est recommandé que vous :

1. machine virtuelle de hello tooensure reçoit une adresse à partir des serveurs DHCP Azure de hello, modifier l’affectation de hello de hello IP adresse tooDHCP précédent dans le système d’exploitation de hello et redémarrage hello virtual machine.
2. Arrêter (désallouer la) machine virtuelle de hello.
3. Modifier l’adresse IP de hello pour la configuration IP de hello dans Azure.
4. Démarrer l’ordinateur virtuel de hello.
5. [Configurer manuellement](virtual-network-multiple-ip-addresses-portal.md#os-config) hello secondaire toomatch de dans le système d’exploitation de hello (et l’adresse IP principale hello dans Windows), les adresses IP que vous définissez dans Azure.
 
En suivant les étapes précédentes hello, hello privé IP adresse affectée toohello interface réseau dans Azure et dans le système d’exploitation de l’ordinateur virtuel, restent identiques hello. suivi tookeep dont les machines virtuelles au sein de votre abonnement que vous avez définies manuellement les adresses IP au sein d’un système d’exploitation, envisagez d’ajouter un Azure [balise](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags) toohello virtuels. Vous pouvez utiliser « attribution d’adresses IP : statique », par exemple. De cette manière, vous pouvez facilement trouver des machines virtuelles de hello dans votre abonnement que vous avez définies manuellement l’adresse IP de hello pour hello système d’exploitation.

En outre, tooenabling un toocommunicate de l’ordinateur virtuel avec d’autres ressources au sein de hello mêmes ou connectés réseaux virtuels, une adresse IP privée adresse également permet un toohello sortant de machine virtuelle toocommunicate Internet. Les connexions sortantes sont adresse de réseau source traduite par son adresse IP publique imprévisible tooan Azure. toolearn plus d’informations sur Azure connectivité Internet sortante, lire hello [Azure connectivité Internet sortante](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article. Vous ne peut pas communiquer l’adresse IP privée de l’ordinateur virtuel de tooa entrant à partir de hello Internet.

### <a name="public"></a>Public

Les adresses IP publiques activer l’ordinateur virtuel connectivité entrante tooa hello Internet. Les connexions sortantes toohello Internet utiliser une adresse IP prévisible. Pour en savoir plus, consultez [Comprendre les connexions sortantes dans Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Vous pouvez attribuer une configuration d’IP du tooan d’adresse IP publique, mais n’est pas nécessaire. Si vous n’affectez pas un ordinateur virtuel des tooa d’adresse publique IP, il peut toujours communiquer sortant toohello Internet à l’aide de son adresse IP privée. toolearn plus d’informations sur les adresses IP publiques, lire hello [adresse IP publique](virtual-network-public-ip-address.md) l’article.

Il existe des limites nombre toohello de privé et des adresses IP publiques que vous pouvez assigner tooa interface de réseau. Pour plus d’informations, consultez hello [Azure limite](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) l’article.

> [!NOTE]
> Azure se traduit par privée tooa publique adresse IP une machine virtuelle. Par conséquent, le système d’exploitation de hello est sans se préoccuper de toute adresse IP publique affectée tooit, donc il n’existe aucun besoin tooever manuellement attribuer une adresse IP publique au sein du système d’exploitation de hello.

## <a name="assignment-methods"></a>Méthodes d’affectation

Les adresses IP publiques et privées sont attribuées à l’aide de hello affectation méthodes suivantes :

### <a name="dynamic"></a>Dynamique

Les adresses IPv4 et (éventuellement) IPv6 privées dynamiques sont assignées par défaut. Les adresses dynamiques peuvent changer si l’ordinateur virtuel de hello est placée dans hello arrêtée (désallouée) d’état, puis démarré. Si vous ne souhaitez pas toochange d’adresses IPv4 pour vie hello de machine virtuelle de hello, affectez des adresses de hello à l’aide de la méthode statique hello. Vous pouvez uniquement affecter une adresse IPv6 privée à l’aide de la méthode d’affectation dynamique hello. Vous ne pouvez attribuer une configuration publique d’IP tooan adresse IPv6 à l’aide de ces deux méthodes.

### <a name="static"></a>statique

Les adresses affectées à l’aide de la méthode statique hello ne changent pas jusqu'à ce qu’un ordinateur virtuel est supprimé. Vous attribuez manuellement une statique privé tooan IP configuration d’adresse IPv4 à partir de l’espace d’adressage hello pour interface réseau de hello sous-réseau hello est. Vous pouvez attribuer (éventuellement) d’une publique ou privée statique tooan IP configuration d’adresse IPv4. Vous ne pouvez pas affecter une statique publique ou privée tooan IP configuration d’adresse IPv6. toolearn en savoir plus sur la façon dont Azure attribue des adresses IPv4 publiques statiques, consultez hello [adresse IP publique](virtual-network-public-ip-address.md) l’article.

## <a name="ip-address-versions"></a>Versions d’adresse IP

Vous pouvez spécifier hello versions suivantes lors de l’attribution d’adresses :

### <a name="ipv4"></a>IPv4

Chaque interface réseau doit avoir une configuration IP [principale](#primary) avec une adresse [privée](#private) [IPv4](#ipv4) qui lui est assignée. Vous pouvez ajouter une ou plusieurs configurations IP [secondaires](#secondary) disposant chacune d’une adresse IPv4 privée et (éventuellement ) d’une adresse IPv4 [publique](#public).

### <a name="ipv6"></a>IPv6

Vous pouvez affecter privé zéro ou un [IPv6](#ipv6) adresse tooone configuration IP secondaire d’une interface réseau. interface de réseau Hello ne peut pas avoir toutes les configurations IP secondaires existantes. Vous ne pouvez pas ajouter une configuration IP avec une adresse IPv6 à l’aide du portail de hello. Utiliser PowerShell ou hello CLI tooadd une configuration IP avec une privée IPv6 adresse tooan interface réseau existante. interface de réseau Hello ne peut pas être attaché tooan existant de machine virtuelle.

> [!NOTE]
> Si vous pouvez créer une interface réseau avec une adresse IPv6 à l’aide du portail de hello, vous ne pouvez pas ajouter un réseau interface tooa nouveau ou existant, ordinateur virtuel existant, à l’aide du portail de hello. Utiliser PowerShell ou hello Azure CLI 2.0 toocreate une interface réseau avec une adresse IPv6 privée, puis l’attachement de l’interface de réseau hello lors de la création d’un ordinateur virtuel. Impossible d’attacher une interface réseau avec une adresse IPv6 privée affectée l’ordinateur virtuel existant de tooit tooan. Vous ne pouvez pas ajouter une configuration d’IP privée des tooan d’adresse IPv6 pour toute interface connecté de réseau tooa machine virtuelle à l’aide d’outils (portail, CLI ou PowerShell).

Vous ne pouvez pas affecter une public tooa principale ou secondaire IP configuration d’adresse IPv6.

## <a name="next-steps"></a>Étapes suivantes
toocreate une machine virtuelle avec différentes configurations IP, lire hello suivant des articles :

|Task|Outil|
|---|---|
|Créer une machine virtuelle avec plusieurs cartes d’interface réseau|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Créer une machine virtuelle à carte réseau unique avec plusieurs adresses IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Créer une machine virtuelle à carte réseau unique avec une adresse IPv6 privée (derrière Azure Load Balancer)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [modèle Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
