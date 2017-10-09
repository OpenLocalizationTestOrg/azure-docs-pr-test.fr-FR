---
title: aaaMonitoring un VM Linux avec une extension de machine virtuelle | Documents Microsoft
description: "Découvrez comment toouse hello Extension Diagnostics Linux toomonitor hello données de performances et diagnostic d’un VM Linux dans Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Utilisez hello Extension Diagnostics Linux toomonitor hello données de performances et diagnostic d’un VM Linux

Ce document décrit la version 2.3 de hello Extension Diagnostics Linux.

> [!IMPORTANT]
> Cette version est dépréciée et sa publication peut cesser au-delà du 30 juin 2018. Elle a été remplacée par la version 3.0. Pour plus d’informations, consultez hello [documentation pour la version 3.0 de hello Extension Diagnostics Linux](../diagnostic-extension.md).

## <a name="introduction"></a>Introduction

(**Remarque**: hello Extension Diagnostics Linux est open source sur [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) sur lequel les informations les plus récentes sur l’extension de hello hello sont tout d’abord publiées. Vous souhaiterez peut-être toocheck hello [page GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) premier.)

Hello Extension Diagnostics Linux permet un Bonjour de moniteur utilisateur les machines virtuelles Linux qui sont en cours d’exécution sur Microsoft Azure. Il a hello suivant de fonctionnalités :

* Collecte et télécharge les informations sur les performances système hello à partir de la table de stockage de l’utilisateur toohello hello Linux VM, y compris les informations de diagnostic et syslog.
* Permet aux utilisateurs toocustomize hello les métriques de données qui seront collectés et téléchargés.
* Permet aux utilisateurs tooupload journal spécifié fichiers tooa désigné stockage table.

Dans la version actuelle de hello 2.3, les données de salutation incluent :

