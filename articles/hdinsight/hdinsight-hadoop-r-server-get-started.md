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
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="6fa7f-103">Commencer à utiliser R Server sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fa7f-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="6fa7f-104">HDInsight inclut une toobe d’option R Server intégré à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="6fa7f-105">Cette option permet à des scripts R toorun distribué des calculs toouse Spark et MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="6fa7f-106">Dans ce document, vous découvrez comment toocreate un serveur R sur le cluster HDInsight, puis sur R script qui montre comment utiliser Spark sur distributed calculs de R.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6fa7f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6fa7f-107">Prerequisites</span></span>

* <span data-ttu-id="6fa7f-108">**Abonnement Azure** : avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="6fa7f-109">Accédez toohello article [gratuite obtenir Microsoft Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="6fa7f-110">**Un client Secure Shell (SSH)**: SSH un client est utilisé tooremotely connecter toohello HDInsight cluster et exécuter des commandes directement sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="6fa7f-111">Pour en savoir plus, consultez [Se connecter à HDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="6fa7f-112">**Clés SSH (facultatifs)**: vous pouvez sécuriser hello SSH compte utilisé tooconnect toohello cluster à l’aide d’un mot de passe ou une clé publique.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="6fa7f-113">À l’aide d’un mot de passe est plus facile et permet de vous tooget démarré sans avoir toocreate une paire de clés publique/privée.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="6fa7f-114">Toutefois, il est plus sûr d’utiliser une clé.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="6fa7f-115">étapes de Hello dans ce document supposent que vous utilisez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="6fa7f-116">Création de cluster automatisée</span><span class="sxs-lookup"><span data-stu-id="6fa7f-116">Automated cluster creation</span></span>

<span data-ttu-id="6fa7f-117">Vous pouvez automatiser la création de hello de HDInsight R Servers à l’aide d’Azure Resource Manager modèles, hello SDK et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="6fa7f-118">toocreate serveur R à l’aide d’un modèle de gestion des ressources Azure, consultez [déployer un cluster HDInsight de serveur R](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="6fa7f-119">toocreate un serveur R à l’aide de hello .NET SDK, consultez [créer des clusters basés sur Linux dans HDInsight à l’aide de hello du SDK .NET.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="6fa7f-120">toodeploy R Server à l’aide de powershell, consultez l’article de hello sur [création d’un serveur de R dans HDInsight avec PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="6fa7f-121">Créer le cluster hello à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="6fa7f-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="6fa7f-122">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="6fa7f-123">Sélectionnez **NOUVEAU** -> **Intelligence et analyse**, -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Image de la création d’un cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="6fa7f-125">Bonjour **création rapide** expérience, entrez un nom pour le cluster de hello Bonjour **nom de Cluster** champ.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="6fa7f-126">Si vous avez plusieurs abonnements Azure, utilisez hello **abonnement** entrée tooselect hello une souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![Sélections de nom et d’abonnement de cluster](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="6fa7f-128">Sélectionnez **Cluster type** tooopen hello **configuration de Cluster** panneau.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="6fa7f-129">Sur hello **Configuration de Cluster** panneau, sélectionnez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="6fa7f-130">**Type de cluster** : R Server</span><span class="sxs-lookup"><span data-stu-id="6fa7f-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="6fa7f-131">**Version**: version select hello de tooinstall R Server sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="6fa7f-132">version de Hello actuellement disponible est ***R Server 9.1 (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="6fa7f-133">Notes de publication pour les versions disponibles de hello du serveur de R sont disponibles [ici](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="6fa7f-134">**Édition de communauté R Studio pour R Server**: cet IDE basé sur le navigateur est installé par défaut sur le nœud de périmètre hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="6fa7f-135">Si vous préférez toonot est installé, puis désactivez la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="6fa7f-136">Si vous choisissez toohave il installé, les URL de hello pour accéder aux hello connexion RStudio Server se trouve sur un panneau de l’application de portail pour votre cluster, une fois qu’il est créé.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="6fa7f-137">Laissez des autres options hello aux valeurs par défaut de hello et utiliser hello **sélectionnez** toosave hello cluster type de bouton.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![Capture d’écran du panneau Type de cluster](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="6fa7f-139">Saisissez un **nom de connexion au cluster** et un **mot de passe de connexion au cluster**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="6fa7f-140">Spécifiez un **nom d’utilisateur SSH**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="6fa7f-141">SSH est utilisé tooremotely se connecter à l’aide du cluster toohello un **Secure Shell (SSH)** client.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="6fa7f-142">Vous pouvez spécifier utilisateur SSH de hello dans cette boîte de dialogue ou après la création du cluster hello (dans l’onglet de Configuration hello pour le cluster de hello).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="6fa7f-143">R Server est configuré tooexpect un **nom d’utilisateur SSH** de « UtilisateurDistant ».</span><span class="sxs-lookup"><span data-stu-id="6fa7f-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="6fa7f-144">**Si vous utilisez un nom d’utilisateur différent, vous devez effectuer une étape supplémentaire après la création du cluster hello.**</span><span class="sxs-lookup"><span data-stu-id="6fa7f-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="6fa7f-145">Laissez hello cases pour **utiliser le même mot de passe en tant que compte de connexion de cluster** toouse **mot de passe** comme hello l’authentification de type, sauf si vous préférez utiliser une clé publique.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="6fa7f-146">Vous avez besoin d’une paire de clés publique/privée de tooaccess R Server sur le cluster hello via un client distant, comme par exemple, RTV, RStudio ou un autre environnement IDE de bureau.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="6fa7f-147">Si vous installez hello édition community de RStudio serveur, vous devez toochoose un mot de passe SSH.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="6fa7f-148">toocreate et utilisez une paire de clés publique/privée, décochez la case **utiliser le même mot de passe en tant que compte de connexion de cluster** , puis sélectionnez **clé publique** et procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="6fa7f-149">Ces instructions supposent que Cygwin avec ssh-keygen ou équivalent est installé.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="6fa7f-150">Générer une paire de clés publique/privée à partir de l’invite de commandes hello sur votre ordinateur portable :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="6fa7f-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="6fa7f-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="6fa7f-152">Suivez hello, tooname demander un fichier de clé, puis entrez une phrase secrète pour une sécurité accrue.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="6fa7f-153">Votre écran doit ressembler à quelque chose comme hello suivant l’image :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-153">Your screen should look something like hello following image:</span></span>

        ![Ligne de commande SSH dans Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="6fa7f-155">Cette commande crée un fichier de clé privée et d’un fichier de clé publique sous hello nom < nom de la clé privée > .pub, par exemple furiosa et furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![SSH dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="6fa7f-157">Puis spécifiez le fichier de clé publique de hello (&#42;. pub) lors de l’affectation HDI informations d’identification du cluster et enfin confirmer votre groupe de ressources, la région et sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Panneau Informations d’identification](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="6fa7f-159">Modifier les autorisations sur le fichier de clé privée hello sur votre ordinateur portable :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="6fa7f-160">chmod 600 <nom-fichier-clé-privée></span><span class="sxs-lookup"><span data-stu-id="6fa7f-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="6fa7f-161">Utiliser le fichier de clé privée hello avec SSH pour la connexion à distance :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="6fa7f-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="6fa7f-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="6fa7f-163">Ou bien, en tant que définition de votre Hadoop Spark hello de partie de contexte de calcul pour R Server sur le client de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="6fa7f-164">Consultez hello **à l’aide de Microsoft R Server comme un Hadoop Client** dans la sous-section [créer un contexte de calcul pour Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="6fa7f-165">Création rapide de Hello vous passe toohello **stockage** compte de stockage panneau tooselect hello toobe de paramètres utilisé pour l’emplacement principal de hello Hello système utilisé par le cluster de hello du fichier HDFS.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="6fa7f-166">Sélectionnez un compte de stockage Azure nouveau ou existant ou un compte de stockage Data Lake existant.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="6fa7f-167">Si vous sélectionnez un compte de stockage Azure, un compte de stockage existant est sélectionné en choisissant **sélectionner un compte de stockage** , puis en sélectionnant le compte de votre choix hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="6fa7f-168">Créer un nouveau compte à l’aide de hello **créer un nouveau** lien Bonjour **sélectionner un compte de stockage** section.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6fa7f-169">Si vous sélectionnez **nouveau** vous devez entrer un nom pour le nouveau compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="6fa7f-170">Une coche verte s’affiche si le nom de hello est accepté.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="6fa7f-171">Hello **conteneur par défaut** nom toohello de valeurs par défaut du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="6fa7f-172">Laissez cette valeur par défaut en tant que valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="6fa7f-173">Si une nouvelle option de compte de stockage a été sélectionnée une invite de commandes tooselect **emplacement** est donné tooselect le toocreate région hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![Panneau Source de données](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="6fa7f-175">Sélectionner l’emplacement de source de données par défaut hello hello définit également l’emplacement hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="6fa7f-176">source de données par défaut et le cluster Hello doit être Bonjour même région.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="6fa7f-177">Si vous voulez toouse un Data Lake Store existant, puis sélectionnez hello toouse de compte de stockage ADLS et ajouter un cluster de hello *ajouter* magasin toohello d’identité tooyour cluster tooallow accès.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="6fa7f-178">Pour plus d’informations sur ce processus, consultez [Créer un cluster HDInsight avec Data Lake Store à l’aide du portail Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="6fa7f-179">Hello d’utilisation **sélectionnez** configuration de source de données bouton toosave hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="6fa7f-180">Hello **Résumé** panneau affiche ensuite toovalidate tous vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="6fa7f-181">Ici, vous pouvez modifier votre **taille de Cluster** toomodify hello du nombre de serveurs de votre cluster et spécifiez **actions de Script** vous souhaitez toorun.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="6fa7f-182">Sauf si vous savez que vous avez besoin d’un cluster plus grand, conservez hello du numéro de nœuds de travail par défaut hello `4`.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="6fa7f-183">Hello estimation de coût de cluster de hello est indiqué dans le panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![Résumé du cluster](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="6fa7f-185">Si nécessaire, vous pouvez redimensionner votre cluster ultérieurement via hello portail (**Cluster** -> **paramètres** -> **échelle Cluster**) tooincrease ou diminuer le nombre hello de nœuds worker.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="6fa7f-186">Ce redimensionnement peut être utile pour ralenti cluster hello inutilisés vers le bas, ou ajouté des besoins en capacité toomeet hello de plus grandes tâches.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="6fa7f-187">Certains tookeep facteurs à l’esprit lors du redimensionnement de votre cluster, des nœuds de données hello et nœud de périmètre hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="6fa7f-188">performances Hello des analyses de R Server distribuées sur Spark est nombre toohello proportionnel de nœuds worker lorsque les données de salutation sont grandes.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="6fa7f-189">performances Hello des analyses de R Server est linéaire taille hello de données en cours d’analyse.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="6fa7f-190">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-190">For example:</span></span>  

     * <span data-ttu-id="6fa7f-191">Pour les données de petite toomodest, les performances sont meilleures lors de l’analyse dans un contexte de calcul local sur le nœud de périmètre hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="6fa7f-192">Pour plus d’informations sur les scénarios de hello sous lequel hello local et Spark contextes de calcul sont satisfaisants, consultez les options de contexte de calcul pour R Server sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="6fa7f-193">Si vous connectez-vous au nœud de périmètre toohello et exécutez votre script R, puis toutes mais hello rx-fonctions ScaleR sont exécutées <strong>localement</strong> sur le nœud de périmètre hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="6fa7f-194">Par conséquent, hello mémoire et nombre de cœurs de nœud de périmètre hello doit être dimensionné en conséquence.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="6fa7f-195">Hello que même règle s’applique si vous utilisez R Server sur HDI comme contexte de calcul à distance à partir de votre ordinateur portable.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Panneau Niveaux de tarification du nœud](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="6fa7f-197">Hello d’utilisation **sélectionnez** nœud de hello bouton toosave configuration de la tarification.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="6fa7f-198">Il existe également un lien permettant de **télécharger le modèle et les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="6fa7f-199">Cliquez sur ce lien toodisplay les scripts qui peuvent être tooautomate utilisé hello la création d’un cluster avec la configuration sélectionnée de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="6fa7f-200">Ces scripts sont également disponibles à partir de hello entrée de portail Azure pour votre cluster une fois qu’elle a été créée.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6fa7f-201">Il prend un certain temps pour hello toobe de cluster créé, généralement environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="6fa7f-202">Utilisez hello vignette sur hello tableau d’accueil ou hello **Notifications** entrée sur hello à gauche de hello page toocheck sur le processus de création de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="6fa7f-203">Se connecter tooRStudio Server</span><span class="sxs-lookup"><span data-stu-id="6fa7f-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="6fa7f-204">Si vous avez choisi tooinclude édition community de RStudio serveur dans votre installation, vous pouvez accéder à connexion de RStudio hello via deux méthodes différentes.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="6fa7f-205">Accédez toohello suivant URL (où **CLUSTERNAME** hello désigne cluster hello que vous avez créé) :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="6fa7f-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="6fa7f-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="6fa7f-207">Ouvrir l’entrée de hello pour votre cluster Bonjour portail Azure, sélectionnez hello **tableaux de bord de serveur R** lien rapide, puis en sélectionnant hello **tableau de bord R Studio**:</span><span class="sxs-lookup"><span data-stu-id="6fa7f-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![Tableau de bord accès hello R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Tableau de bord accès hello R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="6fa7f-210">Quelle que soit la méthode hello utilisée, hello première fois que vous vous connectez vous devez tooauthenticate à deux reprises.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="6fa7f-211">À la première authentification de hello, fournir hello *nom d’utilisateur administrateur de cluster* et *mot de passe*.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="6fa7f-212">À l’invite de deuxième hello, fournir hello *SSH userid* et *mot de passe*.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="6fa7f-213">Fichier journal suivante ins nécessitent uniquement hello *mot de passe SSH* et *userid*.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="6fa7f-214">Connecter le nœud de périmètre toohello R Server</span><span class="sxs-lookup"><span data-stu-id="6fa7f-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="6fa7f-215">Connecter le nœud du bord tooR serveur du cluster HDInsight de hello à l’aide de SSH avec la commande hello :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="6fa7f-216">Vous pouvez trouver hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` adresse Bonjour portail Azure en sélectionnant votre cluster puis **tous les paramètres** -> **applications** -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="6fa7f-217">Cette opération affiche hello les informations de point de terminaison SSH pour le nœud de périmètre hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Image de hello point de terminaison SSH pour le nœud de périmètre hello](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="6fa7f-219">Si vous avez utilisé un toosecure de mot de passe de votre compte d’utilisateur SSH, vous êtes invité à tooenter il.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="6fa7f-220">Si vous avez utilisé une clé publique, vous avez peut-être toouse hello `-i` paramètre toospecify hello la clé privée correspondante.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="6fa7f-221">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="6fa7f-222">Pour plus d’informations, consultez [connecter tooHDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="6fa7f-223">Une fois connecté, vous accédez à une invite de commandes suivant de toohello similaire :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="6fa7f-224">Autoriser plusieurs utilisateurs simultanés</span><span class="sxs-lookup"><span data-stu-id="6fa7f-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="6fa7f-225">Vous pouvez activer plusieurs utilisateurs simultanément en ajoutant de nouveaux utilisateurs pour le nœud de périmètre hello sur quel hello RStudio Communauté version s’exécute.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="6fa7f-226">Lorsque vous créez un cluster HDInsight, vous devez fournir deux utilisateurs, un utilisateur HTTP et un utilisateur SSH :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Utilisateur simultané n° 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="6fa7f-228">**Nom d’utilisateur de cluster**: un utilisateur HTTP pour l’authentification via la passerelle HDInsight hello qui est utilisé tooprotect hello HDInsight de clusters que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="6fa7f-229">Cet utilisateur HTTP est utilisé tooaccess hello Ambari UI, l’interface utilisateur des fils, ainsi que les autres composants d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="6fa7f-230">**Nom d’utilisateur de Shell (SSH) sécurisée**: un cluster de hello SSH utilisateur tooaccess via le shell sécurisé.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="6fa7f-231">Cet utilisateur est un utilisateur de hello système Linux pour tous les nœuds de bord, les nœuds de travail et les nœuds principaux hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="6fa7f-232">Vous pouvez donc utiliser shell sécurisé tooaccess un des nœuds de hello dans un cluster à distance.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="6fa7f-233">version de R Studio Server Community Hello utilisée Bonjour Microsoft R Server sur un cluster de type HDInsight accepte uniquement le nom d’utilisateur Linux et mot de passe comme mécanisme de connexion.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="6fa7f-234">Elle ne prend pas en charge le passage de jetons.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-234">It does not support passing tokens.</span></span> <span data-ttu-id="6fa7f-235">Par conséquent, si vous avez créé un nouveau cluster et que vous souhaitez toouse R Studio tooaccess, vous devez toolog dans deux fois.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="6fa7f-236">Commencez par vous connecter à l’aide des informations d’identification utilisateur de hello HTTP via hello HDInsight passerelle :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![Utilisateur simultané 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="6fa7f-238">Puis utilisez hello SSH utilisateur informations d’identification toolog dans tooRStudio :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![Utilisateur simultané 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="6fa7f-240">Actuellement, on ne peut créer qu’un seul compte d’utilisateur SSH lors de l’approvisionnement d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="6fa7f-241">Afin de clusters de plusieurs utilisateurs tooaccess Microsoft R Server sur HDInsight tooenable, nous devons toocreate des utilisateurs supplémentaires dans hello système Linux.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="6fa7f-242">Étant donné que RStudio Server Community est en cours d’exécution sur le nœud de bord du cluster hello, il existe plusieurs étapes :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="6fa7f-243">Utilisez hello créé SSH utilisateur toolog toohello bord nœud</span><span class="sxs-lookup"><span data-stu-id="6fa7f-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="6fa7f-244">Ajouter d’autres utilisateurs Linux dans le nœud de périmètre</span><span class="sxs-lookup"><span data-stu-id="6fa7f-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="6fa7f-245">Utiliser la version Community de RStudio avec créés par l’utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="6fa7f-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="6fa7f-246">Étape 1 : Utiliser hello créé SSH utilisateur toolog dans le nœud de périmètre toohello</span><span class="sxs-lookup"><span data-stu-id="6fa7f-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="6fa7f-247">Télécharger n’importe quel outil SSH (tel que Putty) et utiliser hello toolog utilisateur SSH existant dans.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="6fa7f-248">Puis suivez les instructions de hello fournies dans [connecter tooHDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello nœud de périmètre.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="6fa7f-249">adresse du nœud bord Hello pour R Server sur le cluster HDInsight est : *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="6fa7f-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="6fa7f-250">Étape n° 2 : Ajouter d’autres utilisateurs Linux dans le nœud de périmètre</span><span class="sxs-lookup"><span data-stu-id="6fa7f-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="6fa7f-251">tooadd un nœud de périmètre toohello utilisateur, exécutez les commandes de hello :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="6fa7f-252">Vous devez voir hello retournés des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-252">You should see hello following items returned:</span></span> 

![Utilisateur simultané 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="6fa7f-254">Lorsque vous y êtes invité pour « mot de passe actuel Kerberos : », appuyez simplement sur **entrée** tooignore il.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="6fa7f-255">Hello `-m` option `useradd` commande indique que le système de hello créera un dossier de base pour l’utilisateur hello, qui est requis pour la version de communauté de RStudio.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="6fa7f-256">Étape 3 : Version utilisez RStudio Communauté créés par l’utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="6fa7f-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="6fa7f-257">Utilisez hello créés par l’utilisateur toolog dans tooRStudio :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-257">Use hello user created toolog in tooRStudio:</span></span>

![Utilisateur simultané 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="6fa7f-259">Notez que RStudio indique que vous utilisez le nouvel utilisateur de hello (ici, par exemple, *sshuser6*) toolog dans un cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![Utilisateur simultané 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="6fa7f-261">Vous pouvez également vous connecter à l’aide des informations d’identification d’origine de hello (par défaut, il est *sshuser*) simultanément à partir d’une autre fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="6fa7f-262">Vous pouvez soumettre un travail à l’aide des fonctions ScaleR.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="6fa7f-263">Voici un exemple de hello commandes utilisées toorun une tâche :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-263">Here is an example of hello commands used toorun a job:</span></span>

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


<span data-ttu-id="6fa7f-264">Notez que les travaux hello soumis sont sous différents noms d’utilisateur dans l’interface utilisateur des fils :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![Utilisateur simultané 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="6fa7f-266">Notez également que hello nouvellement ajouté utilisateurs n’ont pas des droits racines dans le système Linux, mais ils hello même accéder à des fichiers hello tooall hello HDFS et WASB le stockage étendu.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="6fa7f-267">Utilisez la console hello R</span><span class="sxs-lookup"><span data-stu-id="6fa7f-267">Use hello R console</span></span>

1. <span data-ttu-id="6fa7f-268">À partir de la session SSH hello, utilisez hello suivant la console de commande toostart hello R :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="6fa7f-269">Vous devez voir s’afficher sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="6fa7f-270">R version 3.2.2 (2015-08-14)--« Sécurité incendie » Copyright (C) 2015 hello R Foundation pour une plate-forme statistique : x86_64-pc-linux-gnu (64 bits)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="6fa7f-271">R est un logiciel gratuit et est fourni SANS AUCUNE GARANTIE.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="6fa7f-272">Vous êtes tooredistribute Bienvenue sous certaines conditions.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="6fa7f-273">Tapez ’license()’ ou ’licence()’ pour obtenir des informations relatives à la distribution.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="6fa7f-274">Prise en charge du langage naturel, mais exécution dans un paramètre régional anglais</span><span class="sxs-lookup"><span data-stu-id="6fa7f-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="6fa7f-275">R est un projet de collaboration avec de nombreux contributeurs.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="6fa7f-276">Pour plus d’informations et 'citation()' de type 'contributors()' sur comment toocite R ou R packages dans les publications.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="6fa7f-277">Tapez 'demo()' pour certaines des démonstrations, les « help() » de l’aide en ligne ou 'help.start()' pour un toohelp d’interface de navigateur HTML.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="6fa7f-278">Tapez 'q()' tooquit R.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="6fa7f-279">Microsoft R Server version 8.0 : une distribution avancée des packages Microsoft R Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="6fa7f-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="6fa7f-280">Tapez ’readme()’ pour consulter les notes de publication.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="6fa7f-281">À partir de hello `>` invite de commandes, vous pouvez entrer le code R.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="6fa7f-282">Serveur R inclut des packages qui vous permettent de tooeasily interagissent avec Hadoop et exécuter des calculs distribuées.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="6fa7f-283">Par exemple, utilisez hello suivant racine de hello tooview commande hello par défaut du système de fichiers pour le cluster HDInsight de hello :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="6fa7f-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="6fa7f-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="6fa7f-285">Vous pouvez également utiliser l’adressage de hello WASB style.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="6fa7f-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="6fa7f-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="6fa7f-287">À l’aide de R Server sur HDI à partir d’une instance distante de Microsoft R serveur ou Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="6fa7f-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="6fa7f-288">Il est possible tooset contexte de calcul HDI Hadoop Spark accès toohello à partir d’une instance distante de Microsoft R Server ou Microsoft R Client en cours d’exécution sur le bureau ou portable.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="6fa7f-289">Consultez **à l’aide de Microsoft R Server comme un Hadoop Client** sous-section Bonjour [création d’un contexte de calcul pour Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="6fa7f-290">toodo, vous pouvez donc hello toospecify options suivantes lors de la définition du contexte de calcul hello RxSpark sur votre ordinateur portable : hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches et sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="6fa7f-291">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-291">For example:</span></span>


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


## <a name="use-a-compute-context"></a><span data-ttu-id="6fa7f-292">Utiliser un contexte de calcul</span><span class="sxs-lookup"><span data-stu-id="6fa7f-292">Use a compute context</span></span>

<span data-ttu-id="6fa7f-293">Un contexte de calcul vous permet de toocontrol si le calcul est effectué localement sur le nœud de périmètre hello ou répartis entre les nœuds hello dans le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="6fa7f-294">À partir de RStudio hello R la console serveur ou (dans une session SSH), utilisez hello suivant des données d’exemple de code tooload dans le stockage par défaut de hello pour HDInsight :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

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

2. <span data-ttu-id="6fa7f-295">Ensuite, créez des informations de données et définir les deux sources de données afin que nous pouvons utiliser les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

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

3. <span data-ttu-id="6fa7f-296">Nous allons exécuter une régression logistique sur les données hello à l’aide du contexte de calcul local hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="6fa7f-297">Vous devez voir la sortie qui se termine par toohello similaire de lignes suivant :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-297">You should see output that ends with lines similar toohello following:</span></span>

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

4. <span data-ttu-id="6fa7f-298">Ensuite, nous allons exécuter hello même régression logistique à l’aide du contexte de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="6fa7f-299">contexte de Spark Hello distribue hello de traitement sur tous les nœuds de travail hello dans le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

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
   > <span data-ttu-id="6fa7f-300">Vous pouvez également utiliser MapReduce toodistribute calcul entre les nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="6fa7f-301">Pour plus d’informations sur le contexte de calcul, consultez [Options de contexte de calcul pour R Server sur HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="6fa7f-302">Distribuer des nœuds de toomultiple code R</span><span class="sxs-lookup"><span data-stu-id="6fa7f-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="6fa7f-303">Avec R Server, vous pouvez facilement utiliser le code R existant et l’exécuter sur plusieurs nœuds de cluster de hello à l’aide de `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="6fa7f-304">Cette fonction est utile lors d’un balayage paramétrique ou lorsque vous effectuez des simulations.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="6fa7f-305">Hello de code suivant est un exemple de procédure toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="6fa7f-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="6fa7f-306">Si vous utilisez encore hello Spark ou MapReduce contexte, cette commande renvoie ce code hello valeur nodename de hello pour les nœuds de travail hello `(Sys.info()["nodename"])` s’exécute.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="6fa7f-307">Par exemple, sur un cluster à quatre nœuds, vous vous attendez tooreceive sortie similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

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


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="6fa7f-308">Accès aux données dans Hive et Parquet</span><span class="sxs-lookup"><span data-stu-id="6fa7f-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="6fa7f-309">Une fonctionnalité disponible dans R Server 9.1 permet toodata un accès direct dans la ruche et Parquet pour une utilisation par les fonctions ScaleR dans le contexte de calcul hello Spark.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="6fa7f-310">Ces fonctionnalités sont disponibles via les nouvelles données source fonctions ScaleR appelées RxHiveData et RxParquetData qui fonctionnent à l’aide de données de tooload Spark SQL directement dans une trame de données pour l’analyse par ScaleR Spark.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="6fa7f-311">Hello suivant code fournit un exemple de code sur l’utilisation de nouvelles fonctions de hello :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-311">hello following code provides some sample code on use of hello new functions:</span></span>

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


<span data-ttu-id="6fa7f-312">Pour des informations supplémentaires sur l’utilisation de ces nouvelles fonctions, consultez hello aide en ligne de R Server via l’utilisation de hello `?RxHivedata` et `?RxParquetData` commandes.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="6fa7f-313">Installer des packages R supplémentaires sur le nœud de périmètre hello</span><span class="sxs-lookup"><span data-stu-id="6fa7f-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="6fa7f-314">Si vous souhaitez que tooinstall des packages R supplémentaires sur le nœud de périmètre hello, vous pouvez utiliser `install.packages()` directement depuis hello console R lorsque toohello connecté bord nœud via SSH.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="6fa7f-315">Toutefois, si vous avez besoin des packages R tooinstall sur les nœuds de travail hello du cluster de hello, vous devez utiliser une Action de Script.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="6fa7f-316">Actions de script sont des scripts Bash toomake utilisé configuration modifications toohello HDInsight cluster ou tooinstall logiciels supplémentaires, telles que les packages R supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="6fa7f-317">les packages supplémentaires tooinstall à l’aide d’une Action de Script, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fa7f-318">À l’aide des packages R supplémentaires Actions de Script tooinstall utilisable uniquement après que hello cluster a été créé.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="6fa7f-319">N’utilisez pas cette procédure pendant la création du cluster, comme le script de hello s’appuie sur le serveur R en cours complètement installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="6fa7f-320">À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre serveur R sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="6fa7f-321">À partir de hello **paramètres** panneau, sélectionnez **Actions de Script** , puis **soumettre de nouvelles** toosubmit une nouvelle Action de Script.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![Image du panneau Actions de script](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="6fa7f-323">À partir de hello **envoyer l’action de script** panneau, fournir hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="6fa7f-324">**Nom**: un nom convivial de la nommer tooidentify ce script</span><span class="sxs-lookup"><span data-stu-id="6fa7f-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="6fa7f-325">**URI de script bash** : `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="6fa7f-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="6fa7f-326">**En-tête** : cet élément doit être **décoché**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="6fa7f-327">**Worker** : cet élément doit être **coché**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="6fa7f-328">**Nœuds de périmètre** : cet élément doit être **décoché**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="6fa7f-329">**Zookeeper** : cet élément doit être **décoché**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="6fa7f-330">**Paramètres**: hello R packages toobe installé.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="6fa7f-331">Par exemple, `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="6fa7f-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="6fa7f-332">**Conservez cette action de script...** : cet élément doit être **coché**.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="6fa7f-333">Par défaut, tous les packages R sont installés à partir d’un instantané du référentiel de Microsoft MRAN hello cohérent avec la version de hello du serveur R qui a été installé.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="6fa7f-334">Si vous souhaitez tooinstall les versions plus récentes des packages, il est certains risques d’incompatibilité.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="6fa7f-335">Ce type d’installation est toutefois possible en spécifiant `useCRAN` comme hello premier élément du package de hello répertorier, par exemple `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="6fa7f-336">Certains packages R nécessitent des bibliothèques de système Linux supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="6fa7f-337">Pour plus de commodité, nous avons préinstallé dépendances hello requis par hello top 100 packages R plus populaires.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="6fa7f-338">Toutefois, si vous installez le hello R ou nécessite des bibliothèques au-delà de ces vous devez télécharger le script de base hello utilisé ici et ajouter des étapes tooinstall hello système bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="6fa7f-339">Vous devez ensuite téléchargement hello modifié script tooa public blob du conteneur dans le stockage Azure et utiliser des packages de hello modifié script tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="6fa7f-340">Pour plus d’informations sur le développement d’actions de script, consultez la section [Développer des actions de script](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Ajout d’une action de script](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="6fa7f-342">Sélectionnez **créer** script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="6fa7f-343">Une fois que l’achèvement du script de hello, hello R sont disponibles sur tous les nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="6fa7f-344">Utilisation de l’opérationnalisation de Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="6fa7f-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="6fa7f-345">Lors de la modélisation des données est terminée, vous pouvez tiens prédictions toomake du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="6fa7f-346">tooconfigure pour à l’Opérationnalisation Microsoft R Server, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="6fa7f-347">Tout d’abord, ssh dans le nœud de périmètre hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="6fa7f-348">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="6fa7f-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="6fa7f-349">Une fois à l’aide de ssh, remplacez le répertoire pour la version appropriée de hello et sudo hello dotnet dll :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="6fa7f-350">Pour Microsoft R Server 9.1 :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="6fa7f-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="6fa7f-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="6fa7f-352">Pour Microsoft R Server 9.0 :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="6fa7f-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="6fa7f-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="6fa7f-354">à l’Opérationnalisation tooconfigure Microsoft R Server avec une configuration d’une case hello suivant :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="6fa7f-355">Sélectionnez « Configure R Server for Operationalization » (Configurer R Server pour l’opérationnalisation).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="6fa7f-356">Sélectionnez « A.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-356">Select “A.</span></span> <span data-ttu-id="6fa7f-357">One-box (web + compute nodes) » (Solution complète + nœuds de calcul).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="6fa7f-358">Entrez un mot de passe hello **admin** utilisateur</span><span class="sxs-lookup"><span data-stu-id="6fa7f-358">Enter a password for hello **admin** user</span></span>

![opérationnalisation complète](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="6fa7f-360">Vous pouvez éventuellement effectuer les vérifications de diagnostic en exécutant un test de diagnostic, comme suit :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="6fa7f-361">Sélectionnez « 6.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-361">Select “6.</span></span> <span data-ttu-id="6fa7f-362">Exécuter des tests de diagnostic ».</span><span class="sxs-lookup"><span data-stu-id="6fa7f-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="6fa7f-363">Sélectionnez « A.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-363">Select “A.</span></span> <span data-ttu-id="6fa7f-364">Configuration de test ».</span><span class="sxs-lookup"><span data-stu-id="6fa7f-364">Test configuration”</span></span>
3. <span data-ttu-id="6fa7f-365">Entrez le nom d’utilisateur = « admin » et le mot de passe de l’étape de configuration précédente.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="6fa7f-366">Confirmez l’intégrité globale = pass.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="6fa7f-367">Hello quitter utilitaire d’administration</span><span class="sxs-lookup"><span data-stu-id="6fa7f-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="6fa7f-368">Quittez SSH.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-368">Exit SSH</span></span>

![Diagnostics pour l’opérationnalisation](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="6fa7f-370">**Retards importants lors de l’utilisation d’un service web sur Spark**</span><span class="sxs-lookup"><span data-stu-id="6fa7f-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="6fa7f-371">Si vous rencontrez un retard lors de la tentative de tooconsume un service web créé avec des fonctions mrsdeploy dans un contexte de calcul Spark, vous devrez peut-être tooadd certains dossiers manquants.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="6fa7f-372">Hello application de Spark appartient utilisateur tooa appelé '*rserve2*' chaque fois qu’il est appelé à partir d’un service web à l’aide des fonctions de mrsdeploy.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="6fa7f-373">toowork résoudre ce problème :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="6fa7f-374">À ce stade, la configuration à l’Opérationnalisation hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="6fa7f-375">Vous pouvez désormais utiliser hello 'mrsdeploy' du package sur votre toohello de tooconnect RClient à l’Opérationnalisation sur le nœud de périmètre et commencer à utiliser ses fonctionnalités comme [l’exécution à distance](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) et [services web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="6fa7f-376">Selon que votre cluster est configuré sur un réseau virtuel ou non, vous devrez peut-être tooset de port vers l’avant tunneling via la connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="6fa7f-377">Hello sections suivantes expliquent comment tooset de ce tunnel.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="6fa7f-378">Cluster RServer sur un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6fa7f-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="6fa7f-379">Assurez-vous que vous autorisez le trafic via le nœud de port 12800 toohello edge.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="6fa7f-380">De cette façon, vous pouvez utiliser la fonctionnalité à l’Opérationnalisation hello bord nœuds tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="6fa7f-381">Si hello `remoteLogin()` ne peut pas se connecter toohello de nœud de périmètre, mais vous pouvez le nœud de périmètre toohello SSH, vous devez tooverify si hello règle tooallow le trafic sur le port 12800 a été défini correctement ou non.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="6fa7f-382">Si vous continuez le problème de hello tooface, vous pouvez contourner il en configurant le transfert port le tunneling forcé via SSH.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="6fa7f-383">Pour obtenir des instructions, consultez hello suivant la section.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="6fa7f-384">Cluster RServer non configuré sur un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6fa7f-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="6fa7f-385">Si votre cluster n’est pas configuré sur un réseau virtuel ou si vous rencontrez des problèmes de connectivité via un réseau virtuel, vous pouvez utiliser le tunneling de réacheminement du port SSH :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="6fa7f-386">Vous pouvez également le configurer sur PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-386">On Putty, you can set it up as well.</span></span>

![connexion SSH PuTTY](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="6fa7f-388">Une fois votre session SSH est active, le trafic de hello du port de votre ordinateur 12800 est transféré le port du nœud toohello bord 12800 via une session SSH.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="6fa7f-389">Vérifiez que vous utilisez `127.0.0.1:12800` dans votre méthode `remoteLogin()`.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="6fa7f-390">Il se connecte à l’Opérationnalisation du nœud toohello bord via le réacheminement de port.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="6fa7f-391">Comment tooscale à l’Opérationnalisation Microsoft R Server les nœuds de calcul sur les nœuds de travail HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fa7f-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="6fa7f-392">Mettre hors service ou les nœuds worker hello</span><span class="sxs-lookup"><span data-stu-id="6fa7f-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="6fa7f-393">Microsoft R Server n’est actuellement pas géré par YARN.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="6fa7f-394">Si les nœuds de travail hello ne sont pas retirés, hello fils le Gestionnaire de ressources ne fonctionnera pas comme prévu, car elle ne sera pas connaissance des ressources hello est pris en charge par le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="6fa7f-395">Dans l’ordre tooavoid cette situation, nous vous recommandons de désaffectation des nœuds de travail hello avant d’étendre les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="6fa7f-396">Nœuds de travail toodecommissioning comme suit :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="6fa7f-397">Ouvrez une session dans la console du cluster tooHDI Ambari, puis cliquez sur l’onglet « hosts »</span><span class="sxs-lookup"><span data-stu-id="6fa7f-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="6fa7f-398">Sélectionnez les nœuds de travail (toobe désactivé), cliquez sur « Actions » > « Sélectionné les ordinateurs hôtes » > « Hosts » > cliquez sur « Activer le Mode de Maintenance ON ».</span><span class="sxs-lookup"><span data-stu-id="6fa7f-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="6fa7f-399">Par exemple, Bonjour suivant l’image, nous avons sélectionné toodecommission wn3 et wn4.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![Désactiver les nœuds Worker](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="6fa7f-401">Sélectionnez **Actions** > **Hôtes sélectionnés** > **DataNodes** > cliquez sur **Désactiver**</span><span class="sxs-lookup"><span data-stu-id="6fa7f-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="6fa7f-402">Sélectionnez **Actions** > **Hôtes sélectionnés** > **NodeManagers** > cliquez sur **Désactiver**</span><span class="sxs-lookup"><span data-stu-id="6fa7f-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="6fa7f-403">Sélectionnez **Actions** > **Hôtes sélectionnés** > **DataNodes** > cliquez sur **Arrêter**</span><span class="sxs-lookup"><span data-stu-id="6fa7f-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="6fa7f-404">Sélectionnez **Actions** > **Hôtes sélectionnés** > **NodeManagers** > cliquez sur **Arrêter**</span><span class="sxs-lookup"><span data-stu-id="6fa7f-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="6fa7f-405">Sélectionnez **Actions** > **Hôtes sélectionnés** > **Hôtes** > cliquez sur **Stop All Components** (Arrêter tous les composants)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="6fa7f-406">Désélectionnez les nœuds de travail hello et sélectionnez les nœuds principaux hello</span><span class="sxs-lookup"><span data-stu-id="6fa7f-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="6fa7f-407">Sélectionnez **Actions** > **Hôtes sélectionnés** > **Hôtes** > **Restart All Components** (Redémarrer tous les composants)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="6fa7f-408">Configurer les nœuds de calcul sur chaque nœud Worker désactivé</span><span class="sxs-lookup"><span data-stu-id="6fa7f-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="6fa7f-409">Utilisez SSH dans chaque nœud Worker désactivé.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="6fa7f-410">Exécutez l’utilitaire d’administration à l’aide de `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="6fa7f-411">Entrez « 1 » tooselect option « Configurer R Server pour à l’Opérationnalisation ».</span><span class="sxs-lookup"><span data-stu-id="6fa7f-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="6fa7f-412">Entrez l’option « c » tooselect C. »</span><span class="sxs-lookup"><span data-stu-id="6fa7f-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="6fa7f-413">Nœud de calcul ».</span><span class="sxs-lookup"><span data-stu-id="6fa7f-413">Compute node".</span></span> <span data-ttu-id="6fa7f-414">Cela configure le nœud de calcul hello sur le nœud de travail hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="6fa7f-415">Hello de sortie utilitaire d’administration.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="6fa7f-416">Ajouter des détails sur les nœuds de calcul sur le nœud web</span><span class="sxs-lookup"><span data-stu-id="6fa7f-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="6fa7f-417">Après ont configuré tous les nœuds de travail retirés toorun nœud de calcul, revenez sur le nœud de périmètre hello et ajouter des adresses IP des nœuds de travail retirés dans la configuration du nœud hello Microsoft R Server web :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="6fa7f-418">SSH dans le nœud de périmètre hello.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="6fa7f-419">Exécutez `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="6fa7f-420">Recherchez hello section de « URI » et ajoutez IP du nœud de travail et les détails du port.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![Ligne de commande Désactiver les nœuds Worker](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="6fa7f-422">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="6fa7f-422">Troubleshoot</span></span>

<span data-ttu-id="6fa7f-423">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="6fa7f-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="6fa7f-424">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fa7f-424">Next steps</span></span>

<span data-ttu-id="6fa7f-425">Maintenant, vous devez comprendre comment toocreate un nouveau cluster HDInsight qui inclut les principes élémentaires de R Server et hello hello de l’utilisation de hello console R à partir d’une session SSH.</span><span class="sxs-lookup"><span data-stu-id="6fa7f-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="6fa7f-426">Hello rubriques suivantes expliquent autres méthodes de gestion et l’utilisation de R Server sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="6fa7f-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="6fa7f-427">Ajouter RStudio Server tooHDInsight (si ne pas installé lors de la création du cluster)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="6fa7f-428">Options de contexte de calcul pour R Server sur HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="6fa7f-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="6fa7f-429">Options d’Azure Storage pour R Server sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fa7f-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
