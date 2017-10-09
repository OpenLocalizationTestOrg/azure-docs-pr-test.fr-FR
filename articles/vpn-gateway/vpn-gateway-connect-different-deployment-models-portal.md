---
title: "Connecter des réseaux virtuels classiques tooAzure Gestionnaire de ressources VNets : portail | Documents Microsoft"
description: "Découvrez comment toocreate une connexion VPN entre classique des réseaux virtuels et VNets Gestionnaire de ressources à l’aide de la passerelle VPN et du portail de hello"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a>Connecter des réseaux virtuels à partir de modèles de déploiement différents à l’aide du portail de hello

Cet article vous explique comment tooconnect classique des réseaux virtuels tooResource Manager VNets tooallow hello ressources situées dans toocommunicate de modèles de déploiement distinct hello entre eux. étapes Hello dans cet article utilisent principalement hello portail Azure, mais vous pouvez également créer cette configuration à l’aide de hello PowerShell en sélectionnant l’article de hello dans cette liste.

> [!div class="op_single_selector"]
> * [Portail](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

La connexion d’un tooa de réseau virtuel classique Gestionnaire de ressources du VNet est tooconnecting comme emplacement d’un site réseau virtuel tooan local. Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE. Vous pouvez créer une connexion entre des réseaux virtuels situés dans des abonnements différents et des régions différentes. Vous pouvez également connecter des réseaux virtuels qui ont déjà des connexions tooon des réseaux locaux, tant que passerelle hello qui ils ont été configurés avec est dynamique ou basée sur un itinéraire. Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez hello [FAQ sur le réseau à](#faq) à fin hello de cet article. 

Si vos réseaux virtuels sont Bonjour même région, vous souhaiterez peut-être tooinstead connectent à l’aide de l’homologation de réseau virtuel. L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN. Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md). 

### <a name="prerequisites"></a>Composants requis

* Ces étapes supposent que les deux réseaux virtuels ont déjà été créés. Si vous utilisez cet article en guise d’exercice et que vous ne disposez pas des réseaux virtuels, il existe des liaisons dans hello étapes toohelp vous les créez.
* Vérifiez que les plages d’adresses de hello de hello que réseaux virtuels ne se chevauchent pas entre eux, ou se chevauchent avec les hello plages pour les autres connexions qui hello passerelles peuvent être connectés à.
* Installer les applets de commande PowerShell dernière hello pour le Gestionnaire de ressources et de gestion des services (classique). Dans cet article, nous utilisons hello portail Azure et PowerShell. PowerShell est requis toocreate hello connexion toohello de réseau virtuel classique hello Gestionnaire de ressources VNet. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). 

### <a name="values"></a>Exemples de paramètres

Vous pouvez utiliser ces valeurs de toocreate un environnement de test, ou consultez toothem toobetter comprendre les exemples hello dans cet article.

**Réseau virtuel classique**

Nom du réseau virtuel = ClassicVNet <br>
Espace d’adressage = 10.0.0.0/24 <br>
Sous-réseau-1 = 10.0.0.0/27 <br>
Groupe de ressources = ClassicRG <br>
Emplacement = Ouest des États-Unis <br>
Sous-réseau de passerelle = 10.0.0.32/28 <br>
Site local = RMVNetLocal <br>

**Réseau virtuel Resource Manager**

Nom du réseau virtuel = RMVNet <br>
Espace d’adressage = 192.168.0.0/16 <br>
Sous-réseau-1 = 192.168.1.0/24 <br>
Sous-réseau de passerelle = 192.168.0.0/26 <br>
Groupe de ressources = RG1 <br>
Emplacement = Est des États-Unis <br>
Nom de passerelle de réseau virtuel = RMGateway <br>
Type de passerelle = VPN <br>
Type de VPN = Route-based <br>
Nom de l’adresse IP publique de la passerelle = rmgwpip <br>
Passerelle de réseau local = ClassicVNetLocal <br>
Nom de connexion = RMtoClassic

### <a name="connection-overview"></a>Vue d’ensemble de la connexion

