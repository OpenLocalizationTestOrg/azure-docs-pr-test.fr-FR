---
title: "Restreindre l’accès à l’aide des signatures d’accès partagé (SAP)- Azure HDInsight | Microsoft Docs"
description: "Découvrez comment utiliser les signatures d’accès partagé pour limiter l’accès HDInsight aux données stockées dans des objets blob de stockage Azure."
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
ms.openlocfilehash: 2e4b1a307fae06c0639d93b9804c6f0f703d5900
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-shared-access-signatures-to-restrict-access-to-data-in-hdinsight"></a><span data-ttu-id="210a4-103">Utilisation des signatures d’accès partagé du stockage Azure pour restreindre l’accès aux données dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="210a4-103">Use Azure Storage Shared Access Signatures to restrict access to data in HDInsight</span></span>

<span data-ttu-id="210a4-104">HDInsight dispose d’un accès total aux données dans les comptes de stockage Azure associés au cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-104">HDInsight has full access to data in the Azure Storage accounts associated with the cluster.</span></span> <span data-ttu-id="210a4-105">Vous pouvez utiliser des signatures d’accès partagé sur le conteneur d’objets blob pour restreindre l’accès aux données.</span><span class="sxs-lookup"><span data-stu-id="210a4-105">You can use Shared Access Signatures on the blob container to restrict access to the data.</span></span> <span data-ttu-id="210a4-106">Par exemple, pour fournir un accès en lecture seule aux données.</span><span class="sxs-lookup"><span data-stu-id="210a4-106">For example, to provide read-only access to the data.</span></span> <span data-ttu-id="210a4-107">Les signatures d’accès partagé (SAP) sont une fonctionnalité des comptes de stockage Azure qui vous permet de limiter l’accès aux données.</span><span class="sxs-lookup"><span data-stu-id="210a4-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you to limit access to data.</span></span> <span data-ttu-id="210a4-108">Par exemple, en fournissant un accès en lecture seule aux données.</span><span class="sxs-lookup"><span data-stu-id="210a4-108">For example, providing read-only access to data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="210a4-109">Pour une solution utilisant Apache Ranger, envisagez d’utiliser les clusters HDInsight joints à un domaine.</span><span class="sxs-lookup"><span data-stu-id="210a4-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="210a4-110">Pour plus d’informations, consultez le document [Configurer des clusters HDInsight joints à un domaine (préversion)](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="210a4-110">For more information, see the [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="210a4-111">HDInsight doit disposer d’un accès total au stockage par défaut pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-111">HDInsight must have full access to the default storage for the cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="210a4-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="210a4-112">Requirements</span></span>

* <span data-ttu-id="210a4-113">Un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="210a4-113">An Azure subscription</span></span>
* <span data-ttu-id="210a4-114">C# ou Python.</span><span class="sxs-lookup"><span data-stu-id="210a4-114">C# or Python.</span></span> <span data-ttu-id="210a4-115">Un exemple de code C# est fourni en tant que solution Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="210a4-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="210a4-116">La version de Visual Studio doit être 2013, 2015 ou 2017</span><span class="sxs-lookup"><span data-stu-id="210a4-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="210a4-117">La version de Python doit être 2.7 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="210a4-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="210a4-118">Cluster HDInsight basé sur Linux OU [Azure PowerShell][powershell] : si vous avez un cluster existant basé sur Linux, vous pouvez utiliser Ambari pour ajouter une signature d’accès partagé au cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari to add a Shared Access Signature to the cluster.</span></span> <span data-ttu-id="210a4-119">Si ce n’est pas le cas, vous pouvez utiliser Azure PowerShell pour créer un cluster et ajouter une signature d’accès partagé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-119">If not, you can use Azure PowerShell to create a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="210a4-120">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="210a4-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="210a4-121">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="210a4-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="210a4-122">Fichiers d’exemple à l’adresse [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="210a4-122">The example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="210a4-123">Ce dépôt contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="210a4-123">This repository contains the following items:</span></span>

  * <span data-ttu-id="210a4-124">Un projet Visual Studio permettant de créer un conteneur de stockage, une stratégie stockée et une SAP pour une utilisation avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="210a4-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="210a4-125">Un script Python permettant de créer un conteneur de stockage, une stratégie stockée et une SAP pour une utilisation avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="210a4-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="210a4-126">Un script PowerShell permettant de créer un cluster HDInsight et de le configurer afin d’utiliser la SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-126">A PowerShell script that can create a HDInsight cluster and configure it to use the SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="210a4-127">Les signatures d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="210a4-127">Shared Access Signatures</span></span>

