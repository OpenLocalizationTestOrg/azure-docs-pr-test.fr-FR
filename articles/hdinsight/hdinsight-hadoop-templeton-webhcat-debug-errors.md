---
title: "aaaUnderstand et résoudre les erreurs WebHCat sur HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment les erreurs courantes tooabout retourné par WebHCat sur HDInsight et tooresolve les."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>Compréhension et résolution des erreurs reçues à partir de WebHCat sur HDInsight

En savoir plus sur les erreurs reçues lors de l’utilisation de WebHCat hdinsight et comment tooresolve les. WebHCat est utilisée en interne par les outils côté client telles que Azure PowerShell et hello Data Lake Tools pour Visual Studio.

## <a name="what-is-webhcat"></a>Présentation de WebHCat

[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) est une API REST pour [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), une couche de gestion du stockage et des tables pour Hadoop. WebHCat est activé par défaut sur les clusters HDInsight et est utilisé par les travaux de toosubmit différents outils, obtenir l’état du travail, etc. sans session toohello cluster.

## <a name="modifying-configuration"></a>Modification de la configuration

> [!IMPORTANT]
> Plusieurs erreurs de hello répertoriées dans ce document se produire si une configuration maximale a été dépassée. Lors de l’étape de résolution hello mentionne que vous pouvez modifier une valeur, vous devez utiliser une des hello suivant tooperform hello modification :

* Pour **Windows** clusters : utilisez une valeur de script action tooconfigure hello lors de la création du cluster. Pour en savoir plus, consultez la rubrique [Développement d’actions de script avec HDInsight](hdinsight-hadoop-script-actions.md).

* Pour **Linux** clusters : valeur de hello toomodify Ambari d’utilisation (web ou l’API REST). Pour en savoir plus, consultez la rubrique [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="default-configuration"></a>Configuration par défaut

Si hello les valeurs par défaut suivantes est dépassé, il peut dégrader les performances de WebHCat ou de provoquer des erreurs :

| Paramètre | Résultat | Valeur par défaut |
| --- | --- | --- |
| [yarn.scheduler.capacity.maximum-applications][maximum-applications] |nombre maximal de tâches pouvant être actives simultanément de Hello (en attente ou en cours d’exécution) |10 000 |
| [templeton.exec.max-procs][max-procs] |nombre maximal de Hello de demandes qui peuvent être traités simultanément |20 |
| [mapreduce.jobhistory.max-age-ms][max-age-ms] |nombre de Hello de jours pendant lesquels l’historique des travaux est conservé. |7 jours |

## <a name="too-many-requests"></a>Trop de demandes

**Code d’état HTTP**: 429

| Cause : | Résolution : |
| --- | --- |
| Vous avez dépassé les requêtes simultanées maximales hello pris en charge par WebHCat par minute (valeur par défaut 20) |Réduire votre tooensure de charge de travail que vous ne pas envoyer plus de hello nombre maximal de demandes simultanées ou augmenter la limite de demandes simultanées hello en modifiant `templeton.exec.max-procs`. Pour en savoir plus, consultez la section [Modification de la configuration](#modifying-configuration) |

## <a name="server-unavailable"></a>Serveur non disponible

**Code d’état HTTP**: 503

| Cause : | Résolution : |
| --- | --- |
| Ce code d’état se produit généralement lors du basculement entre hello principaux et secondaires nœud principal de cluster de hello |Patientez deux minutes, puis recommencez l’opération de hello |

## <a name="bad-request-content-could-not-find-job"></a>Contenu de demande erroné : impossible de trouver la tâche

**Code d’état HTTP**: 400

| Cause : | Résolution : |
| --- | --- |
| Détails de la tâche ont été nettoyés par l’historique des travaux hello nettoyeur |période de rétention par défaut Hello pour l’historique des travaux est de 7 jours. période de rétention par défaut Hello peut être changée en modifiant `mapreduce.jobhistory.max-age-ms`. Pour en savoir plus, consultez la section [Modification de la configuration](#modifying-configuration) |
| Tâche qui a été supprimée en raison du basculement de tooa |Réessayer la soumission de travaux pour les tootwo minutes |
| L’ID de cette tâche n’est pas valide |Vérifiez si l’id de tâche hello est correct |

## <a name="bad-gateway"></a>Passerelle incorrecte

**Code d’état HTTP**: 502

| Cause : | Résolution : |
| --- | --- |
| Nettoyage de la mémoire interne se produit dans hello WebHCat processus |Attendez que le garbage collection toofinish ou redémarrez le service WebHCat de hello |
| Délai d’attente en attente sur une réponse de hello ResourceManager service. Cette erreur peut se produire lorsque plusieurs hello applications actives devient maximum de hello configuré (par défaut 10 000) |Attendez que toocomplete de travaux en cours d’exécution ou augmenter la limite de travaux simultanés hello en modifiant `yarn.scheduler.capacity.maximum-applications`. Pour plus d’informations, consultez hello [modification configuration](#modifying-configuration) section. |
| Tentative de toutes les tâches via hello tooretrieve [/Jobs GET](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) appel alors `Fields` est défini trop`*` |Ne récupérez pas *tous* les détails des tâches. Utilisez à la place `jobid` tooretrieve les détails des tâches supérieurs uniquement à certain id de tâche. Ou n’utilisez pas `Fields` |
| Hello service WebHCat est arrêté pendant le basculement de nœud principal |Patientez deux minutes et recommencez l’opération de hello |
| Plus de 500 tâches en attente ont été envoyées via WebHCat |Veuillez patienter le temps que les tâches en attente se terminent avant d’envoyer d’autres tâches |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
