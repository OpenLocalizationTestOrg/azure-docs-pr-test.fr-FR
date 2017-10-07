---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - Segments"
description: "Découvrez comment toocreate et gèrent des segments de modèles d’utilisation tooidentify les utilisateurs à l’aide d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="718b6-103">Comment toocreate et gèrent des segments de modèles d’utilisation tooidentify les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="718b6-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="718b6-104">Cet article décrit hello **SEGMENTS** onglet Hello **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="718b6-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="718b6-105">Vous utilisez hello **Mobile Engagement** toomonitor portail et gérer vos applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="718b6-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="718b6-106">section de Segments Hello Hello l’interface utilisateur vous permet de toowork sur la segmentation de vos utilisateurs basés sur un comportement différent hello et analytique que vous pouvez obtenir à partir de l’application hello et est également accessible via l’API de Segments de hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="718b6-107">Segments sont calculées tout d’abord de 24 heures après leur création, et ils sont recalculées toutes les 24 heures en fonction de l’actualité analytique hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="718b6-108">Une fois qu’un segment est calculé, il affiche un graphique de « L’historique de jour tooday » chaque jour.</span><span class="sxs-lookup"><span data-stu-id="718b6-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="718b6-109">De nombreuses sections de hello **Mobile Engagement** interface utilisateur du portail contient hello **afficher l’aide** bouton.</span><span class="sxs-lookup"><span data-stu-id="718b6-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="718b6-110">Appuyez sur ce bouton tooget informations contextuelles supplémentaires sur une section.</span><span class="sxs-lookup"><span data-stu-id="718b6-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="718b6-111">Créer des segments</span><span class="sxs-lookup"><span data-stu-id="718b6-111">Create Segments</span></span>
<span data-ttu-id="718b6-112">Vous pouvez créer un segment en fonction des critères de too10 sur une période spécifique des jours too60 Bonjour passé à partir de la section d’analytique hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="718b6-113">Par exemple, vous pouvez créer un segment basé sur les personnes hello qui disposent de certaines pages consultées ou recherché un contenu spécifique au sein de votre application dans hello des 10 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="718b6-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="718b6-114">Ces informations sont disponibles dans la section d’analytique hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="718b6-115">Par conséquent, vous pouvez l’utiliser toocreate un segment et puis définir un tootarget de notification push ce sous-ensemble d’utilisateurs tooget les toocome toohello arrière application.</span><span class="sxs-lookup"><span data-stu-id="718b6-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="718b6-116">une fois un segment calculé, il ne peut pas être modifié. Il peut uniquement être cloné (copié) ou détruit (supprimé).</span><span class="sxs-lookup"><span data-stu-id="718b6-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="718b6-117">Un segment peut être dupliqué dans hello même application (avec hello même AppID), et il peut également être dupliqué dans d’autres applications (avec un AppID différents).</span><span class="sxs-lookup"><span data-stu-id="718b6-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="718b6-119">Exemples de segments</span><span class="sxs-lookup"><span data-stu-id="718b6-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="718b6-121">Les segments permettent aux utilisateurs finaux de hello toosegment de votre application.</span><span class="sxs-lookup"><span data-stu-id="718b6-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="718b6-122">La segmentation de vos utilisateurs est une stratégie marketing importante.</span><span class="sxs-lookup"><span data-stu-id="718b6-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="718b6-123">Azure Mobile Engagement vous permet de tooget les données historiques et créer des segments personnalisés.</span><span class="sxs-lookup"><span data-stu-id="718b6-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="718b6-124">Cet outil puissant vous permet de toolearn sur l’expérience de vos clients dans votre application.</span><span class="sxs-lookup"><span data-stu-id="718b6-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="718b6-125">Vous pouvez facilement analyser vos segments et les utiliser comme cibles de notification Push.</span><span class="sxs-lookup"><span data-stu-id="718b6-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="718b6-126">Un cas d’usage courant est que vous souhaitez toosend un tooencourage de notification push de vos utilisateurs finaux toorate votre application dans le magasin de hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="718b6-127">Au lieu d’envoyer une notification tooall vos utilisateurs finaux, vous pouvez créer un segment que vous spécifiez uniquement les utilisateurs qui hello mois dernier ont utilisé votre application de tous les jours et ont un utilisateur approprié de rencontrer.</span><span class="sxs-lookup"><span data-stu-id="718b6-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="718b6-128">Avec des notifications Push moins nombreuses et extrêmement ciblées, vous obtenez un meilleur retour sur investissement.</span><span class="sxs-lookup"><span data-stu-id="718b6-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="718b6-130">Vous pouvez créer des segments selon les principaux éléments de Azure Mobile Engagement hello :</span><span class="sxs-lookup"><span data-stu-id="718b6-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="718b6-131">Événement : créer un segment de cet événement spécifique une cible de l’application hello qui se sont produits plus de deux fois par semaine.</span><span class="sxs-lookup"><span data-stu-id="718b6-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="718b6-132">Session : création d’un segment d’utilisateurs qui ont utilisé l’application hello plus de 5 fois la semaine dernière.</span><span class="sxs-lookup"><span data-stu-id="718b6-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="718b6-133">Activité : créez un segment avec les utilisateurs ayant utilisé une page ou un contenu plus ou moins de 10 fois au cours du mois dernier.</span><span class="sxs-lookup"><span data-stu-id="718b6-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="718b6-134">Tâche : créez un segment avec les utilisateurs ayant effectué une tâche plus de deux fois par jour.</span><span class="sxs-lookup"><span data-stu-id="718b6-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="718b6-135">Panne : création d’un segment de tous les utilisateurs de hello qui ont eu une panne plus de 10 fois la semaine dernière.</span><span class="sxs-lookup"><span data-stu-id="718b6-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="718b6-136">(Vous pourriez envoyer une notification Push à ce segment pour présenter des excuses ou offrir un coupon !)</span><span class="sxs-lookup"><span data-stu-id="718b6-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="718b6-137">Erreur : créer un segment de tous les utilisateurs de hello qui ont eu une erreur plus de 100 fois 3 jours.</span><span class="sxs-lookup"><span data-stu-id="718b6-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="718b6-138">Informations sur l’application : créer un segment qui cible un informations personnalisées sur l’application qui se sont produites au cours de hello 25 jours.</span><span class="sxs-lookup"><span data-stu-id="718b6-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="718b6-140">toouse Segment de façon optimale, vous devez effectuer une intégration personnalisée Hello SDK dans votre application avec un plan de marquage de balises de « Application Info ».</span><span class="sxs-lookup"><span data-stu-id="718b6-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="718b6-141">Ensuite, accédez toohello page d’accueil de l’interface de hello, sélectionnez l’application hello et cliquez sur la section « Segments » de hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="718b6-142">Sélectionnez la section « Segments » de hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="718b6-143">Cliquez sur hello « Nouveau segment » bouton toocreate un nouveau segment.</span><span class="sxs-lookup"><span data-stu-id="718b6-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="718b6-144">Exemple en conditions réelles : créer un segment simple en fonction des informations de « Session »</span><span class="sxs-lookup"><span data-stu-id="718b6-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="718b6-145">Création d’un segment de tous les utilisateurs finals hello qui ont utilisé votre application au moins 50 fois Bonjour la semaine dernière.</span><span class="sxs-lookup"><span data-stu-id="718b6-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="718b6-146">À partir de là, trouver uniquement hello aux utilisateurs finaux ont passé au moins 30 secondes dans votre application par session.</span><span class="sxs-lookup"><span data-stu-id="718b6-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="718b6-147">Cette opération affiche tous les hello aux utilisateurs finaux une expérience positive dans votre application.</span><span class="sxs-lookup"><span data-stu-id="718b6-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="718b6-148">Ensuite, segment hello créé peut être utilisé toopush un tooask les utilisateurs finaux de toothese notification les stocker de votre application Bonjour toorate.</span><span class="sxs-lookup"><span data-stu-id="718b6-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="718b6-150">Donnez un nom à votre segment dans l’ordre toofind rapidement dans la liste des « Segment » hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="718b6-151">Cliquez sur hello le bouton « Créer ».</span><span class="sxs-lookup"><span data-stu-id="718b6-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="718b6-153">Sélectionnez Session.</span><span class="sxs-lookup"><span data-stu-id="718b6-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="718b6-155">Sélectionnez la période hello de « Dernière semaine ».</span><span class="sxs-lookup"><span data-stu-id="718b6-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="718b6-156">Cliquez sur Suivant.</span><span class="sxs-lookup"><span data-stu-id="718b6-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="718b6-158">Sélectionnez hello opérateur s’applique parmi la liste de hello : = ; ≥, ≤.</span><span class="sxs-lookup"><span data-stu-id="718b6-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="718b6-159">Entrez le nombre souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="718b6-160">Sélectionnez hello Occurrence souhaité.</span><span class="sxs-lookup"><span data-stu-id="718b6-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="718b6-161">Cliquez sur Suivant.</span><span class="sxs-lookup"><span data-stu-id="718b6-161">Click next.</span></span>
   <span data-ttu-id="718b6-162">Cet exemple est défini afin que plus hello semaine dernière, les utilisateurs de correspondance qui ont effectué au moins 50 sessions.</span><span class="sxs-lookup"><span data-stu-id="718b6-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="718b6-164">Pour hello segmentation de Session, vous pouvez choisir la longueur de hello par session comme critère de.</span><span class="sxs-lookup"><span data-stu-id="718b6-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="718b6-165">Sélectionnez hello opérateur à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="718b6-166">Fournissez hello longueur par session.</span><span class="sxs-lookup"><span data-stu-id="718b6-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="718b6-167">Cliquez sur Suivant.</span><span class="sxs-lookup"><span data-stu-id="718b6-167">Click Next.</span></span>
   <span data-ttu-id="718b6-168">Dans cet exemple, il indique que sur toutes les hello sessions qui ont été partagées sur une section d’occurrence hello, sélectionnez uniquement hello les utilisateurs qui ont passé à plus de 30 secondes par session.</span><span class="sxs-lookup"><span data-stu-id="718b6-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="718b6-170">Nom de votre critère dans tooretrieve order dans hello terminer en entonnoir, puis cliquez sur Terminer.</span><span class="sxs-lookup"><span data-stu-id="718b6-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="718b6-172">Lorsque vous avez défini votre critère, il apparaît dans l’entonnoir de segment hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="718b6-173">Comme un segment est basé sur les données d'analyse, les segments sont calculés une fois par jour.</span><span class="sxs-lookup"><span data-stu-id="718b6-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="718b6-174">Dans cet exemple, 47,7 % des utilisateurs finaux de total hello mis en correspondance le critère de hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="718b6-175">Ils doivent être des utilisateurs de hello qui ont une bonne expérience et s’être tooprovide susceptible d’une évaluation supérieure si vous les envoyez une notification leur demandant application hello de toorate dans le magasin de hello.</span><span class="sxs-lookup"><span data-stu-id="718b6-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="718b6-176">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="718b6-176">See also</span></span>
* <span data-ttu-id="718b6-177">[Concepts][Link 6]</span><span class="sxs-lookup"><span data-stu-id="718b6-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="718b6-178">[Service de guide de résolution des problèmes][Link 24]</span><span class="sxs-lookup"><span data-stu-id="718b6-178">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

