---
title: aaaUse Azure Backup tooreplace votre infrastructure de bande | Documents Microsoft
description: "Découvrez comment Azure Backup offre une sémantique de type bande qui vous permet de toobackup et restaurer des données dans Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a>Déplacer le stockage à long terme à partir de la bande toohello cloud Azure
Les clients Azure Backup et System Center Data Protection Manager peuvent effectuer les actions suivantes :

* Sauvegarder les données de planifications qui en fonction de besoins d’organisation de hello.
* Conserver les données de sauvegarde de hello pendant des périodes plus longues
* intégrer Azure à leurs besoins de rétention à long terme (à la place d’une bande).

Cet article explique comment les clients peuvent mettre en place des stratégies de sauvegarde et de rétention. Les clients qui utilisent des bandes tooaddress leur long-terme rétention doit maintenant avoir une alternative puissante et viable avec disponibilité hello de cette fonctionnalité. fonction Hello est activée dans la version la plus récente de hello Azure Backup hello (qui est disponible [ici](http://aka.ms/azurebackup_agent)). Les clients System Center DPM doivent mettre à jour avec, au minimum, DPM 2012 R2 UR5 avant d’utiliser DPM avec hello service sauvegarde Azure.

## <a name="what-is-hello-backup-schedule"></a>Nouveautés hello la planification de sauvegarde
planification de sauvegarde Hello indique la fréquence de hello hello d’opération de sauvegarde. Par exemple, les paramètres de hello Bonjour suivant écran indiquent que les sauvegardes sont effectuées tous les jours à 6 h 00 et à minuit.

![Planification quotidienne](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

Les clients peuvent également planifier une sauvegarde hebdomadaire. Par exemple, hello paramètres Bonjour suivant écran indiquent que les sauvegardes sont effectuées chaque autre dimanche & mercredi à 9 h 30 et 1:00 AM.

![Planification hebdomadaire](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a>Qu’est hello stratégie de rétention ?
stratégie de rétention Hello spécifie la durée hello pour lequel la sauvegarde de hello doit être stockée. Plutôt que de simplement spécifier « stratégie plate » pour tous les points de sauvegarde, les clients peuvent spécifier des stratégies de rétention différentes en fonction de lors de la sauvegarde de hello est effectuée. Par exemple, hello point de sauvegarde effectuée chaque jour, qui sert d’un point de récupération opérationnelle, est conservé pendant 90 jours. point de sauvegarde Hello effectuée à la fin de hello de chaque trimestre à des fins d’audit est conservé pendant une longue période.

![Stratégie de rétention](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

Hello nombre total de « points de rétention » spécifié dans cette stratégie est 90 (points quotidiennes) + 40 (une pour chaque trimestre pendant 10 ans) = 130.

## <a name="example--putting-both-together"></a>Exemple – Combinaison des deux
![Exemple d’écran](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. **Stratégie de rétention quotidienne**: les sauvegardes effectuées quotidiennement sont stockées pendant sept jours.
2. **Stratégie de rétention hebdomadaire**: les sauvegardes effectuées tous les jours à minuit et à 18 h 00 le samedi sont conservées pendant quatre semaines.
3. **Stratégie de rétention mensuelle**: les sauvegardes effectuées à minuit et 6 h 00 sur hello dernier samedi de chaque mois sont conservés pendant 12 mois
4. **Stratégie de rétention annuelle**: les sauvegardes effectuées à minuit hello dernier samedi de mars, chaque sont conservées pendant 10 ans

Hello nombre total de « points de rétention » (à partir de laquelle un client peut restaurer les données de points) Bonjour diagramme précédent est calculée comme suit :

* deux points par jour pendant sept jours = 14 points de récupération
* deux points par semaine pendant quatre semaines = huit points de récupération
* deux points par mois pendant 12 mois = 24 points de récupération
* un point par an pendant 10 ans = 10 points de récupération

Nombre total de Hello de points de récupération est 56.

> [!NOTE]
> La sauvegarde Azure n'impose aucune restriction sur le nombre de points de récupération.
>
>

## <a name="advanced-configuration"></a>Configuration avancée
En cliquant sur **modifier** Bonjour précédant l’écran, les clients ont davantage de flexibilité lors de la spécification des planifications de rétention.

![Modifier](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la Sauvegarde Azure, consultez :

* [Introduction tooAzure sauvegarde](backup-introduction-to-azure-backup.md)
* [Test d’Azure Backup](backup-try-azure-backup-in-10-mins.md)
