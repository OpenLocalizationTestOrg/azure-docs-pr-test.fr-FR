---
title: "Se connecter à un réseau virtuel Azure à l’aide de Point-to-Site de tooan ordinateur et l’authentification des certificats : PowerShell | Documents Microsoft"
description: "Connectez-vous en toute sécurité un réseau virtuel d’ordinateurs tooyour en créant une connexion de passerelle VPN Point à Site à l’aide de l’authentification par certificat. Cet article s’applique le modèle de déploiement du Gestionnaire de ressources toohello et utilise PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>Configurer un tooa de connexion de Point-to-Site réseau virtuel à l’aide de l’authentification par certificat : PowerShell

Cet article vous explique comment toocreate un réseau virtuel avec une connexion Point à Site dans le déploiement du Gestionnaire de ressources hello modèle à l’aide de PowerShell. Cette configuration utilise hello tooauthenticate de certificats client se connecte. Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portail Azure (classique)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Une passerelle VPN de Point-to-Site (P2S) vous permet de créer un réseau virtuel tooyour de connexion sécurisée à partir d’un ordinateur client. Connexions de point-to-Site VPN sont utiles lorsque vous souhaitez tooconnect tooyour réseau virtuel à partir d’un emplacement distant, par exemple lorsque vous sont télétravailleurs d’accueil ou d’une conférence. Un VPN P2S est également un toouse solution utile au lieu d’un VPN de Site à Site lorsque vous avez seulement quelques clients nécessitant tooconnect tooa réseau virtuel.

P2S utilise hello Tunneling protocole SSTP (Secure Socket), qui est un protocole de VPN basée sur le protocole SSL. Un réseau VPN P2S est établie en le démarrant à partir de l’ordinateur client de hello.

