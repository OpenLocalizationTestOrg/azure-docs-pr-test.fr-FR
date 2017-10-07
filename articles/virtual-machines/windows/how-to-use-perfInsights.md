---
title: aaaHow toouse PerfInsights dans Microsoft Azure | Documents Microsoft
description: "Apprend comment les problèmes de performances toouse PerfInsights tootroubleshoot machine virtuelle Windows."
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>Comment toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload) est un script automatisé qui collecte les informations de diagnostic utiles, exécute des charges d’e/s simultané (Stress) et fournit un toohelp de rapport d’analyse résoudre les problèmes de performances de machine virtuelle Windows dans Microsoft Azure. 

Nous vous recommandons d’exécuter ce script avant d’ouvrir un ticket de support Microsoft pour les problèmes de performances liés aux machines virtuelles.

## <a name="supported-troubleshooting-scenarios"></a>Scénarios de résolution des problèmes pris en charge

PerfInsights peut collecter et analyser plusieurs types d’informations qui sont regroupés dans des scénarios uniques.

### <a name="collect-disk-configuration"></a>Collecter la configuration de disque 

Ce scénario collecte la configuration de disque hello et autres informations importantes, y compris hello éléments suivants :

-   Journaux d’événements

-   État du réseau pour toutes les connexions entrantes et sortantes

-   Paramètres de configuration du pare-feu et du réseau

-   Liste des tâches pour toutes les applications qui sont en cours d’exécution sur le système de hello

-   Fichier d’informations créé par msinfo32 pour hello virtual machine (VM)

-   Paramètres de configuration de base de données Microsoft SQL Server (si hello machine virtuelle est identifié comme un serveur qui exécute SQL Server)

-   Compteurs de fiabilité de stockage

-   Correctifs logiciels Windows importants

-   Pilotes de filtre installés

Il s’agit d’une collection passive d’informations qui ne doivent pas affecter le système de hello. 

>[!Note]
>Ce scénario est automatiquement inclus dans chacun des scénarios suivants de hello.

### <a name="benchmarkstorage-performance-test"></a>Test de performances de stockage/d’évaluation

