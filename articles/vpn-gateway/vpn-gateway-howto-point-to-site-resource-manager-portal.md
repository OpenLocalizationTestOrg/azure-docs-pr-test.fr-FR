---
title: "Connecter un ordinateur à un réseau virtuel Azure à l’aide d’une connexion point à site et d’une authentification par certificat Azure native : Portail Azure | Microsoft Docs"
description: "Connectez de façon sécurisée un ordinateur à votre réseau virtuel Azure en créant une connexion de passerelle VPN point à site à l’aide d’une authentification par certificat. Cet article concerne le modèle de déploiement Resource Manager et utilise le portail Azure."
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
ms.date: 01/17/2018
ms.author: cherylmc
ms.openlocfilehash: 39129572ac9908429dc9b9ef64930e896afc355f
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2018
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-native-azure-certificate-authentication-azure-portal"></a>Configurer une connexion point à site sur un réseau virtuel à l’aide d’une authentification par certificat Azure native : Portail Azure

Cet article explique comment créer un réseau virtuel avec une connexion point à site dans le modèle de déploiement Resource Manager à l’aide du portail Azure. Cette configuration utilise des certificats pour l’authentification. Dans cette configuration, c’est la passerelle VPN Azure qui effectue la validation du certificat, et non un serveur RADIUS. Vous pouvez également créer cette configuration à l’aide d’un autre outil ou modèle de déploiement en sélectionnant une option différente dans la liste suivante :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portail Azure (classique)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Une connexion par passerelle VPN point à site (P2S) vous permet de créer une connexion sécurisée à votre réseau virtuel à partir d’un ordinateur de client individuel. Les connexions VPN point à site sont utiles lorsque vous souhaitez vous connecter à votre réseau virtuel à partir d’un emplacement distant, par exemple lorsque vous travaillez à distance depuis votre domicile ou en conférence. De même, l’utilisation d’un VPN P2S est une solution utile qui constitue une alternative au VPN Site à Site lorsqu’un nombre restreint de clients doivent se connecter à un réseau virtuel. Une connexion VPN P2S est démarrée à partir d’appareils Windows et Mac.

Les clients de connexion peuvent utiliser les méthodes d’authentification suivantes :

* Serveur RADIUS
* Authentification par certificat Azure native de la passerelle VPN

Cet article vous aide à configurer une configuration P2S avec authentification à l’aide de l’authentification par certificat Azure native. Si vous souhaitez utiliser RADIUS pour authentifier les utilisateurs qui se connectent, consultez [P2S à l’aide de l’authentification RADIUS](point-to-site-how-to-radius-ps.md).

![Diagramme de connexion d’un ordinateur à un réseau virtuel Azure à l’aide d’une passerelle point à site](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/p2snativeps.png)

Les connexions de point à site ne nécessitent pas de périphérique VPN ou d’adresse IP publique. La connexion P2S crée la connexion VPN via SSTP (Secure Socket Tunneling Protocol) ou IKEv2.

* SSTP est un tunnel VPN basé sur le protocole SSL qui n’est pris en charge que sur les plateformes clientes Windows. Il peut pénétrer des pare-feux, ce qui en fait une option idéale pour se connecter à Azure à partir de n’importe quel endroit. Côté serveur, nous prenons en charge SSTP, versions 1.0, 1.1 et 1.2. Le client détermine la version à utiliser. Pour Windows 8.1 et supérieur, SSTP utilise la version 1.2 par défaut.

* Un VPN IKEv2 est une solution VPN IPsec basée sur des normes. Un VPN IKEv2 peut être utilisé pour se connecter à partir d’appareils Mac (OSX 10.11 et versions ultérieures).

Les connexions d’authentification par certificat Azure native de point à site requièrent les éléments suivants :

* Une passerelle VPN RouteBased.
* La clé publique (fichier .cer) d’un certificat racine, chargée sur Azure. Une fois le certificat chargé, il est considéré comme un certificat approuvé et est utilisé pour l’authentification.
* Un certificat client généré à partir du certificat racine et installé sur chaque ordinateur client qui se connecte au réseau virtuel. Ce certificat est utilisé pour l’authentification du client.
* Une configuration du client VPN. Les fichiers de configuration du client VPN contiennent les informations nécessaires permettant au client de se connecter sur le réseau virtuel. Les fichiers configurent le client VPN existant qui est natif au système d’exploitation. Chaque client qui se connecte doit être configuré à l’aide des paramètres dans les fichiers de configuration.

Pour plus d’informations sur les connexions point à site, consultez [À propos des connexions point à site](point-to-site-about.md).

