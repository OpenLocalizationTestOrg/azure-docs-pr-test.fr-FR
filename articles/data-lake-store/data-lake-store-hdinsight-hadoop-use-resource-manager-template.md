---
title: "aaaUse modèles Azure toocreate HDInsight et Data Lake Store | Documents Microsoft"
description: "Utilisez toocreate de modèles Azure Resource Manager et clusters HDInsight avec Azure Data Lake Store"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>Créer un cluster HDInsight avec Data Lake Store à l’aide d’un modèle Azure Resource Manager
> [!div class="op_single_selector"]
> * [Utilisation du portail](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Utilisation de PowerShell (pour le stockage par défaut)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Utilisation de PowerShell (pour le stockage supplémentaire)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Utilisation du gestionnaire des ressources](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Découvrez comment toouse Azure PowerShell tooconfigure un HDInsight de cluster avec Azure Data Lake Store **en tant que stockage supplémentaire**.

Pour les types de clusters pris en charge, Data Lake Store est utilisé comme compte de stockage par défaut ou supplémentaire. Lorsque Data Lake Store est utilisé comme espace de stockage supplémentaire, compte de stockage par défaut hello pour les clusters de hello sera toujours les objets BLOB de stockage Azure (WASB) et fichiers hello cluster (par exemple, les journaux, etc.) sont toujours enregistrées toohello du stockage par défaut, lors des données hello que vous avez choix tooprocess peuvent être stockées dans un compte Data Lake Store. À l’aide de Data Lake Store en tant qu’un compte de stockage supplémentaires n’affecte pas les performances ou le stockage de toohello hello capacité tooread/écriture à partir du cluster de hello.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Utilisation de Data Lake Store pour le stockage de cluster HDInsight

Voici quelques considérations importantes pour l’utilisation de HDInsight avec Data Lake Store :

* Clusters de HDInsight option toocreate avec un accès tooData Lake Store en tant que stockage de la valeur par défaut est disponible pour HDInsight version 3.5 et 3.6.

* Clusters de HDInsight option toocreate avec un accès tooData Lake Store en tant que stockage supplémentaire est disponible pour les versions 3.2, 3.4, 3.5 et 3.6 de HDInsight.

Dans cet article, nous approvisionnons un cluster Hadoop avec Data Lake Store comme stockage supplémentaire. Pour savoir comment toocreate un Hadoop cluster avec Data Lake Store en tant que stockage par défaut, consultez [créer un cluster HDInsight à l’aide du portail Azure Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 ou version ultérieure**. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
* **Principal du service Azure Active Directory**. Étapes de ce didacticiel fournissent des instructions sur la façon de toocreate un principal de service dans Azure AD. Toutefois, vous devez être un toocreate en mesure de Azure AD administrateur toobe un principal de service. Si vous êtes un administrateur Azure AD, vous pouvez ignorer cette condition préalable et poursuivre le didacticiel de hello.

    **Si vous n’êtes pas un administrateur Azure AD**, vous ne serez pas en mesure de tooperform hello étapes requises toocreate un principal de service. Dans ce cas, votre administrateur Azure AD doit d’abord créer un principal du service. Vous pourrez ensuite créer un cluster HDInsight avec Data Lake Store. En outre, hello principal du service doit être créé à l’aide d’un certificat, comme décrit dans [créer un principal de service avec certificat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>Créer un cluster HDInsight avec Azure Data Lake Store
modèle de gestionnaire de ressources Hello et conditions préalables de hello pour à l’aide du modèle de hello, sont disponibles sur GitHub à l’adresse [déployer un cluster HDInsight Linux avec la nouvelle Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage). Suivez les instructions de hello fournies à cette toocreate lien un cluster HDInsight avec Azure Data Lake Store en tant qu’espace de stockage supplémentaire hello.

les instructions de Hello au lien hello mentionnés ci-dessus requièrent PowerShell. Avant de commencer avec ces instructions, vérifiez que vous vous connectez tooyour compte Azure. À partir de votre bureau, ouvrez une nouvelle fenêtre Azure PowerShell et entrez hello suivant des extraits de code. Toolog demandée, assurez-vous que vous connectez en tant qu’un des admininistrators/propriétaire de l’abonnement hello :

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>Télécharger l’exemple données toohello Azure Data Lake Store
modèle de gestionnaire de ressources Hello crée un nouveau compte Data Lake Store et l’associe à cluster HDInsight de hello. Vous devez maintenant télécharger certaines toohello de données exemple Data Lake Store. Vous aurez besoin de ces données plus loin dans les tâches de didacticiel toorun hello à partir d’un cluster HDInsight qui accèdent aux données hello Data Lake Store. Pour obtenir des instructions sur la façon de tooupload de données, consultez [télécharger un fichier de tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata). Si vous recherchez des tooupload de données d’exemple, vous pouvez obtenir hello **Ambulance données** dossier hello [référentiel Git de LAC de données Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="set-relevant-acls-on-hello-sample-data"></a>Définir les ACL appropriées sur les données d’exemple hello
toomake que données exemple hello que vous chargez sont accessibles à partir du cluster HDInsight de hello, vous devez vous assurer qu’application hello Azure AD qui est l’identité tooestablish utilisée entre le cluster HDInsight de hello et Data Lake Store a accès toohello fichier/dossier que vous êtes la tentative de tooaccess. toodo, effectuer hello comme suit.

1. Rechercher le nom hello de hello application Azure AD qui est associée au cluster HDInsight et hello Data Lake Store. Une façon toolook pour le nom de hello tooopen panneau du cluster HDInsight de hello que vous avez créé à l’aide du modèle de gestionnaire de ressources hello, cliquez sur hello **Cluster AAD identité** onglet et recherchez la valeur hello **Principal du Service Nom d’affichage**.
2. Maintenant, fournir des accès toothis application Azure AD sur hello fichier/dossier que vous souhaitez tooaccess à partir du cluster HDInsight de hello. tooset hello ACL sur le fichier/dossier hello dans Data Lake Store, voir [sécurisation des données dans Data Lake Store](data-lake-store-secure-data.md#filepermissions).

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Exécuter les tâches de test sur Bonjour HDInsight cluster toouse Bonjour Data Lake Store
Après avoir configuré un cluster HDInsight, vous pouvez exécuter les travaux test sur hello cluster tootest que hello HDInsight peut accéder à Data Lake Store. toodo par conséquent, nous allons exécuter un travail Hive exemple qui crée une table à l’aide des données d’exemple hello que vous avez téléchargé antérieures tooyour Data Lake Store.

Dans cette section sera SSH dans un cluster HDInsight Linux et une exécution hello un exemple de requête Hive. Si vous utilisez un client Windows, nous vous recommandons d’utiliser **PuTTY**, qui peut être téléchargé à partir de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Pour plus d’informations sur l’utilisation de PuTTY, consultez la rubrique [Utilisation de SSH avec Hadoop Linux dans HDInsight à partir de Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

1. Une fois connecté, démarrer hello CLI de la ruche à l’aide de hello de commande suivante :

   ```
   hive
   ```
2. À l’aide de hello CLI, entrez hello suivant les instructions toocreate une nouvelle table nommée **véhicules** à l’aide des données d’exemple hello Bonjour Data Lake Store :

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   Vous devez voir s’afficher une sortie similaire toohello :

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>Accéder à Data Lake Store avec les commandes HDFS
Une fois que vous avez configuré le cluster HDInsight de hello toouse Data Lake Store, vous pouvez utiliser hello HDFS shell commandes tooaccess hello magasin.

Dans cette section sera SSH dans un cluster HDInsight Linux et une exécution hello commandes HDFS. Si vous utilisez un client Windows, nous vous recommandons d’utiliser **PuTTY**, qui peut être téléchargé à partir de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Pour plus d’informations sur l’utilisation de PuTTY, consultez la rubrique [Utilisation de SSH avec Hadoop Linux dans HDInsight à partir de Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

Une fois connecté, utilisez hello suivant fichiers HDFS filesystem commande toolist hello Bonjour Data Lake Store.

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

Elle doit répertorier fichier hello que vous avez téléchargé antérieures toohello Data Lake Store.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

Vous pouvez également utiliser hello `hdfs dfs -put` commande tooupload certains toohello fichiers Data Lake Store, puis utilisez `hdfs dfs -ls` tooverify indique si les fichiers de hello ont été téléchargés avec succès.


## <a name="next-steps"></a>Étapes suivantes
* [Copier des données d’objets BLOB de stockage Azure tooData Lake Store](data-lake-store-copy-data-wasb-distcp.md)
