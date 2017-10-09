---
title: "développement de l’action aaaScript hdinsight basés sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment toouse Bash scripts toocustomize basés sur Linux de HDInsight clusters. fonctionnalité d’action de script Hello de HDInsight vous permet de toorun scripts pendant ou après la création du cluster. Les scripts peuvent être toochange utilisé les paramètres de configuration de cluster ou installer des logiciels supplémentaires."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>Développement d’actions de script avec HDInsight

Découvrez comment votre cluster HDInsight à l’aide Bash toocustomize des scripts. Actions de script sont un moyen de toocustomize HDInsight pendant ou après la création du cluster.

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-are-script-actions"></a>Définition des actions de script

Actions de script sont des scripts Bash Azure s’exécute sur les modifications de configuration hello cluster nœuds toomake ou installer des logiciels. Une action de script est exécutée en tant que racine et fournit un accès complet de nœuds de cluster toohello droits.

Actions de script peuvent être appliquées via hello méthodes suivantes :

| Utilisez cette méthode de tooapply un script... | Pendant la création du cluster... | Sur un cluster en cours d'exécution... |
| --- |:---:|:---:|
| Portail Azure |✓  |✓ |
| Azure PowerShell |✓ |✓ |
| Interface de ligne de commande Azure |&nbsp; |✓ |
| Kit de développement logiciel (SDK) .NET de HDInsight |✓ |✓ |
| Modèle Azure Resource Manager |✓ |&nbsp; |

