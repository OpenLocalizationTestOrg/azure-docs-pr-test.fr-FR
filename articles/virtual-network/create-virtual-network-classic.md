---
title: "aaaCreate un réseau virtuel Azure (classique) avec plusieurs sous-réseaux | Documents Microsoft"
description: "Découvrez comment toocreate un réseau virtuel (classique) avec plusieurs sous-réseaux dans Azure."
services: virtual-network
documentationcenter: 
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
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>Créer un réseau virtuel (Classic) comprenant plusieurs sous-réseaux

> [!IMPORTANT]
> Azure dispose de deux [modèles de déploiement différents](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) pour créer et utiliser des ressources : le déploiement Resource Manager et le déploiement Classic. Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande de créer la plupart des nouveaux réseaux virtuels via hello [le Gestionnaire de ressources](virtual-networks-create-vnet-arm-pportal.md) modèle de déploiement.

Dans ce didacticiel, découvrez comment toocreate un base réseau virtuel Azure (classique) qui a séparer les sous-réseaux privés et publics. Vous pouvez créer des ressources Azure, telles que des machines virtuelles et des services cloud, dans un sous-réseau. Ressources créées dans des réseaux virtuels (classiques) peuvent communiquer entre eux et avec les ressources d’un autre réseau virtuel connecté tooa de réseaux.

Apprenez-en davantage sur tous les paramètres de [réseau virtuel](virtual-network-manage-network.md) et de [sous-réseau](virtual-network-manage-subnet.md).

> [!WARNING]
> Azure supprime immédiatement les réseaux virtuels (Classic) quand un [abonnement est désactivé](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit). Les réseaux virtuels (classiques) sont supprimées, quelle que soit l’existent de ressources dans le réseau virtuel de hello. Si vous ré-activez ultérieurement abonnement de hello, les ressources qui existaient dans le réseau virtuel de hello doivent être recréés.

