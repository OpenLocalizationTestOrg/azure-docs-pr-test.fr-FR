---
title: aaaCreate, modifier ou supprimer une adresse IP publique Azure | Documents Microsoft
description: "Découvrez comment toocreate, modifier ou supprimer une adresse IP publique."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>Créer, modifier ou supprimer une adresse IP publique

En savoir plus sur une adresse IP publique de l’adresse, comment toocreate, modifier et supprimer un. Une adresse IP publique est une ressource disposant de ses propres paramètres configurables. L’attribution d’un tooother d’adresse IP publique ressources Azure active :
- Tooresources de connectivité Internet entrant telles que les Machines virtuelles Azure (VM), groupes de mise à l’échelle de machines virtuelles Azure, passerelle VPN à Azure, passerelles d’Application et équilibreurs de charge Azure connecté à Internet. Ressources Azure ne reçoivent pas les communications entrantes de hello Internet sans une adresse IP publique. Alors que certaines ressources Azure sont, par nature, accessibles via les adresses IP publiques, les autres ressources doivent avoir des adresses IP publiques affectées toobe toothem accessible à partir de hello Internet.
- Connectivité sortante toohello Internet à l’aide d’une adresse IP prévisible. Par exemple, un ordinateur virtuel peuvent communiquer sortant toohello Internet sans un tooit d’adresse IP publique, mais son adresse est l’adresse réseau traduit par une adresse publique de tooan Azure imprévisible. Affectation d’une ressource de tooa d’adresse IP publique vous permet de tooknow adresse IP qui est utilisée pour les connexions sortantes hello. Si elle est prévisible, adresse de hello peut changer, selon la méthode d’affectation hello choisi. Pour plus d’informations, consultez [Créer une adresse IP publique](#create-a-public-ip-address). toolearn plus d’informations sur les connexions sortantes à partir des ressources Azure, lisez hello [comprendre les connexions sortantes](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.

## <a name="before-you-begin"></a>Avant de commencer

Terminer hello tâches suivantes avant d’effectuer l’une des étapes dans une section de cet article :

- Hello de révision [Azure limite](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn l’article sur les limites pour les adresses IP publiques.
- Connectez-vous à Azure de toohello [portal](https://portal.azure.com), Azure interface de ligne de commande (CLI), ou Azure PowerShell avec un compte Azure. Si vous n’avez pas encore de compte, inscrivez-vous pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/free).
- Si les tâches toocomplete dans cet article, les commandes à l’aide de PowerShell [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente des applets de commande PowerShell Azure hello installé hello. aide tooget pour les commandes PowerShell, des exemples, tapez `get-help <command> -full`.
- Si les tâches toocomplete dans cet article, les commandes à l’aide d’Azure interface de ligne de commande (CLI) [installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente hello Hello CLI d’Azure installé. aide tooget pour les commandes CLI, tapez `az <command> --help`. Au lieu de hello lors de l’installation CLI et les logiciels requis, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. toouse hello Cloud interpréteur de commandes, cliquez sur hello Cloud Shell **> _** bouton haut hello hello [portal](https://portal.azure.com).

Le coût des adresses IP publiques est modique. tooview hello tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page. 

## <a name="create-a-public-ip-address"></a>Créer une adresse IP publique

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *adresse ip publique*. Lorsque **des adresses IP publiques** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Cliquez sur **+ ajouter** Bonjour **adresse IP publique** panneau s’affiche.
4. Entrez ou sélectionnez les valeurs pour hello suivant paramètres Bonjour **créer une adresse IP publique** panneau qui s’affiche, puis cliquez sur **créer**:

    |Paramètre|Requis ?|Détails|
    |---|---|---|
    |Nom|Oui|nom de Hello doit être unique au sein du groupe de ressources hello que vous sélectionnez.|
    |Version de l’adresse IP|Oui| Sélectionnez IPv4 ou IPv6. Tandis que IPv4 publique les adresses peuvent être affectées tooseveral ressources Azure, une adresse IP publique de IPv6 peut uniquement avoir équilibrage de charge tooan connecté à Internet. équilibrage de charge Hello peut charger des machines virtuelles de IPv6 d’équilibrer le trafic tooAzure. En savoir plus sur [IPv6 trafic toovirtual machines d’équilibrage de charge](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
    |Affectation d’adresses IP|Oui|**Dynamique :** adresses dynamiques sont attribuées uniquement une fois l’adresse IP publique de hello associé tooa carte réseau attachée tooa VM et hello machine virtuelle est démarré pour hello première fois. Les adresses dynamiques peuvent modifier si hello de machine virtuelle hello NIC est attaché toois arrêté (désalloué). Hello adresse reste hello même si hello machine virtuelle est redémarré ou arrêté (mais pas désalloué). **Statique :** adresses statiques sont affectées lors de l’adresse IP publique de hello est créé. Des adresses statiques ne pas l’état de modification même que si hello est placé dans hello arrêté (désallouée). adresse de Hello n’a lieu que lorsque hello NIC est supprimé. Vous pouvez modifier la méthode d’affectation hello après que hello carte réseau est créé. Si vous sélectionnez IPv6 pour hello **IP version**, méthode d’affectation disponible uniquement hello est **dynamique**.|
    |Délai d’inactivité (minutes)|Non|Nombre de minutes pendant tookeep sans se baser sur les clients des messages Keepalive toosend d’ouvrir une connexion TCP ou HTTP. Si vous sélectionnez IPv6 pour **Version IP**, cette valeur ne peut pas être modifiée. |
    |Étiquette du nom DNS|Non|Doit être unique au sein de hello emplacement Azure vous créez nom hello dans (pour tous les abonnements et tous les clients). Bonjour Azure service DNS public inscrit automatiquement hello nom et adresse IP pour pouvoir vous connecter tooa ressource avec le nom de hello. Azure ajoute *location.cloudapp.azure.com* (où emplacement est l’emplacement que vous sélectionnez hello) nom toohello vous fournissez toocreate hello entièrement le nom DNS complet. Si vous choisissez toocreate les deux versions de l’adresse, hello même nom DNS est attribué tooboth hello IPv4 et IPv6. Hello service DNS Azure contient les enregistrements de nom A d’IPv4 et IPv6 AAAA et répond avec les deux enregistrements lorsque le nom DNS de hello est recherché. client de Hello choisit l’adresse les toocommunicate (IPv4 ou IPv6) avec.|
    |Créer une adresse IPv6 (ou IPv4)|Non| L’affichage de l’adresse IPv6 ou IPv4 dépend du paramétrage de **Version IP**. Par exemple, si vous sélectionnez **IPv4** pour **Version IP**, **IPv6** s’affiche ici.
    |Nom (visible uniquement si vous avez coché hello **créer une adresse IPv6 (ou IPv4)** case à cocher)|Oui, si vous sélectionnez hello **créer d’IPv6** (ou IPv4) case à cocher.|Hello nom doit être différent de celui hello vous commencez par entrer pour hello **nom** dans cette liste. Si vous choisissez toocreate IPv4 et une adresse IPv6, portail de hello crée deux distinct publiques ressources d’adresse IP, l’autre avec chaque version d’adresse IP affectée au tooit.|
    |Attribution d’adresses IP (visible uniquement si vous avez coché hello **créer une adresse IPv6 (ou IPv4)** case à cocher)|Oui, si vous sélectionnez hello **créer d’IPv6** (ou IPv4) case à cocher.|Si la case à cocher hello indique **créer une adresse IPv4**, vous pouvez sélectionner une méthode d’attribution. Si la case à cocher hello indique **créer une adresse IPv6**, vous ne pouvez pas sélectionner une méthode d’attribution, car il doit être **dynamique**.|
    |Abonnement|Oui|Doit exister dans hello même [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) en tant que ressource de hello souhaité tooassociate hello adresse IP publique à.|
    |Groupe de ressources|Oui|Peut exister dans hello identique ou différent, [groupe de ressources](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) en tant que ressource de hello souhaité tooassociate hello adresse IP publique à.|
    |Lieu|Oui|Doit exister dans hello même [emplacement](https://azure.microsoft.com/regions), également appelée ressource hello tooassociate hello adresse IP publique à tooas de la région.|

**Commandes**

Si le portail de hello fournit hello option toocreate deux publiques ressources d’adresse IP (une IPv4 et une seule IPv6), hello suivant les commandes CLI et PowerShell créer une ressource avec une adresse pour une adresse IP version ou hello d’autres. Si vous souhaitez que les deux publics ressources d’adresse IP, une pour chaque version IP, vous devez exécuter commande hello à deux reprises, en spécifiant des noms différents et des versions pour les ressources d’adresse IP publiques hello. 

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network public-ip create](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>Afficher une adresse IP publique, modifier ses paramètres ou la supprimer

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est attribuées (au minimum) des autorisations pour le rôle de collaborateur de réseau hello pour votre abonnement. Hello de lecture [rôles intégrés pour le contrôle d’accès en fonction du rôle de Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) toolearn article plus sur l’attribution de rôles et autorisations tooaccounts.
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *adresse ip publique*. Lorsque **des adresses IP publiques** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **des adresses IP publiques** panneau qui s’affiche, cliquez sur le nom hello de hello adresse IP publique vous souhaitez tooview, modifiez les paramètres d’ou supprimez.
4. Dans le panneau hello qui s’affiche pour l’adresse IP publique hello, de hello suivant les options selon que vous souhaitez tooview, supprimer ou modifier l’adresse IP publique de hello.
    - **Vue**: hello **vue d’ensemble** la section du Panneau de hello présente les paramètres de clé pour l’adresse IP publique de hello, tels que de l’interface de réseau hello associés trop (si l’interface de réseau tooa associé est l’adresse de hello). portail de Hello n’affiche pas de version hello d’adresse hello (IPv4 ou IPv6). informations de version tooview hello, utilisez hello PowerShell ou CLI commande tooview hello adresse IP publique. Si la version d’adresse IP hello est IPv6, hello adresse attribuée s’affiche pas par le portail de hello, PowerShell ou hello CLI. 
    - **Supprimer**: toodelete hello adresse IP publique, cliquez sur **supprimer** Bonjour **vue d’ensemble** section du Panneau de hello. Si l’adresse de hello est actuellement associé tooan configuration d’adresse IP, il ne peut pas être supprimé. Si l’adresse de hello est actuellement associé à une configuration, cliquez sur **recréez-la** adresse de hello toodissociate à partir de la configuration d’adresse IP hello.
    - **Modifier** : cliquez sur **Configuration**. Modifier les paramètres à l’aide des informations de hello à l’étape 4 de hello [créer une adresse IP publique](#create-a-public-ip-address) section de cet article. attribution de hello toochange pour une adresse IPv4 statique toodynamic, vous devez tout d’abord la dissocier hello adresse IPv4 à partir de la configuration d’adresse IP hello à qu'il est associé. Vous pouvez ensuite modifier hello affectation méthode toodynamic et cliquez sur **associer** tooassociate hello IP adresse toohello même IP configuration, une configuration différente ou vous pouvez la laisser dissociée. toodissociate une adresse IP publique, Bonjour **vue d’ensemble** , cliquez sur **recréez-la**.

>[!WARNING]
>Lorsque vous modifiez la méthode d’affectation hello de toodynamic statique, vous perdez les adresse IP hello qui a été attribué l’adresse IP publique de toohello. Alors que hello des serveurs DNS publics Azure gèrent un mappage entre les adresses statiques ou dynamiques et une étiquette de nom DNS (si vous avez défini un), une adresse IP dynamique peut modifier lorsque hello machine virtuelle est démarré après Bonjour arrêtée (désallouée) d’état. adresse de hello tooprevent de modifier, affecter une adresse IP statique.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[AZ réseau public-ip-list](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) les adresses IP publiques toolist, [az réseau public-ip-show](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow paramètres ; [mise à jour de az réseau public-ip](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate ; [az réseau public-ip supprimer](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve une adresse IP publique adresse d’objet et afficher ses paramètres, [Set-AzureRmPublicIpAddress](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooupdate paramètres ; [Remove-AzureRmPublicIpAddress](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>Étapes suivantes
Affecter des adresses IP publiques lors de la création de hello suivant des ressources Azure :

- Machines virtuelles [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure Load Balancer accessible sur Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Application Gateway Azure](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Connexion site à site à l’aide d’une passerelle VPN Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Groupe de machines virtuelles identiques Azure](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
