---
title: aaaQuery ruche via le pilote JDBC de hello - Azure HDInsight | Documents Microsoft
description: "Utiliser le pilote JDBC hello à partir d’un tooHadoop de requêtes Java application toosubmit Hive dans HDInsight. Se connecter par programmation et hello non SQL client."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="72e81-104">Une requête Hive via le pilote JDBC de hello dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="72e81-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="72e81-105">Découvrez comment le pilote JDBC toouse hello un toosubmit d’application Java ruche interroge tooHadoop dans Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="72e81-106">informations Hello dans ce document montre comment tooconnect par programmation et à partir de hello HIPPOCAMPIQUES SQL client.</span><span class="sxs-lookup"><span data-stu-id="72e81-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="72e81-107">Pour plus d’informations sur hello Hive une Interface de JDBC, consultez [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="72e81-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72e81-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="72e81-108">Prerequisites</span></span>

* <span data-ttu-id="72e81-109">Un cluster Hadoop sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="72e81-110">Les clusters basés tant sur Linux que sur Windows fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="72e81-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="72e81-111">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="72e81-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="72e81-112">Pour plus d’informations, reportez-vous à la rubrique [Déclassement de HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="72e81-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="72e81-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="72e81-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="72e81-114">SQuirreL est une application cliente JDBC.</span><span class="sxs-lookup"><span data-stu-id="72e81-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="72e81-115">Hello [Kit de développement Java (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="72e81-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="72e81-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="72e81-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="72e81-117">Maven est un projet de build système pour les projets Java qui est utilisé par le projet hello associé à cet article.</span><span class="sxs-lookup"><span data-stu-id="72e81-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="72e81-118">Chaîne de connexion JDBC</span><span class="sxs-lookup"><span data-stu-id="72e81-118">JDBC connection string</span></span>

<span data-ttu-id="72e81-119">Cluster de HDInsight de tooan de connexions JDBC sur Azure sont effectuées sur 443 et le trafic de hello est sécurisé à l’aide de SSL.</span><span class="sxs-lookup"><span data-stu-id="72e81-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="72e81-120">passerelle publique Hello qui les clusters hello se situent derrière redirige hello trafic toohello port qui écoute réellement HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="72e81-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="72e81-121">Hello Voici un exemple de chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="72e81-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="72e81-122">Remplacez `CLUSTERNAME` par nom de hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="72e81-123">Authentification</span><span class="sxs-lookup"><span data-stu-id="72e81-123">Authentication</span></span>

<span data-ttu-id="72e81-124">Lorsque vous établissez la connexion de hello, vous devez utiliser hello HDInsight cluster admin nom et mot de passe tooauthenticate toohello cluster la passerelle.</span><span class="sxs-lookup"><span data-stu-id="72e81-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="72e81-125">Lors de la connexion à partir de clients JDBC, tel que non SQL, vous devez entrer le nom de l’administrateur hello et le mot de passe dans les paramètres client.</span><span class="sxs-lookup"><span data-stu-id="72e81-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="72e81-126">À partir d’une application Java, vous devez utiliser un mot de passe et nom de hello lors de l’établissement d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="72e81-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="72e81-127">Par exemple, hello code Java suivant ouvre une nouvelle connexion à l’aide de la chaîne de connexion hello, nom d’administrateur et un mot de passe :</span><span class="sxs-lookup"><span data-stu-id="72e81-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="72e81-128">Connexion avec un client SQuirreL SQL</span><span class="sxs-lookup"><span data-stu-id="72e81-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="72e81-129">Non SQL est un client JDBC qui peut être utilisés tooremotely exécuter des requêtes Hive avec votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="72e81-130">Hello étapes suivantes supposent que vous avez déjà installé non SQL.</span><span class="sxs-lookup"><span data-stu-id="72e81-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="72e81-131">Copier les pilotes JDBC de la ruche hello à partir de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="72e81-132">Pour **HDInsight de basés sur Linux**, les fichiers jar toodownload hello requis les étapes suivantes de hello d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="72e81-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="72e81-133">Créez un répertoire qui contient les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="72e81-134">Par exemple, `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="72e81-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="72e81-135">À partir d’une ligne de commande suivant de hello utilisez commandes fichiers hello toocopy cluster HDInsight de hello :</span><span class="sxs-lookup"><span data-stu-id="72e81-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="72e81-136">Remplacez `USERNAME` avec le nom du compte d’utilisateur hello SSH pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="72e81-137">Remplacez `CLUSTERNAME` avec le nom du cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="72e81-138">Pour **HDInsight de basés sur Windows**, les fichiers jar toodownload hello les étapes suivantes de hello d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="72e81-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="72e81-139">À partir de hello portail Azure, sélectionnez votre cluster HDInsight, puis hello **Bureau à distance** icône.</span><span class="sxs-lookup"><span data-stu-id="72e81-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![Icône Bureau à distance](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="72e81-141">Dans Panneau de bureau à distance hello, utilisez hello **Connect** cluster de toohello tooconnect de bouton.</span><span class="sxs-lookup"><span data-stu-id="72e81-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="72e81-142">Si hello Bureau à distance n’est pas activé, utilisez hello formulaire tooprovide un nom d’utilisateur et mot de passe, puis sélectionnez **activer** tooenable Bureau à distance pour un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![Panneau Bureau à distance](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="72e81-144">Lorsque vous sélectionnez le bouton **Se connecter**, un fichier .rdp est téléchargé.</span><span class="sxs-lookup"><span data-stu-id="72e81-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="72e81-145">Utilisez ce client Bureau à distance de fichier toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="72e81-146">Lorsque vous y êtes invité, utilisez le nom d’utilisateur hello et le mot de que passe pour l’accès Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="72e81-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="72e81-147">Une fois connecté, copiez hello fichiers suivants à partir de l’ordinateur local du tooyour session Bureau à distance hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="72e81-148">Placez-les dans un répertoire local nommé `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="72e81-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="72e81-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="72e81-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="72e81-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="72e81-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="72e81-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="72e81-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="72e81-152">version de Hello nombres inclus dans les chemins d’accès hello et noms de fichiers peut être différente pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="72e81-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="72e81-153">Déconnecter la session de bureau à distance hello lorsque vous avez terminé la copie des fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="72e81-154">Démarrer l’application de hello non SQL.</span><span class="sxs-lookup"><span data-stu-id="72e81-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="72e81-155">De gauche hello de fenêtre hello, sélectionnez **pilotes**.</span><span class="sxs-lookup"><span data-stu-id="72e81-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Onglet pilotes hello gauche de la fenêtre hello](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="72e81-157">Parmi les icônes hello haut hello hello **pilotes** boîte de dialogue, sélectionnez hello  **+**  icône toocreate un pilote.</span><span class="sxs-lookup"><span data-stu-id="72e81-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![Icônes des pilotes](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="72e81-159">Dans la boîte de dialogue Ajouter un pilote hello, ajoutez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="72e81-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="72e81-160">**Nom** : Hive</span><span class="sxs-lookup"><span data-stu-id="72e81-160">**Name**: Hive</span></span>
    * <span data-ttu-id="72e81-161">**Exemple d’URL** : `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="72e81-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="72e81-162">**Chemin de classe supplémentaire**: utilisez hello ajouter bouton tooadd hello jar des fichiers téléchargés précédemment</span><span class="sxs-lookup"><span data-stu-id="72e81-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="72e81-163">**Nom de la classe** : org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="72e81-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![boîte de dialogue ajouter un pilote](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="72e81-165">Cliquez sur **OK** toosave ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="72e81-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="72e81-166">Sur la gauche hello de fenêtre de hello non SQL, sélectionnez **alias**.</span><span class="sxs-lookup"><span data-stu-id="72e81-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="72e81-167">Puis cliquez sur hello  **+**  icône toocreate un alias de connexion.</span><span class="sxs-lookup"><span data-stu-id="72e81-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![ajouter un nouvel alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="72e81-169">Valeurs suivantes de hello d’utilisation pour hello **ajouter un Alias** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="72e81-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="72e81-170">**Nom** : Hive sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="72e81-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="72e81-171">**Pilote**: utilisez Bonjour déroulante tooselect Bonjour **Hive** pilote</span><span class="sxs-lookup"><span data-stu-id="72e81-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="72e81-172">**URL** : jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="72e81-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="72e81-173">Remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="72e81-174">**Nom d’utilisateur**: nom de compte de connexion de cluster hello pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="72e81-175">valeur par défaut Hello est `admin`.</span><span class="sxs-lookup"><span data-stu-id="72e81-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="72e81-176">**Mot de passe**: mot de passe hello hello cluster compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="72e81-176">**Password**: hello password for hello cluster login account.</span></span>

 ![boîte de dialogue ajouter un alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="72e81-178">Hello d’utilisation **Test** tooverify bouton qui hello le fonctionnement de la connexion.</span><span class="sxs-lookup"><span data-stu-id="72e81-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="72e81-179">Lorsque **se connecter à : Hive dans HDInsight** boîte de dialogue s’affiche, sélectionnez **Connect** test de hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="72e81-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="72e81-180">Si hello réussit, vous voyez un **connexion réussie** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="72e81-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="72e81-181">connexion de hello toosave utiliser alias, hello **Ok** bouton bas hello hello **ajouter un Alias** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="72e81-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="72e81-182">À partir de hello **se connecter à** liste déroulante en haut de hello non SQL, sélectionnez **Hive dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="72e81-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="72e81-183">Lorsque vous y êtes invité, sélectionnez **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="72e81-183">When prompted, select **Connect**.</span></span>

    ![boîte de dialogue connexion](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="72e81-185">Une fois connecté, entrez hello ci-dessous de requête dans la boîte de dialogue requête hello SQL, puis sélectionnez hello **exécuter** icône.</span><span class="sxs-lookup"><span data-stu-id="72e81-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="72e81-186">zone de résultats Hello doit afficher les résultats de hello de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![boîte de dialogue requête sql, incluant les résultats](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="72e81-188">Connexion à partir d’un exemple d’application Java</span><span class="sxs-lookup"><span data-stu-id="72e81-188">Connect from an example Java application</span></span>

<span data-ttu-id="72e81-189">Un exemple d’utilisation d’un tooquery de client Java Hive dans HDInsight est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="72e81-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="72e81-190">Suivez les instructions de hello dans hello référentiel toobuild et exécuter l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="72e81-191">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="72e81-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="72e81-192">Une erreur inattendue s’est produite lors de le tooopen une connexion SQL</span><span class="sxs-lookup"><span data-stu-id="72e81-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="72e81-193">**Symptômes**: lors de la connexion de cluster HDInsight tooan version 3.3 ou 3.4, vous pouvez recevoir une erreur s’est produite lors d’une erreur inattendue.</span><span class="sxs-lookup"><span data-stu-id="72e81-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="72e81-194">trace de la pile pour cette erreur Hello commence par hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="72e81-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="72e81-195">**Cause**: cette erreur est due à une incompatibilité de version hello de hello commons-codec.jar fichier non et hello requise par les composants de la ruche de JDBC hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="72e81-196">**Résolution**: toofix étapes de cette erreur, hello utilisation suivant :</span><span class="sxs-lookup"><span data-stu-id="72e81-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="72e81-197">Téléchargez le fichier jar hello commons-codec à partir de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="72e81-198">Quitter non et passez toohello répertoire où non est installé sur votre système.</span><span class="sxs-lookup"><span data-stu-id="72e81-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="72e81-199">Dans le répertoire non hello sous hello `lib` active, remplacer hello existant commons-codec.jar avec hello une téléchargé à partir du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="72e81-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="72e81-200">Redémarrez SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="72e81-200">Restart SQuirreL.</span></span> <span data-ttu-id="72e81-201">Erreur de Hello ne devrait plus apparaître lors de la connexion tooHive sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72e81-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72e81-202">Next steps</span></span>

<span data-ttu-id="72e81-203">Maintenant que vous avez appris comment toowork JDBC toouse avec Hive, hello utilisation suivant lie tooexplore autres toowork manières avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72e81-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="72e81-204">Télécharger des données tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="72e81-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="72e81-205">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="72e81-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="72e81-206">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="72e81-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="72e81-207">Utilisation des tâches MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="72e81-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
