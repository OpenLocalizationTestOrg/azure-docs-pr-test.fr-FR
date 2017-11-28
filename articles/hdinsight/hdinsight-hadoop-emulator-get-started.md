---
title: "Utilisation d’un bac à sable Hadoop – Émulateur – Azure HDInsight | Microsoft Docs"
description: "Pour en savoir plus sur l’utilisation de l’écosystème Hadoop, vous pouvez configurer un bac à sable (sandbox) Hadoop à partir de Hortonworks sur une machine virtuelle Azure. "
keywords: "émulateur Hadoop, bac à sable (sandbox) hadoop"
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: b701879464205860edd1c097651b532f87bae388
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="9654b-104">Prise en main avec un bac à sable Hadoop, un émulateur sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9654b-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="9654b-105">Apprenez à installer le bac à sable (sandbox) Hadoop de Hortonworks sur une machine virtuelle pour vous familiariser avec l’écosystème Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9654b-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="9654b-106">Le bac à sable fournit un environnement de développement local pour se familiariser avec Hadoop, Hadoop Distributed File System (HDFS) et la soumission de tâches.</span><span class="sxs-lookup"><span data-stu-id="9654b-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="9654b-107">Une fois que vous êtes familiarisé avec Hadoop, vous pouvez commencer à l’utiliser sur Azure en créant un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9654b-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="9654b-108">Pour plus d’informations sur la prise en main, consultez [Prise en main de Hadoop sur HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9654b-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9654b-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9654b-109">Prerequisites</span></span>
* <span data-ttu-id="9654b-110">[Oracle VirtualBox](https://www.virtualbox.org/)</span><span class="sxs-lookup"><span data-stu-id="9654b-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="9654b-111">Téléchargez et installez l’application à partir d’[ici](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="9654b-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="9654b-112">Téléchargement et installation de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9654b-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="9654b-113">Accédez aux [téléchargements Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="9654b-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="9654b-114">Cliquez sur **TÉLÉCHARGER POUR VIRTUALBOX** pour télécharger le dernier bac à sable Hortonworks sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9654b-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="9654b-115">Vous serez invité à vous inscrire à Hortonworks avant le lancement du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="9654b-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="9654b-116">Une à deux heures sont nécessaires pour le téléchargement, en fonction de la vitesse de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="9654b-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![Image du lien pour le téléchargement de Hortonworks Sandbox pour VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="9654b-118">À partir de la même page web, cliquez sur le lien **Importer dans Virtual Box** pour télécharger un fichier PDF contenant des instructions d’installation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9654b-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="9654b-119">Pour télécharger un bac à sable (sandbox) de version HDP plus ancienne, développez l’archive :</span><span class="sxs-lookup"><span data-stu-id="9654b-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Archive sandbox Hortonworks](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="9654b-121">Démarrage de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9654b-121">Start the virtual machine</span></span>

1. <span data-ttu-id="9654b-122">Ouvrez Oracle VirtualBox pour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9654b-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="9654b-123">À partir du menu **Fichier**, cliquez sur **Importer l’appliance**, puis spécifiez l’image de sandbox Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="9654b-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="9654b-124">Sélectionnez Hortonworks Sandbox, cliquez sur **Démarrer**, puis sur **Démarrage normal**.</span><span class="sxs-lookup"><span data-stu-id="9654b-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="9654b-125">Une fois le processus de démarrage de la machine virtuelle terminé, celle-ci affiche les instructions de connexion.</span><span class="sxs-lookup"><span data-stu-id="9654b-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![Démarrage normal](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="9654b-127">Ouvrez un navigateur web et accédez à l’URL affichée (généralement http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="9654b-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="9654b-128">Définition de mots de passe Sandbox</span><span class="sxs-lookup"><span data-stu-id="9654b-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="9654b-129">Dans la page de **prise en main** de Hortonworks Sandbox, sélectionnez **View Advanced Options (Options d’affichage avancées)**.</span><span class="sxs-lookup"><span data-stu-id="9654b-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="9654b-130">Utilisez les informations de cette page pour vous connecter au bac à sable avec SSH.</span><span class="sxs-lookup"><span data-stu-id="9654b-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="9654b-131">Utilisez le nom et le mot de passe fournis.</span><span class="sxs-lookup"><span data-stu-id="9654b-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9654b-132">Si vous n’avez pas de client SSH installé, vous pouvez utiliser le client SSH en ligne fourni par la machine virtuelle à l’adresse **http://localhost:4200/**.</span><span class="sxs-lookup"><span data-stu-id="9654b-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="9654b-133">La première fois que vous vous connectez avec SSH, vous serez invité à modifier le mot de passe du compte racine.</span><span class="sxs-lookup"><span data-stu-id="9654b-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="9654b-134">Entrez un nouveau mot de passe que vous utiliserez lorsque vous vous connecterez à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="9654b-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="9654b-135">Une fois connecté, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9654b-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="9654b-136">Lorsque vous y êtes invité, indiquez le mot de passe du compte d’administrateur Ambari.</span><span class="sxs-lookup"><span data-stu-id="9654b-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="9654b-137">Il est utilisé pour accéder à l’interface utilisateur web d’Ambari.</span><span class="sxs-lookup"><span data-stu-id="9654b-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="9654b-138">Utilisation de commandes Hive</span><span class="sxs-lookup"><span data-stu-id="9654b-138">Use Hive commands</span></span>

1. <span data-ttu-id="9654b-139">À partir d’une connexion SSH au bac à sable, utilisez la commande suivante pour démarrer l’interpréteur de commandes Hive :</span><span class="sxs-lookup"><span data-stu-id="9654b-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="9654b-140">Une fois l’interpréteur de commandes a démarré, procédez comme suit pour afficher les tables fournies avec le bac à sable :</span><span class="sxs-lookup"><span data-stu-id="9654b-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="9654b-141">Utilisez la commande suivante pour récupérer 10 lignes de la table `sample_07` :</span><span class="sxs-lookup"><span data-stu-id="9654b-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="9654b-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9654b-142">Next steps</span></span>
* [<span data-ttu-id="9654b-143">Apprendre à utiliser Visual Studio avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="9654b-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="9654b-144">Se familiariser avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="9654b-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="9654b-145">Didacticiel Hadoop - Prise en main de HDP</span><span class="sxs-lookup"><span data-stu-id="9654b-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

