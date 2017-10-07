---
title: "aaaAzure Guide de mise en réseau de Site Recovery pour répliquer les machines virtuelles à partir d’Azure tooAzure | Documents Microsoft"
description: "Aide à la mise en réseau pour la réplication des machines virtuelles Azure"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>Aide à la mise en réseau pour la réplication des machines virtuelles Azure

>[!NOTE]
> La réplication Site Recovery pour les machines virtuelles Azure est actuellement en préversion.

Cet article explique hello pour Azure Site Recovery guide relatif au réseau lorsque vous êtes de réplication et de récupération des machines virtuelles à partir de la région de tooanother d’une région. Pour plus d’informations sur la configuration requise d’Azure Site Recovery, consultez hello [conditions préalables](site-recovery-prereq.md) l’article.

## <a name="site-recovery-architecture"></a>Architecture de Site Recovery

Récupération de site fournit un moyen simple et facile de tooreplicate applications s’exécutant sur des machines virtuelles tooanother région Azure afin qu’ils puissent être récupérées s’il existe une interruption de la région principale de hello. En savoir plus sur [ce scénario et l’architecture Site Recovery](site-recovery-azure-to-azure-architecture.md).

## <a name="your-network-infrastructure"></a>Votre infrastructure réseau

Hello diagramme suivant représente hello classique environnement Azure pour une application s’exécutant sur des machines virtuelles :

