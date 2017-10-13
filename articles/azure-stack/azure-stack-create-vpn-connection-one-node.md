---
title: "Créer une connexion VPN de site à site entre deux réseaux virtuels dans des environnements différents du Kit de développement Azure Stack | Microsoft Docs"
description: "Procédure pas à pas à suivre par un administrateur de cloud souhaitant créer une connexion VPN de site à site entre deux environnements du Kit de développement Azure Stack à nœud unique."
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 3f1b4e02-dbab-46a3-8e11-a777722120ec
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: fa2a940620e06521fa110fa13dcbc3050635a502
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="create-a-site-to-site-vpn-connection-between-two-virtual-networks-in-different-azure-stack-development-kit-environments"></a>Créer une connexion VPN de site à site entre deux réseaux virtuels dans des environnements différents du Kit de développement Azure Stack
## <a name="overview"></a>Vue d'ensemble
Cet article vous explique comment créer une connexion VPN de site à site entre deux réseaux virtuels dans deux environnements distincts du Kit de développement Azure Stack. Pendant la configuration des connexions, vous allez découvrir le fonctionnement des passerelles VPN dans Azure Stack.

### <a name="connection-diagram"></a>Diagramme de connexions
Le diagramme ci-après illustre à quoi la configuration d’une connexion devra ressembler lorsque vous aurez terminé.

![Configuration d’une connexion VPN de site à site](media/azure-stack-create-vpn-connection-one-node-tp2/OneNodeS2SVPN.png)

### <a name="before-you-begin"></a>Avant de commencer
Avant de commencer la configuration de la connexion, vérifiez que vous disposez des éléments suivants :

