---
title: "aaaCreate virtuelle Azure réseau d’homologation (modèles de déploiement différentes) même abonnement | Documents Microsoft"
description: "Découvrez comment toocreate une homologation de réseau virtuel entre des réseaux virtuels créés par le biais des modèles de déploiement Azure différents qui existent dans hello même abonnement Azure."
services: virtual-network
documentationcenter: 
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
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Créer une homologation de réseaux virtuels Azure - Modèles de déploiement différents, même abonnement 

Dans ce didacticiel, vous découvrez toocreate un réseau virtuel d’homologation entre réseaux virtuels créés par le biais des modèles de déploiement différent. Les deux réseaux virtuels existe dans hello même abonnement. D’homologation deux réseaux virtuels Active ressources toocommunicate différents réseaux virtuels entre eux avec hello même la bande passante et la latence comme si les ressources hello étaient hello même réseau virtuel. En savoir plus sur l’[homologation de réseaux virtuels](virtual-network-peering-overview.md). 

Hello étapes toocreate une homologation de réseau virtuel sont différents, selon que les réseaux virtuels hello sont dans hello identiques ou différent, les abonnements et qui [modèle de déploiement Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello des réseaux virtuels sont créés via. Découvrez comment toocreate a virtual network homologation dans d’autres scénarios en cliquant sur le scénario hello hello tableau suivant :

|Modèle de déploiement Azure  | Abonnement Azure  |
|--------- |---------|
|[Tous deux Resource Manager](virtual-network-create-peering.md) |Identique|
|[Tous deux Resource Manager](create-peering-different-subscriptions.md) |Différent|
|[Un modèle Resource Manager, un modèle classique](create-peering-different-deployment-models-subscriptions.md) |Différent|

Une homologation de réseau virtuel ne peut pas être créée entre deux réseaux virtuels déployés via le modèle de déploiement classique hello. Une homologation de réseau virtuel ne peut être créée qu’entre deux réseaux virtuels qui existent dans hello même région Azure. Si vous devez tooconnect des réseaux virtuels qui ont été créés via le modèle de déploiement classique de hello, ou qui existe dans différentes régions Azure, vous pouvez utiliser Azure [passerelle VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello des réseaux virtuels. 

Vous pouvez utiliser hello [portail Azure](#portal), hello Azure [une interface de ligne](#cli) (CLI), ou Azure [PowerShell](#powershell) toocreate une homologation de réseau virtuel. Cliquez sur un des hello précédente outil liens toogo directement toohello les étapes de création d’une homologation de réseau virtuel à l’aide de votre outil de choix.

## <a name="cli"></a>Créer une homologation - Portail

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com). compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
2. Cliquez sur **+ Nouveau**, puis sur **Mise en réseau** et **Réseau virtuel**.
3. Bonjour **créer un réseau virtuel** panneau, puis entrez ou sélectionnez les valeurs pour hello suivant les paramètres, **créer**:
    - **Nom** : *myVnet1*
    - **Espace d’adressage** : *10.0.0.0/16*
    - **Nom du sous-réseau** : *par défaut*
    - **Espace d’adressage de sous-réseau** : *10.0.0.0/24*
    - **Abonnement** : sélectionnez votre abonnement
    - **Groupe de ressources** : sélectionnez **Créer** et entrez *myResourceGroup*
    - **Emplacement** : *États-Unis de l’Est*
4. Cliquez sur **+ Nouveau**. Bonjour **hello de recherche Marketplace** , tapez *réseau virtuel*. Cliquez sur **réseau virtuel** lorsqu’il apparaît dans les résultats de recherche hello. 
5. Bonjour **réseau virtuel** panneau, sélectionnez **classique** Bonjour **sélectionner un modèle de déploiement** zone, puis cliquez sur **créer**.
6. Bonjour **créer un réseau virtuel** panneau, puis entrez ou sélectionnez les valeurs pour hello suivant les paramètres, **créer**:
    - **Nom** : *myVnet2*
    - **Espace d’adressage** : *10.1.0.0/16*
    - **Nom du sous-réseau** : *par défaut*
    - **Espace d’adressage de sous-réseau** : *10.1.0.0/24*
    - **Abonnement** : sélectionnez votre abonnement
    - **Groupe de ressources** : sélectionnez **Use existing** (Utiliser existant), puis *myResourceGroup*
    - **Emplacement** : *États-Unis de l’Est*
7. Bonjour **recherche les ressources** zone en haut hello hello du portail de, type *myResourceGroup*. Cliquez sur **myResourceGroup** lorsqu’il apparaît dans les résultats de recherche hello. Un panneau s’affiche pour hello **myresourcegroup** groupe de ressources. groupe de ressources Hello contient hello deux réseaux virtuels créés dans les étapes précédentes.
8. Cliquez sur **myVNet1**.
9. Bonjour **myVnet1** panneau qui s’affiche, cliquez sur **homologations** de liste verticale de hello des options sur hello gauche du Panneau de hello.
10. Bonjour **myVnet1 - homologations** panneau s’affiche, cliquez sur **+ ajouter**
11. Bonjour **ajouter d’homologation** panneau qui s’affiche, entrez, ou sélectionnez hello options suivantes, puis cliquez sur **OK**:
     - **Nom** : *myVnet1ToMyVnet2*
     - **Modèle de déploiement de réseau virtuel** : sélectionnez **Classique**. 
     - **Abonnement** : sélectionnez votre abonnement
     - **Réseau virtuel** : cliquez sur **Choisir un réseau virtuel**, puis sur **myVnet2**.
     - **Autoriser l’accès au réseau virtuel :** vérifiez que l’option **Activé** est sélectionnée.
    Il n’y aucun autre paramètre utilisé dans ce didacticiel. toolearn sur tous les paramètres d’homologation, lire [gérer homologations de réseaux virtuels](virtual-network-manage-peering.md#create-a-peering).
12. Après avoir cliqué sur **OK** à l’étape précédente de hello, hello **ajouter d’homologation** panneau se ferme et vous voyez hello **myVnet1 - homologations** panneau à nouveau. Après quelques secondes, hello d’homologation que vous avez créé s’affiche dans le panneau de hello. **Connecté** est répertorié dans hello **d’homologation de statut** colonne hello **myVnet1ToMyVnet2** d’homologation vous créé.

    Hello d’homologation est désormais établi. Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
14. **Facultatif**: toodelete ressources hello que vous créez dans ce didacticiel, les étapes hello complète Bonjour [supprimer des ressources](#delete-portal) section de cet article.

## <a name="cli"></a>Créer une homologation - interface de ligne de commande Azure

1. [Installer](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) réseau virtuel hello Azure CLI 1.0 toocreate hello (classique).
2. Ouvrez une session de commande et les journaux dans tooAzure à l’aide de hello `azure login` commande.
3. Exécutez hello CLI en mode de gestion de Service en entrant hello `azure config mode asm` commande.
4. Entrez hello toocreate hello réseau virtuelle (classique) de commande suivante :
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Créez un groupe de ressources et un réseau virtuel (Resource Manager). Vous pouvez utiliser hello CLI 1.0 ou 2.0 ([installer](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). Dans ce didacticiel, hello CLI 2.0 est toocreate utilisé hello virtuel réseau (Resource Manager), étant donné que 2.0 doit être d’homologation de hello toocreate utilisé. Exécutez hello suivant bash script CLI à partir de votre ordinateur local hello CLI 2.0.4 ou version ultérieure. Pour les options sur en cours d’exécution bash scripts CLI sur le client Windows, consultez [hello CLI d’Azure en cours d’exécution dans Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Vous pouvez également exécuter le script de hello à l’aide de hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. Cliquez sur hello **essayez-la** bouton dans le script hello qui suit, ce qui permet d’appeler un environnement de Cloud qui vous connecte peut se connecter tooyour compte Azure avec. tooexecute hello script, cliquez sur hello **copie** bouton et coller, le contenu hello dans votre environnement Cloud, puis appuyez sur `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Créez un réseau virtuel d’homologation entre hello deux réseaux virtuels créés par le biais des modèles de déploiement différentes hello. Copiez hello suivant d’éditeur de texte script tooa sur votre PC. Remplacez `<subscription id>` par votre ID d’abonnement. Si vous ne connaissez pas votre Id d’abonnement, entrez hello `az account show` commande. Hello valeur pour **id** Bonjour sortie est votre ID d’abonnement. Collez le script que vous hello modifié dans la session CLI tooyour, puis appuyez sur `Enter`.

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. Après l’exécution du script de hello, passez en revue le hello d’homologation pour le réseau virtuel de hello (Resource Manager). Copie hello suivantes de commandes, collez-le dans votre session CLI et appuyez sur `Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Hello sortie affiche **connecté** Bonjour **PeeringState** colonne. 

    Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
9. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-cli) dans cet article.

## <a name="powershell"></a>Créer une homologation - PowerShell

1. Installer la version la plus récente de hello PowerShell hello [Azure](https://www.powershellgallery.com/packages/Azure) et [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules. Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Démarrez une session PowerShell.
3. Dans PowerShell, connectez-vous tooAzure en entrant hello `Add-AzureAccount` commande.
4. toocreate un réseau virtuel (classique) avec PowerShell, vous devez créer un nouveau, ou modifier un existant, fichier de configuration réseau. Découvrez comment trop[exporter, mettre à jour et importer les fichiers de configuration réseau](virtual-networks-using-network-configuration-file.md). Hello fichier doit suivants hello **VirtualNetworkSite** élément pour le réseau virtuel de hello utilisé dans ce didacticiel :

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importation d’un fichier de configuration de réseau modifié peut entraîner des modifications tooexisting les réseaux virtuels (classiques) dans votre abonnement. Assurez-vous que vous ajoutez uniquement réseau virtuel de hello précédente et que vous ne modifiez ou supprimez des réseaux virtuels existants de votre abonnement. 
5. Ouvrez une session dans le réseau virtuel tooAzure toocreate hello (Resource Manager) en entrant hello `login-azurermaccount` commande. compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
6. Créez un groupe de ressources et un réseau virtuel (Resource Manager). Copiez le script de hello, collez-le dans PowerShell, puis appuyez sur `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Créez un réseau virtuel d’homologation entre hello deux réseaux virtuels créés par le biais des modèles de déploiement différentes hello. Copiez hello suivant d’éditeur de texte script tooa sur votre PC. Remplacez `<subscription id>` par votre ID d’abonnement. Si vous ne connaissez pas votre Id d’abonnement, entrez hello `Get-AzureRmSubscription` commande tooview il. Hello valeur pour **Id** Bonjour retourné de sortie est votre ID d’abonnement. script de hello tooexecute, hello de copie modifiée script à partir de votre éditeur de texte, puis avec le bouton droit dans votre session PowerShell, puis appuyez sur `Enter`.

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. Après l’exécution du script de hello, passez en revue le hello d’homologation pour le réseau virtuel de hello (Resource Manager). Copie hello suivantes de commandes, collez-le dans votre session PowerShell et appuyez sur `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hello sortie affiche **connecté** Bonjour **PeeringState** colonne.

    Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
10. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-powershell) dans cet article.
 
## <a name="permissions"></a>Autorisations

Hello tous les comptes toocreate une homologation de réseau virtuel doivent avoir hello nécessaires ou autorisations. Par exemple, si vous ont été homologation deux réseaux virtuels nommés myVnet1 et myVnet2, doit être affecté à votre compte hello suivant rôle minimale ou les autorisations pour chaque réseau virtuel :
    
|Réseau virtuel|Modèle de déploiement|Rôle|Autorisations|
|---|---|---|---|
|myVnet1|Gestionnaire de ressources|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Classique|[Collaborateur de réseau classique](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/A|
|myVnet2|Gestionnaire de ressources|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Classique|[Collaborateur de réseau classique](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

En savoir plus sur [rôles intégrés](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) et l’affectation des autorisations spécifiques trop[des rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager uniquement).

## <a name="delete"></a>Supprimer des ressources
Lorsque vous avez terminé ce didacticiel, vous pourriez les ressources de hello toodelete que vous avez créé dans le didacticiel de hello, donc vous ne subissez des frais d’utilisation. Suppression d’un groupe de ressources supprime également toutes les ressources qui se trouvent dans le groupe de ressources hello.

### <a name="delete-portal"></a>Portail Azure

1. Dans la zone de recherche du portail hello, entrez **myResourceGroup**. Dans les résultats de recherche de hello, cliquez sur **myResourceGroup**.
2. Sur hello **myResourceGroup** panneau, cliquez sur hello **supprimer** icône.
3. suppression de hello tooconfirm, Bonjour **hello TYPE nom groupe de ressources** , entrez **myResourceGroup**, puis cliquez sur **supprimer**.

### <a name="delete-cli"></a>Interface CLI Azure

1. Utilisez réseau virtuel hello Azure CLI 2.0 toodelete hello (Resource Manager) avec hello de commande suivante :

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Utilisez réseau virtuel hello Azure CLI 1.0 toodelete hello (classiques) avec hello suivant de commandes :

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Entrez hello toodelete hello réseau virtuel (Resource Manager) de commande suivante :

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete hello réseau virtuelle (classique) avec PowerShell, vous devez modifier un fichier de configuration réseau. Découvrez comment trop[exporter, mettre à jour et importer les fichiers de configuration réseau](virtual-networks-using-network-configuration-file.md). Supprimer hello suivant élément VirtualNetworkSite pour le réseau virtuel de hello utilisé dans ce didacticiel :

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importation d’un fichier de configuration de réseau modifié peut entraîner des modifications tooexisting les réseaux virtuels (classiques) dans votre abonnement. Vérifiez que vous supprimez uniquement réseau virtuel de hello précédente et que vous ne modifiez ou supprimez des autres réseaux virtuels existants de votre abonnement. 

## <a name="next-steps"></a>Étapes suivantes

- Familiarisez-vous bien avec les [comportements et contraintes importants de l’homologation de réseaux virtuels](virtual-network-manage-peering.md#requirements-and-constraints) avant d’en créer une pour une utilisation en production.
- Apprenez-en davantage sur tous les [paramètres d’homologation de réseaux virtuels](virtual-network-manage-peering.md#create-a-peering).
- Découvrez comment trop[créer un hub et spoke topologie de réseau](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) avec le réseau virtuel d’homologation.
