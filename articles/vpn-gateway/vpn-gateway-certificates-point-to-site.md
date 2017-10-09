---
title: "Générer et exporter des certificats pour les connexions de point à site : PowerShell : Azure | Microsoft Docs"
description: "Cet article contient les étapes toocreate un certificat racine auto-signé, exporter la clé publique de hello et générer des certificats de client à l’aide de PowerShell sur Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Générer et exporter des certificats pour les connexions de point à site à l’aide de PowerShell sur Windows 10

Connexions de point-to-Site utilisent des certificats tooauthenticate. Cet article vous montre comment toocreate un auto-signé certificat racine et générer des certificats de client à l’aide de PowerShell sur Windows 10. Si vous recherchez des étapes de configuration de Point-to-Site, telles que comment la liste de certificats racines de tooupload, sélectionnez un des articles hello ' configurer Point-to-Site' à partir de hello suivant :

> [!div class="op_single_selector"]
> * [Création de certificat auto-signés - PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Création de certificat auto-signés - Makecert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configuration d’une connexion de point à site à un réseau virtuel - Resource Manager - Portail Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Configuration d’une connexion point à site à un réseau virtuel - Resource Manager - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configuration d’une connexion de point à site à un réseau virtuel - Classic - Portail Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


Vous devez effectuer les étapes de hello dans cet article sur un ordinateur exécutant Windows 10. applets de commande PowerShell Hello que vous utilisez des certificats de toogenerate font partie du système d’exploitation de hello Windows 10 et ne fonctionnent pas sur d’autres versions de Windows. l’ordinateur Hello Windows 10 est uniquement les certificats nécessaires toogenerate hello. Une fois les certificats hello sont générées, vous pouvez les télécharger ou les installer sur n’importe quel système d’exploitation client pris en charge. 

Si vous n’avez pas l’ordinateur d’accès tooa Windows 10, vous pouvez utiliser [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificats. Hello certificats que vous avez généré à l’aide de ces deux méthodes peuvent être installés sur n’importe quel [pris en charge](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) système d’exploitation client.

## <a name="rootcert"></a>Créer un certificat racine auto-signé

Utilisez toocreate d’applet de commande New-SelfSignedCertificate hello un certificat racine auto-signé. Pour obtenir des informations sur des paramètres supplémentaires, consultez [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. Sur un ordinateur sous Windows 10, ouvrez une console Windows PowerShell avec élévation de privilèges.
2. Utilisez hello suivant le certificat racine auto-signé d’exemple toocreate hello. Hello exemple suivant crée un certificat racine auto-signé nommé « P2SRootCert » qui est installé automatiquement dans « Volet actuel de certificats ». Vous pouvez afficher le certificat de hello en ouvrant *certmgr.msc*, ou *gérer des certificats utilisateur*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Exporter la clé publique de hello (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

fichier de exported.cer Hello doit être téléchargé tooAzure. Pour obtenir des instructions, consultez [Configurer une connexion de point à site](vpn-gateway-howto-point-to-site-rm-ps.md#upload). tooadd un certificat racine de confiance supplémentaires, [cette section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) d’article de hello.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Exporter le certificat racine auto-signé de hello et toostore de clé publique il (facultatif)

Vous souhaiterez peut-être tooexport hello racine certificat auto-signé et stocker en toute sécurité. Si besoin est, vous pouvez l’installer ultérieurement sur un autre ordinateur et générer davantage de certificats clients ou exporter un autre fichier .cer. tooexport hello auto-signé certificat racine un .pfx, le certificat racine de hello select et l’utilisation hello mêmes étapes comme décrit dans [exporter un certificat client](#clientexport).

## <a name="clientcert"></a>Générer un certificat client

Chaque ordinateur client qui se connecte tooa virtuel à l’aide de Point-to-Site doit avoir un certificat client est installé. Vous générez un certificat client à partir du certificat racine auto-signé hello et puis exportez et installez le certificat de client hello. Si le certificat de client hello n’est pas installé, l’authentification échoue. 

Hello étapes suivantes vous guident génération d’un certificat client à partir d’un certificat racine auto-signé. Vous pouvez générer plusieurs certificats de client à partir de hello même certificat racine. Lorsque vous générez les certificats de client à l’aide des étapes hello ci-dessous, hello client certificat est automatiquement installé sur l’ordinateur de hello que vous avez utilisé le certificat de hello toogenerate. Si vous voulez tooinstall un certificat client sur un autre ordinateur client, vous pouvez exporter le certificat de hello.

les exemples de Hello utilisent toogenerate d’applet de commande New-SelfSignedCertificate hello un certificat client qui expire un an. Pour plus d’informations de paramètre supplémentaires, telles que la définition d’une valeur d’expiration différentes pour le certificat de client hello, consultez [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Exemple 1

Cet exemple utilise hello déclaré variable '$cert' à partir de la section précédente de hello. Si vous avez fermé la console PowerShell de hello après création hello certificat racine auto-signé, ou sont créer des certificats client supplémentaires pour une nouvelle session de console PowerShell, utilisez les étapes de hello dans [exemple 2](#ex2).

Modifier et exécuter hello exemple toogenerate un certificat client. Si vous exécutez hello exemple suivant sans le modifier, hello en résulte un certificat client nommé « P2SChildCert ».  Si vous souhaitez que le certificat d’enfant tooname hello par autre chose, modifiez la valeur CN de hello. Ne modifiez pas hello TextExtension lors de l’exécution de cet exemple. certificat client Hello que vous générez est automatiquement installé dans « Certificats - actuel\Personnel\Certificats » sur votre ordinateur.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Exemple 2

Si vous créez des clients supplémentaires des certificats, ou de sont ne pas à l’aide de bienvenue même session PowerShell que vous avez utilisé toocreate votre certificat racine auto-signé, hello utilisation comme suit :

1. Identifiez le certificat racine auto-signé hello qui est installé sur l’ordinateur de hello. Cette applet de commande renvoie la liste des certificats installés sur votre ordinateur.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Recherchez le nom du sujet hello d’hello retourné la liste, puis l’empreinte numérique hello copie trouve du texte tooa tooit suivant fichier. Dans l’exemple suivant de hello, il existe deux certificats. nom CN Hello est hello du certificat racine auto-signé de hello à partir de laquelle vous souhaitez toogenerate un certificat enfant. Dans ce cas, « P2SRootCert ».

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Déclarez une variable pour le certificat racine de hello à l’aide de l’empreinte numérique hello à partir de l’étape précédente de hello. Remplacez l’empreinte numérique avec l’empreinte numérique hello hello du certificat de racine à partir duquel vous souhaitez toogenerate un certificat enfant.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Par exemple, la variable de hello à l’aide de l’empreinte numérique hello pour P2SRootCert à l’étape précédente de hello, ressemble à ceci :

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Modifier et exécuter hello exemple toogenerate un certificat client. Si vous exécutez hello exemple suivant sans le modifier, hello en résulte un certificat client nommé « P2SChildCert ». Si vous souhaitez que le certificat d’enfant tooname hello par autre chose, modifiez la valeur CN de hello. Ne modifiez pas hello TextExtension lors de l’exécution de cet exemple. certificat client Hello que vous générez est automatiquement installé dans « Certificats - actuel\Personnel\Certificats » sur votre ordinateur.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Exporter un certificat client   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>Installer un certificat client exporté

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Étapes suivantes

Poursuivez votre configuration point à site. 

* Pour **le Gestionnaire de ressources** étapes du modèle de déploiement, consultez [configurer un tooa de connexion de Point-to-Site réseau virtuel](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Pour **classique** étapes du modèle de déploiement, consultez [configurer un tooa de connexion VPN Point à Site réseau virtuel (classiques)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
