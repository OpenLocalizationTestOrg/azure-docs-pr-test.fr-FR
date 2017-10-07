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
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="c6d95-103">Déplacer le stockage à long terme à partir de la bande toohello cloud Azure</span><span class="sxs-lookup"><span data-stu-id="c6d95-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="c6d95-104">Les clients Azure Backup et System Center Data Protection Manager peuvent effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c6d95-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="c6d95-105">Sauvegarder les données de planifications qui en fonction de besoins d’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="c6d95-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="c6d95-106">Conserver les données de sauvegarde de hello pendant des périodes plus longues</span><span class="sxs-lookup"><span data-stu-id="c6d95-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="c6d95-107">intégrer Azure à leurs besoins de rétention à long terme (à la place d’une bande).</span><span class="sxs-lookup"><span data-stu-id="c6d95-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="c6d95-108">Cet article explique comment les clients peuvent mettre en place des stratégies de sauvegarde et de rétention.</span><span class="sxs-lookup"><span data-stu-id="c6d95-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="c6d95-109">Les clients qui utilisent des bandes tooaddress leur long-terme rétention doit maintenant avoir une alternative puissante et viable avec disponibilité hello de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c6d95-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="c6d95-110">fonction Hello est activée dans la version la plus récente de hello Azure Backup hello (qui est disponible [ici](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="c6d95-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="c6d95-111">Les clients System Center DPM doivent mettre à jour avec, au minimum, DPM 2012 R2 UR5 avant d’utiliser DPM avec hello service sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d95-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="c6d95-112">Nouveautés hello la planification de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="c6d95-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="c6d95-113">planification de sauvegarde Hello indique la fréquence de hello hello d’opération de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="c6d95-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="c6d95-114">Par exemple, les paramètres de hello Bonjour suivant écran indiquent que les sauvegardes sont effectuées tous les jours à 6 h 00 et à minuit.</span><span class="sxs-lookup"><span data-stu-id="c6d95-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Planification quotidienne](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="c6d95-116">Les clients peuvent également planifier une sauvegarde hebdomadaire.</span><span class="sxs-lookup"><span data-stu-id="c6d95-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="c6d95-117">Par exemple, hello paramètres Bonjour suivant écran indiquent que les sauvegardes sont effectuées chaque autre dimanche & mercredi à 9 h 30 et 1:00 AM.</span><span class="sxs-lookup"><span data-stu-id="c6d95-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Planification hebdomadaire](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="c6d95-119">Qu’est hello stratégie de rétention ?</span><span class="sxs-lookup"><span data-stu-id="c6d95-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="c6d95-120">stratégie de rétention Hello spécifie la durée hello pour lequel la sauvegarde de hello doit être stockée.</span><span class="sxs-lookup"><span data-stu-id="c6d95-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="c6d95-121">Plutôt que de simplement spécifier « stratégie plate » pour tous les points de sauvegarde, les clients peuvent spécifier des stratégies de rétention différentes en fonction de lors de la sauvegarde de hello est effectuée.</span><span class="sxs-lookup"><span data-stu-id="c6d95-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="c6d95-122">Par exemple, hello point de sauvegarde effectuée chaque jour, qui sert d’un point de récupération opérationnelle, est conservé pendant 90 jours.</span><span class="sxs-lookup"><span data-stu-id="c6d95-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="c6d95-123">point de sauvegarde Hello effectuée à la fin de hello de chaque trimestre à des fins d’audit est conservé pendant une longue période.</span><span class="sxs-lookup"><span data-stu-id="c6d95-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Stratégie de rétention](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="c6d95-125">Hello nombre total de « points de rétention » spécifié dans cette stratégie est 90 (points quotidiennes) + 40 (une pour chaque trimestre pendant 10 ans) = 130.</span><span class="sxs-lookup"><span data-stu-id="c6d95-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="c6d95-126">Exemple – Combinaison des deux</span><span class="sxs-lookup"><span data-stu-id="c6d95-126">Example – Putting both together</span></span>
![Exemple d’écran](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="c6d95-128">**Stratégie de rétention quotidienne**: les sauvegardes effectuées quotidiennement sont stockées pendant sept jours.</span><span class="sxs-lookup"><span data-stu-id="c6d95-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="c6d95-129">**Stratégie de rétention hebdomadaire**: les sauvegardes effectuées tous les jours à minuit et à 18 h 00 le samedi sont conservées pendant quatre semaines.</span><span class="sxs-lookup"><span data-stu-id="c6d95-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="c6d95-130">**Stratégie de rétention mensuelle**: les sauvegardes effectuées à minuit et 6 h 00 sur hello dernier samedi de chaque mois sont conservés pendant 12 mois</span><span class="sxs-lookup"><span data-stu-id="c6d95-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="c6d95-131">**Stratégie de rétention annuelle**: les sauvegardes effectuées à minuit hello dernier samedi de mars, chaque sont conservées pendant 10 ans</span><span class="sxs-lookup"><span data-stu-id="c6d95-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="c6d95-132">Hello nombre total de « points de rétention » (à partir de laquelle un client peut restaurer les données de points) Bonjour diagramme précédent est calculée comme suit :</span><span class="sxs-lookup"><span data-stu-id="c6d95-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="c6d95-133">deux points par jour pendant sept jours = 14 points de récupération</span><span class="sxs-lookup"><span data-stu-id="c6d95-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="c6d95-134">deux points par semaine pendant quatre semaines = huit points de récupération</span><span class="sxs-lookup"><span data-stu-id="c6d95-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="c6d95-135">deux points par mois pendant 12 mois = 24 points de récupération</span><span class="sxs-lookup"><span data-stu-id="c6d95-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="c6d95-136">un point par an pendant 10 ans = 10 points de récupération</span><span class="sxs-lookup"><span data-stu-id="c6d95-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="c6d95-137">Nombre total de Hello de points de récupération est 56.</span><span class="sxs-lookup"><span data-stu-id="c6d95-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="c6d95-138">La sauvegarde Azure n'impose aucune restriction sur le nombre de points de récupération.</span><span class="sxs-lookup"><span data-stu-id="c6d95-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="c6d95-139">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="c6d95-139">Advanced configuration</span></span>
<span data-ttu-id="c6d95-140">En cliquant sur **modifier** Bonjour précédant l’écran, les clients ont davantage de flexibilité lors de la spécification des planifications de rétention.</span><span class="sxs-lookup"><span data-stu-id="c6d95-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modifier](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="c6d95-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c6d95-142">Next Steps</span></span>
<span data-ttu-id="c6d95-143">Pour plus d’informations sur la Sauvegarde Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="c6d95-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="c6d95-144">Introduction tooAzure sauvegarde</span><span class="sxs-lookup"><span data-stu-id="c6d95-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="c6d95-145">Test d’Azure Backup</span><span class="sxs-lookup"><span data-stu-id="c6d95-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
