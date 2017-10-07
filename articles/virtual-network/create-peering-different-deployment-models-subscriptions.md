---
title: "aaaCreate une homologation de réseau virtuel Azure - déploiement différents modèles - différents abonnements | Documents Microsoft"
description: "Découvrez comment toocreate un réseau virtuel d’homologation entre les réseaux virtuels créés par le biais des modèles de déploiement Azure différentes qui existent dans différents abonnements Azure."
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
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>Créer une homologation de réseaux virtuels Azure - Modèles de déploiement et abonnements différents

Dans ce didacticiel, vous découvrez toocreate un réseau virtuel d’homologation entre réseaux virtuels créés par le biais des modèles de déploiement différent. les réseaux virtuels Hello existent dans différents abonnements. D’homologation deux réseaux virtuels Active ressources toocommunicate différents réseaux virtuels entre eux avec hello même la bande passante et la latence comme si les ressources hello étaient hello même réseau virtuel. En savoir plus sur l’[homologation de réseaux virtuels](virtual-network-peering-overview.md). 

Hello étapes toocreate une homologation de réseau virtuel sont différents, selon que les réseaux virtuels hello sont dans hello identiques ou différent, les abonnements et qui [modèle de déploiement Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello des réseaux virtuels sont créés via. Découvrez comment toocreate a virtual network homologation dans d’autres scénarios en cliquant sur le scénario hello hello tableau suivant :

|Modèle de déploiement Azure  | Abonnement Azure  |
|--------- |---------|
|[Tous deux Resource Manager](virtual-network-create-peering.md) |Identique|
|[Tous deux Resource Manager](create-peering-different-subscriptions.md) |Différent|
|[Un modèle Resource Manager, un modèle classique](create-peering-different-deployment-models.md) |Identique|

Une homologation de réseau virtuel ne peut pas être créée entre deux réseaux virtuels déployés via le modèle de déploiement classique hello. Une homologation de réseau virtuel ne peut être créée qu’entre deux réseaux virtuels qui existent dans hello même région Azure. Lors de la création d’un réseau virtuel d’homologation entre les réseaux virtuels qui existent dans différents abonnements, hello les abonnements doivent être associés toohello même client Azure Active Directory. Si vous n’avez pas encore de locataire Azure Active Directory, vous pouvez rapidement en [créer un](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Si vous avez besoin de tooconnect virtuel réseaux qui ont été créés via le modèle de déploiement classique de hello, qui existe dans différentes régions Azure, ou qui existent dans les abonnements associés clients d’Azure Active Directory toodifferent, que vous pouvez utiliser Azure [Passerelle VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello des réseaux virtuels. 

> [!WARNING]
> La création d’une homologation de réseaux virtuels entre des réseaux virtuels créés par le biais de modèles de déploiement Azure différents qui existent dans des abonnements différents est actuellement en préversion. Homologations de réseaux virtuels créées dans ce scénario ne peuvent pas avoir hello du même niveau de disponibilité et la fiabilité que la création d’un réseau virtuel homologation dans les scénarios de mise en production de la disponibilité. Les homologations de réseaux virtuels créées dans ce scénario ne sont pas prises en charge, peuvent avoir des fonctionnalités limitées et peuvent ne pas être disponibles dans toutes les régions Azure. Pour les notifications actualisées hello sur la disponibilité et l’état de cette fonctionnalité, vérifiez hello [mises à jour du réseau virtuel Azure](https://azure.microsoft.com/updates/?product=virtual-network) page.

Vous pouvez utiliser hello [portail Azure](#portal), hello Azure [une interface de ligne](#cli) (CLI), ou Azure [PowerShell](#powershell) toocreate une homologation de réseau virtuel. Cliquez sur un des hello précédente outil liens toogo directement toohello les étapes de création d’une homologation de réseau virtuel à l’aide de votre outil de choix.

## <a name="register"></a>S’inscrire à la version préliminaire de hello

tooregister pour l’aperçu de hello, étapes hello complète qui suivent pour les deux abonnements qui contiennent des réseaux virtuels hello que vous souhaitez toopeer. Hello l’outil seulement vous pouvez utiliser tooregister pour l’aperçu de hello est PowerShell.

1. Installer la version la plus récente de hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Démarrez une session PowerShell et connectez-vous à tooAzure à l’aide de hello `login-azurermaccount` commande.
3. Inscrire votre abonnement pour l’aperçu de hello en entrant hello suivant de commandes :

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    N’effectuez pas les étapes de hello dans hello Portal, CLI d’Azure ou de PowerShell sections de cet article jusqu'à ce que hello **RegistrationState** de sortie une fois que la saisie de hello commande suivante est **inscrit** pour les deux abonnements :

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>Créer une homologation - portail Azure

Ce didacticiel utilise des comptes différents pour chaque abonnement. Si vous utilisez un compte disposant d’autorisations tooboth abonnements, vous pouvez utiliser hello même compte pour toutes les étapes, ignorez les étapes hello pour la journalisation déconnecte du portail de hello et ignorez les étapes hello pour affecter des réseaux virtuels d’autorisations toohello un autre utilisateur. Avant d’effectuer une des hello comme suit, vous devez vous inscrire pour l’aperçu de hello. tooregister, hello terminé les étapes Bonjour [s’inscrire pour la version préliminaire de hello](#register) section de cet article. Ne poursuivez pas hello restant étapes jusqu'à ce que les deux abonnements sont inscrits pour l’aperçu de hello.
 
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) comme l’UtilisateurA. compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
2. Cliquez sur **+ Nouveau**, puis sur **Mise en réseau** et **Réseau virtuel**.
3. Bonjour **créer un réseau virtuel** panneau, puis entrez ou sélectionnez les valeurs pour hello suivant les paramètres, **créer**:
    - **Nom** : *myVnetA*
    - **Espace d’adressage** : *10.0.0.0/16*
    - **Nom du sous-réseau** : *par défaut*
    - **Espace d’adressage de sous-réseau** : *10.0.0.0/24*
    - **Abonnement :** sélectionnez l’abonnement A.
    - **Groupe de ressources** : sélectionnez **Créer** et entrez *myResourceGroupA*
    - **Emplacement** : *États-Unis de l’Est*
4. Bonjour **recherche les ressources** zone en haut hello hello du portail de, type *myVnetA*. Cliquez sur **myVnetA** lorsqu’il apparaît dans les résultats de recherche hello. Un panneau s’affiche pour hello **myVnetA** réseau virtuel.
5. Bonjour **myVnetA** panneau qui s’affiche, cliquez sur **(IAM) de contrôle d’accès** de liste verticale de hello des options sur hello gauche du Panneau de hello.
6. Bonjour **myVnetA - contrôle d’accès (IAM)** panneau qui s’affiche, cliquez sur **+ ajouter**.
7. Bonjour **ajouter des autorisations** panneau qui s’affiche, sélectionnez **collaborateur de réseau** Bonjour **rôle** boîte.
8. Bonjour **sélectionnez** zone, sélectionnez UserB ou tapez toosearch d’adresse de messagerie de UserB pour celle-ci. Bonjour la liste des utilisateurs affichés est de hello même locataire Azure Active Directory en tant que réseau virtuel de hello que vous configurez hello d’homologation pour. Cliquez sur UserB lorsqu’il apparaît dans la liste de hello.
9. Cliquez sur **Enregistrer**.
10. Se déconnecter portail hello en tant que l’UtilisateurA, puis connectez-vous en tant qu’utilisateur b.
11. Cliquez sur **+ nouveau**, type *réseau virtuel* Bonjour **hello de recherche Marketplace** zone, puis cliquez sur **réseau virtuel** dans les résultats de recherche hello .
12. Bonjour **réseau virtuel** panneau qui s’affiche, sélectionnez **classique** Bonjour **sélectionner un modèle de déploiement** zone, puis cliquez sur **créer**.
13.   Dans hello créer un réseau virtuel (classiques) qui s’affiche, entrez hello valeurs suivantes :

    - **Nom** : *myVnetB*
    - **Espace d’adressage** : *10.1.0.0/16*
    - **Nom du sous-réseau** : *par défaut*
    - **Espace d’adressage de sous-réseau** : *10.1.0.0/24*
    - **Abonnement :** sélectionnez l’abonnement B.
    - **Groupe de ressources** : sélectionnez **Créer** et entrez *myResourceGroupB*
    - **Emplacement** : *États-Unis de l’Est*

14. Bonjour **recherche les ressources** zone en haut hello hello du portail de, type *myVnetB*. Cliquez sur **myVnetB** lorsqu’il apparaît dans les résultats de recherche hello. Un panneau s’affiche pour hello **myVnetB** réseau virtuel.
15. Bonjour **myVnetB** panneau qui s’affiche, cliquez sur **propriétés** de liste verticale de hello des options sur hello gauche du Panneau de hello. Hello de copie **ID de ressource**, qui est utilisé dans une étape ultérieure. ID de ressource Hello est similaire toohello l’exemple suivant : /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. Effectuez les étapes 5 à 9 pour myVnetB, en entrant **UserA** à l’étape 8.
17. Déconnectez-vous de portail hello comme UtilisateurB et connectez-vous en tant que l’UtilisateurA.
18. Bonjour **recherche les ressources** zone en haut hello hello du portail de, type *myVnetA*. Cliquez sur **myVnetA** lorsqu’il apparaît dans les résultats de recherche hello. Un panneau s’affiche pour hello **myVnet** réseau virtuel.
19. Cliquez sur **myVnetA**.
20. Bonjour **myVnetA** panneau qui s’affiche, cliquez sur **homologations** de liste verticale de hello des options sur hello gauche du Panneau de hello.
21. Bonjour **myVnetA - homologations** panneau s’affiche, cliquez sur **+ ajouter**
22. Bonjour **ajouter d’homologation** panneau qui s’affiche, entrez, ou sélectionnez hello options suivantes, puis cliquez sur **OK**:
     - **Nom** : *myVnetAToMyVnetB*
     - **Modèle de déploiement de réseau virtuel** : sélectionnez **Classique**.
     - **Je connais mon ID de ressource** : cochez cette case.
     - **ID de ressource**: entrez les ID de ressource de hello de myVnetB à partir de l’étape 15.
     - **Autoriser l’accès au réseau virtuel :** vérifiez que l’option **Activé** est sélectionnée.
    Il n’y aucun autre paramètre utilisé dans ce didacticiel. toolearn sur tous les paramètres d’homologation, lire [gérer homologations de réseaux virtuels](virtual-network-manage-peering.md#create-a-peering).
23. Après avoir cliqué sur **OK** à l’étape précédente de hello, hello **ajouter d’homologation** panneau se ferme et vous voyez hello **myVnetA - homologations** panneau à nouveau. Après quelques secondes, hello d’homologation que vous avez créé s’affiche dans le panneau de hello. **Connecté** est répertorié dans hello **d’homologation de statut** colonne hello **myVnetAToMyVnetB** d’homologation vous créé. Hello d’homologation est désormais établi. Il n’est aucun besoin toopeer hello réseau virtuelle (classique) toohello réseau virtuel (Resource Manager).

    Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

24. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
25. **Facultatif**: toodelete ressources hello que vous créez dans ce didacticiel, les étapes hello complète Bonjour [supprimer des ressources](#delete-portal) section de cet article.

## <a name="cli"></a>Créer une homologation - interface de ligne de commande Azure

Ce didacticiel utilise des comptes différents pour chaque abonnement. Si vous utilisez un compte disposant d’autorisations tooboth abonnements, vous pouvez utiliser hello même compte pour toutes les étapes, ignorez les étapes hello pour la journalisation en dehors d’Azure et supprimer des lignes hello de script qui créent des attributions de rôles utilisateur. Remplacez UserA@azure.com et UserB@azure.com dans tous les hello scripts avec les noms d’utilisateur hello que vous utilisez pour l’UtilisateurA et UserB suivants. 

Avant d’effectuer une des hello comme suit, vous devez vous inscrire pour l’aperçu de hello. tooregister, hello terminé les étapes Bonjour [s’inscrire pour la version préliminaire de hello](#register) section de cet article. Ne poursuivez pas hello restant étapes jusqu'à ce que les deux abonnements sont inscrits pour l’aperçu de hello.

1. [Installer](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) réseau virtuel hello Azure CLI 1.0 toocreate hello (classique).
2. Ouvrez une session CLI et se connecter en tant qu’utilisateur b à l’aide de hello tooAzure `azure login` commande.
3. Exécutez hello CLI en mode de gestion de Service en entrant hello `azure config mode asm` commande.
4. Entrez hello toocreate hello réseau virtuelle (classique) de commande suivante :
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. Hello restant étapes doit être effectuée à l’aide d’un interpréteur de commandes bash avec hello CLI d’Azure 2.0.4 ou version ultérieure [installé](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), ou à l’aide de hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. Cliquez sur hello **essayez-la** bouton Bonjour génère un script qui suivent, ce qui ouvre un environnement de Cloud qui vous connecte tooyour compte Azure. Pour les options sur en cours d’exécution bash scripts CLI sur un client Windows, consultez [hello CLI d’Azure en cours d’exécution dans Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 
6. Copiez hello suivant d’éditeur de texte script tooa sur votre PC. Remplacez `<SubscriptionB-Id>` par votre ID d’abonnement. Si vous ne connaissez pas votre Id d’abonnement, entrez hello `az account show` commande. Hello valeur pour **id** Bonjour sortie est votre ID d’abonnement. Copiez le script de hello modifié, collez-le dans la session de tooyour CLI 2.0, puis appuyez sur `Enter`. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    Lorsque vous avez créé le réseau virtuel de hello (classique) à l’étape 4, Azure créé le réseau virtuel de hello Bonjour *réseau par défaut* groupe de ressources.
7. Connectez-vous UserB en dehors d’Azure et vous connecter en tant que l’UtilisateurA hello CLI 2.0.
8. Créez un groupe de ressources et un réseau virtuel (Resource Manager). Copie hello suivantes de script, collez-le dans la session CLI tooyour et appuyez sur `Enter`. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Créez un réseau virtuel d’homologation entre hello deux réseaux virtuels créés par le biais des modèles de déploiement différentes hello. Copiez hello suivant d’éditeur de texte script tooa sur votre PC. Remplacez `<SubscriptionB-id>` par votre ID d’abonnement. Si vous ne connaissez pas votre Id d’abonnement, entrez hello `az account show` commande. Hello valeur pour **id** Bonjour sortie est votre ID d’abonnement. Azure créé le réseau virtuel hello (classiques) créé à l’étape 4 dans un groupe de ressources nommé *réseau par défaut*. Collez le script que vous hello modifié dans votre session CLI, puis appuyez sur `Enter`.

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Après l’exécution du script de hello, passez en revue le hello d’homologation pour le réseau virtuel de hello (Resource Manager). Copier hello script suivant et collez-le dans votre session CLI :

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    Hello sortie affiche **connecté** Bonjour **PeeringState** colonne.

    Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

11. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
12. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-cli) dans cet article.

## <a name="powershell"></a>Créer une homologation - PowerShell

Ce didacticiel utilise des comptes différents pour chaque abonnement. Si vous utilisez un compte disposant d’autorisations tooboth abonnements, vous pouvez utiliser hello même compte pour toutes les étapes, ignorez les étapes hello pour la journalisation en dehors d’Azure et supprimer des lignes hello de script qui créent des attributions de rôles utilisateur. Remplacez UserA@azure.com et UserB@azure.com dans tous les hello scripts avec les noms d’utilisateur hello que vous utilisez pour l’UtilisateurA et UserB suivants. 

Avant d’effectuer une des hello comme suit, vous devez vous inscrire pour l’aperçu de hello. tooregister, hello terminé les étapes Bonjour [s’inscrire pour la version préliminaire de hello](#register) section de cet article. Ne poursuivez pas hello restant étapes jusqu'à ce que les deux abonnements sont inscrits pour l’aperçu de hello.

1. Installer la version la plus récente de hello PowerShell hello [Azure](https://www.powershellgallery.com/packages/Azure) et [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules. Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Démarrez une session PowerShell.
3. Dans PowerShell, ouvrir une session dans l’abonnement de tooUserB comme UserB en entrant hello `Add-AzureAccount` commande.
4. toocreate un réseau virtuel (classique) avec PowerShell, vous devez créer un nouveau, ou modifier un existant, fichier de configuration réseau. Découvrez comment trop[exporter, mettre à jour et importer les fichiers de configuration réseau](virtual-networks-using-network-configuration-file.md). Hello fichier doit suivants hello **VirtualNetworkSite** élément pour le réseau virtuel de hello utilisé dans ce didacticiel :

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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

5. Se connecter en entrant hello abonnement de tooUserB que les commandes de gestionnaire de ressources UserB toouse `login-azurermaccount` commande.
6. Affecter l’UtilisateurA autorisations toovirtual réseau suivant de hello B. copie tooa éditeur de texte sur votre PC de script remplace `<SubscriptionB-id>` avec l’ID de hello d’abonnement B. Si vous ne connaissez l’Id d’abonnement hello, entrez hello `Get-AzureRmSubscription` commande tooview il. Hello valeur pour **Id** Bonjour retourné de sortie est votre ID d’abonnement. Azure créé le réseau virtuel hello (classiques) créé à l’étape 4 dans un groupe de ressources nommé *réseau par défaut*. script de hello tooexecute, hello de copie modifiée script, collez-le dans tooPowerShell, puis appuyez sur `Enter`.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. Déconnecter Azure comme l’UtilisateurB et dans l’abonnement de tooUserA en tant que l’UtilisateurA en entrant hello `login-azurermaccount` commande. compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
8. Créer un réseau virtuel de hello (Resource Manager) en copiant hello script, en les collant dans tooPowerShell, puis appuyez sur Suivant `Enter`:

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. Affecter l’UtilisateurB autorisations toomyVnetA. Suivant de hello copie tooa éditeur de texte sur votre PC de script et remplacez `<SubscriptionA-Id>` avec l’ID de hello d’abonnement A. Si vous ne connaissez l’Id d’abonnement hello, entrez hello `Get-AzureRmSubscription` commande tooview il. Hello valeur pour **Id** Bonjour retourné de sortie est votre ID d’abonnement. Collez hello la version modifiée du script de hello dans PowerShell, puis appuyez sur `Enter` tooexecute il.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. Copie hello ci-dessous tooa éditeur de texte sur votre PC de script, remplacez `<SubscriptionB-id>` avec hello l’ID d’abonnement B. toopeer myVnetA toomyVNetB, copiez le script de hello modifié, collez-le dans tooPowerShell, puis appuyez sur `Enter`.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. Afficher l’état de d’homologation de hello de myVnetA en copiant hello script, en les collant dans PowerShell et en appuyant sur Suivant `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    état de Hello est **connecté**. Il change également**connecté** une fois que vous configurez toomyVnetA d’homologation de hello à partir de myVnetB.

    Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

12. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
13. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-powershell) dans cet article.

## <a name="permissions"></a>Autorisations

Hello tous les comptes toocreate une homologation de réseau virtuel doivent avoir hello nécessaires ou autorisations. Par exemple, si vous ont été homologation deux réseaux virtuels nommés myVnetA et myVnetB, doit être affecté à votre compte hello suivant rôle minimale ou les autorisations pour chaque réseau virtuel :
    
|Réseau virtuel|Modèle de déploiement|Rôle|Autorisations|
|---|---|---|---|
|myVnetA|Gestionnaire de ressources|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Classique|[Collaborateur de réseau classique](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/A|
|myVnetB|Gestionnaire de ressources|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Classique|[Collaborateur de réseau classique](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

En savoir plus sur [rôles intégrés](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) et l’affectation des autorisations spécifiques trop[des rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager uniquement).

## <a name="delete"></a>Supprimer des ressources
Lorsque vous avez terminé ce didacticiel, vous pourriez les ressources de hello toodelete que vous avez créé dans le didacticiel de hello, donc vous ne subissez des frais d’utilisation. Suppression d’un groupe de ressources supprime également toutes les ressources qui se trouvent dans le groupe de ressources hello.

### <a name="delete-portal"></a>Portail Azure

1. Dans la zone de recherche du portail hello, entrez **myResourceGroupA**. Dans les résultats de recherche de hello, cliquez sur **myResourceGroupA**.
2. Sur hello **myResourceGroupA** panneau, cliquez sur hello **supprimer** icône.
3. suppression de hello tooconfirm, Bonjour **hello TYPE nom groupe de ressources** , entrez **myResourceGroupA**, puis cliquez sur **supprimer**.
4. Bonjour **recherche les ressources** zone en haut hello hello du portail de, type *myVnetB*. Cliquez sur **myVnetB** lorsqu’il apparaît dans les résultats de recherche hello. Un panneau s’affiche pour hello **myVnetB** réseau virtuel.
5. Bonjour **myVnetB** panneau, cliquez sur **supprimer**.
6. suppression de hello tooconfirm, cliquez sur **Oui** Bonjour **réseau virtuel de suppression** boîte.

### <a name="delete-cli"></a>Interface CLI Azure

1. Ouvrez une session dans tooAzure à l’aide de hello réseau virtuel CLI 2.0 toodelete hello (Resource Manager) avec hello de commande suivante :

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. Ouvrez une session dans tooAzure à l’aide de hello réseau virtuel Azure CLI 1.0 toodelete hello (classiques) avec hello suivant de commandes :

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. À l’invite de commandes PowerShell hello, entrez hello toodelete hello réseau virtuel (Resource Manager) de commande suivante :

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete hello réseau virtuelle (classique) avec PowerShell, vous devez modifier un fichier de configuration réseau. Découvrez comment trop[exporter, mettre à jour et importer les fichiers de configuration réseau](virtual-networks-using-network-configuration-file.md). Supprimer hello suivant élément VirtualNetworkSite pour le réseau virtuel de hello utilisé dans ce didacticiel :

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
