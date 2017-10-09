---
title: "configuration système requise du aaaStorSimple 8000 series | Documents Microsoft"
description: "Décrit la configuration requise et les meilleures pratiques en matière de logiciel, de mise en réseau et de haute disponibilité pour une solution Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: f13ccdb7cb317d72c60e9c2fe49937764d10b43e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-software-high-availability-and-networking-requirements"></a>Configurations logicielles, de haute disponibilité et réseau requises pour StorSimple 8000 Series

## <a name="overview"></a>Vue d'ensemble

Bienvenue dans tooMicrosoft Azure StorSimple. Cet article décrit important requise et meilleures pratiques pour votre appareil StorSimple et pour les clients de stockage hello accédant au périphérique de hello. Nous vous recommandons de consulter attentivement les informations hello avant de déployer votre système StorSimple, puis consultez tooit si nécessaire pendant le déploiement et les opérations suivantes.

Hello requise :

* **Configuration logicielle requise pour les clients de stockage** -décrit hello pris en charge les systèmes d’exploitation et des exigences supplémentaires pour ces systèmes d’exploitation.
* **Configuration réseau requise pour l’appareil StorSimple hello** -fournit des informations sur les ports de hello que toobe besoin ouvert dans votre tooallow pare-feu pour le trafic iSCSI, cloud ou la gestion.
* **Conditions requises de haute disponibilité pour StorSimple** : décrit les exigences de haute disponibilité et les meilleures pratiques pour votre ordinateur hôte et votre appareil StorSimple.

## <a name="software-requirements-for-storage-clients"></a>Configuration logicielle requise pour les clients de stockage

Hello, suivant la configuration logicielle requise est pour les clients de stockage hello qui accèdent à votre appareil StorSimple.