* tous les journaux Rsyslog de Linux, y compris les journaux système, de sécurité et d’applications ;
* Toutes les données système qui sont spécifiées sur [site de System Center Cross-Platform Solutions hello](https://scx.codeplex.com/wikipage?title=xplatproviders).
* les fichiers journaux spécifiés par l’utilisateur.

Cette extension fonctionne avec hello classique et les modèles de déploiement de gestionnaire de ressources.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>Version actuelle de l’extension de hello et désapprobation d’anciennes versions

version la plus récente de l’extension de hello Hello est **2.3**, et **toutes les anciennes versions (2.0, 2.1 et 2.2) seront déconseillées et publiées par la fin de cette année (2017)**. Si vous avez installé hello extension de Diagnostic de Linux avec mise à niveau de version mineure automatique désactivé, il est fortement recommandé de désinstaller l’extension de hello et de le réinstaller avec mise à niveau de version mineure automatique activée. Sur les ordinateurs virtuels (ASM) classiques, vous pouvez y parvenir en spécifiant « 2.* » en tant que version de hello si vous installez extension hello via Azure-XPLAT-CLI ou Powershell. Sur les machines virtuelles ARM, vous pouvez y parvenir en incluant ' « autoUpgradeMinorVersion » : true' dans le modèle de déploiement d’ordinateur virtuel hello. En outre, toute nouvelle installation de l’extension de hello version doit être hello automatique secondaire mise à niveau d’option est activée.

## <a name="enable-hello-extension"></a>Activer l’extension de hello

Vous pouvez activer cette extension à l’aide de hello [portail Azure](https://portal.azure.com/#), Azure PowerShell ou scripts CLI d’Azure.

tooview et configurer hello système et les données de performances directement à partir de hello portail Azure, suivent [ces étapes sur hello blog Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).

Cet article se concentre sur la façon de tooenable et configurer l’extension de hello en utilisant les commandes CLI d’Azure. Cela vous permet de tooread et afficher les données de hello directement à partir de la table de stockage hello.

Notez que les méthodes de configuration hello qui sont décrites ici ne fonctionnent pas pour hello portail Azure. tooview et configurer les données de performances du système et hello directement à partir de hello portail Azure, extension de hello doit être activée via le portail de hello.

## <a name="prerequisites"></a>Composants requis

* **Agent Microsoft Azure Linux version 2.0.6 ou ultérieure**.

  Notez que la plupart des images de la galerie Linux de machines virtuelles Azure comprennent la version 2.0.6 ou ultérieure. Vous pouvez exécuter **WAAgent-version** tooconfirm quelle version est installée sur la machine virtuelle de hello. Hello machine virtuelle exécute une version antérieure à 2.0.6, vous pouvez suivre [ces instructions sur GitHub](https://github.com/Azure/WALinuxAgent "instructions") tooupdate il.
* **Interface de ligne de commande Azure**. Suivez [ce guide pour l’installation du CLI](../../../cli-install-nodejs.md) tooset d’environnement de CLI d’Azure hello sur votre ordinateur. Après l’installation du CLI d’Azure, vous pouvez utiliser hello **azure** commande à partir de votre interface de ligne de commande (interpréteur de commandes, Terminal Server ou invite de commandes) tooaccess hello Azure commandes CLI. Par exemple :

  * Exécutez **azure vm extension set --help** pour obtenir une aide détaillée.
  * Exécutez **connexion azure** toosign dans tooAzure.
  * Exécutez **liste de machine virtuelle azure** toolist tous hello machines virtuelles que vous disposez sur Azure.
* Une données hello des toostore du compte de stockage. Vous devez un nom de compte de stockage créé précédemment et un stockage tooyour de données access tooupload clé hello.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Utilisez la commande tooenable hello Extension Diagnostics Linux hello CLI d’Azure

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>Scénario 1 Activer l’extension hello avec le jeu de données par défaut hello

Dans la version 2.3 ou version ultérieure, les données de valeur par défaut de hello qui seront collectées incluent :

* Toutes les informations de Rsyslog (y compris les journaux système, de sécurité et des applications)  
* Un ensemble principal de données système de base Notez que hello du jeu de données complet est décrit sur hello [site System Center Cross-Platform Solutions](https://scx.codeplex.com/wikipage?title=xplatproviders).
  Si vous souhaitez tooenable des données supplémentaires, passez aux étapes de hello dans les scénarios 2 et 3.

Étape 1. Créez un fichier nommé PrivateConfig.json avec hello suivant contenu :

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

Étape 2. Exécutez **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>Scénario 2 Personnaliser les métriques de moniteur de performances hello

Cette section décrit comment toocustomize hello les performances et la table de données de diagnostic.

Étape 1. Créez un fichier nommé PrivateConfig.json avec un contenu hello qui a été décrite dans le scénario 1. Créez également un fichier nommé PublicConfig.json. Spécifier hello particulier données toocollect.

Pour tous les fournisseurs et les variables, référence hello [site System Center Cross-Platform Solutions](https://scx.codeplex.com/wikipage?title=xplatproviders). Vous pouvez avoir plusieurs requêtes et les stocker dans plusieurs tables en ajoutant le script de toohello plusieurs requêtes.

Par défaut, hello Rsyslog données est systématiquement collecté.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


Étape 2. Exécutez **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

### <a name="scenario-3-upload-your-own-log-files"></a>Scénario 3 Charger vos propres fichiers journaux

Cette section décrit le fonctionnement des fichiers de compte de stockage tooyour toocollect et le téléchargement des journaux spécifiques. Vous devez toospecify à la fois hello chemin d’accès tooyour journal hello de fichiers et de nom de table hello où vous souhaitez toostore votre journal. Vous pouvez créer plusieurs fichiers journaux en ajoutant plusieurs scripts de toohello entrées/table de fichiers.

Étape 1. Créez un fichier nommé PrivateConfig.json avec un contenu hello qui a été décrite dans le scénario 1. Puis créez un autre fichier nommé PublicConfig.json avec hello suivant contenu :

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

Étape 2. Exécutez `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.

Remarque : ce paramètre sur hello extension versions antérieures too2.3, tous les journaux générés trop`/var/log/mysql.err` peut être dupliqué trop`/var/log/syslog` (ou `/var/log/messages` en fonction de distribution de Linux hello) également. Si vous souhaitez que tooavoid ce doublon de journalisation, vous pouvez exclure de la journalisation des `local6` ouvre une fonctionnalité dans votre configuration rsyslog. Il dépend de distribution de Linux hello, mais sur un système Ubuntu 14.04, hello fichier toomodify est `/etc/rsyslog.d/50-default.conf` et vous pouvez remplacer la ligne de hello `*.*;auth,authpriv.none -/var/log/syslog` trop`*.*;auth,authpriv,local6.none -/var/log/syslog`. Ce problème est résolu dans la dernière version de correctif logiciel hello de 2.3 (2.3.9007), donc si vous avez l’extension hello version 2.3, ce problème ne doit pas se produire. Si elle est toujours le cas même après le redémarrage de votre machine virtuelle, veuillez nous contacter et nous aider à résoudre les problèmes de la raison pour laquelle la dernière version de correctif logiciel hello n’est pas installée automatiquement.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>Scénario 4 Arrêter l’extension hello à partir de la collecte de journaux

Cette section décrit comment extension de hello toostop de collecter des journaux. Notez que hello analyse des processus de l’agent sera toujours en cours d’exécution, même avec cette reconfiguration. Si vous souhaitez que hello toostop complètement le processus de l’agent d’analyse, vous pouvez le faire par la désactivation de l’extension de hello. extension de hello Hello commande toodisable est `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.

Étape 1. Créez un fichier nommé PrivateConfig.json avec un contenu hello qui a été décrite dans le scénario 1. Créer un autre fichier nommé PublicConfig.json avec hello suivant contenu :

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


Étape 2. Exécutez **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

## <a name="review-your-data"></a>Passer en revue vos données

performances de Hello et les données de diagnostic sont stockées dans une table de stockage Azure. Révision [comment toouse le stockage de Table à partir de Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn comment les données de salutation tooaccess dans le stockage hello table à l’aide de scripts CLI d’Azure.

En outre, vous pouvez utiliser UI outils tooaccess hello données suivantes :

1. Explorateur de serveurs Visual Studio. Atteindre le compte de stockage tooyour. Une fois hello machine virtuelle s’exécute pendant environ cinq minutes, vous verrez des tables par défaut de hello quatre : « LinuxCpu », « LinuxDisk », « LinuxMemory » et « Linuxsyslog ». Double-cliquez sur les données de salutation table noms tooview hello.
1. [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer");

![image](./media/diagnostic-extension/no1.png)

Si vous avez activé fileCfg ou perfCfg (comme décrit dans les scénarios 2 et 3), vous pouvez utiliser les données de non définis par défaut tooview Explorateur de serveurs Visual Studio et l’Explorateur de stockage Azure.

## <a name="known-issues"></a>Problèmes connus

* Hello Rsyslog informations et spécifié par le client le fichier journal est accessible uniquement via l’écriture de scripts.