#### <a name="example"></a>Exemples de valeurs

Vous pouvez utiliser ces valeurs pour créer un environnement de test ou vous y référer pour mieux comprendre les exemples de cet article :

* **Nom du réseau virtuel :** VNet1
* **Espace d’adressage :** 192.168.0.0/16<br>Pour cet exemple, nous n’utilisons qu’un seul espace d’adressage. Vous pouvez avoir plusieurs espaces d’adressage pour votre réseau virtuel.
* **Nom du sous-réseau :** FrontEnd
* **Plage d’adresses de sous-réseau :** 192.168.1.0/24
* **Abonnement :** vérifiez que vous utilisez l’abonnement approprié si vous en possédez plusieurs.
* **Groupe de ressources :** TestRG
* **Emplacement :** États-Unis de l’Est
* **Sous-réseau de passerelle :** 192.168.200.0/24<br>
* **Serveur DNS :** (facultatif) l’adresse IP du serveur DNS que vous souhaitez utiliser pour la résolution de noms.
* **Nom de passerelle de réseau virtuel :** VNet1GW
* **Type de passerelle :** VPN
* **Type de VPN :** Route-based
* **Adresse IP publique :** VNet1GWpip
* **Type de connexion :** point à site
* **Pool d’adresses des clients :** 172.16.201.0/24<br>Les clients VPN qui se connectent au réseau virtuel à l’aide de cette connexion point à site reçoivent une adresse IP de ce pool d’adresses des clients.

## <a name="createvnet"></a>1. Créez un réseau virtuel