| Systèmes d’exploitation pris en charge | Version requise | Conditions/remarques supplémentaires |
| --- | --- | --- |
| Windows Server |2008 R2 SP1, 2012, 2012 R2, 2016 |Les volumes iSCSI StorSimple sont pris en charge pour une utilisation sur hello uniquement les types de disques Windows suivants :<ul><li>Volume simple sur disque de base</li><li>Volume simple et en miroir sur disque dynamique</li></ul>Uniquement hello initiateurs logiciels iSCSI présents en mode natif dans le système d’exploitation de hello sont pris en charge. Les initiateurs matériels iSCSI ne sont pas pris en charge.<br></br>L’allocation dynamique Windows Server 2012 et 2016 les fonctionnalités ODX sont prises en charge si vous utilisez un volume iSCSI StorSimple.<br><br>StorSimple peut créer des volumes alloués dynamiquement et de façon complète. Il ne permet pas de créer des volumes entièrement ou partiellement alloués.<br><br>Le reformatage d’un volume alloué dynamiquement peut prendre beaucoup de temps. Nous vous recommandons de supprimer hello volume, puis en créant un nouveau au lieu de reformater. Toutefois, si vous avez toujours préférer tooreformat un volume :<ul><li>Exécutez hello commande avant des retards de récupération hello reformater tooavoid espace suivante : <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>Après la mise en forme de hello, suivant de hello utilisez commande toore activer la récupération de l’espace :<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>Appliquer le correctif de Windows Server 2012 de hello comme décrit dans [Ko 2878635](https://support.microsoft.com/kb/2870270) ordinateur de Windows Server tooyour.</li></ul></li></ul></ul> Si vous configurez le Gestionnaire d’instantanés StorSimple ou de l’adaptateur StorSimple pour SharePoint, passez trop[configuration logicielle requise pour les composants facultatifs](#software-requirements-for-optional-components). |
| VMWare ESX |5.5 et 6.0 |Pris en charge avec VMware vSphere en tant que client iSCSI. La fonctionnalité VAAI-block est prise en charge avec VMware vSphere sur les appareils StorSimple. |
| Linux RHEL/CentOS |5, 6 et 7 |Prise en charge des clients Linux iSCSI avec initiateur Open-iSCSI versions 5, 6 et 7. |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> IBM AIX n’est actuellement pas pris en charge avec StorSimple.


## <a name="software-requirements-for-optional-components"></a>Configuration logicielle requise pour les composants facultatifs

Hello, suivant la configuration logicielle requise est pour hello StorSimple composants facultatifs (Gestionnaire d’instantanés StorSimple et de l’adaptateur StorSimple pour SharePoint).

| Composant | Plateforme hôte | Conditions/remarques supplémentaires |
| --- | --- | --- |
| StorSimple Snapshot Manager |Windows Server 2008 R2 SP1, 2012, 2012 R2 |L’utilisation du Gestionnaire d’instantanés StorSimple sur Windows Server est requise pour la sauvegarde/restauration des disques dynamiques en miroir et pour les sauvegardes cohérentes avec les applications.<br> StorSimple Snapshot Manager est pris en charge uniquement sous Windows Server 2008 R2 SP1 (64 bits), Windows Server 2012 R2 et Windows Server 2012.<ul><li>Si vous utilisez Windows Server 2012, vous devez installer .NET 3.5-4.5 avant d’installer le Gestionnaire d’instantanés StorSimple.</li><li>Si vous utilisez Windows Server 2008 R2 SP1, vous devez installer Windows Management Framework 3.0 avant d’installer le Gestionnaire d’instantanés StorSimple.</li></ul> |
| Adaptateur StorSimple pour SharePoint |Windows Server 2008 R2 SP1, 2012, 2012 R2 |<ul><li>L'adaptateur StorSimple pour SharePoint est uniquement pris en charge sur SharePoint 2010 et SharePoint 2013.</li><li>RBS requiert SQL Server Enterprise Edition, version 2008 R2 ou 2012.</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>Configuration réseau requise pour votre appareil StorSimple

Votre appareil StorSimple est un appareil verrouillé. Toutefois, les ports doivent toobe ouvert dans votre tooallow de pare-feu pour le trafic de gestion, iSCSI et cloud. Hello tableau suivant répertorie les ports hello nécessitant toobe ouvert dans votre pare-feu. Dans ce tableau, *dans* ou *entrant* fait référence direction toohello qui demandes entrantes des clients d’accéder à votre appareil. *Out* ou *sortant* fait référence direction toohello dans lequel votre appareil StorSimple envoie des données à l’extérieur, au-delà de déploiement de hello : par exemple, sortant toohello Internet.

| Numéro de port <sup>1,2</sup> | Entrant ou sortant | Étendue de ports | Requis | Remarques |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP)<sup>3</sup> |Sortie |WAN |Non |<ul><li>Port de sortie est utilisé pour les mises à jour de tooretrieve Internet access.</li><li>serveur proxy web sortant Hello est configurable par l’utilisateur.</li><li>mises à jour du système tooallow, ce port doit également être ouvert pour hello IP fixé du contrôleur.</li></ul> |
| TCP 443 (HTTPS)<sup>3</sup> |Sortie |WAN |Oui |<ul><li>Port de sortie est utilisé pour accéder aux données dans le cloud de hello.</li><li>serveur proxy web sortant Hello est configurable par l’utilisateur.</li><li>mises à jour du système tooallow, ce port doit également être ouvert pour hello IP fixé du contrôleur.</li><li>Ce port est également utilisé sur les deux contrôleurs hello pour le garbage collection.</li></ul> |
| UDP 53 (DNS) |Sortie |WAN |Dans certains cas, consultez les notes. |Ce port est requis seulement si vous utilisez un serveur DNS Internet. |
| UDP 123 (NTP) |Sortie |WAN |Dans certains cas, consultez les notes. |Ce port est requis seulement si vous utilisez un serveur NTP Internet. |
| TCP 9354 |Sortie |WAN |Oui |le port sortant Hello est utilisé par toocommunicate de périphérique StorSimple hello avec hello service du Gestionnaire de périphériques StorSimple. |
| 3260 (iSCSI) |Dans |LAN |Non |Ce port est utilisé tooaccess données via iSCSI. |
| 5985 |Dans |LAN |Non |Le port entrant est utilisé par le Gestionnaire d’instantanés StorSimple toocommunicate avec l’appareil StorSimple hello.<br>Ce port est également utilisé lorsque vous vous connectez à distance tooWindows PowerShell pour StorSimple sur HTTP. |
| 5986 |Dans |LAN |Non |Ce port est utilisé lorsque vous vous connectez à distance tooWindows PowerShell pour StorSimple sur HTTPS. |

