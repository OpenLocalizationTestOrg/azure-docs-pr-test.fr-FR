---
title: "Connecter un réseau virtuel à ordinateur tooa à l’aide de l’authentification de Point-to-Site et le certificat : classique du portail Azure | Documents Microsoft"
description: "Connectez-vous en toute sécurité tooyour classique réseau virtuel Azure en créant une connexion de passerelle VPN Point à Site à l’aide de hello portail Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>Configurer un tooa de connexion de Point-to-Site réseau virtuel à l’aide de l’authentification par certificat (classiques) : portail Azure

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Cet article vous explique comment toocreate un réseau virtuel avec une connexion Point à Site à l’aide de modèle de déploiement classique hello hello portail Azure. Cette configuration utilise hello tooauthenticate de certificats client se connecte. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portail Azure (classique)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

Une passerelle VPN de Point-to-Site (P2S) vous permet de créer un réseau virtuel tooyour de connexion sécurisée à partir d’un ordinateur client. Connexions de point-to-Site VPN sont utiles lorsque vous souhaitez tooconnect tooyour réseau virtuel à partir d’un emplacement distant, par exemple lorsque vous sont télétravailleurs d’accueil ou d’une conférence. Un VPN P2S est également un toouse solution utile au lieu d’un VPN de Site à Site lorsque vous avez seulement quelques clients nécessitant tooconnect tooa réseau virtuel. 

P2S utilise hello Tunneling protocole SSTP (Secure Socket), qui est un protocole de VPN basée sur le protocole SSL. Un réseau VPN P2S est établie en le démarrant à partir de l’ordinateur client de hello.