Ce scénario s’exécute hello [diskspd](https://github.com/Microsoft/diskspd) test (e/s et Mbits/s) du banc d’essai pour tous les lecteurs qui sont attachés toohello machine virtuelle. 

> [!Note]
> Ce scénario peut affecter les système hello et ne doit pas être exécuté sur un système de production en direct. Si nécessaire, exécutez ce scénario dans un tooavoid de fenêtre de maintenance dédiée tous les problèmes. Une charge de travail accrue provoquée par un test d’évaluation ou de trace peut nuire aux performances hello de votre machine virtuelle.
>

### <a name="general-vm-slow-analysis"></a>Analyse lente de machine virtuelle générale 

Ce scénario s’exécute un [compteur de performance](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) trace à l’aide de compteurs hello qui sont spécifiés dans le fichier de Generalcounters.txt hello. Si hello machine virtuelle est identifié comme un serveur qui exécute SQL Server, il exécute une trace de compteur de performances à l’aide de compteurs hello qui sont trouvent dans le fichier de Sqlcounters.txt hello. Cela inclut également des données de diagnostics de performances.

### <a name="vm-slow-analysis-and-benchmark"></a>Évaluation et analyse lente de la machine virtuelle

Ce scénario exécute un suivi du [compteur de performances](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx), puis un test d’évaluation [diskspd](https://github.com/Microsoft/diskspd). 

> [!Note]
> Ce scénario peut affecter les système hello et ne doit pas être exécuté sur un système de production en direct. Si nécessaire, exécutez ce scénario dans un tooavoid de fenêtre de maintenance dédiée tous les problèmes. Une charge de travail accrue provoquée par un test d’évaluation ou de trace peut nuire aux performances hello de votre machine virtuelle.
>

### <a name="azure-files-analysis"></a>Analyse de fichiers Azure 

Ce scénario exécute une capture du compteur de performances spéciale ainsi qu’un suivi du réseau. La capture inclut tous les compteurs de « Partages de Client SMB » hello. Hello Voici certaines clés client Partage de compteurs de performances SMB qui font partie de la capture de hello :

| **Type**     | **Compteur de partages de clients SMB** |
|--------------|-------------------------------|
| E/S par seconde         | Requêtes de données/s             |
|              | Requêtes de lecture/s             |
|              | Requêtes d’écriture/s            |
| Latency      | Requête de données/s (moyenne)         |
|              | Lecture/s (moyenne)                 |
|              | Écriture/s (moyenne)                |
| Taille d’E/S      | Avg. Octets/requête de données       |
|              | Avg. Octets/lecture               |
|              | Avg. Octets/écriture              |
| Débit   | Octets de données/s                |
|              | Octets de lecture/s                |
|              | Octets d’écriture/s               |
| Longueur de la file d’attente | Avg. Longueur de la file d’attente de lecture        |
|              | Avg. Longueur de la file d’attente d’écriture       |
|              | Avg. Longueur de la file d’attente de données        |

### <a name="custom-configuration"></a>Configuration personnalisée 

Lorsque vous exécutez une configuration personnalisée, vous exécutez tous les suivis (diagnostics de performances, compteur de performances, xperf, réseau, storport) en parallèle, selon le nombre de suivis sélectionné. Une fois le suivi est terminé, outil de hello exécute banc d’essai de diskspd hello, si elle est activée. 

> [!Note]
> Ce scénario peut affecter les système hello et ne doit pas être exécuté sur un système de production en direct. Si nécessaire, exécutez ce scénario dans un tooavoid de fenêtre de maintenance dédiée tous les problèmes. Une charge de travail accrue provoquée par un test d’évaluation ou de trace peut nuire aux performances hello de votre machine virtuelle.
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>Quelles informations sont collectées par le script de hello ?

Configuration des pools d’informations sur la machine virtuelle Windows, de disques ou de stockage, les compteurs de performance, les journaux et traces différents sont recueillies en fonction du scénario de performances hello utilisé :

|Données collectées                              |  |  | Scénarios de performances |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | Collecter la configuration de disque | Test de performances de stockage/d’évaluation | Analyse lente de machine virtuelle générale | Évaluation et analyse lente de la machine virtuelle | Analyse de fichiers Azure | Configuration personnalisée |
| Informations tirées des journaux d’événements      | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Informations système               | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Mappage de volume                       | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Mappage de disque                         | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Tâches en cours d’exécution                    | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Compteurs de fiabilité de stockage     | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Informations sur le stockage              | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Sortie Fsutil                    | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Informations du pilote de filtre               | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Sortie Netstat                   | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Configuration réseau            | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Configuration du pare-feu           | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Configuration de SQL Server         | Oui                        | Oui                                | Oui                      | Oui                            | Oui                  | Oui                  |
| Suivis des diagnostics de performances* |                            |                                    | Oui                      |                                |                      | Oui                  |
| Suivi du compteur de performances**     |                            |                                    |                          |                                |                      | Oui                  |
| Suivi du compteur SMB**             |                            |                                    |                          |                                | Oui                  |                      |
| Suivi du compteur SQL Server**      |                            |                                    |                          |                                |                      | Oui                  |
| Suivi XPerf                      |                            |                                    |                          |                                |                      | Oui                  |
| Suivi StorPort                   |                            |                                    |                          |                                |                      | Oui                  |
| Suivi réseau                    |                            |                                    |                          |                                | Oui                  | Oui                  |
| Suivi d’évaluation Diskspd***      |                            | Oui                                |                          | Oui                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>Suivi des diagnostics de performances (*)

Exécute un moteur de règles dans les données de toocollect hello en arrière-plan et de diagnostiquer les problèmes de performances en cours. Hello, suivant les règles est actuellement prises en charge :

- Règle de HighCpuUsage : détecte les périodes d’utilisation élevées du processeur et montre les principaux consommateurs de l’utilisation du processeur hello durant ces périodes.
- Règle de HighDiskUsage : détecte les périodes d’utilisation élevée du disque sur les disques physiques et montre des consommateurs de l’utilisation de disque supérieur de hello durant ces périodes.
- Règle HighResolutionDiskMetric : montre les mesures d’E/S par seconde, de débit et de latence d’E/S par intervalles de 50 millisecondes pour chaque disque physique. Il permet d’identifier les périodes de limitation de disque tooquickly.
- Règle de HighMemoryUsage : détecte les périodes d’utilisation élevée de la mémoire et montre des consommateurs de l’utilisation mémoire supérieure de hello durant ces périodes.

> [!NOTE] 
> Actuellement, les versions de Windows qui incluent hello .NET Framework 3.5 ou versions ultérieures sont pris en charge.

### <a name="performance-counter-trace-"></a>Suivi du compteur de performances (**)

Collecte hello suivant des compteurs de performances :

- \Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk
- \Cache\Dirty Pages, \Cache\Lazy Write Flushes/sec, \Server\Pool Nonpaged, Failures, \Server\Pool Paged Failures
- Certains compteurs sous \Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments, \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, \Per Processor Network Interface Card Activity, \Microsoft Winsock BSP

#### <a name="for-sql-server-instances"></a>Pour les instances SQL Server
- \SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\
- \SQLServer:Locks, \SQLServer:General, Statistics
- \SQLServer:Access Methods

#### <a name="for-azure-files"></a>Pour les fichiers Azure
\SMB Client Shares

### <a name="diskspd-benchmark-trace-"></a>Suivi d’évaluation Diskspd (***)
Tests de charge de travail d’E/S Diskspd [disque de système d’exploitation (écriture) et disques du pool (lecture/écriture)]

## <a name="run-hello-perfinsights-on-your-vm"></a>Exécutez hello PerfInsights sur votre machine virtuelle

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>Que dois-je tooknow avant d’exécuter les script hello ? 

**Configuration requise pour le script**

1.  Ce script doit être exécuté sur hello machine virtuelle qui rencontre un problème de performances hello. 

2.  Hello, systèmes d’exploitation suivants sont pris en charge : Windows Server 2008 R2, 2012, 2012 R2, 2016 ; Windows 8.1 et Windows 10.

**Problèmes possibles lorsque vous exécutez le script de hello sur les machines virtuelles de production :**

1.  script de Hello peut nuire aux performances hello Hello machine virtuelle lorsqu’il est utilisé avec le scénario hello « Référence » ou « Custom » qui est configuré à l’aide de XPerf ou DiskSpd. Soyez prudent lorsque vous exécutez le script de hello dans un environnement de production.

2.  Lorsque vous utilisez le script hello avec scénario hello « Référence » ou « Custom » qui est configuré à l’aide de DiskSpd, assurez-vous qu’aucune autre activité d’arrière-plan n’interfère avec la charge de travail d’e/s hello sur des disques hello testé.

3.  Par défaut, le script de hello utilise des données de toocollect de lecteur de stockage temporaire hello. Si le traçage est activé pour une durée plus longue, hello les données collectées est pertinente. Cela peut réduire la disponibilité de hello de l’espace sur le disque temporaire hello, par conséquent, affecter une application qui s’appuie sur ce lecteur.

### <a name="how-do-i-run-perfinsights"></a>Comment exécuter PerfInsights ? 

toorun hello script, procédez comme suit :

1. Téléchargez [PerfInsights.zip](http://aka.ms/perfinsightsdownload).

2. Débloquer hello PerfInsights.zip fichier. toodo ce fichier de PerfInsights.zip hello avec le bouton droit, sélectionnez **propriétés**. Bonjour **général** onglet, sélectionnez **Unblock** , puis sélectionnez **OK**. Cela permet de garantir que le script de hello s’exécute sans invite de toute la sécurité supplémentaire.  

    ![Déverrouiller le fichier zip de hello](media/how-to-use-perfInsights/unlock-file.png)

3.  Développez hello compressé PerfInsights.zip fichier dans votre lecteur temporaire (par défaut, généralement le lecteur hello D). Hello fichier compressé doit contenir les suivant hello fichiers et dossiers :

    ![fichiers dans un dossier zip de hello](media/how-to-use-perfInsights/file-folder.png)

4.  Ouvrez Windows PowerShell en tant qu’administrateur, puis exécutez le script de PerfInsights.ps1 hello.

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    Vous pouvez avoir tooenter « y » tooif vous êtes invité tooconfirm que stratégie d’exécution toochange hello.

    Dans la boîte de dialogue hello exclusion de responsabilité, vous pouvez soit hello option tooshare des informations de diagnostic avec le Support technique de Microsoft. Vous devez également donner son consentement toocontinue de contrat de licence toohello. Procédez à vos sélections, puis cliquez sur **Exécuter le script**.

    ![Boîte de dialogue Exclusion](media/how-to-use-perfInsights/disclaimer.png)

5.  Soumettre le nombre de cas de hello, s’il est disponible, lorsque vous exécutez le script hello (il s’agit de notre statistiques). Cliquez ensuite sur **OK**.
    
    ![entrer l’ID de support](media/how-to-use-perfInsights/enter-support-number.png)

6.  Sélectionnez votre disque de stockage temporaire. Hello Script peut détecte automatiquement les hello lettre de lecteur hello lecteur. Si des problèmes surviennent dans cette étape, vous pouvez être invité à entrer le lecteur de hello tooselect (lecteur par défaut de hello est D). Journaux générés sont stockés ici dans le journal de hello\_dossier de la collection. Une fois que vous entrez ou acceptez la lettre de lecteur hello, cliquez sur **OK**.

    ![entrer le disque](media/how-to-use-perfInsights/enter-drive.png)

7.  Sélectionnez un scénario de dépannage dans hello liste.

       ![Sélectionner des scénarios de support](media/how-to-use-perfInsights/select-scenarios.png)

8.  Vous pouvez également exécuter PerfInsights sans interface utilisateur.

    suivant de Hello commande s’exécute hello « Analyse général VM lente » scénario sans une invite de commandes de l’interface utilisateur de résolution des problèmes ou capture des données pendant 30 secondes. Il vous invite tooconsent toohello même exclusion de responsabilité et le CLUF qui sont mentionnés à l’étape 4.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    Si vous souhaitez PerfInsights toorun en mode silencieux, utilisez la **- AcceptDisclaimerAndShareDiagnostics** paramètre. Par exemple, utilisez hello de commande suivante :

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>Comment résoudre des problèmes lors de l’exécution du script de hello ?

Si le script de hello s’est terminé anormalement, vous pouvez nettoyer un état incohérent en exécutant le script hello avec hello - commutateur de nettoyage, comme suit :

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

Si des problèmes se produisent pendant la détection automatique du lecteur temporaire de hello hello, vous pouvez être invité à entrer le lecteur de hello tooselect (lecteur par défaut de hello est D).

![entrer le disque](media/how-to-use-perfInsights/enter-drive.png)

script de Hello désinstalle des outils d’utilitaires hello et supprime les dossiers temporaires.

### <a name="troubleshooting-other-script-issues"></a>Résolution d’autres problèmes de script 

Si des problèmes se produisent lorsque vous exécutez le script de hello, appuyez sur l’exécution du script Ctrl + C toointerrupt hello. tooremove des objets temporaires, consultez la section de « Nettoyer après un arrêt anormal » hello.

Si vous continuez l’échec du script tooexperience même après plusieurs tentatives, nous vous recommandons d’exécuter les script hello en « mode de débogage » à l’aide de hello »-déboguer « option de paramètre au démarrage.

Échec de hello, hello copier la sortie complète de la console PowerShell hello, et il envoie l’agent de Support technique de Microsoft de toohello qui vous assistera toohelp dépannage hello.

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>Comment exécuter les script hello en mode de configuration personnalisée ?

En sélectionnant hello **personnalisé** configuration, vous pouvez activer plusieurs traces en parallèle (utilisez MAJ toomulti-select) :

![sélectionner des scénarios](media/how-to-use-perfInsights/select-scenario.png)

Lorsque vous sélectionnez hello Diagnostics de performances, suivi du compteur de performances, XPerf Trace, Trace réseau ou les scénarios de suivi de Storport, suivez les instructions de hello dans les boîtes de dialogue hello, puis essayez de problèmes de performances tooreproduce hello après le démarrage de traces de hello.

Hello suivant la boîte de dialogue vous permet de démarrer une trace :

![lancer un suivi](media/how-to-use-perfInsights/start-trace-message.png)

traces de hello toostop, vous avez commande hello de tooconfirm dans la boîte de dialogue.

![arrêter un suivi](media/how-to-use-perfInsights/stop-trace-message.png)
![arrêter un suivi](media/how-to-use-perfInsights/ok-trace-message.png)

Hello lorsque des traces ou les opérations sont terminées, un nouveau fichier est généré dans le lecteur D:\\journal\_collection (ou lecteur temporaire de hello) qui est nommé **CollectedData\_AAAA-MM-jj\_hh\_mm \_ss.zip.** Vous pouvez envoyer cet agent de prise en charge de toohello de fichier pour l’analyse.

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>Passez en revue le rapport de diagnostics hello créé par PerfInsights

Au sein de hello **CollectedData\_AAAA-MM-jj\_hh\_mm\_ss.zip fichier** qui est généré par PerfInsights, vous pouvez trouver un rapport HTML qui détaille les conclusions hello PerfInsights. tooreview hello de rapport, développez hello **CollectedData\_AAAA-MM-jj\_hh\_mm\_ss.zip** de fichier, puis ouvrez hello **PerfInsights report.htm**fichier.

Sélectionnez hello **conclusions** onglet.

![onglet Rechercher](media/how-to-use-perfInsights/findingtab.png)

**Remarques**

-   Les messages qui s’affichent en rouge sont des problèmes de configuration connus qui peuvent provoquer des problèmes de performances.

-   Messages qui s’affichent en jaune sont des avertissements qui représentent des configurations non optimales ne provoquant pas forcément de problèmes de performances.

-   Les messages qui s’affichent en bleu sont présentés à titre informatif uniquement.

Hello de révision des liens HTTP pour tous les messages d’erreur rouge tooget plus des informations détaillées sur les conclusions hello et comment ils peuvent affecter les performances de hello ou les meilleures pratiques pour les configurations de performances optimisées.

### <a name="disk-configuration-tab"></a>Onglet Configuration du disque

Hello **vue d’ensemble** section affiche les différentes vues de la configuration de stockage hello, y compris des informations à partir de Diskpart et des espaces de stockage

Hello **DiskMap** et **VolumeMap** sections décrivent sur un point de vue double logique des volumes et disques physiques sont associé tooeach autres.

Bonjour PhysicalDisk perspective (DiskMap), table de hello affiche tous les volumes logiques qui sont en cours d’exécution sur le disque de hello. Dans l’exemple suivant de hello, PhysicalDrive2 exécute 2 des Volumes logiques créés sur plusieurs partitions (J et H) :

![onglet Données](media/how-to-use-perfInsights/disktab.png)

Bonjour perspective du Volume (*VolumeMap*), les tables hello affichent tous les disques physiques hello sous chaque volume logique. Pour les disques RAID/dynamiques, vous pouvez exécuter un volume logique sur plusieurs disques physiques. Bonjour suivant exemple *C:\\de montage* est un point de montage configuré en tant que *SpannedDisk* sur des disques physiques \#2 et \#3 :

![onglet Volume](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>Onglet Serveur SQL

Si la cible de hello machine virtuelle héberge toutes les instances de SQL Server, vous verrez un onglet supplémentaire dans le rapport hello nommé **SQL Server**:

![onglet sql](media/how-to-use-perfInsights/sqltab.png)

Cette section contient une « vue d’ensemble » et les onglets de sub supplémentaires pour chacune des instances de SQL Server hello hébergés sur hello machine virtuelle.

Hello section « Présentation » contient une table utile qui résume toutes les hello disques physiques (disques système et de données) qui sont en cours d’exécution et qui contiennent un mélange de fichiers de données et fichiers journaux des transactions.

Bonjour, l’exemple suivant *PhysicalDrive0* (en cours d’exécution lecteur de hello C) est affichée, car les deux hello *modeldev* et *modellog* fichiers se trouvent sur le lecteur de hello C, et ils sont de types différents (tels que le fichier de données et le journal des transactions, respectivement) :

![loginfo](media/how-to-use-perfInsights/loginfo.png)

onglets spécifiques à l’instance de SQL Server Hello contient une section générale qui affiche des informations de base sur l’instance sélectionnée de hello et les autres sections pour plus d’informations, y compris les paramètres, les Configurations et les Options de l’utilisateur.

## <a name="references-toohello-external-tools-used"></a>Fait référence à des outils externes toohello utilisés

### <a name="diskspd"></a>Diskspd

DISKSPD est un stockage charge générateur et performances outil de test à partir de hello Windows et Windows Server et l’Infrastructure de serveur Cloud équipes d’ingénierie. Pour plus d’informations, consultez [Diskspd](https://github.com/Microsoft/diskspd).

### <a name="xperf"></a>XPerf

Xperf est une trace de toocapture d’outil de ligne de commande à partir de hello Kit d’outils de performances de Windows.

Pour plus d’informations, consultez [Windows Performance Toolkit : Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).

## <a name="next-steps"></a>Étapes suivantes

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>Télécharger des journaux de diagnostics et tooMicrosoft prise en charge pour un examen approfondi des rapports

Lorsque vous travaillez avec hello personnel de Support technique de Microsoft, vous pouvez être sortie hello tootransmit demandé qui est généré par hello de tooassist PerfInsights processus de dépannage.

l’agent de prise en charge Hello créera un espace de travail DTM pour vous, et vous recevrez un message électronique qui inclut un toohello de lien [DTM portail (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) et d’un ID d’utilisateur unique et d’un mot de passe.

Ce message sera envoyé à partir de **CTS Automated Diagnostics Services** (ctsadiag@microsoft.com).

![Exemple de message de type hello](media/how-to-use-perfInsights/supportemail.png)

Pour renforcer la sécurité, vous serez requis toochange votre mot de passe sur tout d’abord utiliser.

Une fois que vous vous connectez dans tooDTM, vous trouverez un hello de tooupload de boîte de dialogue **CollectedData\_AAAA-MM-jj\_hh\_mm\_ss.zip** fichier qui a été collecté par PerfInsights.
