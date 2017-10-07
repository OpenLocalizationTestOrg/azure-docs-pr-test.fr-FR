---
title: "aaaScript du développement d’actions avec HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toocustomize Hadoop clusters avec l’Action de Script. Action de script peut être utilisé tooinstall des logiciels supplémentaires en cours d’exécution sur une configuration Hadoop cluster ou toochange hello des applications installées sur un cluster."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>Développer des scripts d’action de script pour des clusters HDInsight Windows
Découvrez comment toowrite Action de Script des scripts pour HDInsight. Pour plus d’informations sur les scripts d’action de script, consultez [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster.md). Pour hello même article écrit pour les clusters HDInsight de basés sur Linux, consultez [des scripts de développer une Action de Script pour HDInsight](hdinsight-hadoop-script-actions-linux.md).



> [!IMPORTANT]
> les étapes dans ce document seul le travail clusters HDInsight de basés sur Windows Hello. HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Pour plus d’informations sur l’utilisation des actions de script avec les clusters basés sur Linux, consultez [Développement d’action de script avec HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).
>
>



Action de script peut être utilisé tooinstall des logiciels supplémentaires en cours d’exécution sur une configuration Hadoop cluster ou toochange hello des applications installées sur un cluster. Actions de script sont des scripts qui s’exécutent sur les nœuds de cluster hello lors du déploiement de clusters HDInsight, et elles sont exécutées une fois que les nœuds de cluster de hello terminer la configuration de HDInsight. Une action de script est exécutée sous des privilèges de compte d’administrateur système et fournit des droits d’accès complets des nœuds de cluster toohello. Chaque cluster peut être fourni avec une liste de toobe d’actions de script exécutée dans l’ordre de hello dans lequel elles sont spécifiées.

> [!NOTE]
> Si vous rencontrez hello message d’erreur suivant :
>
> System.Management.Automation.CommandNotFoundException ; %Exceptionmessage : hello terme 'Save-HDIFile' n’est pas reconnu comme nom hello de l’applet de commande, fonction, fichier de script ou programme exécutable. Vérifier l’orthographe hello du nom de hello, ou si un chemin d’accès existe, vérifiez que le chemin hello est correct et réessayez.
> Cela signifie que vous n’avez pas inclure des méthodes d’assistance hello.  Consultez [Méthodes d’assistance pour les scripts personnalisés](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).
>
>

## <a name="sample-scripts"></a>Exemples de scripts
Pour créer des clusters HDInsight sur un système d’exploitation Windows, hello Action de Script est le script Azure PowerShell. Bonjour script suivant est un exemple de configuration des fichiers de configuration de site hello :

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

script de Hello accepte quatre paramètres, nom de fichier de configuration de hello, propriété hello toomodify, hello valeur tooset et une description. Par exemple :

    hive-site.xml hive.metastore.client.socket.timeout 90

Ces paramètres définit hello hive.metastore.client.socket.timeout valeur too90 hello hive-site.XML fichier.  Hello par défaut est 60 secondes.

Cet exemple de script est également disponible à l’adresse [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).

HDInsight fournit plusieurs scripts tooinstall des composants supplémentaires sur les clusters HDInsight :

| Nom | Script |
| --- | --- |
| **Installation de Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Consultez [Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark]. |
| **Installation de R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Consultez [Installer et utiliser R sur les clusters HDInsight][hdinsight-r-scripts]. |
| **Installation de Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Consultez [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Installation de Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Consultez [Installer et utiliser Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md). |

Action de script peut être déployée à partir de hello portail Azure, Azure PowerShell ou à l’aide de hello HDInsight .NET SDK.  Pour plus d’informations, consultez l’article [Personnaliser des clusters HDInsight à l’aide d’une d’action de script][hdinsight-cluster-customize].

> [!NOTE]
> exemples de scripts Hello fonctionnent uniquement avec la version du cluster HDInsight 3.1 ou version ultérieure. Pour plus d’informations sur les versions des clusters HDInsight, consultez la page [Versions des clusters HDInsight](hdinsight-component-versioning.md).
>
>

## <a name="helper-methods-for-custom-scripts"></a>Méthodes d’assistance pour les scripts personnalisés
L’action de script fournit des méthodes d’assistance que vous pouvez utiliser lors de l’écriture de scripts personnalisés. Ces méthodes sont définies dans [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1)et peuvent être inclus dans vos scripts à l’aide de hello suivant l’exemple :

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

Voici les méthodes d’assistance hello fournies par ce script :

| Méthode d'assistance | Description |
| --- | --- |
| **Save-HDIFile** |Télécharger un fichier à partir de hello l’identificateur de ressource uniforme (URI) tooa emplacement spécifié sur le disque local hello associé au cluster de toohello attribué de nœuds de machine virtuelle Azure hello. |
| **Expand-HDIZippedFile** |Décompresser un fichier zippé. |
| **Invoke-HDICmdScript** |Exécuter un script à partir de cmd.exe. |
| **HDILog d'écriture** |Écrire la sortie à partir du script personnalisé de hello utilisé pour une action de script. |
| **Get-Services** |Obtenir la liste des services en cours d’exécution sur l’ordinateur de hello où s’exécute le script de hello. |
| **Get-Service** |Avec le nom de service spécifique hello en tant qu’entrée, obtenir des informations détaillées pour un service spécifique (nom du service, l’identificateur de processus, état, etc.) sur l’ordinateur hello où s’exécute le script de hello. |
| **Get-HDIServices** |Obtenir la liste des services HDInsight en cours d’exécution sur l’ordinateur de hello où s’exécute le script de hello. |
| **Get-HDIService** |Nom de hello spécifique HDInsight service en tant qu’entrée, obtenir des informations détaillées pour un service spécifique (nom du service, l’identificateur de processus, état, etc.) sur l’ordinateur hello où s’exécute le script de hello. |
| **Get-ServicesRunning** |Obtenir la liste des services qui s’exécutent sur l’ordinateur de hello où s’exécute le script de hello. |
| **Get-ServiceRunning** |Vérifiez si un service spécifique (par nom) est en cours d’exécution sur l’ordinateur de hello où s’exécute le script de hello. |
| **Get-HDIServicesRunning** |Obtenir la liste des services HDInsight en cours d’exécution sur l’ordinateur de hello où s’exécute le script de hello. |
| **Get-HDIServiceRunning** |Vérifiez si un service HDInsight spécifique (par nom) est en cours d’exécution sur l’ordinateur de hello où s’exécute le script de hello. |
| **Get-HDIHadoopVersion** |Obtenir la version de hello de Hadoop installé sur l’ordinateur hello où s’exécute le script de hello. |
| **Test-IsHDIHeadNode** |Vérifiez si ordinateur hello où s’exécute le script de hello est un nœud principal. |
| **Test-IsActiveHDIHeadNode** |Vérifiez si ordinateur hello où s’exécute le script de hello est un nœud principal actif. |
| **Test-IsHDIDataNode** |Vérifiez si ordinateur hello où s’exécute le script de hello est un nœud de données. |
| **Edit-HDIConfigFile** |Modifier les fichiers de configuration hive-site.XML hello, core-site.XML, hdfs-site.XML, mapred-site.XML ou yarn-site.Xml. |

## <a name="best-practices-for-script-development"></a>Meilleures pratiques relatives au développement de scripts
Lorsque vous développez un script personnalisé pour un cluster HDInsight, il existe plusieurs meilleures tookeep de pratiques à l’esprit :

* Recherchez la version de Hadoop hello

    Uniquement HDInsight version 3.1 (Hadoop 2.4) et supérieur prennent en charge à l’aide de composants de Script Action tooinstall personnalisés sur un cluster. Dans votre script personnalisé, vous devez utiliser hello **Get-HDIHadoopVersion** version d’assistance méthode toocheck hello Hadoop avant de procéder à la réalisation d’autres tâches dans le script de hello.
* Fournir stable lie les ressources tooscript

    Les utilisateurs devraient vous assurer que tous les scripts hello et autres artefacts sont utilisés dans une personnalisation hello d’un cluster restent disponibles tout au long de durée de vie hello du cluster de hello et que les versions hello de ces fichiers ne changent pas pour la durée hello. Ces ressources sont requises si hello cette opération de nœuds de cluster de hello est requis. meilleure pratique de Hello est toodownload et archivez tous les éléments dans un compte de stockage hello des contrôles utilisateur. Cela peut être le compte de stockage par défaut hello ou un des autres comptes de stockage hello spécifiés au moment de hello du déploiement d’un cluster personnalisé.
    Bonjour Spark et R personnalisé des exemples de cluster fournies dans la documentation de hello, par exemple, nous avons une copie locale des ressources de hello dans ce compte de stockage : https://hdiconfigactions.blob.core.windows.net/.
* Assurez-vous que le script de personnalisation de cluster hello est idempotente

    Vous devez attendre que les nœuds hello d’un cluster HDInsight est réinitialisée pendant la durée de vie de cluster hello. script de personnalisation de cluster Hello est exécutée chaque fois qu’un cluster est réinitialisé. Ce script doit être idempotente toobe conçu dans le sens hello que lors de la réinitialisation, script de hello doit s’assurer que le cluster hello est retourné toohello que état où elle se trouvait juste après que le script de hello pour hello première exécution lorsque le cluster de hello était initialement personnalisés créé. Par exemple, si un script personnalisé installé une application à D:\AppLocation sur sa première exécution, puis à chaque exécution ultérieure, lors de la réinitialisation, script de hello doit vérifier l’existence d’application hello en hello emplacement D:\AppLocation avant de continuer avec d’autres étapes de script de hello.
* Installer des composants personnalisés dans un emplacement optimal de hello

    Lorsque les nœuds de cluster sont réinitialisés, lecteur de ressources C:\ hello et lecteur D:\ du système peuvent être remis en forme, entraînant la perte de hello de données et applications qui avaient été installées sur ces lecteurs. Cela peut également se produire si un nœud de machine virtuelle Azure (VM) qui fait partie du cluster de hello tombe en panne et est remplacé par un nouveau nœud. Vous pouvez installer les composants sur hello lecteur D:\ ou emplacement de C:\apps hello sur le cluster de hello. Tous les autres emplacements sur le lecteur C:\ de hello sont réservés. Spécifiez hello emplacement pour les applications ou bibliothèques toobe installé dans le script de personnalisation de cluster hello.
* Garantir une haute disponibilité de l’architecture de cluster hello

    HDInsight possède une architecture actif / passif pour la haute disponibilité, dans quel un nœud principal est en mode actif (hello HDInsight exécutant services) et hello autres nœud principal est en mode veille (dans le HDInsight services ne sont pas en cours d’exécution). les nœuds Hello basculer entre les modes actifs et passifs si services HDInsight sont interrompues. Si une action de script est services tooinstall utilisé sur les deux nœuds principal pour la haute disponibilité, notez que ce mécanisme de basculement HDInsight hello n’est pas en mesure de tooautomatically échouent sur ces services installé par l’utilisateur. Par conséquent, installé par l’utilisateur des services sur les nœuds principal HDInsight qui sont attendu toobe hautement disponible doivent être ont leur propre mécanisme de basculement en mode actif / passif ou en mode actif-actif.

    Une commande de l’Action de Script HDInsight s’exécute sur les deux nœuds principal lorsque le rôle de nœud principal et hello est spécifié en tant que valeur Bonjour *ClusterRoleCollection* paramètre. Par conséquent, lorsque vous concevez des scripts personnalisés, vérifiez qu'il est au fait de cette configuration. Vous ne devez pas exécuter des problèmes où hello mêmes services sont installés et démarrés sur les deux nœuds principaux d’hello et ils finissent en concurrence avec eux. En outre, sachez que les données sont perdues lors de la réinitialisation, logiciels installés via l’Action de Script a toobe toosuch résilient événements. Les applications doivent prendre toowork conçue avec des données hautement disponibles sont répartie sur plusieurs nœuds. Notez que le maximum de 1/5 de nœuds hello dans un cluster peut être réinitialisé à hello même temps.
* Configurer le stockage d’objets Blob Azure hello des composants personnalisés toouse

    les composants personnalisés Hello que vous installez sur les nœuds de cluster hello peuvent avoir un toouse de configuration par défaut stockage de système de fichiers distribués Hadoop (HDFS). Vous devez modifier hello configuration toouse stockage d’objets Blob Azure à la place. Sur la réinitialisation du cluster, système de fichiers HDFS hello obtient mis en forme et vous perdez toutes les données qui y sont stockées. L'utilisation du stockage d'objets blob Azure au lieu du stockage HDFS garantit que vos données sont conservées.

## <a name="common-usage-patterns"></a>Modes d’utilisation courants
Cette section fournit des conseils sur l’implémentation des modèles d’utilisation courants hello que vous pouvez rencontrer lors de l’écriture de votre propre script personnalisé.

### <a name="configure-environment-variables"></a>Configuration des variables d’environnement
Dans le développement d’action de script, vous sentirez souvent hello devez tooset variables d’environnement. Par exemple, un scénario le plus probable est lorsque vous téléchargez un fichier binaire à partir d’un site externe, l’installer sur un cluster de hello et ajoutez un emplacement où il est variable d’environnement « PATH » installé tooyour hello. Hello suivant extrait de code montre comment les variables d’environnement tooset dans hello script personnalisé.

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

Cette instruction définit la variable d’environnement hello **MDS_RUNNER_CUSTOM_CLUSTER** toohello valeur 'true' et jeux hello étendue de cette variable toobe à l’échelle de l’ordinateur. Dans certains cas, il est important que les variables d’environnement sont définies au niveau de portée approprié hello : utilisateur ou ordinateur. Cliquez [ici][1] pour obtenir plus d’informations sur la définition des variables d’environnement.

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Toolocations d’accès où sont stockés les scripts personnalisés hello
Scripts utilisés toocustomize un tooeither de besoins de cluster soit dans le compte de stockage par défaut hello pour le cluster de hello dans un conteneur en lecture seule public sur d’autres comptes de stockage. Si votre script accède à des ressources situées ailleurs ceux-ci doivent toobe dans accessible publiquement (publics au moins en lecture seule). Par exemple, vous pouvez souhaitez tooaccess un fichier et enregistrez-le à l’aide de la commande hello SaveFile-HDI.

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

Dans cet exemple, vous devez vous assurer que le conteneur de hello 'somecontainer' dans le compte de stockage 'somestorageaccount' n’est accessible publiquement. Dans le cas contraire, le script de hello lève une exception « Introuvable » et échouer.

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>Passer des paramètres toohello Add-AzureRmHDInsightScriptAction applet de commande
toopass plusieurs applet de commande de paramètres toohello Add-AzureRmHDInsightScriptAction, vous devez tooformat hello chaîne valeur toocontain tous les paramètres de script de hello. Par exemple :

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

or

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>Lever une exception pour l’échec d’un déploiement de cluster
Si vous souhaitez tooget précisément averti du fait de hello de personnalisation cluster a échoué comme prévu, il est important toothrow une exception et Échec de la création du cluster hello. Par exemple, vous pouvez souhaitez tooprocess un fichier s’il existe et gérer les cas d’erreur hello où le fichier de hello n’existe pas. Il en résulterait que script de hello s’arrête correctement et hello état du cluster de hello est correctement connu. Hello extrait de code suivant donne un exemple de procédure tooachieve cela :

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

Dans cet extrait de code, si le fichier de hello n’existe pas, il entraînerait tooa état hello script réellement s’arrête correctement après l’impression du message d’erreur hello, alors que le cluster de hello atteint l’état en cours d’exécution, en supposant qu’il les processus de personnalisation de cluster « avec succès » s’est terminée. Si vous souhaitez toobe précisément averti du fait de hello de personnalisation cluster essentiellement a échoué comme prévu en raison d’un fichier manquant, il est plus approprié toothrow une exception et que vous échouer l’étape de personnalisation de cluster hello. tooachieve cela vous devez utiliser hello suivant extrait de code à la place.

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>Liste de vérification pour le déploiement d’une action de script
Voici les étapes hello que étaient lors de la préparation toodeploy ces scripts :

1. Placez les fichiers hello qui contiennent des scripts personnalisés hello dans un emplacement accessible par les nœuds de cluster hello lors du déploiement. Il peut s’agir d’une des valeur par défaut hello ou des comptes de stockage supplémentaires spécifiées au moment de hello de déploiement de cluster, ou tout autre conteneur de stockage accessible publiquement.
2. Ajouter des vérifications en toomake scripts assurer qu’elles s’exécutent de manière idempotente, afin que le script de hello peut être exécutée à plusieurs reprises sur hello même nœud.
3. Hello d’utilisation **Write-Output** tooSTDOUT de tooprint d’applet de commande Azure PowerShell, ainsi que STDERR. N'utilisez pas **Write-Host**.
4. Utiliser un dossier de fichiers temporaires, tels que $env : TEMP, tookeep hello fichier téléchargé utilisée par les scripts de hello et puis les nettoyer après aient l’exécution de scripts.
5. 5.Installez des logiciels personnalisés uniquement aux emplacements suivants : D:\ ou C:\apps. Autres emplacements sur le lecteur C: de hello ne doivent pas servir comme ils sont réservés. Notez que l’installation des fichiers sur le lecteur C: de hello en dehors du dossier de C:\apps hello peut-être générer des échecs d’installation pendant reimages du nœud de hello.
6. Dans événement hello que les paramètres au niveau du système d’exploitation ou les fichiers de configuration de service Hadoop ont été modifiés, vous pouvez vouloir toorestart HDInsight services afin qu’ils peuvent tous les paramètres au niveau du système d’exploitation, tels que des variables d’environnement hello set dans les scripts de hello.

## <a name="debug-custom-scripts"></a>Déboguer des scripts personnalisés
journaux des erreurs de script Hello sont stockées, ainsi que d’autres de sortie du compte de stockage par défaut hello que vous avez spécifié pour le cluster hello lors de sa création. Hello journaux sont stockés dans une table avec le nom de hello *u < \cluster-name-fragment >< \time-stamp > setuplog*. Il s’agit de journaux agrégées qui ont des enregistrements à partir de tous les nœuds hello (nœud principal et nœuds de travail) sur le hello script s’exécute dans un cluster de hello.
Toocheck hello journaux est toouse facilement les outils HDInsight pour Visual Studio. Pour installer les outils de hello, consultez [commencer à l’aide des outils Visual Studio Hadoop pour HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**journal de hello toocheck à l’aide de Visual Studio**

1. Ouvrez Visual Studio.
2. Cliquez sur **Affichage**, puis sur **Explorateur de serveurs**.
3. Cliquez sur « Azure », cliquez sur se connecter trop**abonnements Microsoft Azure**, puis entrez vos informations d’identification.
4. Développez **stockage**compte de stockage Azure hello utilisé en tant que système de fichiers par défaut hello successivement **Tables**, puis double-cliquez sur le nom de la table hello.

Vous pouvez également à distance dans toosee de nœuds de cluster hello STDOUT et STDERR pour des scripts personnalisés. Hello journaux sur chaque nœud sont spécifiques seul nœud toothat et être connectés à **C:\HDInsightLogs\DeploymentAgent.log**. Ces fichiers journaux enregistrent toutes les sorties à partir d’un script personnalisé hello. Un extrait de journal pour une action de script Spark ressemble à ceci :

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


Dans ce journal, il est clair qu’action de script Spark hello a été exécutée sur hello ordinateur virtuel nommé HEADNODE0 et qu’aucune exceptions ont été levées lors de l’exécution de hello.

Dans l’événement de hello un échec d’exécution se produit, sortie hello décrivant il est également contenue dans ce fichier journal. les informations de Hello fournies dans ces journaux doivent être utiles lors du débogage des problèmes de script qui peuvent survenir.

## <a name="see-also"></a>Voir aussi
* [Personnaliser des clusters HDInsight à l’aide d’une action de script][hdinsight-cluster-customize]
* [Installer et utiliser Spark sur les clusters HDInsight][hdinsight-install-spark]
* [Installer et utiliser R sur les clusters HDInsight][hdinsight-r-scripts]
* [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install.md)
* [Installez et utilisez Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
