---
title: aaaConfigure carte de Service dans Operations Management Suite | Documents Microsoft
description: "Carte de service est une solution de Operations Management Suite qui découvre automatiquement les composants de l’application sur Windows et cartes et les systèmes Linux hello la communication entre les services. Cet article fournit des informations sur le déploiement de Service Map dans votre environnement et son utilisation dans divers scénarios."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Configurer Service Map dans Operations Management Suite
Carte de service découvre automatiquement les composants de l’application sur les systèmes Windows et Linux et mappages hello la communication entre les services. Vous pouvez l’utiliser tooview vos serveurs en tant que vous les--considérer comme des réseaux interconnectés qui fournissent des services critiques. Service Map affiche les connexions entre les serveurs, les processus et les ports sur n’importe quelle architecture connectée par TCP, sans configuration requise autre que l’installation d’un agent.

Cet article décrit les détails de hello de configuration des agents de carte de Service et l’intégration. Pour plus d’informations sur l’utilisation de carte de Service, consultez [utiliser des solutions de carte de Service hello dans Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Téléchargements de l’agent de dépendances
| Fichier | SE | Version | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Sources connectées
Carte de service obtient ses données à partir de hello Agent de dépendances Microsoft. Hello Agent de dépendances dépend hello Agent OMS pour son tooOperations connexions Management Suite. Cela signifie qu’un serveur doit avoir hello OMS Agent installé et configuré le premier, puis hello que dépendance Agent peut être installé. Hello tableau suivant décrit les sources de hello connecté qui prend en charge des solutions de carte de Service hello.

| Source connectée | Pris en charge | Description |
|:--|:--|:--|
| Agents Windows | Oui | Carte de service analyse et collecte des données à partir des ordinateurs agents Windows. <br><br>En outre toohello [Agent OMS](../log-analytics/log-analytics-windows-agents.md), agents Windows nécessitent hello Agent de dépendances Microsoft. Consultez hello [prise en charge des systèmes d’exploitation](#supported-operating-systems) pour une liste complète des versions de système d’exploitation. |
| Agents Linux | Oui | Carte de service analyse et collecte des données à partir des ordinateurs agents Linux. <br><br>En outre toohello [Agent OMS](../log-analytics/log-analytics-linux-agents.md), agents Linux nécessitent hello Agent de dépendances Microsoft. Consultez hello [prise en charge des systèmes d’exploitation](#supported-operating-systems) pour une liste complète des versions de système d’exploitation. |
| Groupe d’administration Microsoft System Center Operations Manager | Oui | Service Map analyse et collecte des données provenant des agents Windows et Linux dans un [groupe d’administration System Center Operations Manager](../log-analytics/log-analytics-om-agents.md) connecté. <br><br>Une connexion directe à partir de hello System Center Operations Manager agent ordinateur tooOperations Management Suite est requis. Données sont transférées à partir du référentiel de hello gestion groupe toohello Operations Management Suite.|
| Compte Azure Storage | Non | Carte de service collecte des données à partir d’ordinateurs de l’agent, il n’existe pas de données à partir de celui-ci toocollect depuis le stockage Azure. |

Service Map prend uniquement en charge les plateformes 64 bits.

Sous Windows, hello Microsoft Monitoring Agent (MMA) est utilisé par System Center Operations Manager et Operations Management Suite toogather et envoi de données d’analyse. (Cet agent est appelé hello Agent System Center Operations Manager, OMS Agent, l’Agent Analytique de journal, MMA ou Agent Direct, selon le contexte de hello.) System Center Operations Manager et Operations Management Suite fournissent des versions de zones hors de-hello différente de hello MMA. Ces versions de chaque rapport tooSystem Center Operations Manager, tooOperations Management Suite ou tooboth.  

Sur Linux, hello Agent OMS pour Linux collecte et envoie analyse les données tooOperations Management Suite. Vous pouvez utiliser la carte de Service sur les serveurs dotés d’Agents Direct OMS ou sur des serveurs qui sont attachées tooOperations Management Suite via des groupes d’administration System Center Operations Manager.  

Dans cet article, nous l’appellerons tooall agents--si Linux ou Windows, si connectée tooa groupe d’administration de System Center Operations Manager ou directement tooOperations Management Suite--comme hello « OMS Agent ». Nous allons utiliser le nom de déploiement spécifique de hello de l’agent de hello uniquement si elle est nécessaire pour le contexte.

l’agent de carte de Service Hello ne transmet pas les données elles-mêmes, et il ne nécessite pas de modifications toofirewalls ou des ports. Hello données dans la carte de Service sont toujours transmises par hello Agent OMS tooOperations Management Suite, directement ou via hello OMS passerelle.

![Agents Service Map](media/oms-service-map/agents.png)

Si vous êtes un client de System Center Operations Manager avec un tooOperations de groupe connecté gestion Management Suite :

- Si vos agents de System Center Operations Manager peuvent accéder à hello Internet tooconnect tooOperations Management Suite, aucune configuration supplémentaire n’est requise.  
- Si vos agents de System Center Operations Manager ne peut pas accéder à Operations Management Suite sur hello Internet, vous devez tooconfigure hello OMS passerelle toowork avec System Center Operations Manager.
  
Si vous utilisez hello OMS l’Agent Direct, vous devez tooconfigure hello Agent OMS lui-même tooconnect tooOperations Management Suite ou tooyour OMS passerelle. Hello OMS passerelle peut être téléchargé à partir de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Packs d’administration
Lors de la carte de Service est activé dans un espace de travail Operations Management Suite, un Pack d’administration de 300 Ko est envoyé à des serveurs Windows tooall hello dans cet espace de travail. Si vous utilisez des agents de System Center Operations Manager dans un [groupe d’administration connecté](../log-analytics/log-analytics-om-agents.md), hello Pack d’administration de carte de Service est déployé à partir de System Center Operations Manager. Si les agents hello sont directement connectés, Operations Management Suite offre pack d’administration hello.

pack d’administration Hello est nommé Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Il écrit too%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\. source de données qui utilise du pack d’administration hello Hello est % %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID > \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Installation
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Installer hello Agent de dépendances sur Microsoft Windows
Des privilèges d’administrateur sont requis tooinstall ou désinstaller l’agent de hello.

Hello dépendance Agent est installé sur les ordinateurs Windows via InstallDependencyAgent-Windows.exe. Si vous exécutez ce fichier exécutable sans option, il démarre un Assistant que vous pouvez suivre tooinstall de manière interactive.  

Hello suivant les étapes tooinstall hello dépendance Agent sur chaque ordinateur Windows, utilisez :

1.  Installation hello Agent OMS à l’aide d’instructions hello à [toohello d’ordinateurs Windows de se connecter service Analytique de journal dans Azure](../log-analytics/log-analytics-windows-agents.md).
2.  Télécharger l’agent de Windows hello et l’exécuter à l’aide de hello de commande suivante : <br>`InstallDependencyAgent-Windows.exe`
3.  Suivez l’agent de hello Assistant tooinstall hello.
4.  En cas de hello dépendance Agent toostart, vérifiez les journaux de hello pour les informations d’erreur détaillées. Sur les agents Windows, le répertoire de journal de hello est %Programfiles%\Microsoft Agent\logs de dépendance. 

#### <a name="windows-command-line"></a>Ligne de commande Windows
Utilisez les options de hello suivant tooinstall de la table à partir d’une ligne de commande. toosee une liste des indicateurs d’installation Bonjour, exécutez le programme d’installation de hello à l’aide de hello / ? comme suit.

    InstallDependencyAgent-Windows.exe /?

| Indicateur | Description |
|:--|:--|
| /? | Obtenir la liste des options de ligne de commande hello. |
| /S | Effectuez une installation silencieuse sans invite utilisateur. |

Fichiers de hello Agent de dépendances de Windows sont placés dans C:\Program Files\Microsoft dépendance Agent par défaut.

### <a name="install-hello-dependency-agent-on-linux"></a>Installer hello Agent de dépendances sur Linux
Accès à la racine est requise tooinstall ou configurer l’agent de hello.

Hello dépendance Agent est installé sur les ordinateurs Linux via InstallDependencyAgent-Linux64.bin, un script de shell dans un fichier binaire à extraction automatique. Vous pouvez exécuter hello à l’aide sh ou ajouter d’exécuter le fichier de toohello autorisations lui-même.
 
Hello suivant les étapes tooinstall hello dépendance Agent sur chaque ordinateur Linux, utilisez :

1.  Installation hello Agent OMS à l’aide d’instructions hello à [collecter et gérer les données des ordinateurs Linux](https://technet.microsoft.com/library/mt622052.aspx).
2.  Installer l’agent de dépendance de Linux hello en tant que racine à l’aide de hello de commande suivante :<br>`sh InstallDependencyAgent-Linux64.bin`
3.  En cas de hello dépendance Agent toostart, vérifiez les journaux de hello pour les informations d’erreur détaillées. Sur les agents de Linux, le répertoire de journal de hello est /var/opt/microsoft/dependency-agent/log.

toosee une liste d’indicateurs d’installation hello, exécutez le programme d’installation de hello hello - aide indicateur comme suit.

    InstallDependencyAgent-Linux64.bin -help

| Indicateur | Description |
|:--|:--|
| -help | Obtenir la liste des options de ligne de commande hello. |
| -s | Effectuez une installation silencieuse sans invite utilisateur. |
| --check | Vérifiez les autorisations et le système d’exploitation de hello, mais ne pas installer l’agent de hello. |

Fichiers pourquoi l’Agent de dépendance sont placés dans hello suivant répertoires :

| Fichiers | Lieu |
|:--|:--|
| Fichiers principaux | /opt/microsoft/dependency-agent |
| Fichiers journaux | /var/opt/microsoft/dependency-agent/log |
| Fichiers de configuration | /etc/opt/microsoft/dependency-agent/config |
| Fichiers exécutables de service | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Fichiers de stockage binaires | /var/opt/microsoft/dependency-agent/storage |

## <a name="installation-script-examples"></a>Exemples de script d’installation
tooeasily déployer hello Agent de dépendances sur plusieurs serveurs à la fois, il vous aide à toouse un script. Vous pouvez utiliser hello suivant toodownload des exemples de script et installer hello Agent de dépendances sur Windows ou Linux.

### <a name="powershell-script-for-windows"></a>Script PowerShell pour Windows
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Script shell pour Linux
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>Configuration de l’état souhaité (DSC)
toodeploy hello Agent de dépendances via la Configuration d’état souhaité, vous pouvez utiliser le module xPSDesiredStateConfiguration de hello et un peu de code hello suivante :
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>Désinstallation
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Désinstaller hello Agent de dépendances sur Windows
Un administrateur peut désinstaller l’Agent pour Windows de la dépendance d’hello via le panneau de configuration.

Un administrateur peut également exécuter %Programfiles%\Microsoft dépendance Agent\Uninstall.exe toouninstall hello Agent de dépendances.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Désinstaller hello Agent de dépendances sur Linux
désinstallation de toocompletely hello Agent de dépendance à partir de Linux, vous devez supprimer l’agent hello lui-même hello connecteur, qui est installé automatiquement avec l’agent de hello. Vous pouvez désinstaller à l’aide de hello unique commande suivante :

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous rencontrez des problèmes d’installation ou d’exécution de Service Map, cette section vous aidera peut-être. Si vous n’arrivez toujours pas à les résoudre, contactez le Support Microsoft.

### <a name="dependency-agent-installation-problems"></a>Problèmes d’installation de l’agent de dépendances
#### <a name="installer-asks-for-a-reboot"></a>Le programme d’installation vous demande de redémarrer
Agent de dépendances de Hello *généralement* ne nécessite pas un redémarrage à l’installation ou la désinstallation. Toutefois, dans certains cas rares, Windows Server nécessite une toocontinue de redémarrage d’une installation. Cela se produit lorsqu’une dépendance, généralement les hello redistribuable Microsoft Visual C++, requiert un redémarrage en raison d’un fichier verrouillé.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>Message « Impossible de tooinstall Agent de dépendances : les bibliothèques Runtime Visual Studio a échoué tooinstall (code = [code_number]) » s’affiche

Hello Agent de dépendances Microsoft repose sur les bibliothèques runtime de Microsoft Visual Studio hello. Vous recevez un message signalant si un problème est survenu lors de l’installation des bibliothèques de hello. 

programmes d’installation de bibliothèque de runtime Hello créer des journaux dans le dossier de %LOCALAPPDATA%\temp hello. fichier de Hello est dd_vcredist_arch_yyyymmddhhmmss.log, où *arch* est « x86 » ou « amd64 » et *aaaammjjhhmmss* est hello horodatage (24 heures) lorsque le journal de hello a été créé. journal de Hello fournit des détails sur le problème hello qui bloque l’installation.

Il peut être utile tooinstall hello [dernières bibliothèques runtime](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) vous-même premier.

Hello tableau suivant répertorie les numéros de code et les solutions suggérées.

| Code | Description | Résolution : |
|:--|:--|:--|
| 0x17 | programme d’installation de la bibliothèque Hello requiert une mise à jour de Windows n’a pas été installé. | Recherchez dans le journal du programme d’installation hello plus récent bibliothèque.<br><br>Si une référence trop « Windows8. 1-KB2999226-x 64.msu » est suivi d’une ligne « erreur 0x80240017 : package MSU de tooexecute ayant échoué, « vous n’avez pas hello conditions préalables tooinstall KB2999226. Suivez les instructions de hello dans la section conditions préalables de hello dans [Universal Runtime C dans Windows](https://support.microsoft.com/kb/2999226). Vous pouvez peut-être toorun mise à jour Windows et redémarrer plusieurs fois dans les conditions préalables de commande tooinstall hello.<br><br>Réexécutez le programme d’installation de hello Agent de dépendances Microsoft. |

### <a name="post-installation-issues"></a>Problèmes après installation
#### <a name="server-doesnt-appear-in-service-map"></a>Le serveur n’apparaît pas dans Service Map
Si votre installation de l’Agent de dépendances a réussi, mais vous ne voyez pas votre serveur Bonjour solutions de carte de Service :
* Hello dépendance Agent est installé avec succès ? Vous pouvez le valider par la vérification toosee si hello service est installé et en cours d’exécution.<br><br>
**Windows**: recherchez service hello nommé « Microsoft Dependency Agent ».<br>
**Linux**: recherchez hello exécute le processus de « microsoft-dépendance-agent ».

* Vous êtes sur hello [libre tarification d’Operations Management Suite/journal Analytique](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? un plan gratuit hello permet de configurer des serveurs de carte de Service uniques toofive. Les serveurs suivants ne s’afficheront dans la carte de Service, même si hello cinq préalable n’est plus envoient des données.

* Est votre journal envoi du serveur et les données de performances tooOperations Management Suite ? Accédez tooLog recherche et exécutez hello suivant la requête pour votre ordinateur : 

        * Computer="<your computer name here>" | measure count() by Type
        
  Vous avez reçu une variété d’événements dans les résultats de hello ? Donnée hello récente ? Dans ce cas, l’Agent OMS est fonctionne correctement et communique avec hello service Operations Management Suite. Sinon, vérifiez hello Agent OMS sur votre serveur : [dépannage d’OMS Agent pour Windows](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) ou [Agent OMS pour Linux dépannage](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>Le serveur s’affiche dans Service Map, mais n’a aucun processus
Si votre serveur dans la carte de Service, mais il ne comporte aucune donnée de processus ou de connexion, qui indique que hello dépendance Agent est installé et en cours d’exécution, mais n’a pas de charger le pilote du noyau hello. 

Vérifiez le fichier de C:\Program Files\Microsoft dépendance Agent\logs\wrapper.log hello (Windows) ou /var/opt/microsoft/dependency-agent/log/service.log (Linux). Hello dernières lignes du fichier de hello doivent indiquer pourquoi le noyau de hello n’a pas chargé. Par exemple, hello noyau ne peut pas être pris en charge sous Linux si vous votre noyau mis à jour.

## <a name="data-collection"></a>Collecte des données
Vous pouvez vous attendre tootransmit de chaque agent à peu près 25 Mo par jour, selon la complexité sont de dépendances de votre système. Chaque agent envoie des données de dépendance Service Map toutes les 15 secondes.  

Agent de dépendances de Hello consomme généralement 0,1 pour cent de la mémoire système et de 0,1 pour cent de l’UC système.

## <a name="supported-azure-regions"></a>Régions Azure prises en charge
Carte de service est actuellement disponible dans hello suivant des régions Azure :
- Est des États-Unis
- Europe de l'Ouest
- Centre-Ouest des États-Unis


## <a name="supported-operating-systems"></a>Systèmes d’exploitation pris en charge
Hello sections suivantes répertorient hello pris en charge les systèmes d’exploitation pour hello Agent de dépendances. Service Map ne prend pas en charge les architectures 32 bits, quel que soit le système d’exploitation.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

### <a name="windows-desktop"></a>Ordinateurs Windows
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux et Oracle Linux (avec noyau RHEL)
- Seules les versions du noyau SMP Linux et par défaut sont prises en charge.
- Les versions non standard du noyau, par exemple PAE et Xen, ne sont prises en charge par aucune distribution Linux. Par exemple, un système avec la chaîne de version hello de « 2.6.16.21-0.8-xen » n’est pas prise en charge.
- Les noyaux personnalisés, y compris les recompilations de noyaux standard, ne sont pas pris en charge.
- Le noyau CentOSPlus n’est pas pris en charge.
- Oracle Unbreakable Enterprise Kernel (UEK) est traité dans une autre section, plus loin dans cet article.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| Version du SE | Version du noyau |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| Version du SE | Version du noyau |
|:--|:--|
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
| Version du SE | Version du noyau |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux avec Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| Version du SE | Version du noyau
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4. | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| Version du SE | Version du noyau
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| Version du SE | Version du noyau
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| Version du SE | Version du noyau
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>Données relatives aux diagnostics et à l’utilisation
Microsoft recueille automatiquement des données d’utilisation et de performances via votre utilisation du service de carte de Service de hello. Microsoft utilise cette tooprovide de données et améliorer la qualité de hello, la sécurité et l’intégrité de hello service de carte de Service. Données incluent des informations sur la configuration de votre logiciel, telles que le système d’exploitation et version hello. Il inclut également le nom de la station de travail, nom DNS et adresse IP dans l’ordre tooprovide précise et efficace des capacités de dépannage. Nous ne collectons pas votre nom, votre adresse, ni vos autres coordonnées.

Pour plus d’informations sur la collecte de données et l’utilisation, consultez hello [déclaration de confidentialité Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Étapes suivantes
- Découvrez comment trop[utiliser la carte de Service](operations-management-suite-service-map.md) après qu’il a été déployé et configuré.