![Diagramme point à site](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


Connexions d’authentification de certificat de point-to-Site exiger les éléments de hello :

* Une passerelle VPN dynamique.
* Hello clé publique (fichier .cer) pour un certificat racine, qui est téléchargé tooAzure. Ce certificat est considéré comme un certificat approuvé et est utilisé pour l’authentification.
* Un certificat client généré à partir du certificat racine de hello et installé sur chaque ordinateur client qui se connecte. Ce certificat est utilisé pour l’authentification du client.
* Un package de configuration du client VPN doit être généré et installé sur chaque ordinateur client qui se connecte. package de configuration client Hello configure un client VPN natif hello qui existe déjà sur le système d’exploitation hello hello informations nécessaires tooconnect toohello réseau virtuel.

Les connexions point à site ne nécessitent pas de périphérique VPN ou d’adresse IP publique locale. Hello connexion VPN est créée sur SSTP (Secure Socket Tunneling Protocol). Sur le côté du serveur hello, nous prenons en charge les versions 1.0, 1.1 et 1.2 de SSTP. client de Hello décide quelle toouse de version. Pour Windows 8.1 et supérieur, SSTP utilise la version 1.2 par défaut. 

Pour plus d’informations sur les connexions de Point-to-Site, consultez hello [Point-to-Site FAQ](#faq) à fin hello de cet article.

### <a name="example-settings"></a>Exemples de paramètres

Vous pouvez utiliser hello suivant de valeurs toocreate un environnement de test, ou consultez les valeurs toothese toobetter comprendre les exemples hello dans cet article :

* **Nom : VNet1**
* **Espace d’adressage : 192.168.0.0/16**<br>Pour cet exemple, nous n’utilisons qu’un seul espace d’adressage. Vous pouvez avoir plusieurs espaces d’adressage pour votre réseau virtuel.
* **Nom du sous-réseau : FrontEnd**
* **Plage d’adresses de sous-réseau : 192.168.1.0/24**
* **L’abonnement :** si vous avez plusieurs abonnements, vérifiez que vous utilisez hello correct.
* **Groupe de ressources : TestRG**
* **Emplacement : États-Unis de l’Est**
* **Type de connexion : point à site**
* **Espace d’adressage du client : 172.16.201.0/24**. Les clients VPN qui se connectent toohello virtuel à l’aide de cette connexion Point-to-Site reçoit une adresse IP à partir de hello pool spécifié.
* **Sous-réseau de passerelle : 192.168.200.0/24**. sous-réseau de passerelle Hello doit utiliser le nom de hello « GatewaySubnet ».
* **Taille :** passerelle de hello sélectionnez référence (SKU) que vous souhaitez toouse.
* **Type de routage : dynamique**

## <a name="vnetvpn"></a>1. créer un réseau virtuel et une passerelle VPN ;

Avant de commencer, assurez-vous que vous disposez d’un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial).

### <a name="createvnet"></a>Partie 1 : création d’un réseau virtuel

Si vous n’avez pas de réseau virtuel, créez-en un. Les captures d’écran sont fournies à titre d’exemple. Être des valeurs de hello tooreplace que par les vôtres. un réseau virtuel à l’aide de toocreate hello portail Azure, hello utilisation comme suit :

1. À partir d’un navigateur, accédez à toohello [portail Azure](http://portal.azure.com) et, si nécessaire, connectez-vous à votre compte Azure.
2. Cliquez sur **Nouveau**. Bonjour **marketplace de hello recherche** , tapez « Réseau virtuel ». Recherchez **réseau virtuel** hello retourné à partir de liste et cliquez sur tooopen hello **réseau virtuel** page.

  ![Rechercher la page du réseau virtuel](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Bas hello de page de réseau virtuel hello, à partir de hello **sélectionner un modèle de déploiement** , sélectionnez **classique**, puis cliquez sur **créer**.

  ![Sélectionner le modèle de déploiement](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. Sur hello **créer un réseau virtuel** page, de configurer les paramètres de réseau virtuel hello. Sur cette page, vous ajoutez votre premier espace d’adressage et une plage d’adresses de sous-réseau unique. Après avoir terminé la création de hello réseau virtuel, vous pouvez revenir en arrière et ajouter des espaces d’adressage et des sous-réseaux supplémentaires.

  ![Créer une page Réseau virtuel](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. Vérifiez que hello **abonnement** est hello correct. Vous pouvez modifier des abonnements à l’aide de hello de liste déroulante.
6. Cliquez sur **Groupe de ressources** et sélectionnez un groupe de ressources existant, ou créez un groupe de ressources en tapant un nom pour ce dernier. Si vous créez un nouveau groupe de ressources, groupe de ressources nom hello selon tooyour planifié des valeurs de configuration. Pour plus d’informations sur les groupes de ressources, consultez [Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Ensuite, sélectionnez hello **emplacement** paramètres pour votre réseau virtuel. emplacement de Hello détermine où se trouvera ressources hello que vous déployez toothis réseau virtuel.
8. Sélectionnez **code confidentiel toodashboard** si vous souhaitez toofind en mesure de toobe votre réseau virtuel facilement sur le tableau de bord hello, puis cliquez sur **créer**.

  ![Code confidentiel toodashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. Après avoir cliqué sur Créer, une vignette s’affiche dans votre tableau de bord reflète progression hello de votre réseau virtuel. modifications vignette Hello hello réseau virtuel est en cours de création.

  ![Mosaïque de création du réseau virtuel](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. Une fois votre réseau virtuel a été créé, vous voyez **créé** répertoriés sous **état** sur la page réseaux hello hello portail Azure classic.
11. Ajoutez un serveur DNS (facultatif). Après avoir créé votre réseau virtuel, vous pouvez ajouter l’adresse IP de hello d’un serveur DNS pour la résolution de nom. Hello adresse IP du serveur DNS que vous spécifiez doit être hello d’un serveur DNS peut résoudre les noms de hello pour les ressources hello dans votre réseau virtuel.<br>tooadd un serveur DNS, ouvrez les paramètres de hello pour votre réseau virtuel, cliquez sur serveurs DNS et ajouter l’adresse IP de hello du serveur DNS de hello que vous souhaitez toouse.

### <a name="gateway"></a>Partie 2 : création d’un sous-réseau de passerelle et d’une passerelle de routage dynamique

Vous allez maintenant créer un sous-réseau de passerelle et une passerelle de routage dynamique. Bonjour portail Azure pour le modèle de déploiement classique de hello, création de sous-réseau de passerelle hello et passerelle de hello peut être effectuée via hello même les pages de configuration.

1. Dans le portail de hello, accédez toohello de réseau virtuel pour lequel vous souhaitez toocreate une passerelle.
2. Sur la page hello pour votre réseau virtuel, sur hello **vue d’ensemble** page, dans la section de connexions VPN hello, cliquez sur **passerelle**.

  ![Cliquez sur toocreate une passerelle](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. Sur hello **nouvelle connexion VPN** page, sélectionnez **Point-to-site**.

  ![Type de connexion de point à site](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. Pour **espace d’adressage Client**, ajoutez la plage d’adresses IP hello. Il s’agit de plage hello à partir de laquelle hello clients VPN recevront une adresse IP lors de la connexion. Utilisez une plage d’adresses IP privées qui ne chevauche pas emplacement local hello auxquels vous vous connecterez à partir d’ou avec hello réseau virtuel que vous souhaitez tooconnect à. Vous pouvez supprimer la plage de remplissage automatique de hello, puis ajouter hello privé plage d’adresses IP que vous souhaitez toouse.

  ![Espace d’adressage du client](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. Sélectionnez hello **créer une passerelle immédiatement** case à cocher.

  ![Créer une passerelle immédiatement](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. Cliquez sur **configuration de la passerelle facultatif** tooopen hello **configuration de la passerelle** page.

  ![Cliquer sur Configuration de passerelle facultative](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. Cliquez sur **sous-réseau configurer les paramètres requis** tooadd hello **sous-réseau de passerelle**. Bien qu’il soit possible de toocreate un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus grand qui inclut plusieurs adresses en sélectionnant au moins /28 ou /27. Cette opération permettra suffisamment adresses tooaccommodate possibles des configurations supplémentaires que vous pouvez Bonjour futures. Lorsque vous travaillez avec des sous-réseaux de passerelle, évitez d’association d’un sous-réseau de passerelle de réseau sécurité (groupe) toohello. Association d’un sous-réseau de toothis de groupe de sécurité réseau risque de votre toostop de passerelle VPN fonctionne comme prévu.

  ![Ajouter le sous-réseau de passerelle](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. Passerelle de hello sélectionnez **taille**. taille de Hello est passerelle hello référence (SKU) pour votre passerelle de réseau virtuel. Dans le portail hello, hello référence (SKU) par défaut est **base**. Pour plus d’informations sur les références de passerelle, consultez [À propos des paramètres de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

  ![Taille de la passerelle](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. Sélectionnez hello **Type de routage** pour votre passerelle. Les configurations P2S nécessitent un type de routage **dynamique**. Cliquez sur **OK** lorsque vous avez terminé la configuration de cette page.

  ![Configurer le type de routage](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. Sur hello **nouvelle connexion VPN** , cliquez sur **OK** bas hello hello toobegin de page Création de votre passerelle de réseau virtuel. Une passerelle VPN peut prendre jusqu'à too45 minutes toocomplete, en fonction de la référence de passerelle hello que vous sélectionnez.

## <a name="generatecerts"></a>2. Créer des certificats

Certificats sont utilisés par les clients VPN tooauthenticate Azure pour Point-to-Site VPN. Télécharger des informations de clé publique hello de tooAzure de certificat racine hello. clé publique de Hello est alors considéré comme « approuvé ». Les certificats clients doivent être générés à partir du certificat racine approuvé de hello et installés sur chaque ordinateur client dans le magasin de certificats d’utilisateur de certificats-actuel/personnel hello. certificat de Hello est client de hello tooauthenticate utilisée lorsqu’elle initie un toohello de connexion réseau virtuel. 

Si vous utilisez des certificats auto-signés, ceux-ci doivent être créés à l’aide de paramètres spécifiques. Vous pouvez créer un certificat auto-signé à l’aide d’instructions hello pour [PowerShell et Windows 10](vpn-gateway-certificates-point-to-site.md), ou [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Il est important de suivre les étapes de hello dans ces instructions lors de l’utilisation des certificats racines auto-signés et de générer des certificats de client à partir de certificat racine auto-signé hello. Sinon, les certificats hello que vous créez ne sera pas compatibles avec les connexions P2S et vous recevrez une erreur de connexion.

### <a name="cer"></a>Partie 1 : Obtenir la clé publique de hello (.cer) pour le certificat racine de hello

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>Partie 2 : génération d’un certificat client

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Télécharger le fichier du certificat .cer hello racine

Une fois la passerelle de hello a été créé, vous pouvez télécharger le fichier de .cer hello (qui contient les informations de clé publique hello) pour un tooAzure de certificat racine de confiance. Vous ne téléchargez pas de clé privée hello pour tooAzure de certificat racine hello. Une fois a.cer fichier est téléchargé, Azure peut utiliser tooauthenticate les clients qui ont installé un certificat de client généré à partir du certificat racine approuvé de hello. Vous pouvez télécharger les fichiers de certificat racine de confiance supplémentaires - tooa total de 20 - ultérieurement, si nécessaire.  

1. Sur hello **connexions VPN** section de page hello pour votre réseau virtuel, cliquez sur hello **clients** tooopen graphique hello **Point-to-site VPN connexion** page.

  ![Clients](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Sur hello **connexiondePointàsite** , cliquez sur **gérer les certificats** tooopen hello **certificats** page.<br>

  ![Page Certificats](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Sur hello **certificats** , cliquez sur **télécharger** tooopen hello **télécharger le certificat** page.<br>

    ![Page Télécharger des certificats](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Cliquez sur toobrowse graphique de dossier hello pour le fichier .cer de hello. Sélectionnez le fichier de hello, puis cliquez sur **OK**. Actualisation hello page toosee hello téléchargé certificat sur hello **certificats** page.

  ![Téléchargement d’un certificat](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Configurer hello client

tooconnect tooa virtuel à l’aide d’un VPN de Point-to-Site, chaque client doit installer un client VPN Windows natif package tooconfigure hello. package de configuration Hello configure un client VPN Windows natif de hello avec un réseau virtuel hello paramètres nécessaires tooconnect toohello.

Vous pouvez utiliser hello même configuration du client VPN le package sur chaque ordinateur client, tant que la version de hello correspond à l’architecture hello pour les clients hello. Pour hello de la liste des systèmes d’exploitation client pris en charge, consultez hello [ForumauxquestionssurlesconnexionsPointàSite](#faq) à fin hello de cet article.

### <a name="generateconfigpackage"></a>Partie 1 : Générer et installer le package de configuration de client VPN hello

1. Bonjour portail Azure, Bonjour **vue d’ensemble** page de votre réseau virtuel, **connexions VPN**, cliquez sur les messages hello du graphique tooopen hello client **Point-to-site VPN connexion** page.
2. En haut de hello Hello **Point-to-site VPN connexion** , cliquez sur le package de téléchargement hello correspondant du système d’exploitation de toohello client sur lequel il sera installé :

  * Pour les clients 64 bits, sélectionnez **Client VPN (64 bits)**.
  * Pour les clients 32 bits, sélectionnez **Client VPN (32 bits)**.

  ![Charger le package de configuration du client VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. Une fois que hello empaquetée génère, télécharger et l’installer sur votre ordinateur client. Si une fenêtre contextuelle SmartScreen s’affiche, cliquez sur **Plus d’infos**, puis sur **Exécuter quand même**. Vous pouvez également enregistrer hello package tooinstall sur d’autres ordinateurs client.

### <a name="installclientcert"></a>Partie 2 : Installer le certificat client hello

Si vous voulez toocreate un P2S à partir d’un ordinateur client autre que hello celle que vous avez utilisé des certificats de client de hello toogenerate, vous devez tooinstall un certificat client. Lorsque vous installez un certificat client, vous avez besoin d’un mot de passe hello créé lors de l’exportation du certificat client hello. En règle générale, il s’agit simplement en double-cliquant sur le certificat de hello et l’installer. Pour plus d’informations, consultez la rubrique [Installer un certificat client exporté](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>5. Se connecter tooAzure

### <a name="connect-tooyour-vnet"></a>Se connecter tooyour réseau virtuel

1. tooconnect tooyour réseau virtuel, sur l’ordinateur client de hello, accédez tooVPN connexions et trouver la connexion VPN hello que vous avez créé. Il est nommé hello même nom que votre réseau virtuel. Cliquez sur **Connecter**. Un message peut apparaître qui fait référence le certificat de hello toousing. Si cela se produit, cliquez sur **continuer** toouse des privilèges élevés.
2. Sur hello **connexion** page d’état, cliquez sur **Connect** connexion de hello toostart. Si vous voyez un **sélectionner un certificat** écran, vérifiez que hello certificat client affiché est hello une que vous souhaitez toouse tooconnect. Si elle n’est pas le cas, utilisez bon certificat hello flèche tooselect hello, puis cliquez sur **OK**.

  ![Connexion client VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. Votre connexion est établie.

  ![Connexion établie](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Résolution des problèmes liés aux connexions P2S

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Vérifiez la connexion VPN de hello

1. tooverify que votre connexion VPN est active, ouvrez une invite de commandes avec élévation de privilèges et exécutez *ipconfig/all*.
2. Afficher les résultats hello. Notez que vous avez reçu d’adresseIP hello est une des adresses hello au sein de la plage d’adresses de connectivité hello Point-to-Site que vous avez spécifié lorsque vous avez créé votre réseau virtuel. les résultats de Hello doivent être similaires toothis exemple :

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Connecter l’ordinateur virtuel de tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>Ajout ou suppression de certificats racine approuvés

Vous pouvez ajouter et supprimer des certificats racines approuvés à partir d'Azure. Lorsque vous supprimez un certificat racine, les clients qui possèdent un certificat généré à partir de cette racine ne seront pas en mesure de tooauthenticate et par conséquent ne sera pas en mesure de tooconnect. Si vous souhaitez un tooauthenticate client et vous connecter, vous devez tooinstall un nouveau certificat de client généré à partir d’un certificat racine approuvé tooAzure (téléchargé).

### <a name="addtrustedroot"></a>tooadd un certificat racine approuvé

Vous pouvez ajouter jusqu'à tooAzure de fichiers too20 approuvé racine certificat .cer. Pour obtenir des instructions, consultez [Section 3 - fichier .cer du certificat racine téléchargement hello](#upload).

### <a name="removetrustedroot"></a>tooremove un certificat racine approuvé

1. Sur hello **connexions VPN** section de page hello pour votre réseau virtuel, cliquez sur hello **clients** tooopen graphique hello **Point-to-site VPN connexion** page.

  ![Clients](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Sur hello **connexiondePointàsite** , cliquez sur **gérer les certificats** tooopen hello **certificats** page.<br>

  ![Page Certificats](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Sur hello **certificats** , cliquez sur hello sélection suivant toohello certificat que vous souhaitez tooremove, puis cliquez sur **supprimer**.

  ![Suppression d'un certificat racine](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>Révocation d'un certificat client

Vous pouvez révoquer des certificats clients. certificat Hello liste de révocation vous permet de tooselectively refuser la connectivité de Point à Site basée sur des certificats clients individuels. Cela est différent de la suppression d’un certificat racine approuvé. Si vous supprimez un .cer du certificat racine approuvé à partir d’Azure, il révoque l’accès de hello pour tous les certificats du client généré/signé par le certificat racine révoqués de hello. Révoquer un certificat client, au lieu de certificat racine hello permet hello autres certificats générés à partir de hello racine certificat toocontinue toobe utilisé pour l’authentification de connexion de Point à Site hello.

courant Hello est toouse hello racine certificat toomanage l’accès aux niveaux d’équipe ou organisation, lors de l’utilisation des certificats clients révoqués de contrôle d’accès précis sur les utilisateurs individuels.

### <a name="revokeclientcert"></a>toorevoke un certificat client

Vous pouvez révoquer un certificat client en ajoutant la liste de révocation toohello hello l’empreinte numérique.

1. Récupérer l’empreinte de certificat client hello. Pour plus d’informations, consultez [Comment : récupérer hello empreinte d’un certificat](https://msdn.microsoft.com/library/ms734695.aspx).
2. Éditeur de texte hello informations tooa de copie et supprimer tous les espaces afin qu’il soit une chaîne continue.
3. Accédez toohello **'nom de réseau virtuel classique' > connexion Point-to-site VPN > certificats** page, puis cliquez sur **liste de révocation** page de liste de révocation tooopen hello. 
4. Sur hello **liste de révocation** , cliquez sur **+ ajouter un certificat** tooopen hello **liste toorevocation de certificat ajouter** page.
5. Sur hello **liste toorevocation de certificat ajouter** page, collez l’empreinte numérique du certificat hello comme une ligne continue de texte, sans espaces. Cliquez sur **OK** bas hello de page de hello.
6. Une fois la mise à jour terminée, les certificats hello ne peuvent plus être utilisé tooconnect. Les clients qui tentent de tooconnect à l’aide de ce certificat recevoir un message indiquant que ce certificat hello n’est plus valide.

## <a name="faq"></a>Forum Aux Questions sur les connexions point à site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Étapes suivantes
Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand en savoir plus sur la mise en réseau et les machines virtuelles, consultez [vue d’ensemble du réseau Azure et Linux VM](../virtual-machines/linux/azure-vm-network-overview.md).
