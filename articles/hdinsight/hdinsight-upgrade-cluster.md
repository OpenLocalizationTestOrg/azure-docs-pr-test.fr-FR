---
title: "Mettre à niveau le cluster HDInsight avec une version plus récente - Azure | Microsoft Docs"
description: "Découvrez comment mettre à niveau le cluster HDInsight vers une version plus récente."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: fa2e37bd922690322ccc3d8f68128180d013b701
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="30ae0-103">Mettre à niveau le cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="30ae0-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="30ae0-104">Pour tirer parti des dernières fonctionnalités proposées par HDInsight, nous vous recommandons de mettre à niveau les clusters HDInsight vers la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="30ae0-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="30ae0-105">Suivez les instructions ci-dessous pour mettre à niveau vos clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="30ae0-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="30ae0-106">Les clusters HDInsight version 3.2 et 3.3 seront bientôt obsolètes.</span><span class="sxs-lookup"><span data-stu-id="30ae0-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="30ae0-107">Pour obtenir des informations sur les versions HDInsight prises en charge, consultez [Quels sont les différents composants Hadoop disponibles avec HDInsight ?](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="30ae0-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="30ae0-108">Tâches de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="30ae0-108">Upgrade tasks</span></span>
<span data-ttu-id="30ae0-109">Le workflow pour mettre à niveau un cluster HDInsight est le suivant :</span><span class="sxs-lookup"><span data-stu-id="30ae0-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![Schéma du workflow de mise à niveau](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="30ae0-111">Lisez chaque section de ce document pour comprendre les modifications qui peuvent être nécessaires lors de la mise à jour de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="30ae0-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="30ae0-112">Créez un cluster comme environnement de test ou d’assurance qualité.</span><span class="sxs-lookup"><span data-stu-id="30ae0-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="30ae0-113">Pour plus d’informations sur la création d’un cluster, consultez [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="30ae0-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="30ae0-114">Copiez les travaux, sources de données et récepteurs existants dans le nouvel environnement.</span><span class="sxs-lookup"><span data-stu-id="30ae0-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="30ae0-115">Pour plus d’informations, consultez la section [Copier des données dans l’environnement de test](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment).</span><span class="sxs-lookup"><span data-stu-id="30ae0-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="30ae0-116">Effectuez des tests de validation pour vérifier que vos tâches fonctionnent comme prévu sur le nouveau cluster.</span><span class="sxs-lookup"><span data-stu-id="30ae0-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="30ae0-117">Une fois que vous avez vérifié que tout fonctionne comme prévu, planifiez un temps d’arrêt pour la migration.</span><span class="sxs-lookup"><span data-stu-id="30ae0-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="30ae0-118">Pendant ce temps d’arrêt, effectuez les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="30ae0-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="30ae0-119">Sauvegardez toutes les données temporaires stockées localement sur les nœuds du cluster,</span><span class="sxs-lookup"><span data-stu-id="30ae0-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="30ae0-120">par exemple si vous avez des données stockées directement sur un nœud principal.</span><span class="sxs-lookup"><span data-stu-id="30ae0-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="30ae0-121">Supprimez le cluster existant.</span><span class="sxs-lookup"><span data-stu-id="30ae0-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="30ae0-122">Créez un cluster dans le même sous-réseau de réseau virtuel avec la version HDI la plus récente (ou prise en charge) à l’aide du même magasin de données par défaut que le cluster précédent a utilisé.</span><span class="sxs-lookup"><span data-stu-id="30ae0-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="30ae0-123">Cela permet au nouveau cluster de continuer à travailler sur vos données de production existantes.</span><span class="sxs-lookup"><span data-stu-id="30ae0-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="30ae0-124">Importez toutes les données temporaires que vous avez sauvegardées.</span><span class="sxs-lookup"><span data-stu-id="30ae0-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="30ae0-125">Démarrez des tâches ou poursuivez le traitement avec le nouveau cluster.</span><span class="sxs-lookup"><span data-stu-id="30ae0-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30ae0-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30ae0-126">Next Steps</span></span>
* [<span data-ttu-id="30ae0-127">Création de clusters Hadoop basés sur Linux dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="30ae0-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="30ae0-128">Se connecter à HDInsight à l’aide de SSH</span><span class="sxs-lookup"><span data-stu-id="30ae0-128">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="30ae0-129">Gérer des clusters HDInsight à l’aide de l’interface utilisateur Web d’Ambari</span><span class="sxs-lookup"><span data-stu-id="30ae0-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

