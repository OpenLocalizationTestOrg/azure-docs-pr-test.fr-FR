---
title: "aaaCreate, modifier ou supprimer un réseau virtuel Azure d’homologation | Documents Microsoft"
description: "Découvrez comment toocreate, modifier ou supprimer un réseau virtuel d’homologation."
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
ms.date: 07/26/2017
ms.author: jdial
ms.openlocfilehash: 70f85364ab23e23533ad276aeec0156cebe89be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>Créer, modifier ou supprimer une homologation de réseau virtuel

Découvrez comment toocreate, modifier ou supprimer un réseau virtuel d’homologation. Permet d’homologation de réseau virtuel vous tooconnect deux réseaux virtuels dans hello même emplacement Azure via hello réseau principal Azure. Une fois homologuer, les réseaux virtuels deux hello sont toujours gérés comme des ressources distinctes. Les ressources dans un réseau virtuel communiquent avec hello même latence et la bande passante comme si les ressources hello étaient hello même réseau virtuel. Si vous n’êtes pas familiarisé avec le réseau virtuel d’homologation, nous vous recommandons de lire hello [présentation d’homologation du réseau virtuel](virtual-network-peering-overview.md) et fin hello [créer un didacticiel d’homologation du réseau virtuel](virtual-network-create-peering.md), avant la fin tâches Hello dans cet article.

## <a name="before-you-begin"></a>Avant de commencer

Terminer hello tâches suivantes avant d’effectuer les étapes décrites dans les sections de cet article :

