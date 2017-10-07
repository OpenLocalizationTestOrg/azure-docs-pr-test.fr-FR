---
title: "configuration système requise du Azure StorSimple Virtual Array aaaMicrosoft | Documents Microsoft"
description: "En savoir plus sur hello logicielle et réseau requises pour votre tableau virtuel StorSimple"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: ea1d3bca-e71b-453d-aa82-440d2638f5e3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.openlocfilehash: 7a124873fdd806d409c7279851456e6347e7ec0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-system-requirements"></a>Configuration système requise pour StorSimple Virtual Array
## <a name="overview"></a>Vue d'ensemble
Cet article décrit hello important requise de votre tableau de virtuel StorSimple Microsoft Azure et pour les clients de stockage hello accès hello tableau. Nous vous recommandons de consulter attentivement les informations hello avant de déployer votre système StorSimple, puis consultez tooit si nécessaire pendant le déploiement et les opérations suivantes.

Hello requise :

* **Configuration logicielle requise pour les clients de stockage** -décrit hello pris en charge les plateformes de virtualisation, navigateurs web, les initiateurs iSCSI, les clients SMB, virtuel minimales requises et des exigences supplémentaires pour ces systèmes d’exploitation.
* **Configuration réseau requise pour l’appareil StorSimple hello** -fournit des informations sur les ports de hello que toobe besoin ouvert dans votre tooallow pare-feu pour le trafic iSCSI, cloud ou la gestion.

Hello requise de StorSimple informations publiées dans cet article s’applique uniquement les réseaux virtuels tooStorSimple.

* Pour les appareils de la 8000 série, accédez trop[configuration système requise pour votre appareil de série StorSimple 8000](storsimple-system-requirements.md).
* Pour les appareils de la 7000 série, consultez trop[configuration système requise pour votre appareil de série StorSimple 7000 de 5000](http://onlinehelp.storsimple.com/1_StorSimple_System_Requirements).

## <a name="software-requirements"></a>Configuration logicielle requise
configuration logicielle requise pour Hello inclure hello plus d’informations sur les navigateurs web hello pris en charge, les versions SMB, les plateformes de virtualisation et hello virtuel minimales requises.

### <a name="supported-virtualization-platforms"></a>Plateformes de virtualisation prises en charge
| **Hyperviseur** | **Version** |
| --- | --- |
| Hyper-V |Windows Server 2008 R2 SP1 et versions ultérieures |
| VMware ESXi |5.5 et versions ultérieures |

### <a name="virtual-device-requirements"></a>Configuration requise de l'appareil virtuel
| **Composant** | **Prérequis** |
| --- | --- |
| Nombre minimal de processeurs virtuels (cœurs) |4 |
| Quantité minimale de mémoire (RAM) |8 Go <br> Pour un serveur de fichiers, 8 Go pour moins de 2 millions de fichiers et 16 Go pour 2 à 4 millions de fichiers|
| Espace disque<sup>1</sup> |Disque de système d'exploitation - 80 Go  <br></br>Disque de données - 500 Go too8 to |
| Nombre minimal d'interfaces réseau |1 |
| Bande passante Internet minimale<sup>2</sup> |5 Mbits/s |

<sup>1</sup> - Allocation dynamique

<sup>2</sup> -configuration réseau requise peut varier selon le taux de modification des données quotidiennes hello. Par exemple, si un appareil doit tooback 10 Go ou plus de modifications pendant une journée, puis hello sauvegarde quotidienne via une connexion Mbits/s 5 peut prendre des heures de too4.25 (si les données de hello n’a pas pu être compressées ou dédupliquées).

### <a name="supported-web-browsers"></a>Navigateurs web pris en charge
| **Composant** | **Version** | **Conditions/remarques supplémentaires** |
| --- | --- | --- |
| Microsoft Edge |Version la plus récente | |
| Internet Explorer |Version la plus récente |Testé avec Internet Explorer 11 |
| Google Chrome |Version la plus récente |Testé avec Chrome 46 |

### <a name="supported-storage-clients"></a>Clients de stockage pris en charge
Hello, suivant la configuration logicielle requise est pour les initiateurs iSCSI hello qui accèdent à votre tableau virtuel StorSimple (configuré comme un serveur iSCSI).

| **Systèmes d’exploitation pris en charge** | **Version requise** | **Conditions/remarques supplémentaires** |
| --- | --- | --- |
| Windows Server |2008 R2 SP1, 2012, 2012 R2 |StorSimple peut créer des volumes alloués dynamiquement et de façon complète. Il ne peut pas créer des volumes alloués partiellement. Les volumes iSCSI StorSimple sont pris en charge uniquement pour :  <ul><li>Volumes simples sur des disques de base Windows.</li><li>Windows NTFS pour formater un volume.</li> |

Hello, suivant la configuration logicielle requise est pourquoi les clients SMB qui accèdent à votre tableau virtuel StorSimple (configuré comme un serveur de fichiers).

| **Version SMB** |
| --- |
| SMB 2.x |
| SMB 3.0 |
| SMB 3.02 |

> [!IMPORTANT]
> Ne pas copier ou stocker des fichiers protégés par le serveur de fichiers Windows EFS (ENCRYPTING file) toohello StorSimple Virtual Array. Cela entraîne une configuration non prise en charge. 
> 

### <a name="supported-storage-format"></a>Format de stockage pris en charge
Uniquement hello stockage d’objets blob de blocs Azure est prise en charge. Les objets blob de pages ne sont pas pris en charge. En savoir plus [sur les objets blob de blocs et de pages](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).

## <a name="networking-requirements"></a>Configuration requise du réseau
Hello tableau suivant répertorie les ports hello nécessitant toobe ouvert dans votre tooallow de pare-feu pour iSCSI, SMB, cloud ou le trafic de gestion. Dans ce tableau, *dans* ou *entrant* fait référence direction toohello qui demandes entrantes des clients d’accéder à votre appareil. *Out* ou *sortant* fait référence direction toohello dans lequel votre appareil StorSimple envoie des données à l’extérieur, au-delà de déploiement de hello : par exemple, sortant toohello Internet.

| **Numéro de port<sup>1</sup>** | **Entrant ou sortant** | **Étendue de ports** | **Obligatoire** | **Remarques** |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP) |Sortie |WAN |Non |Port de sortie est utilisé pour les mises à jour de tooretrieve Internet access. <br></br>serveur proxy web sortant Hello est configurable par l’utilisateur. |
| TCP 443 (HTTPS) |Sortie |WAN |Oui |Port de sortie est utilisé pour accéder aux données dans le cloud de hello. <br></br>serveur proxy web sortant Hello est configurable par l’utilisateur. |
| UDP 53 (DNS) |Sortie |WAN |Dans certains cas, consultez les notes. |Ce port est requis seulement si vous utilisez un serveur DNS Internet. <br></br> Notez que si vous déployez un serveur de fichiers, nous recommandons l’utilisation d’un serveur DNS local. |
| UDP 123 (NTP) |Sortie |WAN |Dans certains cas, consultez les notes. |Ce port est requis seulement si vous utilisez un serveur NTP Internet.<br></br> Notez que si vous déployez un serveur de fichiers, nous vous recommandons de synchroniser l’heure avec vos contrôleurs de domaine Active Directory. |
| TCP 80 (HTTP) |Dans |LAN |Oui |Cela est hello port entrant pour l’interface utilisateur local sur l’appareil StorSimple hello pour la gestion locale. <br></br> Notez que l’accès à hello d’interface utilisateur locale sur HTTP redirige automatiquement tooHTTPS. |
| TCP 443 (HTTPS) |Dans |LAN |Oui |Cela est hello port entrant pour l’interface utilisateur local sur l’appareil StorSimple hello pour la gestion locale. |
| TCP 3260 (iSCSI) |Dans |LAN |Non |Ce port est utilisé tooaccess données via iSCSI. |

