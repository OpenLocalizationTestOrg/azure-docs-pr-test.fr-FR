---
title: "Connecter un réseau virtuel à ordinateur tooa à l’aide de l’authentification de Point-to-Site et le certificat : portail Azure | Documents Microsoft"
description: "Connectez-vous en toute sécurité un tooyour ordinateur réseau virtuel Azure en créant une connexion de passerelle VPN Point à Site à l’aide de l’authentification par certificat. Cet article s’applique le modèle de déploiement du Gestionnaire de ressources toohello et utilise hello portail Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>Configurer un tooa de connexion de Point-to-Site réseau virtuel à l’aide de l’authentification par certificat : portail Azure

Cet article vous explique comment toocreate un réseau virtuel avec une connexion Point à Site dans le modèle de déploiement Resource Manager hello d’hello portail Azure. Cette configuration utilise hello tooauthenticate de certificats client se connecte. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portail Azure (classique)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Une passerelle VPN de Point-to-Site (P2S) vous permet de créer un réseau virtuel tooyour de connexion sécurisée à partir d’un ordinateur client. Connexions de point-to-Site VPN sont utiles lorsque vous souhaitez tooconnect tooyour réseau virtuel à partir d’un emplacement distant, par exemple lorsque vous sont télétravailleurs d’accueil ou d’une conférence. Un VPN P2S est également un toouse solution utile au lieu d’un VPN de Site à Site lorsque vous avez seulement quelques clients nécessitant tooconnect tooa réseau virtuel. 

P2S utilise hello Tunneling protocole SSTP (Secure Socket), qui est un protocole de VPN basée sur le protocole SSL. Un réseau VPN P2S est établie en le démarrant à partir de l’ordinateur client de hello.

