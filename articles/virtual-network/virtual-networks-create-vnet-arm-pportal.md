---
title: "aaaCreate un réseau virtuel Azure avec plusieurs sous-réseaux | Documents Microsoft"
description: "Découvrez comment toocreate un réseau virtuel avec plusieurs sous-réseaux dans Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>Créer un réseau virtuel comprenant plusieurs sous-réseaux

Dans ce didacticiel, découvrez comment toocreate un réseau virtuel Azure base ayant séparer les sous-réseaux privés et publics. Vous pouvez créer des ressources Azure, telles que des machines virtuelles, des environnements App Service Environment, des groupes de machines virtuelles identiques, Azure HDInsight et des services cloud dans un sous-réseau. Ressources dans les réseaux virtuels peuvent communiquer entre eux et avec les ressources d’un autre réseau virtuel connecté tooa de réseaux.

Hello sections suivantes contiennent des étapes que vous pouvez prendre toocreate un réseau virtuel à l’aide de hello [portail Azure](#portal), hello interface de ligne de commande Azure ([CLI d’Azure](#azure-cli)), [Azure PowerShell ](#powershell)et un [modèle Azure Resource Manager](#resource-manager-template). résultat de Hello est hello même, indépendamment de l’outil que vous utilisez réseau virtuel de toocreate hello. Cliquez sur un outil lien toogo toothat du didacticiel de hello. Apprenez-en davantage sur tous les paramètres de [réseau virtuel](virtual-network-manage-network.md) et de [sous-réseau](virtual-network-manage-subnet.md).

Cet article fournit des étapes toocreate un réseau virtuel via le modèle de déploiement Resource Manager hello, qui est le modèle de déploiement hello que nous recommandons d’utiliser lors de la création de nouveaux réseaux virtuels. Si vous avez besoin de toocreate un réseau virtuel (classique), consultez [créer un réseau virtuel (classiques)](create-virtual-network-classic.md). Si vous ne connaissez pas les modèles de déploiement Azure, consultez [Comprendre les modèles de déploiement Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="portal"></a>Portail Azure

1. Dans un navigateur Internet, accédez à toohello [portail Azure](https://portal.azure.com). Connectez-vous à votre [compte Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si vous n’en avez pas, vous pouvez demander un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Dans le portail de hello, cliquez sur **+ nouveau** > **réseau** > **réseau virtuel**.
3. Sur hello **créer un réseau virtuel** panneau, entrez hello valeurs suivantes, puis cliquez sur **créer**:

    |Paramètre|Valeur|
    |---|---|
    |Nom|myVnet|
    |Espace d’adressage|10.0.0.0/16|
    |Nom du sous-réseau|Public|
    |Plage d’adresses de sous-réseau|10.0.0.0/24|
    |Groupe de ressources|Laissez l’option **Créer** activée, puis entrez **myResourceGroup**.|
    |Abonnement et emplacement|Sélectionnez votre abonnement et son emplacement.

    Si vous êtes tooAzure nouvelle, en savoir plus sur [groupes de ressources](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnements](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), et [emplacements](https://azure.microsoft.com/regions) (également appelée tooas *régions*).
4. Dans le portail hello, vous pouvez créer un seul sous-réseau lorsque vous créez un réseau virtuel. Dans ce didacticiel, vous créez un deuxième sous-réseau après avoir créé le réseau virtuel de hello. Vous pouvez créer ultérieurement les ressources accessibles sur Internet dans hello **Public** sous-réseau. Vous pouvez également créer des ressources qui ne sont pas accessibles à partir de hello Internet Bonjour **privé** sous-réseau. toocreate hello deuxième sous-réseau, Bonjour **recherche les ressources** en hello haut hello, entrez **myVnet**. Dans les résultats de recherche de hello, cliquez sur **myVnet**. Si vous avez plusieurs réseaux virtuels avec hello du même nom dans votre abonnement, vérifiez les groupes de ressources hello qui sont répertoriés sous chaque réseau virtuel. Vérifiez que vous cliquez sur hello **myVnet** recherche des résultats qui possède le groupe de ressources hello **myResourceGroup**.
5. Sur hello **myVnet** panneau, sous **paramètres**, cliquez sur **sous-réseaux**.
6. Sur hello **myVnet - sous-réseaux** panneau, cliquez sur **+ sous-réseau**.
7. Sur hello **ajouter un sous-réseau** panneau, pour **nom**, entrez **privé**. Pour **Plage d’adresses**, entrez **10.0.1.0/24**.  Cliquez sur **OK**.
8. Sur hello **myVnet - sous-réseaux** panneau, révision hello sous-réseaux. Vous pouvez voir hello **Public** et **privé** sous-réseaux que vous avez créé.
9. **Facultatif :** toodelete ressources hello que vous créez dans ce didacticiel, les étapes hello complète [supprimer des ressources](#delete-portal) dans cet article.

## <a name="azure-cli"></a>Interface de ligne de commande Azure

Les commandes CLI Azure sont hello de même, si vous exécutez des commandes hello à partir de Windows, Linux ou macOS. Toutefois, il existe des différences de script entre les interpréteurs de commandes du système d’exploitation. script de Hello Bonjour comme suit s’exécute dans un interpréteur de commandes Bash. 

1. [Installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente hello Hello CLI d’Azure installé. aide tooget pour les commandes CLI, tapez `az <command> --help`. Au lieu de hello lors de l’installation CLI et les logiciels requis, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Hello Cloud Shell a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. toouse hello Cloud interpréteur de commandes, cliquez sur hello Cloud Shell (**> _**) bouton haut hello hello [portal](https://portal.azure.com) ou cliquez simplement sur hello *essayez-la* bouton étapes hello qui suivent. 
2. Si vous exécutez hello CLI localement, connectez-vous à tooAzure avec hello `az login` commande. Si vous utilisez hello Shell de cloud computing, vous êtes déjà connecté.
3. Hello de révision suivant script et ses commentaires. Dans votre navigateur, copiez le script de hello et collez-le dans votre session CLI :

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Lorsque le script de hello est terminée en cours d’exécution, passez en revue les sous-réseaux hello pour le réseau virtuel de hello. Copiez les hello commande suivante, puis coller ensuite dans votre session CLI :

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-cli) dans cet article.

## <a name="powershell"></a>PowerShell

1. Installer la version la plus récente de hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Dans une session PowerShell, connectez-vous tooAzure avec votre [compte Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) à l’aide de hello `login-azurermaccount` commande.

3. Hello de révision suivant script et ses commentaires. Dans votre navigateur, copiez le script de hello et collez-le dans votre session PowerShell :

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. sous-réseaux de hello tooreview pour le réseau virtuel de hello, copiez hello commande suivante et puis la coller dans votre session PowerShell :

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-powershell) dans cet article.

## <a name="resource-manager-template"></a>Modèle Resource Manager

Vous pouvez déployer un groupe de machines virtuelles à l’aide d’un modèle Azure Resource Manager. toolearn savoir plus sur les modèles, consultez [qu’est le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment). modèle de hello tooaccess et toolearn sur ses paramètres, consultez hello [créer un réseau virtuel avec deux sous-réseaux](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) modèle. Vous pouvez déployer le modèle de hello à l’aide de hello [portal](#template-portal), [CLI d’Azure](#template-cli), ou [PowerShell](#template-powershell).

**Facultatif :** toodelete ressources hello que vous créez dans ce didacticiel, les étapes hello complète dans les sous-sections de [supprimer des ressources](#delete) dans cet article.

### <a name="template-portal"></a>Portail Azure

1. Dans votre navigateur, ouvrez hello [page modèle](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).
2. Cliquez sur hello **déployer tooAzure** bouton. Si vous n’êtes pas déjà connecté dans tooAzure, ouvrez une session sur l’écran de connexion au portail Azure hello qui s’affiche.
3. Connectez-vous à toohello portal à l’aide de votre [compte Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si vous n’en avez pas, vous pouvez demander un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Entrez hello valeurs pour les paramètres de hello suivantes :

    |Paramètre|Valeur|
    |---|---|
    |Abonnement|Sélectionnez votre abonnement|
    |Groupe de ressources|myResourceGroup|
    |Emplacement|Sélectionner un emplacement|
    |Nom du réseau virtuel|myVnet|
    |Préfixe d’adresse de réseau virtuel|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|Public|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|Privé|

5. Acceptez les conditions générales toohello, puis cliquez sur **achat** réseau virtuel de toodeploy hello.

### <a name="template-cli"></a>Interface CLI Azure

1. [Installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Vérifiez que vous avez la version la plus récente hello Hello CLI d’Azure installé. aide tooget pour les commandes CLI, tapez `az <command> --help`. Au lieu de hello lors de l’installation CLI et les logiciels requis, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Hello Cloud Shell a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. toouse hello Cloud interpréteur de commandes, cliquez sur hello Cloud Shell **> _** bouton haut hello hello [portal](https://portal.azure.com), ou cliquez simplement sur hello **essayez-la** bouton étapes hello qui suivent. 
2. Si vous exécutez hello CLI localement, connectez-vous à tooAzure avec hello `az login` commande. Si vous utilisez hello Shell de cloud computing, vous êtes déjà connecté.
3. commande et collez-la dans votre session CLI toocreate un groupe de ressources pour le réseau virtuel de hello, copie hello suivants :

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. Vous pouvez déployer le modèle de hello en utilisant l’une de hello options de paramètres suivantes :
    - **Valeurs de paramètres par défaut**. Entrez hello de commande suivante :
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **Valeurs de paramètres personnalisées**. Télécharger et modifier le modèle de hello avant de déployer le modèle de hello. Vous pouvez également déployer le modèle de hello à l’aide des paramètres à la ligne de commande hello ou déployer le modèle de hello avec un fichier de paramètres distincts. fichiers modèle et les paramètres de hello toodownload, cliquez sur hello **Parcourir sur GitHub** bouton sur hello [créer un réseau virtuel avec deux sous-réseaux](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) page du modèle. Dans GitHub, cliquez sur hello **azuredeploy.parameters.json** ou **azuredeploy.json** fichier. Ensuite, cliquez sur hello **Raw** fichier de bouton toodisplay hello. Dans votre navigateur, copiez le contenu de hello du fichier de hello. Enregistrez-le hello contenu tooa sur votre ordinateur. Vous pouvez modifier les valeurs de paramètre hello dans le modèle de hello ou déployer le modèle de hello avec un fichier de paramètres distincts.  

    toolearn savoir plus sur comment toodeploy des modèles à l’aide de ces méthodes, tapez `az group deployment create --help`.

### <a name="template-powershell"></a>PowerShell

1. Installer la version la plus récente de hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Dans une session PowerShell, toosign avec votre [compte Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), entrez `login-azurermaccount`.
3. toocreate un groupe de ressources pour le réseau virtuel de hello, entrez hello de commande suivante :

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. Vous pouvez déployer le modèle de hello en utilisant l’une de hello options de paramètres suivantes :
    - **Valeurs de paramètres par défaut**. Entrez hello de commande suivante :
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **Valeurs de paramètres personnalisées**. Télécharger et modifier le modèle de hello avant de le déployer. Vous pouvez également déployer le modèle de hello à l’aide des paramètres à la ligne de commande hello ou déployer le modèle de hello avec un fichier de paramètres distincts. fichiers modèle et les paramètres de hello toodownload, cliquez sur hello **Parcourir sur GitHub** bouton sur hello [créer un réseau virtuel avec deux sous-réseaux](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) page du modèle. Dans GitHub, cliquez sur hello **azuredeploy.parameters.json** ou **azuredeploy.json** fichier. Ensuite, cliquez sur hello **Raw** fichier de bouton toodisplay hello. Dans votre navigateur, copiez le contenu de hello du fichier de hello. Enregistrez-le hello contenu tooa sur votre ordinateur. Vous pouvez modifier les valeurs de paramètre hello dans le modèle de hello ou déployer le modèle de hello avec un fichier de paramètres distincts.  

    toolearn savoir plus sur comment toodeploy des modèles à l’aide de ces méthodes, tapez `Get-Help New-AzureRmResourceGroupDeployment`. 

## <a name="delete"></a>Supprimer des ressources

Lorsque vous avez terminé ce didacticiel, vous pourriez ressources hello toodelete que vous avez créé, afin que vous ne subissez des frais d’utilisation. Suppression d’un groupe de ressources supprime également toutes les ressources qui se trouvent dans le groupe de ressources hello.

### <a name="delete-portal"></a>Portail Azure

1. Dans la zone de recherche du portail hello, entrez **myResourceGroup**. Dans les résultats de recherche de hello, cliquez sur **myResourceGroup**.
2. Sur hello **myResourceGroup** panneau, cliquez sur hello **supprimer** icône.
3. suppression de hello tooconfirm, Bonjour **hello TYPE nom groupe de ressources** , entrez **myResourceGroup**, puis cliquez sur **supprimer**.

### <a name="delete-cli"></a>Interface CLI Azure

Dans une session de l’interface CLI, entrez hello de commande suivante :

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Dans une session PowerShell, entrez hello de commande suivante :

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Étapes suivantes

- toolearn sur tous les paramètres réseau virtuel et sous-réseau, consultez [gérer les réseaux virtuels](virtual-network-manage-network.md#view-vnet) et [gérer les sous-réseaux du réseau virtuel](virtual-network-manage-subnet.md#create-subnet). Vous disposez des options différentes pour l’utilisation de réseaux virtuels et sous-réseaux dans les exigences de la toomeet d’environnement de production différent.
- toofilter entrant et sortant du trafic de sous-réseau, créer et appliquer [groupes de sécurité réseau](virtual-networks-nsg.md) toosubnets.
- Créer un [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou un [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) machine virtuelle, puis connectez-la tooan de réseau virtuel existant.
- tooconnect deux des réseaux virtuels dans hello même emplacement, créez un [réseau virtuel d’homologation](virtual-network-peering-overview.md) entre les réseaux virtuels hello.
- Connecter le réseau local de hello réseau virtuel tooan à l’aide un [passerelle VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.
