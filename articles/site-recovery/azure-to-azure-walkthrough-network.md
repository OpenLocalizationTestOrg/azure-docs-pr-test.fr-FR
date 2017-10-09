---
title: "aaaPlan mise en réseau pour la réplication tooAzure VMware avec Site Recovery | Documents Microsoft"
description: "Cet article décrit la planification réseau requise pour la réplication de machines virtuelles Azure avec Azure Site Recovery"
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
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>Étape 3 : planifier la mise en réseau pour la réplication de machines virtuelles Azure

Une fois que vous avez vérifié hello [conditions préalables au déploiement](azure-to-azure-walkthrough-prerequisites.md), lisez cette hello de toounderstand article Considérations lors de la réplication et la récupération des machines virtuelles (VM) à partir d’une région Azure tooanother, la mise en réseau à l’aide de hello Service de récupération de Site Azure. 

- Lorsque vous avez terminé l’article de hello, vous devez avoir un clear comprendre comment tooset des sortant accès pour les machines virtuelles Azure vous souhaitez tooreplicate et comment tooconnect à partir de votre site à site toothose VMs.
- Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
> La réplication de machines virtuelles Azure avec Site Recovery est actuellement en préversion.



## <a name="network-overview"></a>Présentation du réseau

En général, vos machines virtuelles Azure sont situés dans un réseau/sous-réseau virtuel Windows Azure, et il existe une connexion à partir de votre tooAzure de site local à l’aide d’Azure ExpressRoute, ou une connexion VPN.

Les réseaux sont généralement protégés à l’aide de pare-feu et/ou de groupes de sécurité réseau. Pare-feu permet basée sur URL sur les listes basé sur IP, toocontrol connectivité du réseau. Les groupes de sécurité réseau utilisent des règles basées sur des plages d’adresses IP. 


Toowork de récupération de Site prévu, vous devez toomake certaines modifications de connectivité réseau sortant, à partir d’ordinateurs virtuels que vous souhaitez tooreplicate. Récupération de site ne prend pas en charge l’utilisation d’une connectivité réseau de l’authentification proxy toocontrol. Si vous utilisez un proxy d’authentification, la réplication ne peut pas être activée. 


Hello diagramme suivant illustre un environnement classique pour une application en cours d’exécution sur des machines virtuelles Azure.