Pour plus d’informations sur l’utilisation de ces actions de script tooapply méthodes, consultez [HDInsight de personnaliser des clusters à l’aide des actions de script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Meilleures pratiques relatives au développement de scripts

Lorsque vous développez un script personnalisé pour un cluster HDInsight, il existe plusieurs meilleures tookeep de pratiques à l’esprit :

* [Version de Hadoop hello cible](#bPS1)
* [Cibler hello Version du système d’exploitation](#bps10)
* [Fournir stable lie les ressources tooscript](#bPS2)
* [Utiliser des ressources précompilées](#bPS4)
* [Assurez-vous que le script de personnalisation de cluster hello est idempotente](#bPS3)
* [Garantir une haute disponibilité de l’architecture de cluster hello](#bPS5)
* [Configurer le stockage d’objets Blob Azure hello des composants personnalisés toouse](#bPS6)
* [Écrire des informations tooSTDOUT et STDERR](#bPS7)
* [Enregistrer des fichiers au format ASCII avec les fins de ligne LF](#bps8)
* [Utilisez toorecover logique de nouvelle tentative d’erreurs transitoires](#bps9)

> [!IMPORTANT]
> Actions de script doivent se terminer dans les 60 minutes ou hello processus échoue. Lors de la configuration de nœud, script de hello s’exécute en même temps que d’autres processus d’installation et la configuration. Concurrence pour les ressources, telles que la bande passante du réseau ou de temps processeur peut entraîner hello script tootake plu toofinish qu’il ne le fait dans votre environnement de développement.

### <a name="bPS1"></a>Version de Hadoop hello cible

Différentes versions de HDInsight sont équipées de différentes versions de services Hadoop et des composants installés. Si votre script attend une version spécifique d’un service ou un composant, vous devez uniquement utiliser le script de hello avec version hello de HDInsight qui inclut les composants requis de hello. Vous trouverez plus d’informations sur les versions des composants inclus dans HDInsight à l’aide de hello [le contrôle de version HDInsight composant](hdinsight-component-versioning.md) document.

### <a name="bps10"></a>Version de hello du système d’exploitation cible

HDInsight de basés sur Linux est basée sur hello distribution Ubuntu Linux. Les différentes versions de HDInsight s’appuient sur des versions différentes d’Ubuntu, ce qui peut avoir une incidence sur le comportement de votre script. Par exemple, HDInsight 3.4 et les versions antérieures sont basées sur des versions Ubuntu qui utilisent Upstart. La version 3.5 est basée sur 16.04 Ubuntu, qui utilise Systemd. Systemd et Upstart s’appuient sur les différentes commandes pour votre script doit être écrits toowork avec les deux.

Autre différence importante entre HDInsight 3.4 et 3.5 `JAVA_HOME` pointe tooJava 8.

Vous pouvez vérifier la version de hello du système d’exploitation à l’aide de `lsb_release`. Hello de code suivant montre comment toodetermine si hello script s’exécute sur Ubuntu 14 ou 16 :

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

Vous trouverez le script complet hello qui contient ces extraits de code à https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.

Pour la version hello Ubuntu est utilisé par HDInsight, consultez hello [HDInsight la version du composant](hdinsight-component-versioning.md) document.

différences de hello toounderstand entre Systemd et Upstart, consultez [Systemd pour les utilisateurs de Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Fournir stable lie les ressources tooscript

Hello script et des ressources associées doivent rester disponibles pour l’ensemble de la durée de vie hello du cluster de hello. Ces ressources sont requises si de nouveaux nœuds sont ajoutés toohello cluster pendant les opérations de mise à l’échelle.

meilleure pratique de Hello est toodownload et archivez tous les éléments dans un compte de stockage Azure de votre abonnement.

> [!IMPORTANT]
> compte de stockage Hello utilisé doit être le compte de stockage par défaut hello pour le cluster de hello ou un conteneur public en lecture seule sur un autre compte de stockage.

Par exemple, les exemples hello fournis par Microsoft sont stockés dans hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) compte de stockage. Il s’agit d’un conteneur public en lecture seule géré par l’équipe de HDInsight hello.

### <a name="bPS4"></a>Utiliser des ressources précompilées

tooreduce hello fois qu’il prend toorun hello script, évitez les opérations qui compile les ressources à partir de code source. Par exemple, de précompiler des ressources et de les stocker dans un objet blob du compte Azure Storage Bonjour même centre de données en tant que HDInsight.

### <a name="bPS3"></a>Assurez-vous que le script de personnalisation de cluster hello est idempotente

Les scripts doivent être idempotents. Si le script de hello exécute plusieurs fois, elle doit retourner hello toohello cluster même chaque fois que l’état.

Par exemple, un script qui modifie les fichiers de configuration ne doit pas ajouter d’entrées en double s’il est exécuté plusieurs fois.

### <a name="bPS5"></a>Garantir une haute disponibilité de l’architecture de cluster hello

Les clusters HDInsight basés sur Linux fournissent deux nœuds principaux qui sont actives au sein du cluster de hello et exécutent des actions de script sur les deux nœuds. Si vous installez des composants hello n'attendent qu’un seul nœud principal, n’installez pas de composants de hello sur les deux nœuds principal.

> [!IMPORTANT]
> Services fournis dans le cadre de HDInsight sont conçu toofail entre deux nœuds de tête hello en fonction des besoins. Cette fonctionnalité n’est pas étendue toocustom les composants installés par le biais des actions de script. Si vous avez besoin que les composants personnalisés soient très disponibles, vous devez implémenter votre propre mécanisme de basculement.

### <a name="bPS6"></a>Configurer le stockage d’objets Blob Azure hello des composants personnalisés toouse

Les composants que vous installez sur un cluster de hello peuvent avoir une configuration par défaut qui utilise le stockage de système de fichiers distribués Hadoop (HDFS). HDInsight utilise le stockage Azure ou Data Lake Store comme stockage par défaut de hello. Fournissent un système de fichier compatible HDFS qui conserve les données même si le cluster de hello est supprimé. Vous devrez peut-être les composants tooconfigure vous installez toouse WASB ou ADL au lieu de HDFS.

Pour la plupart des opérations, vous n’avez pas besoin de système de fichiers toospecify hello. Par exemple, suivant de hello copie fichier giraph-Examples.jar de hello stockage toocluster de système de fichiers local hello :

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

Dans cet exemple, hello `hdfs` commande utilise en toute transparence de stockage de cluster par défaut hello. Pour certaines opérations, vous devrez peut-être toospecify hello URI. Par exemple, `adl:///example/jars` pour Data Lake Store ou `wasb:///example/jars` pour Stockage Azure.

### <a name="bPS7"></a>Écrire des informations tooSTDOUT et STDERR

HDInsight enregistre la sortie du script qui est écrit tooSTDOUT et STDERR. Vous pouvez afficher ces informations à l’aide de l’interface utilisateur web de Ambari hello.

> [!NOTE]
> Ambari est disponible uniquement si hello cluster a été créé. Si vous utilisez une action de script lors de la création du cluster et Échec de la création, consultez hello section Dépannage [HDInsight de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) pour d’autres façons d’accéder aux informations consignées.

La plupart des utilitaires et des packages d’installation écrivent déjà les informations tooSTDOUT et STDERR, toutefois, vous souhaiterez peut-être tooadd la journalisation supplémentaire. toosend tooSTDOUT de texte, utilisez `echo`. Par exemple :

```bash
echo "Getting ready tooinstall Foo"
```

Par défaut, `echo` envoie hello tooSTDOUT de chaîne. toodirect il tooSTDERR, ajoutez `>&2` avant `echo`. Par exemple :

```bash
>&2 echo "An error occurred installing Foo"
```

Redirige les informations écrites tooSTDOUT tooSTDERR (2) à la place. Pour plus d’informations sur la redirection des E/S, consultez [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Pour plus d’informations sur l’affichage des informations consignées par les actions de script, voir [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a> Enregistrer des fichiers au format ASCII avec les fins de ligne LF

Les scripts d’interpréteur de commandes doivent être stockés au format ASCII, avec des lignes terminées se terminant par LF. Les fichiers sont stockés au format UTF-8 ou utilisent CRLF comme fin de ligne hello peuvent échouer avec hello l’erreur suivante :

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>Utilisez toorecover logique de nouvelle tentative d’erreurs transitoires

Lors du téléchargement de fichiers, l’installation de packages à l’aide d’apt-get, ou autres actions que la transmettent de données hello internet, action de hello peut échouer en raison d’erreurs de mise en réseau tootransient. Par exemple, les ressources distantes hello avec que vous communiquez soit en cours de hello du basculement sur le nœud de sauvegarde tooa.

toomake vos erreurs résilient tootransient script, vous pouvez implémenter la logique de nouvelle tentative. Hello suivant fonction montre comment tooimplement logique de nouvelle tentative. Il effectue une nouvelle tentative opération hello trois fois avant d’échouer.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

Hello exemples suivants montrent comment toouse cette fonction.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>Méthodes d'assistance pour les scripts personnalisés

Les méthodes d’assistance aux actions de script sont des utilitaires que vous pouvez utiliser lors de l’écriture de scripts personnalisés. Ces méthodes sont contenues dans le script[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh). Utilisez hello suivant toodownload et les utiliser dans le cadre de votre script :

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

Hello suivant disponibles pour une utilisation dans votre script :

| Utilisation de l’aide | Description |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Télécharge un fichier hello source URI toohello chemin d’accès spécifié. Par défaut, il ne remplace pas un fichier existant. |
| `untar_file TARFILE DESTDIR` |Extrait un fichier tar (à l’aide de `-xf`) répertoire de destination toohello. |
| `test_is_headnode` |Lorsqu’il est exécuté sur un nœud principal de cluster, la valeur 1 est renvoyée ; dans le cas contraire, c’est la valeur 0. |
| `test_is_datanode` |Si le nœud actuel de hello est un nœud de données (traitement), retourner la valeur 1 ; Sinon, 0. |
| `test_is_first_datanode` |Si hello le nœud actuel est hello commencez par les données (traitement) nœud (nommée workernode0) retourner la valeur 1 ; Sinon, 0. |
| `get_headnodes` |Retourne le nom de domaine complet de hello de hello headnodes dans un cluster de hello. Les noms sont séparés par des virgules. Une chaîne vide est renvoyée en cas d’erreur. |
| `get_primary_headnode` |Obtient le nom de domaine complet de hello de nœud principal de principal hello. Une chaîne vide est renvoyée en cas d’erreur. |
| `get_secondary_headnode` |Obtient le nom de domaine complet de hello du nœud principal secondaire de hello. Une chaîne vide est renvoyée en cas d’erreur. |
| `get_primary_headnode_number` |Obtient le suffixe numérique hello nœud principal principal de hello. Une chaîne vide est renvoyée en cas d’erreur. |
| `get_secondary_headnode_number` |Obtient le suffixe numérique hello nœud principal secondaire de hello. Une chaîne vide est renvoyée en cas d’erreur. |

## <a name="commonusage"></a>Modes d'utilisation courants

Cette section fournit des conseils sur l’implémentation des modèles d’utilisation courants hello que vous pouvez rencontrer lors de l’écriture de votre propre script personnalisé.

### <a name="passing-parameters-tooa-script"></a>Passage de paramètres tooa script

Dans certains cas, votre script peut nécessiter des paramètres. Par exemple, vous devrez peut-être mot de passe administrateur hello pour le cluster de hello lors de l’utilisation de hello Ambari REST API.

Paramètres passés toohello script sont appelés *paramètres positionnels*et sont affectées trop`$1` pour le premier paramètre de hello, `$2` pour hello deuxième et donc sur. `$0`contient le nom hello de script hello proprement dit.

Les valeurs passées toohello script en tant que paramètres doivent être placées par des guillemets simples ('). Cela garantit que hello valeur passée est traité comme un littéral.

### <a name="setting-environment-variables"></a>Définition des variables d'environnement

Définition d’une variable d’environnement est effectuée par hello après l’instruction :

    VARIABLENAME=value

Où NOM_VARIABLE est nom hello de variable de hello. utilisation de la variable, de tooaccess hello `$VARIABLENAME`. Par exemple, tooassign une valeur fournie par un paramètre positionnel comme variable d’environnement nommée mot de passe, vous utiliseriez hello après l’instruction :

    PASSWORD=$1

Informations de toohello accès ultérieur peut ensuite l’utiliser `$PASSWORD`.

Variables d’environnement définies dans le script de hello n’existent que dans la portée de hello du script de hello. Dans certains cas, vous devrez peut-être les variables d’environnement système tooadd qui persistent une fois le script de hello est terminé. les variables d’environnement système tooadd, ajouter une variable de hello trop`/etc/environment`. Par exemple, après l’instruction de hello ajoute `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Toolocations d’accès où sont stockés les scripts personnalisés hello

Scripts utilisés toocustomize un cluster doit toobe stockée dans un des emplacements suivants de hello :

* Un __compte de stockage Azure__ associé au cluster de hello.

* Un __compte de stockage supplémentaire__ associé hello cluster.

* Une __URI lisible publiquement__. Par exemple, une URL toodata stocké sur OneDrive, Dropbox ou un autre fichier de service d’hébergement.

* Un __compte Azure Data Lake Store__ associé au cluster HDInsight de hello. Pour plus d’informations sur l’utilisation d'Azure Data Lake Store avec HDInsight, voir [Créer un cluster HDInsight avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    > [!NOTE]
    > Hello service principal HDInsight utilise tooaccess Data Lake Store doit avoir accès en lecture toohello script.

Ressources utilisées par le script de hello doivent également être publiquement disponibles.

Le stockage des fichiers de hello dans un compte de stockage Azure ou dans Azure Data Lake Store fournit un accès rapide, comme les deux dans hello réseau Azure.

> [!NOTE]
> Hello URI format utilisé tooreference hello script diffère selon service hello utilisé. Pour les comptes de stockage associés au cluster HDInsight de hello, utilisez `wasb://` ou `wasbs://`. Pour des URI lisibles publiquement, utilisez `http://` ou `https://`. Pour Data Lake Store, utilisez `adl://`.

### <a name="checking-hello-operating-system-version"></a>Vérification de la version du système d’exploitation hello

Différentes versions de HDInsight s’appuient sur des versions spécifiques d’Ubuntu. Il peut exister des différences entre les versions de système d’exploitation que vous devez vérifier dans votre script. Par exemple, vous devrez peut-être tooinstall un binaire qui est la version liée toohello d’Ubuntu.

version de hello du système d’exploitation toocheck, utilisez `lsb_release`. Par exemple, hello script suivant montre comment tooreference un tar spécifique de fichiers en fonction de la version du système d’exploitation de hello :

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>Liste de vérification pour le déploiement d'une action de script

Voici les étapes hello que étaient lors de la préparation toodeploy ces scripts :

* Placez les fichiers hello qui contiennent des scripts personnalisés hello dans un emplacement accessible par les nœuds de cluster hello lors du déploiement. Par exemple, hello du stockage par défaut pour le cluster de hello. Les fichiers peuvent également être stockés dans les services d’hébergement lisibles publiquement.
* Vérifiez que le script de hello est impotent. Ainsi, hello script toobe exécutée plusieurs fois sur hello même nœud.
* Utilisez un Bonjour tookeep de fichier temporaire répertoire /tmp téléchargé les fichiers utilisés par les scripts hello et puis les nettoyer après aient l’exécution de scripts.
* Si les paramètres au niveau du système d’exploitation ou les fichiers de configuration de service Hadoop sont modifiées, vous souhaiterez toorestart HDInsight services.

## <a name="runScriptAction"></a>Comment toorun une action de script

Vous pouvez utiliser des clusters HDInsight script actions toocustomize sont à l’aide de hello méthodes suivantes :

* Portail Azure
* Azure PowerShell
* Modèles Microsoft Azure Resource Manager
* Hello HDInsight .NET SDK.

Pour plus d’informations sur l’utilisation de chaque méthode, consultez [comment toouse de script action](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Exemples de scripts personnalisés

Microsoft fournit des exemples de scripts tooinstall composants sur un cluster HDInsight. Consultez hello suivant les liens pour plus d’actions de script d’exemple.

* [Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md)
* [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Installer et utiliser Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Installer ou mettre à niveau Mono sur les clusters HDInsight](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>Résolution des problèmes

Hello Voici les erreurs que vous pouvez rencontrer lors de l’utilisation de scripts que vous avez développé :

**Erreur** : `$'\r': command not found`. Parfois suivi par `syntax error: unexpected end of file`.

*Cause*: cette erreur se produit lorsque des lignes de hello dans un script se terminant par CRLF. Les systèmes UNIX attendent LF uniquement en tant que la fin de ligne hello.

Ce problème se produit souvent lorsque le script de hello est créé dans un environnement Windows, comme CRLF est une ligne commune se terminant par de nombreux éditeurs de texte sous Windows.

*Résolution*: si elle est une option dans votre éditeur de texte, sélectionnez un format Unix ou saut de ligne de fin de ligne hello. Vous pouvez également utiliser hello suivant de commandes sur un système Unix toochange les tooan CRLF d’hello LF :

> [!NOTE]
> Hello commandes suivantes sont à peu près équivalentes dans la mesure où ils doivent modifier hello CRLF ligne fins tooLF. Sélectionnez une basée sur les utilitaires hello disponibles sur votre système.

| Commande | Remarques |
| --- | --- |
| `unix2dos -b INFILE` |fichier d’origine de Hello est sauvegardée avec un. Extension BAK |
| `tr -d '\r' < INFILE > OUTFILE` |OUTFILE contient une version avec des terminaisons LF uniquement |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Modifie le fichier de hello directement |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |OUTFILE contient une version avec des terminaisons LF uniquement. |

**Erreur** : `line 1: #!/usr/bin/env: No such file or directory`.

*Cause*: cette erreur se produit lorsque hello script a été enregistré au format UTF-8 avec marque d’ordre d’octet (BOM).

*Résolution*: hello enregistrer le fichier au format ASCII ou UTF-8 sans une nomenclature. Vous pouvez également utiliser hello suivant de commande sur un système Unix ou Linux toocreate un fichier sans hello nomenclature :

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Remplacez `INFILE` avec le fichier de hello contenant hello nomenclature. `OUTFILE`doit être un nouveau nom de fichier, qui contient le script hello sans hello nomenclature.

## <a name="seeAlso"></a>Étapes suivantes

* Découvrez comment trop[HDInsight de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md)
* Hello d’utilisation [référence du Kit de développement logiciel HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx) toolearn plus d’informations sur la création d’applications .NET qui gérer HDInsight
* Hello d’utilisation [API REST de HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn comment des actions de gestion tooperform toouse reste sur HDInsight clusters.