- Hello de révision [Azure limite](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn l’article sur les limites pour l’homologation.
- Connectez-vous avec un compte Azure toohello portail Azure, Azure interface de ligne de commande (CLI) ou Azure PowerShell. Si vous n’avez pas encore de compte, inscrivez-vous pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/free).
- Si les tâches toocomplete dans cet article, les commandes à l’aide de PowerShell [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente des applets de commande PowerShell Azure hello installé hello. aide tooget pour les commandes PowerShell, des exemples, tapez `get-help <command> -full`.
- Si les tâches toocomplete dans cet article, les commandes à l’aide d’Azure interface de ligne de commande (CLI) [installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente hello Hello CLI d’Azure installé. aide tooget pour les commandes CLI, tapez `az <command> --help`. Au lieu de hello lors de l’installation CLI et les logiciels requis, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Hello Cloud Shell a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. toouse hello Cloud interpréteur de commandes, cliquez sur hello Cloud Shell **> _** bouton haut hello hello [portal](https://portal.azure.com). 

## <a name="create-a-peering"></a>Créer une homologation

>[!NOTE]
>Il existe plusieurs conditions, contraintes, et considérations toosuccessfully créer un réseau virtuel d’homologation. Avant de créer une homologation, assurez-vous de vous avez familiarisé avec hello [exigences et contraintes](#requirements-and-constraints) et [autorisations requises](#permissions).
>

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui est affecté hello nécessaire [rôle ou des autorisations](#permissions).
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *réseaux virtuels*. Lorsque **réseaux virtuels** s’affiche dans les résultats de recherche hello, cliquez dessus. Ne sélectionnez pas **des réseaux virtuels (classiques)** si elle apparaît dans la liste hello, comme vous ne pouvez pas créer une homologation à partir d’un réseau virtuel déployé via le modèle de déploiement classique hello.
3. Bonjour **réseaux virtuels** panneau qui s’affiche, cliquez sur le réseau virtuel de hello souhaité toocreate une homologation pour.
4. Dans le volet hello qui s’affiche pour le réseau virtuel de hello vous avez sélectionné, cliquez sur **homologations** Bonjour **paramètres** section.
5. Cliquez sur **+ Ajouter**. 
6. <a name="add-peering"></a>Bonjour **ajouter d’homologation** panneau, entrez ou sélectionnez des valeurs pour hello suivant les paramètres :
    - **Nom :** nom hello pour l’homologation de hello doit être unique au sein du réseau virtuel de hello.
    - **Modèle de déploiement de réseau virtuel :** sélectionnez quels hello de modèle de déploiement virtuel réseau que vous souhaitez toopeer avec a été déployée via.
    - **Je sais mon ID de ressource :** si vous avez accès en lecture toohello virtuel réseau toopeer avec, laissez cette case à cocher est désactivée. Si vous n’avez pas réseau virtuel de toohello accès en lecture ou d’abonnement que vous souhaitez toopeer avec, cette case à cocher. Entrez l’ID de ressource complet hello de réseau virtuel de hello à toopeer avec Bonjour **ID de ressource** zone qui apparaît lorsque vous avez coché la case de hello. ressource Hello ID que vous entrez doit être d’un réseau virtuel qui existe dans hello Azure même [emplacement](https://azure.microsoft.com/regions) en tant que ce réseau virtuel. ID de ressource complet Hello semble similairetrop/abonnements/<Id>/resourceGroups/ < resource-group-name > /providers/Microsoft.Network/virtualNetworks/ < virtual-network-name >. Vous pouvez obtenir l’ID de ressource hello pour un réseau virtuel en affichant les propriétés hello pour un réseau virtuel. toolearn tooview des propriétés de hello pour un réseau virtuel, voir [gérer les réseaux virtuels](virtual-network-manage-network.md#view-vnet).
    - **L’abonnement :** hello sélectionnez [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) de réseau virtuel de hello souhaité toopeer avec. Un ou plusieurs abonnements sont répertoriés, selon le nombre d’abonnements auxquels votre compte a accès en lecture. Si vous avez coché hello **ID de ressource** case à cocher, ce paramètre n’est pas disponible. Vous pouvez homologuer des réseaux virtuels dans des abonnements différents pour autant que les deux réseaux virtuels aient été créés via le Gestionnaire de ressources. toopeer de capacité Hello entre les abonnements créés par le biais des modèles de déploiement est en version préliminaire. S’inscrire pour la version préliminaire de hello avant de créer une homologation entre les réseaux virtuels déployés par l’intermédiaire des modèles de déploiement différentes qui existent dans différents abonnements. En savoir plus sur la façon tooregister pour l’aperçu de hello et [homologues des réseaux virtuels créés par le biais des modèles de déploiement différentes dans différents abonnements](create-peering-different-deployment-models-subscriptions.md).
    - **Réseau virtuel :** sélectionnez hello réseau virtuel que vous souhaitez toopeer avec. Vous pouvez sélectionner un réseau virtuel créé via un modèle de déploiement d’Azure, mais les réseaux virtuels hello doivent être Bonjour même emplacement que le réseau virtuel de hello vous êtes initialisation hello d’homologation de. Vous devez avoir lecture accéder toohello réseau virtuel pour qu’il toobe visible dans la liste de hello. Si un réseau virtuel est répertorié, mais grisée, il peut être, car l’espace d’adressage de réseau virtuel de hello hello chevauche l’espace d’adressage hello pour ce réseau virtuel. Si les espaces d’adressage de réseaux virtuels se chevauchent, il n’est pas possible d’homologuer ces réseaux. Si vous avez coché hello **ID de ressource** case à cocher, ce paramètre n’est pas disponible.
    - **Autoriser l’accès de réseau virtuel :** sélectionnez **activé** (par défaut) si vous souhaitez tooenable la communication entre les réseaux virtuels hello deux. L’activation des communications entre les réseaux virtuels permet des ressources connectées toocommunicate de réseau virtuel tooeither avec d’autres avec hello même la bande passante et la latence comme s’ils étaient connecté toohello même réseau virtuel. Toutes les communications entre les ressources dans des réseaux virtuels deux hello sont sur hello réseau privé Azure. Hello **VirtualNetwork** marqueur par défaut pour les groupes de sécurité réseau englobe le réseau virtuel de hello et ressources réseau virtuel. balises de valeur par défaut de groupe de sécurité, du réseau toolearn en savoir plus sur lecture hello [présentation des groupes de sécurité réseau](virtual-networks-nsg.md#default-tags) l’article.  Sélectionnez **désactivé** si vous ne souhaitez pas que le trafic tooflow toohello homologuer les réseaux virtuels. Vous pouvez sélectionner **désactivé** si vous avez homologuer un réseau virtuel avec un autre réseau virtuel, mais il peut arriver que toodisable le flux de trafic entre les réseaux virtuels hello deux. Il se peut que vous trouviez plus pratique d’activer ou de désactiver les homologations que de les supprimer et recréer. Lorsque ce paramètre est désactivé, le trafic ne circule pas entre hello homologuer les réseaux virtuels.
    - **Autoriser le trafic transféré :** vérifier cette toohello de trafic transféré tooallow zone homologuer réseau virtuel (le trafic ne provenant ne pas de réseau virtuel ressources de hello) réseau virtuel de tooflow toothis. Trafic est courant lorsque vous avez déployé un matériel de réseau virtuel dans le réseau virtuel de hello vous êtes l’homologation avec et créé des itinéraires définis par l’utilisateur tooforward trafic via hello réseau virtuel. Si vous laissez cette case est désactivée (valeur par défaut), le trafic transféré à partir du réseau virtuel de hello ressources ne peut pas de flux de réseau virtuel de toothis. Pendant l’activation de cette fonctionnalité autorise le trafic de hello transmis via hello d’homologation, il ne crée aucun itinéraire défini par l’utilisateur ni équipements virtuels du réseau. Les itinéraires définis par l’utilisateur et les appliances virtuelles sont créés séparément. Pour en savoir plus, voir [Itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md).
    - **Autoriser le transit de la passerelle :** cette case à cocher si vous avez un réseau virtuel de réseau virtuel passerelle toothis joint et que vous souhaitez tooallow trafic hello homologuer tooflow de réseau virtuel via la passerelle de hello. Par exemple, ce réseau virtuel peut être attaché tooan sur réseau local via une passerelle de réseau virtuel. La vérification de que cette case autorise le trafic de hello homologuer tooflow de réseau virtuel via réseau virtuel de hello passerelle toothis attaché. Si vous cochez cette case, le réseau virtuel de hello ressources ne peut pas avoir une passerelle configurée. réseau virtuel de Hello ressources doit avoir hello **utiliser la passerelle distante** case à cocher activée lorsque la configuration hello d’homologation de hello autre réseau virtuel toothis de réseau virtuel. Si vous laissez cette case est désactivée (valeur par défaut), le trafic de réseau virtuel de hello ressources toujours flux de réseau virtuel de toothis, mais Impossible de transmettre via un réseau virtuel de réseau virtuel passerelle toothis attaché. Pour en savoir plus, voir [Passerelles de réseau virtuel](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti). 
    
    Vous ne pouvez pas activer cette option si vous homologuez un réseau virtuel (Gestionnaire des ressources) avec un réseau virtuel (classique). Bien que le trafic de hello circulent entre les réseaux virtuels deux hello, hello (classique) le trafic réseau virtuel ne peut pas transitent par un réseau virtuel réseau passerelle toohello attaché (Resource Manager).
    - **Utiliser des passerelles à distance :** vérifier ce trafic tooallow de zone à partir de cette tooflow de réseau virtuel via un réseau virtuel joint toohello passerelle réseau virtuel que vous êtes homologation avec. Par exemple, hello réseau virtuel que vous êtes homologation avec n’a une passerelle VPN attachée qui permet à un réseau de communication tooan local.  Cochez cette case autorise le trafic tooflow de ce réseau virtuel via hello VPN passerelle attaché toohello ressources réseau virtuel. Si vous cochez cette case, réseau virtuel de hello ressources doit avoir un tooit attaché de passerelle de réseau virtuel et qu’il doit avoir hello **permettent de transit de la passerelle** case à cocher activée. Si vous laissez cette case est désactivée (valeur par défaut), le trafic de réseau virtuel de hello ressources peut transférer des toothis virtuel réseau, mais Impossible de transmettre via un réseau virtuel de réseau virtuel passerelle toothis attaché. 
    
    Vous ne pouvez pas activer cette option si vous homologuez un réseau virtuel (Gestionnaire des ressources) avec un réseau virtuel (classique). Bien que le trafic de hello circulent entre les réseaux virtuels deux hello, le trafic de réseau virtuel (Resource Manager) hello Impossible de transmettre via un réseau passerelle toohello attachés réseau virtuel (classique).
7. Cliquez sur hello **OK** bouton tooadd hello sous-réseau toohello réseau virtuel sélectionné.

### <a name="commands"></a>Commandes

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network vnet peering create](/cli/azure/network/vnet/peering#create?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|


### <a name="scenarios"></a>Scénarios

Une homologation de réseau virtuel est créée entre les réseaux virtuels créés via hello même, ou des modèles de déploiement différentes qui existent dans hello identiques ou différents abonnements. Effectuez un didacticiel pas à pas pour l’une des hello les scénarios suivants :
 
|Modèle de déploiement Azure  | Abonnement  |
|---------|---------|
|Les deux modèles Resource Manager |[Identique](virtual-network-create-peering.md)|
| |[Différent](create-peering-different-subscriptions.md)|
|Un modèle Resource Manager, un modèle classique     |[Identique](create-peering-different-deployment-models.md)|
| |[Différent](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>Afficher ou modifier les paramètres d’homologation

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui est affecté hello nécessaire [rôle ou des autorisations](#permissions).
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *réseaux virtuels*. Lorsque **réseaux virtuels** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **réseaux virtuels** panneau qui s’affiche, cliquez sur le réseau virtuel de hello souhaité toocreate une homologation pour.
4. Dans le volet hello qui s’affiche pour le réseau virtuel de hello vous avez sélectionné, cliquez sur **homologations** Bonjour **paramètres** section.
5. Cliquez sur l’homologation de hello vous souhaitez tooview ou modifier les paramètres de.
6. Modifier les paramètres appropriés hello. En savoir plus sur les options de hello pour chaque paramètre de [étape 6](#add-peering) Hello créer une section d’homologation de cet article. 

    >[!NOTE]
    >Il existe plusieurs conditions, contraintes, et considérations toosuccessfully créer un réseau virtuel d’homologation. Avant de créer une homologation, assurez-vous de vous avez familiarisé avec hello [exigences et contraintes](#requirements-and-constraints) et [autorisations requises](#permissions).
    >

7. Cliquez sur **Enregistrer**.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[liste d’homologation du réseau virtuel réseau AZ](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#list) homologations toolist pour un réseau virtuel, [az réseau afficher d’homologation du réseau virtuel](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow des paramètres pour l’homologation spécifique, et [az réseau mise à jour d’homologation du réseau virtuel](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#update) paramètres d’homologation toochange.|
|PowerShell|[Get-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve afficher les paramètres d’homologation et [Set-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) toochange paramètres.|

## <a name="delete-a-peering"></a>Supprimer une homologation
Lorsqu’une homologation est supprimée, le trafic d’un réseau virtuel passe n’est plus toohello de réseau virtuel ressources. Lorsque des réseaux virtuels déployés par le biais du Gestionnaire de ressources sont appariés, chaque réseau virtuel a une homologation toohello autre réseau virtuel. Bien que la suppression hello d’homologation à partir d’un réseau virtuel désactive communication hello entre les réseaux virtuels hello, elle ne supprime pas hello d’homologation de hello autre réseau virtuel. Hello état d’homologation pour hello homologation qui existe dans hello autre réseau virtuel est **Disconnected**. Vous ne pouvez pas recréer hello d’homologation jusqu'à ce que vous recréez hello d’homologation dans le réseau virtuel de hello premier et l’état d’homologation de hello pour virtuelle réseaux modifications trop*connecté*. 

Si vous souhaitez parfois des réseaux virtuels toocommunicate, mais pas toujours, au lieu de la suppression d’une homologation, vous pouvez définir hello **autoriser l’accès de réseau virtuel** aussi un paramètre**désactivé** à la place. toolearn, voir l’étape 6 de hello [créer une homologation](#create-peering) section de cet article. Il se peut que vous trouviez plus facile de désactiver et activer l’accès réseau que de supprimer et recréer des homologations.

1. Connectez-vous à toohello [portal](https://portal.azure.com) avec un compte qui est affecté hello nécessaire [rôle ou des autorisations](#permissions).
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *réseaux virtuels*. Lorsque **réseaux virtuels** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **réseaux virtuels** panneau qui s’affiche, cliquez sur le réseau virtuel hello souhaité toodelete une homologation de.
4. Dans hello panneau qui s’affiche pour le réseau virtuel de hello vous avez sélectionné, cliquez sur **homologations** sous **paramètres**.
5. Dans la liste de hello des homologations apparaissant dans le panneau des homologations hello, hello avec le bouton d’homologation vous souhaitez toodelete, cliquez sur **supprimer**, puis **Oui** hello toodelete d’homologation du réseau virtuel de hello premier.
6. Hello complète précédentes étapes toodelete hello d’homologation de hello autre réseau virtuel dans l’homologation de hello.

**Commandes**

|Outil|Commande|
|---|---|
|Interface de ligne de commande|[az network vnet peering delete](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="requirements-and-constraints"></a>Exigences et contraintes 

- les réseaux virtuels Hello que vous homologue doivent avoir des espaces d’adressage IP sans chevauchement.
- Il n’est pas possible d’ajouter ou de supprimer des espaces d’adressage dans un réseau virtuel après que celui-ci est homologué avec un autre réseau virtuel. espaces d’adressage tooadd ou remove, hello delete homologation, ajoutent ou supprimer des espaces d’adressage hello, puis recréez l’homologation de hello. tooadd espaces d’adresses, et de supprimer les espaces d’adressage de réseaux virtuels, en lecture hello [créer, modifier ou supprimer des réseaux virtuels](virtual-network-manage-network.md#add-address-spaces) l’article. 
- Vous pouvez homologue deux réseaux virtuels déployés via le Gestionnaire de ressources ou d’un réseau virtuel est déployé par le biais du Gestionnaire de ressources avec un réseau virtuel déployé via le modèle de déploiement classique hello. Vous ne pouvez pas homologue deux réseaux virtuels créés via le modèle de déploiement classique hello. Si vous n’êtes pas familiarisé avec les modèles de déploiement d’Azure, lisez hello [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article. Vous pouvez utiliser un [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect deux des réseaux virtuels créés via le modèle de déploiement classique hello.
- Lors de l’homologation deux réseaux virtuels créés par le biais du Gestionnaire de ressources, une homologation doit être configurée pour chaque réseau virtuel dans l’homologation de hello. Lorsque vous créez hello d’homologation toohello second réseau virtuel à partir du réseau virtuel premier de hello, état d’homologation de hello est *a été initiée*.  Lorsque vous créez hello d’homologation de hello réseau virtuel deuxième toohello premier réseau virtuel, son état d’homologation est *connecté*. Si vous affichez le statut d’homologation de hello pour le réseau virtuel de hello premier, vous voyez son état a été remplacée par *a été initiée* trop*connecté*. Hello d’homologation n’est pas correctement établie jusqu'à ce que l’état d’homologation hello pour les deux homologations de réseaux virtuels est *connecté*. 
- Lors de l’homologation un réseau virtuel créé par le biais du Gestionnaire de ressources avec un réseau virtuel créé via le modèle de déploiement classique de hello, vous configurez uniquement une homologation pour le réseau virtuel de hello déployé par le biais du Gestionnaire de ressources. Vous ne pouvez pas configurer d’homologation pour un réseau virtuel (classique), ou entre deux réseaux virtuels déployés via le modèle de déploiement classique hello. Lorsque vous créez hello d’homologation du réseau virtuel hello réseau virtuel (Resource Manager) toohello (classique), état d’homologation de hello est *mise à jour*, puis sous peu change également*connecté*.   
- Une homologation est établie entre deux réseaux virtuels. Les homologations ne sont pas transitives. Imaginons que vous créez des homologations entre :
    - VirtualNetwork1 et VirtualNetwork2
    - VirtualNetwork2 et VirtualNetwork3

  Il n’existe aucune homologation entre VirtualNetwork1 et VirtualNetwork3 via VirtualNetwork2. Si vous voulez toocreate un réseau virtuel d’homologation entre VirtualNetwork1 et VirtualNetwork3, vous avez toocreate une homologation entre VirtualNetwork1 et VirtualNetwork3.
- Vous ne pouvez pas résoudre des noms dans des réseaux virtuels homologués en utilisant une résolution de noms Azure par défaut. noms tooresolve dans d’autres réseaux virtuels, vous devez utiliser un serveur DNS personnalisé. toolearn comment tooset votre propre serveur DNS, lire hello [résolution de noms à l’aide de votre propre serveur DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) l’article.
- Ressources dans les deux réseaux virtuels dans l’homologation de hello peuvent communiquer entre eux par hello même la bande passante et la latence comme s’ils étaient dans hello même réseau virtuel. Toutefois, chaque taille de machine virtuelle a sa propre bande passante réseau maximale. toolearn plus d’informations sur la bande passante réseau maximale pour les tailles de machine virtuelle différente, lire hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articles des tailles de machine virtuelle.
- Vous pouvez d’homologues des réseaux virtuels déployés par le biais du Gestionnaire de ressources qui sont dans hello identiques, ou des abonnements différents.
- Vous pouvez d’homologues des réseaux virtuels déployés via les modèles de déploiement différents qui sont dans hello identiques, ou des abonnements différents (version préliminaire). 
- Hello les abonnements qui se trouvent dans les deux réseaux virtuels doivent être associé toohello même locataire Azure Active Directory. Si vous n’avez pas encore de client Active Directory, vous pouvez rapidement en [créer un](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Vous pouvez utiliser un [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect deux réseaux virtuels qui existent dans différents abonnements associés toodifferent les clients Active Directory.
- Un réseau virtuel peut être tooanother ressources des réseaux virtuels et également être connecté tooanother réseau virtuel avec une passerelle de réseau virtuel Azure. Lorsque les réseaux virtuels sont connectés par le biais d’homologation et une passerelle, le trafic entre les réseaux virtuels hello transite par la configuration d’homologation de hello, plutôt que la passerelle de hello.
- Un coût nominal s’applique pour le trafic entrant et sortant qui utilise une homologation de réseau virtuel. Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/virtual-network).


## <a name="permissions"></a>Autorisations

Hello tous les comptes toocreate une homologation de réseau virtuel doivent avoir hello nécessaires ou autorisations. Par exemple, si vous ont été homologation deux réseaux virtuels nommés myVnetA et myVnetB, doit être affecté à votre compte hello suivant rôle minimale ou les autorisations pour chaque réseau virtuel :
    
|Réseau virtuel|Modèle de déploiement|Rôle|Autorisations|
|---|---|---|---|
|myVnetA|Gestionnaire de ressources|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Classique|[Collaborateur de réseau classique](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/A|
|myVnetB|Gestionnaire de ressources|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Classique|[Collaborateur de réseau classique](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

En savoir plus sur [rôles intégrés](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) et l’affectation des autorisations spécifiques trop[des rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager uniquement).

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toocreate un [topologie de réseau hub and spoke](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
