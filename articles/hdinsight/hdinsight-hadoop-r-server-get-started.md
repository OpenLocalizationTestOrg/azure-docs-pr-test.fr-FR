---
title: aaaGet main R Server sur HDInsight - Azure | Documents Microsoft
description: "Découvrez comment toocreate un Apache nouvelles sur le cluster HDInsight qui inclut le serveur R et envoi d’un script R sur le cluster de hello."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>Commencer à utiliser R Server sur HDInsight

HDInsight inclut une toobe d’option R Server intégré à votre cluster HDInsight. Cette option permet à des scripts R toorun distribué des calculs toouse Spark et MapReduce. Dans ce document, vous découvrez comment toocreate un serveur R sur le cluster HDInsight, puis sur R script qui montre comment utiliser Spark sur distributed calculs de R.


## <a name="prerequisites"></a>Composants requis

* **Abonnement Azure** : avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure. Accédez toohello article [gratuite obtenir Microsoft Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) pour plus d’informations.
* **Un client Secure Shell (SSH)**: SSH un client est utilisé tooremotely connecter toohello HDInsight cluster et exécuter des commandes directement sur le cluster de hello. Pour en savoir plus, consultez [Se connecter à HDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md).
* **Clés SSH (facultatifs)**: vous pouvez sécuriser hello SSH compte utilisé tooconnect toohello cluster à l’aide d’un mot de passe ou une clé publique. À l’aide d’un mot de passe est plus facile et permet de vous tooget démarré sans avoir toocreate une paire de clés publique/privée. Toutefois, il est plus sûr d’utiliser une clé.

> [!NOTE]
> étapes de Hello dans ce document supposent que vous utilisez un mot de passe.


## <a name="automated-cluster-creation"></a>Création de cluster automatisée

Vous pouvez automatiser la création de hello de HDInsight R Servers à l’aide d’Azure Resource Manager modèles, hello SDK et PowerShell.

