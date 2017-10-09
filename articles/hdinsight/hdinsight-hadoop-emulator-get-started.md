---
title: "aaaLearn à l’aide d’un bac à sable Hadoop - émulateur - Azure HDInsight | Documents Microsoft"
description: "toostart de formation sur l’utilisation de hello Hadoop écosystème, vous pouvez en configurer un bac à sable Hadoop sur Hortonworks sur une machine virtuelle Azure. "
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
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="31875-104">Prise en main avec un bac à sable Hadoop, un émulateur sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="31875-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="31875-105">Découvrez comment tooinstall hello sandbox Hadoop de Hortonworks sur un toolearn d’ordinateur virtuel sur l’écosystème de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="31875-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="31875-106">bac à sable Hello fournit un toolearn d’environnement de développement local sur Hadoop, système de fichiers distribués Hadoop (HDFS) et la soumission de travaux.</span><span class="sxs-lookup"><span data-stu-id="31875-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="31875-107">Une fois que vous êtes familiarisé avec Hadoop, vous pouvez commencer à l’utiliser sur Azure en créant un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31875-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="31875-108">Pour plus d’informations sur comment tooget Démarrer, consultez [prise en main Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="31875-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31875-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="31875-109">Prerequisites</span></span>
* <span data-ttu-id="31875-110">[Oracle VirtualBox](https://www.virtualbox.org/)</span><span class="sxs-lookup"><span data-stu-id="31875-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="31875-111">Téléchargez et installez l’application à partir d’[ici](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="31875-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="31875-112">Téléchargez et installez la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="31875-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="31875-113">Parcourir toohello [Hortonworks télécharge](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="31875-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="31875-114">Cliquez sur **télécharger pour VIRTUALBOX** toodownload hello dernière Hortonworks Sandbox sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="31875-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="31875-115">Vous êtes invité à tooregister avec Hortonworks avant le début de téléchargement de hello.</span><span class="sxs-lookup"><span data-stu-id="31875-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="31875-116">Il prend un toodownload d’heures tootwo selon la vitesse de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="31875-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![Image du lien pour le téléchargement de Hortonworks Sandbox pour VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="31875-118">À partir de hello même page web, cliquez sur hello **importation sur Virtual Box** lien toodownload un fichier PDF qui contient des instructions d’installation pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="31875-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="31875-119">toodownload une ancienne HDP version bac à sable, développez l’archive de hello :</span><span class="sxs-lookup"><span data-stu-id="31875-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Archive sandbox Hortonworks](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="31875-121">Démarrer l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="31875-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="31875-122">Ouvrez Oracle VirtualBox pour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="31875-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="31875-123">À partir de hello **fichier** menu, cliquez sur **importation Appliance**, puis spécifiez hello image de bac à sable Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="31875-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="31875-124">Cliquez sur la Hortonworks Sandbox, sélectionnez hello **Démarrer**, puis **Normal Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="31875-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="31875-125">Une fois que hello virtual machine a terminé le processus de démarrage hello, il affiche des instructions de connexion.</span><span class="sxs-lookup"><span data-stu-id="31875-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![Démarrage normal](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="31875-127">Ouvrez un navigateur web et accédez URL toohello affiché (généralement http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="31875-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="31875-128">Définition de mots de passe Sandbox</span><span class="sxs-lookup"><span data-stu-id="31875-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="31875-129">À partir de hello **prise en main** étape Hello page Hortonworks Sandbox, sélectionnez **Options avancées de vue**.</span><span class="sxs-lookup"><span data-stu-id="31875-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="31875-130">Utilisez les informations de hello sur cette toolog de page dans un bac à sable toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="31875-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="31875-131">Utiliser le nom de hello et le mot de passe fourni.</span><span class="sxs-lookup"><span data-stu-id="31875-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="31875-132">Si vous n’avez pas un client SSH installé, vous pouvez utiliser hello basée sur le web SSH fourni par machine virtuelle de hello dans **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="31875-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="31875-133">Hello première que connexion à l’aide de SSH, vous sont demandées toochange hello mot de passe de compte racine hello.</span><span class="sxs-lookup"><span data-stu-id="31875-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="31875-134">Entrez un nouveau mot de passe que vous utiliserez lorsque vous vous connecterez à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="31875-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="31875-135">Une fois connecté, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="31875-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="31875-136">Lorsque vous y êtes invité, fournissez un mot de passe pour hello Ambari compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="31875-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="31875-137">Il est utilisé lorsque vous accédez à hello Ambari Web UI.</span><span class="sxs-lookup"><span data-stu-id="31875-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="31875-138">Utilisation de commandes Hive</span><span class="sxs-lookup"><span data-stu-id="31875-138">Use Hive commands</span></span>

1. <span data-ttu-id="31875-139">À partir d’un bac à sable SSH connexion toohello, utilisez hello suivant l’interface de commande toostart hello Hive :</span><span class="sxs-lookup"><span data-stu-id="31875-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="31875-140">Une fois que l’interpréteur de commandes hello a démarré, utilisez hello tooview hello tables qui sont fournis avec le bac à sable hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="31875-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="31875-141">Hello utilisation suivant tooretrieve 10 lignes hello `sample_07` table :</span><span class="sxs-lookup"><span data-stu-id="31875-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="31875-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31875-142">Next steps</span></span>
* [<span data-ttu-id="31875-143">Découvrez comment toouse Visual Studio avec hello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="31875-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="31875-144">Apprentissage des câbles hello Hello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="31875-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="31875-145">Didacticiel Hadoop - Prise en main de HDP</span><span class="sxs-lookup"><span data-stu-id="31875-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