![environnement client](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Si vous utilisez Azure ExpressRoute ou une connexion VPN à partir d’un tooAzure de réseau local, l’environnement de hello ressemble à ceci :

![environnement client](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

En règle générale, les clients protègent leurs réseaux à l’aide de pare-feu et/ou de groupes de sécurité réseau. pare-feux Hello permet qu’il soit basée sur URL ou IP création de listes autorisées pour le contrôle de la connectivité réseau. Règles d’autorisation de groupes de sécurité réseau pour l’utilisation de connectivité du réseau toocontrol plages IP.

>[!IMPORTANT]
> Si vous utilisez une connectivité de réseau toocontrol proxy authentifié, il n’est pas pris en charge et ne peut pas activer la réplication de la récupération de Site. 

Hello sections suivantes décrivent les modifications connectivité sortante hello réseau qui sont requises à partir de machines virtuelles pour toowork de réplication de Site Recovery.

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Connectivité sortante pour les URL Azure Site Recovery

Si vous utilisez toute connexion sortante de pare-feu basé sur l’URL de proxy toocontrol, être toowhitelist que ceux-ci requis des URL de service Azure Site Recovery :


**URL** | **Objectif**  
--- | ---
*.blob.core.windows.net | Requis pour que les données peuvent être écrites compte de stockage de cache toohello dans la région de hello source à partir de la machine virtuelle de hello.
login.microsoftonline.com | Obligatoire pour les authentifications et les URL du service de récupération de Site toohello.
*.hypervrecoverymanager.windowsazure.com | Requis pour que la communication avec le service Site Recovery hello peut se produire à partir de la machine virtuelle de hello.
*.servicebus.windows.net | Requis pour que les données de surveillance et de diagnostic de la récupération de Site hello peuvent être écrites à partir de la machine virtuelle de hello.

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Connectivité sortante pour les plages d’adresses IP Azure Site Recovery

>[!NOTE]
> tooautomatically créer des règles du groupe de sécurité réseau hello requis sur le groupe de sécurité réseau hello, vous pouvez [télécharger et utiliser ce script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

>[!IMPORTANT]
> * Nous vous recommandons de créer des règles de groupe de sécurité réseau hello requis sur un groupe de sécurité de réseau de test et de vérifier qu’il n’y a aucun problème avant de créer des règles de hello sur un groupe de sécurité de réseau de production.
> * nombre de hello requis toocreate de règles du groupe de sécurité réseau, assurez-vous que votre abonnement est dans la liste approuvée. Contactez le support technique tooincrease hello NSG règle limite dans votre abonnement.

Si vous utilisez un pare-feu basé sur IP proxy connectivité sortante de groupe de sécurité réseau règles toocontrol, hello plages IP suivantes besoin dans la liste approuvée toobe, selon les emplacements source et cible de hello d’ordinateurs virtuels hello :

- Emplacement source de toutes les plages IP qui correspondent toohello. (Vous pouvez télécharger hello [plages IP](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Création de listes autorisées est requise afin que les données peuvent être écrites compte de stockage de cache toohello à partir de la machine virtuelle de hello.

- Toutes les plages IP qui correspondent tooOffice 365 [authentification et identité de points de terminaison IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

    >[!NOTE]
    > Si de nouvelles adresses IP sont ajouté les plages d’adresses IP 365 tooOffice Bonjour futures, vous devez toocreate de nouvelles règles de groupe de sécurité réseau.
    
- Adresses IP des points de terminaison du service Site Recovery ([disponibles dans un fichier XML](https://aka.ms/site-recovery-public-ips)), qui dépendent de votre emplacement cible : 

   **Emplacement cible** | **Adresses IP du service Site Recovery** |  **Adresse IP de surveillance Site Recovery**
   --- | --- | ---
   Est de l'Asie | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   Asie du Sud-Est | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   Inde centrale | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   Inde du Sud | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   États-Unis - partie centrale septentrionale | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   Europe du Nord | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   Europe de l’Ouest | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   Est des États-Unis | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   Ouest des États-Unis | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   États-Unis - partie centrale méridionale | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   Centre des États-Unis | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   Est des États-Unis 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   Est du Japon | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   Ouest du Japon | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   Sud du Brésil | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   Est de l’Australie | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   Sud-est de l’Australie | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   Centre du Canada | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   Est du Canada | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   Centre-Ouest des États-Unis | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   Ouest des États-Unis 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   Ouest du Royaume-Uni | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   Sud du Royaume-Uni | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="sample-nsg-configuration"></a>Exemple de configuration de groupe de sécurité réseau
Cette section explique les règles de groupe de sécurité réseau tooconfigure hello étapes afin que la réplication de la récupération de Site peut travailler sur un ordinateur virtuel. Si vous utilisez une connexion sortante de groupe de sécurité réseau règles toocontrol, utilisez « Autoriser HTTPS sortant » de règles pour toutes les plages IP de hello requis.

>[!Note]
> tooautomatically créer des règles du groupe de sécurité réseau hello requis sur le groupe de sécurité réseau hello, vous pouvez [télécharger et utiliser ce script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

Par exemple, si l’emplacement de la source de votre machine virtuelle est « États-Unis » et l’emplacement cible de réplication est « États-Unis », suivez les étapes de hello dans hello deux sections suivantes.

>[!IMPORTANT]
> * Nous vous recommandons de créer des règles de groupe de sécurité réseau hello requis sur un groupe de sécurité de réseau de test et de vérifier qu’il n’y a aucun problème avant de créer des règles de hello sur un groupe de sécurité de réseau de production.
> * nombre de hello requis toocreate de règles du groupe de sécurité réseau, assurez-vous que votre abonnement est dans la liste approuvée. Contactez le support technique tooincrease hello NSG règle limite dans votre abonnement. 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>Règles du groupe de sécurité réseau sur le groupe de sécurité réseau hello est des États-Unis

* Créer des règles qui correspondent trop[plages d’adresses IP d’US East](https://www.microsoft.com/download/confirmation.aspx?id=41653). Cela est nécessaire afin que les données peuvent être écrites compte de stockage de cache toohello à partir de la machine virtuelle de hello.

* Créer des règles pour toutes les plages IP qui correspondent tooOffice 365 [authentification et identité de points de terminaison IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Créer des règles qui correspondent emplacement cible de toohello :

   **Emplacement** | **Adresses IP du service Site Recovery** |  **Adresse IP de surveillance Site Recovery**
    --- | --- | ---
   Centre des États-Unis | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>Règles du groupe de sécurité réseau sur le groupe de sécurité réseau hello du centre des États-Unis

Ces règles sont requis pour que la réplication peut être activée à partir de hello cible région toohello source région après le basculement :

* Les règles qui correspondent trop[plages d’adresses IP d’US Central](https://www.microsoft.com/download/confirmation.aspx?id=41653). Celles-ci sont requises afin que les données peuvent être écrites compte de stockage de cache toohello à partir de la machine virtuelle de hello.

* Règles pour toutes les plages IP qui correspondent tooOffice 365 [authentification et identité de points de terminaison IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Emplacement source de règles qui correspondent toohello :

   **Emplacement** | **Adresses IP du service Site Recovery** |  **Adresse IP de surveillance Site Recovery**
    --- | --- | ---
   Est des États-Unis | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>Instructions pour une configuration ExpressRoute/VPN Azure vers Local

Si vous disposez d’une connexion ExpressRoute ou VPN entre locaux et hello source d’emplacement dans Azure, suivez les instructions de hello dans cette section.

### <a name="forced-tunneling-configuration"></a>Configuration de tunneling forcé

Une configuration de client commune est toodefine un itinéraire par défaut (0.0.0.0/0) force tooflow de trafic Internet sortant via un emplacement local de hello. Nous ne recommandons pas cette configuration. le trafic de réplication Hello et de communication du service de récupération de Site ne doivent pas laisser hello Azure limite. Bonjour solution est tooadd itinéraires définis par l’utilisateur (UDRs) pour [ces plages IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges) afin que le trafic de réplication hello n’accéder localement.

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Connectivité entre l’emplacement local et la cible de hello

Suivez ces instructions pour les connexions entre l’emplacement cible de hello et un emplacement local de hello :
- Si votre application a besoin de machines locales de toohello tooconnect ou s’il existe des clients qui se connectent toohello application sur site via VPN/ExpressRoute, assurez-vous d’avoir au moins un [connexion site à site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) entre votre centre de données cible Azure région et hello locaux.

- Si vous prévoyez un grand nombre de tooflow le trafic entre votre cible région Azure et le centre de données hello local, vous devez créer un autre [connexion ExpressRoute](../expressroute/expressroute-introduction.md) entre le centre de données cible Azure région et hello locaux hello.

- Si vous souhaitez tooretain des adresses IP pour les ordinateurs virtuels de hello après que qu’ils basculent, conserver la connexion de site à site/ExpressRoute de la région de hello cible dans un état déconnecté. Il s’agit de toomake qu’il n’y a aucun conflit de plage entre les plages d’adresses IP de la région de hello source et les plages d’adresses IP de la région cible.

### <a name="best-practices-for-expressroute-configuration"></a>Bonnes pratiques en matière de configuration d’ExpressRoute
Suivez ces bonnes pratiques pour la configuration d’ExpressRoute :

- Vous devez toocreate un circuit ExpressRoute dans les deux régions de hello source et cible. Vous devez ensuite toocreate une connexion entre :
  - réseau virtuel de Hello source et le circuit ExpressRoute de hello.
  - réseau virtuel de Hello cible et le circuit ExpressRoute de hello.

- Dans le cadre de la norme d’ExpressRoute, vous pouvez créer des circuits Bonjour même région géopolitique. toocreate des circuits ExpressRoute dans différentes régions géopolitiques, Azure ExpressRoute Premium est requise, ce qui implique un coût incrémentiel. (Si vous utilisez déjà ExpressRoute Premium, il n’y a aucun frais supplémentaires.) Pour plus d’informations, consultez hello [document d’emplacements ExpressRoute](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) et [ExpressRoute tarification](https://azure.microsoft.com/pricing/details/expressroute/).

- Nous vous recommandons d’utiliser des plages d’adresses IP différentes dans les régions source et cible. Hello circuit ExpressRoute ne pourra plus être tooconnect avec deux réseaux virtuels Azure Hello les plages IP même à hello même temps.

- Vous pouvez créer des réseaux virtuels avec la même adresse IP comprise dans les deux régions et créer des circuits ExpressRoute dans les deux régions de hello. Dans le cas de hello d’un événement de basculement, vous déconnecter de circuit de hello de réseau virtuel de hello source et connectez-vous circuit hello dans le réseau virtuel de hello cible.

 >[!IMPORTANT]
 > Si la région primaire hello est complètement bas, hello déconnexion opération peut échouer. Réseau virtuel de hello cible qui empêche de mise en route de la connectivité d’ExpressRoute.

## <a name="next-steps"></a>Étapes suivantes
Commencez à protéger vos charges de travail en [répliquant des machines virtuelles Azure](site-recovery-azure-to-azure.md).
