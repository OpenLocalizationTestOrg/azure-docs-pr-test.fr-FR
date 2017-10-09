---
title: "aaaCreate un classique de PowerShell sonde personnalisée - passerelle d’Application Azure - | Documents Microsoft"
description: "Découvrez comment toocreate personnalisé sondage pour la passerelle d’Application à l’aide de PowerShell dans le modèle de déploiement classique de hello"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Créer une sonde personnalisée pour Azure Application Gateway (classique) en utilisant PowerShell

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-create-probe-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

Dans cet article, vous ajoutez une passerelle existante d’application sonde personnalisée tooan avec PowerShell. Les sondes personnalisés sont utiles pour les applications qui ont une page de vérification d’intégrité spécifique ou pour les applications qui ne fournissent pas une réponse correcte sur l’application web de hello par défaut.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Créer une passerelle Application Gateway

toocreate une passerelle d’application :

1. Créez une ressource Application Gateway.
2. Créez un fichier XML de configuration ou un objet de configuration.
3. Valider hello toohello de configuration qui vient d’être créé ressource passerelle d’application.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Créer une ressource de passerelle d’application avec une sonde personnalisée

passerelle de hello toocreate, utilisez hello `New-AzureApplicationGateway` applet de commande, en remplaçant les valeurs hello par les vôtres. La facturation pour la passerelle de hello ne démarre pas à ce stade. La facturation commence dans une étape ultérieure, lorsque la passerelle de hello a démarré correctement.

Hello exemple suivant crée une passerelle d’application à l’aide d’un réseau virtuel appelé « testvnet1 » et un sous-réseau nommé « sous-réseau-1 ».

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate qui hello passerelle a été créé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10. Hello la valeur par défaut de *GatewaySize* est moyenne. Vous avez le choix entre Small, Medium et Large.
> 
> 

*Présence* et *DnsName* sont affichés comme vide, car la passerelle de hello n’a pas encore démarré. Ces valeurs sont créés une fois la passerelle de hello en hello état en cours d’exécution.

### <a name="configure-an-application-gateway-by-using-xml"></a>Configurer une passerelle d’application à l’aide de XML

Bonjour l’exemple suivant, un tooconfigure de fichier XML tous les paramètres de passerelle d’application et de les valider toohello ressource de passerelle d’application.  

Copiez hello suivant tooNotepad de texte.

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Modifier les valeurs hello entre parenthèses hello pour les éléments de configuration hello. Hello enregistrez-le avec l’extension .xml.

Hello suivant montre comment toouse un tooset du fichier de configuration des tooload de passerelle d’application hello équilibrer le trafic HTTP sur le port public 80 et envoyer le trafic réseau tooback-end port80 entre deux adresses IP à l’aide d’une sonde personnalisée.

> [!IMPORTANT]
> l’élément Hello protocole Http ou Https est sensible à la casse.

Un élément de configuration \<sonde\> est ajouté tooconfigure les sondes personnalisé.

les paramètres de configuration de Hello sont :

|Paramètre|Description|
|---|---|
|**Nom** |Nom de référence de la sonde personnalisée. |
* **Protocole** | Protocole utilisé (les valeurs possibles sont HTTP ou HTTPS).|
| **Hôte** et **Chemin** | URL du chemin d’accès complet qui est appelée par hello application passerelle toodetermine hello d’intégrité de l’instance de hello. Par exemple, si vous avez un site Web http://contoso.com/, sonde personnalisée de hello peut être configurée pour « http://contoso.com/path/custompath.htm » pour la sonde vérifie toohave une réponse HTTP correcte.|
| **Intervalle** | Configure les vérifications d’intervalle hello sondage en secondes.|
| **Délai d'expiration** | Définit le délai d’attente de la sonde hello pour une vérification de la réponse HTTP.|
| **Seuil de défaillance sur le plan de l’intégrité** | Hello nombre d’échecs de réponse HTTP nécessaires de l’instance tooflag hello principal en tant que *défectueux*.|

nom de la sonde Hello est référencé dans hello \<paramètres\> tooassign configuration quel pool principal utilise des paramètres de sonde personnalisée.

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a>Ajouter une passerelle d’application existant du tooan sonde personnalisée

La modification de configuration actuel hello d’une passerelle d’application nécessite trois étapes : obtenir le fichier de configuration XML actuel hello, modifier toohave une sonde personnalisée et configurer la passerelle d’application hello avec de nouveaux paramètres de XML hello.

1. Obtenir le fichier XML de hello à l’aide de `Get-AzureApplicationGatewayConfig`. Cette toobe XML de configuration applet de commande exporte hello modifié tooadd un paramètre de sonde.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. Ouvrez le fichier XML de hello dans un éditeur de texte. Ajoutez une section `<probe>` après `<frontendport>`.

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  Dans la section Paramètres de hello Hello XML, ajoutez les nom de la sonde hello comme indiqué dans hello l’exemple suivant :

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  Enregistrez le fichier XML de hello.

1. Configuration de passerelle l’application hello mise à jour avec hello fichier XML à l’aide de `Set-AzureApplicationGatewayConfig`. Cette applet de commande met à jour votre passerelle d’application avec la nouvelle configuration de hello.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooconfigure décharger de Secure Sockets Layer (SSL), consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).

Si vous souhaitez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, consultez [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).

