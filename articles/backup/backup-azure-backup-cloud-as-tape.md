---
title: Utiliser Sauvegarde Azure pour remplacer votre infrastructure sur bande | Microsoft Docs
description: "Découvrez comment Azure Backup fournit une sémantique de type bande qui permet de sauvegarder et de restaurer des données dans Azure."
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
ms.openlocfilehash: f0f3152daf5f91f7c9e540797bf09b21969d2d33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="c0d0b-103">Déplacement de votre stockage à long terme de la bande vers le cloud Azure</span><span class="sxs-lookup"><span data-stu-id="c0d0b-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="c0d0b-104">Les clients Azure Backup et System Center Data Protection Manager peuvent effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c0d0b-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="c0d0b-105">sauvegarder leurs données selon des planifications qui correspondent le mieux aux besoins de l’organisation ;</span><span class="sxs-lookup"><span data-stu-id="c0d0b-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="c0d0b-106">conserver les données sauvegardées pendant plus longtemps ;</span><span class="sxs-lookup"><span data-stu-id="c0d0b-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="c0d0b-107">intégrer Azure à leurs besoins de rétention à long terme (à la place d’une bande).</span><span class="sxs-lookup"><span data-stu-id="c0d0b-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="c0d0b-108">Cet article explique comment les clients peuvent mettre en place des stratégies de sauvegarde et de rétention.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="c0d0b-109">Les clients qui utilisent des bandes pour répondre à leurs besoins de rétention à long terme disposent désormais d’une alternative puissante et viable grâce à cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="c0d0b-110">La fonctionnalité est activée dans la dernière version d’Azure Backup (disponible [ici](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="c0d0b-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="c0d0b-111">Les clients System Center DPM doivent passer, au minimum, à DPM 2012 R2 UR5 avant d’utiliser DPM avec le service de Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="c0d0b-112">Qu’est-ce que la planification de sauvegarde ?</span><span class="sxs-lookup"><span data-stu-id="c0d0b-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="c0d0b-113">La planification de sauvegarde indique la fréquence de l'opération de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="c0d0b-114">Par exemple, les paramètres dans l’écran suivant indiquent que les sauvegardes sont effectuées tous les jours à 18 h 00 et à minuit.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Planification quotidienne](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="c0d0b-116">Les clients peuvent également planifier une sauvegarde hebdomadaire.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="c0d0b-117">Par exemple, les paramètres de l’écran suivant indiquent que les sauvegardes sont effectuées le dimanche et le mercredi à 9 h 30 et à 1 h 00.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Planification hebdomadaire](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="c0d0b-119">Qu’est-ce que la stratégie de rétention ?</span><span class="sxs-lookup"><span data-stu-id="c0d0b-119">What is the Retention Policy?</span></span>
<span data-ttu-id="c0d0b-120">La stratégie de rétention spécifie la durée de stockage de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="c0d0b-121">Au lieu de simplement spécifier une même stratégie pour tous les points de sauvegarde, les clients peuvent spécifier différentes stratégies de rétention en fonction du moment où est effectuée la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="c0d0b-122">Par exemple, le point de sauvegarde effectué quotidiennement, qui sert de point de récupération opérationnel, est conservé pendant 90 jours.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="c0d0b-123">Le point de sauvegarde effectué à la fin de chaque trimestre à des fins d’audit est conservé pendant une durée plus longue.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Stratégie de rétention](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="c0d0b-125">Le nombre total de « points de rétention » spécifié dans cette stratégie est 90 (points quotidiens) + 40 (un par trimestre pendant 10 ans) = 130.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="c0d0b-126">Exemple – Combinaison des deux</span><span class="sxs-lookup"><span data-stu-id="c0d0b-126">Example – Putting both together</span></span>
![Exemple d’écran](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="c0d0b-128">**Stratégie de rétention quotidienne**: les sauvegardes effectuées quotidiennement sont stockées pendant sept jours.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="c0d0b-129">**Stratégie de rétention hebdomadaire**: les sauvegardes effectuées tous les jours à minuit et à 18 h 00 le samedi sont conservées pendant quatre semaines.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="c0d0b-130">**Stratégie de rétention mensuelle**: les sauvegardes effectuées le dernier samedi de chaque mois à minuit et à 18 h 00 sont conservées pendant 12 mois.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="c0d0b-131">**Stratégie de rétention annuelle**: les sauvegardes effectuées le dernier samedi de chaque mois de mars à minuit sont conservées pendant 10 ans.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="c0d0b-132">Le nombre total de « points de rétention » (points à partir duquel un client peut restaurer des données) dans le schéma précédent est calculé comme suit :</span><span class="sxs-lookup"><span data-stu-id="c0d0b-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="c0d0b-133">deux points par jour pendant sept jours = 14 points de récupération</span><span class="sxs-lookup"><span data-stu-id="c0d0b-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="c0d0b-134">deux points par semaine pendant quatre semaines = huit points de récupération</span><span class="sxs-lookup"><span data-stu-id="c0d0b-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="c0d0b-135">deux points par mois pendant 12 mois = 24 points de récupération</span><span class="sxs-lookup"><span data-stu-id="c0d0b-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="c0d0b-136">un point par an pendant 10 ans = 10 points de récupération</span><span class="sxs-lookup"><span data-stu-id="c0d0b-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="c0d0b-137">Le nombre total de points de récupération est 56.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d0b-138">La sauvegarde Azure n'impose aucune restriction sur le nombre de points de récupération.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="c0d0b-139">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="c0d0b-139">Advanced configuration</span></span>
<span data-ttu-id="c0d0b-140">En cliquant sur **Modifier** dans l’écran précédent, les clients peuvent spécifier les planifications de rétention de manière plus flexible.</span><span class="sxs-lookup"><span data-stu-id="c0d0b-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modifier](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="c0d0b-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0d0b-142">Next Steps</span></span>
<span data-ttu-id="c0d0b-143">Pour plus d’informations sur la Sauvegarde Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="c0d0b-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="c0d0b-144">Présentation d’Azure Backup</span><span class="sxs-lookup"><span data-stu-id="c0d0b-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="c0d0b-145">Test d’Azure Backup</span><span class="sxs-lookup"><span data-stu-id="c0d0b-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