Avant de commencer, assurez-vous que vous disposez d’un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial).
[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Ajouter un sous-réseau de passerelle

Avant de connecter votre réseau virtuel à une passerelle, vous devez créer le sous-réseau de passerelle pour le réseau virtuel auquel vous souhaitez vous connecter. Les adresses de passerelle utilisent les adresses spécifiées dans le sous-réseau de passerelle. Si possible, créez un sous-réseau de passerelle à l’aide d’un bloc CIDR de /28 ou /27 pour fournir suffisamment d’adresses IP pour satisfaire les exigences de configuration future supplémentaires.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. Spécifier un serveur DNS (facultatif)

Après avoir créé votre réseau virtuel, vous pouvez ajouter l’adresse IP d’un serveur DNS pour gérer la résolution de noms. Le serveur DNS est facultatif pour cette configuration, mais nécessaire si vous souhaitez la résolution de noms. La définition d’une valeur n’entraîne pas la création de serveur DNS. L’adresse IP du serveur DNS que vous spécifiez doit pouvoir résoudre les noms des ressources auxquelles vous vous connectez. Pour cet exemple, nous avons utilisé une adresse IP privée, mais il ne s’agit probablement pas de l’adresse IP de votre serveur DNS. Veillez à utiliser vos propres valeurs. La valeur que vous spécifiez est utilisée par les ressources que vous déployez sur le réseau virtuel, et non par la connexion P2S ou le client VPN.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. Créer une passerelle de réseau virtuel

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. Générer des certificats

Les certificats sont utilisés par Azure pour authentifier les clients qui se connectent à un réseau virtuel via une connexion VPN point à site. Une fois que vous avez obtenu le certificat racine, vous [chargez](#uploadfile) les informations de la clé publique du certificat racine vers Azure. Le certificat racine est alors considéré comme « approuvé » par Azure pour la connexion via P2S sur le réseau virtuel. Vous générez également des certificats de client à partir du certificat racine approuvé, puis vous les installez sur chaque ordinateur client. Le certificat permet d’authentifier le client lorsqu’il établit une connexion avec le réseau virtuel. 

### <a name="getcer"></a>1. Obtenir le fichier .cer pour le certificat racine

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. Générer un certificat client

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Ajouter le pool d’adresses des clients

Le pool d’adresses des clients est une plage d’adresses IP privées que vous spécifiez. Les clients qui se connectent via un réseau virtuel de point à site reçoivent une adresse IP de cette plage. Utilisez une plage d’adresses IP privées qui ne chevauche ni l’emplacement local à partir duquel vous vous connectez ni le réseau virtuel auquel vous souhaitez vous connecter.

1. Une fois la passerelle de réseau virtuel créée, accédez à la section **Paramètres** de la page Passerelle de réseau virtuel. Dans la section **Paramètres**, cliquez sur **Configuration de point à site** pour ouvrir la page **Configuration de point à site**.

  ![Page Point à site](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. Sur la page de la **Configuration de point à site**, vous pouvez supprimer la plage renseignée automatiquement, puis ajouter la plage d’adresses IP privées que vous souhaitez utiliser. Cliquez sur **Enregistrer** pour valider et enregistrer le paramètre.

  ![Pool d’adresses des clients](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Charger les données de certificat public du certificat racine

Après la création de la passerelle, vous chargez la clé publique pour le certificat racine dans Azure. Une fois que les données de certificat public sont chargées, Azure peut les utiliser pour authentifier les clients qui ont installé un certificat client généré à partir du certificat racine approuvé. Vous pouvez charger d’autres certificats racines approuvés, jusqu’à 20 au total.

1. Les certificats sont ajoutés sur la page **Configuration de point à site**, dans la section **Certificat racine**.  
2. Vérifiez que vous avez exporté le certificat racine en tant que fichier Base-64 codé X.509 (.cer). Vous devez exporter le certificat dans ce format pour être en mesure de l’ouvrir avec un éditeur de texte.
3. Ouvrez le certificat avec un éditeur de texte, Bloc-notes par exemple. Lors de la copie des données de certificat, assurez-vous que vous copiez le texte en une seule ligne continue sans retour chariot ou sauts de ligne. Vous devrez peut-être modifier l’affichage dans l’éditeur de texte en activant « Afficher les symboles/Afficher tous les caractères » pour afficher les retours chariot et sauts de ligne. Copiez uniquement la section suivante sur une seule ligne continue :

  ![Données du certificat](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Collez les données du certificat dans le champ **Données du certificat public**. Donnez un **Nom** au certificat, puis cliquez sur **Enregistrer**. Vous pouvez ajouter jusqu’à 20 certificats racine approuvés.

  ![Chargement d’un certificat](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="installclientcert"></a>8. Installer un certificat client exporté

Si vous souhaitez créer une connexion P2S à partir d’un ordinateur client différent de celui que vous avez utilisé pour générer les certificats clients, vous devez installer un certificat client. Quand vous installez un certificat client, vous avez besoin du mot de passe créé lors de l’exportation du certificat client.

Assurez-vous que le certificat client a été exporté dans un fichier .pfx avec la totalité de la chaîne du certificat (qui est la valeur par défaut). Dans le cas contraire, les informations du certificat racine ne sont pas présentes sur l’ordinateur client et le client ne pourra pas s’authentifier correctement.

Pour la procédure d’installation, consultez [Installer un certificat client](point-to-site-how-to-vpn-client-install-azure-cert.md).

## <a name="clientconfig"></a>9. Générer et installer le package de configuration du client VPN

Les fichiers de configuration du client VPN contiennent des paramètres pour configurer les appareils afin qu’ils puissent se connecter à un réseau virtuel via une connexion P2S. Pour obtenir des instructions permettant de générer et d’installer les fichiers de configuration du client VPN, consultez [Créer et installer les fichiers de configuration du client VPN pour les configurations P2S d’authentification par certificat Azure native](point-to-site-vpn-client-configuration-azure-cert.md).

## <a name="connect"></a>10. Connexion à Azure

### <a name="to-connect-from-a-windows-vpn-client"></a>Se connecter à partir d’un client VPN Windows

1. Pour vous connecter à votre réseau virtuel, sur l’ordinateur client, accédez aux connexions VPN et recherchez celle que vous avez créée. Elle porte le même nom que votre réseau virtuel. Cliquez sur **Connecter**. Un message contextuel faisant référence à l’utilisation du certificat peut s’afficher. Cliquez sur **Continuer** pour utiliser des privilèges élevés.

2. Dans la page de statut **Connexion**, cliquez sur **Connecter** pour démarrer la connexion. Si un écran **Sélectionner un certificat** apparaît, vérifiez que le certificat client affiché est celui que vous souhaitez utiliser pour la connexion. Dans le cas contraire, utilisez la flèche déroulante pour sélectionner le certificat approprié, puis cliquez sur **OK**.

  ![Connexion du client VPN à Azure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. Votre connexion est établie.

  ![Connexion établie](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshoot-windows-p2s-connections"></a>Résolution des problèmes liés aux connexions P2S Windows

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="to-connect-from-a-mac-vpn-client"></a>Pour se connecter à partir d’un client VPN Mac

À partir de la boîte de dialogue Réseau, recherchez le profil de client que vous souhaitez utiliser, puis cliquez sur **Connexion**.

  ![Connexion Mac](./media/vpn-gateway-howto-point-to-site-rm-ps/applyconnect.png)

## <a name="verify"></a>Pour vérifier votre connexion

Ces instructions s’appliquent aux clients Windows.

1. Pour vérifier que votre connexion VPN est active, ouvrez une invite de commandes avec élévation de privilèges, puis exécutez *ipconfig/all*.
2. Affichez les résultats. Notez que l’adresse IP que vous avez reçue est l’une des adresses du pool d’adresses de client VPN point à site que vous avez spécifiées dans votre configuration. Les résultats ressemblent à l’exemple qui suit :

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

## <a name="connectVM"></a>Se connecter à une machine virtuelle

Ces instructions s’appliquent aux clients Windows.

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>Pour ajouter ou supprimer des certificats racine approuvés

Vous pouvez ajouter et supprimer des certificats racines approuvés à partir d'Azure. Lorsque vous supprimez un certificat racine, les clients qui possèdent un certificat généré à partir de cette racine ne seront plus en mesure de s’authentifier, et donc de se connecter. Si vous souhaitez que des clients s’authentifient et se connectent, vous devez installer un nouveau certificat client généré à partir d’un certificat racine approuvé (téléchargé) dans Azure.

### <a name="to-add-a-trusted-root-certificate"></a>Ajout d’un certificat racine approuvé

Vous pouvez ajouter jusqu’à 20 fichiers .cer de certificat racine approuvés dans Azure. Pour obtenir des instructions, consultez la section [Télécharger un certificat racine approuvé](#uploadfile) dans cet article.

### <a name="to-remove-a-trusted-root-certificate"></a>Suppression d’un certificat racine approuvé

1. Pour supprimer un certificat racine approuvé, accédez à la page **Configuration Point à site** de votre passerelle de réseau virtuel.
2. Dans la section **Certificat racine** de la page, recherchez le certificat que vous souhaitez supprimer.
3. Cliquez sur le bouton de sélection correspondant au certificat, puis cliquez sur « Supprimer ».

## <a name="revokeclient"></a>Pour révoquer un certificat client

Vous pouvez révoquer des certificats clients. La liste de révocation de certificat vous permet de refuser sélectivement la connexion point à site en fonction des certificats clients individuels. Cela est différent de la suppression d’un certificat racine approuvé. Si vous supprimez un fichier .cer de certificat racine approuvé d’Azure, vous révoquez l’accès pour tous les certificats clients générés/signés par le certificat racine révoqué. Le fait de révoquer un certificat client plutôt que le certificat racine permet de continuer à utiliser les autres certificats générés à partir du certificat racine pour l’authentification.

La pratique courante consiste à utiliser le certificat racine pour gérer l'accès au niveaux de l'équipe ou de l'organisation, tout en utilisant des certificats clients révoqués pour le contrôle d'accès précis des utilisateurs individuels.

### <a name="revoke-a-client-certificate"></a>Révocation d'un certificat client

Vous pouvez révoquer un certificat client en ajoutant son empreinte à la liste de révocation.

1. Récupérez l’empreinte du certificat client. Pour plus d’informations, consultez l’article [Comment : récupérer l’empreinte numérique d’un certificat](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copiez les informations dans un éditeur de texte et supprimez tous les espaces afin d’obtenir une chaîne continue.
3. Accédez à la page **Configuration de point à site** de la passerelle de réseau virtuel. Il s’agit de la page que vous avez utilisé pour [charger un certificat racine approuvé](#uploadfile).
4. Dans la section **Certificats révoqués**, entrez un nom convivial pour le certificat (il ne s’agit pas forcément du nom commun du certificat).
5. Copiez et collez la chaîne d’empreinte numérique dans le champ **Empreinte**.
6. L’empreinte est validée, puis automatiquement ajoutée à la liste de révocation. Un message apparaît pour indiquer que la liste est en cours de mise à jour. 
7. Une fois la mise à jour terminée, le certificat ne peut plus être utilisé pour se connecter. Les clients qui tentent de se connecter à l’aide de ce certificat reçoivent un message indiquant que le certificat n’est plus valide.

## <a name="faq"></a>Forum Aux Questions sur les connexions point à site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-faq-p2s-azurecert-include.md)]

## <a name="next-steps"></a>étapes suivantes
Une fois la connexion achevée, vous pouvez ajouter des machines virtuelles à vos réseaux virtuels. Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). Pour plus d’informations sur la mise en réseau et les machines virtuelles, consultez [Vue d’ensemble du réseau de machines virtuelles Azure et Linux](../virtual-machines/linux/azure-vm-network-overview.md).
