---
title: "Créer une connexion entre des réseaux virtuels (classiques) : portail Azure | Microsoft Docs"
description: "Comment tooconnect Azure virtual networks ensemble à l’aide de PowerShell et hello portail Azure classic."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a>Configurer une connexion de réseau virtuel à réseau virtuel (classique)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Cet article vous montre comment toocreate une connexion de passerelle VPN entre les réseaux virtuels. Hello réseaux virtuels peuvent être hello identiques ou différentes régions, et à partir de hello identiques ou différents abonnements. étapes de Hello dans cet article s’appliquent modèle de déploiement classique toohello et hello portail Azure. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interface de ligne de commande Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portail Azure (classique)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connexions entre différents modèles de déploiement - Portail Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connexions entre différents modèles de déploiement - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![Réseau virtuel tooVNet diagramme de connectivité](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a>À propos des connexions de réseau virtuel à réseau virtuel

Connexion d’un réseau virtuel à tooanother de réseau virtuel (au réseau) dans le modèle de déploiement classique de hello à l’aide d’une passerelle VPN est tooconnecting comme emplacement d’un site réseau virtuel tooan local. Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE.

Hello vous connectez des réseaux virtuels peut être dans différents abonnements et des régions différentes. Vous pouvez combiner la communication tooVNet de réseau virtuel avec des configurations de plusieurs sites. Vous établissez ainsi des topologies réseau qui combinent une connectivité entre différents locaux et une connectivité entre différents réseaux virtuels.

![Réseau virtuel tooVNet connexions](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <a name="why"></a>Pourquoi connecter des réseaux virtuels ?

Vous souhaiterez peut-être les réseaux virtuels tooconnect pour hello suivant raisons :

* **Géo-redondance et présence géographique dans plusieurs régions**

  * Vous pouvez configurer la géo-réplication ou la synchronisation avec une connectivité sécurisée sans passer par les points de terminaison accessibles sur Internet.
  * Avec l’Azure Load Balancer et les technologies de clustering Microsoft ou tierces, vous pouvez configurer une charge de travail hautement disponible avec la géoredondance dans plusieurs régions Azure. Par exemple important, tooset des SQL Always On avec des groupes de disponibilité répartis dans plusieurs régions Azure.
* **Applications multiniveaux régionales avec une forte limite d’isolement**

  * Dans hello même région, vous pouvez définir des applications à plusieurs niveaux avec plusieurs réseaux virtuels interconnectés avec une isolation stricte et communication sécurisée de différents niveaux.
* **Communication interorganisationnelle entre plusieurs abonnements dans Azure**

  * Si vous avez plusieurs abonnements Azure, vous pouvez désormais interconnecter des charges de travail de différents abonnements en toute sécurité entre des réseaux virtuels.
  * Pour les entreprises ou prestataires de services, il est désormais possible d’activer la communication interorganisationnelle avec une technologie VPN sécurisée au sein d’Azure.

Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez [considérations sur le réseau à](#faq) à fin hello de cet article.

### <a name="before-you-begin"></a>Avant de commencer

Avant de commencer cet exercice, téléchargez et installez hello dernière version de hello applets de commande PowerShell de gestion de Service Azure (SM). Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). Nous utilisons le portail de hello pour la plupart des étapes de hello, mais vous devez utiliser des connexions de hello toocreate PowerShell entre hello des réseaux virtuels. Impossible de créer des connexions de hello à l’aide de hello portail Azure.

## <a name="plan"></a>Étape 1 : planifier vos plages d’adresses IP

Il s’agit des plages de hello toodecide important que vous allez utiliser tooconfigure vos réseaux virtuels. Pour cette configuration, il se peut que vous devez vous assurer qu’aucune des plages de votre réseau virtuel se chevauchent entre eux ou avec les réseaux locaux hello auxquels se connectent.

Hello tableau suivant illustre un exemple de toodefine vos réseaux virtuels. Utilisez les plages de hello à titre indicatif uniquement. Écrivez les plages hello pour vos réseaux virtuels. Vous aurez besoin de ces informations pour les étapes ultérieures.

**Exemple**

| Réseau virtuel | Espace d'adressage | Région | Se connecte à un site réseau toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Est des États-Unis |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Ouest des États-Unis |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

## <a name="vnetvalues"></a>Étape 2 : créer des réseaux virtuels hello

Créez deux réseaux virtuels Bonjour [portail Azure](https://portal.azure.com). Les étapes hello toocreate des réseaux virtuels classiques, consultez [créer un réseau virtuel classique](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). 

Lorsque vous utilisez toocreate de portail hello un réseau virtuel classique, vous devez accéder à panneau de réseau virtuel toohello à l’aide de hello comme suit, sinon hello option toocreate un réseau virtuel classique n’apparaît pas :

1. Cliquez sur hello '+' du Panneau de 'New' tooopen hello.
2. Dans le champ de « Marketplace hello de recherche » hello, tapez « Réseau virtuel ». Si vous sélectionnez à la place, la mise en réseau -> réseau virtuel, vous n’obtiendrez hello option toocreate un réseau virtuel classique.
3. Recherchez « Réseau virtuel » à partir de hello retourné la liste et cliquez dessus Panneau de réseau virtuel tooopen hello. 
4. Dans Panneau de réseau virtuel hello, sélectionnez « Classiques » toocreate un réseau virtuel classique. 

Si vous utilisez cet article en guise d’exercice, vous pouvez utiliser hello exemple valeurs suivantes :

**Valeurs pour TestVNet1**

Nom : TestVNet1<br>
Espace d’adressage : 10.11.0.0/16, 10.12.0.0/16 (facultatif)<br>
Nom du sous-réseau : par défaut<br>
Plage d’adresses de sous-réseau : 10.11.0.1/24<br>
Groupe de ressources : ClassicRG<br>
Emplacement : Est des États-Unis<br>
Sous-réseau de passerelle : 10.11.1.0/27

**Valeurs pour TestVNet4**

Nom : TestVNet4<br>
Espace d’adressage : 10.41.0.0/16, 10.42.0.0/16 (facultatif)<br>
Nom du sous-réseau : par défaut<br>
Plage d’adresses de sous-réseau : 10.41.0.1/24<br>
Groupe de ressources : ClassicRG<br>
Emplacement : États-Unis de l’Ouest<br>
Sous-réseau de passerelle : 10.41.1.0/27

**Lorsque vous créez vos réseaux virtuels, gardez Bonjour esprit suivant les paramètres :**

* **Espaces d’adressage de réseau virtuel** – sur la page d’espaces d’adressage de réseau virtuel hello, spécifiez la plage d’adresses hello que vous souhaitez toouse pour votre réseau virtuel. Il s’agit d’adresses IP dynamiques hello qui recevront des machines virtuelles de toohello et d’autres instances de rôle que vous déployez le réseau virtuel de toothis.<br>adresse Hello espaces que vous sélectionnez ne peuvent pas chevaucher les espaces d’adressage hello des hello autres emplacements de réseaux virtuels ou locaux ce réseau virtuel se connectera.

* **Emplacement** : lorsque vous créez un réseau virtuel, vous l’associez à un emplacement Azure (région). Par exemple, si vous souhaitez que vos ordinateurs virtuels qui sont déploiement toobe de réseau virtuel tooyour physiquement située dans l’ouest des États-Unis, sélectionnez cet emplacement. Vous ne pouvez pas modifier l’emplacement hello associé à votre réseau virtuel après que l’avoir créée.

**Après avoir créé vos réseaux virtuels, vous pouvez ajouter hello suivant les paramètres :**

* **L’espace d’adressage** – espace d’adressage supplémentaire n’est pas requis pour cette configuration, mais vous pouvez ajouter l’espace d’adressage supplémentaires après la création d’hello réseau virtuel.

* **Sous-réseaux** : des sous-réseaux supplémentaires ne sont pas requises pour cette configuration, mais vous souhaiterez peut-être toohave vos machines virtuelles dans un sous-réseau séparé de vos autres instances de rôle.

* **Serveurs DNS** – Entrez le nom du serveur DNS hello et l’adresse IP. Ce paramètre n’entraîne pas la création de serveur DNS. Il vous permet de serveurs DNS de toospecify hello que vous souhaitez toouse pour la résolution de nom pour ce réseau virtuel.

Dans cette section, vous configurez le type de connexion hello, site local hello et créez une passerelle de hello.

## <a name="localsite"></a>Étape 3 : configuration du site local de hello

Azure utilise les paramètres de hello spécifié dans chaque toodetermine site de réseau local comment tooroute le trafic entre hello des réseaux virtuels. Chaque réseau virtuel doit pointer toohello respectifs réseau local que vous voulez que le trafic tooroute. Vous déterminez hello nom de site de réseau local toouse toorefer tooeach. Il s’agit des meilleures toouse descriptif plus préci.

Par exemple, TestVNet1 se connecte tooa site réseau local que vous créez nommé 'VNet4Local'. paramètres de Hello pour VNet4Local contiennent des préfixes d’adresse hello pour TestVNet4.

Hello local de site pour chaque réseau virtuel est hello autre réseau virtuel. Hello exemple valeurs suivantes est utilisée pour notre configuration :

| Réseau virtuel | Espace d'adressage | Région | Se connecte à un site réseau toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Est des États-Unis |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Ouest des États-Unis |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

1. Recherchez TestVNet1 Bonjour portail Azure. Bonjour **connexions VPN** section du Panneau de hello, cliquez sur **passerelle**.

    ![Aucune passerelle](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. Sur hello **nouvelle connexion VPN** page, sélectionnez **Site-à-Site**.
3. Cliquez sur **site Local** tooopen hello page du site Local et configurer les paramètres de hello.
4. Sur hello **site Local** page, le nom de votre site local. Dans notre exemple, nous nom site local de hello 'VNet4Local'.
5. Comme **Adresse IP de la passerelle VPN**, vous pouvez utiliser l’adresse IP de votre choix, pourvu qu’elle soit dans un format valide. En règle générale, vous utiliseriez une adresse IP externe réelle hello pour un périphérique VPN. Toutefois, pour une configuration de réseau virtuel à réseau virtuel classique, vous utilisez hello une adresse IP publique affectée toohello passerelle pour votre réseau virtuel. Étant donné que vous n’avez pas encore créé passerelle de réseau virtuel hello, vous spécifiez une adresse IP publique valide comme espace réservé.<br>Ne laissez pas ce champ vide. Il n’est pas facultatif pour cette configuration. Dans une étape ultérieure, vous revenez dans ces paramètres et les configurer avec des adresses IP de passerelle correspondants réseau virtuel hello une fois Azure génère.
6. Pour **espace d’adressage Client**, utilisez espace d’adressage hello Hello autre réseau virtuel. Consultez tooyour exemple. Cliquez sur **OK** toosave vos paramètres et retour toohello arrière **nouvelle connexion VPN** panneau.

    ![site local](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <a name="gw"></a>Étape 4 : créer une passerelle de réseau virtuel hello

Chaque réseau virtuel doit disposer d’une passerelle de réseau virtuel. passerelle de réseau virtuel Hello achemine et chiffre le trafic.

1. Sur hello **nouvelle connexion VPN** panneau, la case à cocher Sélectionner hello **créer une passerelle immédiatement**.
2. Cliquez sur **Sous-réseau, taille et type de routage**. Sur hello **configuration de la passerelle** panneau, cliquez sur **sous-réseau**.
3. nom de sous-réseau de passerelle Hello est automatiquement renseigné avec le nom de hello requis « GatewaySubnet ». Hello **plage d’adresses** contient des adresses IP hello allouées toohello services de la passerelle VPN. Certaines configurations autorisent un sous-réseau de passerelle de /29, mais ses meilleures toouse un /28 ou /27 tooaccommodate futures configurations qui peuvent nécessiter plusieurs adresses IP pour les services de la passerelle hello. Dans les paramètres de notre exemple, nous utilisons 10.11.1.0/27. Ajuster l’espace d’adressage hello, puis cliquez sur **OK**.
4. Configurer hello **taille de la passerelle**. Ce paramètre fait référence toohello [référence (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).
5. Configurer hello **Type de routage**. Hello type de routage pour cette configuration doit être **dynamique**. Vous ne pouvez pas modifier les type de routage hello plus tard, sauf si vous détruire la passerelle de hello et créez un nouveau.
6. Cliquez sur **OK**.
7. Sur hello **nouvelle connexion VPN** panneau, cliquez sur **OK** toobegin création de passerelle de réseau virtuel hello. Création d’une passerelle peut souvent prendre entre 45 minutes ou plus, selon la passerelle sélectionnée de hello référence (SKU).

## <a name="vnet4settings"></a>Étape 5 : configurer les paramètres de TestVNet4

Répétez les étapes de hello trop[créer un site local](#localsite) et [créer une passerelle réseau virtuel hello](#gw) tooconfigure TestVNet4, en remplaçant les valeurs hello lorsque cela est nécessaire. Si vous effectuez cette opération en guise d’exercice, utilisez hello [exemples de valeurs](#vnetvalues).

## <a name="updatelocal"></a>Étape 6 - sites locaux hello de mise à jour

Une fois vos passerelles de réseau virtuel ont été créés pour les deux réseaux virtuels, vous devez ajuster les sites locaux hello **adresse IP de passerelle VPN** valeurs.

|Nom du réseau virtuel|Site connecté|Adresse IP de la passerelle|
|:--- |:--- |:--- |
|TestVNet1|VNet4Local|Adresse IP de passerelle VPN pour TestVNet4|
|TestVNet4|VNet1Local|Adresse IP de passerelle VPN pour TestVNet1|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a>Partie 1 : Get hello réseau virtuel passerelle adresse IP publique

1. Recherchez votre réseau virtuel dans hello portail Azure.
2. Cliquez sur tooopen hello réseau virtuel **vue d’ensemble** panneau. Dans Panneau de hello, dans **connexions VPN**, vous pouvez afficher l’adresse IP de hello pour votre passerelle de réseau virtuel.

  ![Adresse IP publique](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. Copiez l’adresse IP de hello. Vous allez l’utiliser dans la section suivante de hello.
4. Répétez ces étapes pour TestVNet4

### <a name="part-2---modify-hello-local-sites"></a>Partie 2 : modifier des sites locaux hello

1. Recherchez votre réseau virtuel dans hello portail Azure.
2. Sur le réseau virtuel de hello **vue d’ensemble** panneau, cliquez sur le site local hello.

  ![Site local créé](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. Sur hello **connexions VPN Site à Site** panneau, cliquez sur nom hello du site local de hello que vous souhaitez toomodify.

  ![Ouvrir le site local](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. Cliquez sur hello **site Local** que vous souhaitez toomodify.

  ![modifier le site](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. Hello de mise à jour **adresse IP de passerelle VPN** et cliquez sur **OK** toosave les paramètres hello.

  ![IP de la passerelle](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. Fermez hello autres panneaux.
7. Répétez ces étapes pour TestVNet4.

## <a name="getvalues"></a>Étape 7 : récupérer des valeurs à partir du fichier de configuration de réseau hello

Lorsque vous créez des réseaux virtuels classiques dans hello portail Azure, nom hello qui vous permet d’afficher n’est pas complet hello que vous utilisez pour PowerShell. Par exemple, un réseau virtuel apparaît toobe nommé **TestVNet1** dans le portail hello, peut avoir un nom beaucoup plus de temps dans le fichier de configuration de réseau hello. Hello nom peut ressembler à ceci : **groupe ClassicRG TestVNet1**. Lorsque vous créez vos connexions, il est valeurs hello toouse important que vous voyez dans le fichier de configuration de réseau hello.

Bonjour comme suit, vous allez vous connecter tooyour compte Azure et téléchargement et vue Bonjour réseau configuration fichier tooobtain Bonjour les valeurs qui sont requis pour vos connexions.

1. Téléchargez et installez la version la plus récente hello Hello applets de commande PowerShell de gestion de Service Azure (SM). Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

2. Ouvrez la console PowerShell avec des droits élevés et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

  ```powershell
  Login-AzureRmAccount
  ```

  Vérifiez les abonnements hello pour le compte de hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Si vous avez plusieurs abonnements, sélectionnez l’abonnement hello que vous souhaitez toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  Ensuite, utilisez hello suivant l’applet de commande tooadd tooPowerShell de votre abonnement Azure pour le modèle de déploiement classique hello.

  ```powershell
  Add-AzureAccount
  ```
3. Exporter et afficher le fichier de configuration de réseau hello. Créez un répertoire sur votre ordinateur et exportez répertoire toohello du fichier de configuration hello réseau. Dans cet exemple, le fichier de configuration de réseau hello est exporté trop**C:\AzureNet**.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. Ouvrez le fichier de hello avec un texte éditeur et vue hello les noms des réseaux virtuels et des sites. Il s’agit de nom de hello que vous utilisez lorsque vous créez vos connexions.<br>Les noms des réseaux virtuels sont répertoriés comme suit : **VirtualNetworkSite name =**<br>Les noms des sites sont répertoriés comme suit : **LocalNetworkSiteRef name =**

## <a name="createconnections"></a>Étape 8 - créer des connexions de la passerelle VPN hello

Lorsque toutes les étapes précédentes hello ont été exécutées, vous pouvez définir des clés prépartagées IPsec/IKE de hello et créer la connexion de hello. Cet ensemble d’étapes utilise PowerShell. Impossible de configurer des connexions de réseau virtuel à réseau virtuel pour le modèle de déploiement classique hello Bonjour portail Azure.

Dans les exemples hello, notez que la clé partagée de hello est hello exactement identiques. clé partagée de Hello doit toujours correspondre. Être tooreplace que les valeurs hello dans ces exemples dont le nom exact de hello pour vos réseaux virtuels et les Sites de réseau Local.

1. Créer hello TestVNet1 tooTestVNet4 connexion.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. Créer hello TestVNet4 tooTestVNet1 connexion.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. Attendez que hello connexions tooinitialize. Une fois que hello passerelle initialisée, hello statut est 'Réussite'.

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <a name="faq"></a>Interconnexion de réseaux virtuels pour les réseaux virtuels classiques
* les réseaux virtuels Hello peuvent être Bonjour identiques ou différents abonnements.
* les réseaux virtuels Hello peuvent être Bonjour identiques ou différentes régions (emplacements) Azure.
* Un service cloud ou un point de terminaison d’équilibrage de charge ne peut pas s’étendre sur différents réseaux virtuels, même si ces derniers sont interconnectés.
* L’interconnexion de plusieurs réseaux virtuels ne nécessite pas d’appareils VPN.
* La connexion de réseau virtuel à réseau virtuel prend en charge la connexion de réseaux virtuels Azure. Il ne prend pas en charge les machines virtuelles qui se connecte ou des services de cloud qui ne sont pas déployés tooa des réseaux virtuels.
* La connectivité de réseau virtuel à réseau virtuel nécessite des passerelles de routage dynamiques. Les passerelles de routage statique Azure ne sont pas prises en charge.
* Une connectivité réseau virtuelle peut être utilisée en même temps que des VPN multisites. Il existe un maximum de 10 tunnels VPN pour une passerelle VPN de réseau virtuel connexion tooeither d’autres réseaux virtuels ou sites locaux.
* Bonjour espaces d’adressage des réseaux virtuels de hello locaux et sur les sites de réseau local ne doivent pas se chevaucher. Chevauchement des espaces d’adressage entraîne la création de réseaux virtuels ou toofail de fichiers de configuration netcfg téléchargement hello.
* Les tunnels redondants entre deux réseaux virtuels ne sont pas pris en charge.
* Tous les tunnels VPN pour hello réseau virtuel, y compris les VPN P2S, partagent la bande passante disponible de hello pour la passerelle VPN de hello et hello même SLA de disponibilité de la passerelle VPN dans Azure.
* Réseau pour trafic transite sur hello backbone Azure.

## <a name="next-steps"></a>Étapes suivantes
Vérifiez vos connexions. Voir [Vérifier une connexion de passerelle VPN](vpn-gateway-verify-connection-resource-manager.md).
