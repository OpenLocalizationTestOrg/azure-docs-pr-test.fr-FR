---
title: "aaaHow tooplan votre réseau virtuel pour une collection Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment tooplan votre réseau virtuel pour une collection Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>Comment tooplan votre réseau virtuel pour Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Ce document décrit comment tooset votre réseau virtuel Azure (VNET) et le sous-réseau hello pour Azure RemoteApp. Si vous n’êtes pas familiarisé avec les réseaux virtuels Azure, il s’agit d’une fonctionnalité qui vous aide à vous toovirtualize votre réseau infrastructure toohello cloud et toocreate solutions hybrides avec Azure et vos ressources locales. Pour plus d'informations à ce sujet, cliquez [ici](../virtual-network/virtual-networks-overview.md).

Si vous souhaitez que les stratégies de sécurité toodefine pour le trafic (entrant et sortant) dans votre réseau virtuel où vous déployez Azure RemoteApp, nous recommandons de créer un sous-réseau distinct pour Azure RemoteApp reste hello de vos déploiements Bonjour Azure réseau virtuel. Pour plus d’informations sur comment toodefine les stratégies de sécurité sur votre Azure virtual network sous-réseau, veuillez lire [qu’est un groupe de sécurité réseau (NSG) ?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Types de collections RemoteApp Azure avec les réseaux virtuels Azure
Hello graphiques suivants illustrent hello deux options de l’autre collection lorsque vous souhaitez toouse un réseau virtuel.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Collection Cloud Azure RemoteApp avec réseau virtuel
 ![Azure RemoteApp - Collection Cloud avec réseau virtuel](./media/remoteapp-planvpn/ra-cloudvpn.png)

Représente une collection Azure RemoteApp où toutes les ressources hello que les hôtes de session de RemoteApp hello doivent tooaccess sont déployés dans Azure. Ils peuvent être Bonjour même réseau virtuel en tant que hello RemoteApp VNET ou un autre réseau virtuel dans Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Collection hybride RemoteApp avec réseau virtuel
![Azure RemoteApp - Collection hybride avec réseau virtuel](./media/remoteapp-planvpn/ra-hybridvpn.png)

Représente une collection Azure RemoteApp où certaines ressources hello que les hôtes de session de RemoteApp hello doivent tooaccess sont déployés localement. Hello RemoteApp VNET est un réseau local de toohello lié à l’aide de technologies Azure hybride comme VPN de site à site ou Express Route.

## <a name="how-hello-system-works"></a>Fonctionnement du système hello
Dans les coulisses de hello Azure RemoteApp déploie les machines virtuelles Azure (avec votre image téléchargée) toohello sous-réseau du réseau virtuel que vous avez choisi lors de la configuration. Si vous avez opté pour une collection hybride, nous nous efforçons tooresolve hello nom de domaine complet du contrôleur de domaine hello saisis dans hello mise en service de flux de travail avec serveurDNS hello fourni dans le réseau virtuel de hello.  
Si vous vous connectez tooan de réseau virtuel existant, vérifiez les ports nécessaires que tooexpose hello dans vos groupes de sécurité réseau dans votre sous-réseau Azure RemoteApp. 

Nous vous recommandons d’utiliser un [sous-réseau suffisamment grand pour Azure RemoteApp](remoteapp-vnetsizing.md). Hello plus grande prise en charge par le réseau virtuel Azure est la valeur/8 (à l’aide de définitions de sous-réseau CIDR). Votre sous-réseau doit être suffisamment grand tooaccommodate toutes les machines virtuelles hello Azure RemoteApp pendant montée en puissance parallèle lorsque davantage d’utilisateurs accèdent à des applications de hello. 

Voici les choses hello vous devez tooenable sur votre sous-réseau de réseau virtuel : 

1. Le trafic sortant à partir du sous-réseau de hello doit être autorisé sur le port plage 10101-10175 toocommunicate avec l’un des services de Azure RemoteApp hello internes.
2. Le trafic sortant doit être autorisé à partir de votre tooAzure tooconnect de sous-réseau stockage sur le port 443
3. Si vous disposez d’Active Directory hébergé dans Azure, assurez-vous que toutes les machines virtuelles dans le sous-réseau de réseau virtuel hello pour Azure RemoteApp sont contrôleur de domaine en mesure de tooconnect toothat. Hello DNS dans le réseau virtuel de hello doit être en mesure de tooresolve hello nom de domaine complet de ce contrôleur de domaine.

## <a name="virtual-network-with-forced-tunneling"></a>Réseau virtuel avec tunneling forcé
[Tunneling forcé](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) est maintenant pris en charge dans toutes les nouvelles collections Azure RemoteApp. Nous ne gèrent pas la migration hello d’un toosupport collection existante, le tunneling forcé.  Vous avez toodelete vos collections existantes à l’aide de hello réseau virtuel que vous créez un lien tooAzure RemoteApp et créez un nouveau un tooget tunneling activé sur vos collections forcé. 

