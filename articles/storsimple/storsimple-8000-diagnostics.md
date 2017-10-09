---
title: Appareil de tootroubleshoot StorSimple 8000 outil aaaDiagnostics | Documents Microsoft
description: "Décrit les modes du périphérique StorSimple hello et explique comment toouse Windows PowerShell pour StorSimple toochange hello mode de l’appareil."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a>Utilisez les problèmes de périphériques série 8000 hello outil de diagnostic StorSimple tootroubleshoot

## <a name="overview"></a>Vue d'ensemble

Hello, outil de diagnostic de StorSimple diagnostique toosystem connexes de problèmes, les performances, réseau et l’intégrité du composant matériel pour un appareil StorSimple. outil de diagnostic Hello peut être utilisé dans divers scénarios. Ces scénarios incluent la planification de la charge de travail, déploiement d’un appareil StorSimple, évaluer l’environnement de réseau hello et déterminer les performances d’une unité opérationnelle hello. Cet article fournit une vue d’ensemble de l’outil de diagnostic hello et décrit comment les outil hello peuvent être utilisé avec un appareil StorSimple.

outil de diagnostic Hello est principalement utilisée pour les appareils StorSimple 8000 series local (8100 et 8600).

## <a name="run-diagnostics-tool"></a>Exécuter l’outil de diagnostic

Cet outil peut être exécuté via l’interface Windows PowerShell de hello de votre appareil StorSimple. Il existe deux façons tooaccess hello interface locale de votre appareil :

