---
title: "accès aaaRestrict à l’aide de Signatures d’accès partagé - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toorestrict de Signatures d’accès partagé toouse HDInsight aux toodata stockée dans des objets BLOB de stockage Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="06201-103">Utiliser des Signatures d’accès partagé Azure Storage toorestrict accès toodata dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="06201-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="06201-104">HDInsight a toodata d’accès complet dans les comptes de stockage Azure hello associés hello cluster.</span><span class="sxs-lookup"><span data-stu-id="06201-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="06201-105">Vous pouvez utiliser des Signatures d’accès partagé sur hello blob conteneur toorestrict accès toohello des données.</span><span class="sxs-lookup"><span data-stu-id="06201-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="06201-106">Par exemple, tooprovide accès en lecture seule toohello données.</span><span class="sxs-lookup"><span data-stu-id="06201-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="06201-107">Les Signatures d’accès partagé (SAS) sont une fonctionnalité des comptes de stockage Azure qui vous permet de toolimit accès toodata.</span><span class="sxs-lookup"><span data-stu-id="06201-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="06201-108">Par exemple, en fournissant l’accès en lecture seule toodata.</span><span class="sxs-lookup"><span data-stu-id="06201-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06201-109">Pour une solution utilisant Apache Ranger, envisagez d’utiliser les clusters HDInsight joints à un domaine.</span><span class="sxs-lookup"><span data-stu-id="06201-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="06201-110">Pour plus d’informations, consultez hello [configurer appartenant au domaine de HDInsight](hdinsight-domain-joined-configure.md) document.</span><span class="sxs-lookup"><span data-stu-id="06201-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="06201-111">HDInsight doit disposent d’un accès complet toohello par défaut pour les clusters hello.</span><span class="sxs-lookup"><span data-stu-id="06201-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="06201-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="06201-112">Requirements</span></span>

* <span data-ttu-id="06201-113">Un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="06201-113">An Azure subscription</span></span>
* <span data-ttu-id="06201-114">C# ou Python.</span><span class="sxs-lookup"><span data-stu-id="06201-114">C# or Python.</span></span> <span data-ttu-id="06201-115">Un exemple de code C# est fourni en tant que solution Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06201-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="06201-116">La version de Visual Studio doit être 2013, 2015 ou 2017</span><span class="sxs-lookup"><span data-stu-id="06201-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="06201-117">La version de Python doit être 2.7 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="06201-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="06201-118">Un cluster HDInsight de basés sur Linux ou [Azure PowerShell] [ powershell] -si vous disposez d’un cluster existant basés sur Linux, vous pouvez utiliser Ambari tooadd un cluster toohello de Signature d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="06201-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="06201-119">Si ce n’est pas le cas, vous pouvez utiliser Azure PowerShell toocreate un cluster et ajouter une Signature d’accès partagé pendant la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="06201-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="06201-120">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="06201-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="06201-121">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="06201-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="06201-122">Hello d’exemples de fichiers à partir de [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="06201-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="06201-123">Ce référentiel contient hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="06201-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="06201-124">Un projet Visual Studio permettant de créer un conteneur de stockage, une stratégie stockée et une SAP pour une utilisation avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06201-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="06201-125">Un script Python permettant de créer un conteneur de stockage, une stratégie stockée et une SAP pour une utilisation avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="06201-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="06201-126">Un script PowerShell que vous pouvez créer un HDInsight de cluster et le configurer toouse hello SAS.</span><span class="sxs-lookup"><span data-stu-id="06201-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="06201-127">Les signatures d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="06201-127">Shared Access Signatures</span></span>