<span data-ttu-id="210a4-128">Il existe deux types de signatures d’accès partagé :</span><span class="sxs-lookup"><span data-stu-id="210a4-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="210a4-129">Ad hoc : l’heure de début, l’heure d’expiration et les autorisations associées à cette SAP sont spécifiées sur l’URI de SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-129">Ad hoc: The start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span>

* <span data-ttu-id="210a4-130">Stratégie d’accès stockée : une stratégie d’accès stockée est définie sur un conteneur de ressources, tel qu’un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="210a4-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="210a4-131">et permet de gérer les contraintes d’une ou de plusieurs signatures d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="210a4-131">A policy can be used to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="210a4-132">Lorsque vous associez une signature d'accès partagé à une stratégie d'accès stockée, la signature hérite des contraintes (heure de début, heure d'expiration et autorisations) définies pour la stratégie.</span><span class="sxs-lookup"><span data-stu-id="210a4-132">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span>

<span data-ttu-id="210a4-133">La différence entre les deux formes est importante pour un scénario clé : la révocation.</span><span class="sxs-lookup"><span data-stu-id="210a4-133">The difference between the two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="210a4-134">Une signature d'accès partagé est une URL. Par conséquent, toute personne qui obtient la signature peut s'en servir, quel que soit celui qui l'a demandée initialement.</span><span class="sxs-lookup"><span data-stu-id="210a4-134">A SAS is a URL, so anyone who obtains the SAS can use it, regardless of who requested it to begin with.</span></span> <span data-ttu-id="210a4-135">Si une SAP est publiée publiquement, elle peut être utilisée par n’importe qui.</span><span class="sxs-lookup"><span data-stu-id="210a4-135">If a SAS is published publicly, it can be used by anyone in the world.</span></span> <span data-ttu-id="210a4-136">Une clé d'accès partagé qui est distribuée est valide jusqu'à ce que l'un des quatre événements suivants ait lieu :</span><span class="sxs-lookup"><span data-stu-id="210a4-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="210a4-137">L'heure d'expiration spécifiée sur la signature d'accès partagé est atteinte.</span><span class="sxs-lookup"><span data-stu-id="210a4-137">The expiry time specified on the SAS is reached.</span></span>

2. <span data-ttu-id="210a4-138">Le délai d’expiration spécifié sur la stratégie d’accès stockée référencée par la SAP est atteint.</span><span class="sxs-lookup"><span data-stu-id="210a4-138">The expiry time specified on the stored access policy referenced by the SAS is reached.</span></span> <span data-ttu-id="210a4-139">Dans les scénarios suivants, l’heure d’expiration est atteinte :</span><span class="sxs-lookup"><span data-stu-id="210a4-139">The following scenarios cause the expiry time to be reached:</span></span>

    * <span data-ttu-id="210a4-140">L’intervalle de temps est écoulé.</span><span class="sxs-lookup"><span data-stu-id="210a4-140">The time interval has elapsed.</span></span>
    * <span data-ttu-id="210a4-141">La stratégie d’accès stockée est modifiée pour que son heure d’expiration soit passée.</span><span class="sxs-lookup"><span data-stu-id="210a4-141">The stored access policy is modified to have an expiry time in the past.</span></span> <span data-ttu-id="210a4-142">Modifier l’heure d’expiration est un moyen de révoquer la SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-142">Changing the expiry time is one way to revoke the SAS.</span></span>

3. <span data-ttu-id="210a4-143">La stratégie d'accès stockée référencée par la signature d'accès partagé est supprimée, ce qui est une autre manière de révoquer la signature d'accès partagé.</span><span class="sxs-lookup"><span data-stu-id="210a4-143">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span></span> <span data-ttu-id="210a4-144">Si vous recréez la stratégie d’accès stockée avec le même nom, tous les jetons de SAP de la stratégie précédente sont valides (si l’heure d’expiration sur la SAP n’est pas passée).</span><span class="sxs-lookup"><span data-stu-id="210a4-144">If you recreate the stored access policy with the same name, all  SAS tokens for the previous policy are valid (if the expiry time on the SAS has not passed).</span></span> <span data-ttu-id="210a4-145">Si vous avez l’intention de révoquer la SAP, veillez à utiliser un nom différent si vous recréez la stratégie d’accès avec une heure d’expiration située dans le futur.</span><span class="sxs-lookup"><span data-stu-id="210a4-145">If you intend to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span></span>

