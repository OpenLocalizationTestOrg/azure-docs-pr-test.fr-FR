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
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a>Prise en main avec un bac à sable Hadoop, un émulateur sur une machine virtuelle

Découvrez comment tooinstall hello sandbox Hadoop de Hortonworks sur un toolearn d’ordinateur virtuel sur l’écosystème de Hadoop hello. bac à sable Hello fournit un toolearn d’environnement de développement local sur Hadoop, système de fichiers distribués Hadoop (HDFS) et la soumission de travaux. Une fois que vous êtes familiarisé avec Hadoop, vous pouvez commencer à l’utiliser sur Azure en créant un cluster HDInsight. Pour plus d’informations sur comment tooget Démarrer, consultez [prise en main Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

## <a name="prerequisites"></a>Composants requis
* [Oracle VirtualBox](https://www.virtualbox.org/) Téléchargez et installez l’application à partir d’[ici](https://www.virtualbox.org/wiki/Downloads).



## <a name="download-and-install-hello-virtual-machine"></a>Téléchargez et installez la machine virtuelle de hello
1. Parcourir toohello [Hortonworks télécharge](http://hortonworks.com/downloads/#sandbox).

2. Cliquez sur **télécharger pour VIRTUALBOX** toodownload hello dernière Hortonworks Sandbox sur un ordinateur virtuel. Vous êtes invité à tooregister avec Hortonworks avant le début de téléchargement de hello. Il prend un toodownload d’heures tootwo selon la vitesse de votre réseau.
   
    ![Image du lien pour le téléchargement de Hortonworks Sandbox pour VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. À partir de hello même page web, cliquez sur hello **importation sur Virtual Box** lien toodownload un fichier PDF qui contient des instructions d’installation pour la machine virtuelle de hello.

toodownload une ancienne HDP version bac à sable, développez l’archive de hello :

![Archive sandbox Hortonworks](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a>Démarrer l’ordinateur virtuel de hello

1. Ouvrez Oracle VirtualBox pour machine virtuelle.
2. À partir de hello **fichier** menu, cliquez sur **importation Appliance**, puis spécifiez hello image de bac à sable Hortonworks.
1. Cliquez sur la Hortonworks Sandbox, sélectionnez hello **Démarrer**, puis **Normal Démarrer**. Une fois que hello virtual machine a terminé le processus de démarrage hello, il affiche des instructions de connexion.
   
    ![Démarrage normal](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. Ouvrez un navigateur web et accédez URL toohello affiché (généralement http://127.0.0.1:8888).

## <a name="set-sandbox-passwords"></a>Définition de mots de passe Sandbox

1. À partir de hello **prise en main** étape Hello page Hortonworks Sandbox, sélectionnez **Options avancées de vue**. Utilisez les informations de hello sur cette toolog de page dans un bac à sable toohello à l’aide de SSH. Utiliser le nom de hello et le mot de passe fourni.
   
   > [!NOTE]
   > Si vous n’avez pas un client SSH installé, vous pouvez utiliser hello basée sur le web SSH fourni par machine virtuelle de hello dans **http://localhost:4200 /**.
   > 
   
    Hello première que connexion à l’aide de SSH, vous sont demandées toochange hello mot de passe de compte racine hello. Entrez un nouveau mot de passe que vous utiliserez lorsque vous vous connecterez à l’aide de SSH.

2. Une fois connecté, entrez hello de commande suivante :
   
        ambari-admin-password-reset
   
    Lorsque vous y êtes invité, fournissez un mot de passe pour hello Ambari compte d’administrateur. Il est utilisé lorsque vous accédez à hello Ambari Web UI.

## <a name="use-hive-commands"></a>Utilisation de commandes Hive

1. À partir d’un bac à sable SSH connexion toohello, utilisez hello suivant l’interface de commande toostart hello Hive :
   
        hive
2. Une fois que l’interpréteur de commandes hello a démarré, utilisez hello tooview hello tables qui sont fournis avec le bac à sable hello suivantes :
   
        show tables;
3. Hello utilisation suivant tooretrieve 10 lignes hello `sample_07` table :
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>Étapes suivantes
* [Découvrez comment toouse Visual Studio avec hello Hortonworks Sandbox](hdinsight-hadoop-emulator-visual-studio.md)
* [Apprentissage des câbles hello Hello Hortonworks Sandbox](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Didacticiel Hadoop - Prise en main de HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

