---
title: aaaTroubleshooting Diagnostics Azure | Documents Microsoft
description: "Résolution des problèmes lors de l'utilisation des diagnostics Azure dans Azure Virtual Machines, Service Fabric ou Cloud Services."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Résolution des problèmes des diagnostics Azure
Dépannage des informations pertinentes toousing Diagnostics Windows Azure. Pour plus d’informations sur les diagnostics Azure, voir [Présentation des diagnostics Azure](azure-diagnostics.md).

## <a name="logical-components"></a>Composants logiques
**Lanceur de plug-in Diagnostics (DiagnosticsPluginLauncher.exe)**: lance l’extension des Diagnostics Windows Azure hello. Processus du point sert d’entrée de hello.

**Plug-in Diagnostics (DiagnosticsPlugin.exe)**: processus principal qui est lancée par le service de lancement hello ci-dessus et configure l’Agent de surveillance de hello, il lance et gère sa durée de vie. 

**L’Agent de surveillance (MonAgent\*.exe processus)**: ces processus hello plus gros du travail de hello ; autrement dit, analyse, collecte et le transfert de hello les données de diagnostic.  

## <a name="logartifact-paths"></a>Chemins d’accès des journaux/artefacts
Vous trouverez ici les artefacts et les journaux de hello chemins toosome important. Nous utiliserons référence toothese dans reste hello du document de hello :
### <a name="cloud-services"></a>Services cloud
| Artefact | Chemin |
| --- | --- |
| **Fichier de configuration d’Azure Diagnostics** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\Config.txt |
| **Fichiers journaux** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\ |
| **Magasin local pour les données de diagnostic** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Tables |
| **Fichier de configuration de l’agent de surveillance** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Package d’extension Azure Diagnostics** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version> |
| **Chemin d’accès à l’utilitaire de collecte des journaux** | %SystemDrive%\Packages\GuestAgent\ |
| **Fichier journal MonAgentHost** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

### <a name="virtual-machines"></a>Machines virtuelles
| Artefact | Chemin |
| --- | --- |
| **Fichier de configuration d’Azure Diagnostics** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\RuntimeSettings |
| **Fichiers journaux** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Logs\ |
| **Magasin local pour les données de diagnostic** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Tables |
| **Fichier de configuration de l’agent de surveillance** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MaConfig.xml |
| **Fichier d’état** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Status |
| **Package d’extension Azure Diagnostics** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>|
| **Chemin d’accès à l’utilitaire de collecte des journaux** | C:\WindowsAzure\Packages |
| **Fichier journal MonAgentHost** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>Les données métriques ne s’affichent pas dans le portail Azure
Azure Diagnostics fournit un ensemble de données métriques, qui peuvent être affichées dans le portail Azure. Si vous avez des problèmes liés à afficher ces données dans le portail, compte de stockage de diagnostics à cocher hello -> WADMetrics\* toosee de table si existe-t-il des enregistrements de métrique correspondants hello. Ici, hello PartitionKey de la table de hello est hello les ID de ressource d’ordinateur virtuel ou des machines virtuelles identiques et hello RowKey est le nom de la métrique hello autrement dit, les noms de compteur de performances.

Si l’ID de ressource hello est incorrecte, vérifiez la Configuration de Diagnostics -> mesures -> ResourceId toosee si l’ID de ressource hello est défini correctement.

