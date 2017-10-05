---
title: "Installer un bloc-notes Jupyter localement et le connecter à un cluster Spark Azure HDInsight | Microsoft Docs"
description: "Découvrez comment installer un bloc-notes Jupyter localement sur votre ordinateur et le connecter à un cluster Apache Spark sur Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: fe9dcdb643aa6a8ee5d55738b7a446e4b0153986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="21c6a-103">Installer un bloc-notes Jupyter sur votre ordinateur et le connecter à Apache Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c6a-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="21c6a-104">Dans cet article, vous allez apprendre à installer le bloc-notes Jupyter avec les noyaux PySpark (pour Python) et Spark (pour Scala) personnalisés avec Spark magic et connecter le bloc-notes à un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c6a-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="21c6a-105">Plusieurs raisons peuvent motiver l’installation de Jupyter sur votre ordinateur local. Différents défis peuvent également se présenter.</span><span class="sxs-lookup"><span data-stu-id="21c6a-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="21c6a-106">Consultez la section [Pourquoi dois-je installer Jupyter sur mon ordinateur ?](#why-should-i-install-jupyter-on-my-computer) à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="21c6a-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="21c6a-107">L’installation de Jupyter et de Spark magic sur votre ordinateur comprend trois étapes essentielles.</span><span class="sxs-lookup"><span data-stu-id="21c6a-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="21c6a-108">Installation du bloc-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="21c6a-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="21c6a-109">Installation des noyaux PySpark et Spark avec Spark Magic</span><span class="sxs-lookup"><span data-stu-id="21c6a-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="21c6a-110">Configuration de Spark Magic pour accéder au cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c6a-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="21c6a-111">Pour plus d’informations sur les noyaux personnalisés et Spark Magic disponible pour les blocs-notes Jupyter avec le cluster HDInsight, consultez [Noyaux disponibles pour les blocs-notes Jupyter avec les clusters HDInsight Spark Linux sur HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="21c6a-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21c6a-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="21c6a-112">Prerequisites</span></span>
<span data-ttu-id="21c6a-113">La configuration requise indiquée ici ne concerne pas l’installation de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="21c6a-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="21c6a-114">Elle s’applique à la connexion du bloc-notes Jupyter à un cluster HDInsight une fois le bloc-notes installé.</span><span class="sxs-lookup"><span data-stu-id="21c6a-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="21c6a-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="21c6a-115">An Azure subscription.</span></span> <span data-ttu-id="21c6a-116">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="21c6a-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="21c6a-117">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c6a-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="21c6a-118">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="21c6a-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="21c6a-119">Installer le bloc-notes Jupyter sur votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="21c6a-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="21c6a-120">Vous devez installer Python avant de pouvoir installer les blocs-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="21c6a-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="21c6a-121">Python et Jupyter font partie de la [distribution Anaconda](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="21c6a-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="21c6a-122">Lorsque vous installez Anaconda, vous installez une distribution de Python.</span><span class="sxs-lookup"><span data-stu-id="21c6a-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="21c6a-123">Une fois Anaconda installé, vous ajoutez l’installation de Jupyter en exécutant les commandes appropriées.</span><span class="sxs-lookup"><span data-stu-id="21c6a-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="21c6a-124">Téléchargez le [programme d’installation Anaconda](https://www.continuum.io/downloads) pour votre plateforme et exécutez le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="21c6a-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="21c6a-125">Lors de l’exécution de l’assistant d’installation, veillez à sélectionner l’option permettant d’ajouter Anaconda à votre variable PATH.</span><span class="sxs-lookup"><span data-stu-id="21c6a-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="21c6a-126">Exécutez la commande suivante pour installer Jupyter.</span><span class="sxs-lookup"><span data-stu-id="21c6a-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="21c6a-127">Pour plus d’informations sur l’installation de Jupyter, consultez [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html)(Installation de Jupyter à l’aide d’Anaconda).</span><span class="sxs-lookup"><span data-stu-id="21c6a-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="21c6a-128">Installer les noyaux et Spark Magic</span><span class="sxs-lookup"><span data-stu-id="21c6a-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="21c6a-129">Pour obtenir des instructions sur l’installation des noyaux Spark Magic, PySpark et Spark, consultez la [documentation sparkmagic](https://github.com/jupyter-incubator/sparkmagic#installation) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="21c6a-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="21c6a-130">La première étape de la documentation vous invite à installer Spark Magic.</span><span class="sxs-lookup"><span data-stu-id="21c6a-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="21c6a-131">Remplacez la première étape du lien par les commandes suivantes, selon la version du cluster HDInsight auquel vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="21c6a-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="21c6a-132">Après cela, suivez les étapes restantes de la documentation Spark Magic.</span><span class="sxs-lookup"><span data-stu-id="21c6a-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="21c6a-133">Si vous souhaitez installer les différents noyaux, vous devez effectuer l’étape 3 de la section contenant les instructions d’installation.</span><span class="sxs-lookup"><span data-stu-id="21c6a-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="21c6a-134">Pour les clusters v3.4, installez sparkmagic 0.2.3 en exécutant `pip install sparkmagic==0.2.3`.</span><span class="sxs-lookup"><span data-stu-id="21c6a-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="21c6a-135">Pour les clusters v3.5 et v3.6, installez sparkmagic 0.11.2 en exécutant `pip install sparkmagic==0.11.2`.</span><span class="sxs-lookup"><span data-stu-id="21c6a-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="21c6a-136">Configurer Spark Magic pour la connexion au cluster Spark HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c6a-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="21c6a-137">Dans cette section, vous configurez Spark Magic que vous avez installé précédemment pour qu’il se connecte à un cluster Apache Spark que vous devez avoir déjà créé dans Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c6a-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="21c6a-138">Les informations de configuration de Jupyter sont généralement stockées dans le répertoire de base des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="21c6a-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="21c6a-139">Pour localiser votre répertoire de base sur n’importe quelle plateforme de système d’exploitation, tapez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="21c6a-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="21c6a-140">Démarrez l’interface de Python.</span><span class="sxs-lookup"><span data-stu-id="21c6a-140">Start the Python shell.</span></span> <span data-ttu-id="21c6a-141">Dans la fenêtre de commande, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="21c6a-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="21c6a-142">Dans l’interface de Python, entrez la commande suivante pour rechercher le répertoire de base.</span><span class="sxs-lookup"><span data-stu-id="21c6a-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="21c6a-143">Accédez au répertoire de base et créez un dossier nommé **.sparkmagic** s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="21c6a-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="21c6a-144">Dans le dossier, créez un fichier appelé **config.json** et ajoutez-y l’extrait de code JSON suivant.</span><span class="sxs-lookup"><span data-stu-id="21c6a-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="21c6a-145">Remplacez **{USERNAME}**, **{CLUSTERDNSNAME}** et **{BASE64ENCODEDPASSWORD}** par les valeurs appropriées.</span><span class="sxs-lookup"><span data-stu-id="21c6a-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="21c6a-146">Vous pouvez utiliser un certain nombre d’utilitaires dans votre langage de programmation favori ou en ligne pour générer un mot de passe codé en base64 pour votre mot de passe actuel.</span><span class="sxs-lookup"><span data-stu-id="21c6a-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="21c6a-147">Configurez les bons paramètres de pulsation dans `config.json`.</span><span class="sxs-lookup"><span data-stu-id="21c6a-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="21c6a-148">Vous devez ajouter ces paramètres au même niveau que les extraits de code `kernel_python_credentials` et `kernel_scala_credentials` ajoutés précédemment.</span><span class="sxs-lookup"><span data-stu-id="21c6a-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="21c6a-149">Consultez cet [exemple config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json) pour voir comment et où ajouter les paramètres de pulsation.</span><span class="sxs-lookup"><span data-stu-id="21c6a-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="21c6a-150">Pour `sparkmagic 0.2.3` (clusters v3.4), incluez :</span><span class="sxs-lookup"><span data-stu-id="21c6a-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="21c6a-151">Pour `sparkmagic 0.11.2` (clusters v3.5 et v3.6), incluez :</span><span class="sxs-lookup"><span data-stu-id="21c6a-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="21c6a-152">Les pulsations sont envoyées pour vous assurer que les sessions ne sont pas divulguées.</span><span class="sxs-lookup"><span data-stu-id="21c6a-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="21c6a-153">Lorsqu’un ordinateur se met en veille ou s’arrête, la pulsation n’est pas envoyée, causant ainsi le nettoyage de la session.</span><span class="sxs-lookup"><span data-stu-id="21c6a-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="21c6a-154">Pour les clusters v3.4, si vous souhaitez désactiver ce comportement, vous pouvez définir la configuration Livy `livy.server.interactive.heartbeat.timeout` à `0` à partir de l’interface utilisateur Ambari.</span><span class="sxs-lookup"><span data-stu-id="21c6a-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="21c6a-155">Pour les clusters v3.5, si vous ne définissez pas la configuration 3.5 ci-dessus, la session ne sera pas supprimée.</span><span class="sxs-lookup"><span data-stu-id="21c6a-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="21c6a-156">Démarrez Jupyter.</span><span class="sxs-lookup"><span data-stu-id="21c6a-156">Start Jupyter.</span></span> <span data-ttu-id="21c6a-157">Utilisez la commande suivante depuis l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="21c6a-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="21c6a-158">Vérifiez que vous pouvez vous connecter au cluster à l’aide du bloc-notes Jupyter et que vous pouvez utiliser Spark Magic disponible avec les noyaux.</span><span class="sxs-lookup"><span data-stu-id="21c6a-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="21c6a-159">Procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="21c6a-159">Perform the following steps.</span></span>

    <span data-ttu-id="21c6a-160">a.</span><span class="sxs-lookup"><span data-stu-id="21c6a-160">a.</span></span> <span data-ttu-id="21c6a-161">Créer un nouveau bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="21c6a-161">Create a new notebook.</span></span> <span data-ttu-id="21c6a-162">Dans le coin de droite, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="21c6a-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="21c6a-163">Le noyau par défaut **Python2** doit s’afficher, ainsi que les deux nouveaux noyaux que vous installez : **PySpark** et **Spark**.</span><span class="sxs-lookup"><span data-stu-id="21c6a-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="21c6a-164">Cliquez sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="21c6a-164">Click **PySpark**.</span></span>

    <span data-ttu-id="21c6a-165">![Noyaux de bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Noyaux de bloc-notes Jupyter")</span><span class="sxs-lookup"><span data-stu-id="21c6a-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="21c6a-166">b.</span><span class="sxs-lookup"><span data-stu-id="21c6a-166">b.</span></span> <span data-ttu-id="21c6a-167">Exécutez l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="21c6a-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="21c6a-168">Votre connexion au cluster HDInsight sera testée, si vous parvenez à récupérer la sortie.</span><span class="sxs-lookup"><span data-stu-id="21c6a-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="21c6a-169">Si vous souhaitez mettre à jour la configuration du bloc-notes pour vous connecter à un autre cluster, mettez à jour le fichier config.json en tenant compte du nouveau jeu de valeurs, comme indiqué à l’étape 3 ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="21c6a-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="21c6a-170">Pourquoi dois-je installer Jupyter sur mon ordinateur ?</span><span class="sxs-lookup"><span data-stu-id="21c6a-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="21c6a-171">Plusieurs raisons peuvent motiver l’installation de Jupyter sur votre ordinateur et sa connexion à un cluster Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c6a-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="21c6a-172">Même si les blocs-notes Jupyter sont déjà disponibles sur le cluster Spark dans Azure HDInsight, l’installation de Jupyter sur votre ordinateur vous permet de créer vos blocs-notes localement, de tester votre application sur un cluster en cours d’exécution, puis de charger les blocs-notes sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="21c6a-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="21c6a-173">Vous pouvez charger les blocs-notes dans le cluster à l’aide du bloc-notes Jupyter en cours d’exécution ou du cluster, ou en les enregistrant dans le dossier /HdiNotebooks du compte de stockage associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="21c6a-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="21c6a-174">Pour plus d’informations sur le stockage des blocs-notes, consultez [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)(Où sont stockés les blocs-notes Jupyter) ?</span><span class="sxs-lookup"><span data-stu-id="21c6a-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="21c6a-175">Les blocs-notes étant disponibles localement, vous pouvez vous connecter à différents clusters Spark selon les besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="21c6a-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="21c6a-176">Vous pouvez utiliser GitHub pour implémenter un système de contrôle de code source et disposer du contrôle de version pour les blocs-notes.</span><span class="sxs-lookup"><span data-stu-id="21c6a-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="21c6a-177">Vous pouvez également disposer d’un environnement de collaboration où plusieurs utilisateurs peuvent travailler avec le même bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="21c6a-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="21c6a-178">Vous pouvez travailler avec les blocs-notes localement sans avoir un cluster activé.</span><span class="sxs-lookup"><span data-stu-id="21c6a-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="21c6a-179">Il vous suffit d’un cluster avec lequel tester vos blocs-notes, sans avoir à gérer manuellement vos blocs-notes ou à disposer d’un environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="21c6a-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="21c6a-180">Il peut être plus facile de configurer votre propre environnement de développement local que de configurer l’installation de Jupyter sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="21c6a-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="21c6a-181">Vous pouvez tirer parti de tous les logiciels que vous avez installés localement sans configurer un ou plusieurs clusters distants.</span><span class="sxs-lookup"><span data-stu-id="21c6a-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="21c6a-182">Lorsque Jupyter est installé sur votre ordinateur local, plusieurs utilisateurs peuvent exécuter le même bloc-notes sur le même cluster Spark en même temps.</span><span class="sxs-lookup"><span data-stu-id="21c6a-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="21c6a-183">Dans ce cas, plusieurs sessions Livy sont créées.</span><span class="sxs-lookup"><span data-stu-id="21c6a-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="21c6a-184">Si vous rencontrez un problème et que vous souhaitez effectuer un débogage, il sera difficile de savoir quelle session Livy appartient à quel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="21c6a-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <span data-ttu-id="21c6a-185"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="21c6a-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="21c6a-186">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c6a-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="21c6a-187">Scénarios</span><span class="sxs-lookup"><span data-stu-id="21c6a-187">Scenarios</span></span>
* [<span data-ttu-id="21c6a-188">Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI</span><span class="sxs-lookup"><span data-stu-id="21c6a-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="21c6a-189">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC</span><span class="sxs-lookup"><span data-stu-id="21c6a-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="21c6a-190">Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments</span><span class="sxs-lookup"><span data-stu-id="21c6a-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="21c6a-191">Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel</span><span class="sxs-lookup"><span data-stu-id="21c6a-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="21c6a-192">Analyse des journaux de site web à l’aide de Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c6a-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="21c6a-193">Créer et exécuter des applications</span><span class="sxs-lookup"><span data-stu-id="21c6a-193">Create and run applications</span></span>
* [<span data-ttu-id="21c6a-194">Créer une application autonome avec Scala</span><span class="sxs-lookup"><span data-stu-id="21c6a-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="21c6a-195">Exécuter des tâches à distance avec Livy sur un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="21c6a-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="21c6a-196">Outils et extensions</span><span class="sxs-lookup"><span data-stu-id="21c6a-196">Tools and extensions</span></span>
* [<span data-ttu-id="21c6a-197">Utilisation du plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala</span><span class="sxs-lookup"><span data-stu-id="21c6a-197">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="21c6a-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)</span><span class="sxs-lookup"><span data-stu-id="21c6a-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="21c6a-199">Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c6a-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="21c6a-200">Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c6a-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="21c6a-201">Utiliser des packages externes avec les blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="21c6a-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="21c6a-202">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="21c6a-202">Manage resources</span></span>
* [<span data-ttu-id="21c6a-203">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c6a-203">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="21c6a-204">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="21c6a-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
