---
title: "Se connecter à votre tooan de réseau local sur le réseau virtuel Azure : VPN de Site à Site (classiques) : portail | Documents Microsoft"
description: "Toocreate étapes une connexion IPsec à partir de votre site réseau tooan réseau virtuel Azure sur hello Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN Site à Site entre différents locaux à l’aide du portail de hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>Créer une connexion de Site à Site à l’aide de hello portail Azure (classique)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Cet article vous explique comment toouse hello toocreate portail Azure, une connexion de passerelle VPN de Site à Site à partir de votre toohello de réseau sur site réseau virtuel. étapes de Hello dans cet article s’appliquent à modèle de déploiement classique toohello. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [INTERFACE DE LIGNE DE COMMANDE](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portail Azure (classique)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Une connexion de passerelle VPN de Site à Site est utilisé tooconnect votre site réseau tooan réseau virtuel Azure via un tunnel VPN de IPsec/IKE (IKEv1 ou IKEv2). Ce type de connexion requiert un VPN périphérique local qui a un tooit d’adresse IP publique externe. Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).

![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Avant de commencer

Vérifiez que vous avez rempli hello suivant des critères avant de commencer la configuration :

* Vérifiez que vous souhaitez toowork dans le modèle de déploiement classique hello. Si vous souhaitez toowork dans le modèle de déploiement du Gestionnaire de ressources hello, consultez [créer une connexion de Site à Site (Resource Manager)](vpn-gateway-howto-site-to-site-resource-manager-portal.md). Lorsque cela est possible, nous vous recommandons d’utiliser modèle de déploiement du Gestionnaire de ressources hello.
* Assurez-vous que vous disposez d’un périphérique VPN compatible et une personne qui est en mesure de tooconfigure il. Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).
* Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN. Cette adresse IP ne peut pas se trouver derrière un NAT.
* Si vous n’êtes pas familiarisé avec les plages d’adresses IP hello situés dans configuration du réseau de votre site, vous devez toocoordinate avec une personne qui peut fournir ces informations pour vous. Lorsque vous créez cette configuration, vous devez spécifier hello plage préfixes d’adresse que Azure achemine emplacement local de tooyour. Aucun des sous-réseaux hello de votre réseau local peuvent se chevauchant avec les sous-réseaux du réseau virtuel hello tooconnect à souhaitées sur.
* Actuellement, PowerShell est la clé partagée de hello toospecify requises et créer la connexion à la passerelle VPN hello. Installer la version la plus récente hello Hello applets de commande PowerShell de gestion de Service Azure (SM). Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). Si vous utilisez PowerShell pour cette configuration, vérifiez que vous exécutez PowerShell en tant qu’administrateur. 

### <a name="values"></a>Exemples de valeurs de configuration pour cet exercice

exemples de Hello dans cet article utilisent hello valeurs suivantes. Vous pouvez utiliser ces valeurs de toocreate un environnement de test, ou consultez toothem toobetter comprendre les exemples hello dans cet article.

* **Nom du réseau virtuel :** TestVNet1
* **Espace d’adressage :** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (facultatif pour cet exercice)
* **Sous-réseaux :**
  * FrontEnd : 10.11.0.0/24
  * BackEnd : 10.12.0.0/24 (facultatif pour cet exercice)
* **Sous-réseau de passerelle :** 10.11.255.0/27
* **Groupe de ressources :** TestRG1
* **Emplacement :** États-Unis de l’Est
* **Serveur DNS :** 10.11.0.3 (facultatif pour cet exercice)
* **Nom du site local :** Site2
* **Espace d’adressage client :** hello espace d’adressage qui se trouve sur votre site local.

## <a name="CreatVNet"></a>1. Créez un réseau virtuel

