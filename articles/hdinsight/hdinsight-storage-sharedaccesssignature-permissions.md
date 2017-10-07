---
title: "accès aaaRestrict à l’aide de Signatures d’accès partagé - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toorestrict de Signatures d’accès partagé toouse HDInsight aux toodata stockée dans des objets BLOB de stockage Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>Utiliser des Signatures d’accès partagé Azure Storage toorestrict accès toodata dans HDInsight

HDInsight a toodata d’accès complet dans les comptes de stockage Azure hello associés hello cluster. Vous pouvez utiliser des Signatures d’accès partagé sur hello blob conteneur toorestrict accès toohello des données. Par exemple, tooprovide accès en lecture seule toohello données. Les Signatures d’accès partagé (SAS) sont une fonctionnalité des comptes de stockage Azure qui vous permet de toolimit accès toodata. Par exemple, en fournissant l’accès en lecture seule toodata.

> [!IMPORTANT]
> Pour une solution utilisant Apache Ranger, envisagez d’utiliser les clusters HDInsight joints à un domaine. Pour plus d’informations, consultez hello [configurer appartenant au domaine de HDInsight](hdinsight-domain-joined-configure.md) document.

> [!WARNING]
> HDInsight doit disposent d’un accès complet toohello par défaut pour les clusters hello.

## <a name="requirements"></a>Configuration requise

* Un abonnement Azure
* C# ou Python. Un exemple de code C# est fourni en tant que solution Visual Studio.

  * La version de Visual Studio doit être 2013, 2015 ou 2017
  * La version de Python doit être 2.7 ou une version ultérieure.

* Un cluster HDInsight de basés sur Linux ou [Azure PowerShell] [ powershell] -si vous disposez d’un cluster existant basés sur Linux, vous pouvez utiliser Ambari tooadd un cluster toohello de Signature d’accès partagé. Si ce n’est pas le cas, vous pouvez utiliser Azure PowerShell toocreate un cluster et ajouter une Signature d’accès partagé pendant la création du cluster.

    > [!IMPORTANT]
    > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Hello d’exemples de fichiers à partir de [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature). Ce référentiel contient hello éléments suivants :

  * Un projet Visual Studio permettant de créer un conteneur de stockage, une stratégie stockée et une SAP pour une utilisation avec HDInsight.
  * Un script Python permettant de créer un conteneur de stockage, une stratégie stockée et une SAP pour une utilisation avec HDInsight
  * Un script PowerShell que vous pouvez créer un HDInsight de cluster et le configurer toouse hello SAS.

## <a name="shared-access-signatures"></a>Les signatures d’accès partagé

Il existe deux types de signatures d’accès partagé :

* Ad hoc : hello heure de début, date d’expiration et les autorisations pour hello SAS sont spécifiés sur hello URI SAS.

* Stratégie d’accès stockée : une stratégie d’accès stockée est définie sur un conteneur de ressources, tel qu’un conteneur d’objets blob. Une stratégie peut être contraintes toomanage utilisé pour une ou plusieurs signatures d’accès partagé. Lorsque vous associez un SAS avec une stratégie d’accès stockée, hello SAS hérite des contraintes de hello - hello heure de début, date d’expiration et autorisations - définies pour la stratégie d’accès stockée hello.

Hello différence entre les formes hello deux est importante pour un scénario clé : la révocation. Une SAP est une URL, les personnes qui obtiennent hello SAS peuvent l’utiliser, quel que soit le qui a demandé qu’elle toobegin avec. Si une SAP est publiée publiquement, il peut être utilisé par tout le monde dans Bonjour. Une clé d'accès partagé qui est distribuée est valide jusqu'à ce que l'un des quatre événements suivants ait lieu :

1. délai d’expiration Hello spécifié sur hello que SAS est atteinte.

2. délai d’expiration Hello spécifié sur la stratégie d’accès stockée hello référencée par hello que SAS est atteinte. délai d’expiration hello provoquent Hello scénarios suivants toobe atteint :

    * intervalle de temps Hello a expiré.
    * stratégie d’accès stockée Hello est modifié toohave un délai d’expiration Bonjour passées. La modification du délai d’expiration hello est une façon toorevoke hello SAS.