![Se connecter à un réseau virtuel Azure - diagramme de connexions de Point-to-Site de tooan ordinateur](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

Connexions d’authentification de certificat de point-to-Site exiger les éléments de hello :

* Une passerelle VPN RouteBased.
* Hello clé publique (fichier .cer) pour un certificat racine, qui est téléchargé tooAzure. Une fois que le certificat de hello est téléchargé, il est considéré comme un certificat approuvé et est utilisé pour l’authentification.
* Un certificat de client qui est généré à partir du certificat racine de hello et installé sur chaque ordinateur client qui se connectera toohello réseau virtuel. Ce certificat est utilisé pour l’authentification du client.
* Un package de configuration du client VPN. package de configuration de client VPN Hello contient des informations nécessaires de hello pour hello client tooconnect toohello réseau virtuel. Hello configure hello VPN client existant est natif toohello système d’exploitation Windows. Chaque client qui se connecte doit être configuré à l’aide du package de configuration hello.

Les connexions point à site ne nécessitent pas de périphérique VPN ou d’adresse IP publique locale. Hello connexion VPN est créée sur SSTP (Secure Socket Tunneling Protocol). Sur le côté du serveur hello, nous prenons en charge les versions 1.0, 1.1 et 1.2 de SSTP. client de Hello décide quelle toouse de version. Pour Windows 8.1 et supérieur, SSTP utilise la version 1.2 par défaut. 

Pour plus d’informations sur les connexions de Point-to-Site, consultez hello [Point-to-Site FAQ](#faq) à fin hello de cet article.

## <a name="before-beginning"></a>Avant tout chose

* Assurez-vous de disposer d’un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial).
* Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure. Pour plus d’informations sur l’installation des applets de commande PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

### <a name="example"></a>Exemples de valeurs

Vous pouvez utiliser toocreate de valeurs d’exemple hello un environnement de test, ou consultez les valeurs toothese toobetter comprendre les exemples hello dans cet article. Nous avons défini les variables hello dans la section [1](#declare) de l’article de hello. Vous pouvez utiliser les étapes de hello comme une procédure pas à pas et utilisez les valeurs hello sans les modifier ou les modifier tooreflect votre environnement. 

* **Nom : VNet1**
* **Espace d’adressage :192.168.0.0/16** et **10.254.0.0/16**<br>Pour cet exemple, nous utilisons plusieurs tooillustrate espace adresse que cette configuration fonctionne avec plusieurs espaces d’adressage. Toutefois, plusieurs espaces d’adressage ne sont pas nécessaires pour cette configuration.
* **Nom du sous-réseau : FrontEnd**
  * **Plage d’adresses de sous-réseau : 192.168.1.0/24**
* **Nom du sous-réseau : BackEnd**
  * **Plage d’adresses de sous-réseau : 10.254.1.0/24**
* **Nom du sous-réseau : GatewaySubnet**<br>nom du sous-réseau Hello *GatewaySubnet* est obligatoire pour toowork de passerelle VPN hello.
  * **Plage d’adresses de GatewaySubnet : 192.168.200.0/24** 
* **Pool d’adresses des clients VPN : 172.16.201.0/24**<br>Clients VPN qui se connectent toohello virtuel à l’aide de cette connexion Point-to-Site recevront une adresse IP à partir de hello pool d’adresses VPN client.
* **L’abonnement :** si vous avez plusieurs abonnements, vérifiez que vous utilisez hello correct.
* **Groupe de ressources : TestRG**
* **Emplacement : États-Unis de l’Est**
* **Serveur DNS : Adresse IP** du serveur DNS de hello que vous souhaitez toouse pour la résolution de nom.
* **Nom de passerelle : Vnet1GW**
* **Nom d’adresse IP publique : VNet1GWPIP**
* **Type de VPN : RouteBased** 

## <a name="declare"></a>1. Connexion et définition des variables

Dans cette section, vous connectez et déclarez les valeurs hello utilisées pour cette configuration. Hello déclaré valeurs sont utilisées dans les exemples de scripts hello. Modifier hello valeurs tooreflect votre propre environnement. Ou bien, vous pouvez utiliser hello déclaré de valeurs et suivez les étapes de hello en guise d’exercice.

1. Ouvrez la console PowerShell avec des privilèges élevés, puis connectez-vous à tooyour compte Azure. Cette applet de commande vous invite à entrer les informations d’identification de hello. Une fois connecté, il télécharge les paramètres de votre compte afin qu’ils soient disponible tooAzure PowerShell.

  ```powershell
  Login-AzureRmAccount
  ```
2. Obtenez la liste de vos abonnements Azure.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Spécifiez un abonnement hello que vous souhaitez toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. Déclarez les variables hello que vous souhaitez toouse. Utilisez hello suivant l’exemple, en remplaçant les valeurs hello pour votre propre lorsque cela est nécessaire.

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2. Configurer un réseau virtuel

1. Créez un groupe de ressources.

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. Créer des configurations de sous-réseau de réseau virtuel hello, nommant hello *frontal*, *principal*, et *GatewaySubnet*. Ces préfixes doivent faire partie de hello espace d’adressage de réseau virtuel que vous avez déclaré.

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. Créer un réseau virtuel de hello.

  Dans cet exemple, le serveur DNS de hello est facultative. La définition d’une valeur n’entraîne pas la création de serveur DNS. Hello adresse IP du serveur DNS que vous spécifiez doit être un serveur DNS peut résoudre les noms de hello pour les ressources hello que vous êtes connecté. Pour cet exemple, nous avons utilisé une adresse IP privée, mais il est probable qu’il ne s’agit pas d’adresse IP de hello de votre serveur DNS. Être toouse que vos propres valeurs.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. Spécifiez les variables hello pour le réseau virtuel de hello que vous avez créé.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. Une passerelle VPN doit avoir une adresse IP publique. Votre ressource d’adresse IP hello d’abord demander, puis consultez tooit lors de la création de votre passerelle de réseau virtuel. adresse IP de Hello est attribué dynamiquement les ressources toohello lors de la création de la passerelle VPN de hello. Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*. Vous ne pouvez pas demander d’affectation d’adresse IP publique statique. Toutefois, cela ne signifie pas que l’adresse IP de hello change après que qu’elle a été affectée passerelle VPN de tooyour. Hello seule fois changements d’adresses IP publiques hello est hello lorsque la passerelle est supprimé et recréé. Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.

  Demandez une adresse IP publique attribuée dynamiquement.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3. Créer une passerelle VPN de hello

Configurez et créez la passerelle de réseau virtuel hello pour votre réseau virtuel.

* Hello *- le type de passerelle* doit être **Vpn** et hello *- VpnType* doit être **RouteBased**.
* Une passerelle VPN peut prendre jusqu'à too45 minutes toocomplete, en fonction de hello [référence (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md) vous sélectionnez.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4. Ajouter un pool d’adresses client VPN hello

Passerelle VPN de hello après création, vous pouvez ajouter un pool d’adresses client VPN hello. Hello pool d’adresses VPN client est plage hello à partir de laquelle hello clients VPN recevront une adresse IP lors de la connexion. Utilisez une plage d’adresses IP privées qui ne chevauche pas emplacement hello local auquel vous vous connectez à partir d’ou avec hello réseau virtuel que vous souhaitez tooconnect à. Dans cet exemple, hello pool d’adresses VPN client est déclaré comme un [variable](#declare) à l’étape 1.

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5. Générer des certificats

Certificats sont utilisés par les clients VPN tooauthenticate Azure pour Point-to-Site VPN. Télécharger des informations de clé publique hello de tooAzure de certificat racine hello. clé publique de Hello est alors considéré comme « approuvé ». Les certificats clients doivent être générés à partir du certificat racine approuvé de hello et installés sur chaque ordinateur client dans le magasin de certificats d’utilisateur de certificats-actuel/personnel hello. certificat de Hello est client de hello tooauthenticate utilisée lorsqu’elle initie un toohello de connexion réseau virtuel. 

Si vous utilisez des certificats auto-signés, ceux-ci doivent être créés à l’aide de paramètres spécifiques. Vous pouvez créer un certificat auto-signé à l’aide d’instructions hello pour [PowerShell et Windows 10](vpn-gateway-certificates-point-to-site.md), ou, si vous n’avez pas Windows 10, vous pouvez utiliser [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Il est important de suivre les étapes de hello dans les instructions hello lors de la génération des certificats racines auto-signés et les certificats clients. Sinon, vous générez des certificats hello ne sera pas compatibles avec les connexions P2S et vous recevrez une erreur de connexion.

### <a name="cer"></a>1. Obtenir le fichier .cer hello pour le certificat racine de hello

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2. Générer un certificat client

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6. Télécharger les informations clé publique de certificat racine hello

Vérifiez que votre passerelle VPN a terminé la création. Une fois terminée, vous pouvez télécharger le fichier de .cer hello (qui contient les informations de clé publique hello) pour un tooAzure de certificat racine de confiance. Une fois a.cer fichier est téléchargé, Azure peut utiliser tooauthenticate les clients qui ont installé un certificat de client généré à partir du certificat racine approuvé de hello. Vous pouvez télécharger les fichiers de certificat racine de confiance supplémentaires - tooa total de 20 - ultérieurement, si nécessaire.

1. Déclarer la variable hello pour votre nom de certificat, en remplaçant la valeur de hello avec vos propres.

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. Remplacez le chemin d’accès du fichier hello avec vos propres, puis exécutez les applets de commande hello.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. Téléchargez tooAzure des informations de clé publique hello. Une fois les informations de certificat hello sont téléchargées, Azure considère que cette toobe un certificat racine approuvé.

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7. Télécharger le package de configuration de client VPN hello

tooconnect tooa virtuel à l’aide d’un VPN de Point-to-Site, chaque client doit installer un package de configuration de client qui configure le client VPN natif de hello avec des paramètres de hello et les fichiers qui sont le réseau virtuel de toohello tooconnect nécessaire. package de configuration de client VPN Hello configure client VPN Windows natif de hello, il n’installe pas un client VPN nouveaux ou différent. 

Vous pouvez utiliser hello même configuration du client VPN le package sur chaque ordinateur client, tant que la version de hello correspond à l’architecture hello pour les clients hello. Pour hello de la liste des systèmes d’exploitation client pris en charge, consultez hello [ForumauxquestionssurlesconnexionsPointàSite](#faq) à fin hello de cet article.

1. Une fois la passerelle de hello a été créé, vous pouvez générer et télécharger le package de configuration client hello. Cet exemple télécharge le package de hello pour les clients 64 bits. Si vous souhaitez que les clients de toodownload hello 32 bits, remplacez « Amd64 » par « x86 ». Vous pouvez également télécharger le client VPN de hello à l’aide de hello portail Azure.

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. Copiez et collez le lien hello renvoyé tooa navigateur toodownload hello package web, en prenant soin de guillemets de hello tooremove entourant le lien de hello. 
3. Téléchargez et installez le package de hello sur l’ordinateur client de hello. Si une fenêtre contextuelle SmartScreen s’affiche, cliquez sur **Plus d’infos**, puis sur **Exécuter quand même**. Vous pouvez également enregistrer hello package tooinstall sur d’autres ordinateurs client.
4. Sur l’ordinateur client de hello, accédez trop**paramètres réseau** et cliquez sur **VPN**. Hello connexion VPN affiche le nom hello du réseau virtuel hello auquel il se connecte.

## <a name="clientcertificate"></a>8. Installer un certificat client exporté

Si vous voulez toocreate un P2S à partir d’un ordinateur client autre que hello celle que vous avez utilisé des certificats de client de hello toogenerate, vous devez tooinstall un certificat client. Lorsque vous installez un certificat client, vous avez besoin d’un mot de passe hello créé lors de l’exportation du certificat client hello. En règle générale, il est simplement en double-cliquant sur le certificat de hello et l’installer.

Assurez-vous que le certificat de client hello a été exporté dans un fichier .pfx, ainsi que la chaîne de certificat entière hello (qui est la valeur par défaut hello). Dans le cas contraire, informations relatives au certificat racine hello n’est pas présents sur l’ordinateur client de hello et hello client ne sera pas en mesure de tooauthenticate correctement. Pour plus d’informations, consultez la rubrique [Installer un certificat client exporté](vpn-gateway-certificates-point-to-site.md#install). 

## <a name="connect"></a>9. Se connecter tooAzure

1. tooconnect tooyour réseau virtuel, sur l’ordinateur client de hello, accédez tooVPN connexions et trouver la connexion VPN hello que vous avez créé. Il est nommé hello même nom que votre réseau virtuel. Cliquez sur **Connecter**. Un message peut apparaître qui fait référence le certificat de hello toousing. Cliquez sur **continuer** toouse des privilèges élevés. 
2. Sur hello **connexion** page d’état, cliquez sur **Connect** connexion de hello toostart. Si vous voyez un **sélectionner un certificat** écran, vérifiez que hello certificat client affiché est hello une que vous souhaitez toouse tooconnect. Si elle n’est pas le cas, utilisez bon certificat hello flèche tooselect hello, puis cliquez sur **OK**.

  ![Client VPN connecte tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. Votre connexion est établie.

  ![Connexion établie](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Résolution des problèmes liés aux connexions P2S

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10. Vérifier votre connexion

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

## <a name="addremovecert"></a>Ajouter ou supprimer un certificat racine

Vous pouvez ajouter et supprimer des certificats racines approuvés à partir d'Azure. Lorsque vous supprimez un certificat racine, les clients qui possèdent un certificat généré à partir du certificat racine de hello ne peut pas authentifier et ne pourra plus être en mesure de tooconnect. Si vous souhaitez un tooauthenticate client et vous connecter, vous devez tooinstall un nouveau certificat de client généré à partir d’un certificat racine approuvé tooAzure (téléchargé).

### <a name="addtrustedroot"></a>tooadd un certificat racine approuvé

Vous pouvez ajouter jusqu'à tooAzure de fichiers too20 racine certificat .cer. les étapes suivantes de Hello aide vous ajoutez un certificat racine :

#### <a name="certmethod1"></a>Méthode 1

Il s’agit de tooupload de méthode la plus efficace hello un certificat racine.

1. Préparer tooupload de fichier .cer hello :

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Téléchargez le fichier de hello. Vous ne pouvez charger qu’un seul fichier à la fois.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. tooverify ce fichier de certificat hello téléchargés :

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>Méthode 2

Cette méthode est a davantage d’étapes que la méthode 1, mais a hello même résultat. Il est inclus en cas de besoin des données du certificat tooview hello.

1. Créer et préparer hello nouvelle racine certificat tooadd tooAzure. Exporter la clé publique de hello comme Base-64 encodé X.509 (. CER) et ouvrez-le dans un éditeur de texte. Copiez les valeurs hello, comme indiqué dans hello l’exemple suivant :

  ![certificat](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > Lors de la copie des données de certificat hello, assurez-vous que vous copiez le texte hello ligne continue sans les retours chariot ou les sauts de ligne. Vous devrez peut-être toomodify votre affichage dans too'Show de l’éditeur de texte hello symbole/Afficher chariot de tous les caractères toosee hello retourne et sauts de ligne.
  >
  >

2. Spécifiez le nom du certificat hello et les informations de clé en tant que variable. Remplacez les informations de hello avec vos propres, comme indiqué dans hello exemple suivant :

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. Ajouter un nouveau certificat racine de hello. Vous ne pouvez ajouter qu’un seul certificat à la fois.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. Vous pouvez vérifier qu’hello un nouveau certificat a été ajouté correctement à l’aide de hello l’exemple suivant :

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove un certificat racine

1. Déclarer des variables de hello.

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. Supprimer le certificat de hello.

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. Hello utilisation suivant tooverify exemple qui hello certificat a été correctement supprimé.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>Révocation d'un certificat client

Vous pouvez révoquer des certificats clients. certificat Hello liste de révocation vous permet de tooselectively refuser la connectivité de Point à Site basée sur des certificats clients individuels. Cela est différent de la suppression d’un certificat racine approuvé. Si vous supprimez un .cer du certificat racine approuvé à partir d’Azure, il révoque l’accès de hello pour tous les certificats du client généré/signé par le certificat racine révoqués de hello. Révoquer un certificat client, au lieu de certificat racine hello permet hello autres certificats générés à partir de hello racine certificat toocontinue toobe utilisé pour l’authentification.

courant Hello est toouse hello racine certificat toomanage l’accès aux niveaux d’équipe ou organisation, lors de l’utilisation des certificats clients révoqués de contrôle d’accès précis sur les utilisateurs individuels.

### <a name="revokeclientcert"></a>toorevoke un certificat client

1. Récupérer l’empreinte de certificat client hello. Pour plus d’informations, consultez [comment tooretrieve hello empreinte d’un certificat](https://msdn.microsoft.com/library/ms734695.aspx).
2. Éditeur de texte hello informations tooa de copie et supprimer tous les espaces afin qu’il soit une chaîne continue. Cette chaîne est déclarée en tant que variable dans l’étape suivante de hello.
3. Déclarer des variables de hello. Vérifiez l’empreinte numérique de hello toodeclare que vous avez récupéré à l’étape précédente de hello.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. Ajoutez hello empreinte toohello liste de certificats révoqués. Vous voyez « Réussi » lorsque l’empreinte numérique hello a été ajouté.

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. Vérifiez que l’empreinte numérique hello a été ajouté toohello liste de révocation de certificats.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. Après avoir ajouté l’empreinte numérique hello, certificat de hello ne peut plus être utilisé tooconnect. Les clients qui tentent de tooconnect à l’aide de ce certificat recevoir un message indiquant que ce certificat hello n’est plus valide.

### <a name="reinstateclientcert"></a>tooreinstate un certificat client

Vous pouvez le rétablir sous un certificat client en supprimant l’empreinte numérique hello à partir de la liste de hello des certificats clients révoqués.

1. Déclarer des variables de hello. Assurez-vous que vous déclarez hello correct l’empreinte numérique hello certificat que vous souhaitez tooreinstate.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. Supprimer l’empreinte numérique du certificat hello à partir de la liste de révocation de certificats hello.

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. Vérifiez si l’empreinte numérique hello est supprimée à partir de la liste de révocation hello.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>Forum Aux Questions sur les connexions point à site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Étapes suivantes
Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand en savoir plus sur la mise en réseau et les machines virtuelles, consultez [vue d’ensemble du réseau Azure et Linux VM](../virtual-machines/linux/azure-vm-network-overview.md).
