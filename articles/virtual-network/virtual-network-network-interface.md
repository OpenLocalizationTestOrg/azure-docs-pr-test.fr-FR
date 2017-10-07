---
title: "aaaCreate, modifier ou supprimer une interface réseau Azure | Documents Microsoft"
description: "Découvrez les éléments est d’une interface réseau et comment modifier les paramètres de toocreate et supprimer un."
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
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>Créer, modifier ou supprimer une interface réseau

Découvrez comment toocreate, modifier les paramètres d’et supprimer une interface réseau. Une interface réseau active un toocommunicate de Machine virtuelle Azure avec Internet, Azure et des ressources locales. Lorsque vous créez une machine virtuelle à l’aide de hello portail Azure, le portail de hello crée une interface réseau avec les paramètres par défaut pour vous. Vous pouvez à la place choisir toocreate les interfaces réseau avec des paramètres personnalisés et ajouter au moins un ordinateur réseau interfaces tooa virtuel lors de sa création. Vous pouvez également les paramètres d’interface réseau toochange par défaut pour une interface réseau existante. Cet article explique comment toocreate une interface réseau avec des paramètres personnalisés, les paramètres existants, tels que l’affectation de réseau filtre (groupe de sécurité réseau), attribution de sous-réseau, paramètres de serveur DNS et le transfert IP, de modifier et supprimer une interface réseau.

Si vous avez besoin de tooadd, modifier ou supprimer des adresses IP pour une interface réseau, lire hello [les adresses IP de gérer](virtual-network-network-interface-addresses.md) l’article. Si vous avez besoin d’interfaces réseau tooadd ou supprimez des interfaces réseau de machines virtuelles, lire hello [ajouter ou supprimer les interfaces réseau](virtual-network-network-interface-vm.md) l’article.


## <a name="before-you-begin"></a>Avant de commencer

Terminer hello tâches suivantes avant d’effectuer l’une des étapes dans une section de cet article :