3. Hello stockés de la stratégie d’accès référencée par hello que SAS est supprimé, ce qui est hello de toorevoke une autre façon SAS. Si vous recréez la stratégie d’accès stockée hello avec hello même nom, tous les jetons SAP de stratégie précédente de hello sont valides (si le délai d’expiration hello sur hello SAP n’a pas été). Si vous envisagez de toorevoke hello SAS, être toouse qu’un nom différent si vous recréez la stratégie d’accès hello avec un délai d’expiration Bonjour futures.

4. Hello compte qui a été utilisé toocreate hello SAS est régénérée. Régénération de la clé de hello, toutes les applications qui utilisent l’authentification de clé toofail précédente hello. Mettre à jour tous les composants toohello clé.

> [!IMPORTANT]
> Un URI de signature d’accès partagé est associé avec signature d’hello hello compte clé toocreate utilisés et hello stratégie d’accès stockée (le cas échéant). Si aucune stratégie d’accès stockée n’est spécifié, hello uniquement moyen toorevoke une signature d’accès partagé est clé de compte toochange hello.

Nous vous recommandons de toujours utiliser des stratégies d’accès stockées. Lorsque vous utilisez les stratégies stockées, vous pouvez révoquer des signatures ou étendre la date d’expiration hello en fonction des besoins. étapes Hello dans ce document utilisent toogenerate de stratégies d’accès stockée SAS.

