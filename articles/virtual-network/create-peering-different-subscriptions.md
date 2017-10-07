---
title: "aaaCreate virtuelle Azure réseau homologation - Gestionnaire de ressources - différents abonnements | Documents Microsoft"
description: "Découvrez comment toocreate un réseau virtuel d’homologation entre les réseaux virtuels créés via le Gestionnaire des ressources qui existent dans différents abonnements Azure."
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
ms.openlocfilehash: c7983a86031e061c1155144e5c493ee9578fa583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-different-subscriptions"></a>Créer une homologation de réseaux virtuels - Resource Manager - Abonnements différents 

Dans ce didacticiel, vous découvrez toocreate un réseau virtuel d’homologation entre réseaux virtuels créés par le biais du Gestionnaire de ressources. les réseaux virtuels Hello existent dans différents abonnements. D’homologation deux réseaux virtuels Active ressources toocommunicate différents réseaux virtuels entre eux avec hello même la bande passante et la latence comme si les ressources hello étaient hello même réseau virtuel. En savoir plus sur l’[homologation de réseaux virtuels](virtual-network-peering-overview.md). 

Hello étapes toocreate une homologation de réseau virtuel sont différents, selon que les réseaux virtuels hello sont dans hello identiques ou différent, les abonnements et qui [modèle de déploiement Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello des réseaux virtuels sont créés via. Découvrez comment toocreate a virtual network homologation dans d’autres scénarios en cliquant sur le scénario hello hello tableau suivant :

|Modèle de déploiement Azure  | Abonnement Azure  |
|--------- |---------|
|[Tous deux Resource Manager](virtual-network-create-peering.md) |Identique|
|[Un modèle Resource Manager, un modèle classique](create-peering-different-deployment-models.md) |Identique|
|[Un modèle Resource Manager, un modèle classique](create-peering-different-deployment-models-subscriptions.md) |Différent|

Une homologation de réseau virtuel ne peut pas être créée entre deux réseaux virtuels déployés via le modèle de déploiement classique hello. Une homologation de réseau virtuel ne peut être créée qu’entre deux réseaux virtuels qui existent dans hello même région Azure. Lors de la création d’un réseau virtuel d’homologation entre les réseaux virtuels qui existent dans différents abonnements, hello les abonnements doivent être associés toohello même client Azure Active Directory. Si vous n’avez pas encore de locataire Azure Active Directory, vous pouvez rapidement en [créer un](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Si vous avez besoin de tooconnect virtuel réseaux qui ont été créés via le modèle de déploiement classique de hello, qui existe dans différentes régions Azure, ou qui existent dans les abonnements associés clients d’Azure Active Directory toodifferent, que vous pouvez utiliser Azure [Passerelle VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello des réseaux virtuels. 

Vous pouvez utiliser hello [portail Azure](#portal), hello Azure [une interface de ligne](#cli) (CLI), ou Azure [PowerShell](#powershell) toocreate une homologation de réseau virtuel. Cliquez sur un des hello précédente outil liens toogo directement toohello les étapes de création d’une homologation de réseau virtuel à l’aide de votre outil de choix.

## <a name="portal"></a>Créer une homologation - portail Azure

Ce didacticiel utilise des comptes différents pour chaque abonnement. Si vous utilisez un compte disposant d’autorisations tooboth abonnements, vous pouvez utiliser hello même compte pour toutes les étapes, ignorez les étapes hello pour la journalisation déconnecte du portail de hello et ignorez les étapes hello pour affecter des réseaux virtuels d’autorisations toohello un autre utilisateur.

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
8. Bonjour **sélectionnez** zone, sélectionnez un UserB ou tapez toosearch d’adresse de messagerie de UserB pour celle-ci. Bonjour la liste des utilisateurs affichés est de hello même locataire Azure Active Directory en tant que réseau virtuel de hello que vous configurez hello d’homologation pour.
9. Cliquez sur **Enregistrer**.
10. Bonjour **myVnetA - contrôle d’accès (IAM)** panneau, cliquez sur **propriétés** de liste verticale de hello des options sur hello gauche du Panneau de hello. Hello de copie **ID de ressource**, qui est utilisé dans une étape ultérieure. ID de ressource Hello est similaire toohello l’exemple suivant : /subscriptions/<Subscription Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/virtualNetworks/myVnetA.
11. Se déconnecter portail hello en tant que l’UtilisateurA, puis connectez-vous en tant qu’utilisateur b.
12. Effectuez les étapes 2 et 3, entrant ou en sélectionnant hello suivant à l’étape 3 :

    - **Nom** : *myVnetB*
    - **Espace d’adressage** : *10.1.0.0/16*
    - **Nom du sous-réseau** : *par défaut*
    - **Espace d’adressage de sous-réseau** : *10.1.0.0/24*
    - **Abonnement :** sélectionnez l’abonnement B.
    - **Groupe de ressources** : sélectionnez **Créer** et entrez *myResourceGroupB*
    - **Emplacement** : *États-Unis de l’Est*

13. Bonjour **recherche les ressources** zone en haut hello hello du portail de, type *myVnetB*. Cliquez sur **myVnetB** lorsqu’il apparaît dans les résultats de recherche hello. Un panneau s’affiche pour hello **myVnetB** réseau virtuel.
14. Bonjour **myVnetB** panneau qui s’affiche, cliquez sur **propriétés** de liste verticale de hello des options sur hello gauche du Panneau de hello. Hello de copie **ID de ressource**, qui est utilisé dans une étape ultérieure. ID de ressource Hello est similaire toohello l’exemple suivant : /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB.
15. Cliquez sur **(IAM) de contrôle d’accès** Bonjour **myVnetB** lame et puis suivez les étapes 5 à 10 pour myVnetB, entrez **UserA** à l’étape 8.
16. Déconnectez-vous de portail hello comme UtilisateurB et connectez-vous en tant que l’UtilisateurA.
17. Bonjour **recherche les ressources** zone en haut hello hello du portail de, type *myVnetA*. Cliquez sur **myVnetA** lorsqu’il apparaît dans les résultats de recherche hello. Un panneau s’affiche pour hello **myVnet** réseau virtuel.
18. Cliquez sur **myVnetA**.
19. Bonjour **myVnetA** panneau qui s’affiche, cliquez sur **homologations** de liste verticale de hello des options sur hello gauche du Panneau de hello.
20. Bonjour **myVnetA - homologations** panneau s’affiche, cliquez sur **+ ajouter**
21. Bonjour **ajouter d’homologation** panneau qui s’affiche, entrez, ou sélectionnez hello options suivantes, puis cliquez sur **OK**:
     - **Nom** : *myVnetAToMyVnetB*
     - **Modèle de déploiement de réseau virtuel** : sélectionnez **Resource Manager**.
     - **Je connais mon ID de ressource** : cochez cette case.
     - **ID de ressource**: entrez l’ID de ressource hello à l’étape 14.
     - **Autoriser l’accès au réseau virtuel :** vérifiez que l’option **Activé** est sélectionnée.
    Il n’y aucun autre paramètre utilisé dans ce didacticiel. toolearn sur tous les paramètres d’homologation, lire [gérer homologations de réseaux virtuels](virtual-network-manage-peering.md#create-a-peering).
22. Après avoir cliqué sur **OK** à l’étape précédente de hello, hello **ajouter d’homologation** panneau se ferme et vous voyez hello **myVnetA - homologations** panneau à nouveau. Après quelques secondes, hello d’homologation que vous avez créé s’affiche dans le panneau de hello. **Initiée par** est répertorié dans hello **d’homologation de statut** colonne hello **myVnetAToMyVnetB** d’homologation vous créé. Vous avez homologuer myVnetA toomyVnetB, mais vous devez maintenant homologue myVnetB toomyVnetA. Hello d’homologation doit être créé dans les deux sens tooenable ressources toocommunicate de réseaux virtuels hello entre eux.
23. Déconnectez-vous de portail hello en tant que l’UtilisateurA et connectez-vous en tant qu’utilisateur b.
24. Répétez les étapes 17 à 21 pour MyVnetB. À l’étape 21, nom hello d’homologation *myVnetBToMyVnetA*, sélectionnez *myVnetA* pour **réseau virtuel**et entrez l’ID de hello à l’étape 10 de hello **ID de ressource** boîte.
25. Quelques secondes après avoir cliqué sur **OK** toocreate hello d’homologation pour myVnetB, hello **myVnetBToMyVnetA** d’homologation vous venez de créer est répertorié avec **connecté** Bonjour  **ÉTAT de l’homologation** colonne.
26. Déconnectez-vous de portail hello comme UtilisateurB et connectez-vous en tant que l’UtilisateurA.
27. Répétez les étapes 17-19. Hello **d’homologation de statut** pour hello **myVnetAToVNetB** d’homologation est désormais également **connecté**. Hello d’homologation est établie avec succès une fois que vous **connecté** Bonjour **d’homologation de statut** colonne pour les deux réseaux virtuels dans l’homologation de hello. Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
28. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
29. **Facultatif**: toodelete ressources hello que vous créez dans ce didacticiel, les étapes hello complète Bonjour [supprimer des ressources](#delete-portal) section de cet article.

## <a name="cli"></a>Créer une homologation - interface de ligne de commande Azure

Ce didacticiel utilise des comptes différents pour chaque abonnement. Si vous utilisez un compte disposant d’autorisations tooboth abonnements, vous pouvez utiliser hello même compte pour toutes les étapes, ignorez les étapes hello pour la journalisation en dehors d’Azure et supprimer des lignes hello de script qui créent des attributions de rôles utilisateur. Remplacez UserA@azure.com et UserB@azure.com dans tous les hello scripts avec les noms d’utilisateur hello que vous utilisez pour l’UtilisateurA et UserB suivants.

Hello le script suivant :

- Requiert hello CLI d’Azure version 2.0.4 ou version ultérieure. version de hello toofind, exécutez `az --version`. Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Fonctionne dans un interpréteur de commandes Bash. Pour les options sur l’exécution de scripts CLI d’Azure sur le client Windows, consultez [hello CLI d’Azure en cours d’exécution dans Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Au lieu d’installer hello CLI et ses dépendances, vous pouvez utiliser hello Azure Cloud Shell. Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure. Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte. Cliquez sur hello **essayez-la** bouton dans le script hello qui suit, qui permet d’appeler un environnement de Cloud qui vous pouvez vous connecter tooyour compte Azure avec. 

1. Ouvrez une session CLI et se connecter en tant que l’UtilisateurA à l’aide de hello tooAzure `azure login` commande. compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
2. Copiez hello suivant l’éditeur de texte script tooa sur votre ordinateur, remplacez `<SubscriptionA-Id>` avec hello ID d’abonnement a, puis hello de copie modifié script, collez-le dans votre session CLI, puis appuyez sur `Enter`. Si vous ne connaissez pas votre Id d’abonnement, entrez la commande de 'afficher de compte az' hello. Hello valeur pour **id** Bonjour sortie est votre ID d’abonnement.

    ```azurecli-interactive
    # Create a resource group.
    az group create \
      --name myResourceGroupA \
      --location eastus

    # Create virtual network A.
    az network vnet create \
      --name myVnetA \
      --resource-group myResourceGroupA \
      --location eastus \
      --address-prefix 10.0.0.0/16

    # Assign UserB permissions toovirtual network A.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```
    
     attribution d’autorisation Hello pour l’UtilisateurB n’est pas obligatoire. Homologation peut être établie même si les utilisateurs individuellement déclenchent des demandes d’homologation pour leurs réseaux virtuels respectifs, tant que hello demande la correspondance. Ajout d’un utilisateur doté de privilèges de myVNetB en tant que réseau collaborateur dans le réseau virtuel local de hello rend plus facile d’installation de hello toodo.
3. Déconnectez-vous d’Azure en tant que l’UtilisateurA à l’aide de hello `az logout` de commandes, puis connectez-vous à tooAzure comme UserB. compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
4. Créez myVnetB. Copiez le contenu du script hello dans l’éditeur de texte étape 2 tooa sur votre PC. Remplacez `<SubscriptionA-Id>` par hello ID de SubscriptionB. Modifiez 10.0.0.0/16 too10.1.0.0/16, des modifications sous la forme tooB et tous les Bs tooA. Copiez le script de hello modifié, collez-le dans la session CLI tooyour, puis appuyez sur `Enter`. 
5. Déconnecter Azure comme l’UtilisateurB et dans tooAzure comme l’UtilisateurA.
6. Créez un réseau virtuel d’homologation de myVnetA toomyVnetB. Copiez hello suivant d’éditeur de texte de script contenu tooa sur votre PC. Remplacez `<SubscriptionB-Id>` par hello ID de SubscriptionB. script de hello tooexecute, copiez le script de hello modifié, collez-le dans votre session CLI, appuyez sur ENTRÉE.
 
    ```azurecli-interactive
        # Get hello id for myVnetA.
        vnetAId=$(az network vnet show \
          --resource-group myResourceGroupA \
          --name myVnetA \
          --query id --out tsv)
    
        # Peer myVNetA toomyVNetB.
        az network vnet peering create \
          --name myVnetAToMyVnetB \
          --resource-group myResourceGroupA \
          --vnet-name myVnetA \
          --remote-vnet-id /subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/VirtualNetworks/myVnetB \
          --allow-vnet-access
    ```

7. État d’homologation de hello de myVnetA d’affichage.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroupA \
      --vnet-name myVnetA \
      --output table
    ```

    état de Hello est **a été initiée**. Il change également**connecté** après avoir créé les toomyVnetA d’homologation hello de myVnetB.

8. Déconnecter l’UtilisateurA à partir d’Azure et dans tooAzure en tant qu’utilisateur b.
9. Créer hello d’homologation de myVnetB toomyVnetA. Copiez le contenu du script hello dans l’éditeur de texte étape 6 tooa sur votre PC. Remplacez `<SubscriptionB-Id>` avec ID hello SubscriptionA et de modification sous la forme tooB et tous les Bs tooA. Une fois que vous avez apporté des modifications de hello, hello de copie modifiée de script, collez-le dans votre session CLI, puis appuyez sur `Enter`.
10. État d’homologation de hello de myVnetB d’affichage. Copiez le contenu du script hello dans l’éditeur de texte étape 7 tooa sur votre PC. Modifier un tooB pour le groupe de ressources hello et noms de réseau virtuel, copiez le script de hello, collez le script que vous hello modifié dans la session CLI tooyour, puis appuyez sur `Enter`. Hello d’homologation de l’état est **connecté**. Hello d’homologation état myVnetA modifications trop**connecté** après avoir créé hello d’homologation de myVnetB toomyVnetA. Vous pouvez reconnecter l’UtilisateurA tooAzure et l’étape 7 état d’homologation de hello tooverify de myVnetA. 

    > [!NOTE]
    > Hello d’homologation n’est pas établie jusqu'à ce que l’état d’homologation hello est **connecté** pour les deux réseaux virtuels.

11. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
12. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-cli) dans cet article.

Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
 
## <a name="powershell"></a>Créer une homologation - PowerShell

Ce didacticiel utilise des comptes différents pour chaque abonnement. Si vous utilisez un compte disposant d’autorisations tooboth abonnements, vous pouvez utiliser hello même compte pour toutes les étapes, ignorez les étapes hello pour la journalisation en dehors d’Azure et supprimer des lignes hello de script qui créent des attributions de rôles utilisateur. Remplacez UserA@azure.com et UserB@azure.com dans tous les hello scripts avec les noms d’utilisateur hello que vous utilisez pour l’UtilisateurA et UserB suivants.

1. Installer la version la plus récente de hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Démarrez une session PowerShell.
3. Dans PowerShell, connectez-vous tooAzure comme l’UtilisateurA en entrant hello `login-azurermaccount` commande. compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
4. Créer un groupe de ressources et le réseau virtuel A. copie hello suivant le texte du script tooa éditeur sur votre PC. Remplacez `<SubscriptionA-Id>` par hello ID d’abonnement a. Si vous ne connaissez pas votre Id d’abonnement, entrez hello `Get-AzureRmSubscription` commande tooview il. Hello valeur pour **Id** Bonjour retourné de sortie est votre ID d’abonnement. script de hello tooexecute, hello de copie modifiée script, collez-le dans tooPowerShell, puis appuyez sur `Enter`.

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name MyResourceGroupA `
      -Location eastus

    # Create virtual network A.
    $vNetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName MyResourceGroupA `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus

    # Assign UserB permissions toomyVnetA.
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

    attribution d’autorisation Hello pour l’UtilisateurB n’est pas obligatoire. Homologation peut être établie même si les utilisateurs individuellement déclenchent des demandes d’homologation pour leurs réseaux virtuels respectifs, tant que hello demande la correspondance. Ajout d’un utilisateur doté de privilèges de hello autre réseau virtuel en tant qu’utilisateur dans le réseau virtuel local de hello rend plus facile d’installation de hello toodo.
5. Déconnectez UserA d’Azure et connectez UserB. compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel. Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.
6. Copiez le contenu du script hello dans l’éditeur de texte étape 4 tooa sur votre PC. Remplacez `<SubscriptionA-Id>` avec l’ID de hello pour l’abonnement B. modification 10.0.0.0/16 too10.1.0.0/16. Modification, tout comme tooB et tous les Bs tooA. script de hello tooexecute, hello de copie modifiée script, collez dans PowerShell, puis appuyez sur `Enter`.
7. Déconnectez UserB d’Azure et connectez UserA.
8. Créer hello d’homologation de myVnetA toomyVnetB. Copiez hello suivant d’éditeur de texte script tooa sur votre PC. Remplacez `<SubscriptionB-Id>` avec hello l’ID d’abonnement script hello de b. tooexecute, copiez hello modifié script, collez dans tooPowerShell, puis appuyez sur `Enter`.
 
    ```powershell
    # Peer myVnetA toomyVnetB.
    $vNetA=Get-AzureRmVirtualNetwork -Name myVnetA -ResourceGroupName myResourceGroupA
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vNetA `
      -RemoteVirtualNetworkId "/subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/virtualNetworks/myVnetB"
    ```

9. État d’homologation de hello de myVnetA d’affichage.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroupA `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    état de Hello est **a été initiée**. Il change également**connecté** une fois que vous configurez toomyVnetA d’homologation de hello à partir de myVnetB.

10. Déconnectez UserA d’Azure et connectez UserB.
11. Créer hello d’homologation de myVnetB toomyVnetA. Copiez le contenu du script hello dans l’éditeur de texte étape tooa 8 sur votre PC. Remplacez `<SubscriptionB-Id>` avec l’ID de hello d’abonnement A et modifier tous les tooB de A et tooA de l’ensemble B. script de hello tooexecute, hello de copie modifiée script, collez-le dans tooPowerShell, puis appuyez sur `Enter`.
12. État d’homologation de hello de myVnetB d’affichage. Copiez le contenu du script hello dans l’éditeur de texte étape 9 tooa sur votre PC. Modifier un tooB pour le groupe de ressources hello et noms de réseau virtuel. script de hello tooexecute, collez hello modifié script PowerShell, puis appuyez sur `Enter`. état de Hello est **connecté**. Hello d’état d’homologation de **myVnetA** change également**connecté** après avoir créé hello d’homologation de **myVnetB** trop**myVnetA**. Vous pouvez reconnecter l’UtilisateurA tooAzure et l’étape 9 état d’homologation de hello tooverify de myVnetA. 

    > [!NOTE]
    > Hello d’homologation n’est pas établie jusqu'à ce que l’état d’homologation hello est **connecté** pour les deux réseaux virtuels.

    Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP. Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello. Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS. Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

13. **Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.
14. **Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-powershell) dans cet article.

## <a name="permissions"></a>Autorisations

Hello tous les comptes toocreate une homologation de réseau virtuel doivent avoir hello nécessaires ou autorisations. Par exemple, si vous ont été d’homologation deux réseaux virtuels nommés **myVnetA** et **myVnetB**, hello suivant rôle minimale ou les autorisations pour chaque réseau virtuel doit être affecté à votre compte :
    
|Réseau virtuel|Rôle|Autorisations|
|---|---|---|
|myVnetA|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|myVnetB|[Collaborateur de réseau](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

En savoir plus sur [rôles intégrés](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) et l’affectation des autorisations spécifiques trop[des rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager uniquement).

## <a name="delete"></a>Supprimer des ressources
Lorsque vous avez terminé ce didacticiel, vous pourriez les ressources de hello toodelete que vous avez créé dans le didacticiel de hello, donc vous ne subissez des frais d’utilisation. Suppression d’un groupe de ressources supprime également toutes les ressources qui se trouvent dans le groupe de ressources hello.

### <a name="delete-portal"></a>Portail Azure

1. Ouvrez une session dans toohello portail Azure en tant que l’UtilisateurA.
2. Dans la zone de recherche du portail hello, entrez **myResourceGroupA**. Dans les résultats de recherche de hello, cliquez sur **myResourceGroupA**.
3. Sur hello **myResourceGroupA** panneau, cliquez sur hello **supprimer** icône.
4. suppression de hello tooconfirm, Bonjour **hello TYPE nom groupe de ressources** , entrez **myResourceGroupA**, puis cliquez sur **supprimer**.
5. Déconnectez-vous de portail hello en tant que l’UtilisateurA et connectez-vous en tant qu’utilisateur b.
6. Effectuez les étapes 2 à 4 pour myResourceGroupB.

### <a name="delete-cli"></a>Interface CLI Azure

1. Connectez-vous en tooAzure en tant que l’UtilisateurA et exécutez hello de commande suivante :

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```
2. Déconnectez-vous d’Azure en tant que UserA, puis connectez-vous en tant que UserB.
3. Exécutez hello de commande suivante :

    ```azurecli-interactive
    az group delete --name myResourceGroupB --yes
    ```

### <a name="delete-powershell"></a>PowerShell

1. Connectez-vous en tooAzure en tant que l’UtilisateurA et exécutez hello de commande suivante :

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -force
    ```

2. Déconnectez-vous d’Azure en tant que UserA, puis connectez-vous en tant que UserB.
3. Exécutez hello de commande suivante :

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupB -force
    ```

## <a name="next-steps"></a>Étapes suivantes

- Familiarisez-vous bien avec les [comportements et contraintes importants de l’homologation de réseaux virtuels](virtual-network-manage-peering.md#requirements-and-constraints) avant d’en créer une pour une utilisation en production.
- Apprenez-en davantage sur tous les [paramètres d’homologation de réseaux virtuels](virtual-network-manage-peering.md#create-a-peering).
- Découvrez comment trop[créer un hub et spoke topologie de réseau](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) avec le réseau virtuel d’homologation.