Vous pouvez créer un réseau virtuel (classiques) à l’aide de hello [portail Azure](#portal), hello [Azure interface de ligne de commande (CLI) 1.0](#azure-cli), ou [PowerShell](#powershell).

## <a name="portal"></a>Portail

1. Dans un navigateur Internet, accédez à toohello [portail Azure](https://portal.azure.com). Connectez-vous à votre [compte Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si vous n’en avez pas, vous pouvez demander un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Cliquez sur **+ nouveau** dans le portail de hello.
3. Entrez *réseau virtuel* Bonjour **hello de recherche Marketplace** zone en haut de hello de hello **nouveau** panneau s’affiche.  Cliquez sur **réseau virtuel** lorsqu’il apparaît dans les résultats de recherche hello.
4. Sélectionnez **classique** Bonjour **sélectionner un modèle de déploiement** zone hello **réseau virtuel** panneau qui s’affiche, puis cliquez sur **créer**. 
5. Entrez hello suivant de valeurs de hello **créer un réseau virtuel (classiques)** panneau, puis cliquez sur **créer**:

    |Paramètre|Valeur|
    |---|---|
    |Nom|myVnet|
    |Espace d’adressage|10.0.0.0/16|
    |Nom du sous-réseau|Public|
    |Plage d’adresses de sous-réseau|10.0.0.0/24|
    |Groupe de ressources|Laissez l’option **Créer** activée, puis entrez **myResourceGroup**.|
    |Abonnement et emplacement|Sélectionnez votre abonnement et son emplacement.

    Si vous êtes tooAzure nouvelle, en savoir plus sur [groupes de ressources](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnements](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), et [emplacements](https://azure.microsoft.com/regions) (également appelée tooas *régions*).
4. Dans le portail hello, vous pouvez créer un seul sous-réseau lorsque vous créez un réseau virtuel. Dans ce didacticiel, vous créez un deuxième sous-réseau après avoir créé le réseau virtuel de hello. Vous pouvez créer ultérieurement les ressources accessibles sur Internet dans hello **Public** sous-réseau. Vous pouvez également créer des ressources qui ne sont pas accessibles à partir de hello Internet Bonjour **privé** sous-réseau. toocreate hello deuxième sous-réseau, entrez **myVnet** Bonjour **recherche les ressources** zone en hello haut hello. Cliquez sur **myVnet** lorsqu’il apparaît dans les résultats de recherche hello.
5. Cliquez sur **sous-réseaux** (Bonjour **paramètres** section) sur hello **créer un réseau virtuel (classiques)** panneau s’affiche.
6. Cliquez sur **+ ajouter** sur hello **myVnet - sous-réseaux** panneau s’affiche.
7. Entrez **privé** pour **nom** sur hello **ajouter un sous-réseau** panneau. Pour **Plage d’adresses**, entrez **10.0.1.0/24**.  Cliquez sur **OK**.
8. Sur hello **myVnet - sous-réseaux** panneau, vous pouvez voir hello **Public** et **privé** sous-réseaux que vous avez créé.
9. **Facultatif**: lorsque vous avez terminé ce didacticiel, vous pourriez ressources hello toodelete que vous avez créé, afin que vous ne subissez des frais d’utilisation :
    - Cliquez sur **vue d’ensemble** sur hello **myVnet** panneau.
    - Cliquez sur hello **supprimer** icône sur hello **myVnet** panneau.
    - suppression de hello tooconfirm, cliquez sur **Oui** Bonjour **réseau virtuel de suppression** boîte.

## <a name="azure-cli"></a>Interface de ligne de commande Azure

1. Vous pouvez soit [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), ou utilisez hello CLI dans hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. aide tooget pour les commandes CLI, tapez `azure <command> --help`. 
2. Dans une session CLI, connectez-vous tooAzure avec la commande hello qui suit. Si vous cliquez sur **essayez-la** dans la zone de hello ci-dessous, un environnement de Cloud s’ouvre. Vous pouvez vous connecter tooyour abonnement Azure, sans entrer de hello de commande suivante :

    ```azurecli-interactive
    azure login
    ```

3. hello tooensure CLI est en mode de gestion de Service, entrez hello de commande suivante :

    ```azurecli-interactive
    azure config mode asm
    ```

4. Créez un réseau virtuel avec un sous-réseau privé :

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Créer un sous-réseau public dans le réseau virtuel de hello :

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Examiner le réseau virtuel hello et sous-réseaux :

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **Facultatif**: vous pourriez ressources hello toodelete que vous avez créé lorsque vous avez terminé ce didacticiel, afin que vous ne subissez des frais d’utilisation :

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Si vous ne pouvez pas spécifier un toocreate de groupe de ressources un réseau virtuel (classique) à l’aide de hello CLI, Azure crée le réseau virtuel de hello dans un groupe de ressources nommé *réseau par défaut*.

## <a name="powershell"></a>PowerShell

1. Installer la version la plus récente de hello PowerShell hello [Azure](https://www.powershellgallery.com/packages/Azure) module. Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Démarrez une session PowerShell.
3. Dans PowerShell, connectez-vous tooAzure en entrant hello `Add-AzureAccount` commande.
4. Modifier hello suivants chemin d’accès et nom de fichier, comme il convient, puis exporter votre fichier de configuration de réseau existant :

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate un réseau virtuel avec les sous-réseaux privés et publics, utilisez n’importe quel hello de tooadd de l’éditeur de texte **VirtualNetworkSite** élément qui suit le fichier de configuration réseau toohello.

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    Hello révision complète [schéma de fichier de configuration réseau](https://msdn.microsoft.com/library/azure/jj157100.aspx).

6. Importez le fichier de configuration de réseau hello :

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > Importation d’un fichier de configuration de réseau modifié peut entraîner des modifications tooexisting les réseaux virtuels (classiques) dans votre abonnement. Assurez-vous que vous ajoutez uniquement réseau virtuel de hello précédente et que vous ne modifiez ou supprimez des réseaux virtuels existants de votre abonnement. 

7. Examiner le réseau virtuel hello et sous-réseaux :

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **Facultatif**: vous pourriez ressources hello toodelete que vous avez créé lorsque vous avez terminé ce didacticiel, afin que vous ne subissez des frais d’utilisation. toodelete hello réseau virtuel, complète étapes 4 à 6, cette hello suppression temps **VirtualNetworkSite** élément ajouté à l’étape 5.
 
> [!NOTE]
> Si vous ne pouvez pas spécifier un toocreate de groupe de ressources un réseau virtuel (classique) dans l’aide de PowerShell, Azure crée le réseau virtuel de hello dans un groupe de ressources nommé *réseau par défaut*.

---

## <a name="next-steps"></a>Étapes suivantes

- toolearn sur tous les paramètres réseau virtuel et sous-réseau, consultez [gérer les réseaux virtuels](virtual-network-manage-network.md) et [gérer les sous-réseaux du réseau virtuel](virtual-network-manage-subnet.md). Vous disposez des options différentes pour l’utilisation de réseaux virtuels et sous-réseaux dans les exigences de la toomeet d’environnement de production différent.
- toofilter entrant et sortant du trafic de sous-réseau, créer et appliquer [groupes de sécurité réseau](virtual-networks-nsg.md) toosubnets.
- Créer un [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou un [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) machine virtuelle, puis connectez-la tooan de réseau virtuel existant.
- tooconnect deux des réseaux virtuels dans hello même emplacement, créez un [réseau virtuel d’homologation](create-peering-different-deployment-models.md) entre les réseaux virtuels hello. Vous pouvez homologue d’un réseau virtuel de réseau virtuel (Resource Manager) tooa (classique), mais vous ne pouvez pas créer une homologation entre deux réseaux virtuels (classiques).
- Connecter le réseau local de hello réseau virtuel tooan à l’aide un [passerelle VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.
