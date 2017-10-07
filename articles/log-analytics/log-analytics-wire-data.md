---
title: "aaaWire solution de données dans le journal Analytique | Documents Microsoft"
description: "Les données de communication sont des données de réseau et de performance centralisées issues d’ordinateurs sur lesquels des agents OMS sont installés, notamment Operations Manager et les agents connectés à Windows. Données réseau sont combinées avec votre toohelp de données de journal vous corréler les données."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Solution Wire Data 2.0 (préversion) dans Log Analytics

![Symbole de Wire Data](./media/log-analytics-wire-data/wire-data2-symbol.png)

Les données de communication sont des données réseau et des données de performances consolidées, provenant d’ordinateurs équipés d’agents OMS, notamment les agents Operations Manager, connectés à Windows et Linux. Données réseau sont combinées avec vos autres toohelp de données de journal vous corréler les données.

En outre tooOMS agents, hello solution données de collecte utilise des agents Microsoft Dependency que vous installez sur les ordinateurs dans votre infrastructure informatique. Hello en 2 à 3 niveaux de tooand de données envoyées dépendance Agents Moniteur réseau à partir de vos ordinateurs pour le réseau [modèle OSI](https://en.wikipedia.org/wiki/OSI_model), y compris hello différents protocoles et ports utilisés. Les données sont ensuite envoyées tooLog Analytique à l’aide d’agents.

> [!NOTE]
> Vous ne pouvez pas ajouter version précédente de hello d’espaces de travail toonew hello Wire Data solution. Si vous avez activée la solution données réseau et d’origine hello, vous pouvez continuer toouse il. Toutefois, toouse câble données 2.0, vous devez d’abord supprimer version d’origine de hello.

Par défaut, Log Analytics recueille les données enregistrées dans les journaux concernant les performances du processeur, de la mémoire, des disques et du réseau à partir de compteurs intégrés à Windows. Collecte réseau et autres données s’effectue en temps réel pour chaque agent, y compris les sous-réseaux et les protocoles de niveau application utilisés par hello ordinateur. Vous pouvez ajouter d’autres compteurs de performance sur la page des paramètres sur l’onglet journaux de hello hello.

Si vous avez utilisé [sFlow](http://www.sflow.org/) ou d’autres logiciels avec [protocole NetFlow de Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), puis hello statistiques et que vous voyez à partir des données de collecte des données seront tooyou familier.

Voici quelques-uns des types hello de requêtes de recherche de journal intégrées :

- Agents qui fournissent des données de communication
- Adresse IP des agents fournissant des données de communication
- Communications sortantes par adresse IP
- Nombre d’octets envoyés par les protocoles d’application
- Nombre d’octets envoyés par un service d’application
- Octets reçus par différents protocoles
- Nombre total d’octets envoyés et reçus par version d’adresse IP
- Latence moyenne pour les connexions qui ont été mesurées de manière fiable
- Processus informatiques ayant initié ou reçu du trafic réseau
- Quantité de trafic réseau pour un processus

Lorsque vous recherchez à l’aide des données de collecte, vous pouvez filtrer et groupe données tooview informations hello principaux agents et protocoles. Vous pouvez aussi savoir quand certains ordinateurs (adresses IP/MAC) ont communiqué les uns avec les autres et connaître la durée de ces communications et la quantité de données envoyées. En fait, vous affichez des métadonnées sur le trafic réseau, qui fonctionne par recherches.

Toutefois, comme il s’agit de métadonnées, elles ne sont pas nécessairement utiles pour résoudre des problèmes complexes. Les données de communication de Log Analytics ne capturent pas toutes les données réseau. Elles ne sont donc pas censées être utilisées pour résoudre des problèmes complexes au niveau du paquet. Hello avantage de l’utilisation de l’agent de hello, par rapport à des méthodes de collection tooother, est que vous ne disposez tooinstall appliances, reconfigurer vos commutateurs réseau ou dispenser complexe. Données de collecte sont simplement basées sur l’agent, vous installez l’agent de hello sur un ordinateur et celui-ci analyse son propre trafic réseau. Un autre avantage est lorsque vous souhaitez que les charges de travail toomonitor en cours d’exécution dans les fournisseurs de cloud ou fournisseur de services ou Microsoft Azure, où les utilisateurs hello ne possèdent pas de couche d’infrastructure hello.

## <a name="connected-sources"></a>Sources connectées

Les données réseau et obtient ses données à partir de hello Agent de dépendances Microsoft. Hello Agent de dépendances dépend hello Agent OMS pour son tooLog connexions Analytique. Cela signifie qu’un serveur doit avoir hello OMS Agent installé et configuré le premier et vous installez hello Agent de dépendances. Hello tableau suivant décrit les sources de hello connecté qui prend en charge de la solution de données de collecte hello.

| **Source connectée** | **Pris en charge** | **Description** |
| --- | --- | --- |
| Agents Windows | Oui | Wire Data analyse et collecte des données provenant d’ordinateurs agents Windows. <br><br> En outre toohello [Agent OMS](log-analytics-windows-agents.md), agents Windows nécessitent hello Agent de dépendances Microsoft. Consultez hello [prise en charge des systèmes d’exploitation](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) pour une liste complète des versions de système d’exploitation. |
| Agents Linux | Oui | Wire Data analyse et collecte des données provenant d’ordinateurs agents Linux.<br><br> En outre toohello [Agent OMS](log-analytics-linux-agents.md), agents Linux nécessitent hello Agent de dépendances Microsoft. Consultez hello [prise en charge des systèmes d’exploitation](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) pour une liste complète des versions de système d’exploitation. |
| Groupe d’administration Microsoft System Center Operations Manager | Oui | Wire Data analyse et collecte des données provenant des agents Windows et Linux dans un [groupe d’administration System Center Operations Manager](log-analytics-om-agents.md) connecté. <br><br> Une connexion directe à partir de hello System Center Operations Manager agent ordinateur tooLog Analytique est requis. Données sont transférées à partir de hello gestion groupe tooLog Analytique. |
| Compte Azure Storage | Non | Les données réseau et collecte les données à partir d’ordinateurs de l’agent, il n’existe pas de données à partir de celui-ci toocollect depuis le stockage Azure. |

Sous Windows, hello Microsoft Monitoring Agent (MMA) est utilisé par System Center Operations Manager et Analytique de journal toogather et envoyer des données. Selon le contexte de hello, l’agent de hello est appelée hello Agent System Center Operations Manager, OMS Agent, l’Agent Analytique de journal, MMA ou Agent Direct. System Center Operations Manager et Analytique de journal fournissent des versions légèrement différentes de hello MMA. Ces versions de chaque rapport tooSystem Center Operations Manager, tooLog Analytique ou tooboth.

Sur Linux, hello Agent OMS pour Linux collecte et envoie des données tooLog Analytique. Vous pouvez utiliser les données de collecte sur les serveurs dotés d’Agents Direct OMS ou sur des serveurs qui sont attaché tooLog Analytique via des groupes d’administration System Center Operations Manager.

Dans cet article, fait référence à des agents tooall, si Linux ou Windows, groupe d’administration System Center Operations Manager tooa connecté directement ou tooLog Analytique qui sont appelés hello _agent OMS_. Nous allons utiliser le nom de déploiement spécifique de hello de l’agent de hello uniquement si elle est nécessaire pour le contexte.

Hello Agent de dépendances ne transmet pas les données elles-mêmes, et il ne nécessite pas de modifications toofirewalls ou des ports. données Hello dans les données de collecte sont toujours transmises par hello OMS agent tooLog Analytique, soit directement ou à l’aide de hello OMS passerelle.

![diagramme de l’agent](./media/log-analytics-wire-data/agents.png)

Si vous êtes un utilisateur de System Center Operations Manager avec un tooLog de groupe connecté gestion Analytique :

- Aucune configuration supplémentaire n’est requise lors de vos agents de System Center Operations Manager peuvent accéder hello Internet tooconnect tooLog Analytique.
- Vous devez tooconfigure hello OMS passerelle toowork avec System Center Operations Manager lorsque vos agents de System Center Operations Manager ne peut pas accéder à l’Analytique de journal sur hello Internet.

Si vous utilisez hello Agent Direct, vous avez besoin de tooconfigure hello OMS agent lui-même tooconnect tooLog Analytique ou tooyour OMS passerelle. Vous pouvez télécharger hello OMS passerelle hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

## <a name="prerequisites"></a>Composants requis

- Requiert hello [Insight & Analytique](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) offre des solutions.
- Si vous utilisez une version précédente de hello Hello solution données de collecte, vous devez tout d’abord le supprimer. Toutefois, toutes les données obtenues à partir de la solution de données de collecte hello d’origine est toujours disponible dans le câble données 2.0 et de recherche de journal.
- Des privilèges d’administrateur sont requis tooinstall ou désinstaller hello Agent de dépendances.
- Hello dépendance Agent doit être installé sur un ordinateur avec un système d’exploitation de 64 bits.

### <a name="operating-systems"></a>Systèmes d’exploitation

Hello sections suivantes répertorient hello pris en charge les systèmes d’exploitation pour hello Agent de dépendances. Wire Data ne prend pas en charge les architectures 32 bits, quel que soit le système d’exploitation.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

#### <a name="windows-desktop"></a>Ordinateurs Windows

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux et Oracle Linux (avec noyau RHEL)

- Seules les versions du noyau SMP Linux et par défaut sont prises en charge.
- Les versions non standard du noyau, par exemple PAE et Xen, ne sont prises en charge par aucune distribution Linux. Par exemple, un système avec la chaîne de version hello de _2.6.16.21-0.8-xen_ n’est pas pris en charge.
- Les noyaux personnalisés, y compris les recompilations de noyaux standard, ne sont pas pris en charge.
- Le noyau CentOSPlus n’est pas pris en charge.
- Oracle Unbreakable Enterprise Kernel (UEK) est traité dans une autre section, plus loin dans cet article.

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **Version du SE** | **Version du noyau** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **Version du SE** | **Version du noyau** |
| --- | --- |
| 6.0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4. | 2.6.32-358 |
| 6.5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6,8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5

| **Version du SE** | **Version du noyau** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18-417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux avec Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **Version du SE** | **Version du noyau** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4. | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **Version du SE** | **Version du noyau** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **Version du SE** | **Version du noyau** |
| --- | --- |
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **Version du SE** | **Version du noyau** |
| --- | --- |
| 10 SP4 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>Téléchargements de l’agent de dépendances

| **File** | **SE** | **Version** | **SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>Configuration

Effectuer hello suivant les étapes tooconfigure hello câble solution des données pour vos espaces de travail.

1. Activer la solution Analytique de journal d’activité hello hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).
2. Installer hello dépendance Agent sur chaque ordinateur où vous souhaitez que les données de tooget. Hello Agent de dépendances peut surveiller voisins tooimmediate de connexions, donc vous n’ayez pas d’un agent sur chaque ordinateur.

### <a name="install-hello-dependency-agent-on-windows"></a>Installer hello Agent de dépendances sur Windows

Des privilèges d’administrateur sont requis tooinstall ou désinstaller l’agent de hello.

Hello dépendance Agent est installé sur les ordinateurs exécutant Windows via InstallDependencyAgent-Windows.exe. Si vous exécutez ce fichier exécutable sans option, il démarre un Assistant que vous pouvez suivre tooinstall de manière interactive.

Hello suivant les étapes tooinstall hello dépendance Agent sur chaque ordinateur exécutant Windows, utilisez :

1. Installation hello Agent OMS à l’aide d’instructions hello à [toohello d’ordinateurs Windows de se connecter service Analytique de journal dans Azure](log-analytics-windows-agents.md).
2. Télécharger l’agent de Windows hello à l’aide du lien de hello dans la section précédente de hello et exécutez-le à l’aide de hello de commande suivante : InstallDependencyAgent-Windows.exe
3. Suivez l’agent de hello Assistant tooinstall hello.
4. En cas de hello dépendance Agent toostart, vérifiez les journaux de hello pour les informations d’erreur détaillées. Sur les agents Windows, le répertoire de journal de hello est %Programfiles%\Microsoft Agent\logs de dépendance.

#### <a name="windows-command-line"></a>Ligne de commande Windows

Utilisez les options de hello suivant tooinstall de la table à partir d’une ligne de commande. toosee une liste des indicateurs d’installation Bonjour, exécutez le programme d’installation de hello à l’aide de hello / ? comme suit.

InstallDependencyAgent-Windows.exe /?

| **Indicateur** | **Description** |
| --- | --- |
| <code>/?</code> | Obtenir la liste des options de ligne de commande hello. |
| <code>/S</code> | Effectuez une installation silencieuse sans invite utilisateur. |

Fichiers de hello Agent de dépendances de Windows sont placés dans C:\Program Files\Microsoft dépendance Agent par défaut.

### <a name="install-hello-dependency-agent-on-linux"></a>Installer hello Agent de dépendances sur Linux

Accès à la racine est requise tooinstall ou configurer l’agent de hello.

Hello dépendance Agent est installé sur les ordinateurs Linux via InstallDependencyAgent-Linux64.bin, un script de shell dans un fichier binaire à extraction automatique. Vous pouvez exécuter hello à l’aide _sh_ ou ajouter d’exécuter le fichier de toohello autorisations lui-même.

Hello suivant les étapes tooinstall hello dépendance Agent sur chaque ordinateur Linux, utilisez :

1. Installation hello Agent OMS à l’aide d’instructions hello à [collecter et gérer les données des ordinateurs Linux](log-analytics-agent-linux.md).
2. Télécharger l’agent de dépendance de Linux hello à l’aide du lien de hello dans la section précédente de hello et l’installer en tant que racine à l’aide de hello de commande suivante : sh-Linux64.bin InstallDependencyAgent
3. En cas de hello dépendance Agent toostart, vérifiez les journaux de hello pour les informations d’erreur détaillées. Sur les agents de Linux, le répertoire du journal hello est : /var/opt/microsoft/dependency-agent/log.

toosee une liste d’indicateurs d’installation hello, exécutez le programme d’installation de hello avec hello `-help` indicateur comme suit.

```
InstallDependencyAgent-Linux64.bin -help
```

| **Indicateur** | **Description** |
| --- | --- |
| <code>-help</code> | Obtenir la liste des options de ligne de commande hello. |
| <code>-s</code> | Effectuez une installation silencieuse sans invite utilisateur. |
| <code>--check</code> | Vérifiez les autorisations et le système d’exploitation de hello, mais ne pas installer l’agent de hello. |

Fichiers pourquoi l’Agent de dépendance sont placés dans hello suivant répertoires :

| **Fichiers** | **Emplacement** |
| --- | --- |
| Fichiers principaux | /opt/microsoft/dependency-agent |
| Fichiers journaux | /var/opt/microsoft/dependency-agent/log |
| Fichiers de configuration | /etc/opt/microsoft/dependency-agent/config |
| Fichiers exécutables de service | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br><br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Fichiers de stockage binaires | /var/opt/microsoft/dependency-agent/storage |

### <a name="installation-script-examples"></a>Exemples de script d’installation

tooeasily déployer hello Agent de dépendances sur plusieurs serveurs à la fois, il vous aide à toouse un script. Vous pouvez utiliser hello suivant toodownload des exemples de script et installer hello Agent de dépendances sur Windows ou Linux.

#### <a name="powershell-script-for-windows"></a>Script PowerShell pour Windows

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>Script shell pour Linux

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>Configuration de l’état souhaité (DSC)

toodeploy hello Agent de dépendances via la Configuration d’état souhaité, vous pouvez utiliser le module xPSDesiredStateConfiguration de hello et un peu de code hello suivante :

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>Désinstaller hello Agent de dépendances

Utilisez hello suivant toohelp sections vous supprimez hello Agent de dépendances.

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>Désinstaller hello Agent de dépendances sur Windows

Un administrateur peut désinstaller l’Agent pour Windows de la dépendance d’hello via le panneau de configuration.

Un administrateur peut également exécuter %Programfiles%\Microsoft dépendance Agent\Uninstall.exe toouninstall hello Agent de dépendances.

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>Désinstaller hello Agent de dépendances sur Linux

désinstallation de toocompletely hello Agent de dépendance à partir de Linux, vous devez supprimer l’agent hello lui-même hello connecteur, qui est installé automatiquement avec l’agent de hello. Vous pouvez désinstaller à l’aide de hello unique commande suivante :

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>Packs d’administration

Lorsque les données réseau et est activée dans un espace de travail Analytique de journal, un Pack d’administration de 300 Ko est envoyé à des serveurs Windows tooall hello dans cet espace de travail. Si vous utilisez des agents de System Center Operations Manager dans un [groupe d’administration connecté](log-analytics-om-agents.md), hello Pack d’administration de l’analyse de dépendance est déployée à partir de System Center Operations Manager. Si les agents hello sont directement connectés, Analytique de journal offre pack d’administration hello.

pack d’administration Hello est nommé Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Il est enregistré dans : %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs. source de données de Hello hello management pack utilise est : % %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="using-hello-solution"></a>À l’aide de la solution de hello

**L’installation et la configuration de solution de hello**

Utilisez hello suivant tooinstall des informations et configurer une solution de hello.

- Hello solution données de collecte récupère les données à partir d’ordinateurs exécutant Windows Server 2012 R2, Windows 8.1 et systèmes d’exploitation ultérieurs.
- Microsoft .NET Framework 4.0 ou version ultérieure est requis sur les ordinateurs où vous souhaitez tooacquire les données de collecte à partir de.
- Ajouter hello Wire Data solution tooyour Analytique de journal espace de travail à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md). Aucune configuration supplémentaire n’est requise.
- Si vous souhaitez que les données réseau et tooview pour une solution spécifique, vous avez besoin de solution de hello toohave déjà ajoutée tooyour espace de travail.

