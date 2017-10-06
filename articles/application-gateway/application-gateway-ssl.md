---
title: "aaaConfigure SSL décharger - passerelle d’Application Azure - PowerShell classique | Documents Microsoft"
description: "Cet article fournit des instructions toocreate déchargement d’une passerelle d’application avec SSL à l’aide de hello modèle de déploiement classique Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>Configurer une passerelle d’application pour le déchargement SSL à l’aide du modèle de déploiement classique de hello

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-ssl-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Passerelle d’Application Azure peut être configuré tooterminate hello Secure Sockets Layer (SSL) session à hello passerelle tooavoid coûteux SSL déchiffrement tâches toohappen au niveau de la batterie de serveurs web hello. Déchargement SSL simplifie également la configuration de serveur frontal de hello et la gestion d’application web de hello.

## <a name="before-you-begin"></a>Avant de commencer

1. Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer. Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).
2. Vérifiez que vous disposez d'un réseau virtuel qui fonctionne avec un sous-réseau valide. Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello. passerelle d’application Hello doit être par lui-même dans un sous-réseau de réseau virtuel.
3. serveurs Hello configurer la passerelle d’application hello toouse doivent exister ou aient leurs points de terminaison créés dans le réseau virtuel de hello ou avec une adresse IP publique/VIP affectés.

tooconfigure SSL décharger sur une passerelle d’application, hello dans l’ordre de hello répertoriés comme suit :

1. [Créer une passerelle Application Gateway](#create-an-application-gateway)
2. [Télécharger des certificats SSL](#upload-ssl-certificates)
3. [Configurer la passerelle de hello](#configure-the-gateway)
4. [Jeu de configuration de la passerelle hello](#set-the-gateway-configuration)
5. [Démarrer hello passerelle](#start-the-gateway)
6. [Vérifiez l’état de la passerelle hello](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Créer une passerelle Application Gateway

passerelle de hello toocreate, utilisez hello `New-AzureApplicationGateway` applet de commande, en remplaçant les valeurs hello par les vôtres. La facturation pour la passerelle de hello ne démarre pas à ce stade. La facturation commence dans une étape ultérieure, lorsque la passerelle de hello a démarré correctement.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate qui hello passerelle a été créé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande.

Dans l’exemple hello, *Description*, *InstanceCount*, et *GatewaySize* sont des paramètres facultatifs. Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10. Hello la valeur par défaut de *GatewaySize* est moyenne. Les autres valeurs disponibles sont Small et Large. *Présence* et *DnsName* sont affichés comme vide, car la passerelle de hello n’a pas encore démarré. Ces valeurs sont créés une fois la passerelle de hello en hello état en cours d’exécution.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>Télécharger des certificats SSL

Utilisez `Add-AzureApplicationGatewaySslCertificate` certificat de serveur hello tooupload dans *pfx* passerelle d’application toohello format. nom du certificat Hello est un nom d’utilisateur choisi et doit être unique au sein de la passerelle d’application hello. Ce certificat est tooby auxquels ce nom dans toutes les opérations de gestion de certificat sur la passerelle d’application hello.

Cet exemple suivant montre l’applet de commande hello, remplacez les valeurs hello dans l’exemple hello par les vôtres.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

Ensuite, validez chargement du certificat hello. Hello d’utilisation `Get-AzureApplicationGatewayCertificate` applet de commande.

Cet exemple montre l’applet de commande hello sur la première ligne de hello, suivi par la sortie hello.

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> mot de passe du certificat Hello a toobe entre 4 too12 caractères, des lettres ou chiffres. Les caractères spéciaux ne sont pas acceptés.

## <a name="configure-hello-gateway"></a>Configurer la passerelle de hello

La configuration d'une passerelle Application Gateway se compose de plusieurs valeurs. les valeurs Hello peuvent être liées configuration de hello tooconstruct ensemble.

les valeurs Hello sont :

* **Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello. adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.
* **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.
* **Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).
* **La règle :** règle de hello lie le port d’écoute hello et pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier. Actuellement, seuls hello *base* règle est pris en charge. Hello *base* règle est la distribution de la charge de tourniquet.

**Notes de configuration supplémentaires :**

Pour configurer des certificats SSL, hello protocole dans **HttpListener** doit également modifier*Https* (sensible à la casse). Hello **SslCert** l’élément est ajouté trop**HttpListener** avec hello valeur toohello même nom que celui de téléchargement hello de la précédente section de certificats SSL. le port frontal Hello doit être too443 mis à jour.

**affinité basé sur cookie de tooenable**: une passerelle d’application peut être configurée tooensure qu’une demande à partir d’une session cliente est toujours dirigée toohello même machine virtuelle dans la batterie de serveurs web hello. Ce scénario est effectué par injection d’un cookie de session qui autorise le trafic toodirect de passerelle de hello de manière appropriée. l’affinité basé sur cookie tooenable, définie **CookieBasedAffinity** trop*activé* Bonjour **paramètres** élément.

Vous pouvez construire votre configuration en créant un objet de configuration ou en utilisant un fichier XML de configuration.
tooconstruct votre configuration à l’aide d’une configuration de fichier XML, utilisez hello suivants exemple :

**Exemple de configuration XML**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

## <a name="set-hello-gateway-configuration"></a>Jeu de configuration de la passerelle hello

Ensuite, vous définissez la passerelle d’application hello. Vous pouvez utiliser hello `Set-AzureApplicationGatewayConfig` applet de commande avec un objet de configuration ou un fichier XML de configuration.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>Démarrer hello passerelle

Une fois que la passerelle de hello a été configurée, utilisez hello `Start-AzureApplicationGateway` passerelle de hello toostart applet de commande. Le coût d’une passerelle d’application commence une fois la passerelle de hello a démarré.

> [!NOTE]
> Hello `Start-AzureApplicationGateway` applet de commande peut prendre les toofinish too15 à 20 minutes.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Vérifiez l’état de la passerelle hello

Hello d’utilisation `Get-AzureApplicationGateway` état de hello toocheck applet de commande de passerelle de hello. Si `Start-AzureApplicationGateway` a réussi à l’étape précédente de hello, *état* doit être en cours d’exécution, et *présence* et *DnsName* doit avoir des entrées valides.

Cet exemple montre une passerelle d’application, en cours d’exécution, et le trafic de tootake prêt.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :

* [Équilibrage de charge Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