Lorsque vous créez un toouse de réseau virtuel pour une connexion S2S, vous devez toomake que des espaces d’adressage hello que vous spécifiez ne se chevauchent pas avec les espaces d’adressage client hello pour les sites locaux hello que vous souhaitez tooconnect à. Si vos sous-réseaux se chevauchent, votre connexion ne fonctionnera pas correctement.

* Si vous disposez déjà d’un réseau virtuel, vérifiez que les paramètres de hello sont compatibles avec votre conception de passerelle VPN. Accordez une attention particulière aux sous-réseaux tooany peuvent se chevaucher avec d’autres réseaux. 

* Si vous n’avez pas de réseau virtuel, créez-en un. Les captures d’écran sont fournies à titre d’exemple. Être des valeurs de hello tooreplace que par les vôtres.

### <a name="toocreate-a-virtual-network"></a>toocreate un réseau virtuel

1. À partir d’un navigateur, accédez à toohello [portail Azure](http://portal.azure.com) et, si nécessaire, connectez-vous à votre compte Azure.
2. Cliquez sur **+** Bonjour **marketplace de hello recherche** , tapez « Réseau virtuel ». Recherchez **réseau virtuel** hello retourné à partir de liste et cliquez sur tooopen hello **réseau virtuel** page.

  ![Rechercher la page du réseau virtuel](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Bas hello de page de réseau virtuel hello, à partir de hello **sélectionner un modèle de déploiement** liste déroulante, sélectionnez **classique**, puis cliquez sur **créer**.

  ![Sélectionner le modèle de déploiement](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. Sur hello **créer virtuel network(classic)** page, de configurer les paramètres de réseau virtuel hello. Sur cette page, vous ajoutez votre premier espace d’adressage et une plage d’adresses de sous-réseau unique. Après avoir terminé la création de hello réseau virtuel, vous pouvez revenir en arrière et ajouter des espaces d’adressage et des sous-réseaux supplémentaires.

  ![Page Créer un réseau virtuel](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Page Créer un réseau virtuel")
5. Vérifiez que hello **abonnement** est hello correct. Vous pouvez modifier des abonnements à l’aide de hello de liste déroulante.
6. Cliquez sur **Groupe de ressources** et sélectionnez un groupe de ressources existant, ou créez un groupe de ressources en tapant un nom pour ce dernier. Pour plus d’informations sur les groupes de ressources, consultez [Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Ensuite, sélectionnez hello **emplacement** paramètres pour votre réseau virtuel. emplacement de Hello détermine où se trouvera ressources hello que vous déployez toothis réseau virtuel.
8. Si vous souhaitez toofind en mesure de toobe votre réseau virtuel facilement sur le tableau de bord hello, sélectionnez **toodashboard du code confidentiel**. Cliquez sur **créer** toocreate votre réseau virtuel.

  ![Code confidentiel toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "toodashboard du code confidentiel")
9. Après avoir cliqué sur « Créer », une vignette s’affiche sur le tableau de bord hello qui reflète la progression de hello de votre réseau virtuel. modifications vignette Hello hello réseau virtuel est en cours de création.

  ![Vignette de création du réseau virtuel](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "Création du réseau virtuel")

Une fois votre réseau virtuel est créé, vous voyez **créé** répertoriés sous **état** sur la page réseaux hello hello portail Azure classic.

## <a name="additionaladdress"></a>2. Ajouter un espace d’adressage supplémentaire

Après avoir créé votre réseau virtuel, vous pouvez ajouter un espace d’adressage supplémentaire. Ajout d’espace d’adressage supplémentaire n’est pas obligatoire dans une configuration S2S, mais si vous avez besoin de plusieurs espaces d’adressage, utilisez hello comme suit :

1. Recherchez les réseaux virtuels hello dans le portail de hello.
2. Sur la page hello pour votre réseau virtuel, sous hello **paramètres** , cliquez sur **l’espace d’adressage**.
3. Hello adresse espace page, cliquez sur **+ ajouter** et entrez l’espace d’adressage supplémentaire.

## <a name="dns"></a>3. Spécifier un serveur DNS

Les paramètres DNS ne sont pas indispensables à une configuration de site à site. Toutefois, vous devrez les configurer pour bénéficier de la résolution de noms. La définition d’une valeur n’entraîne pas la création de serveur DNS. Hello adresse IP du serveur DNS que vous spécifiez doit être un serveur DNS peut résoudre les noms de hello pour les ressources hello que vous êtes connecté. Pour les paramètres d’exemple hello, nous avons utilisé une adresse IP privée. adresse IP de Hello, nous utilisons n’est probablement pas hello adresseIP de votre serveur DNS. Être toouse que vos propres valeurs.

Après avoir créé votre réseau virtuel, vous pouvez ajouter l’adresse IP de hello d’une résolution de nom DNS server toohandle. Ouvrez les paramètres de hello pour votre réseau virtuel, cliquez sur serveurs DNS et ajouter l’adresse IP de hello du serveur DNS de hello que vous souhaitez toouse pour la résolution de nom.

1. Recherchez les réseaux virtuels hello dans le portail de hello.
2. Sur la page hello pour votre réseau virtuel, sous hello **paramètres** , cliquez sur **serveurs DNS**.
3. Ajoutez un serveur DNS.
4. toosave vos paramètres, cliquez sur **enregistrer** en hello haut hello.

## <a name="localsite"></a>4. Configurer le site local de hello

site local de Hello fait généralement référence d’emplacement de site tooyour. Il contient des adresse IP hello toowhich d’appareil VPN hello que vous allez créer une connexion et les plages d’adresses IP hello qui doivent être routés via le périphérique VPN toohello hello VPN gateway.

1. Dans le portail de hello, accédez toohello de réseau virtuel pour lequel vous souhaitez toocreate une passerelle.
2. Sur la page hello pour votre réseau virtuel, sur hello **vue d’ensemble** page, dans la section de connexions VPN hello, cliquez sur **passerelle** tooopen hello **nouvelle connexion VPN** page.

  ![Cliquez sur paramètres de la passerelle tooconfigure](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "cliquez sur paramètres de la passerelle tooconfigure")
3. Sur hello **nouvelle connexion VPN** page, sélectionnez **Site-à-site**.
4. Cliquez sur **Local de site - configurer les paramètres requis** tooopen hello **site Local** page. Configurer les paramètres de hello, puis cliquez sur **OK** toosave les paramètres hello.
  - **Nom :** créer un nom pour votre site local de toomake vous tooidentify plus facilement.
  - **Adresse IP de passerelle VPN :** hello une adresse IP publique du périphérique VPN de hello pour votre réseau local. périphérique VPN de Hello requiert une adresse IPv4 publique IP. Spécifiez une adresse IP publique valide pour hello toowhich de périphérique VPN souhaité tooconnect. Il ne peut pas se trouver derrière un NAT et toobe accessible par Azure. Si vous ne connaissez pas hello adresseIP de votre périphérique VPN, vous pouvez toujours placer dans une valeur d’espace réservé (tant qu’il est au format hello d’une adresse IP publique valide) et les modifier ultérieurement.
  - **Espace d’adressage client :** liste hello plages d’adresses que vous souhaitez routé réseau du site local toohello via cette passerelle. Vous pouvez ajouter plusieurs plages d’espaces d’adressage. Assurez-vous que vous spécifiez ici des plages hello ne se chevauchent pas avec d’autres réseaux d’à que votre réseau virtuel se connecte des plages, ou avec des plages d’adresses hello de hello réseau virtuel.

  ![Site local](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Configurez le site local")

## <a name="gatewaysubnet"></a>5. Configurez le sous-réseau de passerelle hello

Vous devez créer un sous-réseau de passerelle pour votre passerelle VPN. sous-réseau de passerelle Hello contient des adresses IP hello qui utilisent des services de la passerelle VPN hello.

1. Sur hello **nouvelle connexion VPN** page, la case à cocher Sélectionner hello **créer une passerelle immédiatement**. page Hello « configuration de passerelle facultatif » s’affiche. Si vous n’activez la case à cocher hello, vous ne voyez le sous-réseau de passerelle hello page tooconfigure hello.

  ![Configuration de la passerelle - Sous-réseau, taille, type de routage](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Configuration de la passerelle - Sous-réseau, taille, type de routage")
2. tooopen hello **configuration de la passerelle** , cliquez sur **configuration de la passerelle facultatif - sous-réseau, la taille et type de routage**.
3. Sur hello **Configuration de la passerelle** , cliquez sur **Subnet - configurer les paramètres requis** tooopen hello **ajouter un sous-réseau** page.

  ![Configuration de la passerelle - sous-réseau de passerelle](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "Configuration de la passerelle - sous-réseau de passerelle")
4. Sur hello **ajouter un sous-réseau** , ajoutez le sous-réseau de passerelle hello. taille de Hello du sous-réseau de passerelle hello que vous spécifiez dépend de configuration de la passerelle VPN hello que vous souhaitez toocreate. Bien qu’il soit possible de toocreate un sous-réseau de passerelle aussi petit que /29, nous vous recommandons d’utiliser /27 ou /28. Cette opération crée un sous-réseau plus grand qui inclut plusieurs adresses. Permet à l’aide d’un sous-réseau de passerelle supérieure suffisamment IP adresses tooaccommodate futures configurations possibles.

  ![Ajoutez un sous-réseau de passerelle](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Ajoutez un sous-réseau de passerelle")

## <a name="sku"></a>6. Spécifiez hello référence (SKU) et le type de VPN

1. Passerelle de hello sélectionnez **taille**. Il s’agit de passerelle de hello référence (SKU) que vous utilisez toocreate votre passerelle de réseau virtuel. Dans le portail hello, hello 'Par défaut SKU' = **base**. Les passerelles VPN classiques utilisent la passerelle de (hérités) ancien de hello références (SKU). Pour plus d’informations sur la passerelle de hérité hello références (SKU), consultez [utilisation de la passerelle de réseau virtuel références (SKU ancien)](vpn-gateway-about-skus-legacy.md).

  ![Sélectionnez la référence et le type de VPN](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "Sélectionnez la référence et le type de VPN")
2. Sélectionnez hello **Type de routage** pour votre passerelle. Cela est également appelé type de VPN hello. Il est important tooselect hello passerelle est correct, car il est impossible de convertir la passerelle de hello un type tooanother. Votre périphérique VPN doit être compatible avec le type de routage hello que vous sélectionnez. Pour plus d’informations sur le type de VPN, consultez la rubrique [À propos des paramètres de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype). Vous pouvez voir les articles de la référence too'RouteBased' et 'Basée sur des stratégies' VPN types. « Dynamique » correspond too'RouteBased », et correspond 'Static' à « Basée sur des stratégies ».
3. Cliquez sur **OK** toosave les paramètres hello.
4. Sur hello **nouvelle connexion VPN** , cliquez sur **OK** bas hello hello toobegin de page Création de votre passerelle de réseau virtuel. En fonction de la référence (SKU), vous sélectionnez de hello, peut prendre jusqu'à too45 minutes toocreate une passerelle de réseau virtuel.

## <a name="vpndevice"></a>7. Configuration de votre périphérique VPN

Réseau local de tooan connexions site à Site requièrent un périphérique VPN. Dans cette étape, vous configurez votre périphérique VPN. Lorsque vous configurez votre périphérique VPN, vous devez suivant de hello :

- Une clé partagée. Cela est hello même partagé clé que vous spécifiez lors de la création de votre connexion VPN de Site à Site. Dans nos exemples, nous utilisons une clé partagée basique. Nous conseillons de générer un toouse de clé plus complexe.
- Hello adresse IP publique de votre passerelle de réseau virtuel. Vous pouvez afficher l’adresse IP publique de hello à l’aide de hello portail Azure, PowerShell ou CLI.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Créer la connexion de hello
Dans cette étape, vous définissez la clé partagée de hello et créez la connexion de hello. vous définissez la clé Hello est doit être hello même clé que celle utilisée dans la configuration de votre périphérique VPN.

> [!NOTE]
> Actuellement, cette étape n’est pas disponible dans hello portail Azure. Vous devez utiliser la version de Service Management (SM) hello Hello applets de commande PowerShell de Azure.
>

### <a name="step-1-connect-tooyour-azure-account"></a>Étape 1. Se connecter tooyour compte Azure

1. Ouvrez la console PowerShell avec des droits élevés et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

  ```powershell
  Add-AzureAccount
  ```
2. Vérifiez les abonnements hello pour le compte de hello.

  ```powershell
  Get-AzureSubscription
  ```
3. Si vous avez plusieurs abonnements, sélectionnez l’abonnement hello que vous souhaitez toouse.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>Étape 2. Définir la clé partagée de hello et créer la connexion de hello

Lorsque vous travaillez avec un modèle de déploiement classique de PowerShell et hello, parfois, les noms de ressources dans le portail de hello hello ne sont pas hello noms hello Azure attend toosee lors de l’utilisation de PowerShell. Hello suit vous permet d’exporter hello fichier tooobtain hello exacte valeurs de configuration réseau pour les noms de hello.

1. Créez un répertoire sur votre ordinateur et exportez répertoire toohello du fichier de configuration hello réseau. Dans cet exemple, le fichier de configuration de réseau hello est tooC:\AzureNet exporté.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Ouvrez le fichier de configuration de réseau hello avec un éditeur xml et vérifier les valeurs hello pour 'LocalNetworkSite name' et 'Nom de VirtualNetworkSite'. Modifiez hello exemple tooreflect hello valeurs dont vous avez besoin. Lorsque vous spécifiez un nom qui contient des espaces, utilisez des guillemets simples autour de valeur de hello.

3. Définir la clé partagée de hello et créer la connexion de hello. Hello '-SharedKey' est une valeur que vous générez et que vous spécifiez. Dans l’exemple de hello, nous avons utilisé « abc123 », mais vous pouvez générer (et devraient) utiliser quelque chose de plus complexe. Hello important est cette valeur hello que vous spécifiez ici doit être hello que même valeur que vous avez spécifié lors de la configuration de votre périphérique VPN.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Lors de la connexion de hello est créée, hello résulte : **état : réussite**.

## <a name="verify"></a>9. Vérifier votre connexion

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

Si vous rencontrez des problèmes de connexion, consultez hello **dépannage** section hello de table des matières dans le volet gauche de hello.

## <a name="reset"></a>Comment tooreset une passerelle VPN

La réinitialisation d’une passerelle VPN Azure est utile si vous perdez la connectivité VPN entre différents locaux sur un ou plusieurs tunnels VPN de site à site. Dans ce cas, vos périphériques VPN sur site sont tous les fonctionne correctement, mais sont tooestablish n’a pas pu les tunnels IPsec avec les passerelles VPN Azure hello. Pour obtenir la procédure, consultez [Réinitialiser une passerelle VPN](vpn-gateway-resetgw-classic.md).

## <a name="changesku"></a>Comment toochange une passerelle de référence (SKU)

Les étapes de hello toochange une référence (SKU) de la passerelle, consultez [redimensionner une référence (SKU) de la passerelle](vpn-gateway-about-SKUS-legacy.md).

## <a name="next-steps"></a>Étapes suivantes

* Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Pour plus d’informations sur le tunneling forcé, consultez [Configuration du tunneling forcé à l’aide du modèle de déploiement classique](vpn-gateway-about-forced-tunneling.md).