Une fois que les agents sont installés et que vous installez la solution de hello, vignette de hello câble données 2.0 s’affiche dans votre espace de travail.

> [!NOTE]
> Actuellement, vous devez utiliser les données réseau et tooview portail OMS hello. Vous ne pouvez pas utiliser les données de collecte hello tooview portail Azure.

![Vignette de Wire Data](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>À l’aide de la solution de hello câble données 2.0

Dans le portail OMS hello, cliquez sur hello **câble données 2.0** vignette tooopen hello les données réseau et tableau de bord. tableau de bord Hello inclut les panneaux hello Bonjour tableau suivant. Chaque panneau répertorie les articles too10 mise en correspondance que les critères du panneau pour hello spécifié plage étendue et d’heure. Vous pouvez exécuter une recherche de journal qui retourne tous les enregistrements en cliquant sur **afficher tous les** bas hello du Panneau de hello ou en cliquant sur hello panneau en-tête.

| **Panneau** | **Description** |
| --- | --- |
| Agents qui capturent le trafic réseau | Affiche le nombre de hello d’agents de capture du trafic réseau et répertorie les hello top 10 ordinateurs qui sont capture du trafic. Cliquez sur toorun de nombre hello une recherche de journal pour <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>. Cliquez sur un ordinateur dans hello liste toorun une recherche de journal retour hello le nombre total d’octets capturés. |
| Sous-réseaux locaux | Montre nombre hello de sous-réseaux locaux qui ont les agents découverts.  Cliquez sur toorun de nombre hello pour une recherche de journal <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> qui répertorie tous les sous-réseaux avec numéro hello d’octets envoyés sur chacun d’eux. Cliquez sur un sous-réseau dans hello liste toorun une recherche de journal retour hello le nombre total d’octets envoyés sur le sous-réseau de hello. |
| Protocole de niveau application | Indique hello de protocoles de niveau application en cours d’utilisation, découverts par les agents. Cliquez sur toorun de nombre hello une recherche de journal pour <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>. Cliquez sur un protocole toorun une recherche de journal retour hello le nombre total d’octets envoyés à l’aide du protocole de hello. |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Tableau de bord de Wire Data](./media/log-analytics-wire-data/wire-data-dash.png)

