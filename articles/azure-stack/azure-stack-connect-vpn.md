---
title: "Connexion d’Azure Stack à Azure à l’aide d’un VPN"
description: "Découvrez comment connecter des réseaux virtuels Azure Stack à des réseaux virtuels Azure à l’aide d’un VPN."
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: victorh
ms.openlocfilehash: c06eb0bb44bdfeab956e9b5051786b5bc631acf5
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="connect-azure-stack-to-azure-using-vpn"></a>Connexion d’Azure Stack à Azure à l’aide d’un VPN

*S’applique à : systèmes intégrés Azure Stack*

Cet article explique comment créer un VPN de site à site pour connecter un réseau virtuel dans Azure Stack à un réseau virtuel dans Azure.

### <a name="connection-diagram"></a>Diagramme de connexions
Le diagramme ci-après illustre à quoi la configuration d’une connexion devra ressembler lorsque vous aurez terminé :

![Configuration d’une connexion VPN de site à site](media/azure-stack-connect-vpn/image2.png)

### <a name="before-you-begin"></a>Avant de commencer
Avant de commencer la configuration de la connexion, vérifiez que vous disposez des éléments suivants :

* Un déploiement de systèmes intégrés Azure Stack (plusieurs nœuds) directement connecté à Internet. Cela signifie que votre plage d’adresses IP publiques externe doit être directement accessible à partir du réseau Internet public.
* Un abonnement Azure valide.  Si vous n’avez pas d’abonnement Azure, vous pouvez créer un [compte Azure gratuit ici](https://azure.microsoft.com/free/?b=17.06).

## <a name="network-example-values-table"></a>Tableau d’exemples de valeurs réseau
Le tableau d’exemples de valeurs réseau affiche les exemples de valeurs qui sont utilisés dans cet article. Vous pouvez utiliser ces valeurs ou vous y référer pour mieux comprendre les exemples de cet article.

**Tableau d’exemples de valeurs réseau**
|   |Azure Stack|Microsoft Azure|
|---------|---------|---------|
|Nom du réseau virtuel     |Azs-VNet|AzureVNet |
|Espace d’adressage du réseau virtuel |10.1.0.0/16|10.100.0.0/16|
|Nom du sous-réseau     |FrontEnd|FrontEnd|
|Plage d’adresses de sous-réseau|10.1.0.0/24 |10.100.0.0/24 |
|Sous-réseau de passerelle     |10.1.1.0/24|10.100.1.0/24|

## <a name="create-the-network-resources-in-azure"></a>Créer les ressources réseau dans Azure

Vous devez tout d’abord créer les ressources réseau pour Azure. Les instructions ci-après vous indiquent comment créer les ressources à partir du [portail Azure](http://portal.azure.com/).

### <a name="create-the-virtual-network-and-vm-subnet"></a>Créer le réseau virtuel et le sous-réseau de machine virtuelle

1. Connectez-vous au [portail Azure](http://portal.azure.com/) avec votre compte Azure.
2. Dans le portail utilisateur, sélectionnez **Nouveau**.
3. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
4. Sélectionnez **Réseau virtuel**.
5. À l’aide des informations données dans la table de configuration réseau, renseignez les champs **Nom**, **Espace d’adressage**, **Nom de sous-réseau** et **Plage d’adresses de sous-réseau** de manière appropriée pour Azure.
6. Pour le champ **Groupe de ressources**, créez un groupe de ressources ou, si vous en avez déjà un, sélectionnez **Utiliser l’existant**.
7. Sélectionnez l’**emplacement** de votre réseau virtuel.  Si vous utilisez les exemples de valeurs, sélectionnez **Est des États-Unis** ou utilisez un autre emplacement si vous préférez.
8. Sélectionnez **Épingler au tableau de bord**.
9. Sélectionnez **Créer**.

### <a name="create-the-gateway-subnet"></a>Créer le sous-réseau de passerelle
1. Ouvrez la ressource de réseau virtuel que vous avez créée (**AzureVNet**) à partir du tableau de bord.
2. Dans la section **Paramètres**, sélectionnez **Sous-réseaux**.
3. Sélectionnez **Sous-réseau de passerelle** pour ajouter un sous-réseau de passerelle au réseau virtuel.
4. Par défaut, le nom du sous-réseau est défini sur **GatewaySubnet**.
   Les sous-réseaux de passerelle sont des éléments spéciaux et doivent porter ce nom pour fonctionner correctement.
5. Dans le champ **Plage d’adresses**, vérifiez que l’adresse est **10.100.0.0/24**.
6. Sélectionnez **OK** pour créer le sous-réseau de passerelle.

### <a name="create-the-virtual-network-gateway"></a>Créer la passerelle de réseau virtuel
1. Dans le Portail Azure, sélectionnez **Nouveau**.  
2. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
3. Dans la liste des ressources réseau, sélectionnez **Passerelle de réseau virtuel**.
4. Sous **Nom**, saisissez **Azure-GW**.
5. Pour choisir un réseau virtuel, sélectionnez **Réseau virtuel**. Sélectionnez ensuite **AzureVnet** dans la liste.
6. Sélectionnez **Adresse IP publique**. Quand la section **Choisir une adresse IP publique** s’affiche, sélectionnez **Créer**.
7. Sous **nom**, saisissez **Azure-GW-PiP**, puis sélectionnez **OK**.
8. Dans le champ **Type de VPN**, l’élément **Basé sur itinéraires** est sélectionné par défaut.
    Conservez le type de VPN **Basé sur itinéraires**.
9. Vérifiez que l’**abonnement** et l’**emplacement** sont corrects. Vous pouvez épingler la ressource au tableau de bord. Sélectionnez **Créer**.

### <a name="create-the-local-network-gateway-resource"></a>Créer la ressource de passerelle de réseau local

1. Dans le Portail Azure, sélectionnez **Nouveau**. 
4. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
5. Dans la liste des ressources, sélectionnez **Passerelle de réseau local**.
6. Dans le champ **Nom**, saisissez **Azs-GW**.
7. Pour **Adresse IP**, saisissez l’adresse IP publique de votre passerelle de réseau virtuel Azure Stack, indiquée plus haut dans le tableau de configuration du réseau.
8. Dans **Espace d’adressage**, à partir d’Azure Stack, entrez l’espace d’adressage **10.0.10.0/23** pour **AzureVNet**.
9. Vérifiez l’exactitude des valeurs des champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **Créer**.

## <a name="create-the-connection"></a>Créer la connexion
1. Dans le portail utilisateur, sélectionnez **Nouveau**. 
2. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
3. Dans la liste des ressources, sélectionnez **Connexion**.
4. Dans la section de paramètres **De base**, pour le champ **Type de connexion**, choisissez **Site à site (IPSec)**.
5. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
6. Dans la section **Paramètres**, sélectionnez **Passerelle de réseau virtuel**, puis **Azure-GW**.
7. Sélectionnez **Passerelle de réseau local**, puis **Azs-GW**.
8. Dans le champ **Nom de la connexion**, saisissez **Azure-Azs**.
9. Dans **Clé partagée (PSK)**, saisissez **12345**. Si vous choisissez une autre valeur, n’oubliez pas qu’elle *doit* correspondre à la valeur de la clé partagée que vous créez à l’autre extrémité de la connexion. Sélectionnez **OK**.
10. Dans la section **Résumé**, vérifiez les paramètres, puis sélectionnez **OK**.

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle
Créez d’abord une machine virtuelle dans Azure, puis ajoutez-la au sous-réseau de machine virtuelle dans votre réseau virtuel.

1. Dans le Portail Azure, sélectionnez **Nouveau**.
2. Accédez à la **Place de marché**, puis sélectionnez **Compute**.
3. Dans la liste des images de machine virtuelle, sélectionnez l’image **Windows Server 2016 Datacenter Evals**.
4. Dans la section **De base**, sous **Nom**, saisissez **AzureVM**.
5. Entrez un nom d’utilisateur et un mot de passe valides. Vous utiliserez ce compte plus tard pour vous connecter à la machine virtuelle que vous créez actuellement.
6. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
7. Dans la section **Taille**, sélectionnez une taille de machine virtuelle pour cette instance, puis choisissez **Sélectionner**.
8. Dans la section **Paramètres**, vous pouvez accepter les valeurs par défaut. Vérifiez que le réseau virtuel **AzureVnet** est sélectionné et que le sous-réseau est défini sur **10.0.20.0/24**. Sélectionnez **OK**.
9. Dans la section **Résumé**, vérifiez les paramètres, puis sélectionnez **OK**.

## <a name="create-the-network-resources-in-azure-stack"></a>Créer les ressources réseau dans Azure Stack
Vous devez maintenant créer les ressources réseau dans Azure Stack.

### <a name="sign-in-as-a-user"></a>Connectez-vous en tant qu’utilisateur
Un administrateur de services fédérés peut se connecter en tant qu’utilisateur pour tester les plans, les offres et les abonnements mis à la disposition des utilisateurs. Si vous ne l’avez pas encore fait, [créez un compte d’utilisateur](azure-stack-add-new-user-aad.md) avant de vous connecter.

### <a name="create-the-virtual-network-and-vm-subnet"></a>Créer le réseau virtuel et le sous-réseau de machine virtuelle
1. Utilisez un compte d’utilisateur pour vous connecter au portail utilisateur.
2. Dans le portail utilisateur, sélectionnez **Nouveau**.

    ![Créer un réseau virtuel](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
4. Sélectionnez **Réseau virtuel**.
5. Renseignez les champs **Nom**, **Espace d’adressage**, **Nom de sous-réseau** et **Plage d’adresses de sous-réseau** avec les valeurs qui figurent dans la table de configuration réseau.
6. Le champ **Abonnement** affiche l’abonnement que vous avez créé précédemment.
7. Pour le champ **Groupe de ressources**, créez un groupe de ressources ou, si vous en avez déjà un, sélectionnez **Utiliser l’existant**.
8. Vérifiez l’emplacement par défaut.
9. Sélectionnez **Épingler au tableau de bord**.
10. Sélectionnez **Créer**.

### <a name="create-the-gateway-subnet"></a>Créer le sous-réseau de passerelle
1. Dans le tableau de bord, ouvrez la ressource de réseau virtuel Azs-VNet que vous avez créée.
2. Dans la section **Paramètres**, sélectionnez **Sous-réseaux**.
3. Pour ajouter un sous-réseau de passerelle au réseau virtuel, sélectionnez **Sous-réseau de passerelle**.
   
    ![Ajouter un sous-réseau de passerelle](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. Par défaut, le nom du sous-réseau est **GatewaySubnet**.
   Les sous-réseaux de passerelle ont une particularité. Pour fonctionner correctement, ils doivent avoir le nom *GatewaySubnet*.
5. Dans **Plage d’adresses**, vérifiez que l’adresse est **10.1.1.0/24**.
6. Sélectionnez **OK** pour créer le sous-réseau de passerelle.

### <a name="create-the-virtual-network-gateway"></a>Créer la passerelle de réseau virtuel
1. Dans le portail Azure Stack, sélectionnez **Nouveau**. 
2. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
3. Dans la liste des ressources réseau, sélectionnez **Passerelle de réseau virtuel**.
4. Dans le champ **Nom**, saisissez **Azs-GW**.
5. Sélectionnez l’élément **Réseau virtuel** pour choisir un réseau virtuel.
   Sélectionnez **Azs-VNet** dans la liste.
6. Sélectionnez l’élément de menu **Adresse IP publique**. Quand la section **Choisir une adresse IP publique** s’affiche, sélectionnez **Créer**.
7. Dans le champ **Nom**, saisissez **Azs-GW-PiP**, puis sélectionnez **OK**.
8.  Dans le champ **Type de VPN**, l’élément **Basé sur itinéraires** est sélectionné par défaut.
    Conservez le type de VPN **Basé sur itinéraires**.
9. Vérifiez que l’**abonnement** et l’**emplacement** sont corrects. Vous pouvez épingler la ressource au tableau de bord. Sélectionnez **Créer**.

### <a name="create-the-local-network-gateway"></a>Créer la passerelle de réseau local
La notion de *passerelle de réseau local* dans Azure Stack diffère légèrement de celle dans un déploiement Azure.

En effet, dans un déploiement Azure, une passerelle de réseau local représente un appareil physique local (à l’emplacement de l’utilisateur), que vous utilisez pour vous connecter à une passerelle de réseau virtuel dans Azure. Dans Azure Stack, les deux extrémités de la connexion sont des passerelles de réseau virtuel.

De façon plus générale, la ressource de passerelle de réseau local représente toujours la passerelle distante située à l’autre extrémité de la connexion. 

### <a name="create-the-local-network-gateway-resource"></a>Créer la ressource de passerelle de réseau local
1. Connectez-vous au portail Azure Stack.
2. Dans le portail utilisateur, sélectionnez **Nouveau**.
3. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
4. Dans la liste des ressources, sélectionnez **Passerelle de réseau local**.
5. Sous **Nom**, saisissez **Azure-GW**.
6. Dans le champ **Adresse IP**, entrez l’adresse IP publique de la passerelle de réseau virtuel dans Azure **Azure-GW-PiP**. Cette adresse figure dans la table de configuration réseau, plus haut dans cet article.
7. Dans le champ **Espace d’adressage**, entrez **10.0.20.0/23** comme espace d’adressage du réseau virtuel Azure que vous venez de créer.
8. Vérifiez l’exactitude des valeurs des champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **Créer**.

### <a name="create-the-connection"></a>Créer la connexion
1. Dans le portail utilisateur, sélectionnez **Nouveau**.
2. Accédez à la **Place de marché**, puis sélectionnez **Mise en réseau**.
3. Dans la liste des ressources, sélectionnez **Connexion**.
4. Dans la section des paramètres **De base**, pour le champ **Type de connexion**, sélectionnez **Site à site (IPSec)**.
5. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
6. Dans la section **Paramètres**, sélectionnez **Passerelle de réseau virtuel**, puis **Azs-GW**.
7. Sélectionnez **Passerelle de réseau local**, puis **Azure-GW**.
8. Dans le champ **Nom de la connexion**, entrez **Azs-Azure**.
9. Sous **Clé partagée (PSK)**, entrez **12345**, puis sélectionnez **OK**.
10. Dans la section **Résumé**, sélectionnez **OK**.

### <a name="create-a-vm"></a>Créer une machine virtuelle
Pour vous assurer que les données transitent bien par la connexion VPN, vous devez créer des machines virtuelles à chaque extrémité pour envoyer et recevoir les données via le tunnel VPN. 

1. Dans le Portail Azure, sélectionnez **Nouveau**.
2. Accédez à la **Place de marché**, puis sélectionnez **Compute**.
3. Dans la liste des images de machine virtuelle, sélectionnez l’image **Windows Server 2016 Datacenter Evals**.
4. Dans la section **De base**, sous **Nom**, saisissez **Azs-VM**.
5. Entrez un nom d’utilisateur et un mot de passe valides. Vous utiliserez ce compte plus tard pour vous connecter à la machine virtuelle que vous créez actuellement.
6. Renseignez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis sélectionnez **OK**.
7. Dans la section **Taille**, sélectionnez une taille de machine virtuelle pour cette instance, puis choisissez **Sélectionner**.
8. Dans la section **Paramètres**, acceptez les valeurs par défaut. Assurez-vous que le réseau virtuel **Azs-VNet** est sélectionné. Vérifiez que le sous-réseau est défini sur **10.1.0.0/24**. Sélectionnez ensuite **OK**.
9. Dans la section **Résumé**, vérifiez les paramètres, puis sélectionnez **OK**.


## <a name="test-the-connection"></a>Tester la connexion
Vous avez établi la connexion de site à site. Vous devez maintenant vérifier que le trafic transite bien par cette connexion. Pour valider, connectez-vous à l’une des machines virtuelles que vous avez créées dans Azure Stack. Ensuite, effectuez un test Ping sur la machine virtuelle que vous avez créée dans Azure Stack. 

Pour vérifier que le trafic envoyé passe par la connexion de site à site, effectuez le test Ping sur l’adresse IP directe (DIP) de la machine virtuelle du sous-réseau distant, et non sur l’adresse IP virtuelle. Pour cela, recherchez l’adresse DIP à l’autre extrémité de la connexion. Enregistrez l’adresse pour l’utiliser plus tard.

### <a name="sign-in-to-the-user-vm-in-azure-stack"></a>Connectez-vous à la machine virtuelle utilisateur dans Azure Stack
1. Connectez-vous au portail Azure Stack.
2. Sélectionnez **Machines virtuelles** dans la barre de navigation de gauche.
3. Dans la liste des machines virtuelles, recherchez la machine virtuelle **AZs-VM** que vous avez créée précédemment et sélectionnez-la.
4. Dans la section de la machine virtuelle, cliquez sur **Se connecter**, puis ouvrez le fichier Azs-VM.rdp.
   
     ![Bouton Se connecter](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. Connectez-vous avec le compte que vous avez configuré pendant la création de la machine virtuelle.
6. Ouvrez une fenêtre **Windows PowerShell** avec des privilèges élevés.
7. Entrez **ipconfig/all**.
8. Dans la sortie, recherchez la valeur **Adresse IPv4**, puis enregistrez l’adresse pour l’utiliser plus tard. Il s’agit de l’adresse sur laquelle vous allez effectuer un test Ping à partir d’Azure. Dans l’exemple d’environnement, l’adresse est **10.0.10.4**, mais peut être différente dans votre environnement. Elle doit faire partie du sous-réseau **10.0.10.0/24** que vous avez créé précédemment.
9. Pour créer une règle de pare-feu qui autorise la machine virtuelle à répondre aux tests ping, exécutez la commande PowerShell suivante :

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-to-the-tenant-vm-in-azure"></a>Se connecter à la machine virtuelle locataire dans Azure
1. Connectez-vous au portail Azure.
2. Dans la barre de navigation de gauche, cliquez sur **Machines virtuelles**.
3. Dans la liste des machines virtuelles, recherchez la machine virtuelle **Azure-VM** que vous avez créée précédemment et sélectionnez-la.
4. Dans la section de la machine virtuelle, cliquez sur **Se connecter**.
5. Connectez-vous avec le compte que vous avez configuré pendant la création de la machine virtuelle.
6. Ouvrez une fenêtre **Windows PowerShell** avec des privilèges élevés.
7. Entrez **ipconfig/all**.
8. Vous devez normalement voir une adresse IPv4 qui fait partie du sous-réseau **10.0.20.0/24**. Dans l’exemple d’environnement, l’adresse est **10.0.20.4**, mais votre adresse peut être différente.
9. Pour créer une règle de pare-feu qui autorise la machine virtuelle à répondre aux tests ping, exécutez la commande PowerShell suivante :

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. À partir de la machine virtuelle dans Azure, effectuez un test Ping de la machine virtuelle dans Azure Stack, par le biais du tunnel. Pour cela, effectuez un test Ping sur l’adresse IP directe (DIP) que vous avez enregistrée à partir d’Azs-VM.
   Dans l’exemple d’environnement, l’adresse est **10.0.10.4**, mais vous devez effectuer le test ping sur l’adresse que vous avez notée dans votre lab. Vous devez obtenir un résultat semblable à celui présenté dans la capture d’écran suivante :
   
    ![Test ping réussi](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. La réception d’une réponse de la machine virtuelle distante indique que le test a réussi ! Vous pouvez fermer la fenêtre de la machine virtuelle. Pour tester votre connexion, vous pouvez essayer d’autres types de transferts de données, par exemple, une copie de fichier.

### <a name="viewing-data-transfer-statistics-through-the-gateway-connection"></a>Affichage des statistiques de transfert de données via la connexion de passerelle
Si vous souhaitez connaître la quantité de données qui transite par votre connexion de site à site, consultez cette information dans la section **Connexion**. Ce test est également un autre moyen de vérifier que la commande ping que vous venez d’envoyer est bien passée par la connexion VPN.

1. Quand vous êtes connecté à la machine virtuelle utilisateur dans Azure Stack, utilisez votre compte d’utilisateur pour vous connecter au portail utilisateur.
2. Accédez à **Toutes les ressources**, puis sélectionnez la connexion **Azs-Azure**. Le panneau **Connexion** s’affiche.
4. La section **Connexion** affiche les statistiques pour **Données entrantes** et **Données sortantes**. Dans la capture d’écran suivante, les valeurs élevées sont dues au transfert de fichiers supplémentaires. Normalement, vous ne devez pas voir de valeurs nulles ici.
   
    ![Données entrantes et sortantes](media/azure-stack-connect-vpn/Connection.png)

## <a name="next-steps"></a>Étapes suivantes

[Déployer des applications sur Azure et Azure Stack](azure-stack-solution-pipeline.md)