Pour cette configuration, vous créez une connexion de passerelle VPN via un tunnel IPsec/IKE VPN entre les réseaux virtuels hello. Assurez-vous qu’aucune des plages de votre réseau virtuel se chevauchent entre eux ou avec les réseaux locaux hello auquel ils se connectent à.

Hello tableau suivant montre un exemple de la façon dont l’exemple hello des réseaux virtuels et des sites locaux sont définies :

| Réseau virtuel | Espace d'adressage | Région | Se connecte à un site réseau toolocal |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Ouest des États-Unis | RMVNetLocal (192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |Est des États-Unis |ClassicVNetLocal (10.0.0.0/24) |

## <a name="classicvnet"></a>1. Configurer les paramètres de réseau virtuel classiques hello

Dans cette section, vous créez hello local (site local) de réseau et passerelle de réseau virtuel hello pour votre réseau virtuel classique. Si vous n’avez pas un réseau virtuel classique et que vous exécutez ces étapes en guise d’exercice, vous pouvez créer un réseau virtuel à l’aide de [cet article](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) et hello [exemple](#values) les valeurs des paramètres ci-dessus.

Lorsque vous utilisez toocreate de portail hello un réseau virtuel classique, vous devez accéder à panneau de réseau virtuel toohello à l’aide de hello comme suit, sinon hello option toocreate un réseau virtuel classique n’apparaît pas :

1. Cliquez sur hello '+' du Panneau de 'New' tooopen hello.
2. Dans le champ de « Marketplace hello de recherche » hello, tapez « Réseau virtuel ». Si vous sélectionnez à la place, la mise en réseau -> réseau virtuel, vous n’obtiendrez hello option toocreate un réseau virtuel classique.
3. Recherchez « Réseau virtuel » à partir de hello retourné la liste et cliquez dessus Panneau de réseau virtuel tooopen hello. 
4. Dans Panneau de réseau virtuel hello, sélectionnez « Classiques » toocreate un réseau virtuel classique. 

Si vous disposez déjà d’un réseau virtuel avec une passerelle VPN, vérifiez que cette passerelle hello est dynamique. Si elle est statique, vous devez d’abord supprimer la passerelle VPN de hello, puis continuer.

Les captures d’écran sont fournies à titre d’exemple. Être tooreplace que les valeurs hello par les vôtres ou utilisez hello [exemple](#values) valeurs.

### <a name="part-1---configure-hello-local-site"></a>Partie 1 : configurer le site local de hello

Ouvrez hello [portail Azure](https://ms.portal.azure.com) et connectez-vous avec votre compte Azure.

1. Accédez trop**toutes les ressources** et recherchez hello **ClassicVNet** dans la liste de hello.
2. Sur hello **vue d’ensemble** panneau, Bonjour **connexions VPN** , cliquez sur hello **passerelle** toocreate graphique une passerelle.

    ![Configurer une passerelle VPN](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "Configurer une passerelle VPN")
3. Sur hello **nouvelle connexion VPN** panneau, pour **type de connexion**, sélectionnez **Site-à-site**.
4. Sous **Site local**, cliquez sur **Configurer les paramètres requis**. Cette opération ouvre hello **site Local** panneau.
5. Sur hello **site Local** panneau, créer un toohello toorefer de nom du Gestionnaire de ressources VNet. Par exemple, « RMVNetLocal ».
6. Si la passerelle VPN de hello pour hello Gestionnaire de ressources VNet a déjà une adresse IP publique, utiliser la valeur de hello pour hello **adresse IP de passerelle VPN** champ. Si vous effectuez ces étapes en guise d’exercice, ou si ne disposez pas encore dune passerelle de réseau virtuel pour votre réseau virtuel Resource Manager, vous pouvez créer une adresse IP d’espace réservé. Assurez-vous que les adresse IP d’espace réservé hello utilise un format valide. Une version ultérieure, vous remplacez adresse espace réservé de hello en hello adresse IP publique de la passerelle de réseau virtuel du Gestionnaire de ressources hello.
7. Pour **espace d’adressage Client**, utilisez les valeurs de hello pour les espaces d’adressage IP hello réseau virtuel pour hello Gestionnaire de ressources VNet. Ce paramètre est utilisé toospecify hello adresse espaces tooroute toohello Gestionnaire de ressources du réseau virtuel.
8. Cliquez sur **OK** toosave hello valeurs et retourner toohello **nouvelle connexion VPN** panneau.

### <a name="part-2---create-hello-virtual-network-gateway"></a>Partie 2 : créer une passerelle de réseau virtuel hello

1. Sur hello **nouvelle connexion VPN** panneau, sélectionnez hello **créer une passerelle immédiatement** case à cocher et cliquez sur **configuration de la passerelle facultatif** tooopen hello  **Configuration de la passerelle** panneau. 

    ![Ouvrir le panneau Configuration de la passerelle](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "Ouvrir le panneau Configuration de la passerelle")
2. Cliquez sur **Subnet - configurer les paramètres requis** tooopen hello **ajouter un sous-réseau** panneau. Hello **nom** est déjà configuré avec la valeur de hello requis **GatewaySubnet**.
3. Hello **plage d’adresses** fait référence toohello plage de sous-réseau de passerelle hello. Bien que vous puissiez créer un sous-réseau de passerelle avec une plage d’adresses /29 (3 adresses), nous vous recommandons de créer un sous-réseau de passerelle qui contient plus d’adresses IP. Cela afin d’accueillir des configurations futures nécessitant la disponibilité d’un plus grand nombre d’adresses IP. Si possible, utilisez /27 ou /28. Si vous utilisez ces étapes en guise d’exercice, vous pouvez faire référence à toohello [exemple](#values) valeurs. Cliquez sur **OK** sous-réseau de passerelle toocreate hello.
4. Sur hello **configuration de la passerelle** panneau, **taille** fait référence toohello passerelle référence (SKU). Sélectionnez hello passerelle référence (SKU) pour votre passerelle VPN.
5. Vérifiez que hello **Type de routage** est **dynamique**, puis cliquez sur **OK** tooreturn toohello **nouvelle connexion VPN** panneau.
6. Sur hello **nouvelle connexion VPN** panneau, cliquez sur **OK** toobegin créer votre passerelle VPN. Création d’une passerelle VPN peut prendre jusqu'à too45 minutes toocomplete.

### <a name="ip"></a>Partie 3 : passerelle de réseau virtuel hello copie adresse IP publique

Une fois la passerelle de réseau virtuel hello a été créé, vous pouvez afficher l’adresse IP de passerelle hello. 

1. Accédez tooyour classique réseau virtuel, puis cliquez sur **vue d’ensemble**.
2. Cliquez sur **connexions VPN** Panneau de connexions VPN tooopen hello. Dans Panneau de connexions VPN hello, vous pouvez afficher l’adresse IP publique de hello. Il s’agit d’adresse IP publique de hello passerelle de réseau virtuel tooyour affectée. 
3. Notez ou copiez l’adresse IP de hello. Vous en aurez besoin aux étapes suivantes pour vos paramètres de configuration de passerelle de réseau local Resource Manager. Vous pouvez également afficher le statut de hello de vos connexions de passerelle. Site de réseau local hello avis que vous avez créé est répertorié comme « Connexion ». état de Hello passe après avoir créé vos connexions.
4. Fermez le panneau de hello après la copie d’adresse IP de passerelle hello.

## <a name="rmvnet"></a>2. Configurer les paramètres de réseau virtuel du Gestionnaire des ressources hello

Dans cette section, vous créer une passerelle de réseau virtuel hello et passerelle de réseau local hello du VNet de votre gestionnaire de ressources. Si vous n’avez pas un VNet Gestionnaire de ressources et que vous exécutez ces étapes en guise d’exercice, vous pouvez créer un réseau virtuel à l’aide de [cet article](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) et hello [exemple](#values) les valeurs des paramètres ci-dessus.

Les captures d’écran sont fournies à titre d’exemple. Être tooreplace que les valeurs hello par les vôtres ou utilisez hello [exemple](#values) valeurs.

### <a name="part-1---create-a-gateway-subnet"></a>Partie 1 : Créer un sous-réseau de passerelle

Avant de créer une passerelle de réseau virtuel, vous devez d’abord sous-réseau de passerelle toocreate hello. Créez un sous-réseau de passerelle avec un nombre CIDR de /28 ou plus. (/27, /26, etc.)

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a>Partie 2 : Créer une passerelle de réseau virtuel

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>Partie 3 : Créer une passerelle de réseau local

passerelle de réseau local Hello spécifie la plage d’adresses hello et l’adresse IP publique de hello associé à votre réseau virtuel classique et la passerelle de réseau virtuel.

Si vous effectuez ces étapes en guise d’exercice, consultez les paramètres toothese :

| Réseau virtuel | Espace d'adressage | Région | Se connecte à un site réseau toolocal |Adresse IP publique de la passerelle|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Ouest des États-Unis | RMVNetLocal (192.168.0.0/16) |Hello adresse IP publique affectée toohello ClassicVNet passerelle|
| RMVNet | (192.168.0.0/16) |Est des États-Unis |ClassicVNetLocal (10.0.0.0/24) |Hello adresse IP publique affectée toohello RMVNet passerelle.|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>3. Modifier les paramètres du site local hello classiques réseau virtuel

Dans cette section, vous remplacez les adresses IP hello espace réservé que vous avez utilisé lors de la spécification des paramètres de site local hello, par le Gestionnaire de ressources IP adresse la passerelle VPN de hello. Cette section utilise les applets de commande hello classique (SM) PowerShell.

1. Bonjour portail Azure, accédez à toohello de réseau virtuel classique.
2. Dans le panneau hello pour votre réseau virtuel, cliquez sur **vue d’ensemble**.
3. Bonjour **connexions VPN** , cliquez sur le nom de hello de votre site local dans le graphique de hello.

    ![Connexions VPN](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "Connexions VPN")
4. Sur hello **les connexions VPN de Site à site** panneau, cliquez sur nom hello du site de hello.

    ![Nom du site](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "Nom du site local")
5. Dans Panneau de connexion hello pour votre site local, cliquez sur nom hello Hello de hello site local tooopen **site Local** panneau.

    ![Ouvrir le site local](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "Ouvrir le site local")
6. Sur hello **site Local** panneau, remplacer hello **adresse IP de passerelle VPN** avec l’adresse IP de hello de passerelle du Gestionnaire de ressources hello.

    ![Adresse IP de la passerelle](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "Adresse IP de la passerelle")
7. Cliquez sur **OK** adresse IP de hello tooupdate.

## <a name="RMtoclassic"></a>4. Créer la connexion du Gestionnaire de ressources tooclassic

Dans ces étapes, vous configurez la connexion de hello de hello Gestionnaire de ressources VNet toohello classique réseau virtuel à l’aide de hello portail Azure.

1. Dans **toutes les ressources**, recherchez la passerelle de réseau local hello. Dans notre exemple, passerelle de réseau local hello est **ClassicVNetLocal**.
2. Cliquez sur **Configuration** et vérifiez que valeur de l’adresse IP hello est la passerelle VPN de hello pour hello réseau virtuel classique. Mettez à jour si nécessaire, puis cliquez sur **Enregistrer**. Panneau de fermeture hello.
3. Dans **toutes les ressources**, cliquez sur la passerelle de réseau local hello.
4. Cliquez sur **connexions** Panneau de connexions tooopen hello.
5. Sur hello **connexions** panneau, cliquez sur  **+**  tooadd une connexion.
6. Sur hello **ajouter une connexion** panneau, nom de connexion hello. Par exemple, « RMtoClassic ».
7. **Site à site** est déjà sélectionnée sur ce panneau.
8. Sélectionnez hello passerelle de réseau virtuel que vous souhaitez tooassociate avec ce site.
9. Créer une **clé partagée**. Cette clé est également utilisée dans la connexion hello que vous créez à partir de toohello de réseau virtuel classique hello Gestionnaire de ressources VNet. Vous pouvez générer une clé de hello ou en créer un. Dans l’exemple, nous avons utilisé « abc123 », mais vous pouvez (et devriez) utiliser une valeur plus complexe.
10. Cliquez sur **OK** connexion de hello toocreate.

##<a name="classictoRM"></a>5. Créer le Gestionnaire de connexions tooResource classique

Dans ces étapes, vous configurez connexion hello toohello de réseau virtuel classique hello Gestionnaire de ressources VNet. Pour ce faire, vous devez utiliser PowerShell. Impossible de créer cette connexion dans le portail de hello. Assurez-vous que vous avez téléchargé et installé hello classique (SM) et les applets de commande PowerShell de gestionnaire de ressources (RM).

### <a name="1-connect-tooyour-azure-account"></a>1. Se connecter tooyour compte Azure

Ouvrez la console PowerShell de hello avec des droits élevés et connectez-vous à tooyour compte Azure. Hello applet de commande suivante vous demande les informations d’identification de hello pour votre compte Azure. Après la connexion, les paramètres de votre compte sont téléchargés afin qu’ils soient disponible tooAzure PowerShell.

```powershell
Login-AzureRmAccount
```
   
Si vous possédez plusieurs abonnements, procurez-vous la liste de vos abonnements Azure.

```powershell
Get-AzureRmSubscription
```

Spécifiez un abonnement hello que vous souhaitez toouse. 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

Ajoutez votre compte Azure toouse hello classique applets de commande PowerShell (SM). toodo par conséquent, vous pouvez utiliser hello de commande suivante :

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a>2. Afficher les valeurs du fichier de configuration réseau hello

Lorsque vous créez un réseau virtuel dans hello portail Azure, nom complet hello que Azure utilise n’est pas visible dans hello portail Azure. Par exemple, un réseau virtuel qui s’affiche toobe nommé 'ClassicVNet' Bonjour portail Azure peut avoir un nom beaucoup plus de temps dans le fichier de configuration de réseau hello. Hello nom peut ressembler à ceci : « ClassicRG ClassicVNet de groupe ». Dans ces étapes, vous téléchargez hello fichier et affichage hello valeurs de configuration réseau.

Créez un répertoire sur votre ordinateur et exportez répertoire toohello du fichier de configuration hello réseau. Dans cet exemple, le fichier de configuration de réseau hello est tooC:\AzureNet exporté.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

Ouvrez le fichier de hello avec un éditeur et vue hello nom pour votre réseau virtuel classique. Utiliser des noms de hello dans le fichier de configuration de réseau hello lors de l’exécution de vos applets de commande PowerShell.

- Les noms des réseaux virtuels sont répertoriés comme suit : **VirtualNetworkSite name =**
- Les noms de site sont répertoriés comme suit : **LocalNetworkSite name=**

### <a name="3-create-hello-connection"></a>3. Créer la connexion de hello

Définir la clé partagée de hello et créez hello connexion toohello de réseau virtuel classique hello Gestionnaire de ressources VNet. Impossible de définir la clé partagée de hello à l’aide du portail de hello. Assurez-vous que vous exécutez ces étapes lorsque vous êtes connecté à l’aide de la version classique de hello Hello applets de commande PowerShell. toodo donc utiliser **Add-AzureAccount**. Dans le cas contraire, vous ne serez pas en mesure de tooset hello '-AzureVNetGatewayKey'.

- Dans cet exemple, **VNetName -** est le nom de hello hello classique réseau virtuel en tant que trouvé dans le fichier de configuration de votre réseau. 
- Hello **- LocalNetworkSiteName** nom hello vous avez spécifié pour le site local de hello, comme se trouve dans votre fichier de configuration réseau.
- Hello **SharedKey -** est une valeur que vous générez et que vous spécifiez. Dans l’exemple, nous avons utilisé *abc123*, mais vous pouvez générer quelque chose de plus complexe. Hello important est cette valeur hello que vous spécifiez ici doit être hello que même valeur que vous avez spécifié lors de la création de votre connexion tooclassic du Gestionnaire de ressources.

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>6. Vérifiez vos connexions

Vous pouvez vérifier que vos connexions à l’aide de hello portail Azure ou PowerShell. Lors de la vérification, vous devrez peut-être toowait une ou deux minutes lors de la création de connexions de hello. Lorsqu’une connexion est réussie, état de la connectivité hello passe de « Connexion » too'Connected'.

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>connexion de hello tooverify à partir de votre tooyour de réseau virtuel classique Gestionnaire de ressources VNet

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>connexion de hello tooverify à partir de votre gestionnaire de ressources du VNet de tooyour réseau virtuel classique

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
