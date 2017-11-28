---
title: "version plus récente du tooa cluster HDInsight aaaUpgrade-Azure | Documents Microsoft"
description: "Découvrez comment tooUpgrade HDInsight de cluster version plus récente de tooa."
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
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="cd102-103">Mise à niveau de version plus récente du tooa cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd102-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="cd102-104">avantage tootake de hello dernières fonctionnalités HDInsight, nous recommandons que les clusters HDInsight être mis à niveau toolatest version.</span><span class="sxs-lookup"><span data-stu-id="cd102-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="cd102-105">Suivez hello ci-dessous les instructions tooupgrade les versions à votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd102-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="cd102-106">Les clusters HDInsight version 3.2 et 3.3 seront bientôt obsolètes.</span><span class="sxs-lookup"><span data-stu-id="cd102-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="cd102-107">Pour obtenir des informations sur les versions HDInsight prises en charge, consultez [Quels sont les différents composants Hadoop disponibles avec HDInsight ?](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="cd102-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="cd102-108">Tâches de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="cd102-108">Upgrade tasks</span></span>
<span data-ttu-id="cd102-109">Hello workflow tooupgrade HDInsight Cluster est la suivante.</span><span class="sxs-lookup"><span data-stu-id="cd102-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![Schéma du workflow de mise à niveau](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="cd102-111">Lisez chaque section de ce document toounderstand les modifications qui peuvent être requises lors de la mise à niveau votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd102-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="cd102-112">Créez un cluster comme environnement de test ou d’assurance qualité.</span><span class="sxs-lookup"><span data-stu-id="cd102-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="cd102-113">Pour plus d’informations sur la création d’un cluster, consultez [apprendre comment toocreate clusters HDInsight de basés sur Linux](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="cd102-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="cd102-114">Copie des travaux, des sources de données et récepteurs toohello nouvel environnement.</span><span class="sxs-lookup"><span data-stu-id="cd102-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="cd102-115">Consultez [tooTest de copier des données environnement](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="cd102-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="cd102-116">Effectuer une validation test toomake assurer que vos tâches fonctionnent comme prévu sur le nouveau cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="cd102-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="cd102-117">Une fois que vous avez vérifié que tout fonctionne comme prévu, planifier des temps d’arrêt pour la migration de hello.</span><span class="sxs-lookup"><span data-stu-id="cd102-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="cd102-118">Pendant ce temps mort, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cd102-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="cd102-119">Sauvegardez toutes les données temporaires stockées localement sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cd102-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="cd102-120">par exemple si vous avez des données stockées directement sur un nœud principal.</span><span class="sxs-lookup"><span data-stu-id="cd102-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="cd102-121">Supprimer le cluster existant de hello.</span><span class="sxs-lookup"><span data-stu-id="cd102-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="cd102-122">Créer un cluster Bonjour même réseau virtuel sous-réseau avec la plus récente (ou pris en charge) HDI version à l’aide de hello même magasin de données par défaut hello précédent cluster utilisé.</span><span class="sxs-lookup"><span data-stu-id="cd102-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="cd102-123">Cela permet de nouveaux toocontinue de cluster hello travailler sur vos données de production existant.</span><span class="sxs-lookup"><span data-stu-id="cd102-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="cd102-124">Importez toutes les données temporaires que vous avez sauvegardées.</span><span class="sxs-lookup"><span data-stu-id="cd102-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="cd102-125">Début travaux/continuer le traitement à l’aide du nouveau cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="cd102-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd102-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd102-126">Next Steps</span></span>
* [<span data-ttu-id="cd102-127">Découvrez comment toocreate clusters HDInsight de basés sur Linux</span><span class="sxs-lookup"><span data-stu-id="cd102-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="cd102-128">Se connecter tooHDInsight à l’aide de SSH</span><span class="sxs-lookup"><span data-stu-id="cd102-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="cd102-129">Gérer des clusters HDInsight à l’aide de l’interface utilisateur Web d’Ambari</span><span class="sxs-lookup"><span data-stu-id="cd102-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