<sup>1</sup> aucun port entrant ne doit toobe ouvert sur hello Internet public.

<sup>2</sup> si plusieurs ports comportent une configuration de passerelle, hello ordre du trafic routé sortant est déterminé en fonction de l’ordre de routage de port hello décrite dans [routage de Port](#routing-metric), ci-dessous.

<sup>3</sup> contrôleur hello adresses IP fixé sur votre appareil StorSimple doit être routable et en mesure de tooconnect toohello Internet directement ou via hello configuré le proxy web. Hello fixée des adresses IP sont utilisées pour la maintenance des appareils de toohello hello mises à jour. Si les contrôleurs de périphérique hello ne peut pas se connecter à toohello Internet via hello des adresses IP fixes, vous ne serez pas en mesure de tooupdate votre appareil StorSimple.

> [!IMPORTANT]
> Assurez-vous que le pare-feu hello ne pas modifier ou déchiffrer tout le trafic SSL entre l’appareil StorSimple hello et Azure.


### <a name="url-patterns-for-firewall-rules"></a>Modèles d’URL pour règles de pare-feu

Les administrateurs réseau peuvent configurer souvent pare-feu avancé règles basées sur Bonjour URL modèles toofilter Bonjour entrant et le trafic sortant de hello. Votre appareil StorSimple et le hello service du Gestionnaire de périphériques StorSimple reposent sur d’autres applications Microsoft tels que le Bus des services Azure, Azure Active Directory Access Control, comptes de stockage et les serveurs Microsoft Update. des modèles d’URL Hello associés à ces applications peuvent être utilisés tooconfigure les règles de pare-feu. Il est important toounderstand des modèles d’URL hello associés à ces applications susceptibles de changer. Cela sera à son tour nécessitent hello réseau administrateur toomonitor et mettre à jour les règles de pare-feu pour votre StorSimple en tant qu’et le cas échéant.

Dans la plupart des cas, nous vous recommandons de définir librement les règles de pare-feu pour le trafic sortant en fonction des ADresses IP fixes StorSimple. Toutefois, vous pouvez utiliser des informations de hello ci-dessous tooset avancé des règles de pare-feu qui sont des environnements sécurisés toocreate nécessaires.

> [!NOTE]
> interfaces de réseau tooall hello activé doit toujours être défini à l’appareil de Hello (source) des adresses IP. destination Hello adresses IP doivent être défini trop[plages d’adresses IP de centre de données Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).


#### <a name="url-patterns-for-azure-portal"></a>Modèles d’URL pour le portail Azure

| Modèle d’URL | Composant/Fonctionnalité | Adresses IP d’appareil |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*`<br>`https://login.windows.net` |Service StorSimple Device Manager<br>Service de contrôle d’accès<br>Azure Service Bus<br>Service d’authentification |Interfaces réseau activées pour le cloud |
| `https://*.backup.windowsazure.com` |Enregistrement de l’appareil |DATA 0 uniquement |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Révocation de certificat |Interfaces réseau activées pour le cloud |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Comptes de stockage Azure et surveillance |Interfaces réseau activées pour le cloud |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Serveurs Microsoft Update<br> |Adresses IP fixes du contrôleur uniquement |
| `http://*.deploy.akamaitechnologies.com` |CDN Akamai |Adresses IP fixes du contrôleur uniquement |
| `https://*.partners.extranet.microsoft.com/*`<br>`https://dcupload.microsoft.com/`<br>`https://*.support.microsoft.com/` |Package de prise en charge |Interfaces réseau activées pour le cloud |

#### <a name="url-patterns-for-azure-government-portal"></a>Modèles d’URL pour le portail Azure Government

| Modèle d’URL | Composant/Fonctionnalité | Adresses IP d’appareil |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*`<br>`https://login-us.microsoftonline.com` |Service StorSimple Device Manager<br>Service de contrôle d’accès<br>Azure Service Bus<br>Service d’authentification |Interfaces réseau activées pour le cloud |
| `https://*.backup.windowsazure.us` |Enregistrement de l’appareil |DATA 0 uniquement |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Révocation de certificat |Interfaces réseau activées pour le cloud |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Comptes de stockage Azure et surveillance |Interfaces réseau activées pour le cloud |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Serveurs Microsoft Update<br> |Adresses IP fixes du contrôleur uniquement |
| `http://*.deploy.akamaitechnologies.com` |CDN Akamai |Adresses IP fixes du contrôleur uniquement |
| `https://*.partners.extranet.microsoft.com/*`<br>`https://dcupload.microsoft.com/`<br>`https://*.support.microsoft.com/` |Package de prise en charge |Interfaces réseau activées pour le cloud |

### <a name="routing-metric"></a>Métrique de routage

Une métrique de routage est associée à des interfaces de hello et passerelle hello Router hello toohello de données spécifié réseaux. Métrique de routage est utilisé par hello routage protocole toocalculate hello meilleures chemin d’accès tooa donnée de destination, si elle a appris plusieurs chemins d’accès existent toohello même destination. Hello inférieur hello routage métrique, hello hello une préférence plus élevée.

Bonjour contexte de StorSimple, si plusieurs interfaces réseau et les passerelles sont configurés toochannel trafic, les métriques de routage hello entrent en ordre relatif play toodetermine hello dans le hello interfaces obtenir servira. métriques de routage Hello ne peut pas être modifié par l’utilisateur de hello. Toutefois, vous pouvez utiliser hello `Get-HcsRoutingTable` tooprint d’applet de commande hello table de routage (et mesures) sur votre appareil StorSimple. Pour plus d’informations sur l’applet de commande Get-HcsRoutingTable, consultez le [dépannage du déploiement StorSimple](storsimple-troubleshoot-deployment.md).

algorithme métrique de routage Hello utilisé pour la mise à jour 2 et versions ultérieures permettre être décrites comme suit.

* Les interfaces toonetwork ont été affectés à un ensemble de valeurs prédéterminées.
* Considérez une table de l’exemple ci-dessous avec les valeurs assignées toohello diverses interfaces réseau lorsqu’ils sont cloud activé ou désactivé en nuage, mais avec une passerelle configurée. Remarque Les valeurs hello affectés ici sont des valeurs d’exemple uniquement.

    | Interface réseau | Activée pour le cloud | Désactivée pour le cloud avec passerelle |
    |-----|---------------|---------------------------|
    | Data 0  | 1            | -                        |
    | Data 1  | 2            | 20                       |
    | Data 2  | 3            | 30                       |
    | Data 3  | 4            | 40                       |
    | Data 4  | 5            | 50                       |
    | Data 5  | 6            | 60                       |


* commande Hello dans lequel le trafic de nuage hello sera routé via des interfaces réseau hello est la suivante :
  
    *Data 0 &gt; Data 1 &gt; Date 2 &gt; Data 3 &gt; Data 4 &gt; Data 5*
  
    Cela peut s’expliquer par hello l’exemple suivant.
  
    Prenez l’exemple d’un appareil StorSimple avec deux interfaces réseau activées pour le cloud, Data 0 et Data 5. Data 1 à Data 4 sont désactivées pour le cloud mais disposent d’une passerelle configurée. commande Hello dans lequel le trafic est routé pour cet appareil sera :
  
    *Data 0 (1) &gt; Data 5 (6) &gt; Data 1 (20) &gt; Data 2 (30) &gt; Data 3 (40) &gt; Data 4 (50)*
  
    *nombres de Hello entre parenthèses indiquent les métriques de routage respectifs hello.*
  
    En cas de Data 0, le trafic de nuage hello est routé à Data 5. Étant donné qu’une passerelle est configurée sur le réseau, si Data 0 et Data 5 étaient toofail, le trafic de nuage hello allez parcourir les données 1.
* Si une interface réseau compatible cloud échoue, puis sont 3 tentatives avec une interface 30 toohello de tooconnect deuxième délai. Si toutes les tentatives de hello échouent, le trafic de hello est routé toohello suivant disponible activé pour le cloud interface comme déterminé par la table de routage hello. Si tous les hello activé pour le cloud échouent des interfaces réseau, puis les appareil hello basculent toohello autre contrôleur (pas de redémarrage dans ce cas).
* En cas d’échec de l’adresse IP virtuelle pour une interface réseau compatible iSCSI, 3 tentatives seront effectuées à une intervalle de 2 secondes. Ce comportement est restée hello même depuis des versions précédentes de hello. Si toutes les interfaces de réseau iSCSI hello échouent, un basculement de contrôleur se produit (accompagné par un redémarrage).
* Une alerte est également émise sur votre appareil StorSimple en cas d’échec de l’adresse IP virtuelle. Pour plus d’informations, consultez trop[aide-mémoire d’alerte](storsimple-8000-manage-alerts.md).
* En ce qui concerne les nouvelles tentatives, iSCSI a priorité sur le cloud.
  
    Envisagez de hello l’exemple suivant : StorSimple un périphérique possède deux interfaces réseau activés, Data 0 et 1 de données. Data 0 est activée pour le cloud tandis que Data 1 est à la fois activée pour le cloud et compatible iSCSI. Aucune autre interface réseau sur cet appareil n’est activée pour le cloud ou compatible iSCSI.
  
    Si des données 1 échoue, étant donnés qu’il est la dernière interface de réseau iSCSI hello, cela entraîne un tooData de basculement du contrôleur 1 hello sur autre contrôleur.

### <a name="networking-best-practices"></a>Meilleures pratiques de mise en réseau

En outre toohello au-dessus de la configuration réseau requise, pour hello optimiser les performances de votre solution StorSimple, veuillez adhérer toohello suivant les meilleures pratiques :

* Assurez-vous que votre appareil StorSimple a une bande passante dédiée de 40 Mbits/s (ou plus) disponible à tout moment. La bande passante ne doit pas être partagée (ou l’allocation doit être garantie via l’utilisation de hello des stratégies de QoS) avec d’autres applications.
* Vérifiez toohello de connectivité réseau Internet est disponible en permanence. Sporadiques ou non fiables connexions toohello périphériques Internet, sans connexion Internet que ce soit, y compris les entraîne une configuration non prise en charge.
* Isoler le trafic iSCSI et cloud de hello en dédiant des interfaces réseau sur votre appareil pour l’accès iSCSI et cloud. Pour plus d’informations, consultez Comment trop[modifier des interfaces réseau](storsimple-8000-modify-device-config.md#modify-network-interfaces) sur votre appareil StorSimple.
* N’utilisez pas une configuration Link Aggregation Control Protocol (LACP) pour vos interfaces réseau. Cette configuration n’est pas prise en charge.

## <a name="high-availability-requirements-for-storsimple"></a>Conditions requises de haute disponibilité pour StorSimple

plateforme matérielle Hello qui est inclus dans la solution de StorSimple hello possède des fonctionnalités de disponibilité et de fiabilité qui constituent la base d’une infrastructure de stockage hautement disponible et à tolérance de pannes dans votre centre de données. Toutefois, configuration requise et meilleures pratiques que vous devez respecter toohelp garantir la disponibilité de hello de votre solution StorSimple. Avant de déployer StorSimple, lisez attentivement hello suivant la configuration requise et meilleures pratiques pour l’appareil StorSimple hello et connecté des ordinateurs hôtes.

Pour plus d’informations sur la surveillance et la maintenance des composants matériels de hello de votre appareil StorSimple, consultez trop[utiliser l’état et les composants matériels de hello le Gestionnaire de périphériques StorSimple service toomonitor](storsimple-8000-monitor-hardware-status.md) et [ Remplacement de composant matériel StorSimple](storsimple-8000-hardware-component-replacement.md).

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>Configuration requise pour la haute disponibilité et procédures pour votre appareil StorSimple

Hello révision suivant attentivement les informations tooensure hello haute disponibilité de votre appareil StorSimple.

#### <a name="pcms"></a>Modules PCM

Les appareils StorSimple incluent des modules d’alimentation et de refroidissement redondants et échangeables à chaud (PCM). Chaque PCM a suffisamment service tooprovide de capacité charge ensemble du châssis hello. tooensure haute disponibilité, les deux modules PCM doit être installée.

* Connectez votre disponibilité tooprovide de PCM toodifferent power sources si une source d’alimentation échoue.
* Si un module PCM tombe en panne, demandez immédiatement son remplacement.
* Supprimer un PCM défaillant uniquement lorsque vous disposez de remplacement de hello et prêt tooinstall il.
* Ne supprimez pas les deux modules PCM en même temps. module PCM Hello inclut un module de batterie de secours hello. Retrait des deux Hello PCM entraînera un arrêt sans protection par batterie et état de l’appareil hello n’est pas enregistrée. Pour plus d’informations sur la batterie de hello, accédez trop[module de batterie de secours de tenir à jour hello](storsimple-8000-battery-replacement.md#maintain-the-backup-battery-module).

#### <a name="controller-modules"></a>Modules de contrôleur

Les appareils StorSimple incluent des modules de contrôleur redondants et échangeables à chaud. modules de contrôleur Hello fonctionnent en mode actif/passif. À un moment donné, un module de contrôleur est actif et fournit un service, hello lors de l’autre module de contrôleur est passive. module de contrôleur passif Hello est sous tension et devient opérationnel si le module de contrôleur actif hello échoue ou est supprimé. Chaque module de contrôleur a suffisamment service tooprovide de capacité charge ensemble du châssis hello. Les deux modules de contrôleur doivent être installés tooensure haute disponibilité.

* Assurez-vous que les deux modules de contrôleur sont installés en permanence.
* En cas de panne d’un module de contrôleur, demandez immédiatement son remplacement.
* Supprimer un module de contrôleur uniquement lorsque vous disposez de remplacement de hello et prêt tooinstall il. Retrait d’un module pendant des périodes prolongées affectera la ventilation de hello et donc hello refroidissement du système de hello.
* Assurez-vous que les modules de contrôleur tooboth hello réseau connexions sont identiques et interfaces réseau connectées hello ont une configuration de réseau identiques.
* Si un module de contrôleur tombe en panne ou doit être remplacé, assurez-vous que hello autre module de contrôleur est dans un état actif avant de remplacer le module de contrôleur défectueux hello. tooverify qu’un contrôleur est actif, accédez trop[contrôleur actif de hello identifier sur votre appareil](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device).
* Ne supprimez pas les deux modules de contrôleur à hello même temps. Si un basculement de contrôleur est en cours d’exécution, ne pas arrêter le module de contrôleur de secours hello ou supprimez-le du châssis de hello.
* Après un basculement de contrôleur, attendez au moins cinq minutes avant de retirer l’un des deux modules de contrôleur.

#### <a name="network-interfaces"></a>Interfaces réseau

Les modules de contrôleur d’un appareil StorSimple possèdent chacun quatre interfaces réseau 1 Gigabit et deux interfaces réseau 10 Gigabit Ethernet.

* Vous assurer que les modules de contrôleur tooboth hello réseau connexions sont identiques, et des interfaces réseau de hello que les interfaces de module de contrôleur hello sont connecté toohave une configuration réseau identiques.
* Lorsque cela est possible, déployez les connexions réseau entre la disponibilité du service différents commutateurs tooensure dans les cas de hello d’une panne de périphérique réseau.
* Lorsque vous déconnectez hello uniquement ou le dernier hello compatible iSCSI d’interface (avec les adresses IP affectée), désactivez d’abord les interface hello, puis débranchez les câbles hello. Si l’interface de hello est débranché tout d’abord, il entraîne puis hello contrôleur actif toofail sur le contrôleur passif de toohello. Si le contrôleur passif de hello a également ses interfaces correspondantes déconnectés, les deux contrôleurs hello va redémarrer plusieurs fois avant de s’installer sur un seul contrôleur.
* Se connecter au moins deux réseau toohello interfaces à partir de chaque module de contrôleur.
* Si vous avez activé des interfaces de hello deux de 10 GbE, déployez-les entre les différents commutateurs.
* Lorsque cela est possible, utilisez MPIO sur tooensure de serveurs que les serveurs hello peuvent tolérer un lien, un réseau ou une défaillance de l’interface.

Pour plus d’informations sur la mise en réseau de votre appareil pour la haute disponibilité et performances, accédez trop[installer votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [installer votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

#### <a name="ssds-and-hdds"></a>Disques SSD et disques durs

Un appareil StorSimple comprend des disques SSD et des disques durs qui sont protégés au moyen d'espaces en miroir. Utilisation d’espaces en miroir garantit que Hello est Échec de hello tootolerate en mesure d’un ou plusieurs disques SSD ou disques durs.

* Assurez-vous que tous les disques SSD et disques durs sont en place.
* Si un disque SSD ou un disque dur tombe en panne, demandez immédiatement son remplacement.
* Si un disque SSD ou un disque dur tombe en panne ou défectueux, assurez-vous que vous supprimez hello SSD ou défectueux.
* Ne retirez pas plus d’un disque SSD ou HDD système hello à n’importe quel point dans le temps.
  Si au moins deux disques d’un même type (disque dur ou disque SSD) tombent en panne ou que plusieurs pannes consécutives surviennent en peu de temps, un dysfonctionnement du système et une perte potentielle de données risquent de se produire. Si cela se produit, [contactez le support Microsoft](storsimple-8000-contact-microsoft-support.md) .
* En cas de remplacement, surveillez hello **des composants partagés** Bonjour **l’intégrité du matériel** panneau pour hello disques SSD de hello et des disques durs. Une coche verte indique que les disques hello sont intègres ou OK, tandis que le point d’un point d’exclamation rouge indique un échec sur disque SSD ou HDD.
* Nous vous recommandons de configurer les instantanés cloud pour tous les volumes que vous avez besoin de tooprotect en cas de défaillance du système.

#### <a name="ebod-enclosure"></a>Boîtier EBOD

Modèle d’appareil StorSimple 8600 inclut un ensemble de disques boîtier EBOD (Extended) dans le boîtier principal du toohello Ajout. Un boîtier EBOD se compose de contrôleurs EBOD et de disques durs qui sont protégés à l’aide d’espaces en miroir. Utilisation d’espaces en miroir garantit que Hello est Échec de hello tootolerate en mesure d’un ou plusieurs disques durs. Hello boîtier EBOD est connecté toohello le boîtier principal câbles SAS redondants.

* Assurez-vous que les deux modules de contrôleur du boîtier EBOD, les deux câbles SAS et tous les lecteurs de disque dur hello sont installés à tout moment.
* Si un module de contrôleur de boîtier EBOD tombe en panne, demandez immédiatement son remplacement.
* Si un module de contrôleur du boîtier EBOD échoue, assurez-vous que ce hello autre module de contrôleur est actif avant de remplacer le module défaillant de hello. tooverify qu’un contrôleur est actif, accédez trop[contrôleur actif de hello identifier sur votre appareil](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device).
* Au cours d’un remplacement d’un module EBOD contrôleur, de surveiller en continu état hello du composant hello Bonjour service du Gestionnaire de périphériques StorSimple en accédant à **moniteur** > **l’intégrité du matériel** .
* Si un câble SAS tombe en panne ou défectueux (Support technique de Microsoft doivent être impliqué toomake cette décision), assurez-vous que vous supprimez uniquement les câble SAS hello nécessite un remplacement.
* Ne pas simultanément supprimez les deux câbles SAS système hello à n’importe quel point dans le temps.

### <a name="high-availability-recommendations-for-your-host-computers"></a>Recommandations relatives à la haute disponibilité de vos ordinateurs hôtes

Lisez attentivement ces meilleures pratiques tooensure hello haute disponibilité de l’appareil StorSimple hôtes tooyour connecté.

* Configurez StorSimple avec des [configurations de cluster de serveur de fichiers à deux nœuds][1]. En supprimant des points uniques de panne et en assurant la redondance côté hôte de hello, solution complète de hello devient hautement disponible.
* Utilisez partages (CA) disponibles en permanence disponibles avec Windows Server 2012 (SMB 3.0) pour la haute disponibilité pendant le basculement des contrôleurs de stockage hello. Pour plus d’informations pour la configuration des clusters de serveur de fichiers et les partages disponibles en continu avec Windows Server 2012, consultez toothis [vidéo de démonstration](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares).

## <a name="next-steps"></a>Étapes suivantes

* [En savoir plus sur les limites du système StorSimple](storsimple-8000-limits.md).
* [Découvrez comment toodeploy votre solution StorSimple](storsimple-8000-deployment-walkthrough-u2.md).

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx
