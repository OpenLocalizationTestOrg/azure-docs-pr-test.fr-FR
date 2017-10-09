---
title: "Création - Azure d’un cluster aaaAdd les bibliothèques Hive pendant HDInsight | Documents Microsoft"
description: "Découvrez comment les bibliothèques Hive tooadd (fichiers jar), tooan HDInsight de cluster lors de la création du cluster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>Ajouter des bibliothèques Hive personnalisées lors de la création de votre cluster HDInsight

Si vous avez des bibliothèques que vous utilisez fréquemment avec Hive dans HDInsight, ce document contient des informations sur l’utilisation de bibliothèques de hello toopre-charge un Action de Script lors de la création du cluster. Bibliothèques ajoutés à l’aide des étapes de hello dans ce document sont disponibles dans la ruche - il n’existe aucun besoin toouse [ajouter JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload les.

## <a name="how-it-works"></a>Fonctionnement

Lorsque vous créez un cluster, vous pouvez éventuellement spécifier une Action de Script qui exécute un script sur les nœuds de cluster hello lors de leur création. script Hello dans ce document accepte un seul paramètre, qui est un emplacement WASB contenant toobe de bibliothèques (stockés en tant que fichiers jar) hello préchargé.

Lors de la création du cluster, script de hello énumère les fichiers de hello, copie les toohello `/usr/lib/customhivelibs/` active sur les nœuds de tête et de travail, puis les ajoute toohello `hive.aux.jars.path` propriété Bonjour `core-site.xml` fichier. Sur les clusters basés sur Linux, il met également à jour hello `hive-env.sh` fichier à l’emplacement des fichiers de hello hello.

> [!NOTE]
> À l’aide des actions de script hello dans cet article fournit les bibliothèques hello Bonjour les scénarios suivants :
>
> * **HDInsight de basés sur Linux** : quand à l’aide de hello un client Hive, **WebHCat**, et **HiveServer2**.
> * **Basé sur Windows de HDInsight** - lors de l’utilisation du client de ruche hello et **WebHCat**.

## <a name="hello-script"></a>script de Hello

**Emplacement du script**

Pour les **clusters basés sur Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

Pour les **clusters basés sur Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

**Configuration requise**

* les scripts Hello doivent être appliqué tooboth hello **Head nœuds** et **nœuds Worker**.

* Hello JAR que vous souhaitez tooinstall doivent être stockées dans le stockage d’objets Blob Azure dans un **seul conteneur**.

* compte de stockage Hello contenant la bibliothèque hello des fichiers jar **doit** être toohello lié HDInsight cluster lors de la création. Il doit être compte de stockage par défaut hello ou un compte ajouté via __configuration facultative__.

* conteneur de toohello Hello WASB chemin d’accès doit être spécifiée comme un toohello du paramètre Action de Script. Par exemple, si hello JAR est stockés dans un conteneur nommé **libs** sur un compte de stockage nommé **mystorage**, paramètre hello serait  **wasb://libs@mystorage.blob.core.windows.net/** .

  > [!NOTE]
  > Ce document suppose que vous avez déjà créer un compte de stockage, conteneur d’objets blob et tooit des fichiers téléchargés hello.
  >
  > Si vous n’avez pas créé un compte de stockage, vous pouvez le faire via hello [portail Azure](https://portal.azure.com). Vous pouvez ensuite utiliser un utilitaire tel que [Azure Storage Explorer](http://storageexplorer.com/) toocreate un conteneur dans le compte de hello et le téléchargement des fichiers tooit.

## <a name="create-a-cluster-using-hello-script"></a>Créer un cluster à l’aide du script de hello

> [!NOTE]
> Hello suit créer un cluster HDInsight de basés sur Linux. toocreate un cluster basé sur Windows, sélectionnez **Windows** comme hello de cluster du système d’exploitation lors de la création du cluster de hello et utiliser le script de Windows (PowerShell) hello au lieu de script d’interpréteur de commandes hello.
>
> Vous pouvez également utiliser Azure PowerShell ou toocreate du Kit de développement logiciel HDInsight .NET hello un cluster à l’aide de ce script. Pour plus d’informations sur ces méthodes, consultez [Personnaliser des clusters HDInsight à l’aide d’actions de script](hdinsight-hadoop-customize-cluster-linux.md).

1. Démarrer l’approvisionnement d’un cluster à l’aide des étapes hello dans [HDInsight de configurer des clusters sur Linux](hdinsight-hadoop-provision-linux-clusters.md), mais n’effectuez pas la mise en service.

2. Sur hello **Configuration facultative** panneau, sélectionnez **Actions de Script**et fournir hello informations suivantes :

   * **NOM**: entrez un nom convivial pour l’action de script hello.

   * **URI du script** : https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **HEAD**: cochez cette option.

   * **WORKER** : cochez cette option.

   * **ZOOKEEPER** : laissez ce champ vide.

   * **PARAMÈTRES**: entrez hello WASB toohello conteneur et le stockage compte d’adresse qui contient les fichiers JAR hello. Par exemple : **wasb://libs@mystorage.blob.core.windows.net/**.

3. En bas de hello Hello **Actions de Script**, utilisez hello **sélectionnez** configuration hello toosave du bouton.

4. Sur hello **Configuration facultative** panneau, sélectionnez **des comptes de stockage liés** et sélectionnez hello **ajouter une clé de stockage** lien. Sélectionnez le compte de stockage hello qui contient les fichiers JAR hello et utilisez hello **sélectionnez** paramètres toosave de boutons et retour hello **Configuration facultative** panneau.

5. Hello d’utilisation **sélectionnez** bouton bas hello hello **Configuration facultative** informations de configuration facultatives panneau toosave hello.

6. Continuer la mise en service de cluster de hello comme décrit dans [HDInsight de configurer des clusters sur Linux](hdinsight-hadoop-provision-linux-clusters.md).

Une fois la création du cluster terminée, vous êtes en mesure de toouse fichiers JAR hello ajoutées via ce script à partir de la ruche sans avoir toouse hello `ADD JAR` instruction.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d'informations sur l’utilisation de Hive, consultez la rubrique [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
