---
title: "aaaCreate une connexion VPN de site à site entre deux réseaux virtuels dans différents environnements du Kit de développement de pile Azure | Documents Microsoft"
description: "Procédure pas à pas qu’un administrateur de cloud utilise le réseau toocreate un site à site VPN entre les deux environnements de Kit de développement Azure pile à nœud unique."
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
ms.openlocfilehash: 74225a82efae7d9ca6dc08b45ff04c578fae785c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-vpn-connection-between-two-virtual-networks-in-different-azure-stack-development-kit-environments"></a>Créer une connexion VPN de site à site entre deux réseaux virtuels dans des environnements différents du Kit de développement Azure Stack
## <a name="overview"></a>Vue d'ensemble
Cet article vous montre comment toocreate une connexion VPN de site à site entre deux réseaux virtuels dans deux environnements de Kit de développement de pile Azure distincts. Lorsque vous configurez des connexions de hello, vous allez apprendre comment fonctionnent les passerelles VPN dans la pile de Azure.

### <a name="connection-diagram"></a>Diagramme de connexions
diagramme qui suit de Hello montre quelle configuration de connexion hello doit ressembler à la fois.

![Configuration d’une connexion VPN de site à site](media/azure-stack-create-vpn-connection-one-node-tp2/OneNodeS2SVPN.png)

### <a name="before-you-begin"></a>Avant de commencer
configuration de la connexion toocomplete hello, assurez-vous d’avoir hello suivant d’éléments avant de commencer :

