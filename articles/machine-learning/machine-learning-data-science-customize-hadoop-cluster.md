---
title: "aaaCustomize Hadoop clusters pour hello processus de science des données équipe | Documents Microsoft"
description: "Modules de Python populaires disponibles dans les clusters Hadoop Azure HDInsight personnalisés."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="952fa-103">Personnaliser les clusters Azure HDInsight Hadoop pour hello processus de science des données équipe</span><span class="sxs-lookup"><span data-stu-id="952fa-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="952fa-104">Cet article décrit comment toocustomize un HDInsight Hadoop de cluster en installant 64 bits Anaconda (Python 2.7) sur chaque nœud lorsque le cluster de hello est approvisionné comme un service HDInsight.</span><span class="sxs-lookup"><span data-stu-id="952fa-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="952fa-105">Il montre également comment tooaccess hello cluster toohello de nœud principal toosubmit des tâches personnalisées.</span><span class="sxs-lookup"><span data-stu-id="952fa-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="952fa-106">Cette personnalisation permet de nombreux modules Python populaires, qui sont inclus dans Anaconda, facilement disponibles pour une utilisation dans utilisateur défini les fonctions qui sont conçues tooprocess enregistrements Hive dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="952fa-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="952fa-107">Pour obtenir des instructions sur les procédures de hello utilisées dans ce scénario, consultez [comment les requêtes Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="952fa-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="952fa-108">Hello menu suivant lie tootopics qui décrivent comment tooset des hello différents environnements de science des données utilisé par hello [processus de science des données équipe (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="952fa-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="952fa-109"><a name="customize"></a>Personnaliser le cluster Hadoop Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="952fa-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="952fa-110">toocreate un cluster HDInsight Hadoop personnalisé, commencez par session trop[**portail Azure classic**](https://manage.windowsazure.com/), cliquez sur **nouveau** à gauche de hello coin inférieur, puis sélectionnez les SERVICES de données -> HDINSIGHT -> **création personnalisée** toobring des hello **détails du Cluster** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="952fa-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="952fa-112">Nom hello de hello toobe de cluster créé sur la page 1 de la configuration d’entrée et acceptez les valeurs par défaut pour hello autres champs.</span><span class="sxs-lookup"><span data-stu-id="952fa-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="952fa-113">Cliquez sur toohello-page de configuration suivante hello flèche toogo.</span><span class="sxs-lookup"><span data-stu-id="952fa-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="952fa-115">Sur la page de configuration 2, entrez le nombre de hello de **nœuds de données**, sélectionnez hello **région/réseau virtuel**, puis sélectionnez les tailles de hello Hello **le nœud principal** et hello **Nœud de données**.</span><span class="sxs-lookup"><span data-stu-id="952fa-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="952fa-116">Cliquez sur toohello-page de configuration suivante hello flèche toogo.</span><span class="sxs-lookup"><span data-stu-id="952fa-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="952fa-117">Hello **région/réseau virtuel** a toobe hello même région hello hello du compte de stockage qui est en train de toobe utilisé pour hello cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="952fa-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="952fa-118">Sinon, dans la page configuration de la quatrième hello, compte de stockage hello apparaîtra pas dans la liste déroulante de hello des **nom de compte**.</span><span class="sxs-lookup"><span data-stu-id="952fa-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="952fa-120">Sur la page de configuration 3, fournissez un nom d’utilisateur et un mot de passe pour hello cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="952fa-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="952fa-121">**Ne le faites pas** hello sélectionnez *entrée hello Metastores Hive/Oozie*.</span><span class="sxs-lookup"><span data-stu-id="952fa-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="952fa-122">Ensuite, cliquez sur toohello-page de configuration suivante hello flèche toogo.</span><span class="sxs-lookup"><span data-stu-id="952fa-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="952fa-124">Sur la page de configuration 4, spécifiez le nom de compte de stockage hello, conteneur par défaut de hello Hello cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="952fa-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="952fa-125">Si vous sélectionnez *créer un conteneur par défaut* Bonjour **conteneur par défaut** liste déroulante, un conteneur avec hello même nom que celui que hello cluster sera créé.</span><span class="sxs-lookup"><span data-stu-id="952fa-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="952fa-126">Cliquez sur hello flèche toogo toohello dernière configuration page.</span><span class="sxs-lookup"><span data-stu-id="952fa-126">Click hello arrow toogo toohello last configuration page.</span></span>

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="952fa-128">Sur hello final **Actions de Script** page de configuration, cliquez sur **ajouter une action de script** bouton et remplissez les champs de texte hello avec hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="952fa-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="952fa-129">**NOM** -n’importe quelle chaîne comme nom hello de cette action de script</span><span class="sxs-lookup"><span data-stu-id="952fa-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="952fa-130">**TYPE DE NŒUD** : sélectionnez **Tous les nœuds**</span><span class="sxs-lookup"><span data-stu-id="952fa-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="952fa-131">**URI DE SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="952fa-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="952fa-132">*publicscripts* est un conteneur public dans le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="952fa-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="952fa-133">*getgoing* nous utilisons tooshare PowerShell script fichiers toofacilitate travail des utilisateurs dans Azure</span><span class="sxs-lookup"><span data-stu-id="952fa-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="952fa-134">**PARAMÈTRES** : (laisser cette zone vide)</span><span class="sxs-lookup"><span data-stu-id="952fa-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="952fa-135">Enfin, cliquez sur hello coche toostart hello la création de cluster HDInsight Hadoop de hello personnalisé.</span><span class="sxs-lookup"><span data-stu-id="952fa-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="952fa-137"><a name="headnode"></a>Accéder au nœud principal de Hadoop Cluster de hello</span><span class="sxs-lookup"><span data-stu-id="952fa-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="952fa-138">Vous devez activer le cluster de Hadoop toohello l’accès à distance dans Azure avant de pouvoir accéder hello nœud de tête hello Hadoop cluster via RDP.</span><span class="sxs-lookup"><span data-stu-id="952fa-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="952fa-139">Connectez-vous à toohello [ **portail Azure classic**](https://manage.windowsazure.com/), sélectionnez **HDInsight** sur hello gauche, sélectionnez votre cluster Hadoop dans liste hello de clusters, cliquez sur hello  **CONFIGURATION** onglet, puis cliquez sur hello **activer distant** icône bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="952fa-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="952fa-141">Bonjour **configurer le Bureau à distance** fenêtre, entrez hello nom d’utilisateur et les champs de mot de passe et sélectionnez la date d’expiration de hello pour l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="952fa-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="952fa-142">Cliquez ensuite sur hello coche tooenable hello accès à distance toohello nœud principal du cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="952fa-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="952fa-144">nom d’utilisateur Hello et le mot de passe pour l’accès à distance hello ne sont pas nom d’utilisateur hello et un mot de passe que vous utilisez lorsque vous avez créé le cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="952fa-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="952fa-145">Il s’agit d’un ensemble d’informations d’identification distinct.</span><span class="sxs-lookup"><span data-stu-id="952fa-145">This is a separate set of credentials.</span></span> <span data-ttu-id="952fa-146">En outre, date d’expiration de hello d’accès à distance de hello a toobe dans les 7 jours à partir de hello date actuelle.</span><span class="sxs-lookup"><span data-stu-id="952fa-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="952fa-147">Une fois l’accès à distance est activé, cliquez sur **CONNECT** bas hello tooremote de page hello dans le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="952fa-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="952fa-148">Vous ouvrez une session toohello le nœud principal du cluster Hadoop de hello en entrant les informations d’identification hello pour l’utilisateur de l’accès à distance hello que vous avez spécifié précédemment.</span><span class="sxs-lookup"><span data-stu-id="952fa-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![Create workspace](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="952fa-150">les étapes suivantes dans hello avancé du processus d’analytique Hello sont mappées dans hello [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) et peuvent inclure des étapes de déplacement des données dans HDInsight, puis traitent et aperçu en préparation pour l’apprentissage à partir des données de hello avec Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="952fa-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="952fa-151">Consultez [comment les requêtes Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) pour obtenir des instructions sur la façon dont tooaccess hello modules Python inclus dans Anaconda à partir du nœud principal de hello du cluster hello dans les fonctions utilisateur (UDF) qui sont utilisés tooprocess Hive enregistrements stockés dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="952fa-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

