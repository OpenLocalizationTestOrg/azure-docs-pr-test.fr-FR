---
title: Installer RStudio avec R Server sur HDInsight - Azure | Microsoft Docs
description: Comment installer RStudio avec R Server sur HDInsight.
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="8fbfa-103">Installation de RStudio avec R Server sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fbfa-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="8fbfa-104">Cet article explique comment installer la version (gratuite) communautaire de [RStudio Server](https://www.rstudio.com/products/rstudio-server/) sur le nœud périphérique d’un cluster à l’aide d’un script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-104">This article describes how to install the community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on the edge node of a cluster using a custom script.</span></span> <span data-ttu-id="8fbfa-105">RStudio Server fournit un IDE sur navigateur utilisable par des clients distants ; il est très répandu sous Linux.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="8fbfa-106">Il existe actuellement plusieurs environnements de développement intégré (IDE) disponibles pour R, notamment :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="8fbfa-107">[Outils R pour Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) de Microsoft ;</span><span class="sxs-lookup"><span data-stu-id="8fbfa-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- <span data-ttu-id="8fbfa-108">[RStudio Server](https://www.rstudio.com/products/rstudio-server/) ;</span><span class="sxs-lookup"><span data-stu-id="8fbfa-108">[RStudio Server](https://www.rstudio.com/products/rstudio-server/)</span></span> 
- <span data-ttu-id="8fbfa-109">[StatET](http://www.walware.de/goto/statet) sur Eclipse de WalWare.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="8fbfa-110">L’installation de RStudio Server sur le nœud périphérique d’un cluster HDInsight présente l’avantage d’offrir une expérience d’IDE complète pour le développement et l’exécution de scripts R avec R Server sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-110">The advantage of installing RStudio Server on the edge node of an HDInsight cluster is that it provides a full IDE experience for the development and execution of R scripts with R Server on the cluster.</span></span> <span data-ttu-id="8fbfa-111">Cette configuration peut être considérablement plus productive que l’utilisation par défaut de la console R.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-111">This configuration can be considerably more productive than default use of the R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="8fbfa-112">La procédure décrite dans cet article s'applique uniquement si vous n’avez pas choisi d'installer RStudio Server Community Edition lors de la configuration de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-112">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="8fbfa-113">Si vous l’avez ajouté lors de l’approvisionnement, vous pouvez y accéder en cliquant sur la mosaïque **Tableaux de bord R Server** dans l’entrée de votre cluster sur le Portail Azure, puis en cliquant sur la mosaïque **R Studio Server**.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-113">If you added it during provisioning, then to access it you click on the **R Server Dashboards** tile in the Azure portal entry for your cluster, then on the **R Studio Server** tile.</span></span> 

<span data-ttu-id="8fbfa-114">Si vous préférez utiliser la version commerciale Pro sous licence de RStudio Server, vous devez suivre les instructions d’installation de [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="8fbfa-114">If you prefer to use the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="8fbfa-115">Si vous utilisez un cluster HDInsight pour lequel R Server a été installé à l’aide de l’option [Installer une action de script R](hdinsight-hadoop-r-scripts-linux.md), la procédure décrite dans ce document ne fonctionnera pas correctement, car il faut qu’un R Server se trouve sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-115">If you are using an HDInsight cluster for which R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), the steps in this document will not work correctly as they require an R Server on the HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="8fbfa-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8fbfa-116">Prerequisites</span></span>

* <span data-ttu-id="8fbfa-117">Un cluster Azure HDInsight avec R Server installé.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="8fbfa-118">Pour obtenir des instructions, consultez la page [Prise en main de R Server sur les clusters HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8fbfa-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="8fbfa-119">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-119">An SSH client.</span></span> <span data-ttu-id="8fbfa-120">Pour les distributions Linux et Unix ou pour Macintosh OS X, la commande `ssh` est fournie avec le système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-120">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="8fbfa-121">Pour Windows, nous vous recommandons [Cygwin](http://www.redhat.com/services/custom/cygwin/) avec [l’option OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU) ou [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="8fbfa-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a><span data-ttu-id="8fbfa-122">Installation de RStudio sur le cluster à l’aide d’un script personnalisé</span><span class="sxs-lookup"><span data-stu-id="8fbfa-122">Install RStudio on the cluster using a custom script</span></span>

<span data-ttu-id="8fbfa-123">Voici la procédure à suivre :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-123">Here are the steps:</span></span>

1. <span data-ttu-id="8fbfa-124">Identifiez le nœud de périmètre du cluster.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-124">Identify the edge node of the cluster.</span></span> <span data-ttu-id="8fbfa-125">Concernant le cluster HDInsight avec R Server, voici la convention d’affectation de noms pour le nœud principal et le nœud de périmètre.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-125">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="8fbfa-126">Nœud principal `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="8fbfa-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="8fbfa-127">Nœud de périmètre `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="8fbfa-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="8fbfa-128">Établissez une connexion SSH dans le nœud périphérique du cluster selon le modèle d’affectation de noms fourni à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-128">SSH into the edge node of the cluster using the naming pattern provided in step 1.</span></span> <span data-ttu-id="8fbfa-129">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8fbfa-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="8fbfa-130">Une fois que vous êtes connecté, devenez un utilisateur racine sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-130">Once you are connected, become a root user on the cluster.</span></span> <span data-ttu-id="8fbfa-131">Dans la session SSH, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-131">In the SSH session, use the following command:</span></span>

        sudo su -

4. <span data-ttu-id="8fbfa-132">Téléchargez le script personnalisé pour installer RStudio.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-132">Download the custom script to install RStudio.</span></span> <span data-ttu-id="8fbfa-133">Utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-133">Use the following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="8fbfa-134">Modifiez les autorisations sur le fichier de script personnalisé et exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-134">Change the permissions on the custom script file and run the script.</span></span> <span data-ttu-id="8fbfa-135">Utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-135">Use the following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="8fbfa-136">Si vous avez utilisé un mot de passe SSH en créant un cluster HDInsight avec R Server, vous pouvez ignorer cette étape et passer à la suivante.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span></span> <span data-ttu-id="8fbfa-137">Si vous avez utilisé à la place une clé SSH pour créer le cluster, vous devez définir un mot de passe pour votre utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-137">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="8fbfa-138">Vous avez besoin de ce mot de passe pour vous connecter à RStudio.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-138">You need this password when connecting to RStudio.</span></span> <span data-ttu-id="8fbfa-139">Exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-139">Run the following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="8fbfa-140">Lorsque vous êtes invité à entrer le **Mot de passe Kerberos actuel**, appuyez sur **ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="8fbfa-141">Notez que vous devez remplacer `USERNAME` par un utilisateur SSH pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="8fbfa-142">Si votre mot de passe est défini correctement, le message suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-142">If your password is successfully set, you should see the following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="8fbfa-143">Quittez la session SSH.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-143">Exit the SSH session.</span></span>

8. <span data-ttu-id="8fbfa-144">Créez un tunnel SSH vers le cluster en mappant `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` sur le cluster HDInsight à l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-144">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span></span> <span data-ttu-id="8fbfa-145">Vous devez créer un tunnel SSH avant d’ouvrir une nouvelle session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="8fbfa-146">Sur un client Linux ou un client Windows avec [Cygwin](http://www.redhat.com/services/custom/cygwin/), ouvrez une session de terminal et utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use the following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="8fbfa-147">Remplacez **USERNAME** par un utilisateur SSH de votre cluster HDInsight et **CLUSTERNAME** par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>
       <span data-ttu-id="8fbfa-148">Vous pouvez également utiliser une clé SSH plutôt qu’un mot de passe en ajoutant `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="8fbfa-149">Si vous utilisez un client Windows avec PuTTY</span><span class="sxs-lookup"><span data-stu-id="8fbfa-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="8fbfa-150">Ouvrez PuTTY et saisissez vos informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="8fbfa-151">Dans la rubrique **Catégorie** située à gauche dans la boîte de dialogue, développez **Connexion** et **SSH**, puis sélectionnez **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-151">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="8fbfa-152">Indiquez les informations suivantes dans le formulaire des **Options de contrôle de transfert du port SSH** .</span><span class="sxs-lookup"><span data-stu-id="8fbfa-152">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="8fbfa-153">**Port source** : le port sur le client que vous souhaitez transférer.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-153">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="8fbfa-154">Par exemple, **8787**.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-154">For example, **8787**.</span></span>
        * <span data-ttu-id="8fbfa-155">**Destination** - La destination doit être mappée à l’ordinateur client local.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-155">**Destination** - The destination that must be mapped to the local client machine.</span></span> <span data-ttu-id="8fbfa-156">Par exemple, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="8fbfa-157">![Création d’un tunnel SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Création d’un tunnel SSH")</span><span class="sxs-lookup"><span data-stu-id="8fbfa-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="8fbfa-158">Cliquez sur **Ajouter** pour ajouter les paramètres, puis cliquez sur **Ouvrir** pour ouvrir une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-158">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>
     5. <span data-ttu-id="8fbfa-159">Lorsque vous y êtes invité, connectez-vous au serveur pour établir une session SSH et activer le tunnel.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-159">When prompted, log in to the server to establish an SSH session and enable the tunnel.</span></span>

9. <span data-ttu-id="8fbfa-160">Ouvrez un navigateur web et entrez l’URL suivante en fonction du port que vous avez entré pour le tunnel :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-160">Open a web browser and enter the following URL based on the port you entered for the tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="8fbfa-161">Vous êtes invité à entrer le nom d’utilisateur SSH et le mot de passe pour vous connecter au cluster.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-161">You are prompted to enter the SSH username and password to connect to the cluster.</span></span> <span data-ttu-id="8fbfa-162">Si vous avez utilisé une clé SSH en créant le cluster, vous devez entrer le mot de passe que vous avez créé à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-162">If you used an SSH key while creating the cluster, you must enter the password you created in step 5.</span></span>

    <span data-ttu-id="8fbfa-163">![Connexion à R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Création d’un tunnel SSH")</span><span class="sxs-lookup"><span data-stu-id="8fbfa-163">![Connect to R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="8fbfa-164">Pour tester si l’installation de RStudio s’est bien déroulée, vous pouvez exécuter un script de test qui exécute des travaux R MapReduce et Spark sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-164">To test whether the RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on the cluster.</span></span> <span data-ttu-id="8fbfa-165">Pour télécharger le script de test à exécuter dans RStudio, revenez à la console SSH et entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-165">To download the test script to run in RStudio, go back to the SSH console and enter the following commands:</span></span>

    *    <span data-ttu-id="8fbfa-166">Si vous avez créé un cluster Hadoop avec R, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="8fbfa-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="8fbfa-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="8fbfa-168">Si vous avez créé un cluster Spark avec R, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="8fbfa-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="8fbfa-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="8fbfa-170">Dans RStudio, vous verrez le script de test que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-170">In RStudio, you see the test script you downloaded.</span></span> <span data-ttu-id="8fbfa-171">Double-cliquez sur le fichier pour l’ouvrir, sélectionnez son contenu, puis cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-171">Double-click the file to open it, select the contents of the file, and then click **Run**.</span></span> <span data-ttu-id="8fbfa-172">Vous devriez voir la sortie dans le volet **Console** :</span><span class="sxs-lookup"><span data-stu-id="8fbfa-172">You should see the output in the **Console** pane:</span></span>

   <span data-ttu-id="8fbfa-173">![Test de l’installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test de l’installation")</span><span class="sxs-lookup"><span data-stu-id="8fbfa-173">![Test the installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span></span>

<span data-ttu-id="8fbfa-174">Vous pouvez également taper `source(testhdi.r)` ou `source(testhdi_spark.r)` pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="8fbfa-174">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span></span>

## <a name="see-also"></a><span data-ttu-id="8fbfa-175">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8fbfa-175">See also</span></span>

* [<span data-ttu-id="8fbfa-176">Calcul d’options de contexte pour R Server sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fbfa-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="8fbfa-177">Options d’Azure Storage pour R Server sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fbfa-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

