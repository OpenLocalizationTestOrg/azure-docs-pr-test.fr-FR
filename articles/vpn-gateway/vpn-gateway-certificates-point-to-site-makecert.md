---
title: "Générer et exporter des certificats pour les connexions de point à site : MakeCert : Azure | Microsoft Docs"
description: "Cet article contient les étapes toocreate un certificat racine auto-signé, exporter la clé publique de hello et générer des certificats de client à l’aide de MakeCert."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>Générer et exporter des certificats pour les connexions de point à site à l’aide de MakeCert

Connexions de point-to-Site utilisent des certificats tooauthenticate. Cet article vous montre comment toocreate un auto-signé certificat racine et générer des certificats de client à l’aide de MakeCert. Si vous recherchez des étapes de configuration de Point-to-Site, telles que comment la liste de certificats racines de tooupload, sélectionnez un des articles hello ' configurer Point-to-Site' à partir de hello suivant :

> [!div class="op_single_selector"]
> * [Création de certificat auto-signés - PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Création de certificat auto-signés - Makecert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configuration d’une connexion de point à site à un réseau virtuel - Resource Manager - Portail Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Configuration d’une connexion point à site à un réseau virtuel - Resource Manager - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configuration d’une connexion de point à site à un réseau virtuel - Classic - Portail Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

Pendant que nous recommandons d’utiliser hello [Windows PowerShell de 10 étapes](vpn-gateway-certificates-point-to-site.md) toocreate vos certificats, nous fournir ces instructions MakeCert comme une méthode facultative. les certificats de Hello que vous générez à l’aide de ces deux méthodes peuvent être installés sur [n’importe quel système d’exploitation client pris en charge](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq). Toutefois, MakeCert a hello après limitation :

* MakeCert est déconseillé. Cela signifie que cet outil pourrait être supprimé à tout moment. Les certificats que vous avez déjà générés à l’aide de MakeCert ne sont pas affectés quand MakeCert n’est plus disponible. MakeCert fait uniquement les certificats hello toogenerate utilisées, pas comme un mécanisme de validation.

## <a name="rootcert"></a>Créer un certificat racine auto-signé

Hello suit vous montre comment toocreate un auto-signé certificat à l’aide de MakeCert. Ces étapes ne sont pas spécifiques au modèle de déploiement. Elles sont valides pour le modèle Resource Manager et classique.

1. Téléchargez et installez [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).
2. Après l’installation, vous trouverez généralement utilitaire makecert.exe de hello sous ce chemin d’accès : « C:\Program Files (x86) \Windows Kits\10\bin\<arch >'. Toutefois, il est possible qu’il a été installé tooanother emplacement. Ouvrez une invite de commandes en tant qu’administrateur et accédez emplacement toohello Hello utilitaire MakeCert. Vous pouvez utiliser hello l’exemple suivant, l’ajustement de l’emplacement approprié de hello :

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. Créez et installez un certificat dans le magasin de certificats personnel hello sur votre ordinateur. Hello exemple suivant crée un correspondant *.cer* fichier que vous téléchargez tooAzure lors de la configuration P2S. Remplacez 'P2SRootCert' et 'P2SRootCert.cer' nom hello que vous souhaitez toouse pour le certificat de hello. certificat de Hello se trouve dans votre 'certificats - actuel\Personnel\Certificats'.

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>Exporter la clé publique de hello (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

fichier de exported.cer Hello doit être téléchargé tooAzure. Pour obtenir des instructions, consultez [Configurer une connexion de point à site](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile). tooadd un certificat racine de confiance supplémentaires, consultez [cette section](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) d’article de hello.

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>Exporter hello un certificat auto-signé et toostore clé privée il (facultatif)

Vous souhaiterez peut-être tooexport hello racine certificat auto-signé et stocker en toute sécurité. Si besoin est, vous pouvez l’installer ultérieurement sur un autre ordinateur et générer davantage de certificats clients ou exporter un autre fichier .cer. tooexport hello auto-signé certificat racine un .pfx, le certificat racine de hello select et l’utilisation hello mêmes étapes comme décrit dans [exporter un certificat client](#clientexport).

## <a name="create-and-install-client-certificates"></a>Créer et installer des certificats clients

Vous n’installez hello un certificat auto-signé directement sur l’ordinateur client de hello. Vous devez toogenerate un certificat client à partir de hello un certificat auto-signé. Vous exportez et installez l’ordinateur client de hello client certificat toohello. Hello suit n’est pas spécifiques du modèle de déploiement. Elles sont valides pour le modèle Resource Manager et classique.

### <a name="clientcert"></a>Générer un certificat client

Chaque ordinateur client qui se connecte tooa virtuel à l’aide de Point-to-Site doit avoir un certificat client est installé. Vous générez un certificat client à partir du certificat racine auto-signé hello et puis exportez et installez le certificat de client hello. Si le certificat de client hello n’est pas installé, l’authentification échoue. 

Hello étapes suivantes vous guident génération d’un certificat client à partir d’un certificat racine auto-signé. Vous pouvez générer plusieurs certificats de client à partir de hello même certificat racine. Lorsque vous générez les certificats de client à l’aide des étapes hello ci-dessous, hello client certificat est automatiquement installé sur l’ordinateur de hello que vous avez utilisé le certificat de hello toogenerate. Si vous voulez tooinstall un certificat client sur un autre ordinateur client, vous pouvez exporter le certificat de hello.
 
1. Sur hello même ordinateur que vous avez utilisé toocreate hello un certificat auto-signé, ouvrez une invite de commandes en tant qu’administrateur.
2. Modifier et exécuter hello exemple toogenerate un certificat client.
  * Modification *« P2SRootCert »* nom toohello de racine auto-signé hello que vous générez un certificat de client hello de. Assurez-vous que vous utilisez le nom hello du certificat racine hello, qui est le hello ' CN =' la valeur était que vous avez spécifié lorsque vous avez créé les racine auto-signé hello.
  * Modification *P2SChildCert* nom toohello toogenerate un toobe de certificat client.

  Si vous exécutez hello exemple suivant sans le modifier, hello en résulte un certificat client appelé P2SChildcert dans votre magasin de certificats personnel qui a été généré à partir du certificat P2SRootCert.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>Exporter un certificat client

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>Installer un certificat client exporté

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Étapes suivantes

Poursuivez votre configuration point à site. 

* Pour **le Gestionnaire de ressources** étapes du modèle de déploiement, consultez [configurer un tooa de connexion de Point-to-Site réseau virtuel](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Pour **classique** étapes du modèle de déploiement, consultez [configurer un tooa de connexion VPN Point à Site réseau virtuel (classiques)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