* toocreate serveur R à l’aide d’un modèle de gestion des ressources Azure, consultez [déployer un cluster HDInsight de serveur R](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).
* toocreate un serveur R à l’aide de hello .NET SDK, consultez [créer des clusters basés sur Linux dans HDInsight à l’aide de hello du SDK .NET.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* toodeploy R Server à l’aide de powershell, consultez l’article de hello sur [création d’un serveur de R dans HDInsight avec PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>Créer le cluster hello à l’aide de hello portail Azure

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Sélectionnez **NOUVEAU** -> **Intelligence et analyse**, -> **HDInsight**.

    ![Image de la création d’un cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. Bonjour **création rapide** expérience, entrez un nom pour le cluster de hello Bonjour **nom de Cluster** champ. Si vous avez plusieurs abonnements Azure, utilisez hello **abonnement** entrée tooselect hello une souhaité toouse.

    ![Sélections de nom et d’abonnement de cluster](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. Sélectionnez **Cluster type** tooopen hello **configuration de Cluster** panneau. Sur hello **Configuration de Cluster** panneau, sélectionnez hello options suivantes :

    * **Type de cluster** : R Server
    * **Version**: version select hello de tooinstall R Server sur le cluster de hello. version de Hello actuellement disponible est ***R Server 9.1 (HDI 3.6)***. Notes de publication pour les versions disponibles de hello du serveur de R sont disponibles [ici](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).
    * **Édition de communauté R Studio pour R Server**: cet IDE basé sur le navigateur est installé par défaut sur le nœud de périmètre hello. Si vous préférez toonot est installé, puis désactivez la case à cocher hello. Si vous choisissez toohave il installé, les URL de hello pour accéder aux hello connexion RStudio Server se trouve sur un panneau de l’application de portail pour votre cluster, une fois qu’il est créé.
    * Laissez des autres options hello aux valeurs par défaut de hello et utiliser hello **sélectionnez** toosave hello cluster type de bouton.

        ![Capture d’écran du panneau Type de cluster](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. Saisissez un **nom de connexion au cluster** et un **mot de passe de connexion au cluster**.

    Spécifiez un **nom d’utilisateur SSH**. SSH est utilisé tooremotely se connecter à l’aide du cluster toohello un **Secure Shell (SSH)** client. Vous pouvez spécifier utilisateur SSH de hello dans cette boîte de dialogue ou après la création du cluster hello (dans l’onglet de Configuration hello pour le cluster de hello). R Server est configuré tooexpect un **nom d’utilisateur SSH** de « UtilisateurDistant ».  **Si vous utilisez un nom d’utilisateur différent, vous devez effectuer une étape supplémentaire après la création du cluster hello.**

    Laissez hello cases pour **utiliser le même mot de passe en tant que compte de connexion de cluster** toouse **mot de passe** comme hello l’authentification de type, sauf si vous préférez utiliser une clé publique.  Vous avez besoin d’une paire de clés publique/privée de tooaccess R Server sur le cluster hello via un client distant, comme par exemple, RTV, RStudio ou un autre environnement IDE de bureau. Si vous installez hello édition community de RStudio serveur, vous devez toochoose un mot de passe SSH.     

    toocreate et utilisez une paire de clés publique/privée, décochez la case **utiliser le même mot de passe en tant que compte de connexion de cluster** , puis sélectionnez **clé publique** et procédez comme suit. Ces instructions supposent que Cygwin avec ssh-keygen ou équivalent est installé.

    * Générer une paire de clés publique/privée à partir de l’invite de commandes hello sur votre ordinateur portable :

        ssh-keygen -t rsa -b 2048

    * Suivez hello, tooname demander un fichier de clé, puis entrez une phrase secrète pour une sécurité accrue. Votre écran doit ressembler à quelque chose comme hello suivant l’image :

        ![Ligne de commande SSH dans Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * Cette commande crée un fichier de clé privée et d’un fichier de clé publique sous hello nom < nom de la clé privée > .pub, par exemple furiosa et furiosa.pub.

        ![SSH dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * Puis spécifiez le fichier de clé publique de hello (&#42;. pub) lors de l’affectation HDI informations d’identification du cluster et enfin confirmer votre groupe de ressources, la région et sélectionnez **suivant**.

        ![Panneau Informations d’identification](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * Modifier les autorisations sur le fichier de clé privée hello sur votre ordinateur portable :

        chmod 600 <nom-fichier-clé-privée>

   * Utiliser le fichier de clé privée hello avec SSH pour la connexion à distance :

        ssh –i <private-key-filename> remoteuser@<hostname public ip>

      Ou bien, en tant que définition de votre Hadoop Spark hello de partie de contexte de calcul pour R Server sur le client de hello. Consultez hello **à l’aide de Microsoft R Server comme un Hadoop Client** dans la sous-section [créer un contexte de calcul pour Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).

6. Création rapide de Hello vous passe toohello **stockage** compte de stockage panneau tooselect hello toobe de paramètres utilisé pour l’emplacement principal de hello Hello système utilisé par le cluster de hello du fichier HDFS. Sélectionnez un compte de stockage Azure nouveau ou existant ou un compte de stockage Data Lake existant.

    - Si vous sélectionnez un compte de stockage Azure, un compte de stockage existant est sélectionné en choisissant **sélectionner un compte de stockage** , puis en sélectionnant le compte de votre choix hello. Créer un nouveau compte à l’aide de hello **créer un nouveau** lien Bonjour **sélectionner un compte de stockage** section.

      > [!NOTE]
      > Si vous sélectionnez **nouveau** vous devez entrer un nom pour le nouveau compte de stockage hello. Une coche verte s’affiche si le nom de hello est accepté.

      Hello **conteneur par défaut** nom toohello de valeurs par défaut du cluster de hello. Laissez cette valeur par défaut en tant que valeur de hello.

      Si une nouvelle option de compte de stockage a été sélectionnée une invite de commandes tooselect **emplacement** est donné tooselect le toocreate région hello compte de stockage.  

         ![Panneau Source de données](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > Sélectionner l’emplacement de source de données par défaut hello hello définit également l’emplacement hello du cluster HDInsight de hello. source de données par défaut et le cluster Hello doit être Bonjour même région.

    - Si vous voulez toouse un Data Lake Store existant, puis sélectionnez hello toouse de compte de stockage ADLS et ajouter un cluster de hello *ajouter* magasin toohello d’identité tooyour cluster tooallow accès. Pour plus d’informations sur ce processus, consultez [Créer un cluster HDInsight avec Data Lake Store à l’aide du portail Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).

    Hello d’utilisation **sélectionnez** configuration de source de données bouton toosave hello.


7. Hello **Résumé** panneau affiche ensuite toovalidate tous vos paramètres. Ici, vous pouvez modifier votre **taille de Cluster** toomodify hello du nombre de serveurs de votre cluster et spécifiez **actions de Script** vous souhaitez toorun. Sauf si vous savez que vous avez besoin d’un cluster plus grand, conservez hello du numéro de nœuds de travail par défaut hello `4`. Hello estimation de coût de cluster de hello est indiqué dans le panneau de hello.

    ![Résumé du cluster](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > Si nécessaire, vous pouvez redimensionner votre cluster ultérieurement via hello portail (**Cluster** -> **paramètres** -> **échelle Cluster**) tooincrease ou diminuer le nombre hello de nœuds worker.  Ce redimensionnement peut être utile pour ralenti cluster hello inutilisés vers le bas, ou ajouté des besoins en capacité toomeet hello de plus grandes tâches.
   >
   >

   Certains tookeep facteurs à l’esprit lors du redimensionnement de votre cluster, des nœuds de données hello et nœud de périmètre hello sont les suivantes :  

   * performances Hello des analyses de R Server distribuées sur Spark est nombre toohello proportionnel de nœuds worker lorsque les données de salutation sont grandes.  

   * performances Hello des analyses de R Server est linéaire taille hello de données en cours d’analyse. Par exemple :  

     * Pour les données de petite toomodest, les performances sont meilleures lors de l’analyse dans un contexte de calcul local sur le nœud de périmètre hello.  Pour plus d’informations sur les scénarios de hello sous lequel hello local et Spark contextes de calcul sont satisfaisants, consultez les options de contexte de calcul pour R Server sur HDInsight.<br>
     * Si vous connectez-vous au nœud de périmètre toohello et exécutez votre script R, puis toutes mais hello rx-fonctions ScaleR sont exécutées <strong>localement</strong> sur le nœud de périmètre hello. Par conséquent, hello mémoire et nombre de cœurs de nœud de périmètre hello doit être dimensionné en conséquence. Hello que même règle s’applique si vous utilisez R Server sur HDI comme contexte de calcul à distance à partir de votre ordinateur portable.

     ![Panneau Niveaux de tarification du nœud](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     Hello d’utilisation **sélectionnez** nœud de hello bouton toosave configuration de la tarification.

   Il existe également un lien permettant de **télécharger le modèle et les paramètres**. Cliquez sur ce lien toodisplay les scripts qui peuvent être tooautomate utilisé hello la création d’un cluster avec la configuration sélectionnée de hello. Ces scripts sont également disponibles à partir de hello entrée de portail Azure pour votre cluster une fois qu’elle a été créée.

   > [!NOTE]
   > Il prend un certain temps pour hello toobe de cluster créé, généralement environ 20 minutes. Utilisez hello vignette sur hello tableau d’accueil ou hello **Notifications** entrée sur hello à gauche de hello page toocheck sur le processus de création de hello.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>Se connecter tooRStudio Server

Si vous avez choisi tooinclude édition community de RStudio serveur dans votre installation, vous pouvez accéder à connexion de RStudio hello via deux méthodes différentes.

1. Accédez toohello suivant URL (où **CLUSTERNAME** hello désigne cluster hello que vous avez créé) :

    https://**CLUSTERNAME**.azurehdinsight.net/rstudio/

2. Ouvrir l’entrée de hello pour votre cluster Bonjour portail Azure, sélectionnez hello **tableaux de bord de serveur R** lien rapide, puis en sélectionnant hello **tableau de bord R Studio**:

     ![Tableau de bord accès hello R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Tableau de bord accès hello R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > Quelle que soit la méthode hello utilisée, hello première fois que vous vous connectez vous devez tooauthenticate à deux reprises.  À la première authentification de hello, fournir hello *nom d’utilisateur administrateur de cluster* et *mot de passe*. À l’invite de deuxième hello, fournir hello *SSH userid* et *mot de passe*. Fichier journal suivante ins nécessitent uniquement hello *mot de passe SSH* et *userid*.

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Connecter le nœud de périmètre toohello R Server

Connecter le nœud du bord tooR serveur du cluster HDInsight de hello à l’aide de SSH avec la commande hello :

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> Vous pouvez trouver hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` adresse Bonjour portail Azure en sélectionnant votre cluster puis **tous les paramètres** -> **applications** -> **RServer**. Cette opération affiche hello les informations de point de terminaison SSH pour le nœud de périmètre hello.
>
> ![Image de hello point de terminaison SSH pour le nœud de périmètre hello](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

Si vous avez utilisé un toosecure de mot de passe de votre compte d’utilisateur SSH, vous êtes invité à tooenter il. Si vous avez utilisé une clé publique, vous avez peut-être toouse hello `-i` paramètre toospecify hello la clé privée correspondante. Par exemple :

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Pour plus d’informations, consultez [connecter tooHDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

Une fois connecté, vous accédez à une invite de commandes suivant de toohello similaire :

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>Autoriser plusieurs utilisateurs simultanés

Vous pouvez activer plusieurs utilisateurs simultanément en ajoutant de nouveaux utilisateurs pour le nœud de périmètre hello sur quel hello RStudio Communauté version s’exécute.

Lorsque vous créez un cluster HDInsight, vous devez fournir deux utilisateurs, un utilisateur HTTP et un utilisateur SSH :

![Utilisateur simultané n° 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **Nom d’utilisateur de cluster**: un utilisateur HTTP pour l’authentification via la passerelle HDInsight hello qui est utilisé tooprotect hello HDInsight de clusters que vous avez créé. Cet utilisateur HTTP est utilisé tooaccess hello Ambari UI, l’interface utilisateur des fils, ainsi que les autres composants d’interface utilisateur.
- **Nom d’utilisateur de Shell (SSH) sécurisée**: un cluster de hello SSH utilisateur tooaccess via le shell sécurisé. Cet utilisateur est un utilisateur de hello système Linux pour tous les nœuds de bord, les nœuds de travail et les nœuds principaux hello. Vous pouvez donc utiliser shell sécurisé tooaccess un des nœuds de hello dans un cluster à distance.

version de R Studio Server Community Hello utilisée Bonjour Microsoft R Server sur un cluster de type HDInsight accepte uniquement le nom d’utilisateur Linux et mot de passe comme mécanisme de connexion. Elle ne prend pas en charge le passage de jetons. Par conséquent, si vous avez créé un nouveau cluster et que vous souhaitez toouse R Studio tooaccess, vous devez toolog dans deux fois.

- Commencez par vous connecter à l’aide des informations d’identification utilisateur de hello HTTP via hello HDInsight passerelle : 

    ![Utilisateur simultané 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- Puis utilisez hello SSH utilisateur informations d’identification toolog dans tooRStudio :
  
    ![Utilisateur simultané 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

Actuellement, on ne peut créer qu’un seul compte d’utilisateur SSH lors de l’approvisionnement d’un cluster HDInsight. Afin de clusters de plusieurs utilisateurs tooaccess Microsoft R Server sur HDInsight tooenable, nous devons toocreate des utilisateurs supplémentaires dans hello système Linux.

Étant donné que RStudio Server Community est en cours d’exécution sur le nœud de bord du cluster hello, il existe plusieurs étapes :

1. Utilisez hello créé SSH utilisateur toolog toohello bord nœud
2. Ajouter d’autres utilisateurs Linux dans le nœud de périmètre
3. Utiliser la version Community de RStudio avec créés par l’utilisateur hello

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>Étape 1 : Utiliser hello créé SSH utilisateur toolog dans le nœud de périmètre toohello

Télécharger n’importe quel outil SSH (tel que Putty) et utiliser hello toolog utilisateur SSH existant dans. Puis suivez les instructions de hello fournies dans [connecter tooHDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello nœud de périmètre. adresse du nœud bord Hello pour R Server sur le cluster HDInsight est : *clustername-ed-ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>Étape n° 2 : Ajouter d’autres utilisateurs Linux dans le nœud de périmètre

tooadd un nœud de périmètre toohello utilisateur, exécutez les commandes de hello :

    sudo useradd yournewusername -m
    sudo passwd yourusername

Vous devez voir hello retournés des éléments suivants : 

![Utilisateur simultané 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

Lorsque vous y êtes invité pour « mot de passe actuel Kerberos : », appuyez simplement sur **entrée** tooignore il. Hello `-m` option `useradd` commande indique que le système de hello créera un dossier de base pour l’utilisateur hello, qui est requis pour la version de communauté de RStudio.


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>Étape 3 : Version utilisez RStudio Communauté créés par l’utilisateur hello

Utilisez hello créés par l’utilisateur toolog dans tooRStudio :

![Utilisateur simultané 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

Notez que RStudio indique que vous utilisez le nouvel utilisateur de hello (ici, par exemple, *sshuser6*) toolog dans un cluster de hello : 

![Utilisateur simultané 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

Vous pouvez également vous connecter à l’aide des informations d’identification d’origine de hello (par défaut, il est *sshuser*) simultanément à partir d’une autre fenêtre de navigateur.

Vous pouvez soumettre un travail à l’aide des fonctions ScaleR. Voici un exemple de hello commandes utilisées toorun une tâche :

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


Notez que les travaux hello soumis sont sous différents noms d’utilisateur dans l’interface utilisateur des fils :

![Utilisateur simultané 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

Notez également que hello nouvellement ajouté utilisateurs n’ont pas des droits racines dans le système Linux, mais ils hello même accéder à des fichiers hello tooall hello HDFS et WASB le stockage étendu.


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>Utilisez la console hello R

1. À partir de la session SSH hello, utilisez hello suivant la console de commande toostart hello R :  

        R

2. Vous devez voir s’afficher sortie similaire toohello :
    
    R version 3.2.2 (2015-08-14)--« Sécurité incendie » Copyright (C) 2015 hello R Foundation pour une plate-forme statistique : x86_64-pc-linux-gnu (64 bits)

    R est un logiciel gratuit et est fourni SANS AUCUNE GARANTIE.
    Vous êtes tooredistribute Bienvenue sous certaines conditions.
    Tapez ’license()’ ou ’licence()’ pour obtenir des informations relatives à la distribution.

    Prise en charge du langage naturel, mais exécution dans un paramètre régional anglais

    R est un projet de collaboration avec de nombreux contributeurs.
    Pour plus d’informations et 'citation()' de type 'contributors()' sur comment toocite R ou R packages dans les publications.

    Tapez 'demo()' pour certaines des démonstrations, les « help() » de l’aide en ligne ou 'help.start()' pour un toohelp d’interface de navigateur HTML.
    Tapez 'q()' tooquit R.

    Microsoft R Server version 8.0 : une distribution avancée des packages Microsoft R Copyright (C) 2016 Microsoft Corporation

    Tapez ’readme()’ pour consulter les notes de publication.
    >

3. À partir de hello `>` invite de commandes, vous pouvez entrer le code R. Serveur R inclut des packages qui vous permettent de tooeasily interagissent avec Hadoop et exécuter des calculs distribuées. Par exemple, utilisez hello suivant racine de hello tooview commande hello par défaut du système de fichiers pour le cluster HDInsight de hello :

    rxHadoopListFiles("/")

4. Vous pouvez également utiliser l’adressage de hello WASB style.

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>À l’aide de R Server sur HDI à partir d’une instance distante de Microsoft R serveur ou Microsoft R Client

Il est possible tooset contexte de calcul HDI Hadoop Spark accès toohello à partir d’une instance distante de Microsoft R Server ou Microsoft R Client en cours d’exécution sur le bureau ou portable. Consultez **à l’aide de Microsoft R Server comme un Hadoop Client** sous-section Bonjour [création d’un contexte de calcul pour Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md). toodo, vous pouvez donc hello toospecify options suivantes lors de la définition du contexte de calcul hello RxSpark sur votre ordinateur portable : hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches et sshProfileScript. Par exemple :


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>Utiliser un contexte de calcul

Un contexte de calcul vous permet de toocontrol si le calcul est effectué localement sur le nœud de périmètre hello ou répartis entre les nœuds hello dans le cluster HDInsight de hello.

1. À partir de RStudio hello R la console serveur ou (dans une session SSH), utilisez hello suivant des données d’exemple de code tooload dans le stockage par défaut de hello pour HDInsight :

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. Ensuite, créez des informations de données et définir les deux sources de données afin que nous pouvons utiliser les données de salutation.

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. Nous allons exécuter une régression logistique sur les données hello à l’aide du contexte de calcul local hello.

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    Vous devez voir la sortie qui se termine par toohello similaire de lignes suivant :

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. Ensuite, nous allons exécuter hello même régression logistique à l’aide du contexte de Spark hello. contexte de Spark Hello distribue hello de traitement sur tous les nœuds de travail hello dans le cluster HDInsight de hello.

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > Vous pouvez également utiliser MapReduce toodistribute calcul entre les nœuds de cluster. Pour plus d’informations sur le contexte de calcul, consultez [Options de contexte de calcul pour R Server sur HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).


## <a name="distribute-r-code-toomultiple-nodes"></a>Distribuer des nœuds de toomultiple code R

Avec R Server, vous pouvez facilement utiliser le code R existant et l’exécuter sur plusieurs nœuds de cluster de hello à l’aide de `rxExec`. Cette fonction est utile lors d’un balayage paramétrique ou lorsque vous effectuez des simulations. Hello de code suivant est un exemple de procédure toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

Si vous utilisez encore hello Spark ou MapReduce contexte, cette commande renvoie ce code hello valeur nodename de hello pour les nœuds de travail hello `(Sys.info()["nodename"])` s’exécute. Par exemple, sur un cluster à quatre nœuds, vous vous attendez tooreceive sortie similaire toohello suivantes :

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a>Accès aux données dans Hive et Parquet

Une fonctionnalité disponible dans R Server 9.1 permet toodata un accès direct dans la ruche et Parquet pour une utilisation par les fonctions ScaleR dans le contexte de calcul hello Spark. Ces fonctionnalités sont disponibles via les nouvelles données source fonctions ScaleR appelées RxHiveData et RxParquetData qui fonctionnent à l’aide de données de tooload Spark SQL directement dans une trame de données pour l’analyse par ScaleR Spark.  

Hello suivant code fournit un exemple de code sur l’utilisation de nouvelles fonctions de hello :

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


Pour des informations supplémentaires sur l’utilisation de ces nouvelles fonctions, consultez hello aide en ligne de R Server via l’utilisation de hello `?RxHivedata` et `?RxParquetData` commandes.  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Installer des packages R supplémentaires sur le nœud de périmètre hello

Si vous souhaitez que tooinstall des packages R supplémentaires sur le nœud de périmètre hello, vous pouvez utiliser `install.packages()` directement depuis hello console R lorsque toohello connecté bord nœud via SSH. Toutefois, si vous avez besoin des packages R tooinstall sur les nœuds de travail hello du cluster de hello, vous devez utiliser une Action de Script.

Actions de script sont des scripts Bash toomake utilisé configuration modifications toohello HDInsight cluster ou tooinstall logiciels supplémentaires, telles que les packages R supplémentaires. les packages supplémentaires tooinstall à l’aide d’une Action de Script, utilisez hello comme suit :

> [!IMPORTANT]
> À l’aide des packages R supplémentaires Actions de Script tooinstall utilisable uniquement après que hello cluster a été créé. N’utilisez pas cette procédure pendant la création du cluster, comme le script de hello s’appuie sur le serveur R en cours complètement installé et configuré.
>
>

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre serveur R sur le cluster HDInsight.

2. À partir de hello **paramètres** panneau, sélectionnez **Actions de Script** , puis **soumettre de nouvelles** toosubmit une nouvelle Action de Script.

   ![Image du panneau Actions de script](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. À partir de hello **envoyer l’action de script** panneau, fournir hello informations suivantes :

   * **Nom**: un nom convivial de la nommer tooidentify ce script

   * **URI de script bash** : `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **En-tête** : cet élément doit être **décoché**.

   * **Worker** : cet élément doit être **coché**.

   * **Nœuds de périmètre** : cet élément doit être **décoché**.

   * **Zookeeper** : cet élément doit être **décoché**.

   * **Paramètres**: hello R packages toobe installé. Par exemple, `bitops stringr arules`

   * **Conservez cette action de script...** : cet élément doit être **coché**.  

   > [!NOTE]
   > 1. Par défaut, tous les packages R sont installés à partir d’un instantané du référentiel de Microsoft MRAN hello cohérent avec la version de hello du serveur R qui a été installé. Si vous souhaitez tooinstall les versions plus récentes des packages, il est certains risques d’incompatibilité. Ce type d’installation est toutefois possible en spécifiant `useCRAN` comme hello premier élément du package de hello répertorier, par exemple `useCRAN bitops, stringr, arules`.  
   > 2. Certains packages R nécessitent des bibliothèques de système Linux supplémentaires. Pour plus de commodité, nous avons préinstallé dépendances hello requis par hello top 100 packages R plus populaires. Toutefois, si vous installez le hello R ou nécessite des bibliothèques au-delà de ces vous devez télécharger le script de base hello utilisé ici et ajouter des étapes tooinstall hello système bibliothèques. Vous devez ensuite téléchargement hello modifié script tooa public blob du conteneur dans le stockage Azure et utiliser des packages de hello modifié script tooinstall hello.
   >    Pour plus d’informations sur le développement d’actions de script, consultez la section [Développer des actions de script](hdinsight-hadoop-script-actions-linux.md).  
   >
   >

   ![Ajout d’une action de script](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. Sélectionnez **créer** script de hello toorun. Une fois que l’achèvement du script de hello, hello R sont disponibles sur tous les nœuds de travail.


## <a name="using-microsoft-r-server-operationalization"></a>Utilisation de l’opérationnalisation de Microsoft R Server

Lors de la modélisation des données est terminée, vous pouvez tiens prédictions toomake du modèle hello. tooconfigure pour à l’Opérationnalisation Microsoft R Server, effectuez hello comme suit :

Tout d’abord, ssh dans le nœud de périmètre hello. Par exemple, 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Une fois à l’aide de ssh, remplacez le répertoire pour la version appropriée de hello et sudo hello dotnet dll : 

- Pour Microsoft R Server 9.1 :

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- Pour Microsoft R Server 9.0 :

    cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

à l’Opérationnalisation tooconfigure Microsoft R Server avec une configuration d’une case hello suivant :

1. Sélectionnez « Configure R Server for Operationalization » (Configurer R Server pour l’opérationnalisation).
2. Sélectionnez « A. One-box (web + compute nodes) » (Solution complète + nœuds de calcul).
3. Entrez un mot de passe hello **admin** utilisateur

![opérationnalisation complète](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

Vous pouvez éventuellement effectuer les vérifications de diagnostic en exécutant un test de diagnostic, comme suit :

1. Sélectionnez « 6. Exécuter des tests de diagnostic ».
2. Sélectionnez « A. Configuration de test ».
3. Entrez le nom d’utilisateur = « admin » et le mot de passe de l’étape de configuration précédente.
4. Confirmez l’intégrité globale = pass.
5. Hello quitter utilitaire d’administration
6. Quittez SSH.

![Diagnostics pour l’opérationnalisation](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**Retards importants lors de l’utilisation d’un service web sur Spark**
>
>Si vous rencontrez un retard lors de la tentative de tooconsume un service web créé avec des fonctions mrsdeploy dans un contexte de calcul Spark, vous devrez peut-être tooadd certains dossiers manquants. Hello application de Spark appartient utilisateur tooa appelé '*rserve2*' chaque fois qu’il est appelé à partir d’un service web à l’aide des fonctions de mrsdeploy. toowork résoudre ce problème :

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


À ce stade, la configuration à l’Opérationnalisation hello est terminée. Vous pouvez désormais utiliser hello 'mrsdeploy' du package sur votre toohello de tooconnect RClient à l’Opérationnalisation sur le nœud de périmètre et commencer à utiliser ses fonctionnalités comme [l’exécution à distance](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) et [services web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette). Selon que votre cluster est configuré sur un réseau virtuel ou non, vous devrez peut-être tooset de port vers l’avant tunneling via la connexion SSH. Hello sections suivantes expliquent comment tooset de ce tunnel.

### <a name="rserver-cluster-on-virtual-network"></a>Cluster RServer sur un réseau virtuel

Assurez-vous que vous autorisez le trafic via le nœud de port 12800 toohello edge. De cette façon, vous pouvez utiliser la fonctionnalité à l’Opérationnalisation hello bord nœuds tooconnect toohello.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


Si hello `remoteLogin()` ne peut pas se connecter toohello de nœud de périmètre, mais vous pouvez le nœud de périmètre toohello SSH, vous devez tooverify si hello règle tooallow le trafic sur le port 12800 a été défini correctement ou non. Si vous continuez le problème de hello tooface, vous pouvez contourner il en configurant le transfert port le tunneling forcé via SSH. Pour obtenir des instructions, consultez hello suivant la section.

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>Cluster RServer non configuré sur un réseau virtuel

Si votre cluster n’est pas configuré sur un réseau virtuel ou si vous rencontrez des problèmes de connectivité via un réseau virtuel, vous pouvez utiliser le tunneling de réacheminement du port SSH :

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Vous pouvez également le configurer sur PuTTY.

![connexion SSH PuTTY](./media/hdinsight-hadoop-r-server-get-started/putty.png)

Une fois votre session SSH est active, le trafic de hello du port de votre ordinateur 12800 est transféré le port du nœud toohello bord 12800 via une session SSH. Vérifiez que vous utilisez `127.0.0.1:12800` dans votre méthode `remoteLogin()`. Il se connecte à l’Opérationnalisation du nœud toohello bord via le réacheminement de port.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Comment tooscale à l’Opérationnalisation Microsoft R Server les nœuds de calcul sur les nœuds de travail HDInsight

### <a name="decommission-hello-worker-nodes"></a>Mettre hors service ou les nœuds worker hello

Microsoft R Server n’est actuellement pas géré par YARN. Si les nœuds de travail hello ne sont pas retirés, hello fils le Gestionnaire de ressources ne fonctionnera pas comme prévu, car elle ne sera pas connaissance des ressources hello est pris en charge par le serveur de hello. Dans l’ordre tooavoid cette situation, nous vous recommandons de désaffectation des nœuds de travail hello avant d’étendre les nœuds de calcul hello.

Nœuds de travail toodecommissioning comme suit :

* Ouvrez une session dans la console du cluster tooHDI Ambari, puis cliquez sur l’onglet « hosts »
* Sélectionnez les nœuds de travail (toobe désactivé), cliquez sur « Actions » > « Sélectionné les ordinateurs hôtes » > « Hosts » > cliquez sur « Activer le Mode de Maintenance ON ». Par exemple, Bonjour suivant l’image, nous avons sélectionné toodecommission wn3 et wn4.  

   ![Désactiver les nœuds Worker](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* Sélectionnez **Actions** > **Hôtes sélectionnés** > **DataNodes** > cliquez sur **Désactiver**
* Sélectionnez **Actions** > **Hôtes sélectionnés** > **NodeManagers** > cliquez sur **Désactiver**
* Sélectionnez **Actions** > **Hôtes sélectionnés** > **DataNodes** > cliquez sur **Arrêter**
* Sélectionnez **Actions** > **Hôtes sélectionnés** > **NodeManagers** > cliquez sur **Arrêter**
* Sélectionnez **Actions** > **Hôtes sélectionnés** > **Hôtes** > cliquez sur **Stop All Components** (Arrêter tous les composants)
* Désélectionnez les nœuds de travail hello et sélectionnez les nœuds principaux hello
* Sélectionnez **Actions** > **Hôtes sélectionnés** > **Hôtes** > **Restart All Components** (Redémarrer tous les composants)

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>Configurer les nœuds de calcul sur chaque nœud Worker désactivé

1. Utilisez SSH dans chaque nœud Worker désactivé.
2. Exécutez l’utilitaire d’administration à l’aide de `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.
3. Entrez « 1 » tooselect option « Configurer R Server pour à l’Opérationnalisation ».
4. Entrez l’option « c » tooselect C. » Nœud de calcul ». Cela configure le nœud de calcul hello sur le nœud de travail hello.
5. Hello de sortie utilitaire d’administration.

### <a name="add-compute-nodes-details-on-web-node"></a>Ajouter des détails sur les nœuds de calcul sur le nœud web

Après ont configuré tous les nœuds de travail retirés toorun nœud de calcul, revenez sur le nœud de périmètre hello et ajouter des adresses IP des nœuds de travail retirés dans la configuration du nœud hello Microsoft R Server web :

* SSH dans le nœud de périmètre hello.
* Exécutez `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.
* Recherchez hello section de « URI » et ajoutez IP du nœud de travail et les détails du port.

    ![Ligne de commande Désactiver les nœuds Worker](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).


## <a name="next-steps"></a>Étapes suivantes

Maintenant, vous devez comprendre comment toocreate un nouveau cluster HDInsight qui inclut les principes élémentaires de R Server et hello hello de l’utilisation de hello console R à partir d’une session SSH. Hello rubriques suivantes expliquent autres méthodes de gestion et l’utilisation de R Server sur HDInsight :

* [Ajouter RStudio Server tooHDInsight (si ne pas installé lors de la création du cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Options de contexte de calcul pour R Server sur HDInsight (version préliminaire)](hdinsight-hadoop-r-server-compute-contexts.md)
* [Options d’Azure Storage pour R Server sur HDInsight](hdinsight-hadoop-r-server-storage.md)
