---
title: aaaAzure Interface utilisateur de Mobile Engagement - atteindre
description: "Découvrez comment tooreach les toohello les utilisateurs de votre application avec les notifications push à l’aide d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="60d8e-103">Comment tooreach les toohello les utilisateurs de votre application avec des notifications push</span><span class="sxs-lookup"><span data-stu-id="60d8e-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="60d8e-104">Cet article décrit hello **atteindre** onglet Hello **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="60d8e-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="60d8e-105">Vous utilisez hello **Mobile Engagement** toomonitor portail et gérer vos applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="60d8e-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="60d8e-106">Notez que toostart à l’aide du portail hello vous devez tout d’abord toocreate un **Azure Mobile Engagement** compte.</span><span class="sxs-lookup"><span data-stu-id="60d8e-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="60d8e-107">Pour plus d'informations, consultez [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="60d8e-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="60d8e-108">Hello atteindre section Hello interface utilisateur de l’outil de gestion de campagne Push hello dans laquelle vous pouvez créer/modifier/activer/fin/analyse et obtenir les statistiques sur les campagnes Push notification et les fonctionnalités qui sont également accessibles via hello API couverture (et certains éléments de hello basse niveau d’API de Push).</span><span class="sxs-lookup"><span data-stu-id="60d8e-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="60d8e-109">Rappelez-vous que si vous utilisez hello API ou hello l’interface utilisateur, vous devez toointegrate Azure Mobile Engagement et portée dans votre application pour chaque plateforme avec hello SDK avant de pouvoir utiliser atteint des campagnes.</span><span class="sxs-lookup"><span data-stu-id="60d8e-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="60d8e-110">De nombreuses sections de hello **Mobile Engagement** interface utilisateur du portail contient hello **afficher l’aide** bouton.</span><span class="sxs-lookup"><span data-stu-id="60d8e-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="60d8e-111">Appuyez sur ce bouton tooget informations contextuelles supplémentaires sur une section.</span><span class="sxs-lookup"><span data-stu-id="60d8e-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="60d8e-112">Quatre types de notifications Push</span><span class="sxs-lookup"><span data-stu-id="60d8e-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="60d8e-113">Annonces - autoriser un toosend publicité messages toousers qui redirigent les emplacement tooanother à l’intérieur de votre application ou le toosend leur page Web de tooa ou à stocker en dehors de votre application.</span><span class="sxs-lookup"><span data-stu-id="60d8e-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="60d8e-114">Interroge - vous permettent d’informations de toogather aux utilisateurs finaux en posant des questions.</span><span class="sxs-lookup"><span data-stu-id="60d8e-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="60d8e-115">Push de données - autoriser toosend un fichier de données binaire ou en base 64.</span><span class="sxs-lookup"><span data-stu-id="60d8e-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="60d8e-116">Hello les informations contenues dans un push de données sont envoyées tooyour application toomodify expérience actuelle de vos utilisateurs dans votre application.</span><span class="sxs-lookup"><span data-stu-id="60d8e-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="60d8e-117">Votre application a besoin de données hello toobe tooprocess en mesure de push de données.</span><span class="sxs-lookup"><span data-stu-id="60d8e-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="60d8e-118">Informations relatives à la campagne</span><span class="sxs-lookup"><span data-stu-id="60d8e-118">Campaign Details</span></span>
<span data-ttu-id="60d8e-119">Vous pouvez modifier, cloner, supprimer ou activer les campagnes qui n’ont pas encore été activés en pointant sur leurs noms ou vous pouvez cliquer sur tooopen les.</span><span class="sxs-lookup"><span data-stu-id="60d8e-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="60d8e-120">Vous pouvez cloner des campagnes qui ont déjà été activées en pointant sur leurs noms, ou vous pouvez cliquer sur tooopen les.</span><span class="sxs-lookup"><span data-stu-id="60d8e-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="60d8e-121">Toutefois, vous ne pouvez pas modifier une campagne une fois celle-ci activée.</span><span class="sxs-lookup"><span data-stu-id="60d8e-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="60d8e-123">Commentaire Reach</span><span class="sxs-lookup"><span data-stu-id="60d8e-123">Reach Feedback</span></span>
<span data-ttu-id="60d8e-124">Cliquez sur **statistiques** détails de hello toosee d’une couverture campagne.</span><span class="sxs-lookup"><span data-stu-id="60d8e-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="60d8e-125">Hello **Simple** vue fournit une représentation visuelle sous forme de hello d’un graphique à barres que s’est-il passé après une campagne a été activée sur la colonne.</span><span class="sxs-lookup"><span data-stu-id="60d8e-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="60d8e-126">Hello **avancé** vue fournit des détails plus précis sur la campagne de push hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="60d8e-127">Ces informations ne sera pas disponibles si vous envoyez une campagne de test par exemple, un appareil de test tooa envoyés par émission de données.</span><span class="sxs-lookup"><span data-stu-id="60d8e-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="60d8e-128">Voici comment interpréter ces détails :</span><span class="sxs-lookup"><span data-stu-id="60d8e-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="60d8e-129">**Objet d’un push** -spécifie nombre hello des messages transmis toohello périphériques.</span><span class="sxs-lookup"><span data-stu-id="60d8e-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="60d8e-130">Ce nombre dépend visé hello que vous avez spécifié lors de la création de campagne de push hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="60d8e-131">Si vous ne spécifiez pas de n’importe quel public cible, puis cette opération push sera envoyée tooall hello inscrit périphériques.</span><span class="sxs-lookup"><span data-stu-id="60d8e-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="60d8e-132">Comme tous les autres services par émission de données, nous ne pas distribuer les notifications de hello directement les périphériques toohello mais de les transmettre à la place plateforme respectifs de toohello des Services de Notification Push (PNS - APNS/GCM/WNS) qui leur peuvent de remettre les notifications hello toohello périphériques.</span><span class="sxs-lookup"><span data-stu-id="60d8e-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="60d8e-133">**Remis** -spécifie nombre hello de messages qui sont correctement remis par l’appareil de toohello PNS hello et d’accusé de réception comme reçu par le Kit de développement logiciel de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="60d8e-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="60d8e-134">*Raisons pour lesquelles le nombre de messages remis est inférieur au nombre de notifications Push :*</span><span class="sxs-lookup"><span data-stu-id="60d8e-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="60d8e-135">Si l’utilisateur de hello a désinstallé l’application hello à partir de l’appareil de hello mais hello PNS ne connaît au moment de hello que nous envoyer hello push toohello PNS message de type hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="60d8e-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="60d8e-136">Si les appareils hello a application hello sans périphériques hello eux-mêmes étaient hors connexion pendant de longues périodes de temps, puis hello PNS échouera appareil de toohello toodeliver hello message.</span><span class="sxs-lookup"><span data-stu-id="60d8e-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="60d8e-137">Si message de type hello remis toohello appareil mais hello Kit de développement logiciel de Mobile Engagement dans l’application hello ne reconnaît pas le contenu du message de type hello hello, il dépose ensuite ce message.</span><span class="sxs-lookup"><span data-stu-id="60d8e-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="60d8e-138">Cela peut se produire si la personnalisation hello de notification hello dans l’application hello génère une exception qui nous catch dans le message de salutation SDK et drop hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="60d8e-139">Cela peut également se produire si l’application hello sur l’appareil de hello est à l’aide d’une version de hello Mobile Engagement Kit de développement logiciel qui n’est pas de version plus récente de hello toounderstand en mesure de message de type hello par émission de données envoyées à partir de la plateforme de hello, mais uniquement lorsque l’application hello a été mis à niveau après la notification de hello a été distribuée à partir de la plateforme de service hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="60d8e-140">Hello **avancé** onglet indique combien de messages ont été supprimés.</span><span class="sxs-lookup"><span data-stu-id="60d8e-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="60d8e-141">Sur les appareils iOS, messages parfois ne pas remis si l’appareil hello est sur batterie faible ou si l’application hello consomme une quantité importante de puissance lors du traitement des notifications à distance.</span><span class="sxs-lookup"><span data-stu-id="60d8e-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="60d8e-142">Il s’agit d’une limitation des appareils iOS de hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="60d8e-143">**Affiche** -spécifie nombre hello de messages qui sont correctement affichés toohello utilisateur d’applications sur l’appareil hello sous forme de hello d’une notification push/out-de-l’application de système dans le centre de notifications hello ou une notification dans l’application au sein de hello mobile application.</span><span class="sxs-lookup"><span data-stu-id="60d8e-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="60d8e-144">Hello **avancé** onglet vous indique combien ont été les notifications système et combien ont été les notifications dans l’application.</span><span class="sxs-lookup"><span data-stu-id="60d8e-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="60d8e-145">*Nombre de raisons affichées est inférieur au nombre de remis (toobe attente affiché)*</span><span class="sxs-lookup"><span data-stu-id="60d8e-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="60d8e-146">Si la campagne de notification hello avait une date de fin sur celui-ci, il est possible que la remise de notification de hello, mais lorsque le temps de hello fournie tooopen et l’afficher toohello utilisateur d’applications, elle a déjà expiré afin qu’il n’a jamais été affiche.</span><span class="sxs-lookup"><span data-stu-id="60d8e-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="60d8e-147">Si une notification de hello est une notification dans l’application notifications de hello s’affiche uniquement lorsque l’utilisateur d’application hello ouvre l’application hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="60d8e-148">Dans les cas où les utilisateurs d’application hello n’a pas ouvert application hello, hello SDK signalera que notification de hello a été remise mais pas encore affichée jusqu'à ce que l’application hello est ouvert.</span><span class="sxs-lookup"><span data-stu-id="60d8e-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="60d8e-149">Si la notification de hello est une notification dans l’application et configuré toobe indiqué sur un activité spécifique/écran puis également notification de hello est signalée comme remis mais n’ont ne pas encore été remis en tant qu’utilisateur de hello ouvre application hello sur un écran spécifique.</span><span class="sxs-lookup"><span data-stu-id="60d8e-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="60d8e-150">**Interactions de l’utilisateur** -Spécifie le nombre de hello de messages utilisateur application hello interagisse avec et inclut des messages hello sont actionnés ou quittés.</span><span class="sxs-lookup"><span data-stu-id="60d8e-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="60d8e-151">*utilisateur d’application Hello peut actionner une notification, que ce soit de hello suivant façons :*</span><span class="sxs-lookup"><span data-stu-id="60d8e-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="60d8e-152">Si hello notification est une notification système/out-de-l’application ou une notification dans l’application est envoyé en tant que notification uniquement utilisateur d’application hello clique ensuite sur la notification de hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="60d8e-153">Si les notifications hello sont une notification dans l’application avec un texte ou un affichage de web ou sondages hello puis utilisateur de l’application clique sur hello bouton d’Action de notification de hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="60d8e-154">Si une notification de hello est une notification dans l’application avec un affichage web puis hello application utilisateur clique sur une URL dans hello web [Android uniquement]</span><span class="sxs-lookup"><span data-stu-id="60d8e-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="60d8e-155">*utilisateur d’application Hello peut quitter une notification, que ce soit de hello suivant façons :*</span><span class="sxs-lookup"><span data-stu-id="60d8e-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="60d8e-156">Bouton hello fermer de notification de hello directement.</span><span class="sxs-lookup"><span data-stu-id="60d8e-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="60d8e-157">Le glissement absent ou suppression de notification de hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="60d8e-158">Notifications dans l’application avec le contenu de texte/web et les sondages sont généralement affichées toohello utilisateur d’applications dans un processus en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="60d8e-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="60d8e-159">Ils reçoivent une notification tout d’abord, et lorsqu’ils cliquent dessus, ils voient du contenu texte/web/interrogation hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="60d8e-160">utilisateur d’application Hello peut quitter une notification dans une de ces étapes et les détails de hello dans la vue avancée de hello capture cela.</span><span class="sxs-lookup"><span data-stu-id="60d8e-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="60d8e-161">**Déclenchée** -cela spécifie le nombre de hello de messages qui ont été explicitement déclenchée par l’utilisateur d’application hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="60d8e-162">Il s’agit de nombre plus intéressant de hello cela indique à combien d’utilisateurs application intéressés par le message de type hello poussé dans la notification de hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="60d8e-163">Sur iOS et les plateformes Windows, si utilisateur de hello a application hello ouvrir et la campagne de hello était une campagne « À tout moment », il est possible que les notifications d’application et dans l’application sont affichées sur hello même temps.</span><span class="sxs-lookup"><span data-stu-id="60d8e-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="60d8e-164">Cela peut entraîner un nombre affiché supérieur hello remis.</span><span class="sxs-lookup"><span data-stu-id="60d8e-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="60d8e-165">Si hello utilisateur interagit ou une notification actions hello, hello puis même nombre d’Interactions d’utilisateur/Actioned peut être supérieur à remis.</span><span class="sxs-lookup"><span data-stu-id="60d8e-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="60d8e-167">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="60d8e-167">See also</span></span>
* <span data-ttu-id="60d8e-168">[Concepts][Link 6]</span><span class="sxs-lookup"><span data-stu-id="60d8e-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="60d8e-169">[Service de guide de résolution des problèmes][Link 24]</span><span class="sxs-lookup"><span data-stu-id="60d8e-169">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