Vous pouvez utiliser hello **Agents de capture du trafic réseau** toodetermine panneau quantité de bande passante réseau est consommée par les ordinateurs. Ce panneau, vous pouvez facilement rechercher hello _chattiest_ ordinateur dans votre environnement. Ces ordinateurs peuvent être surchargés, agir de façon anormale ou utiliser plus de ressources réseau que la normale.

![Exemple de recherche de journal](./media/log-analytics-wire-data/log-search-example01.png)

De même, vous pouvez utiliser hello **les sous-réseaux locaux** toodetermine panneau déplace de la quantité de trafic réseau via vos sous-réseaux. Les utilisateurs définissent souvent des sous-réseaux autour des zones critiques de leurs applications. Ce panneau permet de surveiller ces zones.

![Exemple de recherche de journal](./media/log-analytics-wire-data/log-search-example02.png)

Hello **protocoles de niveau Application** lame est utile, car il est utile de savoir quels protocoles sont en cours d’utilisation. Par exemple, vous pouvez vous attendre SSH toonot être en cours d’utilisation dans votre environnement réseau. Affichage des informations disponibles dans le panneau de hello, vous pouvez rapidement confirmer ou dément vos attentes.

![Exemple de recherche de journal](./media/log-analytics-wire-data/log-search-example03.png)

