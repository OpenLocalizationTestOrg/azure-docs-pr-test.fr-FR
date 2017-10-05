---
title: "Alertes en temps réel Azure CDN | Microsoft Docs"
description: "Alertes en temps réel dans Microsoft Azure CDN. Les alertes en temps réel fournissent des notifications sur les performances des points de terminaison dans votre profil CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6e66eb076ac7220823a848b5047f147d4101cd55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="f1fd8-104">Alertes en temps réel dans Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f1fd8-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="f1fd8-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f1fd8-105">Overview</span></span>
<span data-ttu-id="f1fd8-106">Ce document explique les alertes en temps réel dans Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="f1fd8-107">Cette fonctionnalité fournit des notifications en temps réel sur les performances des points de terminaison dans votre profil CDN.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="f1fd8-108">Vous pouvez configurer des alertes par courrier électronique ou HTTP en fonction des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f1fd8-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="f1fd8-109">Bande passante</span><span class="sxs-lookup"><span data-stu-id="f1fd8-109">Bandwidth</span></span>
* <span data-ttu-id="f1fd8-110">Codes d’état</span><span class="sxs-lookup"><span data-stu-id="f1fd8-110">Status Codes</span></span>
* <span data-ttu-id="f1fd8-111">États du cache</span><span class="sxs-lookup"><span data-stu-id="f1fd8-111">Cache Statuses</span></span>
* <span data-ttu-id="f1fd8-112">Connexions</span><span class="sxs-lookup"><span data-stu-id="f1fd8-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="f1fd8-113">Création d’une alerte en temps réel</span><span class="sxs-lookup"><span data-stu-id="f1fd8-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="f1fd8-114">Dans le [portail Azure](https://portal.azure.com), accédez à votre profil CDN.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Panneau du profil CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="f1fd8-116">Dans le panneau de profil CDN, cliquez sur le bouton **Gérer** .</span><span class="sxs-lookup"><span data-stu-id="f1fd8-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="f1fd8-118">Le portail de gestion CDN s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="f1fd8-119">Pointez sur l’onglet **Analyse**, puis sur le menu volant **Statistiques en temps réel**.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="f1fd8-120">Cliquez sur **Alertes en temps réel**.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portail de gestion CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="f1fd8-122">La liste des configurations d’alerte existantes (le cas échéant) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="f1fd8-123">Cliquez sur le bouton **Ajouter une alerte** .</span><span class="sxs-lookup"><span data-stu-id="f1fd8-123">Click the **Add Alert** button.</span></span>
   
    ![Bouton d’ajout d’alerte](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="f1fd8-125">Un formulaire s’affiche pour créer une nouvelle alerte.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-125">A form for creating a new alert is displayed.</span></span>
   
    ![Formulaire de nouvelle alerte](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="f1fd8-127">Si vous souhaitez que cette alerte soit active lorsque vous cliquez sur **Enregistrer**, cochez la case **Alerte activée**.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="f1fd8-128">Entrez un nom descriptif pour votre alerte dans le champ **Nom** .</span><span class="sxs-lookup"><span data-stu-id="f1fd8-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="f1fd8-129">Dans la liste déroulante **Type de média**, sélectionnez **HTTP Large Object**.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Type de média avec HTTP Large Object sélectionné](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="f1fd8-131">Vous devez sélectionner **HTTP Large Object** comme **Type de média**.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="f1fd8-132">Les autres options ne sont pas utilisées par **Azure CDN de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="f1fd8-133">Si vous ne sélectionnez pas **HTTP Large Object** , votre alerte ne se déclenchera jamais.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="f1fd8-134">Créez une **Expression** à surveiller en sélectionnant **Mesure**, **Opérateur** et **Valeur de déclenchement**.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="f1fd8-135">Pour **Mesure**, sélectionnez le type de condition que vous souhaitez surveiller.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="f1fd8-136">**Bandwidth Mbps (Mbits/s de bande passante)** est la quantité de bande passante en mégabits par seconde.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="f1fd8-137">**Nombre total de connexions** est le nombre de connexions HTTP simultanées à nos serveurs Edge.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="f1fd8-138">Pour obtenir les définitions des différents états de cache et les codes d’état, voir [Azure CDN Cache Status Codes (Codes d’état du cache Azure CDN)](https://msdn.microsoft.com/library/mt759237.aspx) et [Azure CDN HTTP Status Codes (Codes d’état HTTP d’Azure CDN)](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="f1fd8-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="f1fd8-139">**Opérateur** est l’opérateur mathématique qui établit la relation entre la mesure et la valeur du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="f1fd8-140">**Valeur de déclenchement** est la valeur de seuil qui doit être atteinte avant l’envoi d’une notification.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="f1fd8-141">Dans l’exemple ci-dessous, l’expression que j’ai créée indique que je souhaite être averti lorsque le nombre de codes d’état 404 est supérieur à 25.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![Expression de l’exemple d’alerte en temps réel](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="f1fd8-143">Pour **Intervalle**, entrez la fréquence à laquelle vous souhaitez que l’expression soit évaluée.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="f1fd8-144">Dans la liste déroulante **Notify on (Notifier sur)** , sélectionnez quand vous souhaitez être averti lorsque l’expression est vraie.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="f1fd8-145">**Condition Start (Début de la condition)** indique qu’une notification sera envoyée lors de la première détection de la condition spécifiée.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="f1fd8-146">**Condition End (Fin de la condition)** indique qu’une notification sera envoyée lorsque la condition spécifiée ne sera plus détectée.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="f1fd8-147">Cette notification ne peut être déclenchée qu’une fois que notre système de surveillance du réseau a détecté que la condition spécifiée s’est produite.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="f1fd8-148">**Continu** indique qu’une notification sera envoyée chaque fois que le système de surveillance du réseau détecte la condition spécifiée.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="f1fd8-149">N’oubliez pas que le système de surveillance du réseau ne recherche la condition spécifiée qu’une seule fois par intervalle.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="f1fd8-150">**Condition Start and End (Début et fin de la condition)** indique qu’une notification sera envoyée lors de la première détection de la condition spécifiée, puis à nouveau lorsque la condition ne sera plus détectée.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="f1fd8-151">Si vous souhaitez recevoir des notifications par courrier électronique, cochez la case **Notify by Email (Notifier par courrier électronique)** .</span><span class="sxs-lookup"><span data-stu-id="f1fd8-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![Formulaire de notification par courrier électronique](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="f1fd8-153">Dans le champ **À** , entrez l’adresse de messagerie à laquelle vous voulez que les notifications soient envoyées.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="f1fd8-154">Pour **Objet** et **Corps**, vous pouvez laisser la valeur par défaut ou personnaliser le message à l’aide de la liste **Available keywords (Mots clés disponibles)** pour insérer dynamiquement les données d’alerte lors de l’envoi du message.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="f1fd8-155">Vous pouvez tester la notification par courrier électronique en cliquant sur le bouton **Tester la notification** , mais uniquement après l’enregistrement de la configuration de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="f1fd8-156">Si vous souhaitez que les notifications soient publiées sur un serveur web, cochez la case **Notify par HTTP Post (Notifier par HTTP Post)** .</span><span class="sxs-lookup"><span data-stu-id="f1fd8-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![Formulaire de notification par HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="f1fd8-158">Dans le champ **Url** , entrez l’adresse URL à laquelle vous souhaitez que le message HTTP soit publié.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="f1fd8-159">Dans la zone de texte **En-têtes** , entrez les en-têtes HTTP à envoyer dans la demande.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="f1fd8-160">Pour **Corps**, vous pouvez personnaliser le message à l’aide de la liste **Available keywords (Mots clés disponibles)** pour insérer dynamiquement les données d’alerte lors de l’envoi du message.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="f1fd8-161">La valeur par défaut des zones de texte **En-têtes** et **Corps** est une charge XML semblable à celle de l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="f1fd8-162">Vous pouvez tester la notification HTTP Post en cliquant sur le bouton **Tester la notification** , mais uniquement après l’enregistrement de la configuration de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="f1fd8-163">Cliquez sur le bouton **Enregistrer** pour enregistrer votre configuration d’alerte.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="f1fd8-164">Si vous avez coché la case **Alerte activée** à l’étape 5, votre alerte est maintenant active.</span><span class="sxs-lookup"><span data-stu-id="f1fd8-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1fd8-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1fd8-165">Next Steps</span></span>
* <span data-ttu-id="f1fd8-166">Analyser des [statistiques en temps réel dans Azure CDN](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="f1fd8-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="f1fd8-167">Aller plus loin en vous familiarisant avec les [rapports HTTP avancés](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="f1fd8-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="f1fd8-168">Analysez les [modes d’utilisation](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="f1fd8-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

