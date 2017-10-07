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
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>Mise à niveau de version plus récente du tooa cluster HDInsight
avantage tootake de hello dernières fonctionnalités HDInsight, nous recommandons que les clusters HDInsight être mis à niveau toolatest version. Suivez hello ci-dessous les instructions tooupgrade les versions à votre cluster HDInsight.

> [!NOTE]
> Les clusters HDInsight version 3.2 et 3.3 seront bientôt obsolètes. Pour obtenir des informations sur les versions HDInsight prises en charge, consultez [Quels sont les différents composants Hadoop disponibles avec HDInsight ?](hdinsight-component-versioning.md#supported-hdinsight-versions).
>
>

## <a name="upgrade-tasks"></a>Tâches de mise à niveau
Hello workflow tooupgrade HDInsight Cluster est la suivante.

![Schéma du workflow de mise à niveau](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. Lisez chaque section de ce document toounderstand les modifications qui peuvent être requises lors de la mise à niveau votre cluster HDInsight.
2. Créez un cluster comme environnement de test ou d’assurance qualité. Pour plus d’informations sur la création d’un cluster, consultez [apprendre comment toocreate clusters HDInsight de basés sur Linux](hdinsight-hadoop-provision-linux-clusters.md)
3. Copie des travaux, des sources de données et récepteurs toohello nouvel environnement. Consultez [tooTest de copier des données environnement](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) pour plus d’informations.
4. Effectuer une validation test toomake assurer que vos tâches fonctionnent comme prévu sur le nouveau cluster de hello.


Une fois que vous avez vérifié que tout fonctionne comme prévu, planifier des temps d’arrêt pour la migration de hello. Pendant ce temps mort, hello comme suit :

1.  Sauvegardez toutes les données temporaires stockées localement sur les nœuds de cluster hello. par exemple si vous avez des données stockées directement sur un nœud principal.
2.  Supprimer le cluster existant de hello.
3.  Créer un cluster Bonjour même réseau virtuel sous-réseau avec la plus récente (ou pris en charge) HDI version à l’aide de hello même magasin de données par défaut hello précédent cluster utilisé. Cela permet de nouveaux toocontinue de cluster hello travailler sur vos données de production existant.
4.  Importez toutes les données temporaires que vous avez sauvegardées.
5.  Début travaux/continuer le traitement à l’aide du nouveau cluster de hello.

## <a name="next-steps"></a>Étapes suivantes
* [Découvrez comment toocreate clusters HDInsight de basés sur Linux](hdinsight-hadoop-provision-linux-clusters.md)
* [Se connecter tooHDInsight à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Gérer des clusters HDInsight à l’aide de l’interface utilisateur Web d’Ambari](hdinsight-hadoop-manage-ambari.md)

