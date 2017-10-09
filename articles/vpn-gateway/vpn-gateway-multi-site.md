---
title: "Se connecter à un site toomultiple de réseau virtuel à l’aide de la passerelle VPN et PowerShell : classique | Documents Microsoft"
description: "Cet article vous guidera dans la connexion réseau virtuel tooa sur site local sites multiples à l’aide d’une passerelle VPN pour le modèle de déploiement classique hello."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Ajouter un tooa de connexion de Site à Site réseau virtuel avec une connexion de passerelle VPN existante (classique)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (classique)](vpn-gateway-multi-site.md)
>
>

Cet article vous guide tout au long de l’aide de PowerShell tooadd Site à Site (S2S) connexions tooa passerelle VPN qui dispose d’une connexion existante. Ce type de connexion est souvent tooas auxquels une configuration de « multisite ». Hello étapes décrites dans cet article s’appliquent les réseaux toovirtual créés à l’aide du modèle de déploiement classique hello (également appelé Service Management). Ces étapes ne s’appliquent pas à la configuration des connexions coexistence tooExpressRoute/Site à Site.

### <a name="deployment-models-and-methods"></a>Outils et modèles de déploiement

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Nous mettons à jour ce tableau à mesure que de nouveaux articles et des outils supplémentaires sont disponibles pour cette configuration. Quand un article est disponible, nous lier directement tooit à partir de cette table.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>À propos de la connexion

Vous pouvez connecter plusieurs sites tooa unique virtuel réseau local. Cela est particulièrement intéressant pour la création de solutions de cloud hybrides. Création d’une passerelle de réseau virtuel Azure tooyour connexion multisite est similaire toocreating autres connexions de Site à Site. En fait, vous pouvez utiliser une passerelle VPN Azure existante, tant que passerelle de hello est dynamique (basé sur l’itinéraire).

Si vous disposez déjà d’un réseau virtuel de passerelle statique tooyour connecté, vous pouvez modifier toodynamic de type hello passerelle sans avoir besoin de réseau virtuel de toorebuild hello dans plusieurs sites de commande tooaccommodate. Avant de modifier le type de routage hello, assurez-vous que votre passerelle VPN locale prend en charge les configurations de VPN basée sur un itinéraire.

![diagramme multi-sites](./media/vpn-gateway-multi-site/multisite.png "multi-sites")

## <a name="points-tooconsider"></a>Points tooconsider

**Vous ne serez pas réseau virtuel toothis du modifications toomake portail toouse en mesure de hello.** Vous avez besoin de fichier de configuration réseau toomake modifications toohello au lieu d’utiliser le portail de hello. Si vous apportez des modifications dans le portail de hello, elles remplaceront vos paramètres de référence multisite pour ce réseau virtuel.

Vous devriez vous sentir à l’aise à l’aide du fichier de configuration de réseau hello par temps de hello vous avez terminé la procédure de plusieurs sites hello. Toutefois, si vous avez plusieurs personnes travaillent sur la configuration de votre réseau, vous devez toomake assurer que tout le monde connaît cette limitation. Cela ne signifie pas que vous ne pouvez pas utiliser portal de hello du tout. Vous pouvez l’utiliser pour tout le reste, à l’exception de renforcement de réseau virtuel particulier toothis configuration modifications.

## <a name="before-you-begin"></a>Avant de commencer

Avant de commencer la configuration, vérifiez que vous disposez des éléments suivants de hello :

* Matériel VPN compatible pour chaque emplacement local. Vérifiez [sur des périphériques VPN pour la connectivité de réseau virtuel](vpn-gateway-about-vpn-devices.md) tooverify si unité hello que toouse est un élément connu toobe compatible.
* Une adresse IP IPv4 publique exposée en externe pour chaque périphérique VPN. adresse IP de Hello ne peut pas se trouver derrière un NAT. Cela est obligatoire.
* Vous devez tooinstall hello dernière version de hello applets de commande PowerShell de Azure. Assurez-vous que vous installez la version de Service Management (SM) de hello dans la version de gestionnaire de ressources toohello Ajout. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations.
* Un expert en configuration du matériel VPN. Vous avez toohave un fort comprendre comment tooconfigure votre périphérique VPN ou un travail avec une personne.
* plages d’adresses IP Hello que vous souhaitez toouse pour votre réseau virtuel (si vous n’avez pas déjà créé une).
* plages d’adresses IP Hello pour chacun des sites de réseau local hello que vous vous connectez. Vous devez toomake que les plages d’adresse IP de hello pour chacun des sites de réseau local hello que vous souhaitez tooconnect toodo pas de chevauchement. Dans le cas contraire, le portail de hello ou hello API REST rejettera configuration hello en cours de téléchargement.<br>Par exemple, si vous avez deux sites de réseau local que tous les deux contenir hello IP adresse plage 10.2.3.0/24 et que vous disposez d’un package avec une adresse de destination 10.2.3.3, Azure ne saura pas le site auquel vous souhaitez que les plages d’adresses toosend hello package toobecause hello sont qui se chevauchent. problèmes de routage tooprevent, Azure n’autorise pas vous tooupload un fichier de configuration qui comporte des plages qui se chevauchent.