<span data-ttu-id="06201-128">Il existe deux types de signatures d’accès partagé :</span><span class="sxs-lookup"><span data-stu-id="06201-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="06201-129">Ad hoc : hello heure de début, date d’expiration et les autorisations pour hello SAS sont spécifiés sur hello URI SAS.</span><span class="sxs-lookup"><span data-stu-id="06201-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="06201-130">Stratégie d’accès stockée : une stratégie d’accès stockée est définie sur un conteneur de ressources, tel qu’un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="06201-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="06201-131">Une stratégie peut être contraintes toomanage utilisé pour une ou plusieurs signatures d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="06201-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="06201-132">Lorsque vous associez un SAS avec une stratégie d’accès stockée, hello SAS hérite des contraintes de hello - hello heure de début, date d’expiration et autorisations - définies pour la stratégie d’accès stockée hello.</span><span class="sxs-lookup"><span data-stu-id="06201-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="06201-133">Hello différence entre les formes hello deux est importante pour un scénario clé : la révocation.</span><span class="sxs-lookup"><span data-stu-id="06201-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="06201-134">Une SAP est une URL, les personnes qui obtiennent hello SAS peuvent l’utiliser, quel que soit le qui a demandé qu’elle toobegin avec.</span><span class="sxs-lookup"><span data-stu-id="06201-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="06201-135">Si une SAP est publiée publiquement, il peut être utilisé par tout le monde dans Bonjour.</span><span class="sxs-lookup"><span data-stu-id="06201-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="06201-136">Une clé d'accès partagé qui est distribuée est valide jusqu'à ce que l'un des quatre événements suivants ait lieu :</span><span class="sxs-lookup"><span data-stu-id="06201-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="06201-137">délai d’expiration Hello spécifié sur hello que SAS est atteinte.</span><span class="sxs-lookup"><span data-stu-id="06201-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="06201-138">délai d’expiration Hello spécifié sur la stratégie d’accès stockée hello référencée par hello que SAS est atteinte.</span><span class="sxs-lookup"><span data-stu-id="06201-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="06201-139">délai d’expiration hello provoquent Hello scénarios suivants toobe atteint :</span><span class="sxs-lookup"><span data-stu-id="06201-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="06201-140">intervalle de temps Hello a expiré.</span><span class="sxs-lookup"><span data-stu-id="06201-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="06201-141">stratégie d’accès stockée Hello est modifié toohave un délai d’expiration Bonjour passées.</span><span class="sxs-lookup"><span data-stu-id="06201-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="06201-142">La modification du délai d’expiration hello est une façon toorevoke hello SAS.</span><span class="sxs-lookup"><span data-stu-id="06201-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="06201-143">Hello stockés de la stratégie d’accès référencée par hello que SAS est supprimé, ce qui est hello de toorevoke une autre façon SAS.</span><span class="sxs-lookup"><span data-stu-id="06201-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="06201-144">Si vous recréez la stratégie d’accès stockée hello avec hello même nom, tous les jetons SAP de stratégie précédente de hello sont valides (si le délai d’expiration hello sur hello SAP n’a pas été).</span><span class="sxs-lookup"><span data-stu-id="06201-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="06201-145">Si vous envisagez de toorevoke hello SAS, être toouse qu’un nom différent si vous recréez la stratégie d’accès hello avec un délai d’expiration Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="06201-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="06201-146">Hello compte qui a été utilisé toocreate hello SAS est régénérée.</span><span class="sxs-lookup"><span data-stu-id="06201-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="06201-147">Régénération de la clé de hello, toutes les applications qui utilisent l’authentification de clé toofail précédente hello.</span><span class="sxs-lookup"><span data-stu-id="06201-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="06201-148">Mettre à jour tous les composants toohello clé.</span><span class="sxs-lookup"><span data-stu-id="06201-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06201-149">Un URI de signature d’accès partagé est associé avec signature d’hello hello compte clé toocreate utilisés et hello stratégie d’accès stockée (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="06201-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="06201-150">Si aucune stratégie d’accès stockée n’est spécifié, hello uniquement moyen toorevoke une signature d’accès partagé est clé de compte toochange hello.</span><span class="sxs-lookup"><span data-stu-id="06201-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="06201-151">Nous vous recommandons de toujours utiliser des stratégies d’accès stockées.</span><span class="sxs-lookup"><span data-stu-id="06201-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="06201-152">Lorsque vous utilisez les stratégies stockées, vous pouvez révoquer des signatures ou étendre la date d’expiration hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="06201-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="06201-153">étapes Hello dans ce document utilisent toogenerate de stratégies d’accès stockée SAS.</span><span class="sxs-lookup"><span data-stu-id="06201-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="06201-154">Pour plus d’informations sur les Signatures d’accès partagé, consultez [modèle de présentation hello SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="06201-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="06201-155">Créer une stratégie stockée et une SAP à l’aide de C\#</span><span class="sxs-lookup"><span data-stu-id="06201-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="06201-156">Ouvrez la solution de hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06201-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="06201-157">Dans l’Explorateur de solutions, cliquez sur hello **SASToken** de projet et sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="06201-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="06201-158">Sélectionnez **paramètres** et ajouter des valeurs pour hello suivant entrées :</span><span class="sxs-lookup"><span data-stu-id="06201-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="06201-159">StorageConnectionString : hello chaîne de connexion de compte de stockage hello que vous souhaitez toocreate une stratégie stockée et le SAS pour.</span><span class="sxs-lookup"><span data-stu-id="06201-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="06201-160">Hello format doit être `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` où `myaccount` est le nom de hello de votre compte de stockage et `mykey` est hello clé hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="06201-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="06201-161">ContainerName : hello conteneur hello compte de stockage que vous voulez accéder toorestrict à.</span><span class="sxs-lookup"><span data-stu-id="06201-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="06201-162">SASPolicyName : toouse de nom hello pour hello stockées toocreate de stratégie.</span><span class="sxs-lookup"><span data-stu-id="06201-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="06201-163">FileToUpload : hello chemin d’accès tooa fichier qui est téléchargé toohello conteneur.</span><span class="sxs-lookup"><span data-stu-id="06201-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="06201-164">Exécutez le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-164">Run hello project.</span></span> <span data-ttu-id="06201-165">Toohello similaire à informations suivant le texte s’affiche une fois hello SAP a été générée :</span><span class="sxs-lookup"><span data-stu-id="06201-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="06201-166">Enregistrer le jeton de stratégie SAP hello, nom de compte de stockage et nom du conteneur.</span><span class="sxs-lookup"><span data-stu-id="06201-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="06201-167">Ces valeurs sont utilisées lorsque vous associez un compte de stockage hello avec votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06201-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="06201-168">Créer une stratégie stockée et une SAP à l’aide de Python</span><span class="sxs-lookup"><span data-stu-id="06201-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="06201-169">Ouvrir le fichier de SASToken.py hello et modifier hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="06201-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="06201-170">stratégie\_nom : toouse de nom hello pour hello stockées toocreate de stratégie.</span><span class="sxs-lookup"><span data-stu-id="06201-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="06201-171">stockage\_compte\_nom : nom hello de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="06201-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="06201-172">stockage\_compte\_clé : hello clé hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="06201-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="06201-173">stockage\_conteneur\_nom : hello conteneur hello compte de stockage que vous voulez accéder toorestrict à.</span><span class="sxs-lookup"><span data-stu-id="06201-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="06201-174">exemple\_fichier\_chemin d’accès : hello chemin d’accès tooa fichier qui est téléchargé toohello conteneur.</span><span class="sxs-lookup"><span data-stu-id="06201-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="06201-175">Exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-175">Run hello script.</span></span> <span data-ttu-id="06201-176">Il affiche hello SAS jeton similaire toohello lors de l’achèvement du script de hello suivantes : texte :</span><span class="sxs-lookup"><span data-stu-id="06201-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="06201-177">Enregistrer le jeton de stratégie SAP hello, nom de compte de stockage et nom du conteneur.</span><span class="sxs-lookup"><span data-stu-id="06201-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="06201-178">Ces valeurs sont utilisées lorsque vous associez un compte de stockage hello avec votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06201-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="06201-179">Utilisez hello SAS avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="06201-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="06201-180">Lorsque vous créez un cluster HDInsight, vous devez spécifier un compte de stockage principal, et vous pouvez éventuellement indiquer des comptes de stockage supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="06201-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="06201-181">Ces deux méthodes d’ajout de stockage nécessitent des comptes de stockage toohello un accès complet et les conteneurs qui sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="06201-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="06201-182">toouse un conteneur tooa de Signature d’accès partagé toolimit d’accès, ajouter une entrée personnalisée de toohello **core-site** configuration de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="06201-183">Pour **basé sur Windows** ou **basés sur Linux** des clusters HDInsight, vous pouvez ajouter l’entrée de hello lors de la création du cluster à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06201-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="06201-184">Pour **basés sur Linux** clusters HDInsight, modifier la configuration de hello après la création du cluster à l’aide de Ambari.</span><span class="sxs-lookup"><span data-stu-id="06201-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="06201-185">Créer un cluster qui utilise hello SAS</span><span class="sxs-lookup"><span data-stu-id="06201-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="06201-186">Un exemple de création d’un cluster HDInsight que hello utilise SAS est inclus dans hello `CreateCluster` répertoire du référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="06201-187">toouse il, hello utilisation suivant les étapes :</span><span class="sxs-lookup"><span data-stu-id="06201-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="06201-188">Ouvrez hello `CreateCluster\HDInsightSAS.ps1` dans un éditeur de texte et modifiez hello valeurs au début de hello du document de hello suivantes.</span><span class="sxs-lookup"><span data-stu-id="06201-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="06201-189">Par exemple, remplacez `'mycluster'` toohello nom du cluster de hello souhaité toocreate.</span><span class="sxs-lookup"><span data-stu-id="06201-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="06201-190">les valeurs Hello SAS doivent correspondre à des valeurs hello des étapes précédentes de hello lors de la création d’un compte de stockage et un jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="06201-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="06201-191">Une fois que vous avez modifié les valeurs hello, enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="06201-192">Ouvrez une nouvelle invite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06201-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="06201-193">Si vous ne maîtrisez pas Azure PowerShell ou que vous ne l’avez pas installé, consultez la rubrique [Installer et configurer Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="06201-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="06201-194">À partir de l’invite de commandes hello, utilisez hello suivant commande tooauthenticate tooyour abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="06201-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="06201-195">Lorsque vous y êtes invité, connectez-vous avec le compte hello pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="06201-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="06201-196">Si votre compte est associé à plusieurs abonnements Azure, vous devrez peut-être toouse `Select-AzureRmSubscription` tooselect hello souscription toouse.</span><span class="sxs-lookup"><span data-stu-id="06201-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="06201-197">À partir de l’invite de commandes hello, modifiez les répertoires toohello `CreateCluster` répertoire qui contient le fichier de HDInsightSAS.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="06201-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="06201-198">Utilisez ensuite hello commande toorun hello script suivant</span><span class="sxs-lookup"><span data-stu-id="06201-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="06201-199">En tant que script de hello s’exécute, il enregistre invite de commandes de sortie toohello PowerShell lorsqu’il crée des comptes de stockage et le groupe de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="06201-200">Vous êtes invité à tooenter hello HTTP pour hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06201-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="06201-201">Ce compte est utilisé toosecure cluster de toohello d’accès HTTP/s.</span><span class="sxs-lookup"><span data-stu-id="06201-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="06201-202">Si vous créez un cluster basé sur Linux, vous êtes invité à saisir un nom et un mot de passe de compte d’utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="06201-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="06201-203">Ce compte est journal utilisé tooremotely toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="06201-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="06201-204">Lorsque vous y êtes invité hello HTTP/s ou SSH nom d’utilisateur et mot de passe, vous devez fournir un mot de passe qui répond aux hello suivant des critères :</span><span class="sxs-lookup"><span data-stu-id="06201-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="06201-205">Il doit contenir au moins 10 caractères.</span><span class="sxs-lookup"><span data-stu-id="06201-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="06201-206">Il doit contenir au moins un chiffre.</span><span class="sxs-lookup"><span data-stu-id="06201-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="06201-207">Il doit contenir au moins un caractère non alphanumérique.</span><span class="sxs-lookup"><span data-stu-id="06201-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="06201-208">Il doit contenir au moins une lettre minuscule et une lettre majuscule.</span><span class="sxs-lookup"><span data-stu-id="06201-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="06201-209">Il prend un certain temps pour ce script toocomplete, généralement environ 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="06201-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="06201-210">Lorsque le script de hello se termine sans erreur, le cluster de hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="06201-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="06201-211">Utilisez hello SAS avec un cluster existant</span><span class="sxs-lookup"><span data-stu-id="06201-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="06201-212">Si vous disposez d’un cluster existant basés sur Linux, vous pouvez ajouter hello SAS toohello **core-site** configuration à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="06201-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="06201-213">Ouvrez hello Ambari web l’interface utilisateur pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="06201-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="06201-214">adresse Hello pour cette page est https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="06201-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="06201-215">Lorsque vous y êtes invité, authentifier cluster toohello à l’aide du nom de l’administrateur hello (admin) et la création de mot de passe utilisé lorsque le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="06201-216">À partir de la partie gauche de l’interface utilisateur web de Ambari hello de hello, sélectionnez **HDFS** , puis sélectionnez hello **configurations** onglet milieu hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="06201-217">Sélectionnez hello **avancé** onglet, puis faites défiler jusqu'à ce que vous trouviez hello **personnalisé core-site** section.</span><span class="sxs-lookup"><span data-stu-id="06201-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="06201-218">Développez hello **personnalisé core-site** section, puis fin toohello de défilement et sélectionnez hello **ajouter la propriété...**  lien.</span><span class="sxs-lookup"><span data-stu-id="06201-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="06201-219">Valeurs suivantes de hello d’utilisation pour hello **clé** et **valeur** champs :</span><span class="sxs-lookup"><span data-stu-id="06201-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="06201-220">**Clé**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="06201-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="06201-221">**Valeur**: hello SAS retourné par hello application c# ou Python, vous avez exécuté précédemment</span><span class="sxs-lookup"><span data-stu-id="06201-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="06201-222">Remplacez **CONTAINERNAME** avec le nom du conteneur hello que vous avez utilisé avec les applications c# ou SAS hello.</span><span class="sxs-lookup"><span data-stu-id="06201-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="06201-223">Remplacez **STORAGEACCOUNTNAME** par le nom de compte de stockage hello vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="06201-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="06201-224">Cliquez sur hello **ajouter** toosave cette clé et valeur, puis cliquez sur hello **enregistrer** bouton les modifications de configuration toosave hello.</span><span class="sxs-lookup"><span data-stu-id="06201-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="06201-225">Lorsque vous y êtes invité, ajoutez une description de modification hello (« l’ajout d’accès au stockage SAS » par exemple), puis **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="06201-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="06201-226">Cliquez sur **OK** quand les modifications de hello ont été effectuées.</span><span class="sxs-lookup"><span data-stu-id="06201-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="06201-227">Vous devez redémarrer plusieurs services avant hello modification prenne effet.</span><span class="sxs-lookup"><span data-stu-id="06201-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="06201-228">Dans hello Ambari interface utilisateur web, sélectionnez **HDFS** à partir de la liste hello dans hello gauche, puis sélectionnez **redémarrer tous les** de hello **Actions Service** liste sur hello droite déroulante.</span><span class="sxs-lookup"><span data-stu-id="06201-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="06201-229">Lorsque vous y êtes invité, sélectionnez **Activer le mode de maintenance**, puis sélectionnez __Conform Restart All".</span><span class="sxs-lookup"><span data-stu-id="06201-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="06201-230">Répétez ce processus pour les entrées MapReduce2 et YARN.</span><span class="sxs-lookup"><span data-stu-id="06201-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="06201-231">Une fois que hello sont redémarrés, sélectionnez chacune d’elles et désactiver le mode de maintenance à partir de hello **Actions Service** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="06201-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="06201-232">Tester l’accès restreint</span><span class="sxs-lookup"><span data-stu-id="06201-232">Test restricted access</span></span>

