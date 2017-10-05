---
title: Interface utilisateur d'Azure Mobile Engagement - Reach
description: "Découvrez comment atteindre les utilisateurs de votre application avec des notifications Push grâce à Azure Mobile Engagement"
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
ms.openlocfilehash: ce30456e41ff1a2f4824bcb64246ee115fdd1ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reach-out-to-the-users-of-your-application-with-push-notifications"></a><span data-ttu-id="161c2-103">Comment atteindre les utilisateurs de votre application avec des notifications Push</span><span class="sxs-lookup"><span data-stu-id="161c2-103">How to reach out to the users of your application with push notifications</span></span>
<span data-ttu-id="161c2-104">Cet article décrit l’onglet **REACH** du portail **Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="161c2-104">This article describes the **REACH** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="161c2-105">Le portail **Mobile Engagement** sert à surveiller et à gérer vos applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="161c2-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="161c2-106">Notez que pour utiliser le portail, vous devez tout d’abord créer un compte **Azure Mobile Engagement** .</span><span class="sxs-lookup"><span data-stu-id="161c2-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="161c2-107">Pour plus d'informations, consultez [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="161c2-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="161c2-108">La section Reach de l'interface utilisateur est l'outil de gestion des campagnes Push qui vous permet de créer, modifier, activer, terminer ou surveiller et obtenir des statistiques relatives aux campagnes de notifications Push et des fonctionnalités. Vous pouvez accéder à celles-ci via l'API Reach (ainsi que certains éléments de l'API Push de bas niveau).</span><span class="sxs-lookup"><span data-stu-id="161c2-108">The Reach section of the UI is the Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via the Reach API (and some elements of the low level Push API).</span></span> <span data-ttu-id="161c2-109">Que vous utilisiez ces API ou l'interface utilisateur, il vous faudra intégrer Azure Mobile Engagement et Reach à votre application pour chaque plateforme à l'aide du Kit de développement logiciel (SDK) avant de pouvoir utiliser les campagnes Reach.</span><span class="sxs-lookup"><span data-stu-id="161c2-109">Remember that whether you are using the APIs or the UI, you will need to integrate both Azure Mobile Engagement and Reach into your application for each platform with the SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="161c2-110">De nombreuses sections de l’interface utilisateur du portail **Mobile Engagement** contiennent un bouton **AFFICHER L’AIDE**.</span><span class="sxs-lookup"><span data-stu-id="161c2-110">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="161c2-111">Appuyez sur ce bouton pour obtenir des informations contextuelles supplémentaires sur une section.</span><span class="sxs-lookup"><span data-stu-id="161c2-111">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="161c2-112">Quatre types de notifications Push</span><span class="sxs-lookup"><span data-stu-id="161c2-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="161c2-113">Annonces : elles vous permettent d'envoyer aux utilisateurs des messages publicitaires qui les redirigent vers un autre emplacement dans votre application ou les envoient vers une page Web ou un Store en dehors de votre application.</span><span class="sxs-lookup"><span data-stu-id="161c2-113">Announcements - allow you to send advertising messages to users that redirect them to another location inside your app or to send them to a webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="161c2-114">Sondages : ces notifications vous permettent de regrouper des informations sur les utilisateurs finaux en leur posant des questions.</span><span class="sxs-lookup"><span data-stu-id="161c2-114">Polls - allow you to gather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="161c2-115">Push de données : ces notifications vous permettent d'envoyer un fichier de données binaire ou base 64.</span><span class="sxs-lookup"><span data-stu-id="161c2-115">Data Pushes - allow you to send a binary or base64 data file.</span></span> <span data-ttu-id="161c2-116">Les informations contenues dans un Push de données sont envoyées à votre application pour modifier l'expérience actuelle des utilisateurs de votre application.</span><span class="sxs-lookup"><span data-stu-id="161c2-116">The information contained in a data push is sent to your application to modify your users' current experience in your app.</span></span> <span data-ttu-id="161c2-117">Votre application doit être en mesure de traiter les données dans un Push de données.</span><span class="sxs-lookup"><span data-stu-id="161c2-117">Your application needs to be able to process the data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="161c2-118">Informations relatives à la campagne</span><span class="sxs-lookup"><span data-stu-id="161c2-118">Campaign Details</span></span>
<span data-ttu-id="161c2-119">Vous pouvez modifier, cloner, supprimer ou activer les campagnes qui n'ont pas encore été activées en plaçant le curseur sur leurs noms ou en cliquant pour les ouvrir.</span><span class="sxs-lookup"><span data-stu-id="161c2-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="161c2-120">Vous pouvez cloner les campagnes qui ont déjà été activées en plaçant le curseur sur leurs noms ou en cliquant pour les ouvrir.</span><span class="sxs-lookup"><span data-stu-id="161c2-120">You can clone campaigns that have already been activated by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="161c2-121">Toutefois, vous ne pouvez pas modifier une campagne une fois celle-ci activée.</span><span class="sxs-lookup"><span data-stu-id="161c2-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="161c2-123">Commentaire Reach</span><span class="sxs-lookup"><span data-stu-id="161c2-123">Reach Feedback</span></span>
<span data-ttu-id="161c2-124">Cliquez sur **Statistiques** pour afficher les détails d'une campagne Reach.</span><span class="sxs-lookup"><span data-stu-id="161c2-124">Click on **Statistics** to see the details of a Reach campaign.</span></span> <span data-ttu-id="161c2-125">L'affichage **Simple** fournit une représentation visuelle sous la forme d'un graphique à barres en colonnes sur ce qui s'est passé après l'activation d'une campagne.</span><span class="sxs-lookup"><span data-stu-id="161c2-125">The **Simple** view provides a visual representation in the form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="161c2-126">L'affichage **Avancé** fournit des détails plus précis sur la campagne Push.</span><span class="sxs-lookup"><span data-stu-id="161c2-126">The **Advanced** view provides more granular details about the push campaign.</span></span> <span data-ttu-id="161c2-127">Ces détails ne sont pas disponibles si vous envoyez une campagne de test, c'est-à-dire une notification Push envoyée à un appareil de test.</span><span class="sxs-lookup"><span data-stu-id="161c2-127">These details will not be available if you are sending a test campaign i.e. a push sent to a test device.</span></span> <span data-ttu-id="161c2-128">Voici comment interpréter ces détails :</span><span class="sxs-lookup"><span data-stu-id="161c2-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="161c2-129">**Push** : indique le nombre de messages envoyés aux appareils.</span><span class="sxs-lookup"><span data-stu-id="161c2-129">**Pushed** - This specifies the number of messages pushed to the devices.</span></span> <span data-ttu-id="161c2-130">Ce nombre dépend du public cible spécifié lors de la création de la campagne Push.</span><span class="sxs-lookup"><span data-stu-id="161c2-130">This number will depend on the target audience you specified while creating the push campaign.</span></span> <span data-ttu-id="161c2-131">Si vous ne spécifiez aucun public cible, cette notification Push sera envoyée à tous les appareils inscrits.</span><span class="sxs-lookup"><span data-stu-id="161c2-131">If you do not specify any target audience, then this push will be sent out to all the registered devices.</span></span> <span data-ttu-id="161c2-132">Comme tous les autres services Push, nous n'envoyons pas les notifications directement aux appareils. Nous les envoyons aux services de notification Push (PNS - APNS/GCM/WNS) spécifiques à la plateforme respective afin qu'ils transfèrent les notifications aux appareils.</span><span class="sxs-lookup"><span data-stu-id="161c2-132">Like all other push services, we do not push the notifications directly to the devices but instead push them to the respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver the notifications to the devices.</span></span> 
2. <span data-ttu-id="161c2-133">**Remis** : indique le nombre de messages remis avec succès par le PNS à l'appareil et reconnus comme reçus par le Kit de développement logiciel (SDK) Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="161c2-133">**Delivered** - This specifies the number of messages which are successfully delivered by the PNS to the device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="161c2-134">*Raisons pour lesquelles le nombre de messages remis est inférieur au nombre de notifications Push :*</span><span class="sxs-lookup"><span data-stu-id="161c2-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="161c2-135">Si l'utilisateur a désinstallé l'application de l'appareil mais que le service PNS ne le sait pas au moment où nous envoyons la notification Push au service PNS, alors le message est supprimé.</span><span class="sxs-lookup"><span data-stu-id="161c2-135">If the user has uninstalled the app from the device but the PNS doesn't know about it at the time we send the push to the PNS then the message will be dropped.</span></span>
   2. <span data-ttu-id="161c2-136">Si l'appareil dispose de l'application mais que les appareils eux-mêmes étaient hors ligne pendant de longues périodes, alors la remise du message à l'appareil par le service PNS échoue.</span><span class="sxs-lookup"><span data-stu-id="161c2-136">If the device has the app but the devices themselves were offline for long periods of time, then the PNS will fail to deliver the message to the device.</span></span> 
   3. <span data-ttu-id="161c2-137">Si le message est remis à l'appareil mais que le Kit de développement logiciel (SDK) Mobile Engagement dans l'application ne reconnaît pas le contenu du message, alors le message est supprimé.</span><span class="sxs-lookup"><span data-stu-id="161c2-137">If the message does get delivered to the device but the Mobile Engagement SDK in the app doesn’t recognize the content of the message, then it drops that message.</span></span> <span data-ttu-id="161c2-138">Cela peut se produire si la personnalisation de la notification dans l'application génère une exception que nous relevons dans le Kit de développement logiciel (SDK) et que nous supprimons le message.</span><span class="sxs-lookup"><span data-stu-id="161c2-138">This could happen if the customization of the notification in the app generates an exception which we catch in the SDK and drop the message.</span></span> <span data-ttu-id="161c2-139">Cela peut également se produire si l'application sur l'appareil utilise une version du Kit de développement logiciel (SDK) Engagement Mobile qui n'est pas en mesure de comprendre la version la plus récente du message Push envoyé à partir de la plateforme. Cela ne s'applique que lorsque l'application a été mise à niveau après la distribution de la notification par la plateforme de services.</span><span class="sxs-lookup"><span data-stu-id="161c2-139">This could also occur if the app on the device is using a version of the Mobile Engagement SDK which is not able to understand the newer version of the push message sent from the platform but this is only when the app was upgraded after the notification was dispatched from the service platform.</span></span> <span data-ttu-id="161c2-140">L’onglet **Avancé** indique le nombre de messages supprimés.</span><span class="sxs-lookup"><span data-stu-id="161c2-140">The **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="161c2-141">Sur les appareils iOS, la remise des messages peut parfois échouer si la batterie de l’appareil est faible ou que l’application consomme trop d’énergie pendant le traitement des notifications distantes.</span><span class="sxs-lookup"><span data-stu-id="161c2-141">On iOS devices, messages sometimes do not get delivered if either the device is on low battery or if the app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="161c2-142">Il s’agit d’une limitation des appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="161c2-142">This is a limitation of the iOS devices.</span></span>   
3. <span data-ttu-id="161c2-143">**Affichés** : indique le nombre de messages qui sont affichés correctement à l’utilisateur de l’application sur l’appareil sous la forme d’une notification système Push/hors application dans le centre de notification ou une notification dans l’application au sein de l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="161c2-143">**Displayed** - This specifies the number of messages which are successfully shown to the app user on the device in the form of a system push/out-of-app notification in the notification center or an in-app notification within the mobile app.</span></span>  <span data-ttu-id="161c2-144">L’onglet **Avancé** indique le nombre de notifications système et le nombre de notifications dans l’application.</span><span class="sxs-lookup"><span data-stu-id="161c2-144">The **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="161c2-145">*Raisons pour lesquelles le nombre d’éléments affichés est inférieur au nombre d’éléments remis (en attente d’être affichés)*</span><span class="sxs-lookup"><span data-stu-id="161c2-145">*Reasons for Displayed count being less than Delivered count (waiting to be displayed)*</span></span>
   
   1. <span data-ttu-id="161c2-146">Si la campagne de notification avait une date de fin, alors il est possible que la notification ait été remise, mais au moment de l’ouvrir et de l’afficher sur l’application de l’utilisateur, elle avait déjà expiré et donc ne s’est jamais affichée.</span><span class="sxs-lookup"><span data-stu-id="161c2-146">If the notification campaign had an end date on it then it is possible that the notification was delivered but when the time came to open and display it to the app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="161c2-147">Si la notification est une notification dans l’application, elle est alors uniquement affichée lorsque l’utilisateur de l’application ouvre celle-ci.</span><span class="sxs-lookup"><span data-stu-id="161c2-147">If the notification is an in-app notification then the notification is only displayed when the app user opens the app.</span></span> <span data-ttu-id="161c2-148">Dans le cas où l’utilisateur n’aurait pas ouvert l’application, le kit de développement logiciel (SDK) signale que la notification a été remise mais pas encore affichée puisque l’application n’a pas été ouverte.</span><span class="sxs-lookup"><span data-stu-id="161c2-148">In cases where the app user hasn't opened the app, the SDK will report that the notification was delivered but not yet displayed until the app is opened.</span></span> 
   3. <span data-ttu-id="161c2-149">S’il s’agit d’une notification dans l’application et qu’elle est configurée pour s’afficher sur un écran spécifique ou lors d’une activité spécifique, alors elle sera également signalée comme remise mais ne sera véritablement remise qu’après l’ouverture par l’utilisateur de l’application sur un écran spécifique.</span><span class="sxs-lookup"><span data-stu-id="161c2-149">If the notification is an in-app notification and configured to be shown on a specific activity/screen then also the notification will be reported as delivered but not yet delivered until the user opens the app on a specific screen.</span></span> 
4. <span data-ttu-id="161c2-150">**Interactions utilisateur** : indique le nombre de messages avec lesquels l’utilisateur de l’application a eu une interaction et inclut les messages qui font l’objet d’une action ou qui sont abandonnés.</span><span class="sxs-lookup"><span data-stu-id="161c2-150">**User Interactions** - This specifies the number of messages which the app user has interacted with and will include the messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="161c2-151">*L'utilisateur de l'application peut agir sur une notification de l'une des manières suivantes :*</span><span class="sxs-lookup"><span data-stu-id="161c2-151">*The app user can action a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="161c2-152">Si la notification est une notification système/hors application ou une notification dans l'application envoyée comme notification uniquement, alors l'utilisateur de l'application clique sur la notification.</span><span class="sxs-lookup"><span data-stu-id="161c2-152">If the notification is a system/out-of-app notification or an in-app notification sent as notification-only then the app user clicks on the notification.</span></span>
     2. <span data-ttu-id="161c2-153">Si la notification est une notification dans l'application avec un texte ou un affichage web ou des sondages, alors l'utilisateur de l'application clique sur le bouton Action dans la notification.</span><span class="sxs-lookup"><span data-stu-id="161c2-153">If the notification is an in-app notification with a text or web-view or polls then the app user clicks on the Action button in the notification.</span></span>
     3. <span data-ttu-id="161c2-154">Si la notification est une notification dans l'application avec un affichage web, alors l'utilisateur de l'application clique sur une URL dans l'affichage web [Android uniquement]</span><span class="sxs-lookup"><span data-stu-id="161c2-154">If the notification is an in-app notification with a web-view then the app user clicks on a URL in the web view [Android Only]</span></span>
   * <span data-ttu-id="161c2-155">*L'utilisateur de l'application peut quitter une notification de l'une des manières suivantes :*</span><span class="sxs-lookup"><span data-stu-id="161c2-155">*The app user can exit a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="161c2-156">En cliquant sur le bouton Fermer directement dans la notification.</span><span class="sxs-lookup"><span data-stu-id="161c2-156">Clicking the close button on the notification directly.</span></span> 
     2. <span data-ttu-id="161c2-157">En balayant ou en supprimant la notification.</span><span class="sxs-lookup"><span data-stu-id="161c2-157">Swiping away or deleting the notification.</span></span> 
     3. <span data-ttu-id="161c2-158">Les notifications dans l'application avec du texte/contenu web et les sondages sont généralement affichées à l'utilisateur de l'application dans un processus en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="161c2-158">In-app notifications with text/web content and polls are typically displayed to the app user in a two-step process.</span></span> <span data-ttu-id="161c2-159">L'utilisateur reçoit tout d'abord une notification et lorsqu'il clique dessus, le contenu du texte/web/sondage s'affiche.</span><span class="sxs-lookup"><span data-stu-id="161c2-159">They see a notification first and when they click on it, they see the subsequent text/web/poll content.</span></span> <span data-ttu-id="161c2-160">L'utilisateur de l'application peut quitter une notification dans n'importe laquelle de ces étapes et les détails dans la vue Avancée indiquent cela.</span><span class="sxs-lookup"><span data-stu-id="161c2-160">The app user can exit a notification in either of these steps and the details in the Advanced view captures this.</span></span> 
5. <span data-ttu-id="161c2-161">**Actionnés** : indique le nombre de messages qui ont explicitement fait l’objet d’une action par l’utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="161c2-161">**Actioned** - This specifies the number of messages which were explicitly actioned by the app user.</span></span> <span data-ttu-id="161c2-162">Il s'agit du nombre le plus intéressant car il indique le nombre d'utilisateurs de l'application intéressés par le message transmis dans la notification.</span><span class="sxs-lookup"><span data-stu-id="161c2-162">This is the most interesting number as this tells how many app users were interested by the message you pushed out in the notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="161c2-163">Sur les plateformes iOS et Windows, si l'utilisateur dispose de l'application ouverte et que la campagne était du type « À tout moment », il est possible que les notifications hors application et dans l'application s'affichent en même temps.</span><span class="sxs-lookup"><span data-stu-id="161c2-163">On iOS & Windows platforms, if the user has the app open and the campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at the same time.</span></span> <span data-ttu-id="161c2-164">Cela peut entraîner un nombre plus élevé pour le paramètre Affichés que pour le paramètre Remis.</span><span class="sxs-lookup"><span data-stu-id="161c2-164">This may cause a Displayed count higher than the Delivered.</span></span> <span data-ttu-id="161c2-165">Si l'utilisateur interagit avec la notification ou qu'il exécute une action dessus, alors même le nombre Interactions utilisateur/Actionnés peut être supérieur au nombre Remis.</span><span class="sxs-lookup"><span data-stu-id="161c2-165">If the user interacts or actions the notification, then even the User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="161c2-167">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="161c2-167">See also</span></span>
* <span data-ttu-id="161c2-168">[Concepts][Link 6]</span><span class="sxs-lookup"><span data-stu-id="161c2-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="161c2-169">[Service de guide de résolution des problèmes][Link 24]</span><span class="sxs-lookup"><span data-stu-id="161c2-169">[Troubleshooting Guide Service][Link 24]</span></span>

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