Si aucune donnée pour une métrique spécifique de hello, vérifiez la Configuration de Diagnostics -> PerformanceCounter toosee si le métrique hello (compteur de performances) est inclus. Nous allons activer hello suivant compteurs par défaut.
- \Processus(_Total)\% Temps processeur
- \Memory\Octets disponibles
- \ASP.NET Applications(__Total__)\Requests/Sec
- \ASP.NET Applications(__Total__)\Errors Total/Sec
- \ASP.NET\Demandes en file d’attente
- \ASP.NET\Demandes rejetées
- \Processor(w3wp)\% Temps processeur
- \Processus(w3wp) \Octets privés
- \Processus(WaIISHost)\% Temps processeur
- \Processus(WaIISHost)\Octets privés
- \Processus(WaWorkerHost)\% Temps processeur
- \Processus(WaWorkerHost)\Octets privés
- \Mémoire\Défauts de page/s
- \.Mémoire NET CLR(_Global_)\% Temps en GC
- \LogicalDisk(C:)\Disk Write Bytes/sec
- \LogicalDisk(C:)\Disk Read Bytes/sec
- \LogicalDisk(D:)\Disk Write Bytes/sec
- \LogicalDisk(D:)\Disk Read Bytes/sec

Si hello est configuré correctement, mais vous ne voyez pas les données de mesure hello, suivez les instructions de hello ci-dessous pour une analyse approfondie de hello.


## <a name="azure-diagnostics-is-not-starting"></a>Azure Diagnostics ne démarre pas
Examinez **DiagnosticsPluginLauncher.log** et **DiagnosticsPlugin.log** fichiers à partir de l’emplacement de hello Hello fournies ci-dessus pour plus d’informations sur la raison pour laquelle diagnostics a échoué toostart des fichiers journaux. 

Si ces journaux indiquent `Monitoring Agent not reporting success after launch`, cela signifie que le lancement de MonAgentHost.exe a échoué. Consultez les journaux hello pour cet emplacement hello indiqué pour `MonAgentHost log file` dans la section hello ci-dessus.

