---
title: "scénarios d’aaaAdvanced avec Azure MFA et des réseaux privés virtuels tiers"
description: "Guides de configuration pas à pas pour toointegrate Azure MFA avec Cisco et Juniper Citrix."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/13/2017
ms.author: kgremban
ms.openlocfilehash: e23960ca4977cc01271f99fa2bec70449e9acfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>Scénarios avancés avec l'authentification multifacteur Azure et des solutions VPN tierces
Azure multi-Factor Authentication peut servir tooseamlessly se connecter avec différentes solutions VPN tiers. Cet article se concentre sur l’équipement Cisco® ASA VPN, équipement Citrix NetScaler SSL VPN et hello Juniper réseaux Secure accès/Pulse Secure connecter sécurisé SSL appareil VPN. Nous avons créé tooaddress des guides de configuration de ces trois appareils courantes, mais serveur multi-Factor peut s’intégrer avec la plupart des systèmes qui utilisent RADIUS, LDAP, IIS ou authentification basée sur les revendications tooAD FS. Pour plus de détails, consultez la rubrique [Configurations de serveur MFA](multi-factor-authentication-get-started-server.md#next-steps).

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Appareil Cisco ASA VPN et authentification multifacteur Azure
L’authentification multifacteur Azure s’intègre à votre VPN de Cisco® ASA appliance tooprovide une sécurité supplémentaire pour les connexions de Cisco AnyConnect® VPN et d’accès au portail.  Cela est possible à l’aide d’un protocole LDAP ou RADIUS hello.  Sélectionnez une des hello configuration pas à pas détaillé de hello toodownload suivante détaille la procédure.

| Guide de configuration | Description |
| --- | --- |
| [Cisco ASA avec Anyconnect VPN et Azure MFA Configuration pour LDAP](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | Intégrer votre appliance VPN Cisco ASA avec Azure MFA à l’aide de LDAP |
| [Cisco ASA avec Anyconnect VPN et Azure MFA Configuration pour RADIUS](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | Intégrer votre appliance VPN Cisco ASA avec Azure MFA à l’aide de RADIUS |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>Citrix NetScaler SSL VPN et authentification multifacteur Azure
L’authentification multifacteur Azure s’intègre à votre Citrix NetScaler SSL VPN matériel tooprovide une sécurité supplémentaire pour les connexions Citrix NetScaler SSL VPN et d’accès au portail.  Cela est possible à l’aide d’un protocole LDAP ou RADIUS hello.  Sélectionnez une des hello configuration pas à pas détaillé de hello toodownload suivante détaille la procédure.

| Guide de configuration | Description |
| --- | --- |
| [Citrix NetScaler SSL VPN et Azure MFA Configuration pour LDAP](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | Intégrer votre appliance VPN Citrix NetScaler SSL avec Azure MFA à l’aide de LDAP |
| [Citrix NetScaler SSL VPN et Azure MFA Configuration pour RADIUS](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | Intégrer votre appliance VPN Citrix NetScaler SSL avec Azure MFA à l’aide de RADIUS |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Appareil Juniper/Pulse Secure SSL VPN et authentification multifacteur Azure
L’authentification multifacteur Azure s’intègre à votre Juniper/Pulse Secure SSL VPN matériel tooprovide une sécurité supplémentaire pour les connexions Juniper/Pulse Secure SSL VPN et d’accès au portail.  Cela est possible à l’aide d’un protocole LDAP ou RADIUS hello.  Sélectionnez une des hello configuration pas à pas détaillé de hello toodownload suivante détaille la procédure.

| Guide de configuration | Description |
| --- | --- |
| [Juniper/Pulse Secure SSL VPN et Azure MFA Configuration pour LDAP](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | Intégrer votre appliance VPN Juniper/Pulse Secure SSL avec Azure MFA à l’aide de LDAP |
| [Juniper/Pulse Secure SSL VPN et Azure MFA Configuration pour RADIUS](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | Intégrer votre appliance VPN Juniper/Pulse Secure SSL avec Azure MFA à l’aide de RADIUS |

## <a name="next-steps"></a>Étapes suivantes

- [Augmenter votre infrastructure d’authentification existante avec hello extension du serveur NPS pour Azure multi-Factor Authentication](multi-factor-authentication-nps-extension.md)

- [Configurer les paramètres d’Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md)