## <a name="1-create-a-site-to-site-vpn"></a>1. Créer un VPN de site à site
Si vous avez déjà un VPN de site à site avec une passerelle de routage dynamique, bravo ! Vous pouvez passer trop[exporter les paramètres de configuration de réseau virtuel hello](#export). Dans le cas contraire, procédez comme hello suivant :

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>Si vous avez déjà un réseau virtuel de site à site, mais que sa passerelle de routage est statique :
1. Modifier votre toodynamic de type de passerelle routage. Un VPN multisite requiert une passerelle de routage dynamique (ou basée sur un itinéraire). type de toochange votre passerelle, vous aurez besoin toofirst delete hello existant passerelle, puis créez-en un nouveau. Pour obtenir des instructions, consultez [comment toochange hello type de routage VPN pour votre passerelle](vpn-gateway-configure-vpn-gateway-mp.md).  
2. Configurez votre nouvelle passerelle et créez votre tunnel VPN. Pour obtenir des instructions, consultez [configurer une passerelle VPN Bonjour portail classique Azure](vpn-gateway-configure-vpn-gateway-mp.md). Tout d’abord, modifiez votre toodynamic de type de passerelle routage.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>Si vous n’avez pas de réseau virtuel de site à site :
1. Créer votre réseau virtuel de Site à Site à l’aide de ces instructions : [créer un réseau virtuel avec une connexion VPN de Site à Site Bonjour portail classique Azure](vpn-gateway-site-to-site-create.md).  
2. Configurez une passerelle de routage dynamique en suivant la procédure décrite dans [Configuration d’une passerelle VPN](vpn-gateway-configure-vpn-gateway-mp.md). Être vraiment tooselect **routage dynamique** pour le type de passerelle.

## <a name="export"></a>2. Exporter le fichier de configuration de réseau hello
Exportez votre fichier de configuration réseau Azure en exécutant hello commande suivante. Vous pouvez modifier l’emplacement de hello de hello tooexport tooa autre emplacement de fichier si nécessaire.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. Fichier de configuration de réseau hello ouvert
Ouvrez le fichier de configuration de réseau hello que vous avez téléchargé dans la dernière étape de hello. Utilisez l’éditeur xml de votre choix. fichier de Hello doit ressembler similaire toohello suivantes :

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Ajouter plusieurs références de site
Lorsque vous ajoutez ou supprimez les informations de référence de site, vous apporterez des modifications de configuration toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef. Ajoutez une nouvelle référence de site locale déclenche toocreate Azure un tunnel. Dans l’exemple hello ci-dessous, la configuration du réseau hello est pour une connexion de site unique. Enregistrer le fichier de hello une fois que vous avez terminé d’apporter vos modifications.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

références à des sites supplémentaires tooadd (créer une configuration multisite), ajoutez simplement les lignes « LocalNetworkSiteRef » supplémentaires, comme indiqué dans l’exemple hello ci-dessous :

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. Importer le fichier configuration réseau hello
Importez le fichier de configuration de réseau hello. Lorsque vous importez ce fichier avec les modifications de hello, nouveaux tunnels de hello seront ajoutés. les tunnels Hello utilisera la passerelle dynamique hello que vous avez créé précédemment. Vous pouvez utiliser portail classique de hello ou fichier de hello tooimport PowerShell.

## <a name="6-download-keys"></a>6. Télécharger les clés
Une fois que les nouveaux tunnels ont été ajoutés, utilisez hello PowerShell applet de commande 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE clés prépartagées pour chaque tunnel.

Par exemple :

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

Si vous préférez, vous pouvez également utiliser hello *Get Virtual Network Gateway Shared Key* tooget de l’API REST hello clés prépartagées.

## <a name="7-verify-your-connections"></a>7. Vérifiez vos connexions
Vérifiez l’état des tunnels multisite hello. Après avoir téléchargé les clés hello de chaque tunnel, vous souhaiterez tooverify connexions. Utilisez « Get-AzureVnetConnection' tooget une liste de réseau virtuel tunnels, comme indiqué dans l’exemple hello ci-dessous. VNet1 désigne hello hello réseau virtuel.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

L’exemple renvoie :

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les passerelles VPN, consultez [sur les passerelles VPN](vpn-gateway-about-vpngateways.md).