* Deux serveurs qui répondent aux exigences de matériel Kit de développement de pile Azure hello, qui sont définis par hello [conditions préalables au déploiement de Azure pile](azure-stack-deploy.md). Vérifiez que hello autres conditions préalables qui s’affichent dans hello [article](azure-stack-deploy.md) sont remplies en trop.
* Hello [Kit de développement Azure pile](https://azure.microsoft.com/en-us/overview/azure-stack/try/) package de déploiement.

## <a name="deploy-hello-azure-stack-development-kit-environments"></a>Déployer des environnements de Kit de développement de pile Azure hello
configuration de la connexion toocomplete hello, vous devez déployer les deux environnements de Kit de développement de pile Azure.
> [!NOTE] 
> Pour chaque Kit de développement de pile Azure que vous déployez, suivez hello [des instructions de déploiement](azure-stack-run-powershell-script.md). Dans cet article, les environnements de Kit de développement de pile Azure hello sont appelés *POC1* et *POC2*.


## <a name="prepare-an-offer-on-poc1-and-poc2"></a>Préparer une offre sur POC1 et POC2
Sur POC1 et POC2, préparez une offre afin qu’un utilisateur peut s’abonner toohello offre et déployer des ordinateurs virtuels de hello. Pour plus d’informations sur la façon de toocreate une offre, consultez [rendre tooyour disponible des ordinateurs virtuels aux utilisateurs d’Azure pile](azure-stack-tutorial-tenant-vm.md).

## <a name="review-and-complete-hello-network-configuration-table"></a>Révision et la table de configuration de réseau hello terminée
Hello tableau suivant récapitule la configuration du réseau pour les deux environnements de Kit de développement de pile Azure hello. Utilisez la procédure hello apparaît après hello tooadd de table hello adresse BGPNAT externe qui est spécifique à votre réseau.

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
> Hello BGPNAT des adresses IP externes dans l’environnement de l’exemple hello sont 10.16.167.195 pour POC1 et 10.16.169.131 pour POC2. Utilisez hello suivant la procédure toodetermine hello BGPNAT les adresses IP externes pour vos hôtes de Kit de développement de pile Azure et les ajouter la table de configuration réseau toohello précédente.


### <a name="get-hello-ip-address-of-hello-external-adapter-of-hello-nat-vm"></a>Obtenir l’adresse IP de hello de hello de carte externe hello NAT VM
1. Ouvrez une session toohello machine physique de pile de Azure pour POC1.
2. Modifiez hello suivant tooreplace de code Powershell votre mot de passe administrateur et puis exécutez le code de hello sur l’ordinateur hôte de preuve de concept hello :

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
3. Ajoutez hello toohello réseau configuration table d’adresses IP qui s’affiche dans la section précédente de hello.

4. Répétez cette procédure pour POC2.

## <a name="create-hello-network-resources-in-poc1"></a>Créer des ressources réseau hello dans POC1
Vous créez maintenant hello POC1 ressources de réseau que vous avez besoin tooset vos passerelles. Hello, suivant les instructions vous indiquent comment les ressources de hello toocreate à l’aide de hello portail de l’utilisateur. Vous pouvez également utiliser les ressources de PowerShell code toocreate hello.

![Flux de travail utilisés toocreate ressources](media/azure-stack-create-vpn-connection-one-node-tp2/image2.png)

### <a name="sign-in-as-a-tenant"></a>Se connecter en tant que locataire
Un administrateur de service peut se connecter en tant qu’un tootest client hello des plans, des offres et des abonnements susceptibles d’utiliser leurs clients. Si vous ne l’avez pas encore fait, [créez un compte de locataire](azure-stack-add-new-user-aad.md) avant de vous connecter.

### <a name="create-hello-virtual-network-and-vm-subnet"></a>Créer le réseau virtuel de hello et le sous-réseau d’ordinateurs virtuels
1. Utilisez un toosign de compte du client dans le portail de l’utilisateur toohello.
2. Dans le portail de l’utilisateur hello, sélectionnez **nouveau**.

    ![Créer un réseau virtuel](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. Accédez trop**Marketplace**, puis sélectionnez **réseau**.
4. Sélectionnez **Réseau virtuel**.
5. Pour **nom**, **l’espace d’adressage**, **nom du sous-réseau**, et **plage d’adresses de sous-réseau**, utiliser des valeurs hello qui apparaissent plus tôt dans hello réseau table de configuration.
6. Dans **abonnement**, abonnement hello que vous avez créé précédemment s’affiche.
7. Pour le champ **Groupe de ressources**, créez un groupe de ressources ou, si vous en avez déjà un, sélectionnez **Utiliser l’existant**.
8. Vérifiez l’emplacement par défaut de hello.
9. Sélectionnez **toodashboard du code confidentiel**.
10. Sélectionnez **Créer**.

### <a name="create-hello-gateway-subnet"></a>Créez le sous-réseau de passerelle hello
1. Sur le tableau de bord hello, ouvrez les ressources réseau virtuel hello-01 du réseau virtuel que vous avez créé précédemment.
2. Sur hello **paramètres** panneau, sélectionnez **sous-réseaux**.
3. tooadd un sous-réseau de passerelle pour réseau virtuel de hello, sélectionnez **sous-réseau de passerelle**.
   
    ![Ajouter un sous-réseau de passerelle](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. Par défaut, le nom du sous-réseau hello est défini trop**GatewaySubnet**.
   Les sous-réseaux de passerelle ont une particularité. toofunction correctement, ils doivent utiliser hello *GatewaySubnet* nom.
5. Dans **plage d’adresses**, vérifiez l’adresse hello **10.0.11.0/24**.
6. Sélectionnez **OK** sous-réseau de passerelle toocreate hello.

### <a name="create-hello-virtual-network-gateway"></a>Créer une passerelle de réseau virtuel hello
1. Bonjour portail Azure, sélectionnez **nouveau**. 
2. Accédez trop**Marketplace**, puis sélectionnez **réseau**.
3. Dans la liste hello des ressources réseau, sélectionnez **passerelle de réseau virtuel**.
4. Dans le champ **Nom**, entrez **GW1**.
5. Sélectionnez hello **réseau virtuel** élément toochoose un réseau virtuel.
   Sélectionnez **réseau virtuel-01** à partir de la liste de hello.
6. Sélectionnez hello **adresse IP publique** élément de menu. Hello lorsque **choisir une adresse IP publique** panneau s’ouvre, sélectionnez **nouvel**.
7. Dans le champ **Nom**, entrez **GW1-PiP**, puis sélectionnez **OK**.
8.  Dans le champ **Type de VPN**, l’élément **Basé sur itinéraires** est sélectionné par défaut.
    Conserver hello **basée sur un itinéraire** type de VPN.
9. Vérifiez que l’**abonnement** et l’**emplacement** sont corrects. Vous pouvez épingler le tableau de bord toohello de ressources hello. Sélectionnez **Créer**.

### <a name="create-hello-local-network-gateway"></a>Créer une passerelle de réseau local hello
Hello d’implémentation d’un *passerelle de réseau local* dans cette pile Azure déploiement d’évaluation est un peu différente de celle dans un déploiement d’Azure réel.

Dans un déploiement d’Azure, une passerelle de réseau local représente une unité physique local (au locataire de hello), que vous utilisez passerelle de réseau virtuel tooconnect tooa dans Azure. Dans ce déploiement d’évaluation de la pile d’Azure, les deux extrémités de la connexion de hello sont des passerelles de réseau virtuel !

Un toothink de façon à ce sujet est plus générique que ressources de passerelle de réseau local hello indique toujours passerelle à distance de hello en hello à autre extrémité de la connexion de hello. En raison de hello de façon hello que Kit de développement de pile Azure a été conçu, vous avez besoin tooprovide hello adresse IP de carte réseau externe hello traduction d’adresses réseau hello (NAT) VM de hello autres Azure pile Kit de développement comme hello adresse IP publique de hello passerelle de réseau local. Vous créez ensuite des mappages NAT sur hello toomake NAT VM assurer que les deux extrémités sont correctement connectées.


### <a name="create-hello-local-network-gateway-resource"></a>Créer des ressources de passerelle de réseau local hello
1. Ouvrez une session toohello machine physique de pile de Azure pour POC1.
2. Dans le portail de l’utilisateur hello, sélectionnez **nouveau**.
3. Accédez trop**Marketplace**, puis sélectionnez **réseau**.
4. Dans la liste hello des ressources, sélectionnez **passerelle de réseau local**.
5. Dans le champ **Nom**, entrez **POC2-GW**.
6. Dans **adresse IP**, entrez hello externe BGPNAT adresse POC2. Cette adresse s’affiche plus haut dans la table de configuration de réseau hello.
7. Dans **espace d’adressage**, pour l’espace d’adressage hello Hello réseau virtuel POC2 que vous créerez ultérieurement, entrez **10.0.20.0/23**.
8. Vérifiez l’exactitude des valeurs des champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **Créer**.

### <a name="create-hello-connection"></a>Créer la connexion de hello
1. Dans le portail de l’utilisateur hello, sélectionnez **nouveau**.
2. Accédez trop**Marketplace**, puis sélectionnez **réseau**.
3. Dans la liste hello des ressources, sélectionnez **connexion**.
4. Sur hello **notions de base** Panneau de paramètres, pourquoi **type de connexion**, sélectionnez **Site à site (IPSec)**.
5. Sélectionnez hello **abonnement**, **groupe de ressources**, et **emplacement**, puis sélectionnez **OK**.
6. Sur hello **paramètres** panneau, sélectionnez **passerelle de réseau virtuel**, puis sélectionnez **GW1**.
7. Sélectionnez **Passerelle de réseau local**, puis **POC2-GW**.
8. Dans **Nom de la connexion**, entrez **POC1-POC2**.
9. Dans **Clé partagée (PSK)**, entrez **12345**, puis sélectionnez **OK**.
10. Sur hello **Résumé** panneau, sélectionnez **OK**.

### <a name="create-a-vm"></a>Créer une machine virtuelle
données hello toovalidate qui passent à travers hello connexion VPN, vous devez hello toosend de machines virtuelles et de recevoir des données dans le Kit de développement de chaque pile de Azure. Créez d’abord une machine virtuelle dans POC1, puis ajoutez-la au sous-réseau de machine virtuelle dans votre réseau virtuel.

1. Bonjour portail Azure, sélectionnez **nouveau**.
2. Accédez trop**Marketplace**, puis sélectionnez **de calcul**.
3. Dans la liste de hello des images de machine virtuelle, sélectionnez hello **Eval de centre de données de Windows Server 2016** image.
4. Sur hello **notions de base** panneau, dans **nom**, entrez **VM01**.
5. Entrez un nom d’utilisateur et un mot de passe valides. Vous utilisez cette toosign de compte dans toohello machine virtuelle après sa création.
6. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
7. Sur hello **taille** panneau, pour cette instance, sélectionnez une taille de machine virtuelle, puis **sélectionnez**.
8. Sur hello **paramètres** panneau, acceptez les valeurs par défaut hello. Vérifiez que hello **réseau virtuel-01** réseau virtuel est sélectionné. Vérifiez que le sous-réseau hello est défini trop**10.0.10.0/24**. Sélectionnez ensuite **OK**.
9. Sur hello **Résumé** panneau, passez en revue les paramètres de hello, puis sélectionnez **OK**.



## <a name="create-hello-network-resources-in-poc2"></a>Créer des ressources réseau hello dans POC2

étape suivante de Hello est ressources du réseau toocreate hello pour POC2. Hello suivant instructions indiquent comment les ressources de hello toocreate à l’aide de hello portail de l’utilisateur.

### <a name="sign-in-as-a-tenant"></a>Se connecter en tant que locataire
Un administrateur de service peut se connecter en tant qu’un tootest client hello des plans, des offres et des abonnements susceptibles d’utiliser leurs clients. Si vous ne l’avez pas encore fait, [créez un compte de locataire](azure-stack-add-new-user-aad.md) avant de vous connecter.

### <a name="create-hello-virtual-network-and-vm-subnet"></a>Créer le réseau virtuel de hello et le sous-réseau d’ordinateurs virtuels

1. Connectez-vous en utilisant un compte de locataire.
2. Dans le portail de l’utilisateur hello, sélectionnez **nouveau**.
3. Accédez trop**Marketplace**, puis sélectionnez **réseau**.
4. Sélectionnez **Réseau virtuel**.
5. Utilisez les informations de hello plus haut dans les valeurs hello hello réseau configuration table tooidentify pour hello POC2 **nom**, **l’espace d’adressage**, **nom du sous-réseau**et  **Plage d’adresses de sous-réseau**.
6. Dans **abonnement**, abonnement hello que vous avez créé précédemment s’affiche.
7. Pour le champ **Groupe de ressources**, créez un groupe de ressources ou, si vous en avez déjà un, sélectionnez **Utiliser l’existant**.
8. Vérifiez la valeur par défaut hello **emplacement**.
9. Sélectionnez **toodashboard du code confidentiel**.
10. Sélectionnez **Créer**.

### <a name="create-hello-gateway-subnet"></a>Créer hello sous-réseau de passerelle
1. Ouvrir la ressource de réseau virtuel hello vous avez créé (**réseau virtuel-02**) à partir du tableau de bord hello.
2. Sur hello **paramètres** panneau, sélectionnez **sous-réseaux**.
3. Sélectionnez **sous-réseau de passerelle** tooadd un sous-réseau de passerelle pour réseau virtuel de hello.
4. nom Hello du sous-réseau de hello est défini trop**GatewaySubnet** par défaut.
   Les sous-réseaux de passerelle sont spéciales et doivent avoir cette toofunction nom spécifique correctement.
5. Bonjour **plage d’adresses** champ, vérifiez l’adresse hello **10.0.21.0/24**.
6. Sélectionnez **OK** sous-réseau de passerelle toocreate hello.

### <a name="create-hello-virtual-network-gateway"></a>Créer une passerelle de réseau virtuel hello
1. Bonjour portail Azure, sélectionnez **nouveau**.  
2. Accédez trop**Marketplace**, puis sélectionnez **réseau**.
3. Dans la liste hello des ressources réseau, sélectionnez **passerelle de réseau virtuel**.
4. Dans le champ **Nom**, entrez **GW2**.
5. toochoose un réseau virtuel, sélectionnez **réseau virtuel**. Puis sélectionnez **réseau virtuel-02** à partir de la liste de hello.
6. Sélectionnez **Adresse IP publique**. Hello lorsque **choisir une adresse IP publique** panneau s’ouvre, sélectionnez **nouvel**.
7. Dans le champ **Nom**, entrez **GW2-PiP**, puis sélectionnez **OK**.
8. Dans le champ **Type de VPN**, l’élément **Basé sur itinéraires** est sélectionné par défaut.
    Conserver hello **basée sur un itinéraire** type de VPN.
9. Vérifiez que l’**abonnement** et l’**emplacement** sont corrects. Vous pouvez épingler le tableau de bord toohello de ressources hello. Sélectionnez **Créer**.

### <a name="create-hello-local-network-gateway-resource"></a>Créer des ressources de passerelle de réseau local hello

1. Dans le portail de l’utilisateur hello POC2, sélectionnez **nouveau**. 
4. Accédez trop**Marketplace**, puis sélectionnez **réseau**.
5. Dans la liste hello des ressources, sélectionnez **passerelle de réseau Local**.
6. Dans le champ **Nom**, entrez **POC1-GW**.
7. Dans **adresse IP**, entrez hello externe BGPNAT adresse POC1 répertorié plus haut dans la table de configuration de réseau hello.
8. Dans **espace d’adressage**, à partir de POC1, entrez hello **10.0.10.0/23** espace d’adressage de **-01 du réseau virtuel**.
9. Vérifiez l’exactitude des valeurs des champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **Créer**.

## <a name="create-hello-connection"></a>Créer la connexion de hello
1. Dans le portail de l’utilisateur hello, sélectionnez **nouveau**. 
2. Accédez trop**Marketplace**, puis sélectionnez **réseau**.
3. Dans la liste hello des ressources, sélectionnez **connexion**.
4. Sur hello **base** Panneau de paramètres, pourquoi **type de connexion**, choisissez **Site à site (IPSec)**.
5. Sélectionnez hello **abonnement**, **groupe de ressources**, et **emplacement**, puis sélectionnez **OK**.
6. Sur hello **paramètres** panneau, sélectionnez **passerelle de réseau virtuel**, puis sélectionnez **cassettes numériques GW2**.
7. Sélectionnez **Passerelle de réseau local**, puis **POC1-GW**.
8. Dans **Nom de la connexion**, entrez **POC2-POC1**.
9. Dans **Clé partagée (PSK)**, entrez **12345**. Si vous choisissez une autre valeur, n’oubliez pas qu’il *doit* correspond à la valeur hello pour la clé partagée hello que vous avez créé sur POC1. Sélectionnez **OK**.
10. Hello de révision **Résumé** panneau, puis sélectionnez **OK**.

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle
Créez d’abord une machine virtuelle dans POC2, puis ajoutez-la au sous-réseau de machine virtuelle dans votre réseau virtuel.

1. Bonjour portail Azure, sélectionnez **nouveau**.
2. Accédez trop**Marketplace**, puis sélectionnez **de calcul**.
3. Dans la liste de hello des images de machine virtuelle, sélectionnez hello **Eval de centre de données de Windows Server 2016** image.
4. Sur hello **notions de base** panneau, pour **nom**, entrez **VM02**.
5. Entrez un nom d’utilisateur et un mot de passe valides. Vous utilisez cette toosign de compte dans la machine virtuelle de toohello après sa création.
6. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
7. Sur hello **taille** panneau, sélectionnez un ordinateur virtuel de taille pour cette instance, puis **sélectionnez**.
8. Sur hello **paramètres** panneau, vous pouvez accepter les valeurs par défaut hello. Vérifiez que hello **réseau virtuel-02** réseau virtuel est sélectionné et vérifiez que le sous-réseau hello est défini trop**10.0.20.0/24**. Sélectionnez **OK**.
9. Passez en revue les paramètres hello sur hello **Résumé** panneau, puis sélectionnez **OK**.

## <a name="configure-hello-nat-virtual-machine-on-each-azure-stack-development-kit-for-gateway-traversal"></a>Configurer un ordinateur virtuel hello NAT sur chaque Kit de développement de pile Azure pour le parcours de la passerelle
Hello Kit de développement Azure pile étant autonome et isolé du réseau sur le hello hôte physique est déployé, hello *externe* réseau adresse IP virtuelle que les passerelles de hello sont connectés toois pas réellement externe. Au lieu de cela, le réseau d’adresses IP virtuelles hello est masquée derrière un routeur qui effectue la traduction d’adresses réseau. 

Le routeur est un ordinateur virtuel Windows Server, appelé *AzS-bgpnat01*, qui exécute le service de routage et le rôle Services d’accès distant (RRAS) dans hello infrastructure du Kit de développement Azure pile. Vous devez configurer NAT sur hello AzS-bgpnat01 machine virtuelle tooallow hello site-à-site VPN connexion tooconnect aux deux extrémités. 

connexion VPN de hello tooconfigure, vous devez créer un itinéraire de mappage NAT statique qui mappe l’interface externe hello hello BGPNAT machine virtuelle toohello VIP de hello Pool de passerelle de périphérie. Un routage de mappage NAT statique est nécessaire pour chaque port utilisé dans une connexion VPN.

> [!NOTE]
> Cette configuration est requise uniquement pour les environnements du Kit de développement Azure Stack.
> 
> 

### <a name="configure-hello-nat"></a>Configurer hello NAT
> [!IMPORTANT]
> Vous devez effectuer cette procédure pour *les deux* environnements du Kit de développement Azure Stack.

1. Déterminer hello **adresse IP interne** toouse Bonjour suite du script PowerShell. Passerelle de réseau virtuel hello Open (GW1 et cassettes numériques GW2), puis sous hello **vue d’ensemble** panneau, enregistrez la valeur hello pour hello **adresse IP publique** pour une utilisation ultérieure.
![Adresse IP interne](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)
2. Ouvrez une session toohello machine physique de pile de Azure pour POC1.
3. Copiez et modifiez hello suite du script PowerShell. tooconfigure hello NAT sur chaque Kit de développement de la pile de Azure, exécuter un script de hello dans un Windows PowerShell ISE avec élévation de privilèges. Dans le script de hello, ajouter des valeurs toohello *les adresses externes BGPNAT* et *adresse IP interne* des espaces réservés :

   ```powershell
   # Designate hello external NAT address for hello ports that use hello IKE authentication.
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
   # create a static NAT mapping toomap hello external address toohello Gateway
   # Public IP Address toomap hello ISAKMP port 500 for PHASE 1 of hello IPSEC tunnel
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
   # successfully establish hello complete IPSEC tunnel over NAT devices
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

## <a name="test-hello-connection"></a>Tester la connexion hello
Maintenant que la connexion de site à site hello est établie, vous devez valider que vous pouvez obtenir le trafic passant par son biais. toovalidate, tooone d’ordinateurs virtuels hello que vous avez créé dans un environnement du Kit de développement Azure pile de connexion. Ensuite, la machine virtuelle ping hello que vous avez créé dans hello autre environnement. 

tooensure qui permet d’envoyer le trafic de hello via la connexion de site à site hello, assurez-vous que vous ping adresse IP directe (DIP) de hello de machine virtuelle de hello sur un sous-réseau distant hello, pas les adresses IP virtuelles hello. toodo cela, rechercher hello DIP adresse sur hello l’autre extrémité de la connexion de hello. Enregistrez l’adresse hello pour une utilisation ultérieure.

### <a name="sign-in-toohello-tenant-vm-in-poc1"></a>Connectez-vous à toohello locataire machine virtuelle dans POC1
1. Connectez-vous à l’ordinateur physique toohello Azure pile pour POC1 et ensuite utiliser un toosign de compte du client dans le portail de l’utilisateur toohello.
2. Dans la barre de navigation gauche hello, sélectionnez **de calcul**.
3. Dans la liste hello des machines virtuelles, recherchez **VM01** créé précédemment, puis sélectionnez-le.
4. Dans le panneau hello pour la machine virtuelle de hello, cliquez sur **connexion**, puis ouvrez le fichier de VM01.rdp hello.
   
     ![Bouton Se connecter](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. Connectez-vous avec hello compte que vous avez configuré lors de la création de la machine virtuelle de hello.
6. Ouvrez une fenêtre **Windows PowerShell** avec des privilèges élevés.
7. Entrez **ipconfig /all**.
8. Dans la sortie de hello, recherchez hello **adresse IPv4**, puis enregistrez adresse hello pour une utilisation ultérieure. Il s’agit d’adresse de hello vous test ping sera exécuté à partir de POC2. Dans l’environnement de l’exemple hello, l’adresse est **10.0.10.4**, mais dans votre environnement, il peut être différent. Il doit être inférieure à hello **10.0.10.0/24** sous-réseau que vous avez créé précédemment.
9. toocreate une règle de pare-feu qui autorise les toopings de toorespond de machine virtuelle hello, exécutez hello suivant de commande PowerShell :

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-toohello-tenant-vm-in-poc2"></a>Connectez-vous à toohello locataire machine virtuelle dans POC2
1. Connectez-vous à l’ordinateur physique toohello Azure pile pour POC2 et ensuite utiliser un toosign de compte du client dans le portail de l’utilisateur toohello.
2. Dans la barre de navigation gauche hello, cliquez sur **de calcul**.
3. À partir de la liste de hello des machines virtuelles, trouver **VM02** créé précédemment, puis sélectionnez-le.
4. Dans le panneau hello pour la machine virtuelle de hello, cliquez sur **connexion**.
5. Connectez-vous avec hello compte que vous avez configuré lors de la création de la machine virtuelle de hello.
6. Ouvrez une fenêtre **Windows PowerShell** avec des privilèges élevés.
7. Entrez **ipconfig /all**.
8. Vous devez normalement voir une adresse IPv4 qui fait partie du sous-réseau **10.0.20.0/24**. Dans l’environnement de l’exemple hello, l’adresse hello est **10.0.20.4**, mais votre adresse peut être différente.
9. toocreate une règle de pare-feu qui autorise les toopings de toorespond de machine virtuelle hello, exécutez hello suivant de commande PowerShell :

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. À partir de la machine virtuelle de hello sur POC2, interrogez la machine virtuelle de hello sur POC1, via un tunnel de hello. toodo, ping de hello DIP que vous avez enregistrée à partir de VM01.
   Dans l’environnement de l’exemple hello, il s’agit **10.0.10.4**, mais sera adresse de hello tooping que vous avez noté dans votre laboratoire. Vous devez voir un résultat qui ressemble à hello suivant :
   
    ![Test ping réussi](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. Une réponse à partir de la machine virtuelle à distance de hello indique un test réussi ! Vous pouvez fermer la fenêtre d’ordinateur virtuel hello. tootest votre connexion, vous pouvez essayer d’autres types de transferts de données comme une copie du fichier.

### <a name="viewing-data-transfer-statistics-through-hello-gateway-connection"></a>Affichage des données de transfert de statistiques au moyen de la connexion à la passerelle hello
Si vous souhaitez tooknow la quantité de données passe via une connexion site à site, ces informations sont disponibles sur hello **connexion** panneau. Ce test est également une autre méthode alliez tooverify qui hello ping que vous venez d’envoyer via la connexion VPN de hello.

1. Lorsque vous vous connectez dans machine virtuelle POC2 toohello client, utilisez votre toosign de compte du client dans le portail de l’utilisateur toothe.
2. Accédez trop**toutes les ressources**, puis sélectionnez hello **POC2-POC1** connexion. Le panneau **Connexion** s’affiche.
4. Sur hello **connexion** panneau, les statistiques de hello pour **données** et **données** s’affichent. Bonjour suivant capture d’écran, hello grands nombres sont attribuées tooadditional le transfert de fichiers. Normalement, vous ne devez pas voir de valeurs nulles ici.
   
    ![Données entrantes et sortantes](media/azure-stack-create-vpn-connection-one-node-tp2/image20.png)