- Hello de révision [Azure limite](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn l’article sur les limites des interfaces réseau.
- Connectez-vous à Azure de toohello [portal](https://portal.azure.com), Azure interface de ligne de commande (CLI), ou Azure PowerShell avec un compte Azure. Si vous n’avez pas encore de compte, inscrivez-vous pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/free).
- Si les tâches toocomplete dans cet article, les commandes à l’aide de PowerShell [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente des applets de commande PowerShell Azure hello installé hello. aide tooget pour les commandes PowerShell, des exemples, tapez `get-help <command> -full`.
- Si les tâches toocomplete dans cet article, les commandes à l’aide d’Azure interface de ligne de commande (CLI) [installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente hello Hello CLI d’Azure installé. aide tooget pour les commandes CLI, tapez `az <command> --help`. Au lieu de hello lors de l’installation CLI et les logiciels requis, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. toouse hello Cloud interpréteur de commandes, cliquez sur hello Cloud Shell **> _** bouton haut hello hello [portal](https://portal.azure.com).

## <a name="create-a-network-interface"></a>Créer une interface réseau

Lorsque vous créez une machine virtuelle à l’aide de hello portail Azure, le portail de hello crée une interface réseau avec les paramètres par défaut pour vous. Si vous devez spécifier au lieu de tous vos paramètres d’interface réseau, vous pouvez créer une interface réseau avec des paramètres personnalisés et attacher la machine virtuelle de hello réseau interface tooa lors de la création d’ordinateur virtuel de hello (à l’aide de PowerShell ou hello CLI d’Azure). Vous pouvez également créer une interface réseau et l’ajouter tooan ordinateur virtuel existant (à l’aide de PowerShell ou hello CLI d’Azure). toolearn comment toocreate un ordinateur virtuel avec un existant interface ou tooadd au réseau, ou supprimer des interfaces réseau de machines virtuelles existantes, lire hello [ajouter ou supprimer les interfaces réseau](virtual-network-network-interface-vm.md) l’article. Avant de créer une interface réseau, vous devez avoir un [réseau virtuel](virtual-networks-create-vnet-arm-pportal.md) dans hello même emplacement et abonnement vous créez une interface réseau.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *interfaces réseau*. Lorsque **interfaces réseau** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **interfaces réseau** panneau qui s’affiche, cliquez sur **+ ajouter**.
4. Bonjour **interface réseau de créer** panneau qui s’affiche, entrez, ou sélectionnez les valeurs pour hello suivant les paramètres, puis cliquez sur **créer**:

    |Paramètre|Requis ?|Détails|
    |---|---|---|
    |Nom|Oui|nom de Hello doit être unique au sein du groupe de ressources hello que vous sélectionnez. Au fil du temps, vous accumulerez probablement plusieurs interfaces réseau dans votre abonnement Azure. Hello de lecture [conventions d’affectation de noms](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) pour des suggestions lors de la création d’un toomake convention d’affectation de noms, la gestion de plusieurs interfaces plus faciles du réseau de l’article. nom de Hello ne peut pas être modifié une fois que l’interface de réseau hello est créée.|
    |Réseau virtuel|Oui|Sélectionnez hello de réseau virtuel pour l’interface de réseau hello. Vous ne pouvez affecter un réseau interface tooa réseau virtuel qui existe dans hello même abonnement et l’emplacement en tant qu’interface de réseau hello. Après la création d’une interface réseau, vous ne pouvez pas modifier le réseau virtuel de hello à qu'il est assigné. Hello machine virtuelle que vous ajoutez hello réseau interface toomust existent également dans hello même emplacement et abonnement en tant qu’interface de réseau hello.|
    |Sous-réseau|Oui|Sélectionnez un sous-réseau au sein du réseau virtuel de hello que vous avez sélectionné. Vous pouvez modifier le sous-réseau de hello interface de réseau hello est assigné tooafter, il est créé.|
    |Affectation d’adresses IP privées|Oui| Dans ce paramètre, vous choisissez méthode d’affectation hello pour hello adresse IPv4. Choisissez hello affectation méthodes suivantes : **dynamique :** lorsque vous sélectionnez cette option, Azure affecte automatiquement une adresse disponible à partir de l’espace d’adressage hello du sous-réseau hello vous avez sélectionné. Azure peut attribuer une interface de réseau tooa autre adresse de démarrage de la machine virtuelle de hello dans après avoir été Bonjour arrêtée (désallouée) état. Hello adresse reste hello même si l’ordinateur virtuel de hello est redémarré sans avoir été Bonjour arrêtée (désallouée) état. **Statique :** lorsque vous sélectionnez cette option, vous devez affecter manuellement une adresse IP disponible dans l’espace d’adressage hello du sous-réseau hello vous avez sélectionné. Des adresses statiques ne changent pas jusqu'à ce que vous les modifiez ou l’interface de réseau hello est supprimé. Vous pouvez modifier la méthode d’affectation hello après que hello network interface est créée. serveur DHCP Azure de Hello affecte cette interface de réseau adresse toohello hello système d’exploitation de machine virtuelle de hello.|
    |Groupe de sécurité réseau|Non| Laissez la valeur trop**aucun**, sélectionnez un existant [groupe de sécurité réseau](virtual-networks-nsg.md), ou [créer un groupe de sécurité réseau](virtual-networks-create-nsg-arm-pportal.md). Groupes de sécurité réseau permettent toofilter du trafic réseau vers et depuis une interface réseau. Vous pouvez appliquer l’interface de réseau du zéro ou un réseau sécurité groupe tooa. Zéro ou un groupe de sécurité réseau peut également être appliqué interface de réseau toohello sous-réseau hello est assigné à. Lorsqu’un groupe de sécurité réseau n’est appliqué tooa réseau interface interface de réseau hello sous-réseau hello est assignée, des résultats inattendus parfois se produisent. toonetwork appliqué interfaces et des sous-réseaux, les groupes de sécurité de réseau de tootroubleshoot lire hello [résoudre les groupes de sécurité réseau](virtual-network-nsg-troubleshoot-portal.md#nsg) l’article.|
    |Abonnement|Oui|Sélectionnez l’un de vos [abonnements](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) Azure. machine virtuelle de Hello vous attachez un réseau de hello virtual network interface tooand vous connecterez existe toomust Bonjour même abonnement.|
    |Adresse IP privée (IPv6)|Non| Si vous activez cette case à cocher, une adresse IPv6 est l’interface de réseau toohello attribué, de plus toohello adresse IPv4 affectées interface de réseau toohello. Consultez hello [IPv6](#IPv6) section de cet article contient des informations importantes sur l’utilisation du protocole IPv6 avec des interfaces réseau. Vous ne pouvez pas sélectionner une méthode d’affectation pour hello adresse IPv6. Si vous choisissez tooassign une adresse IPv6, il est chargé de la méthode dynamique hello.
    |Nom de IPv6 (apparaît uniquement lorsque hello **l’adresse IP privée (IPv6)** case à cocher est activée) |Oui, si hello **l’adresse IP privée (IPv6)** case à cocher est activée.| Ce nom est attribué tooa une configuration IP secondaire pour l’interface de réseau hello. En savoir plus sur les configurations IP Bonjour [afficher les paramètres d’interface réseau](#view-network-interface-settings) section de cet article.|
    |Groupe de ressources|Oui|Sélectionnez un [groupe de ressources](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) ou créez-en un. Une interface réseau peut exister dans hello même ou autre groupe de ressources, à l’ordinateur virtuel de hello vous joindre à un, ou hello virtual network vous connecter à.|
    |Lieu|Oui|machine virtuelle de Hello vous attachez un réseau de hello virtual network interface tooand vous connecterez existe toomust Bonjour même [emplacement](https://azure.microsoft.com/regions), également appelée tooas une région.|

portail de Hello ne fournit pas hello option tooassign une interface de réseau IP adresse toohello publique lorsque vous créez, bien que le portail de hello créer une adresse IP publique et affectez-le interface de réseau tooa lorsque vous créez une machine virtuelle à l’aide du portail de hello. toolearn comment tooadd un réseau toohello l’adresse IP publique de l’interface après sa création, lecture hello [les adresses IP de gérer](virtual-network-network-interface-addresses.md) l’article. Si vous souhaitez toocreate une interface réseau avec une adresse IP publique, vous devez utiliser hello CLI ou PowerShell toocreate hello interface réseau.

>[!Note]
> Azure affecte une interface de réseau MAC adresse toohello uniquement après l’interface de réseau hello tooa attaché virtual machine et machine virtuelle de hello est hello premier démarrage. Vous ne pouvez pas spécifier l’adresse MAC de hello qu’Azure attribue interface de réseau toohello. Hello interface de réseau toohello MAC adresse reste affectée jusqu'à ce que l’interface de réseau hello est supprimé ou adresse IP privée hello affecté toohello principal de configuration IP de l’interface réseau principale de hello est modifié. toolearn plus d’informations sur les adresses IP et des configurations IP, lire hello [les adresses IP de gérer](virtual-network-network-interface-addresses.md) l’article.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network nic create](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>Afficher les paramètres d’interface réseau

Vous pouvez afficher et modifier la plupart des paramètres d’une interface réseau après sa création.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *interfaces réseau*. Lorsque **interfaces réseau** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **interfaces réseau** panneau qui s’affiche, cliquez sur l’interface réseau hello vous souhaitez tooview ou modifiez les paramètres de.
4. Hello paramètres suivants sont répertoriés dans le panneau de hello qui s’affiche pour l’interface de réseau hello que vous avez sélectionné :
    - **Vue d’ensemble :** fournit des informations sur l’interface de réseau hello, tels que des adresses IP hello affectés tooit, interface de réseau hello hello/le sous-réseau de réseau virtuel est assigné à, et interface de réseau hello hello ordinateur virtuel est attaché trop (le cas Il est attaché tooone). Hello image suivante présente les paramètres de vue d’ensemble de hello pour une interface réseau nommé **mywebserver256**: ![présentation de l’interface réseau](./media/virtual-network-network-interface/nic-overview.png) vous pouvez déplacer un groupe de ressources différent de tooa interface réseau ou abonnement en cliquant sur (**modifier**) toohello suivant **groupe de ressources** ou **nom de l’abonnement**. Si vous déplacez d’interface réseau de hello, vous devez déplacer l’interface de réseau toutes les ressources associées toohello avec lui. Si interface de réseau hello est attaché tooa virtual machine, par exemple, vous devez également déplacer des machines virtuelles de hello et autres ressources liées à la machine virtuelle. toomove une interface réseau, lire hello [déplacer des ressources tooa nouveau groupe de ressources ou d’un abonnement](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) l’article. article de Hello répertorie les conditions préalables et comment les ressources toomove hello portail Azure, PowerShell et hello CLI d’Azure.
    - **Les configurations IP :** publiques et privées adresses IPv4 et IPv6 tooIP configurations assignées sont répertoriées ici. Si une adresse IPv6 est affectée la configuration d’adresse IP tooan, adresse de hello ne s’affiche pas. En savoir plus sur les configurations IP et comment les adresses IP tooadd et supprimer Bonjour [adresses IP de configurer pour une interface réseau Azure](virtual-network-network-interface-addresses.md) l’article. Le transfert IP et l’affectation de sous-réseau sont également configurés dans cette section. toolearn plus d’informations sur ces paramètres, lire hello [activer ou désactiver le transfert IP](#enable-or-disable-ip-forwarding) et [modifier l’attribution de sous-réseau](#change-subnet-assignment) sections de cet article.
    - **Serveurs DNS :** vous pouvez spécifier quel serveur DNS une interface réseau est assignée par hello serveurs DHCP d’Azure. Hello interface réseau peut hériter des paramètres de hello de hello est affectée à interface de réseau de réseau virtuel hello ou ont un paramètre personnalisé qui remplace le paramètre hello pour le réseau virtuel de hello auquel elle est assignée. toomodify ce qui est affiché, hello terminé les étapes Bonjour [serveurs DNS de modification](#change-dns-servers) section de cet article.
    - **Groupe de sécurité réseau (NSG) :** affiche ce qui est du groupe de sécurité réseau associé l’interface de réseau toohello (le cas échéant). Un groupe de sécurité réseau contient des règles de trafic entrant et sortant du trafic réseau toofilter pour l’interface de réseau hello. Si un groupe de sécurité réseau est l’interface de réseau associé toohello, hello nom Hello que NSG associé s’affiche. toomodify ce qui est affiché, hello terminé les étapes Bonjour [gérer les associations de groupe de sécurité réseau](virtual-network-manage-nsg-arm-portal.md#manage-associations) l’article.
    - **Propriétés :** présente les paramètres sur l’interface de réseau hello, y compris son adresse MAC (vide si l’interface de réseau hello n’est pas attaché tooa virtual machine) de clé et hello d’abonnement, il existe dans.
    - **Les règles de sécurité efficace :** les règles de sécurité sont répertoriés si l’interface de réseau hello est attaché tooa machine virtuelle en cours d’exécution, et un groupe de sécurité réseau est l’interface de réseau associé toohello, sous-réseau hello auquel elle est assignée ou les deux. toolearn en savoir plus sur ce qui est affiché, lire hello [résoudre les groupes de sécurité réseau](virtual-network-nsg-troubleshoot-portal.md#nsg) l’article. toolearn plus d’informations sur les groupes de sécurité réseau, lire hello [groupes de sécurité réseau](virtual-networks-nsg.md) l’article.
    - **Itinéraires effectifs :** itinéraires répertoriés si l’interface de réseau hello est attaché tooa machine virtuelle en cours d’exécution. les itinéraires Hello sont une combinaison de hello par défaut Azure itinéraires, les itinéraires définis par l’utilisateur (UDR) et tous les itinéraires BGP qui peuvent exister pour l’interface de réseau hello sous-réseau hello est assigné à. toolearn en savoir plus sur ce qui est affiché, lire hello [résoudre les itinéraires](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) l’article. toolearn plus d’informations sur Azure par défaut et UDRs, lecture hello [itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md) l’article.
    - **Paramètres communs de Azure Resource Manager :** toolearn plus d’informations sur les paramètres communs du Gestionnaire de ressources Azure, lire hello [le journal d’activité](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [(IAM) de contrôle d’accès](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [balises ](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [Verrouille](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json), et [script d’automatisation](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) articles.

**Commandes**

Si une adresse IPv6 est affectée l’interface de réseau tooa, hello PowerShell sortie retourne faits hello que hello adresse est assignée, mais il ne retourne pas les adresses hello attribué. De même, les hello CLI retourne faits hello qui hello adresse est attribué, mais retourne *null* dans sa sortie pour l’adresse de hello.

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[liste des cartes réseau réseau AZ](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list) tooview des interfaces de réseau dans l’abonnement de hello ; [az réseau nic afficher](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooview des paramètres pour une interface réseau|
|PowerShell|[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) interfaces réseau tooview hello abonnement ou afficher les paramètres pour une interface réseau|

## <a name="change-dns-servers"></a>Modifier les serveurs DNS

hello DHCP Azure toohello interface réseau du serveur dans le système d’exploitation de machine virtuelle hello est affecté au serveur DNS de Hello. serveur DNS de Hello affecté est tout paramètre hello du serveur DNS pour une interface réseau. toolearn savoir plus sur les paramètres de résolution de nom pour une interface réseau, consultez [la résolution de noms pour les ordinateurs virtuels](virtual-networks-name-resolution-for-vms-and-role-instances.md). interface de réseau Hello permettre hériter des paramètres de hello du réseau virtuel de hello, ou utiliser ses propres paramètres uniques qui remplacent le paramètre hello pour le réseau virtuel de hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *interfaces réseau*. Lorsque **interfaces réseau** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **interfaces réseau** panneau qui s’affiche, cliquez sur l’interface réseau hello vous souhaitez tooview ou modifiez les paramètres de.
4. Dans le panneau hello pour l’interface de réseau hello vous avez sélectionné, cliquez sur **serveurs DNS** sous **paramètres**.
5. Cliquez sur l’une des deux options suivantes :
    - **Hériter de réseau virtuel (par défaut)**: choisissez ce paramètre serveur option tooinherit hello DNS défini pour l’interface de réseau hello hello réseau virtuel est assigné à. Au niveau du réseau virtuel hello, un serveur DNS personnalisé ou un serveur DNS fourni par Azure de hello est défini. Hello fournie par Azure serveur DNS peut résoudre les noms d’hôtes pour les ressources affectées toohello même réseau virtuel. Nom de domaine complet doit être tooresolve utilisé pour les ressources affectées toodifferent des réseaux virtuels.
    - **Personnalisé**: vous pouvez configurer vos propres noms de tooresolve du serveur DNS sur plusieurs réseaux virtuels. Entrez l’adresse IP de hello du serveur de hello souhaité toouse comme un serveur DNS. adresse du serveur DNS Hello que vous spécifiez reçoit uniquement interface de réseau toothis et substitue à que les paramètres DNS pour l’interface de réseau hello hello réseau virtuel sont assigné.
6. Cliquez sur **Enregistrer**.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>Activer et désactiver le transfert IP

Le transfert IP permet de machine virtuelle de hello à qu'une interface réseau est attachée :
- Recevoir le trafic réseau ne destiné pas une des adresses IP de hello affectés tooany des configurations IP de hello affecté l’interface de réseau toohello.
- Envoyer le trafic réseau avec une adresse IP de source différente que hello tooone d’attribué une des configurations IP de l’interface d’un réseau.

paramètre de Hello doit être activé pour chaque interface réseau qui est l’ordinateur virtuel toohello attachés qui reçoit le trafic qui hello tooforward des besoins de machine virtuelle. Un ordinateur virtuel peut transférer le trafic qu’il possède plusieurs interfaces réseau ou un tooit interface connecté de réseau unique. Alors que le transfert IP est un paramètre d’Azure, hello virtual machine doit également exécuter un application tooforward en mesure de hello le trafic, telles que les pare-feu, l’optimisation de réseau étendue et applications d’équilibrage de charge. Lorsqu’un ordinateur virtuel est en cours d’exécution des applications de réseau, ordinateur virtuel de hello est souvent tooas auxquels un matériel de réseau virtuel. Vous pouvez afficher une liste d’équipements virtuels du réseau prêt toodeploy Bonjour [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). Le transfert IP est généralement utilisé avec les routages définis par l’utilisateur. toolearn plus d’informations sur les itinéraires définis par l’utilisateur, lecture hello [itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md) l’article.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *interfaces réseau*. Lorsque **interfaces réseau** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **interfaces réseau** panneau qui s’affiche, cliquez sur l’interface réseau hello vous souhaitez tooenable ou désactivez le transfert IP pour.
4. Dans le panneau hello pour l’interface de réseau hello vous avez sélectionné, cliquez sur **configurations IP** Bonjour **paramètres** section.
5. Cliquez sur **activé** ou **désactivé** paramètre de hello toochange (paramètre par défaut).
6. Cliquez sur **Enregistrer**.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>Modifier l’affectation de sous-réseau

Vous pouvez modifier le sous-réseau de hello, mais pas hello réseau virtuel, affectée à une interface réseau.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *interfaces réseau*. Lorsque **interfaces réseau** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **interfaces réseau** panneau qui s’affiche, cliquez sur l’interface réseau hello vous souhaitez tooview ou modifiez les paramètres de.
4. Cliquez sur **configurations IP** sous **paramètres** dans le panneau hello pour l’interface de réseau hello vous avez sélectionné. Si la liste de toutes les adresses IP privées de toutes les configurations IP ont **(statique)** toothem suivant, vous devez modifier hello IP adresse affectation méthode toodynamic en hello étapes qui suivent. Toutes les adresses IP privées doivent être attribuées avec affectation sous-réseau hello affectation dynamique méthode toochange hello pour l’interface de réseau hello. Si les adresses de hello sont affectées par la méthode dynamique hello, continuer toostep cinq. Si toutes les adresses IPv4 sont attribuées avec la méthode d’affectation statique hello, procédez hello suivant les étapes toochange hello affectation méthode toodynamic :
    - Cliquez sur configuration IP de hello souhaité toochange hello méthode d’affectation adresse IPv4 pour à partir de la liste de hello des configurations IP.
    - Dans hello panneau qui s’affiche pour la configuration IP de hello, cliquez sur **dynamique** pour hello **affectation** (méthode). Vous ne pouvez attribuer une adresse IPv6 avec la méthode d’affectation statique hello.
    - Cliquez sur **Enregistrer**.
5. Sélectionnez sous-réseau hello tooconnect Bonjour réseau interface toofrom Bonjour **sous-réseau** liste déroulante.
6. Cliquez sur **Enregistrer**. Nouvelles adresses dynamiques sont affectés à partir de la plage d’adresses de sous-réseau hello pour le sous-réseau hello. Après avoir affecté hello interface tooa nouveau sous-réseau, vous pouvez affecter une adresse IPv4 statique à partir de la plage d’adresses hello nouveau sous-réseau si vous choisissez. toolearn plus d’informations sur l’ajout, modification et suppression d’adresses IP pour une interface réseau, lire hello [les adresses IP de gérer](virtual-network-network-interface-addresses.md) l’article.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>Supprimer une interface réseau

Vous pouvez supprimer une interface réseau tant qu’il n’est pas attaché tooa virtual machine. S’il est attaché tooa virtual machine, vous devez première place hello Bonjour arrêté (désalloué) état des ordinateurs virtuels, puis détachement de l’interface de réseau de hello à partir de la machine virtuelle de hello, avant de supprimer l’interface de réseau hello. toodetach une interface réseau à partir d’un ordinateur virtuel, les étapes hello complète Bonjour [détacher une interface réseau à partir d’un ordinateur virtuel](virtual-network-network-interface-vm.md#vm-remove-nic) section Hello [ajouter ou supprimer les interfaces réseau](virtual-network-network-interface-vm.md) l’article. Suppression d’une machine virtuelle détache de tous les tooit de joint d’interfaces réseau, mais ne supprime pas les interfaces réseau de hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *interfaces réseau*. Lorsque **interfaces réseau** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Interface de réseau avec le bouton hello toodelete et cliquez sur **supprimer**.
4. Cliquez sur **Oui** tooconfirm la suppression de l’interface de réseau hello.

Lorsque vous supprimez une interface réseau, n’importe quel MAC ou les adresses IP attribuées tooit sont libérés.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network nic delete](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Étapes suivantes
toocreate une machine virtuelle avec plusieurs interfaces réseau ou l’adresse IP, les adresses, lisez hello suivant des articles :

**Commandes**

|Tâche|Outil|
|---|---|
|Créer une machine virtuelle avec plusieurs cartes d’interface réseau|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Créer une machine virtuelle à carte réseau unique avec plusieurs adresses IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Créer une machine virtuelle à carte réseau unique avec une adresse IPv6 privée (derrière Azure Load Balancer)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [modèle Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
