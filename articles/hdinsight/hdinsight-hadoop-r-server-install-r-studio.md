---
title: aaaInstall RStudio avec R Server sur HDInsight - Azure | Documents Microsoft
description: Comment tooinstall RStudio avec R Server sur HDInsight.
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
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="f7dab-103">Installation de RStudio avec R Server sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f7dab-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="f7dab-104">Cet article décrit comment tooinstall hello version (gratuit) communautaire de [RStudio Server](https://www.rstudio.com/products/rstudio-server/) sur le nœud de périmètre hello d’un cluster à l’aide d’un script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f7dab-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="f7dab-105">RStudio Server fournit un IDE sur navigateur utilisable par des clients distants ; il est très répandu sous Linux.</span><span class="sxs-lookup"><span data-stu-id="f7dab-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="f7dab-106">Il existe actuellement plusieurs environnements de développement intégré (IDE) disponibles pour R, notamment :</span><span class="sxs-lookup"><span data-stu-id="f7dab-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="f7dab-107">[Outils R pour Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) de Microsoft ;</span><span class="sxs-lookup"><span data-stu-id="f7dab-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- <span data-ttu-id="f7dab-108">[RStudio Server](https://www.rstudio.com/products/rstudio-server/) ;</span><span class="sxs-lookup"><span data-stu-id="f7dab-108">[RStudio Server](https://www.rstudio.com/products/rstudio-server/)</span></span> 
- <span data-ttu-id="f7dab-109">[StatET](http://www.walware.de/goto/statet) sur Eclipse de WalWare.</span><span class="sxs-lookup"><span data-stu-id="f7dab-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="f7dab-110">avantages de Hello de l’installation de serveur de RStudio sur le nœud de périmètre hello d’un cluster HDInsight sont qu’il offre une expérience complète de l’IDE pour le développement de hello et de l’exécution de scripts R R Server sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f7dab-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="f7dab-111">Cette configuration peut être considérablement plus productive à utiliser par défaut de hello Console R.</span><span class="sxs-lookup"><span data-stu-id="f7dab-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="f7dab-112">Hello procédure décrite dans cet article est uniquement pertinente si vous n’avez pas sélectionné tooinstall édition community de RStudio serveur lors de la configuration de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="f7dab-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="f7dab-113">Si vous l’avez ajouté pendant la configuration, puis les tooaccess il vous cliquez sur hello **tableaux de bord de serveur R** vignette Bonjour Azure entrée portail pour votre cluster, puis sur hello **R Studio Server** vignette.</span><span class="sxs-lookup"><span data-stu-id="f7dab-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="f7dab-114">Si vous préférez toouse hello commerciale sous licence Pro version du serveur de RStudio, vous devez suivre des instructions d’installation à partir de hello [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="f7dab-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="f7dab-115">Si vous utilisez un cluster HDInsight pour lequel R a été installé à l’aide de hello [installer une Action de Script R](hdinsight-hadoop-r-scripts-linux.md), étapes hello dans ce document ne fonctionneront pas correctement car elles nécessitent un serveur R sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="f7dab-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="f7dab-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f7dab-116">Prerequisites</span></span>

* <span data-ttu-id="f7dab-117">Un cluster Azure HDInsight avec R Server installé.</span><span class="sxs-lookup"><span data-stu-id="f7dab-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="f7dab-118">Pour obtenir des instructions, consultez la page [Prise en main de R Server sur les clusters HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f7dab-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="f7dab-119">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="f7dab-119">An SSH client.</span></span> <span data-ttu-id="f7dab-120">Pour les distributions Linux et Unix ou Macintosh OS X, hello `ssh` commande est fournie avec le système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="f7dab-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="f7dab-121">Pour Windows, nous vous recommandons de [Cygwin](http://www.redhat.com/services/custom/cygwin/) avec hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), ou [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="f7dab-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="f7dab-122">Installer RStudio sur cluster hello à l’aide d’un script personnalisé</span><span class="sxs-lookup"><span data-stu-id="f7dab-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="f7dab-123">Voici les étapes hello :</span><span class="sxs-lookup"><span data-stu-id="f7dab-123">Here are hello steps:</span></span>

1. <span data-ttu-id="f7dab-124">Identifier le nœud de périmètre hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f7dab-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="f7dab-125">Pour un cluster HDInsight avec R Server, voici convention d’affectation de noms de hello pour le nœud principal et le nœud de périmètre.</span><span class="sxs-lookup"><span data-stu-id="f7dab-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="f7dab-126">Nœud principal `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="f7dab-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="f7dab-127">Nœud de périmètre `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="f7dab-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="f7dab-128">SSH dans le nœud de périmètre hello du cluster hello à l’aide du modèle d’affectation de noms de hello fourni à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="f7dab-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="f7dab-129">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f7dab-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="f7dab-130">Une fois que vous êtes connecté, devenir un utilisateur racine sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f7dab-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="f7dab-131">Dans la session SSH hello, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f7dab-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="f7dab-132">Télécharger un script personnalisé de hello tooinstall RStudio.</span><span class="sxs-lookup"><span data-stu-id="f7dab-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="f7dab-133">Utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f7dab-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="f7dab-134">Modifier les autorisations de hello sur le fichier de script personnalisé hello et exécuter le script de hello.</span><span class="sxs-lookup"><span data-stu-id="f7dab-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="f7dab-135">Utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="f7dab-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="f7dab-136">Si vous avez utilisé un mot de passe SSH lors de la création d’un cluster HDInsight avec R Server, vous pouvez ignorer cette étape et passez toohello ensuite.</span><span class="sxs-lookup"><span data-stu-id="f7dab-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="f7dab-137">Si vous avez utilisé une clé SSH à la place cluster hello de toocreate, vous devez définir un mot de passe pour votre utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="f7dab-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="f7dab-138">Vous avez besoin de ce mot de passe lors de la connexion tooRStudio.</span><span class="sxs-lookup"><span data-stu-id="f7dab-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="f7dab-139">Exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="f7dab-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="f7dab-140">Lorsque vous êtes invité à entrer le **Mot de passe Kerberos actuel**, appuyez sur **ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="f7dab-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="f7dab-141">Notez que vous devez remplacer `USERNAME` par un utilisateur SSH pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f7dab-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="f7dab-142">Si votre mot de passe est correctement défini, vous devez voir hello message suivant :</span><span class="sxs-lookup"><span data-stu-id="f7dab-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="f7dab-143">Quittez la session SSH hello.</span><span class="sxs-lookup"><span data-stu-id="f7dab-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="f7dab-144">Créer un cluster de toohello tunnel SSH en mappant `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` sur hello HDInsight le cluster toohello ordinateur du client.</span><span class="sxs-lookup"><span data-stu-id="f7dab-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="f7dab-145">Vous devez créer un tunnel SSH avant d’ouvrir une nouvelle session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="f7dab-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="f7dab-146">Sur un client Linux ou un client Windows avec [Cygwin](http://www.redhat.com/services/custom/cygwin/), ouvrez une session Terminal Server et utiliser hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f7dab-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="f7dab-147">Remplacez **nom d’utilisateur** à un utilisateur SSH pour votre cluster HDInsight, puis remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f7dab-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="f7dab-148">Vous pouvez également utiliser une clé SSH plutôt qu’un mot de passe en ajoutant `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="f7dab-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="f7dab-149">Si vous utilisez un client Windows avec PuTTY</span><span class="sxs-lookup"><span data-stu-id="f7dab-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="f7dab-150">Ouvrez PuTTY et saisissez vos informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="f7dab-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="f7dab-151">Bonjour **catégorie** toohello de la section gauche de la boîte de dialogue hello, développez **connexion**, développez **SSH**, puis sélectionnez **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="f7dab-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="f7dab-152">Fournir hello suivant les informations de hello **réacheminement de port Options contrôlant SSH** formulaire :</span><span class="sxs-lookup"><span data-stu-id="f7dab-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="f7dab-153">**Port source** -hello port client hello que vous souhaitez tooforward.</span><span class="sxs-lookup"><span data-stu-id="f7dab-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="f7dab-154">Par exemple, **8787**.</span><span class="sxs-lookup"><span data-stu-id="f7dab-154">For example, **8787**.</span></span>
        * <span data-ttu-id="f7dab-155">**Destination** - hello destination doit être mappée ordinateur du client local toohello.</span><span class="sxs-lookup"><span data-stu-id="f7dab-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="f7dab-156">Par exemple, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="f7dab-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="f7dab-157">![Création d’un tunnel SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Création d’un tunnel SSH")</span><span class="sxs-lookup"><span data-stu-id="f7dab-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="f7dab-158">Cliquez sur **ajouter** tooadd hello paramètres, puis cliquez sur **ouvrir** tooopen une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="f7dab-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="f7dab-159">Lorsque vous y êtes invité, connectez-vous toohello server tooestablish un tunnel hello SSH la session et l’activer.</span><span class="sxs-lookup"><span data-stu-id="f7dab-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="f7dab-160">Ouvrez un navigateur web, puis entrez hello suivant URL basée sur le port hello que vous avez entré pour un tunnel de hello :</span><span class="sxs-lookup"><span data-stu-id="f7dab-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="f7dab-161">Vous êtes invité à tooenter hello SSH nom d’utilisateur et mot de passe tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="f7dab-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="f7dab-162">Si vous avez utilisé une clé SSH lors de la création du cluster de hello, vous devez entrer un mot de passe hello créé à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="f7dab-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="f7dab-163">![Se connecter tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "créer un tunnel SSH")</span><span class="sxs-lookup"><span data-stu-id="f7dab-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="f7dab-164">tootest si hello RStudio installation a réussi, vous pouvez exécuter un script de test qui exécute des tâches de MapReduce et Spark R sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f7dab-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="f7dab-165">toodownload hello test script toorun dans RStudio, revenez en arrière toohello SSH console, puis entrez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="f7dab-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="f7dab-166">Si vous avez créé un cluster Hadoop avec R, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="f7dab-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="f7dab-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="f7dab-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="f7dab-168">Si vous avez créé un cluster Spark avec R, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="f7dab-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="f7dab-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="f7dab-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="f7dab-170">Dans RStudio, vous voyez hello tester le script que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="f7dab-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="f7dab-171">Double-cliquez sur hello fichier tooopen, sélectionnez le contenu du fichier de hello hello, puis cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="f7dab-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="f7dab-172">Vous devez voir la sortie hello Bonjour **Console** volet :</span><span class="sxs-lookup"><span data-stu-id="f7dab-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="f7dab-173">![Tester l’installation de hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "tester hello installation")</span><span class="sxs-lookup"><span data-stu-id="f7dab-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="f7dab-174">Une autre option serait tootype `source(testhdi.r)` ou `source(testhdi_spark.r)` script de hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="f7dab-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="f7dab-175">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f7dab-175">See also</span></span>

* [<span data-ttu-id="f7dab-176">Calcul d’options de contexte pour R Server sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="f7dab-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="f7dab-177">Options d’Azure Storage pour R Server sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f7dab-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