![Diagramme point à site](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

Connexions d’authentification de certificat de point-to-Site exiger les éléments de hello :

* Une passerelle VPN RouteBased.
* Hello clé publique (fichier .cer) pour un certificat racine, qui est téléchargé tooAzure. Une fois que le certificat de hello est téléchargé, il est considéré comme un certificat approuvé et est utilisé pour l’authentification.
* Un certificat de client qui est généré à partir du certificat racine de hello et installé sur chaque ordinateur client qui se connectera toohello réseau virtuel. Ce certificat est utilisé pour l’authentification du client.
* Un package de configuration du client VPN. package de configuration de client VPN Hello contient des informations nécessaires de hello pour hello client tooconnect toohello réseau virtuel. Hello configure hello VPN client existant est natif toohello système d’exploitation Windows. Chaque client qui se connecte doit être configuré à l’aide du package de configuration hello.

Les connexions point à site ne nécessitent pas de périphérique VPN ou d’adresse IP publique locale. Hello connexion VPN est créée sur SSTP (Secure Socket Tunneling Protocol). Sur le côté du serveur hello, nous prenons en charge les versions 1.0, 1.1 et 1.2 de SSTP. client de Hello décide quelle toouse de version. Pour Windows 8.1 et supérieur, SSTP utilise la version 1.2 par défaut.

Pour plus d’informations sur les connexions de Point-to-Site, consultez hello [Point-to-Site FAQ](#faq) à fin hello de cet article.

#### <a name="example"></a>Exemples de valeurs

Vous pouvez utiliser hello suivant de valeurs toocreate un environnement de test, ou consultez les valeurs toothese toobetter comprendre les exemples hello dans cet article :

* **Nom du réseau virtuel :** VNet1
* **Espace d’adressage :** 192.168.0.0/16<br>Pour cet exemple, nous n’utilisons qu’un seul espace d’adressage. Vous pouvez avoir plusieurs espaces d’adressage pour votre réseau virtuel.
* **Nom du sous-réseau :** FrontEnd
* **Plage d’adresses de sous-réseau :** 192.168.1.0/24
* **L’abonnement :** si vous avez plusieurs abonnements, vérifiez que vous utilisez hello correct.
* **Groupe de ressources :** TestRG
* **Emplacement :** États-Unis de l’Est
* **Sous-réseau de passerelle :** 192.168.200.0/24<br>
* **Serveur DNS :** (facultatif) une adresse IP du serveur DNS de hello que vous souhaitez toouse pour la résolution de nom.
* **Nom de passerelle de réseau virtuel :** VNet1GW
* **Type de passerelle :** VPN
* **Type de VPN :** Route-based
* **Adresse IP publique :** VNet1GWpip
* **Type de connexion :** point à site
* **Pool d’adresses des clients :** 172.16.201.0/24<br>Les clients VPN qui se connectent toohello virtuel à l’aide de cette connexion Point-to-Site reçoivent une adresse IP du pool d’adresses client hello.

## <a name="createvnet"></a>1. Créez un réseau virtuel

Avant de commencer, assurez-vous que vous disposez d’un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial).

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Ajouter un sous-réseau de passerelle

Avant de connecter votre passerelle tooa de réseau virtuel, vous devez d’abord sous-réseau de passerelle hello toocreate toowhich de réseau virtuel hello vous voulez tooconnect. services de la passerelle Hello utilisent des adresses IP hello spécifiés dans le sous-réseau de passerelle hello. Si possible, créez un sous-réseau de passerelle à l’aide d’un bloc CIDR de /28 ou /27 tooprovide suffisamment IP adresses tooaccommodate futures de configuration supplémentaires requises.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. Spécifier un serveur DNS (facultatif)

Après avoir créé votre réseau virtuel, vous pouvez ajouter l’adresse IP de hello d’une résolution de nom DNS server toohandle. serveur DNS de Hello est facultative pour cette configuration, mais nécessaires si vous souhaitez que la résolution de noms. La définition d’une valeur n’entraîne pas la création de serveur DNS. Hello adresse IP du serveur DNS que vous spécifiez doit être un serveur DNS peut résoudre les noms de hello pour les ressources hello que vous êtes connecté. Pour cet exemple, nous avons utilisé une adresse IP privée, mais il est probable qu’il ne s’agit pas d’adresse IP de hello de votre serveur DNS. Être toouse que vos propres valeurs.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. Créer une passerelle de réseau virtuel

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. Générer des certificats

Les certificats sont utilisés par les clients Azure tooauthenticate tooa réseau virtuel via une connexion VPN de Site à Point de connexion. Une fois que vous obtenez un certificat racine, vous [télécharger](#uploadfile) hello tooAzure des informations de clé publique. certificat racine de Hello est alors considéré comme « approuvé » par Azure pour la connexion via P2S toohello virtual network. Votre également générer les certificats clients à partir de certificat racine approuvé de hello, puis installez-les sur chaque ordinateur client. certificat de client Hello est client de hello tooauthenticate utilisée lorsqu’elle initie un toohello de connexion réseau virtuel. 

### <a name="getcer"></a>1. Obtenir le fichier .cer hello pour le certificat racine de hello

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. Générer un certificat client

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Ajouter un pool d’adresses client hello

pool d’adresses client Hello est une plage d’adresses IP privées que vous spécifiez. les clients Hello qui se connectent via un VPN de Point-to-Site reçoivent une adresse IP à partir de cette plage. Utilisez une plage d’adresses IP privées qui ne chevauche pas avec emplacement hello local auquel vous vous connectez à partir d’ou hello réseau virtuel que vous souhaitez tooconnect à.

1. Une fois que la passerelle de réseau virtuel hello a été créé, accédez à toohello **paramètres** section de la page de passerelle de réseau virtuel hello. Bonjour **paramètres** , cliquez sur **configurationPointàsite** tooopen hello **Point-à-Site-Configuration** page.

  ![Page Point à site](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. Sur hello **Point-à-Site-Configuration** page, vous pouvez supprimer la plage de remplissage automatique de hello, puis ajouter hello privé plage d’adresses IP que vous souhaitez toouse. Cliquez sur **enregistrer** toovalidate et enregistrer les paramètre hello.

  ![Pool d’adresses des clients](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Télécharger les données de certificat public de certificat racine salutation

Une fois la passerelle de hello a été créé, vous téléchargez les informations de clé publique hello pour tooAzure de certificat racine hello. Une fois que les données de certificat public hello sont téléchargées, Azure peut utiliser tooauthenticate les clients qui ont installé un certificat de client généré à partir du certificat racine approuvé de hello. Vous pouvez télécharger le total des certificats tooa de racine de confiance supplémentaires de 20.

1. Les certificats sont ajoutés sur hello **configurationPointàsite** page Bonjour **certificat racine** section.  
2. Assurez-vous que vous avez exporté le certificat hello comme Base-64 encodé en fichier X.509 (.cer). Vous avez besoin de certificat de hello tooexport dans ce format afin de vous pouvez ouvrir les certificats hello avec l’éditeur de texte.
3. Ouvrez le certificat de hello avec un éditeur de texte, tel que le bloc-notes. Lors de la copie des données de certificat hello, assurez-vous que vous copiez le texte hello ligne continue sans les retours chariot ou les sauts de ligne. Vous devrez peut-être toomodify votre affichage dans too'Show de l’éditeur de texte hello symbole/Afficher chariot de tous les caractères toosee hello retourne et sauts de ligne. Copiez hello uniquement après la section comme une ligne continue :

  ![Données du certificat](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Collez les données de certificat hello hello **les données de certificat Public** champ. **Nom** hello du certificat, puis cliquez sur **enregistrer**. Vous pouvez ajouter des certificats d’origine too20 approuvé.

  ![Chargement d’un certificat](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. Générer et installer le package de configuration de client VPN hello

tooconnect tooa virtuel à l’aide d’un VPN de Point-to-Site, chaque client doit installer un package de configuration de client qui configure le client VPN natif de hello avec des paramètres de hello et les fichiers qui sont le réseau virtuel de toohello tooconnect nécessaire. package de configuration de client VPN Hello configure client VPN Windows natif de hello, il n’installe pas un client VPN nouveaux ou différent.

Vous pouvez utiliser hello même configuration du client VPN le package sur chaque ordinateur client, tant que la version de hello correspond à l’architecture hello pour les clients hello. Pour hello de la liste des systèmes d’exploitation client pris en charge, consultez hello [ForumauxquestionssurlesconnexionsPointàSite](#faq) à fin hello de cet article.

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>Étape 1 : générer et télécharger le package de configuration client hello

1. Sur hello **configurationPointàsite** , cliquez sur **client VPN de téléchargement** tooopen hello **client VPN de téléchargement** page. Il prend une ou deux minutes pour hello package toogenerate.

  ![Téléchargement du client VPN 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. Sélectionnez le bon package de hello pour votre client, puis cliquez sur **télécharger**. Enregistrez le fichier de package de configuration hello. Vous installez le package de configuration de client VPN hello sur chaque ordinateur client qui se connecte les réseaux virtuels toohello.

  ![Téléchargement du client VPN 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>Étape 2 : le package d’installation Bonjour client de configuration

1. Fichier de configuration de copie hello toohello localement les ordinateurs que vous souhaitez le réseau virtuel de tooconnect tooyour. 
2. Double-cliquez sur hello .exe fichier tooinstall hello package sur l’ordinateur client de hello. Étant donné que vous avez créé le package de configuration hello, il n’est pas signé, et vous pouvez voir un avertissement. Si vous obtenez un menu contextuel Windows SmartScreen, cliquez sur **plus d’informations** (sur hello gauche), puis **quand même exécuter** package de hello tooinstall.
3. Hello installer sur l’ordinateur client de hello. Si vous obtenez un menu contextuel Windows SmartScreen, cliquez sur **plus d’informations** (sur hello gauche), puis **quand même exécuter** package de hello tooinstall.
4. Sur l’ordinateur client de hello, accédez trop**paramètres réseau** et cliquez sur **VPN**. Hello connexion VPN affiche le nom hello du réseau virtuel hello auquel il se connecte.

## <a name="installclientcert"></a>9. Installer un certificat client exporté

Si vous voulez toocreate un P2S à partir d’un ordinateur client autre que hello celle que vous avez utilisé des certificats de client de hello toogenerate, vous devez tooinstall un certificat client. Lorsque vous installez un certificat client, vous avez besoin d’un mot de passe hello créé lors de l’exportation du certificat client hello. En règle générale, il est simplement en double-cliquant sur le certificat de hello et l’installer.

Assurez-vous que le certificat de client hello a été exporté dans un fichier .pfx, ainsi que la chaîne de certificat entière hello (qui est la valeur par défaut hello). Dans le cas contraire, informations relatives au certificat racine hello n’est pas présents sur l’ordinateur client de hello et hello client ne sera pas en mesure de tooauthenticate correctement. Pour plus d’informations, consultez la rubrique [Installer un certificat client exporté](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>10. Se connecter tooAzure

1. tooconnect tooyour réseau virtuel, sur l’ordinateur client de hello, accédez tooVPN connexions et trouver la connexion VPN hello que vous avez créé. Il est nommé hello même nom que votre réseau virtuel. Cliquez sur **Connecter**. Un message peut apparaître qui fait référence le certificat de hello toousing. Cliquez sur **continuer** toouse des privilèges élevés.

2. Sur hello **connexion** page d’état, cliquez sur **Connect** connexion de hello toostart. Si vous voyez un **sélectionner un certificat** écran, vérifiez que hello certificat client affiché est hello une que vous souhaitez toouse tooconnect. Si elle n’est pas le cas, utilisez bon certificat hello flèche tooselect hello, puis cliquez sur **OK**.

  ![Client VPN connecte tooAzure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. Votre connexion est établie.

  ![Connexion établie](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Résolution des problèmes liés aux connexions P2S

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. Vérifier votre connexion

1. tooverify que votre connexion VPN est active, ouvrez une invite de commandes avec élévation de privilèges et exécutez *ipconfig/all*.
2. Afficher les résultats hello. Notez qu’adresse hello que vous avez reçu est une des adresses hello dans le Pool d’adresses hello Point-to-Site VPN Client que vous avez spécifié dans votre configuration. les résultats de Hello sont similaires toothis exemple :

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Connecter l’ordinateur virtuel de tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>Ajout ou suppression de certificats racine approuvés

Vous pouvez ajouter et supprimer des certificats racines approuvés à partir d'Azure. Lorsque vous supprimez un certificat racine, les clients qui possèdent un certificat généré à partir de cette racine ne seront pas en mesure de tooauthenticate et par conséquent ne sera pas en mesure de tooconnect. Si vous souhaitez un tooauthenticate client et vous connecter, vous devez tooinstall un nouveau certificat de client généré à partir d’un certificat racine approuvé tooAzure (téléchargé).

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd un certificat racine approuvé

Vous pouvez ajouter jusqu'à tooAzure de fichiers too20 approuvé racine certificat .cer. Pour obtenir des instructions, consultez la section de hello [télécharger un certificat racine approuvé](#uploadfile) dans cet article.

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove un certificat racine approuvé

1. tooremove un certificat racine approuvé, accédez à toohello **configurationPointàsite** page de votre passerelle de réseau virtuel.
2. Bonjour **certificat racine** section de la page de hello, localisez le certificat de hello que vous souhaitez tooremove.
3. Cliquez sur le certificat de toohello suivant hello points de suspension, puis cliquez sur « Supprimer ».

## <a name="revokeclient"></a>Révocation d'un certificat client

Vous pouvez révoquer des certificats clients. certificat Hello liste de révocation vous permet de tooselectively refuser la connectivité de Point à Site basée sur des certificats clients individuels. Cela est différent de la suppression d’un certificat racine approuvé. Si vous supprimez un .cer du certificat racine approuvé à partir d’Azure, il révoque l’accès de hello pour tous les certificats du client généré/signé par le certificat racine révoqués de hello. Révoquer un certificat client, au lieu de certificat racine hello permet hello autres certificats générés à partir de hello racine certificat toocontinue toobe utilisé pour l’authentification.

courant Hello est toouse hello racine certificat toomanage l’accès aux niveaux d’équipe ou organisation, lors de l’utilisation des certificats clients révoqués de contrôle d’accès précis sur les utilisateurs individuels.

### <a name="toorevoke-a-client-certificate"></a>toorevoke un certificat client

Vous pouvez révoquer un certificat client en ajoutant la liste de révocation toohello hello l’empreinte numérique.

1. Récupérer l’empreinte de certificat client hello. Pour plus d’informations, consultez [comment tooretrieve hello empreinte d’un certificat](https://msdn.microsoft.com/library/ms734695.aspx).
2. Éditeur de texte hello informations tooa de copie et supprimer tous les espaces afin qu’il soit une chaîne continue.
3. Accédez de passerelle de réseau virtuel toohello **Point-à-site-configuration** page. Il s’agit de hello même page que vous avez utilisé trop[télécharger un certificat racine approuvé](#uploadfile).
4. Bonjour **les certificats révoqués** section, entrez un nom convivial pour le certificat hello (absence de nom commun du certificat toobe hello).
5. Copiez et collez hello empreinte chaîne toohello **l’empreinte numérique** champ.
6. l’empreinte numérique Hello valide et est automatiquement ajouté la liste de révocation toohello. Un message s’affiche sur l’écran hello que hello est mise à jour. 
7. Une fois la mise à jour terminée, les certificats hello ne peuvent plus être utilisé tooconnect. Les clients qui tentent de tooconnect à l’aide de ce certificat recevoir un message indiquant que ce certificat hello n’est plus valide.

## <a name="faq"></a>Forum Aux Questions sur les connexions point à site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Étapes suivantes
Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand en savoir plus sur la mise en réseau et les machines virtuelles, consultez [vue d’ensemble du réseau Azure et Linux VM](../virtual-machines/linux/azure-vm-network-overview.md).