<sup>1</sup> aucun port entrant ne doit toobe ouvert sur hello Internet public.

> [!IMPORTANT]
> Assurez-vous que le pare-feu hello ne pas modifier ou déchiffrer tout le trafic SSL entre l’appareil StorSimple hello et Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Modèles d’URL pour règles de pare-feu
Les administrateurs réseau peuvent configurer souvent pare-feu avancé règles basées sur Bonjour URL modèles toofilter Bonjour entrant et le trafic sortant de hello. Votre tableau virtuel et le hello service du Gestionnaire de périphériques StorSimple reposent sur d’autres applications Microsoft tels que le Bus des services Azure, Azure Active Directory Access Control, comptes de stockage et les serveurs Microsoft Update. des modèles d’URL Hello associés à ces applications peuvent être utilisés tooconfigure les règles de pare-feu. Il est important toounderstand des modèles d’URL hello associés à ces applications susceptibles de changer. Cela sera à son tour nécessitent hello réseau administrateur toomonitor et mettre à jour les règles de pare-feu pour votre StorSimple en tant qu’et le cas échéant. 

Dans la plupart des cas, nous vous recommandons de définir librement les règles de pare-feu pour le trafic sortant en fonction des ADresses IP fixes StorSimple. Toutefois, vous pouvez utiliser des informations de hello ci-dessous tooset avancé des règles de pare-feu qui sont des environnements sécurisés toocreate nécessaires.

> [!NOTE]
> 
> * interfaces de réseau compatible cloud hello tooall doit toujours être défini à l’appareil de Hello (source) des adresses IP. 
> * destination Hello adresses IP doivent être défini trop[plages d’adresses IP de centre de données Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

| Modèle d’URL | Composant/Fonctionnalité |
| --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |Service StorSimple Device Manager<br>Service de contrôle d’accès<br>Azure Service Bus |
| `http://*.backup.windowsazure.com` |Enregistrement de l’appareil |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Révocation de certificat |
| `https://*.core.windows.net/*`<br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Comptes de stockage Azure et surveillance |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Serveurs Microsoft Update<br> |
| `http://*.deploy.akamaitechnologies.com` |CDN Akamai |
| `https://*.partners.extranet.microsoft.com/*` |Package de prise en charge |
| `http://*.data.microsoft.com ` |Le service de télémétrie dans Windows, consultez hello [mise à jour de l’expérience utilisateur et de télémétrie de diagnostic](https://support.microsoft.com/en-us/kb/3068708) |

## <a name="next-step"></a>Étape suivante
* [Préparer les toodeploy portail hello votre tableau virtuel StorSimple](storsimple-virtual-array-deploy1-portal-prep.md)

