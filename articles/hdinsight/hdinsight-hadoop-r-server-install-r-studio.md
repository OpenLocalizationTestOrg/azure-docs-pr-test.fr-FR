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
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>Installation de RStudio avec R Server sur HDInsight

Cet article décrit comment tooinstall hello version (gratuit) communautaire de [RStudio Server](https://www.rstudio.com/products/rstudio-server/) sur le nœud de périmètre hello d’un cluster à l’aide d’un script personnalisé. RStudio Server fournit un IDE sur navigateur utilisable par des clients distants ; il est très répandu sous Linux. Il existe actuellement plusieurs environnements de développement intégré (IDE) disponibles pour R, notamment :

- [Outils R pour Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) de Microsoft ; 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) ; 
- [StatET](http://www.walware.de/goto/statet) sur Eclipse de WalWare.

avantages de Hello de l’installation de serveur de RStudio sur le nœud de périmètre hello d’un cluster HDInsight sont qu’il offre une expérience complète de l’IDE pour le développement de hello et de l’exécution de scripts R R Server sur le cluster de hello. Cette configuration peut être considérablement plus productive à utiliser par défaut de hello Console R.

> [!NOTE]
> Hello procédure décrite dans cet article est uniquement pertinente si vous n’avez pas sélectionné tooinstall édition community de RStudio serveur lors de la configuration de votre cluster. Si vous l’avez ajouté pendant la configuration, puis les tooaccess il vous cliquez sur hello **tableaux de bord de serveur R** vignette Bonjour Azure entrée portail pour votre cluster, puis sur hello **R Studio Server** vignette. 

Si vous préférez toouse hello commerciale sous licence Pro version du serveur de RStudio, vous devez suivre des instructions d’installation à partir de hello [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).

> [!NOTE]
> Si vous utilisez un cluster HDInsight pour lequel R a été installé à l’aide de hello [installer une Action de Script R](hdinsight-hadoop-r-scripts-linux.md), étapes hello dans ce document ne fonctionneront pas correctement car elles nécessitent un serveur R sur le cluster HDInsight de hello.
>
> 

## <a name="prerequisites"></a>Composants requis

* Un cluster Azure HDInsight avec R Server installé. Pour obtenir des instructions, consultez la page [Prise en main de R Server sur les clusters HDInsight](hdinsight-hadoop-r-server-get-started.md).
* Un client SSH. Pour les distributions Linux et Unix ou Macintosh OS X, hello `ssh` commande est fournie avec le système d’exploitation de hello. Pour Windows, nous vous recommandons de [Cygwin](http://www.redhat.com/services/custom/cygwin/) avec hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), ou [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>Installer RStudio sur cluster hello à l’aide d’un script personnalisé

Voici les étapes hello :

1. Identifier le nœud de périmètre hello du cluster de hello. Pour un cluster HDInsight avec R Server, voici convention d’affectation de noms de hello pour le nœud principal et le nœud de périmètre.
   * Nœud principal `CLUSTERNAME-ssh.azurehdinsight.net`
   * Nœud de périmètre `CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. SSH dans le nœud de périmètre hello du cluster hello à l’aide du modèle d’affectation de noms de hello fourni à l’étape 1. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Une fois que vous êtes connecté, devenir un utilisateur racine sur le cluster de hello. Dans la session SSH hello, utilisez hello de commande suivante :

        sudo su -

4. Télécharger un script personnalisé de hello tooinstall RStudio. Utilisez hello de commande suivante :

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Modifier les autorisations de hello sur le fichier de script personnalisé hello et exécuter le script de hello. Utilisez hello suivant de commandes :

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. Si vous avez utilisé un mot de passe SSH lors de la création d’un cluster HDInsight avec R Server, vous pouvez ignorer cette étape et passez toohello ensuite. Si vous avez utilisé une clé SSH à la place cluster hello de toocreate, vous devez définir un mot de passe pour votre utilisateur SSH. Vous avez besoin de ce mot de passe lors de la connexion tooRStudio. Exécutez hello suivant de commandes :

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. Lorsque vous êtes invité à entrer le **Mot de passe Kerberos actuel**, appuyez sur **ENTRÉE**.  Notez que vous devez remplacer `USERNAME` par un utilisateur SSH pour votre cluster HDInsight. Si votre mot de passe est correctement défini, vous devez voir hello message suivant :

        passwd: password updated successfully

    Quittez la session SSH hello.

8. Créer un cluster de toohello tunnel SSH en mappant `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` sur hello HDInsight le cluster toohello ordinateur du client. Vous devez créer un tunnel SSH avant d’ouvrir une nouvelle session de navigateur.

   * Sur un client Linux ou un client Windows avec [Cygwin](http://www.redhat.com/services/custom/cygwin/), ouvrez une session Terminal Server et utiliser hello de commande suivante :

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       Remplacez **nom d’utilisateur** à un utilisateur SSH pour votre cluster HDInsight, puis remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight.
       Vous pouvez également utiliser une clé SSH plutôt qu’un mot de passe en ajoutant `-i id_rsa_key`.        
   * Si vous utilisez un client Windows avec PuTTY

     1. Ouvrez PuTTY et saisissez vos informations de connexion.
     2. Bonjour **catégorie** toohello de la section gauche de la boîte de dialogue hello, développez **connexion**, développez **SSH**, puis sélectionnez **Tunnels**.
     3. Fournir hello suivant les informations de hello **réacheminement de port Options contrôlant SSH** formulaire :

        * **Port source** -hello port client hello que vous souhaitez tooforward. Par exemple, **8787**.
        * **Destination** - hello destination doit être mappée ordinateur du client local toohello. Par exemple, **localhost:8787**.

            ![Création d’un tunnel SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Création d’un tunnel SSH")

     4. Cliquez sur **ajouter** tooadd hello paramètres, puis cliquez sur **ouvrir** tooopen une connexion SSH.
     5. Lorsque vous y êtes invité, connectez-vous toohello server tooestablish un tunnel hello SSH la session et l’activer.

9. Ouvrez un navigateur web, puis entrez hello suivant URL basée sur le port hello que vous avez entré pour un tunnel de hello :

        http://localhost:8787/ 

10. Vous êtes invité à tooenter hello SSH nom d’utilisateur et mot de passe tooconnect toohello cluster. Si vous avez utilisé une clé SSH lors de la création du cluster de hello, vous devez entrer un mot de passe hello créé à l’étape 5.

    ![Se connecter tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "créer un tunnel SSH")

11. tootest si hello RStudio installation a réussi, vous pouvez exécuter un script de test qui exécute des tâches de MapReduce et Spark R sur le cluster de hello. toodownload hello test script toorun dans RStudio, revenez en arrière toohello SSH console, puis entrez hello suivant de commandes :

    *    Si vous avez créé un cluster Hadoop avec R, utilisez cette commande :

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    Si vous avez créé un cluster Spark avec R, utilisez cette commande :

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. Dans RStudio, vous voyez hello tester le script que vous avez téléchargé. Double-cliquez sur hello fichier tooopen, sélectionnez le contenu du fichier de hello hello, puis cliquez sur **exécuter**. Vous devez voir la sortie hello Bonjour **Console** volet :

   ![Tester l’installation de hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "tester hello installation")

Une autre option serait tootype `source(testhdi.r)` ou `source(testhdi_spark.r)` script de hello tooexecute.

## <a name="see-also"></a>Voir aussi

* [Calcul d’options de contexte pour R Server sur les clusters HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)
* [Options d’Azure Storage pour R Server sur HDInsight](hdinsight-hadoop-r-server-storage.md)