* [Console série du périphérique toohello tooconnect PuTTY utilisation](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
* [Accéder à distance à outil hello via hello Windows PowerShell pour StorSimple](storsimple-remote-connect.md).

Dans cet article, nous supposons que vous avez connecté la console série du périphérique toohello via PuTTY.

#### <a name="toorun-hello-diagnostics-tool"></a>outil de diagnostic hello toorun

Une fois que vous avez connecté l’interface Windows PowerShell de toohello du périphérique de hello, effectuer hello suivant les étapes toorun hello applet de commande.
1. Ouvrez une session sur la console série du périphérique toohello en suivant les étapes de hello dans [console série du périphérique toohello tooconnect utilisez PuTTY](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).

2. Tapez hello de commande suivante :

    `Invoke-HcsDiagnostics`

    Si le paramètre d’étendue hello n’est pas spécifié, hello applet de commande exécute tous les tests de diagnostic hello. Ceux-ci incluent des tests du système, de l’intégrité des composants matériels, du réseau et des performances. 
    
    toorun un test spécifique, spécifier un paramètre d’étendue hello. Par exemple, toorun uniquement hello réseau test, type

    `Invoke-HcsDiagnostics -Scope Network`

3. Sélectionner et copier la sortie de hello hello PuTTY fenêtre dans un fichier texte pour une analyse plus approfondie.

## <a name="scenarios-toouse-hello-diagnostics-tool"></a>Outil de diagnostic de scénarios toouse hello

Utilisez hello diagnostics outil tootroubleshoot hello réseau, les performances, système et matériel d’intégrité du système de hello. Voici quelques scénarios possibles :

* **Appareil hors connexion** : votre appareil de la gamme StorSimple 8000 est hors connexion. Toutefois, à partir de l’interface Windows PowerShell de hello, il semble que les deux contrôleurs hello sont en cours d’exécution.
    * Vous pouvez utiliser cet outil toothen déterminer l’état du réseau hello.
         
         > [!NOTE]
         > N’utilisez pas cette tooassess performances et les paramètres réseau sur un appareil avant l’inscription de hello (ou de configurer via l’Assistant d’installation). Une adresse IP valide est attribuée toohello périphérique lors de l’inscription et l’Assistant installation. Vous pouvez exécuter cette applet de commande sur un appareil qui n’est pas inscrit pour évaluer l’intégrité matérielle et le système. Utilisez le paramètre d’étendue hello, par exemple :
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* **Problèmes de l’appareil persistant** -vous rencontrez des problèmes de l’appareil qui semblent toopersist. Par exemple, son inscription échoue. Vous pouvez également rencontrer des problèmes de périphérique une fois hello appareil correctement inscrit et opérationnel pendant un certain temps.
    * Dans ce cas, utilisez cet outil pour procéder à un dépannage préliminaire avant d’enregistrer une demande de service auprès du Support Microsoft. Nous vous conseillons d’exécuter cette sortie hello outil et de capture de cet outil. Vous pouvez ensuite fournir cette sortie tooSupport tooexpedite procédure de dépannage.
    * En cas de défaillances de composants matériels ou de clusters, vous devez enregistrer une demande de Support.

* **Faibles performances de l’appareil** : votre appareil StorSimple est lent.
    * Dans ce cas, exécutez cette applet de commande avec tooperformance de jeu de paramètres de portée. Analyser la sortie de hello. Vous obtenez le cloud de hello latences de lecture-écriture. Hello d’utilisation signalées facteur dans une surcharge pour le traitement des données internes hello et latences en tant que cible réalisable maximale, puis déployer les charges de travail hello sur le système de hello. Pour plus d’informations, consultez trop[utiliser les performances de l’appareil hello réseau test tootroubleshoot](#network-test).


## <a name="diagnostics-test-and-sample-outputs"></a>Tests de diagnostic et exemples de sorties

### <a name="hardware-test"></a>Test du matériel

Ce test détermine hello état des composants matériels de hello, le microprogramme USM hello et du microprogramme du disque hello en cours d’exécution sur votre système.

* les composants de matériels Hello signalés sont ces composants ce test hello ayant échoué ou ne sont pas présentes dans le système de hello.
* versions du microprogramme Hello USM microprogramme et de disque sont signalées pour hello contrôleur 0, le contrôleur 1 et des composants partagés de votre système. Pour obtenir une liste complète des composants matériels, consultez :

    * [Composants du boîtier principal](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [Composants du boîtier EBOD](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> Si les composants en échec, des rapports de test sur du matériel hello [connectez-vous à une demande de service avec le Support technique de Microsoft](storsimple-contact-microsoft-support.md).

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a>Exemple de sortie du test du matériel sur un appareil 8100

Voici un exemple de sortie pour un appareil StorSimple 8100. Dans l’appareil de modèle 8100 hello, hello boîtiers n’est pas présente. Par conséquent, les composants du contrôleur EBOD hello ne sont pas signalées.

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a>Test du système

Ce test signale des informations de système de hello, hello mises à jour disponibles, les informations de cluster hello et informations du service hello pour votre appareil.

* informations de système de Hello incluent hello modèle, numéro de série de périphérique, fuseau horaire, l’état du contrôleur et en cours d’exécution sur le système de hello de la version du logiciel détaillées hello. hello toounderstand divers paramètres système signalés en tant que sortie de hello, accédez trop[interprétation des informations système](#appendix-interpreting-system-information).

* rapports de disponibilité de mises à jour de Hello si les modes standard et la maintenance hello sont disponibles et leurs noms de package associé. Si `RegularUpdates` et `MaintenanceModeUpdates` sont `false`, cela indique que les mises à jour hello ne sont pas disponibles. Votre appareil est à jour.
* cluster Hello contient hello des informations sur les différents composants de logiques de tous les groupes de cluster HCS hello et leurs États respectifs. Si vous voyez un groupe de clusters en mode hors connexion dans cette section du rapport de hello, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md).
* informations sur le service Hello incluent les noms de hello et états de tous les hello HCS et services des éléments de configuration en cours d’exécution sur votre appareil. Ces informations sont utiles pour hello Support Microsoft à résoudre les problème de périphérique hello.

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a>Exemple de sortie du test du système sur un appareil 8100

Voici un exemple de sortie hello système de série de tests sur un appareil 8100.

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a>Test du réseau

Ce test vérifie l’état de hello des interfaces réseau de hello, ports, DNS et NTP connectivité du serveur, SSL certificat, informations d’identification du compte de stockage, serveurs de mise à jour toohello de connectivité et connectivité de proxy web sur votre appareil StorSimple.

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a>Exemple de sortie du test du réseau lorsque seule l’interface DATA0 est activée

Voici un exemple de sortie de l’appareil de 8100 hello. Vous pouvez voir dans la sortie de hello qui :
* Seules les interfaces réseau DATA0 et DATA1 sont activées et configurées.
* 2 à 5 de données ne sont pas activées dans le portail de hello.
* configuration du serveur DNS Hello est valide et appareils de hello de se connecter via des serveurs DNS hello.
* Hello connectivité du serveur NTP fonctionne également bien.
* Les ports 80 et 443 sont ouverts. Toutefois, le port 9354 est bloqué. En fonction de hello [configuration système requise du réseau](storsimple-system-requirements.md), vous devez tooopen ce port pour la communication de bus de service hello.
* la certification SSL de Hello est valide.
* Hello appareils de se connecter compte de stockage toohello : _myss8000storageacct_.
* serveurs de tooUpdate Hello connectivité n’est valide.
* le proxy web Hello n’est pas configuré sur ce périphérique.

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a>Exemple de sortie du test du réseau lorsque les interfaces DATA0 et DATA1 sont activées

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a>Test de performance

Ce test signale les performances du cloud hello via des latences de lecture-écriture hello cloud pour votre appareil. Cet outil peut être utilisé tooestablish une ligne de base des performances de cloud hello que vous pouvez obtenir avec StorSimple. Hello outil rapports hello performances maximales (scénario meilleur des cas de latence de lecture-écriture) que vous pouvez obtenir pour votre connexion.

Outil de hello rapports des performances maximales réalisable hello, nous pouvons utiliser hello déclarée en lecture-écriture latences cibles lors du déploiement hello les charges de travail.

test de Hello simule les tailles de blob hello associées aux types de volume différent hello sur l’appareil de hello. Les volumes hiérarchisés standard et les sauvegardes des volumes épinglés localement utilisent une taille d’objet blob de 64 Ko. Les volumes hiérarchisés avec option d’archivage activée utilisent une taille d’objet blob de 512 Ko. Si votre appareil a volumes attachés localement et hiérarchisés configuré, seuls hello test too64 Ko objet blob correspondant taille des données est exécutée.

toouse cette outil, effectuer hello comme suit :

1.  Tout d’abord, créez un ensemble de volumes hiérarchisés et de volumes hiérarchisés avec option d’archivage activée. Cette action garantit que cet outil hello exécute les tests de hello 64 Ko et 512 Ko pour les tailles des objets blob.

2. Exécuter l’applet de commande hello après avoir créé et configuré les volumes hello. Entrez :

    `Invoke-HcsDiagnostics -Scope Performance`

3. Prenez note des latences de lecture-écriture hello signalés par l’outil de hello. Ce test peut prendre plusieurs minutes toorun avant de signaler les résultats hello.

4. Si le temps de latence de connexion hello sont tous sous hello plages attendues, puis hello latences signalés par l’outil de hello est utilisable comme cible réalisable maximale lors du déploiement de charges de travail hello. Prenez en compte une certaine surcharge pour le traitement interne des données.

    Si la latence de lecture-écriture hello signalés par outil de diagnostic hello sont élevées :

    1. Configurer le stockage Analytique pour les services blob et analysez les hello sortie toounderstand hello latences pour hello compte de stockage Azure. Pour obtenir des instructions détaillées, consultez trop[activer et configurer le stockage Analytique](../storage/common/storage-enable-and-view-metrics.md). Si ces temps de latence sont également numéros élevée et comparables toohello que vous avez reçu de hello outil de diagnostic de StorSimple, vous devez toolog une demande de service avec le stockage Azure.

    2. Si les latences de compte de stockage hello sont insuffisantes, contactez votre tooinvestigate d’administrateur réseau aucun temps d’attente de problèmes dans votre réseau.

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a>Exemple de sortie du test des performances sur un appareil 8100

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a>Annexe : Interprétation des informations système

Voici un tableau décrivant le hello différents paramètres de Windows PowerShell dans les informations de système de hello mappent à. 

| Paramètre PowerShell    | Description  |
|-------------------------|------------------|
| ID de l’instance             | Un identificateur unique ou un GUID est associé à chaque contrôleur.|
| Nom                    | nom convivial de Hello du périphérique hello configuré via hello portail Azure pendant le déploiement de l’appareil. nom convivial de Hello par défaut est le numéro de série du périphérique hello. |
| Modèle                   | modèle Hello de votre appareil de série StorSimple 8000. modèle de Hello peut être 8100 ou 8600.|
| SerialNumber            | numéro de série du périphérique Hello est attribué à la fabrique de hello et 15 caractères. Par exemple, 8600-SHX0991003G44HT indique :<br> 8600 – est le modèle d’appareil hello.<br>SHX – hello fabrication site.<br> 0991003 : produit spécifique. <br> G44HT-hello 5 derniers chiffres sont incrémentés toocreate les numéros de série uniques. Il ne s’agit pas nécessairement d’une suite.|
| TimeZone                | Hello fuseau horaire configuré Bonjour Azure portal durant le déploiement de l’appareil.|
| CurrentController       | contrôleur Hello que vous êtes connecté toothrough interface de Windows PowerShell hello de votre appareil StorSimple.|
| ActiveController        | contrôleur Hello qui est active sur votre appareil et contrôle toutes les opérations de réseau et disque hello. Il peut s’agir du contrôleur 0 ou du contrôleur 1.  |
| Controller0Status       | état de Hello du contrôleur 0 sur votre appareil. état du contrôleur Hello peut être normal, en mode de récupération ou inaccessible.|
| Controller1Status       | état de Hello du contrôleur 1 sur votre appareil.  état du contrôleur Hello peut être normal, en mode de récupération ou inaccessible.|
| SystemMode              | Bonjour à l’état global de votre appareil StorSimple. état du périphérique Hello peut être normal, maintenance, ou mis hors service (correspond toodeactivated Bonjour portail Azure).|
| FriendlySoftwareVersion | chaîne conviviale Hello correspondant toohello version du logiciel. Pour un système exécutant la mise à jour 4, version du logiciel convivial hello serait StorSimple 8000 Series Update 4.0.|
| HcsSoftwareVersion      | version du logiciel HCS Hello en cours d’exécution sur votre appareil. Par exemple, hello tooStorSimple correspondante de la version logicielle HCS 8000 Series Update 4.0 est 6.3.9600.17820. |
| ApiVersion              | version du logiciel Hello Hello API PowerShell de Windows du périphérique HCS de hello.|
| VhdVersion              | version du logiciel Hello d’image de fabrique hello hello périphérique a été livré avec. Si vous réinitialisez votre toofactory de périphérique par défaut, puis il exécute cette version du logiciel.|
| OSVersion:               | version du logiciel Hello de hello système d’exploitation Windows en cours d’exécution sur l’appareil de hello. hello Windows Server 2012 R2 correspondant too6.3.9600 est basée sur l’appareil StorSimple Hello.|
| CisAgentVersion         | version Hello pour votre agent d’éléments de configuration en cours d’exécution sur votre appareil StorSimple. Cet agent permet de communiquer avec le service StorSimple Manager hello s’exécutant dans Azure.|
| MdsAgentVersion         | Hello version toohello Mds agent correspondant en cours d’exécution sur votre appareil StorSimple. Cet agent déplace les données toohello analyse et Diagnostics de Service (MDS).|
| Lsisas2Version          | Bonjour version des pilotes toohello LSI correspondants sur votre appareil StorSimple.|
| Capacity                | capacité totale de Hello du périphérique hello en octets.|
| RemoteManagementMode    | Indique si les appareils hello peuvent être gérés à distance via son interface Windows PowerShell. |
| FipsMode                | Indique si le mode hello United States traitement Standard FIPS (Federal Information) est activé sur votre appareil. norme de Hello FIPS 140 définit les algorithmes de chiffrement approuvés pour une utilisation par les systèmes d’ordinateur gouvernement fédéral nous pour une protection des données sensibles hello. Pour les appareils exécutant Update 4 ou version ultérieure, le mode FIPS est activé par défaut. |

## <a name="next-steps"></a>Étapes suivantes

* En savoir plus hello [syntaxe de l’applet de commande Invoke-HcsDiagnostics de hello](https://technet.microsoft.com/library/mt795371.aspx).

* En savoir plus sur la façon trop[résoudre les problèmes de déploiement](storsimple-troubleshoot-deployment.md) sur votre appareil StorSimple.