4. <span data-ttu-id="210a4-146">La clé de compte qui a été utilisée pour créer la signature d'accès partagé est régénérée.</span><span class="sxs-lookup"><span data-stu-id="210a4-146">The account key that was used to create the SAS is regenerated.</span></span> <span data-ttu-id="210a4-147">Cette régénération provoque l’échec de l’authentification de toutes les applications qui utilisent la clé précédente.</span><span class="sxs-lookup"><span data-stu-id="210a4-147">Regenerating the key causes all applications that use the previous key to fail authentication.</span></span> <span data-ttu-id="210a4-148">Mettez à jour tous les composants vers la nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="210a4-148">Update all components to the new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="210a4-149">L’URI d’une signature d’accès partagé est associé à la clé du compte utilisée pour créer la signature et à la stratégie d’accès stockée correspondante (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="210a4-149">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span></span> <span data-ttu-id="210a4-150">Si aucune stratégie d’accès stockée n’est spécifiée, la seule façon de révoquer une signature d’accès partagé consiste à modifier la clé du compte.</span><span class="sxs-lookup"><span data-stu-id="210a4-150">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span></span>

<span data-ttu-id="210a4-151">Nous vous recommandons de toujours utiliser des stratégies d’accès stockées.</span><span class="sxs-lookup"><span data-stu-id="210a4-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="210a4-152">Lorsque vous utilisez des stratégies stockées, vous pouvez révoquer des signatures ou étendre la date d’expiration, selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="210a4-152">When using stored policies, you can either revoke signatures or extend the expiry date as needed.</span></span> <span data-ttu-id="210a4-153">Les étapes décrites dans ce document utilisent les stratégies d’accès stockées pour générer des SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-153">The steps in this document use stored access policies to generate SAS.</span></span>