![environnement client](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Environnement de machines virtuelles Azure**

Il vous faudra également un tooAzure connexion configurer à partir de votre site local, à l’aide d’Azure ExpressRoute ou une connexion VPN. 

![environnement client](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**TooAzure de connexion locale**



## <a name="outbound-connectivity-for-urls"></a>Connectivité sortante pour les URL

Si vous utilisez une connexion sortante de pare-feu basé sur l’URL de proxy toocontrol, veillez à que laisser ces URL utilisées par la récupération de Site

**URL** | **Détails**  
--- | ---
*.blob.core.windows.net | Permet de toobe données écrite hello machine virtuelle, le compte de stockage de cache toohello dans la région de la source hello.
login.microsoftonline.com | Fournit des URL du service de récupération tooSite d’authentification et d’autorisation.
*.hypervrecoverymanager.windowsazure.com | Permet la communication avec le service de récupération de Site à partir de la machine virtuelle de hello de hello.
*.servicebus.windows.net | Requis pour que les données de surveillance et de diagnostic de la récupération de Site hello peuvent être écrites à partir de la machine virtuelle de hello.

## <a name="outbound-connectivity-for-ip-address-ranges"></a>Connectivité sortante pour les plages d’adresses IP

- Vous pouvez créer automatiquement des règles de hello requis sur hello NSG en téléchargeant et en cours d’exécution [ce script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).
- Nous vous recommandons de créer des règles de groupe de sécurité réseau hello requis sur un groupe de sécurité réseau de test et de vérifier qu’il n’y a aucun problème, avant de créer des règles de hello sur un groupe de sécurité réseau de production.
- nombre de hello requis toocreate de règles du groupe de sécurité réseau, assurez-vous que votre abonnement est dans la liste approuvée. Contactez le support technique tooincrease hello NSG règle limite dans votre abonnement.
Si vous utilisez un pare-feu basé sur IP proxy connectivité sortante de groupe de sécurité réseau règles toocontrol, hello plages IP suivantes besoin dans la liste approuvée toobe, selon les emplacements source et cible de hello d’ordinateurs virtuels hello :

    - Emplacement source de toutes les plages d’adresses IP qui correspondent toohello. Téléchargement hello [plages](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Création de listes autorisées est requise, afin que les données peuvent être écrites compte de stockage de cache toohello à partir de la machine virtuelle de hello.
    - Toutes les plages IP qui correspondent tooOffice 365 [authentification et identité de points de terminaison IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity). Si de nouvelles adresses IP sont ajouté tooOffice 365 plages d’adresses IP, vous devez toocreate de nouvelles règles de groupe de sécurité réseau.
-     Adresses IP des points de terminaison du service Site Recovery ([disponibles dans un fichier XML](https://aka.ms/site-recovery-public-ips)), qui dépendent de votre emplacement cible : 

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

## <a name="example-nsg-configuration"></a>Exemple de configuration de groupe de sécurité réseau

Cette section présente le fonctionnement des règles de tooconfigure groupe de sécurité réseau, afin que les réplications fonctionne pour un ordinateur virtuel. Si vous utilisez une connexion sortante de groupe de sécurité réseau règles toocontrol, utilisez « Autoriser HTTPS sortant » de règles pour toutes les plages IP de hello requis.

Dans cet exemple, hello emplacement source d’ordinateur virtuel est « États-Unis ». emplacement cible de réplication Hello est Centre des États-Unis.


### <a name="example"></a>Exemple

#### <a name="east-us"></a>Est des États-Unis

1. Créer des règles qui correspondent trop[plages d’adresses IP d’US East](https://www.microsoft.com/download/confirmation.aspx?id=41653). Cela est nécessaire afin que les données peuvent être écrites compte de stockage de cache toohello à partir de la machine virtuelle de hello.
2. Créer des règles pour toutes les plages IP qui correspondent tooOffice 365 [authentification et identité de points de terminaison IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Créer des règles qui correspondent emplacement cible de toohello :

   **Emplacement** | **Adresses IP du service Site Recovery** |  **Adresse IP de surveillance Site Recovery**
    --- | --- | ---
   Centre des États-Unis | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>Centre des États-Unis

Ces règles sont obligatoires pour que la réplication peut être activée à partir de hello région toohello source région cible après le basculement.

1. Créer des règles qui correspondent trop[plages d’adresses IP d’US Central](https://www.microsoft.com/download/confirmation.aspx?id=41653).
2. Créer des règles pour toutes les plages IP qui correspondent tooOffice 365 [authentification et identité de points de terminaison IP V4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Créer des règles qui correspondent toohello emplacement de la source :

   **Emplacement** | **Adresses IP du service Site Recovery** |  **Adresse IP de surveillance Site Recovery**
    --- | --- | ---
   Est des États-Unis | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>Connexion locale existante

Si vous avez une connexion ExpressRoute ou VPN entre votre site local et l’emplacement de source de hello dans Azure, suivez ces instructions :

**Configuration** | **Détails**
--- | ---
**Tunneling forcé** | En règle générale, un itinéraire par défaut (0.0.0.0/0) force tooflow de trafic internet sortant via un emplacement local de hello. Nous ne recommandons pas cette approche. Le trafic de réplication et les communications de Site Recovery doivent rester dans Azure.<br/><br/> En tant que solution, ajouter des itinéraires définis par l’utilisateur (UDRs) pour [ces plages IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges), de sorte que le trafic de hello n’accédez localement.
**Connectivité** | Si les applications besoin de machines de tooon local tooconnect, ou localement des clients connectent toohello application via sur site via VPN/ExpressRoute, vérifiez que vous disposez d’au moins un [connexion site à site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), entre le cible hello région Azure et site local de Hello.<br/><br/> Si les volumes de trafic élevées entre la cible de hello région Azure et hello sur site local, créez un autre [connexion ExpressRoute](../expressroute/expressroute-introduction.md), entre la région cible hello et sur site.<br/><br/> Si vous souhaitez tooretain des adresses IP pour les machines virtuelles après basculement, conserver une connexion de site à site/ExpressRoute de la région de hello cible dans un état déconnecté. Ainsi, il n’y a aucun conflit de plage entre hello source et cible plages d’adresses IP.
**ExpressRoute** | Créer un circuit ExpressRoute Bonjour régions source et cible.<br/><br/> Créer une connexion entre le réseau source de hello et circuit ExpressRoute de hello et entre le réseau de cible hello et circuit de hello.<br/><br/> Nous vous recommandons d’utiliser des plages d’adresses IP différentes dans les régions source et cible. Hello circuit ne pourra plus être en mesure de tooconnect toomore qu’un Azure réseaux avec hello même plages IP, hello même temps.<br/><br/> Vous pouvez créer des réseaux virtuels avec la même adresse IP comprise dans les deux régions et puis créer des circuits ExpressRoute dans les deux régions de hello. Pour le basculement, vous déconnecter de circuit de hello de réseau virtuel de hello source et connecter circuit hello dans le réseau virtuel de hello cible.<br/><br/> Si la région primaire hello est complètement bas, hello l’opération de déconnexion risque d’échouer. Dans ce cas, réseau virtuel de hello cible ne sera pas obtenir la connectivité d’ExpressRoute.
**ExpressRoute Premium** | Vous pouvez créer des circuits Bonjour même région géopolitique.<br/><br/> circuits toocreate dans différentes régions géopolitiques, vous devez Azure ExpressRoute Premium.<br/><br/> Avec Premium, hello coût est incrémentielle. Si vous l’utilisez déjà, cela ne représente aucun coût supplémentaire.<br/><br/> En savoir plus sur les [emplacements](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) et la [tarification](https://azure.microsoft.com/pricing/details/expressroute/).



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 4 : créer un coffre](azure-to-azure-walkthrough-vault.md)