Dans cet exemple, vous pouvez étudier en toosee détails SSH quels ordinateurs sont à l’aide de SSH et beaucoup d’autres détails de communication.

![Résultats de la recherche sh](./media/log-analytics-wire-data/ssh-details.png)

Il est également utile tooknow si le trafic augmente ou diminue au fil du temps. Par exemple, si l’augmentation de la quantité hello des données transmises par une application, qui peuvent être quelque chose que vous devez être conscient de, ou que vous pouvez trouver dignes d’intérêt.

## <a name="input-data"></a>Données d’entrée

Les données réseau et collecte des métadonnées relatives au trafic réseau à l’aide d’agents hello que vous avez activés. Chaque agent envoie des données toutes les 15 secondes environ.

## <a name="output-data"></a>Données de sortie

Un enregistrement de type _WireData_ est créé pour chaque type de données d’entrée. Les enregistrements de données de collecte ont des propriétés illustrées hello tableau suivant :

| Propriété | Description |
|---|---|
| Ordinateur | Nom de l’ordinateur sur lequel les données ont été recueillies |
| TimeGenerated | Heure d’enregistrement de hello |
| LocalIP | Adresse IP de l’ordinateur local de hello |
| SessionState | Connecté ou déconnecté |
| ReceivedBytes | Nombre d’octets reçus |
| ProtocolName | Nom du protocole de réseau hello utilisé |
| IPVersion | Version de l’adresse IP |
| Direction | Entrant ou sortant |
| MaliciousIP | Adresse IP d’une source malveillante connue |
| Severity | Niveau de gravité suspecté |
| RemoteIPCountry | Pays de l’adresse IP distante de hello |
| ManagementGroupName | Nom du groupe d’administration Operations Manager hello |
| SourceSystem | Source où les données ont été recueillies |
| SessionStartTime | Heure de début de la session |
| SessionEndTime | Heure de fin de la session |
| LocalSubnet | Sous-réseau sur lequel les données ont été recueillies |
| LocalPortNumber | Numéro de port local |
| RemoteIP | Adresse IP distante utilisée par l’ordinateur distant de hello |
| RemotePortNumber | Numéro de port utilisé par l’adresse IP distante de hello |
| SessionID | Valeur unique qui identifie la session de communication entre deux adresses IP |
| SentBytes | Nombre d’octets envoyés |
| TotalBytes | Nombre total d’octets envoyés au cours de la session |
| ApplicationProtocol | Type de protocole réseau utilisé   |
| ProcessID | ID du processus Windows |
| ProcessName | Chemin d’accès et le nom du processus de hello |
| RemoteIPLongitude | Valeur de longitude de l’adresse IP |
| RemoteIPLatitude | Valeur de latitude de l’adresse IP |


## <a name="next-steps"></a>Étapes suivantes

- [Rechercher des journaux](log-analytics-log-searches.md) tooview détaillé des enregistrements de recherche de données de câble.