<span data-ttu-id="210a4-154">Pour plus d’informations sur les SAP, voir [Présentation du modèle SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="210a4-154">For more information on Shared Access Signatures, see [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="210a4-155">Créer une stratégie stockée et une SAP à l’aide de C\#</span><span class="sxs-lookup"><span data-stu-id="210a4-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="210a4-156">Ouvrez la solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="210a4-156">Open the solution in Visual Studio.</span></span>

2. <span data-ttu-id="210a4-157">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **SASToken**, puis sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="210a4-157">In Solution Explorer, right-click on the **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="210a4-158">Sélectionnez **Paramètres** et ajoutez des valeurs pour les entrées suivantes :</span><span class="sxs-lookup"><span data-stu-id="210a4-158">Select **Settings** and add values for the following entries:</span></span>

   * <span data-ttu-id="210a4-159">StorageConnectionString : chaîne de connexion pour le compte de stockage pour lequel vous souhaitez créer une stratégie stockée et une SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-159">StorageConnectionString: The connection string for the storage account that you want to create a stored policy and SAS for.</span></span> <span data-ttu-id="210a4-160">Le format doit être `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey`, où `myaccount` est le nom de votre compte de stockage et `mykey` est la clé pour le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="210a4-160">The format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is the name of your storage account and `mykey` is the key for the storage account.</span></span>

   * <span data-ttu-id="210a4-161">ContainerName : conteneur du compte de stockage auquel vous souhaitez restreindre l’accès.</span><span class="sxs-lookup"><span data-stu-id="210a4-161">ContainerName: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="210a4-162">SASPolicyName : nom à utiliser pour la stratégie stockée à créer.</span><span class="sxs-lookup"><span data-stu-id="210a4-162">SASPolicyName: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="210a4-163">FileToUpload : chemin d’accès à un fichier qui est chargé sur le conteneur.</span><span class="sxs-lookup"><span data-stu-id="210a4-163">FileToUpload: The path to a file that is uploaded to the container.</span></span>

4. <span data-ttu-id="210a4-164">Exécutez le projet.</span><span class="sxs-lookup"><span data-stu-id="210a4-164">Run the project.</span></span> <span data-ttu-id="210a4-165">Des informations semblables au texte suivant s’affichent une fois la signature d’accès partagé générée :</span><span class="sxs-lookup"><span data-stu-id="210a4-165">Information similar to the following text is displayed once the SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="210a4-166">Enregistrez le jeton de stratégie SAP, le nom du compte de stockage et le nom du conteneur.</span><span class="sxs-lookup"><span data-stu-id="210a4-166">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="210a4-167">Ces valeurs sont utilisées quand vous associez le compte de stockage à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="210a4-167">These values are used when associating the storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="210a4-168">Créer une stratégie stockée et une SAP à l’aide de Python</span><span class="sxs-lookup"><span data-stu-id="210a4-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="210a4-169">Ouvrez le fichier SASToken.py et modifiez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="210a4-169">Open the SASToken.py file and change the following values:</span></span>

   * <span data-ttu-id="210a4-170">nom\_stratégie : nom à utiliser pour la stratégie stockée à créer.</span><span class="sxs-lookup"><span data-stu-id="210a4-170">policy\_name: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="210a4-171">storage\_account\_name : le nom de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="210a4-171">storage\_account\_name: The name of your storage account.</span></span>

   * <span data-ttu-id="210a4-172">storage\_account\_key : la clé du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="210a4-172">storage\_account\_key: The key for the storage account.</span></span>

   * <span data-ttu-id="210a4-173">storage\_container\_name : conteneur du compte de stockage auquel vous souhaitez restreindre l’accès.</span><span class="sxs-lookup"><span data-stu-id="210a4-173">storage\_container\_name: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="210a4-174">exemple\_chemin\_fichier : chemin d’accès à un fichier qui est chargé sur le conteneur.</span><span class="sxs-lookup"><span data-stu-id="210a4-174">example\_file\_path: The path to a file that is uploaded to the container.</span></span>

2. <span data-ttu-id="210a4-175">Exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="210a4-175">Run the script.</span></span> <span data-ttu-id="210a4-176">Il affiche le jeton SAP semblable au texte suivant quand il est terminé :</span><span class="sxs-lookup"><span data-stu-id="210a4-176">It displays the SAS token similar to the following text when the script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="210a4-177">Enregistrez le jeton de stratégie SAP, le nom du compte de stockage et le nom du conteneur.</span><span class="sxs-lookup"><span data-stu-id="210a4-177">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="210a4-178">Ces valeurs sont utilisées quand vous associez le compte de stockage à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="210a4-178">These values are used when associating the storage account with your HDInsight cluster.</span></span>

## <a name="use-the-sas-with-hdinsight"></a><span data-ttu-id="210a4-179">Utilisation de la SAP avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="210a4-179">Use the SAS with HDInsight</span></span>

<span data-ttu-id="210a4-180">Lorsque vous créez un cluster HDInsight, vous devez spécifier un compte de stockage principal, et vous pouvez éventuellement indiquer des comptes de stockage supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="210a4-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="210a4-181">Ces deux méthodes d’ajout de stockage nécessitent un accès complet aux comptes de stockage et aux conteneurs qui sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="210a4-181">Both of these methods of adding storage require full access to the storage accounts and containers that are used.</span></span>

<span data-ttu-id="210a4-182">Pour utiliser une signature d’accès partagé afin de limiter l’accès à un conteneur, ajoutez une entrée personnalisée à la configuration **core-site** du cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-182">To use a Shared Access Signature to limit access to a container, add a custom entry to the **core-site** configuration for the cluster.</span></span>

* <span data-ttu-id="210a4-183">Pour les clusters HDInsight **basés sur Windows** ou **basés sur Linux**, vous pouvez ajouter l’entrée lors de la création du cluster à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="210a4-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add the entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="210a4-184">Pour les clusters HDInsight **basés sur Linux**, modifiez la configuration après la création du cluster à l’aide d’Ambari.</span><span class="sxs-lookup"><span data-stu-id="210a4-184">For **Linux-based** HDInsight clusters, change the configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-the-sas"></a><span data-ttu-id="210a4-185">Créer un cluster qui utilise la signature d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="210a4-185">Create a cluster that uses the SAS</span></span>

<span data-ttu-id="210a4-186">Un exemple de création de cluster HDInsight utilisant les SAP est inclus dans le répertoire `CreateCluster` du dépôt.</span><span class="sxs-lookup"><span data-stu-id="210a4-186">An example of creating an HDInsight cluster that uses the SAS is included in the `CreateCluster` directory of the repository.</span></span> <span data-ttu-id="210a4-187">Pour l’utiliser, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="210a4-187">To use it, use the following steps:</span></span>

1. <span data-ttu-id="210a4-188">Ouvrez le fichier `CreateCluster\HDInsightSAS.ps1` dans un éditeur de texte et modifiez les valeurs suivantes au début du document.</span><span class="sxs-lookup"><span data-stu-id="210a4-188">Open the `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify the following values at the beginning of the document.</span></span>

    ```powershell
    # Replace 'mycluster' with the name of the cluster to be created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with the name of the group to be created
    $resourceGroupName = 'myresourcegroup'
    # Replace with the Azure data center you want to the cluster to live in
    $location = 'North Europe'
    # Replace with the name of the default storage account to be created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with the name of the SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with the name of the SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with the SAS token generated earlier
    $SASToken = 'sastoken'
    # Set the number of worker nodes in the cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="210a4-189">Par exemple, remplacez `'mycluster'` avec le nom du cluster que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="210a4-189">For example, change `'mycluster'` to the name of the cluster you want to create.</span></span> <span data-ttu-id="210a4-190">Les valeurs SAP doivent correspondre aux valeurs des étapes précédentes lors de la création du compte de stockage et du jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-190">The SAS values should match the values from the previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="210a4-191">Une fois que vous avez modifié les valeurs, enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="210a4-191">Once you have changed the values, save the file.</span></span>

2. <span data-ttu-id="210a4-192">Ouvrez une nouvelle invite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="210a4-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="210a4-193">Si vous ne maîtrisez pas Azure PowerShell ou que vous ne l’avez pas installé, consultez la rubrique [Installer et configurer Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="210a4-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="210a4-194">À partir de l’invite, utilisez la commande suivante pour vous identifier auprès de votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="210a4-194">From the prompt, use the following command to authenticate to your Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="210a4-195">Quand vous y êtes invité, connectez-vous avec le compte associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="210a4-195">When prompted, log in with the account for your Azure subscription.</span></span>

    <span data-ttu-id="210a4-196">Si votre compte est associé à plusieurs abonnements Azure, vous devrez peut-être utiliser `Select-AzureRmSubscription` pour sélectionner l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="210a4-196">If your account is associated with multiple Azure subscriptions, you may need to use `Select-AzureRmSubscription` to select the subscription you wish to use.</span></span>

4. <span data-ttu-id="210a4-197">À partir de l’invite, remplacez les répertoires par le répertoire `CreateCluster` qui contient le fichier HDInsightSAS.ps1.</span><span class="sxs-lookup"><span data-stu-id="210a4-197">From the prompt, change directories to the `CreateCluster` directory that contains the HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="210a4-198">Utilisez ensuite la commande suivante pour exécuter le script</span><span class="sxs-lookup"><span data-stu-id="210a4-198">Then use the following command to run the script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="210a4-199">Quand il s’exécute, le script consigne la sortie dans l’invite PowerShell et crée le groupe de ressources et les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="210a4-199">As the script runs, it logs output to the PowerShell prompt as it creates the resource group and storage accounts.</span></span> <span data-ttu-id="210a4-200">Il vous invite à entrer le nom d’utilisateur HTTP pour le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="210a4-200">You are prompted to enter the HTTP user for the HDInsight cluster.</span></span> <span data-ttu-id="210a4-201">Ce compte est utilisé pour sécuriser l’accès HTTP/s au cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-201">This account is used to secure HTTP/s access to the cluster.</span></span>

    <span data-ttu-id="210a4-202">Si vous créez un cluster basé sur Linux, vous êtes invité à saisir un nom et un mot de passe de compte d’utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="210a4-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="210a4-203">Ce compte est utilisé pour la connexion à distance au cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-203">This account is used to remotely log in to the cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="210a4-204">Lorsque vous êtes invité à saisir le nom d’utilisateur et le mot de passe HTTP/s ou SSH, vous devez fournir un mot de passe qui répond aux critères suivants :</span><span class="sxs-lookup"><span data-stu-id="210a4-204">When prompted for the HTTP/s or SSH user name and password, you must provide a password that meets the following criteria:</span></span>
   >
   > * <span data-ttu-id="210a4-205">Il doit contenir au moins 10 caractères.</span><span class="sxs-lookup"><span data-stu-id="210a4-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="210a4-206">Il doit contenir au moins un chiffre.</span><span class="sxs-lookup"><span data-stu-id="210a4-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="210a4-207">Il doit contenir au moins un caractère non alphanumérique.</span><span class="sxs-lookup"><span data-stu-id="210a4-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="210a4-208">Il doit contenir au moins une lettre minuscule et une lettre majuscule.</span><span class="sxs-lookup"><span data-stu-id="210a4-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="210a4-209">L’exécution de ce script prend un certain temps, environ 15 minutes en général.</span><span class="sxs-lookup"><span data-stu-id="210a4-209">It takes a while for this script to complete, usually around 15 minutes.</span></span> <span data-ttu-id="210a4-210">Lorsque le script se termine sans erreur, le cluster a été créé.</span><span class="sxs-lookup"><span data-stu-id="210a4-210">When the script completes without any errors, the cluster has been created.</span></span>

### <a name="use-the-sas-with-an-existing-cluster"></a><span data-ttu-id="210a4-211">Utiliser la signature d’accès partagé avec un cluster existant</span><span class="sxs-lookup"><span data-stu-id="210a4-211">Use the SAS with an existing cluster</span></span>

<span data-ttu-id="210a4-212">Si vous disposez d’un cluster existant basé sur Linux, vous pouvez ajouter la SAP pour la configuration **core-site** en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="210a4-212">If you have an existing Linux-based cluster, you can add the SAS to the **core-site** configuration by using the following steps:</span></span>

1. <span data-ttu-id="210a4-213">Ouvrez l’interface utilisateur web Ambari de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-213">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="210a4-214">L’adresse de cette page est https://VOTRE NOM DE CLISTER.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="210a4-214">The address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="210a4-215">À l’invite, authentifiez-vous auprès du cluster au moyen du nom et du mot de passe d’administrateur que vous avez utilisés lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-215">When prompted, authenticate to the cluster using the admin name (admin) and password you used when creating the cluster.</span></span>

2. <span data-ttu-id="210a4-216">Dans la partie gauche de l’interface utilisateur web d’Ambari, sélectionnez **HDFS**, puis sélectionnez l’onglet **Configurations** au milieu de la page.</span><span class="sxs-lookup"><span data-stu-id="210a4-216">From the left side of the Ambari web UI, select **HDFS** and then select the **Configs** tab in the middle of the page.</span></span>

3. <span data-ttu-id="210a4-217">Sélectionnez l’onglet **Avancé** et faites défiler jusqu’à ce que vous trouviez la section **Configuration core-site personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="210a4-217">Select the **Advanced** tab, and then scroll until you find the **Custom core-site** section.</span></span>

4. <span data-ttu-id="210a4-218">Développez la section **Configuration core-site personnalisée**, puis faites défiler jusqu’à la fin et sélectionnez le lien **Ajouter une propriété...**.</span><span class="sxs-lookup"><span data-stu-id="210a4-218">Expand the **Custom core-site** section, then scroll to the end and select the **Add property...** link.</span></span> <span data-ttu-id="210a4-219">Utilisez les valeurs suivantes pour les champs **Clé** et **Valeur** :</span><span class="sxs-lookup"><span data-stu-id="210a4-219">Use the following values for the **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="210a4-220">**Clé**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="210a4-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="210a4-221">**Valeur**: la SAP retournée par l’application C# ou Python exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="210a4-221">**Value**: The SAS returned by the C# or Python application you ran previously</span></span>

     <span data-ttu-id="210a4-222">Remplacez **CONTAINERNAME** avec le nom du conteneur que vous avez utilisé avec l’application C# ou SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-222">Replace **CONTAINERNAME** with the container name you used with the C# or SAS application.</span></span> <span data-ttu-id="210a4-223">Remplacez **STORAGEACCOUNTNAME** avec le nom du compte de stockage que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="210a4-223">Replace **STORAGEACCOUNTNAME** with the storage account name you used.</span></span>

5. <span data-ttu-id="210a4-224">Cliquez sur le bouton **Ajouter** pour enregistrer cette clé et cette valeur, puis cliquez sur le bouton **Enregistrer** pour enregistrer les modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="210a4-224">Click the **Add** button to save this key and value, then click the **Save** button to save the configuration changes.</span></span> <span data-ttu-id="210a4-225">Lorsque vous y êtes invité, ajoutez une description de la modification (« Ajout d’accès de stockage SAP », par exemple), puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="210a4-225">When prompted, add a description of the change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="210a4-226">Cliquez sur **OK** lorsque les modifications ont été effectuées.</span><span class="sxs-lookup"><span data-stu-id="210a4-226">Click **OK** when the changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="210a4-227">Vous devez redémarrer plusieurs services pour que la modification prenne effet.</span><span class="sxs-lookup"><span data-stu-id="210a4-227">You must restart several services before the change takes effect.</span></span>

6. <span data-ttu-id="210a4-228">Dans l’interface utilisateur web Ambari, sélectionnez **HDFS** dans la liste sur la gauche, puis sélectionnez **Redémarrer tout** dans la liste déroulante **Actions de service** située à droite.</span><span class="sxs-lookup"><span data-stu-id="210a4-228">In the Ambari web UI, select **HDFS** from the list on the left, and then select **Restart All** from the **Service Actions** drop down list on the right.</span></span> <span data-ttu-id="210a4-229">Lorsque vous y êtes invité, sélectionnez **Activer le mode de maintenance**, puis sélectionnez __Conform Restart All".</span><span class="sxs-lookup"><span data-stu-id="210a4-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="210a4-230">Répétez ce processus pour les entrées MapReduce2 et YARN.</span><span class="sxs-lookup"><span data-stu-id="210a4-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="210a4-231">Une fois les services redémarrés, sélectionnez chacun d’entre eux et désactivez le mode maintenance à partir de la liste déroulante **Actions de service**.</span><span class="sxs-lookup"><span data-stu-id="210a4-231">Once the services have restarted, select each one and disable maintenance mode from the **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="210a4-232">Tester l’accès restreint</span><span class="sxs-lookup"><span data-stu-id="210a4-232">Test restricted access</span></span>

<span data-ttu-id="210a4-233">Pour vérifier que vous disposez d’un accès restreint, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="210a4-233">To verify that you have restricted access, use the following methods:</span></span>

* <span data-ttu-id="210a4-234">Pour les clusters HDInsight **basés sur Windows**, utilisez le Bureau à distance pour vous connecter au cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-234">For **Windows-based** HDInsight clusters, use Remote Desktop to connect to the cluster.</span></span> <span data-ttu-id="210a4-235">Pour plus d’informations, consultez [Se connecter à HDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="210a4-235">For more information, see [Connect to HDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="210a4-236">Une fois la connexion établie, utilisez l’icône de **ligne de commande Hadoop** du Bureau pour ouvrir une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="210a4-236">Once connected, use the **Hadoop Command-Line** icon on the desktop to open a command prompt.</span></span>

* <span data-ttu-id="210a4-237">Pour les clusters HDInsight **basés sur Linux** , utilisez SSH pour vous connecter au cluster.</span><span class="sxs-lookup"><span data-stu-id="210a4-237">For **Linux-based** HDInsight clusters, use SSH to connect to the cluster.</span></span> <span data-ttu-id="210a4-238">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="210a4-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="210a4-239">Une fois connecté au cluster, procédez comme suit pour vérifier que vous pouvez uniquement lire et répertorier les éléments sur le compte de stockage SAP :</span><span class="sxs-lookup"><span data-stu-id="210a4-239">Once connected to the cluster, use the following steps to verify that you can only read and list items on the SAS storage account:</span></span>

1. <span data-ttu-id="210a4-240">Pour répertorier le contenu du conteneur, utilisez la commande suivante à partir de l’invite :</span><span class="sxs-lookup"><span data-stu-id="210a4-240">To list the contents of the container, use the following command from the prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="210a4-241">Remplacez **SASCONTAINER** avec le nom du conteneur créé pour le compte de stockage SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-241">Replace **SASCONTAINER** with the name of the container created for the SAS storage account.</span></span> <span data-ttu-id="210a4-242">Remplacez **SASACCOUNTNAME** par le nom du compte de stockage utilisé pour la SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-242">Replace **SASACCOUNTNAME** with the name of the storage account used for the SAS.</span></span>

    <span data-ttu-id="210a4-243">La liste inclut le fichier chargé lors de la création du conteneur et de la SAP.</span><span class="sxs-lookup"><span data-stu-id="210a4-243">The list includes the file uploaded when the container and SAS were created.</span></span>

2. <span data-ttu-id="210a4-244">Utilisez la commande suivante pour vérifier que vous pouvez lire le contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="210a4-244">Use the following command to verify that you can read the contents of the file.</span></span> <span data-ttu-id="210a4-245">Remplacez **SASCONTAINER** et **SASACCOUNTNAME** comme à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="210a4-245">Replace the **SASCONTAINER** and **SASACCOUNTNAME** as in the previous step.</span></span> <span data-ttu-id="210a4-246">Remplacez **FILENAME** avec le nom du fichier affiché dans la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="210a4-246">Replace **FILENAME** with the name of the file displayed in the previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="210a4-247">Cette commande répertorie le contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="210a4-247">This command lists the contents of the file.</span></span>

3. <span data-ttu-id="210a4-248">Pour télécharger le fichier sur le système de fichiers local, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="210a4-248">Use the following command to download the file to the local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="210a4-249">Cette commande télécharge le fichier sur un fichier local nommé **testfile.txt**.</span><span class="sxs-lookup"><span data-stu-id="210a4-249">This command downloads the file to a local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="210a4-250">Utilisez la commande suivante pour charger le fichier local sur un nouveau fichier nommé **testupload.txt** sur le stockage SAP :</span><span class="sxs-lookup"><span data-stu-id="210a4-250">Use the following command to upload the local file to a new file named **testupload.txt** on the SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="210a4-251">Vous recevez un message similaire au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="210a4-251">You receive a message similar to the following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="210a4-252">Cette erreur se produit, car l’emplacement de stockage est en lecture + liste uniquement.</span><span class="sxs-lookup"><span data-stu-id="210a4-252">This error occurs because the storage location is read+list only.</span></span> <span data-ttu-id="210a4-253">Pour placer les données sur le stockage par défaut pour le cluster, accessible en écriture, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="210a4-253">Use the following command to put the data on the default storage for the cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="210a4-254">Cette fois, l’opération doit se terminer normalement.</span><span class="sxs-lookup"><span data-stu-id="210a4-254">This time, the operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="210a4-255">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="210a4-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="210a4-256">Une tâche a été annulée</span><span class="sxs-lookup"><span data-stu-id="210a4-256">A task was canceled</span></span>

<span data-ttu-id="210a4-257">**Symptômes**: lorsque vous créez un cluster à l’aide du script PowerShell, le message d’erreur suivant peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="210a4-257">**Symptoms**: When creating a cluster using the PowerShell script, you may receive the following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="210a4-258">**Cause** : cette erreur peut se produire si vous utilisez un mot de passe pour l’utilisateur admin/HTTP pour le cluster ou pour l’utilisateur SSH (pour les clusters basés sur Linux).</span><span class="sxs-lookup"><span data-stu-id="210a4-258">**Cause**: This error can occur if you use a password for the admin/HTTP user for the cluster, or (for Linux-based clusters) the SSH user.</span></span>

<span data-ttu-id="210a4-259">**Résolution**: utilisez un mot de passe qui répond aux critères suivants :</span><span class="sxs-lookup"><span data-stu-id="210a4-259">**Resolution**: Use a password that meets the following criteria:</span></span>

* <span data-ttu-id="210a4-260">Il doit contenir au moins 10 caractères.</span><span class="sxs-lookup"><span data-stu-id="210a4-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="210a4-261">Il doit contenir au moins un chiffre.</span><span class="sxs-lookup"><span data-stu-id="210a4-261">Must contain at least one digit</span></span>
* <span data-ttu-id="210a4-262">Il doit contenir au moins un caractère non alphanumérique.</span><span class="sxs-lookup"><span data-stu-id="210a4-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="210a4-263">Il doit contenir au moins une lettre minuscule et une lettre majuscule.</span><span class="sxs-lookup"><span data-stu-id="210a4-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="210a4-264">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="210a4-264">Next steps</span></span>

<span data-ttu-id="210a4-265">Maintenant que vous avez appris comment ajouter un stockage à accès limité à votre cluster HDInsight, découvrez d’autres façons de travailler avec des données sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="210a4-265">Now that you have learned how to add limited-access storage to your HDInsight cluster, learn other ways to work with data on your cluster:</span></span>

* [<span data-ttu-id="210a4-266">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="210a4-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="210a4-267">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="210a4-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="210a4-268">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="210a4-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