* Deux serveurs conformes aux exigences matérielles du Kit de développement Azure Stack définies dans [Prérequis pour le déploiement Azure Stack](azure-stack-deploy.md). Vérifiez également qu’ils remplissent tous les autres prérequis indiqués dans cet [article](azure-stack-deploy.md).
* Le package de déploiement du [Kit de développement Azure Stack](https://azure.microsoft.com/en-us/overview/azure-stack/try/).

## <a name="deploy-the-azure-stack-development-kit-environments"></a>Déployer les environnements du Kit de développement Azure Stack
Pour configurer la connexion, vous devez déployer deux environnements du Kit de développement Azure Stack.
> [!NOTE] 
> Suivez les [instructions de déploiement](azure-stack-run-powershell-script.md) pour chaque environnement du Kit de développement Azure Stack à déployer. Dans cet article, les deux environnements du Kit de développement Azure Stack sont appelés *POC1* et *POC2*.


## <a name="prepare-an-offer-on-poc1-and-poc2"></a>Préparer une offre sur POC1 et POC2
Sur POC1 et POC2, préparez une offre à laquelle les utilisateurs peuvent s’abonner pour déployer les machines virtuelles. Pour plus d’informations sur la création d’une offre, consultez [Mettre des machines virtuelles à la disposition de vos utilisateurs Azure Stack](azure-stack-tutorial-tenant-vm.md).

## <a name="review-and-complete-the-network-configuration-table"></a>Vérifier et compléter la table de configuration réseau
La table ci-dessous récapitule la configuration réseau des deux environnements du Kit de développement Azure Stack. Suivez la procédure décrite sous la table pour ajouter l’adresse BGPNAT externe qui est propre à votre réseau.

**Table de configuration réseau**
|   |POC1|POC2|
|---------|---------|---------|
|Nom du réseau virtuel     |VNET-01|VNET-02 |
|Espace d’adressage du réseau virtuel |10.0.10.0/23|10.0.20.0/23|
|Nom du sous-réseau     |Subnet-01|Subnet-02|
|Plage d’adresses de sous-réseau|10.0.10.0/24 |10.0.20.0/24 |
|Sous-réseau de passerelle     |10.0.11.0/24|10.0.21.0/24|
|Adresse BGPNAT externe     |         |         |

> [!NOTE]
> Les adresses IP BGPNAT externes de ces exemples d’environnements sont 10.16.167.195 pour POC1 et 10.16.169.131 pour POC2. Utilisez la procédure ci-après pour obtenir les adresses IP BGPNAT externes des hôtes du Kit de développement Azure Stack, puis ajoutez-les à la table de configuration réseau ci-dessus.


### <a name="get-the-ip-address-of-the-external-adapter-of-the-nat-vm"></a>Obtenir l’adresse IP de la carte externe de la machine virtuelle NAT
1. Connectez-vous à la machine physique Azure Stack pour POC1.
2. Modifiez le code PowerShell ci-dessous pour remplacer votre mot de passe d’administrateur, puis exécutez le code sur l’hôte POC :

   ```powershell
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "AzS-bgpnat01" `
    -Password $Password
   ```
3. Ajoutez l’adresse IP à la table de configuration réseau figurant à la section précédente.

4. Répétez cette procédure pour POC2.

## <a name="create-the-network-resources-in-poc1"></a>Créer les ressources réseau dans POC1
Vous allez maintenant créer les ressources réseau POC1 dont vous avez besoin pour configurer vos passerelles. Les instructions ci-après vous indiquent comment créer les ressources à partir du portail utilisateur. Vous pouvez également créer les ressources à l’aide de code PowerShell.

![Workflow utilisé pour créer des ressources](media/azure-stack-create-vpn-connection-one-node-tp2/image2.png)

### <a name="sign-in-as-a-tenant"></a>Se connecter en tant que locataire
Un administrateur de services fédérés peut se connecter en tant que locataire pour tester les plans, les offres et les abonnements mis à la disposition des locataires. Si vous ne l’avez pas encore fait, [créez un compte de locataire](azure-stack-add-new-user-aad.md) avant de vous connecter.

### <a name="create-the-virtual-network-and-vm-subnet"></a>Créer le réseau virtuel et le sous-réseau de machine virtuelle
1. Utilisez un compte de locataire pour vous connecter au portail utilisateur.
2. Dans le portail utilisateur, sélectionnez **Nouveau**.

    ![Créer un réseau virtuel](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
4. Sélectionnez **Réseau virtuel**.
5. Renseignez les champs **Nom**, **Espace d’adressage**, **Nom de sous-réseau** et **Plage d’adresses de sous-réseau** avec les valeurs qui figurent dans la table de configuration réseau au début de cet article.
6. Le champ **Abonnement** affiche l’abonnement que vous avez créé précédemment.
7. Pour le champ **Groupe de ressources**, créez un groupe de ressources ou, si vous en avez déjà un, sélectionnez **Utiliser l’existant**.
8. Vérifiez l’emplacement par défaut.
9. Sélectionnez **Épingler au tableau de bord**.
10. Sélectionnez **Créer**.

### <a name="create-the-gateway-subnet"></a>Créer le sous-réseau de passerelle
1. Dans le tableau de bord, ouvrez la ressource de réseau virtuel VNET-01 que vous avez déjà créée.
2. Dans le panneau **Paramètres**, sélectionnez **Sous-réseaux**.
3. Pour ajouter un sous-réseau de passerelle au réseau virtuel, sélectionnez **Sous-réseau de passerelle**.
   
    ![Ajouter un sous-réseau de passerelle](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. Par défaut, le nom du sous-réseau est **GatewaySubnet**.
   Les sous-réseaux de passerelle ont une particularité. Pour fonctionner correctement, ils doivent avoir le nom *GatewaySubnet*.
5. Dans **Plage d’adresses**, vérifiez que l’adresse est **10.0.11.0/24**.
6. Sélectionnez **OK** pour créer le sous-réseau de passerelle.

### <a name="create-the-virtual-network-gateway"></a>Créer la passerelle de réseau virtuel
1. Dans le Portail Azure, sélectionnez **Nouveau**. 
2. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
3. Dans la liste des ressources réseau, sélectionnez **Passerelle de réseau virtuel**.
4. Dans le champ **Nom**, entrez **GW1**.
5. Sélectionnez l’élément **Réseau virtuel** pour choisir un réseau virtuel.
   Sélectionnez **VNET-01** dans la liste.
6. Sélectionnez l’élément de menu **Adresse IP publique**. Quand le panneau **Choisir une adresse IP publique** s’affiche, sélectionnez **Créer**.
7. Dans le champ **Nom**, entrez **GW1-PiP**, puis sélectionnez **OK**.
8.  Dans le champ **Type de VPN**, l’élément **Basé sur itinéraires** est sélectionné par défaut.
    Conservez le type de VPN **Basé sur itinéraires**.
9. Vérifiez que l’**abonnement** et l’**emplacement** sont corrects. Vous pouvez épingler la ressource au tableau de bord. Sélectionnez **Créer**.

### <a name="create-the-local-network-gateway"></a>Créer la passerelle de réseau local
L’implémentation d’une *passerelle de réseau local* dans ce déploiement d’évaluation d’Azure Stack est un peu différente dans un déploiement Azure réel.

Dans un déploiement Azure, une passerelle de réseau local représente un appareil physique local (sur le locataire), que vous utilisez pour vous connecter à une passerelle de réseau virtuel dans Azure. Dans ce déploiement d’évaluation d’Azure Stack, les deux extrémités de la connexion sont des passerelles de réseau virtuel.

De façon plus générale, la ressource de passerelle de réseau local représente toujours la passerelle distante située à l’autre extrémité de la connexion. Du fait de la conception même du Kit de développement Azure Stack, vous devez spécifier l’adresse IP de la carte réseau externe sur la machine virtuelle NAT de l’autre Kit de développement Azure Stack comme adresse IP publique de la passerelle de réseau local. Vous devez ensuite créer les mappages NAT appropriés sur la machine virtuelle NAT pour connecter correctement les deux extrémités.


### <a name="create-the-local-network-gateway-resource"></a>Créer la ressource de passerelle de réseau local
1. Connectez-vous à la machine physique Azure Stack pour POC1.
2. Dans le portail utilisateur, sélectionnez **Nouveau**.
3. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
4. Dans la liste des ressources, sélectionnez **Passerelle de réseau local**.
5. Dans le champ **Nom**, entrez **POC2-GW**.
6. Dans le champ **Adresse IP**, entrez l’adresse BGPNAT externe pour POC2. Cette adresse figure dans la table de configuration réseau, plus haut dans cet article.
7. Dans le champ **Espace d’adressage**, entrez **10.0.20.0/23** comme espace d’adressage du réseau virtuel POC2 que vous allez créer par la suite.
8. Vérifiez l’exactitude des valeurs des champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **Créer**.

### <a name="create-the-connection"></a>Créer la connexion
1. Dans le portail utilisateur, sélectionnez **Nouveau**.
2. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
3. Dans la liste des ressources, sélectionnez **Connexion**.
4. Dans le panneau de paramètres **De base**, pour le champ **Type de connexion**, sélectionnez **Site à site (IPSec)**.
5. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
6. Dans le panneau **Paramètres**, sélectionnez **Passerelle de réseau virtuel**, puis **GW1**.
7. Sélectionnez **Passerelle de réseau local**, puis **POC2-GW**.
8. Dans **Nom de la connexion**, entrez **POC1-POC2**.
9. Dans **Clé partagée (PSK)**, entrez **12345**, puis sélectionnez **OK**.
10. Dans le panneau **Résumé**, sélectionnez **OK**.

### <a name="create-a-vm"></a>Créer une machine virtuelle
Pour vous assurer que les données transitent bien par la connexion VPN, vous devez vérifier que les machines virtuelles envoient et reçoivent les données dans chaque Kit de développement Azure Stack. Créez d’abord une machine virtuelle dans POC1, puis ajoutez-la au sous-réseau de machine virtuelle dans votre réseau virtuel.

1. Dans le Portail Azure, sélectionnez **Nouveau**.
2. Accédez à la **Place de marché**, puis sélectionnez **Compute**.
3. Dans la liste des images de machine virtuelle, sélectionnez l’image **Windows Server 2016 Datacenter Evals**.
4. Dans le panneau **Bases**, dans **Nom**, entrez **VM01**.
5. Entrez un nom d’utilisateur et un mot de passe valides. Vous utiliserez ce compte plus tard pour vous connecter à la machine virtuelle que vous créez actuellement.
6. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
7. Dans le panneau **Taille**, sélectionnez une taille de machine virtuelle pour cette instance, puis sélectionnez **Sélectionner**.
8. Dans le panneau **Paramètres**, acceptez les valeurs par défaut. Vérifiez que le réseau virtuel **VNET-01** est sélectionné. Vérifiez que le sous-réseau est défini sur **10.0.10.0/24**. Sélectionnez ensuite **OK**.
9. Dans le panneau **Résumé**, vérifiez les paramètres, puis sélectionnez **OK**.



## <a name="create-the-network-resources-in-poc2"></a>Créer les ressources réseau dans POC2

L’étape suivante consiste à créer les ressources réseau pour POC2. Les instructions ci-après vous indiquent comment créer les ressources à partir du portail utilisateur.

### <a name="sign-in-as-a-tenant"></a>Se connecter en tant que locataire
Un administrateur de services fédérés peut se connecter en tant que locataire pour tester les plans, les offres et les abonnements mis à la disposition des locataires. Si vous ne l’avez pas encore fait, [créez un compte de locataire](azure-stack-add-new-user-aad.md) avant de vous connecter.

### <a name="create-the-virtual-network-and-vm-subnet"></a>Créer le réseau virtuel et le sous-réseau de machine virtuelle

1. Connectez-vous en utilisant un compte de locataire.
2. Dans le portail utilisateur, sélectionnez **Nouveau**.
3. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
4. Sélectionnez **Réseau virtuel**.
5. À l’aide des informations données dans la table de configuration réseau, plus haut dans cet article, renseignez les champs **Nom**, **Espace d’adressage**, **Nom de sous-réseau** et **Plage d’adresses de sous-réseau** de manière appropriée pour POC2.
6. Le champ **Abonnement** affiche l’abonnement que vous avez créé précédemment.
7. Pour le champ **Groupe de ressources**, créez un groupe de ressources ou, si vous en avez déjà un, sélectionnez **Utiliser l’existant**.
8. Vérifiez l’**emplacement** par défaut.
9. Sélectionnez **Épingler au tableau de bord**.
10. Sélectionnez **Créer**.

### <a name="create-the-gateway-subnet"></a>Créer le sous-réseau de passerelle
1. Ouvrez la ressource de réseau virtuel que vous avez créée (**VNET-02**) à partir du tableau de bord.
2. Dans le panneau **Paramètres**, sélectionnez **Sous-réseaux**.
3. Sélectionnez **Sous-réseau de passerelle** pour ajouter un sous-réseau de passerelle au réseau virtuel.
4. Par défaut, le nom du sous-réseau est défini sur **GatewaySubnet**.
   Les sous-réseaux de passerelle sont des éléments spéciaux et doivent porter ce nom pour fonctionner correctement.
5. Dans le champ **Plage d’adresses**, vérifiez que l’adresse est **10.0.21.0/24**.
6. Sélectionnez **OK** pour créer le sous-réseau de passerelle.

### <a name="create-the-virtual-network-gateway"></a>Créer la passerelle de réseau virtuel
1. Dans le Portail Azure, sélectionnez **Nouveau**.  
2. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
3. Dans la liste des ressources réseau, sélectionnez **Passerelle de réseau virtuel**.
4. Dans le champ **Nom**, entrez **GW2**.
5. Pour choisir un réseau virtuel, sélectionnez **Réseau virtuel**. Sélectionnez ensuite **VNET-02** dans la liste.
6. Sélectionnez **Adresse IP publique**. Quand le panneau **Choisir une adresse IP publique** s’affiche, sélectionnez **Créer**.
7. Dans le champ **Nom**, entrez **GW2-PiP**, puis sélectionnez **OK**.
8. Dans le champ **Type de VPN**, l’élément **Basé sur itinéraires** est sélectionné par défaut.
    Conservez le type de VPN **Basé sur itinéraires**.
9. Vérifiez que l’**abonnement** et l’**emplacement** sont corrects. Vous pouvez épingler la ressource au tableau de bord. Sélectionnez **Créer**.

### <a name="create-the-local-network-gateway-resource"></a>Créer la ressource de passerelle de réseau local

1. Dans le portail utilisateur POC2, sélectionnez **Nouveau**. 
4. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
5. Dans la liste des ressources, sélectionnez **Passerelle de réseau local**.
6. Dans le champ **Nom**, entrez **POC1-GW**.
7. Dans **Adresse IP**, entrez l’adresse BGPNAT externe pour POC1, qui est indiquée plus haut dans la table de configuration réseau.
8. Dans **Espace d’adressage**, à partir de POC1, entrez l’espace d’adressage **10.0.10.0/23** du réseau virtuel **VNET-01**.
9. Vérifiez l’exactitude des valeurs des champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **Créer**.

## <a name="create-the-connection"></a>Créer la connexion
1. Dans le portail utilisateur, sélectionnez **Nouveau**. 
2. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
3. Dans la liste des ressources, sélectionnez **Connexion**.
4. Dans le panneau de paramètres **De base**, pour le champ **Type de connexion**, choisissez **Site à site (IPSec)**.
5. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
6. Dans le panneau **Paramètres**, sélectionnez **Passerelle de réseau virtuel**, puis **GW2**.
7. Sélectionnez **Passerelle de réseau local**, puis **POC1-GW**.
8. Dans **Nom de la connexion**, entrez **POC2-POC1**.
9. Dans **Clé partagée (PSK)**, entrez **12345**. Si vous choisissez une autre valeur, n’oubliez pas qu’elle *doit* correspondre à la valeur de la clé partagée que vous avez créée dans POC1. Sélectionnez **OK**.
10. Dans le panneau **Résumé**, vérifiez les paramètres, puis sélectionnez **OK**.

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle
Créez d’abord une machine virtuelle dans POC2, puis ajoutez-la au sous-réseau de machine virtuelle dans votre réseau virtuel.

1. Dans le Portail Azure, sélectionnez **Nouveau**.
2. Accédez à la **Place de marché**, puis sélectionnez **Compute**.
3. Dans la liste des images de machine virtuelle, sélectionnez l’image **Windows Server 2016 Datacenter Evals**.
4. Dans le panneau **De base**, dans **Nom**, entrez **VM02**.
5. Entrez un nom d’utilisateur et un mot de passe valides. Vous utiliserez ce compte plus tard pour vous connecter à la machine virtuelle que vous créez actuellement.
6. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
7. Dans le panneau **Taille**, sélectionnez une taille de machine virtuelle pour cette instance, puis sélectionnez **Sélectionner**.
8. Dans le panneau **Paramètres**, acceptez les valeurs par défaut. Vérifiez que le réseau virtuel **VNET-02** est sélectionné et que le sous-réseau est défini sur **10.0.20.0/24**. Sélectionnez **OK**.
9. Dans le panneau **Résumé**, vérifiez les paramètres, puis sélectionnez **OK**.

## <a name="configure-the-nat-virtual-machine-on-each-azure-stack-development-kit-for-gateway-traversal"></a>Configurer la machine virtuelle NAT sur chaque Kit de développement Azure Stack pour la traversée de passerelle
Étant donné que le Kit de développement Azure Stack a été conçu pour être autonome et isolé du réseau sur lequel l’hôte physique est déployé, le réseau VIP *externe* auquel les passerelles sont connectées n’est pas réellement externe. En fait, le réseau VIP est masqué derrière un routeur qui effectue la traduction d’adresses réseau (NAT). 

Le routeur est une machine virtuelle Windows Server, appelée *AzS-bgpnat01*, qui a le rôle RRAS (Routing and Remote Access Services) dans l’infrastructure du Kit de développement Azure Stack. Vous devez configurer NAT sur la machine virtuelle AzS-bgpnat01 pour permettre à la connexion VPN de site à site de se connecter aux deux extrémités. 

Pour configurer la connexion VPN, créez un routage de mappage NAT statique qui mappe l’interface externe sur la machine virtuelle BGPNAT à l’adresse IP virtuelle du pool de passerelles Edge. Un routage de mappage NAT statique est nécessaire pour chaque port utilisé dans une connexion VPN.

> [!NOTE]
> Cette configuration est requise uniquement pour les environnements du Kit de développement Azure Stack.
> 
> 

### <a name="configure-the-nat"></a>Configurer NAT
> [!IMPORTANT]
> Vous devez effectuer cette procédure pour *les deux* environnements du Kit de développement Azure Stack.

1. Déterminez quelle **adresse IP interne** utiliser dans le script PowerShell suivant. Ouvrez la passerelle de réseau virtuel (GW1 et GW2) et, dans le panneau **Vue d’ensemble**, enregistrez la valeur du champ **Adresse IP publique** pour l’utiliser plus tard.
![Adresse IP interne](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)
2. Connectez-vous à la machine physique Azure Stack pour POC1.
3. Copiez et modifiez le script PowerShell suivant. Pour configurer NAT sur chaque Kit de développement Azure Stack, exécutez le script dans une fenêtre Windows PowerShell ISE avec des privilèges élevés. Dans le script, entrez les valeurs appropriées dans les espaces réservés *Adresse BGPNAT externe* et *Adresse IP interne* :

   ```powershell
   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping to map the external address to the Gateway
   # Public IP Address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish the complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

4. Répétez cette procédure pour POC2.

## <a name="test-the-connection"></a>Tester la connexion
Vous avez établi la connexion de site à site. Vous devez maintenant vérifier que le trafic transite bien par cette connexion. Pour cela, connectez-vous à l’une des machines virtuelles que vous avez créées dans l’un des environnements du Kit de développement Azure Stack. Ensuite, effectuez un test ping sur la machine virtuelle que vous avez créée dans l’autre environnement. 

Pour vérifier que le trafic envoyé passe par la connexion de site à site, vous devez effectuer le test ping sur l’adresse IP directe (DIP) de la machine virtuelle du sous-réseau distant, et non sur l’adresse IP virtuelle. Pour cela, recherchez l’adresse DIP à l’autre extrémité de la connexion. Enregistrez l’adresse pour l’utiliser plus tard.

### <a name="sign-in-to-the-tenant-vm-in-poc1"></a>Se connecter à la machine virtuelle locataire dans POC1
1. Connectez-vous à la machine physique Azure Stack pour POC1, puis connectez-vous au portail utilisateur à l’aide d’un compte de locataire.
2. Dans la barre de navigation de gauche, sélectionnez **Compute**.
3. Dans la liste des machines virtuelles, recherchez la machine virtuelle **VM01** que vous avez créée précédemment et sélectionnez-la.
4. Dans le panneau de la machine virtuelle, cliquez sur **Se connecter**, puis ouvrez le fichier VM01.rdp.
   
     ![Bouton Se connecter](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. Connectez-vous avec le compte que vous avez configuré pendant la création de la machine virtuelle.
6. Ouvrez une fenêtre **Windows PowerShell** avec des privilèges élevés.
7. Entrez **ipconfig /all**.
8. Dans la sortie, recherchez la valeur **Adresse IPv4**, puis enregistrez l’adresse pour l’utiliser plus tard. Il s’agit de l’adresse sur laquelle vous allez effectuer un test ping à partir de POC2. Dans l’exemple d’environnement, l’adresse est **10.0.10.4**, mais peut être différente dans votre environnement. Elle doit faire partie du sous-réseau **10.0.10.0/24** que vous avez créé précédemment.
9. Pour créer une règle de pare-feu qui autorise la machine virtuelle à répondre aux tests ping, exécutez la commande PowerShell suivante :

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-to-the-tenant-vm-in-poc2"></a>Se connecter à la machine virtuelle locataire dans POC2
1. Connectez-vous à la machine physique Azure Stack pour POC2, puis connectez-vous au portail utilisateur à l’aide d’un compte de locataire.
2. Dans la barre de navigation de gauche, cliquez sur **Compute**.
3. Dans la liste des machines virtuelles, recherchez la machine virtuelle **VM02** que vous avez créée précédemment et sélectionnez-la.
4. Dans le panneau de la machine virtuelle, cliquez sur **Se connecter**.
5. Connectez-vous avec le compte que vous avez configuré pendant la création de la machine virtuelle.
6. Ouvrez une fenêtre **Windows PowerShell** avec des privilèges élevés.
7. Entrez **ipconfig /all**.
8. Vous devez normalement voir une adresse IPv4 qui fait partie du sous-réseau **10.0.20.0/24**. Dans l’exemple d’environnement, l’adresse est **10.0.20.4**, mais votre adresse peut être différente.
9. Pour créer une règle de pare-feu qui autorise la machine virtuelle à répondre aux tests ping, exécutez la commande PowerShell suivante :

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. À partir de la machine virtuelle dans POC2, effectuez un test ping sur la machine virtuelle dans POC1, par le biais du tunneling. Pour cela, effectuez un test ping sur l’adresse IP directe (DIP) que vous avez enregistrée à partir de VM01.
   Dans l’exemple d’environnement, l’adresse est **10.0.10.4**, mais vous devez effectuer le test ping sur l’adresse que vous avez notée dans votre lab. Vous devez obtenir un résultat similaire à la sortie suivante :
   
    ![Test ping réussi](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. La réception d’une réponse de la machine virtuelle distante indique que le test a réussi ! Vous pouvez fermer la fenêtre de la machine virtuelle. Pour tester votre connexion, vous pouvez essayer d’autres types de transferts de données, par exemple, une copie de fichier.

### <a name="viewing-data-transfer-statistics-through-the-gateway-connection"></a>Affichage des statistiques de transfert de données via la connexion de passerelle
Si vous souhaitez connaître la quantité de données qui transite par votre connexion de site à site, consultez cette information dans le panneau **Connexion**. Ce test est également un autre moyen de vérifier que la commande ping que vous venez d’envoyer est bien passée par la connexion VPN.

1. Quand vous êtes connecté à la machine virtuelle locataire dans POC2, utilisez votre compte de locataire pour vous connecter au portail utilisateur.
2. Accédez à **Toutes les ressources**, puis sélectionnez la connexion **POC2-POC1**. Le panneau **Connexion** s’affiche.
4. Le panneau **Connexion** affiche les statistiques **Données entrantes** et **Données sortantes**. Dans la capture d’écran suivante, les valeurs élevées sont dues au transfert de fichiers supplémentaires. Normalement, vous ne devez pas voir de valeurs nulles ici.
   
    ![Données entrantes et sortantes](media/azure-stack-create-vpn-connection-one-node-tp2/image20.png)