Hello dernière ligne de fichiers de journaux hello contient le code de sortie hello.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Si vous trouvez un **négatif** code de sortie, consultez le toohello [table des codes de sortie](#azure-diagnostics-plugin-exit-codes) Bonjour [références](#references).

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>Données de diagnostic sont enregistrés pas tooAzure stockage
Déterminez si aucune donnée ne s’affichent ou que seules certaines des données de hello ne s’affichent pas.

### <a name="diagnostics-infrastructure-logs"></a>Journaux d’infrastructure de diagnostics
Les journaux d’infrastructure de diagnostics correspondent à l’emplacement de journalisation des erreurs par Azure Diagnostics. Assurez-vous que vous avez activé ([comment ?](#how-to-check-diagnostics-extension-configuration)) capturer des journaux d’Infrastructure de diagnostic dans votre configuration et de rechercher rapidement les erreurs appropriées qui s’affichent dans hello `DiagnosticInfrastructureLogsTable` table dans votre compte de stockage.

### <a name="no-data-is-showing-up"></a>Aucune donnée n’est affichée
cause la plus courante des données d’événement manquant entièrement Hello est les informations de compte de stockage défini de manière incorrecte.

Solution : corrigez la configuration du plug-in Diagnostics et réinstallez-le.

Si le compte de stockage hello est correctement configuré, à distance Bureau dans la création et de la machine de hello DiagnosticsPlugin.exe et MonAgentCore.exe sont en cours d’exécution. Si vous n’êtes pas en cours d’exécution, suivez [Azure Diagnostics ne démarre pas](#azure-diagnostics-is-not-starting). Si les processus hello sont en cours d’exécution, passez trop[est mise en route capturées localement des données](#is-data-getting-captured-locally) et suivez ce guide à partir de là,.

### <a name="part-of-hello-data-is-missing"></a>Les données de salutation est incomplet
Si vous obtenez des données, mais pas d’autres, Cela signifie que la collecte de données hello / le pipeline de transfert est correctement définie. Suivez les sous-sections hello ici toonarrow quel problème hello est :
#### <a name="is-collection-configured"></a>Configuration de la collecte : 
Configuration des diagnostics affiche hello qui fait en sorte que pour un type particulier de toobe des données collectée. [Passez en revue votre configuration](#how-to-check-diagnostics-extension-configuration) toomake vraiment pas souhaité pour les données vous n’avez pas configuré pour la collection.
#### <a name="is-hello-host-generating-data"></a>Hôte de hello génère des données :
- **Les compteurs de performance**: Ouvrez l’Analyseur de performances et vérifiez le compteur de hello.
- **Journaux de suivi**: Bureau à distance dans hello VM et ajouter le fichier de configuration d’une application toohello TextWriterTraceListener.  Consultez tooset http://msdn.microsoft.com/library/sk36c28t.aspx d’écouteur de texte hello.  Vérifiez que hello `<trace>` élément a `<trace autoflush="true">`.<br />
Si vous ne voyez pas de journaux de suivi générés, suivez les étapes décrites dans la section [En savoir plus sur les journaux de suivi manquants](#more-about-trace-logs-missing).
- **Les suivis ETW**: Bureau à distance dans hello machine virtuelle et installez PerfView.  Dans PerfView, exécutez Fichier -> Commande utilisateur -> Écouter etwprovider1, etwprovider2, etc.  Notez que hello écoute commande respecte la casse et il ne peut pas être des espaces de hello séparées par des virgules de la liste des fournisseurs ETW.  En cas de commande hello toorun, vous pouvez cliquer sur le bouton de « Log » hello en hello en bas à droite de hello Perfview outil toosee que ce qui a été tentée toorun et quel résultat hello a été.  En supposant que l’entrée de hello est correcte, que puis une nouvelle fenêtre s’affiche et dans quelques secondes vous commencerez voir les traces ETW.
- **Journaux des événements**: Bureau à distance dans hello machine virtuelle. Ouvrez `Event Viewer` et vous assurer que les événements hello existent.
#### <a name="is-data-getting-captured-locally"></a>Capture locale des données :
Vérifiez ensuite la mise en route capture des données de hello localement.
les données de salutation sont stockées localement dans `*.tsf` dans les fichiers [magasin local de hello pour les données de diagnostic](#log-artifacts-path). Différents types de journaux sont collectés dans différents fichiers `.tsf`. les noms de Hello sont des noms de table toohello similaires dans le stockage azure. Par exemple, `Performance Counters` est collecté dans le fichier `PerformanceCountersTable.tsf`, et les journaux des événements sont collectés dans le fichier `WindowsEventLogsTable.tsf`. Utilisez les instructions hello dans [Extraction de journal Local](#local-log-extraction) section des fichiers de collecte locale tooopen hello et assurez-vous que vous les voyez obtention collectées sur le disque.

Si vous ne consultez Mise en route collectées localement dans les journaux et avez déjà vérifié que les hôtes hello sont la génération des données, vous avez probablement un problème de configuration. Passez en revue votre configuration soigneusement pour la section appropriée de hello. Consulter également la configuration hello générée pour MonitoringAgent [MaConfig.xml](#log-artifacts-path) et assurez-vous qu’il existe une section décrivant la source de journal pertinentes hello et qu’il n’est pas perdue au cours de la traduction entre la configuration des diagnostics azure et configuration de l’agent.
#### <a name="is-data-getting-transferred"></a>Transfert des données :
Si vous avez vérifié la mise en route capture des données de hello localement, mais vous toujours pas visible dans votre compte de stockage : 
- Tout d’abord, assurez-vous que vous avez fourni un compte de stockage correct et que vous n’avez pas reportée sur de clés etc.for hello est fonction du compte de stockage. Pour les services cloud, il arrive parfois que les utilisateurs ne mettent pas à jour le paramètre `useDevelopmentStorage=true`.
- Si le compte de stockage fourni est correct. Assurez-vous que vous n’avez pas de certaines restrictions réseau qui n’autorisent pas les composants hello tooreach points de terminaison de stockage public. Une façon toodo tooremote des ordinateurs de bureau dans hello de l’ordinateur et essayez de toowrite toohello quelque chose du compte de stockage même vous-même.
- Pour finir, vous pouvez essayer de voir les échecs signalés par l’agent de surveillance. Agent d’analyse écrit ses journaux `maeventtable.tsf` situé dans [magasin local de hello pour les données de diagnostic](#log-artifacts-path). Suivez les instructions de [Extraction de journal Local](#local-log-extraction) section tooopen ce fichier et essayez de déterminer s’il y a `errors` indiquant les fichiers locaux échecs tooread ou toostorage d’écriture.

### <a name="capturing--archiving-logs"></a>Capture/Archivage des journaux
Vous avons abordé hello étapes ci-dessus, mais pas pouvez déterminer ce qui était incorrect et que vous pensiez à contacter le support technique. Hello première chose qu’ils peuvent vous demander est toocollect les journaux à partir de votre ordinateur. Vous pouvez gagner du temps en effectuant vous-même cette procédure. Exécutez hello `CollectGuestLogs.exe` utilitaire à [chemin d’accès de l’utilitaire de collecte de journaux](#log-artifacts-path) et qu’il génère un fichier zip avec tous les journaux azure pertinentes Bonjour même dossier.

## <a name="diagnostics-data-tables-not-found"></a>Tables des données de diagnostic introuvables
tables Hello dans le stockage Azure contenant les événements ETW sont nommées à l’aide de hello suivant de code :

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

Voici un exemple :

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
Avec génération de 4 tables :

| Événement | Nom de la table |
| --- | --- |
| provider=”prov1” &lt;Event id=”1” /&gt; |WADEvent+MD5(“prov1”)+”1” |
| provider=”prov1” &lt;Event id=”2” eventDestination=”dest1” /&gt; |WADdest1 |
| provider=”prov1” &lt;DefaultEvents /&gt; |WADDefault+MD5(“prov1”) |
| provider=”prov2” &lt;DefaultEvents eventDestination=”dest2” /&gt; |WADdest2 |

## <a name="references"></a>Références

### <a name="how-toocheck-diagnostics-extension-configuration"></a>Comment toocheck Configuration de l’Extension Diagnostics
Hello toocheck de façon plus simple votre configuration de l’extension est toonavigate toohttp://resources.azure.com, accédez toohello virtual machine ou un service cloud sur le hello extension Azure Diagnostics (IaaSDiagnostics / PaaDiagnostics) en question.

Vous pouvez également Bureau à distance sur l’ordinateur de hello et examinez le fichier de Configuration des Diagnostics Azure hello décrites dans la section appropriée de hello [ici](#log-artifacts-path).

Dans le cas chercher **Microsoft.Azure.Diagnostics** ensuite pour hello **xmlCfg** ou **WadCfg** champ. 

En cas de machines virtuelles, si le champ de WadCfg hello est présent, cela signifie hello config est au format JSON. Si le champ de xmlCfg hello est présent, cela signifie la configuration hello est XML et est l’encodé en base64. Vous devez trop[décoder](http://www.bing.com/search?q=base64+decoder) toosee hello XML qui a été chargé par les Diagnostics.

Pour le rôle de Service Cloud, si vous choisissez configuration hello à partir du disque, les données de salutation sont encodage base64 et vous devrez donc trop[décoder](http://www.bing.com/search?q=base64+decoder) toosee hello XML qui a été chargé par les Diagnostics.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Codes de sortie du plug-in Azure Diagnostics
plug-in Hello renvoie hello suivant des codes de sortie :

| Code de sortie | Description |
| --- | --- |
| 0 |Vous avez réussi ! |
| -1 |Erreur générique. |
| -2 |Fichier de rcf hello tooload impossible.<p>Cette erreur interne doit se produire uniquement si le Lanceur de plug-in agent hello invité est appelée manuellement, de manière incorrecte, sur hello machine virtuelle. |
| -3 |Impossible de charger le fichier de configuration des Diagnostics hello.<p><p>Solution : cette erreur se produit lorsqu'un fichier de configuration ne passe pas la validation de schéma. solution de Hello est tooprovide un fichier de configuration qui est conforme à un schéma de hello. |
| -4 |Répertoire des ressources locales hello est déjà utilisé par une autre instance de hello Diagnostics de l’agent de surveillance.<p><p>Solution : spécifiez une valeur différente pour **LocalResourceDirectory**. |
| -6 |Lanceur de plug-in agent Hello invité a tenté de Diagnostics toolaunch avec une ligne de commande non valide.<p><p>Cette erreur interne doit se produire uniquement si le Lanceur de plug-in agent hello invité est appelée manuellement, de manière incorrecte, sur hello machine virtuelle. |
| -10 |plug-in des Diagnostics Hello s’est terminé avec une exception non gérée. |
| -11 |l’agent invité de Hello a été processus hello toocreate Impossible pour l’analyse de hello l’agent de surveillance et de lancement.<p><p>Solution : Vérifiez que suffisamment de ressources système est disponibles toolaunch nouveaux processus.<p> |
| -101 |Arguments non valides lors de l’appel de plug-in des Diagnostics hello.<p><p>Cette erreur interne doit se produire uniquement si le Lanceur de plug-in agent hello invité est appelée manuellement, de manière incorrecte, sur hello machine virtuelle. |
| -102 |processus de plug-in de Hello est impossible tooinitialize lui-même.<p><p>Solution : Vérifiez que suffisamment de ressources système est disponibles toolaunch nouveaux processus. |
| -103 |processus de plug-in de Hello est impossible tooinitialize lui-même. Plus précisément, il est objet enregistreur de hello toocreate impossible.<p><p>Solution : Vérifiez que suffisamment de ressources système est disponibles toolaunch nouveaux processus. |
| -104 |Fichier de rcf hello Impossible tooload fourni par l’agent invité de hello.<p><p>Cette erreur interne doit se produire uniquement si le Lanceur de plug-in agent hello invité est appelée manuellement, de manière incorrecte, sur hello machine virtuelle. |
| -105 |plug-in des Diagnostics Hello ne peut pas ouvrir le fichier de configuration des Diagnostics hello.<p><p>Cette erreur interne doit se produire uniquement si le plug-in des Diagnostics hello est appelée manuellement, de manière incorrecte, sur hello machine virtuelle. |
| -106 |Impossible de lire le fichier de configuration des Diagnostics hello.<p><p>Solution : cette erreur se produit lorsqu'un fichier de configuration ne passe pas la validation de schéma. Solution de hello est donc tooprovide un fichier de configuration qui est conforme à un schéma de hello. Consultez [comment toocheck Configuration de l’Extension Diagnostics](#how-to-check-diagnostics-extension-configuration). |
| -107 |Hello ressource active passe toohello l’agent de surveillance n’est pas valide.<p><p>Cette erreur interne doit se produire uniquement si hello l’agent de surveillance est appelée manuellement, de manière incorrecte, sur hello machine virtuelle.</p> |
| -108 |Fichier de configuration Diagnostics tooconvert Impossible hello en hello analyse le fichier de configuration de l’agent.<p><p>Cette erreur interne doit se produire uniquement si le plug-in des Diagnostics hello est appelée manuellement avec un fichier de configuration non valide. |
| -110 |Erreur de configuration générale de Diagnostics.<p><p>Cette erreur interne doit se produire uniquement si le plug-in des Diagnostics hello est appelée manuellement avec un fichier de configuration non valide. |
| -111 |Agent de surveillance hello toostart impossible.<p><p>Solution : vérifiez que les ressources système disponibles sont suffisantes pour lancer de nouveaux processus. |
| -112 |Erreur générale |

### <a name="local-log-extraction"></a>Extraction locale des journaux
Hello, l’agent de surveillance collecte les journaux et des artefacts en tant que `.tsf` fichiers. Le fichier `.tsf` n’est pas lisible, mais vous pouvez le convertir en fichier `.csv`, comme suit : 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Un nouveau fichier appelé `<relevantLogFile>.csv` sera créé dans hello même chemin d’accès comme hello correspondant `.tsf` fichier.

**Remarque**: vous ne devez toorun cet utilitaire sur fichier de tsf principal hello (par exemple, PerformanceCountersTable.tsf). Hello accompagnant les fichiers (par exemple, PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002. tsf etc.) sont traitées automatiquement.

### <a name="more-about-trace-logs-missing"></a>En savoir plus sur les journaux de suivi manquants

**Remarque :** principalement s’applique toocloud services uniquement, sauf si vous avez configuré hello DiagnosticsMonitorTraceListener sur une application en cours d’exécution sur votre VM IaaS. 

- Vérifiez que hello que diagnosticmonitortracelistener est configuré dans hello web.config ou app.config.  Ceci est configuré par défaut dans les projets de service cloud, mais certains clients comment hors, ce qui provoque l’hello trace instructions toonot être collectés par les diagnostics. 
- Si les journaux ne sont pas mise en route écrites à partir de la méthode OnStart ou de l’exécution de hello rendre hello que DiagnosticMonitorTraceListener est hello app.config.  Par défaut, il est dans le fichier web.config de hello, mais qui s’applique uniquement toocode qui s’exécutent dans w3wp.exe ; Par conséquent, vous en avez besoin dans les traces de toocapture app.config en cours d’exécution dans WaIISHost.exe.
- Veillez à utiliser Diagnostics.Trace.TraceXXX à la place de Diagnostics.Debug.WriteXXX.  Hello instructions de débogage seront supprimées à partir d’une version Release.
- Assurez-vous que le code de hello compilé présente réellement des lignes de Diagnostics.Trace hello (utilisez tooverify Reflector, ildasm ou ILSpy).  Les commandes Diagnostics.Trace sont supprimés de binaire de hello compilé sauf si vous utilisez le symbole de compilation conditionnelle TRACE hello.  Si à l’aide du projet de msbuild toobuild hello Ceci constitue un toorun problème commun dans.

## <a name="known-issues-and-mitigations"></a>Problèmes connus et atténuations des risques
Voici la liste des problèmes connus avec les atténuations des risques :

**1. Dépendance de .NET 4.5 :**

WAD connaît une dépendance d’exécution dans .NET Framework 4.5 ou supérieur. Au moment de hello de rédaction de cet article, tous les ordinateurs configurés pour les services de cloud computing, ainsi que tous les officiel azure base images de Machine virtuelle ont .NET 4.5 ou ultérieure. Il est possible de toujours toutefois tooland dans une situation où vous essayez de toorun WAD sur un ordinateur qui n’a pas de .NET 4.5 ou version ultérieure. Cela se produit si vous créez votre machine à partir d’une ancienne image ou capture instantanée, ou encore si vous utilisez votre propre disque personnalisé.

Cela se manifeste généralement par le code de sortie **255** lorsque vous exécutez DiagnosticsPluginLauncher.exe. Échec se produit en raison de l’exception de toohello non gérée : 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Atténuation :** installez .NET 4.5 ou version supérieure sur votre machine.

**2. Données des compteurs de performances disponibles dans le stockage, mais non affichées dans le portail**

Par défaut, le portail des machines virtuelles affiche certains compteurs de performances. Si vous ne les voyez et que vous connaissez les données de salutation sont générées, car il est disponible dans le stockage. Vérifiez les points suivants :
- Si les données hello dans le stockage ont les noms de compteur en anglais. Si les noms de compteur hello ne sont pas en anglais, portail graphique de métrique ne sera pas en mesure de toorecognize il.
- Si vous utilisez des caractères génériques (\*) dans vos noms de compteur de performances, portail de hello ne sera pas en mesure de toocorrelate hello configurée et collecte le compteur.

**Atténuation**: modifier tooEnglish de langue de l’ordinateur hello pour les comptes système. Le panneau de configuration -> région administration -> Paramètres -> Décochez la case « Bienvenue dans l’écran et système comptes » afin que la langue de personnalisée hello n’est pas appliqué toosystem compte. Assurez-vous également que vous n’utilisez pas les caractères génériques si vous souhaitez toobe portail de votre expérience de consommation principale.