Pour plus d’informations sur les Signatures d’accès partagé, consultez [modèle de présentation hello SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="create-a-stored-policy-and-sas-using-c"></a>Créer une stratégie stockée et une SAP à l’aide de C\#

1. Ouvrez la solution de hello dans Visual Studio.

2. Dans l’Explorateur de solutions, cliquez sur hello **SASToken** de projet et sélectionnez **propriétés**.

3. Sélectionnez **paramètres** et ajouter des valeurs pour hello suivant entrées :

   * StorageConnectionString : hello chaîne de connexion de compte de stockage hello que vous souhaitez toocreate une stratégie stockée et le SAS pour. Hello format doit être `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` où `myaccount` est le nom de hello de votre compte de stockage et `mykey` est hello clé hello compte de stockage.

   * ContainerName : hello conteneur hello compte de stockage que vous voulez accéder toorestrict à.

   * SASPolicyName : toouse de nom hello pour hello stockées toocreate de stratégie.

   * FileToUpload : hello chemin d’accès tooa fichier qui est téléchargé toohello conteneur.

4. Exécutez le projet de hello. Toohello similaire à informations suivant le texte s’affiche une fois hello SAP a été générée :

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Enregistrer le jeton de stratégie SAP hello, nom de compte de stockage et nom du conteneur. Ces valeurs sont utilisées lorsque vous associez un compte de stockage hello avec votre cluster HDInsight.

### <a name="create-a-stored-policy-and-sas-using-python"></a>Créer une stratégie stockée et une SAP à l’aide de Python

1. Ouvrir le fichier de SASToken.py hello et modifier hello valeurs suivantes :

   * stratégie\_nom : toouse de nom hello pour hello stockées toocreate de stratégie.

   * stockage\_compte\_nom : nom hello de votre compte de stockage.

   * stockage\_compte\_clé : hello clé hello compte de stockage.

   * stockage\_conteneur\_nom : hello conteneur hello compte de stockage que vous voulez accéder toorestrict à.

   * exemple\_fichier\_chemin d’accès : hello chemin d’accès tooa fichier qui est téléchargé toohello conteneur.

2. Exécutez le script de hello. Il affiche hello SAS jeton similaire toohello lors de l’achèvement du script de hello suivantes : texte :

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Enregistrer le jeton de stratégie SAP hello, nom de compte de stockage et nom du conteneur. Ces valeurs sont utilisées lorsque vous associez un compte de stockage hello avec votre cluster HDInsight.

## <a name="use-hello-sas-with-hdinsight"></a>Utilisez hello SAS avec HDInsight

Lorsque vous créez un cluster HDInsight, vous devez spécifier un compte de stockage principal, et vous pouvez éventuellement indiquer des comptes de stockage supplémentaires. Ces deux méthodes d’ajout de stockage nécessitent des comptes de stockage toohello un accès complet et les conteneurs qui sont utilisés.

toouse un conteneur tooa de Signature d’accès partagé toolimit d’accès, ajouter une entrée personnalisée de toohello **core-site** configuration de cluster de hello.

* Pour **basé sur Windows** ou **basés sur Linux** des clusters HDInsight, vous pouvez ajouter l’entrée de hello lors de la création du cluster à l’aide de PowerShell.
* Pour **basés sur Linux** clusters HDInsight, modifier la configuration de hello après la création du cluster à l’aide de Ambari.

### <a name="create-a-cluster-that-uses-hello-sas"></a>Créer un cluster qui utilise hello SAS

Un exemple de création d’un cluster HDInsight que hello utilise SAS est inclus dans hello `CreateCluster` répertoire du référentiel de hello. toouse il, hello utilisation suivant les étapes :

1. Ouvrez hello `CreateCluster\HDInsightSAS.ps1` dans un éditeur de texte et modifiez hello valeurs au début de hello du document de hello suivantes.

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    Par exemple, remplacez `'mycluster'` toohello nom du cluster de hello souhaité toocreate. les valeurs Hello SAS doivent correspondre à des valeurs hello des étapes précédentes de hello lors de la création d’un compte de stockage et un jeton SAP.

    Une fois que vous avez modifié les valeurs hello, enregistrez le fichier de hello.

2. Ouvrez une nouvelle invite Azure PowerShell. Si vous ne maîtrisez pas Azure PowerShell ou que vous ne l’avez pas installé, consultez la rubrique [Installer et configurer Azure PowerShell][powershell].

1. À partir de l’invite de commandes hello, utilisez hello suivant commande tooauthenticate tooyour abonnement Azure :

    ```powershell
    Login-AzureRmAccount
    ```

    Lorsque vous y êtes invité, connectez-vous avec le compte hello pour votre abonnement Azure.

    Si votre compte est associé à plusieurs abonnements Azure, vous devrez peut-être toouse `Select-AzureRmSubscription` tooselect hello souscription toouse.

4. À partir de l’invite de commandes hello, modifiez les répertoires toohello `CreateCluster` répertoire qui contient le fichier de HDInsightSAS.ps1 hello. Utilisez ensuite hello commande toorun hello script suivant

    ```powershell
    .\HDInsightSAS.ps1
    ```

    En tant que script de hello s’exécute, il enregistre invite de commandes de sortie toohello PowerShell lorsqu’il crée des comptes de stockage et le groupe de ressource de hello. Vous êtes invité à tooenter hello HTTP pour hello cluster HDInsight. Ce compte est utilisé toosecure cluster de toohello d’accès HTTP/s.

    Si vous créez un cluster basé sur Linux, vous êtes invité à saisir un nom et un mot de passe de compte d’utilisateur SSH. Ce compte est journal utilisé tooremotely toohello cluster.

   > [!IMPORTANT]
   > Lorsque vous y êtes invité hello HTTP/s ou SSH nom d’utilisateur et mot de passe, vous devez fournir un mot de passe qui répond aux hello suivant des critères :
   >
   > * Il doit contenir au moins 10 caractères.
   > * Il doit contenir au moins un chiffre.
   > * Il doit contenir au moins un caractère non alphanumérique.
   > * Il doit contenir au moins une lettre minuscule et une lettre majuscule.

Il prend un certain temps pour ce script toocomplete, généralement environ 15 minutes. Lorsque le script de hello se termine sans erreur, le cluster de hello a été créé.

### <a name="use-hello-sas-with-an-existing-cluster"></a>Utilisez hello SAS avec un cluster existant

Si vous disposez d’un cluster existant basés sur Linux, vous pouvez ajouter hello SAS toohello **core-site** configuration à l’aide de hello comme suit :

1. Ouvrez hello Ambari web l’interface utilisateur pour votre cluster. adresse Hello pour cette page est https://YOURCLUSTERNAME.azurehdinsight.net. Lorsque vous y êtes invité, authentifier cluster toohello à l’aide du nom de l’administrateur hello (admin) et la création de mot de passe utilisé lorsque le cluster de hello.

2. À partir de la partie gauche de l’interface utilisateur web de Ambari hello de hello, sélectionnez **HDFS** , puis sélectionnez hello **configurations** onglet milieu hello de page de hello.

3. Sélectionnez hello **avancé** onglet, puis faites défiler jusqu'à ce que vous trouviez hello **personnalisé core-site** section.

4. Développez hello **personnalisé core-site** section, puis fin toohello de défilement et sélectionnez hello **ajouter la propriété...**  lien. Valeurs suivantes de hello d’utilisation pour hello **clé** et **valeur** champs :

   * **Clé**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **Valeur**: hello SAS retourné par hello application c# ou Python, vous avez exécuté précédemment

     Remplacez **CONTAINERNAME** avec le nom du conteneur hello que vous avez utilisé avec les applications c# ou SAS hello. Remplacez **STORAGEACCOUNTNAME** par le nom de compte de stockage hello vous avez utilisé.

5. Cliquez sur hello **ajouter** toosave cette clé et valeur, puis cliquez sur hello **enregistrer** bouton les modifications de configuration toosave hello. Lorsque vous y êtes invité, ajoutez une description de modification hello (« l’ajout d’accès au stockage SAS » par exemple), puis **enregistrer**.

    Cliquez sur **OK** quand les modifications de hello ont été effectuées.

   > [!IMPORTANT]
   > Vous devez redémarrer plusieurs services avant hello modification prenne effet.

6. Dans hello Ambari interface utilisateur web, sélectionnez **HDFS** à partir de la liste hello dans hello gauche, puis sélectionnez **redémarrer tous les** de hello **Actions Service** liste sur hello droite déroulante. Lorsque vous y êtes invité, sélectionnez **Activer le mode de maintenance**, puis sélectionnez __Conform Restart All".

    Répétez ce processus pour les entrées MapReduce2 et YARN.

7. Une fois que hello sont redémarrés, sélectionnez chacune d’elles et désactiver le mode de maintenance à partir de hello **Actions Service** liste déroulante.

## <a name="test-restricted-access"></a>Tester l’accès restreint

tooverify que vous avez un accès limité, hello utilisez méthodes suivantes :

* Pour **basé sur Windows** clusters HDInsight, utiliser le cluster de toohello tooconnect de bureau à distance. Pour plus d’informations, consultez [se connecter à l’aide du protocole RDP de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

    Une fois connecté, utilisez hello **Hadoop de ligne de commande** icône sur tooopen de bureau hello une invite de commandes.

* Pour **basés sur Linux** clusters HDInsight, utiliser SSH tooconnect toohello cluster. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

Une fois connecté toohello cluster, utilisez hello suivant tooverify étapes que vous pouvez uniquement en lecture et la liste des éléments sur le compte de stockage SAS hello :

1. contenu de hello toolist du conteneur de hello, utilisez hello de commande suivante à partir de l’invite de commandes hello : 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    Remplacez **SASCONTAINER** avec nom hello du conteneur hello créé pour hello compte de stockage SAS. Remplacez **SASACCOUNTNAME** avec nom hello hello du compte de stockage utilisé pour hello SAS.

    liste de Hello inclut fichier hello téléchargé lorsque le conteneur de hello et associations de sécurité ont été créées.

2. Utilisez hello suivant tooverify de commande que vous pouvez lire le contenu de hello du fichier de hello. Remplacez hello **SASCONTAINER** et **SASACCOUNTNAME** comme à l’étape précédente de hello. Remplacez **nom de fichier** avec nom hello du fichier hello affiché dans la commande précédente hello :

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    Cette commande répertorie le contenu hello du fichier de hello.

3. Utilisez hello suivant le système de fichiers local toohello de fichier de commandes toodownload hello :

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    Cette commande téléchargements hello fichier tooa fichier local nommé **testfile.txt**.

4. Suivant de hello utilisez commande tooupload hello fichier local tooa nouveau fichier nommé **testupload.txt** sur hello stockage SAS :

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    Vous recevez un toohello similaire message suit texte :

        put: java.io.IOException

    Cette erreur se produit, car l’emplacement de stockage hello est lecture + liste uniquement. Utilisez hello suivant des données de commande tooput hello de stockage par défaut de hello pour cluster hello, qui est accessible en écriture :

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    Cette fois-ci, hello opération doit se terminer avec succès.

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="a-task-was-canceled"></a>Une tâche a été annulée

**Symptômes**: lorsque vous créez un cluster à l’aide du script PowerShell de hello, hello message d’erreur suivant peut s’afficher :

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**Cause**: cette erreur peut se produire si vous utilisez un mot de passe pour l’utilisateur d’administration/HTTP hello pour hello cluster ou (pour les clusters basés sur Linux) utilisateur SSH de hello.

**Résolution**: utiliser un mot de passe qui répond aux hello suivant des critères :

* Il doit contenir au moins 10 caractères.
* Il doit contenir au moins un chiffre.
* Il doit contenir au moins un caractère non alphanumérique.
* Il doit contenir au moins une lettre minuscule et une lettre majuscule.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment tooadd un stockage à accès limité tooyour cluster HDInsight, des informations autres toowork manières avec des données sur votre cluster :

* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
