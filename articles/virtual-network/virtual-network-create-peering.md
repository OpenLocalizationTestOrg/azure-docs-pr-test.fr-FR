---
title: "aaaCreate un réseau virtuel Azure d’homologation - Gestionnaire de ressources - même abonnement | Documents Microsoft"
description: "Découvrez comment toocreate une homologation de réseau virtuel entre des réseaux virtuels créés via le Gestionnaire de ressources qui existent dans hello même abonnement Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>Créer une homologation de réseaux virtuels - Resource Manager - Même abonnement

Dans ce didacticiel, vous découvrez toocreate un réseau virtuel d’homologation entre réseaux virtuels créés par le biais du Gestionnaire de ressources. Les deux réseaux virtuels existe dans hello même abonnement. D’homologation deux réseaux virtuels Active ressources toocommunicate différents réseaux virtuels entre eux avec hello même la bande passante et la latence comme si les ressources hello étaient hello même réseau virtuel. En savoir plus sur l’[homologation de réseaux virtuels](virtual-network-peering-overview.md). 

Hello étapes toocreate une homologation de réseau virtuel sont différents, selon que les réseaux virtuels hello sont dans hello identiques ou différent, les abonnements et qui [modèle de déploiement Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello des réseaux virtuels sont créés via. Découvrez comment toocreate a virtual network homologation dans d’autres scénarios en cliquant sur le scénario hello hello tableau suivant :

|Modèle de déploiement Azure  | Abonnement Azure  |
|--------- |---------|
|[Deux modèles Resource Manager](create-peering-different-subscriptions.md) |Différent|
|[Un modèle Resource Manager, un modèle classique](create-peering-different-deployment-models.md) |Identique|
|[Un modèle Resource Manager, un modèle classique](create-peering-different-deployment-models-subscriptions.md) |Différent|

Une homologation de réseau virtuel ne peut pas être créée entre deux réseaux virtuels déployés via le modèle de déploiement classique hello. Une homologation de réseau virtuel ne peut être créée qu’entre deux réseaux virtuels qui existent dans hello même région Azure. Si vous devez tooconnect des réseaux virtuels qui ont été créés via le modèle de déploiement classique de hello, ou qui existe dans différentes régions Azure, vous pouvez utiliser Azure [passerelle VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello des réseaux virtuels. 

Vous pouvez utiliser hello [portail Azure](#portal), hello Azure [une interface de ligne](#cli) (CLI), Azure [PowerShell](#powershell), ou une [le modèle Azure Resource Manager](#template) toocreate une homologation de réseau virtuel. Cliquez sur un des hello précédente outil liens toogo directement toohello les étapes de création d’une homologation de réseau virtuel à l’aide de votre outil de choix.

## <a name="portal"></a>Créer une homologation - portail Azure

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
4. Effectuez les étapes 2 et 3 à nouveau en spécifiant hello suivant à l’étape 3 :
    - **Nom** : *myVnet2*
    - **Espace d’adressage** : *10.1.0.0/16*
    - **Nom du sous-réseau** : *par défaut*
    - **Espace d’adressage de sous-réseau** : *10.1.0.0/24*
    - **Abonnement** : sélectionnez votre abonnement
    - **Groupe de ressources** : sélectionnez **Use existing** (Utiliser existant), puis *myResourceGroup*
    - **Emplacement** : *États-Unis de l’Est*
5. Bonjour **recherche les ressources** zone en haut hello hello du portail de, type *myResourceGroup*. Cliquez sur **myResourceGroup** lorsqu’il apparaît dans les résultats de recherche hello. Un panneau s’affiche pour hello **myresourcegroup** groupe de ressources. groupe de ressources Hello contient hello deux réseaux virtuels créés dans les étapes précédentes.
6. Cliquez sur **myVNet1**.
7. Bonjour **myVnet1** panneau qui s’affiche, cliquez sur **homologations** de liste verticale de hello des options sur hello gauche du Panneau de hello.
8. Bonjour **myVnet1 - homologations** panneau s’affiche, cliquez sur **+ ajouter**
9. Bonjour **ajouter d’homologation** panneau qui s’affiche, entrez, ou sélectionnez hello options suivantes, puis cliquez sur **OK**:
     - **Nom** : *myVnet1ToMyVnet2*
     - **Modèle de déploiement de réseau virtuel** : sélectionnez **Resource Manager**. 
     - **Abonnement** : sélectionnez votre abonnement
     - **Réseau virtuel** : cliquez sur **Choisir un réseau virtuel**, puis sur **myVnet2**.
     - **Autoriser l’accès au réseau virtuel :** vérifiez que l’option **Activé** est sélectionnée.
    Il n’y aucun autre paramètre utilisé dans ce didacticiel. toolearn sur tous les paramètres d’homologation, lire [gérer homologations de réseaux virtuels](virtual-network-manage-peering.md#create-a-peering).
10. Après avoir cliqué sur **OK** à l’étape précédente de hello, hello **ajouter d’homologation** panneau se ferme et vous voyez hello **myVnet1 - homologations** panneau à nouveau. Après quelques secondes, hello d’homologation que vous avez créé s’affiche dans le panneau de hello. **Initiée par** est répertorié dans hello **d’homologation de statut** colonne hello **myVnet1ToMyVnet2** d’homologation vous créé. Vous avez homologuer tooVnet2 de Vnet1, mais vous devez maintenant homologue myVnet2 toomyVnet1. Hello d’homologation doit être créé dans les deux sens tooenable ressources toocommunicate de réseaux virtuels hello entre eux.
11. Répétez les étapes 5 à 10 pour myVnet2.  Homologation de nom hello *myVnet2ToMyVnet1*.
12. Quelques secondes après avoir cliqué sur **OK** toocreate hello d’homologation pour MyVnet2, hello **myVnet2ToMyVnet1** d’homologation vous venez de créer est répertorié avec **connecté** Bonjour  **ÉTAT de l’homologation** colonne.
13. Répétez les étapes 5 à 7 pour MyVnet1. Hello **d’homologation de statut** pour hello **myVnet1ToVNet2** d’homologation est désormais également **connecté**. Hello d’homologation est établie avec succès une fois que vous **connecté** Bonjour **d’homologation de statut** colonne pour les deux réseaux virtuels dans l’homologation de hello.
14. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
15. **Facultatif**: toodelete ressources hello que vous créez dans ce didacticiel, les étapes hello complète Bonjour [supprimer des ressources](#delete-portal) section de cet article.

Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="cli"></a>Créer une homologation - interface de ligne de commande Azure

Hello le script suivant :

- Requiert hello CLI d’Azure version 2.0.4 ou version ultérieure. version de hello toofind, exécutez hello `az --version` commande. Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Fonctionne dans un interpréteur de commandes Bash. Pour les options sur l’exécution de scripts CLI d’Azure sur le client Windows, consultez [hello CLI d’Azure en cours d’exécution dans Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Au lieu d’installer hello CLI et ses dépendances, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. Cliquez sur hello **essayez-la** bouton dans le script hello qui suit, ce qui permet d’appeler un environnement de Cloud qui vous connecte peut se connecter tooyour compte Azure avec. tooexecute hello script, cliquez sur hello **copie** bouton et coller le contenu hello dans votre environnement Cloud.

1. Créez un groupe de ressources et deux réseaux virtuels.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. Créez un réseau virtuel d’homologation entre les réseaux virtuels deux hello.
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Après l’exécution du script de hello, passez en revue les homologations hello pour chaque réseau virtuel. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Exécuter la commande précédente hello à nouveau, en remplaçant *myVnet1* avec *myVnet2*. sortie Hello des deux commandes montre **connecté** Bonjour **PeeringState** colonne.

     Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

4. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
5. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-cli) dans cet article.


## <a name="powershell"></a>Créer une homologation - PowerShell

1. Installer la version la plus récente de hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. toostart une session de PowerShell, consultez trop**Démarrer**, entrez **powershell**, puis cliquez sur **PowerShell**.
3. Dans PowerShell, connectez-vous tooAzure en entrant hello `login-azurermaccount` commande. compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
4. Créez un groupe de ressources et deux réseaux virtuels. script de hello tooexecute, copie hello suivantes de script, collez-le dans PowerShell et appuyez sur `Enter` après la dernière ligne de hello s’affiche sur l’écran hello :

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. Créez un réseau virtuel d’homologation entre les réseaux virtuels deux hello. Copie hello suivantes de script, collez dans tooPowerShell et appuyez sur `Enter` après la dernière ligne de hello s’affiche sur l’écran hello :
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. tooreview des sous-réseaux hello pour le réseau virtuel de hello, copie hello suivantes de commande, collez dans tooPowerShell et appuyez sur `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Exécuter la commande précédente hello à nouveau, en remplaçant *myVnet1* avec *myVnet2*. sortie Hello des deux commandes montre **connecté** Bonjour **PeeringState** colonne.
7. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
8. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-powershell) dans cet article.

Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="template"></a>Créer une homologation - modèle Resource Manager

1. Faites référence au modèle Azure Resource Manager [Créer une homologation de réseaux virtuels](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering). Les instructions sont fournies avec le modèle hello pour le déploiement de modèle de hello à l’aide de hello portail Azure, PowerShell ou hello CLI d’Azure. Journal dans l’outil toowhichever vous choisissez modèle hello toodeploy à l’aide d’un compte qui dispose hello toocreate des autorisations nécessaires à un réseau virtuel d’homologation. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
2. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
3. **Facultatif**: toodelete ressources hello que vous créez dans ce didacticiel, les étapes hello complète Bonjour [supprimer des ressources](#delete) section de cet article, à l’aide hello portail Azure, PowerShell ou hello CLI d’Azure.

## <a name="permissions"></a>Autorisations

Hello tous les comptes toocreate une homologation de réseau virtuel doivent avoir hello nécessaires ou autorisations. Par exemple, si vous ont été homologation deux réseaux virtuels nommés VNet1 et VNet2, doit être affecté à votre compte hello suivant rôle minimale ou les autorisations pour chaque réseau virtuel :
    
|Réseau virtuel|Rôle|Autorisations|
|---|---|---|
|VNet1|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

En savoir plus sur [rôles intégrés](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) et l’affectation des autorisations spécifiques trop[des rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager uniquement).

## <a name="delete"></a>Supprimer des ressources
Lorsque vous avez terminé ce didacticiel, vous pourriez les ressources de hello toodelete que vous avez créé dans le didacticiel de hello, donc vous ne subissez des frais d’utilisation. Suppression d’un groupe de ressources supprime également toutes les ressources qui se trouvent dans le groupe de ressources hello.

### <a name="delete-portal"></a>Portail Azure

1. Dans la zone de recherche du portail hello, entrez **myResourceGroup**. Dans les résultats de recherche de hello, cliquez sur **myResourceGroup**.
2. Sur hello **myResourceGroup** panneau, cliquez sur hello **supprimer** icône.
3. suppression de hello tooconfirm, Bonjour **hello TYPE nom groupe de ressources** , entrez **myResourceGroup**, puis cliquez sur **supprimer**.

### <a name="delete-cli"></a>Interface CLI Azure

Entrez hello de commande suivante :

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Entrez hello de commande suivante :

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>Étapes suivantes

- Familiarisez-vous bien avec les [comportements et contraintes importants de l’homologation de réseaux virtuels](virtual-network-manage-peering.md#requirements-and-constraints) avant d’en créer une pour une utilisation en production.
- Apprenez-en davantage sur tous les [paramètres d’homologation de réseaux virtuels](virtual-network-manage-peering.md#create-a-peering).
- Découvrez comment trop[créer un hub et spoke topologie de réseau](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) avec le réseau virtuel d’homologation.