<span data-ttu-id="06201-233">tooverify que vous avez un accès limité, hello utilisez méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="06201-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="06201-234">Pour **basé sur Windows** clusters HDInsight, utiliser le cluster de toohello tooconnect de bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="06201-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="06201-235">Pour plus d’informations, consultez [se connecter à l’aide du protocole RDP de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="06201-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="06201-236">Une fois connecté, utilisez hello **Hadoop de ligne de commande** icône sur tooopen de bureau hello une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="06201-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="06201-237">Pour **basés sur Linux** clusters HDInsight, utiliser SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="06201-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="06201-238">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="06201-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="06201-239">Une fois connecté toohello cluster, utilisez hello suivant tooverify étapes que vous pouvez uniquement en lecture et la liste des éléments sur le compte de stockage SAS hello :</span><span class="sxs-lookup"><span data-stu-id="06201-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="06201-240">contenu de hello toolist du conteneur de hello, utilisez hello de commande suivante à partir de l’invite de commandes hello :</span><span class="sxs-lookup"><span data-stu-id="06201-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="06201-241">Remplacez **SASCONTAINER** avec nom hello du conteneur hello créé pour hello compte de stockage SAS.</span><span class="sxs-lookup"><span data-stu-id="06201-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="06201-242">Remplacez **SASACCOUNTNAME** avec nom hello hello du compte de stockage utilisé pour hello SAS.</span><span class="sxs-lookup"><span data-stu-id="06201-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="06201-243">liste de Hello inclut fichier hello téléchargé lorsque le conteneur de hello et associations de sécurité ont été créées.</span><span class="sxs-lookup"><span data-stu-id="06201-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="06201-244">Utilisez hello suivant tooverify de commande que vous pouvez lire le contenu de hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="06201-245">Remplacez hello **SASCONTAINER** et **SASACCOUNTNAME** comme à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="06201-246">Remplacez **nom de fichier** avec nom hello du fichier hello affiché dans la commande précédente hello :</span><span class="sxs-lookup"><span data-stu-id="06201-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="06201-247">Cette commande répertorie le contenu hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="06201-248">Utilisez hello suivant le système de fichiers local toohello de fichier de commandes toodownload hello :</span><span class="sxs-lookup"><span data-stu-id="06201-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="06201-249">Cette commande téléchargements hello fichier tooa fichier local nommé **testfile.txt**.</span><span class="sxs-lookup"><span data-stu-id="06201-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="06201-250">Suivant de hello utilisez commande tooupload hello fichier local tooa nouveau fichier nommé **testupload.txt** sur hello stockage SAS :</span><span class="sxs-lookup"><span data-stu-id="06201-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="06201-251">Vous recevez un toohello similaire message suit texte :</span><span class="sxs-lookup"><span data-stu-id="06201-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="06201-252">Cette erreur se produit, car l’emplacement de stockage hello est lecture + liste uniquement.</span><span class="sxs-lookup"><span data-stu-id="06201-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="06201-253">Utilisez hello suivant des données de commande tooput hello de stockage par défaut de hello pour cluster hello, qui est accessible en écriture :</span><span class="sxs-lookup"><span data-stu-id="06201-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="06201-254">Cette fois-ci, hello opération doit se terminer avec succès.</span><span class="sxs-lookup"><span data-stu-id="06201-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="06201-255">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="06201-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="06201-256">Une tâche a été annulée</span><span class="sxs-lookup"><span data-stu-id="06201-256">A task was canceled</span></span>

<span data-ttu-id="06201-257">**Symptômes**: lorsque vous créez un cluster à l’aide du script PowerShell de hello, hello message d’erreur suivant peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="06201-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="06201-258">**Cause**: cette erreur peut se produire si vous utilisez un mot de passe pour l’utilisateur d’administration/HTTP hello pour hello cluster ou (pour les clusters basés sur Linux) utilisateur SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="06201-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="06201-259">**Résolution**: utiliser un mot de passe qui répond aux hello suivant des critères :</span><span class="sxs-lookup"><span data-stu-id="06201-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="06201-260">Il doit contenir au moins 10 caractères.</span><span class="sxs-lookup"><span data-stu-id="06201-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="06201-261">Il doit contenir au moins un chiffre.</span><span class="sxs-lookup"><span data-stu-id="06201-261">Must contain at least one digit</span></span>
* <span data-ttu-id="06201-262">Il doit contenir au moins un caractère non alphanumérique.</span><span class="sxs-lookup"><span data-stu-id="06201-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="06201-263">Il doit contenir au moins une lettre minuscule et une lettre majuscule.</span><span class="sxs-lookup"><span data-stu-id="06201-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="06201-264">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06201-264">Next steps</span></span>

<span data-ttu-id="06201-265">Maintenant que vous avez appris comment tooadd un stockage à accès limité tooyour cluster HDInsight, des informations autres toowork manières avec des données sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="06201-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="06201-266">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="06201-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="06201-267">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="06201-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="06201-268">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="06201-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
