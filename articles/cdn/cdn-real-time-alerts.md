---
title: "alertes en temps réel du CDN aaaAzure | Documents Microsoft"
description: "Alertes en temps réel dans Microsoft Azure CDN. Les alertes en temps réel fournissent des notifications sur les performances de hello de points de terminaison hello dans votre profil CDN."
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
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="c32c1-104">Alertes en temps réel dans Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="c32c1-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="c32c1-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c32c1-105">Overview</span></span>
<span data-ttu-id="c32c1-106">Ce document explique les alertes en temps réel dans Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="c32c1-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="c32c1-107">Cette fonctionnalité fournit des notifications en temps réel sur les performances de hello de points de terminaison hello dans votre profil CDN.</span><span class="sxs-lookup"><span data-stu-id="c32c1-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="c32c1-108">Vous pouvez configurer des alertes par courrier électronique ou HTTP en fonction des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c32c1-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="c32c1-109">Bande passante</span><span class="sxs-lookup"><span data-stu-id="c32c1-109">Bandwidth</span></span>
* <span data-ttu-id="c32c1-110">Codes d’état</span><span class="sxs-lookup"><span data-stu-id="c32c1-110">Status Codes</span></span>
* <span data-ttu-id="c32c1-111">États du cache</span><span class="sxs-lookup"><span data-stu-id="c32c1-111">Cache Statuses</span></span>
* <span data-ttu-id="c32c1-112">Connexions</span><span class="sxs-lookup"><span data-stu-id="c32c1-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="c32c1-113">Création d’une alerte en temps réel</span><span class="sxs-lookup"><span data-stu-id="c32c1-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="c32c1-114">Bonjour [Azure Portal](https://portal.azure.com), recherchez le profil CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="c32c1-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Panneau du profil CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="c32c1-116">À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.</span><span class="sxs-lookup"><span data-stu-id="c32c1-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="c32c1-118">portail de gestion CDN Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c32c1-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="c32c1-119">Placez votre curseur sur hello **Analytique** tab, puis pointez sur hello **les statistiques en temps réel** menu volant.</span><span class="sxs-lookup"><span data-stu-id="c32c1-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="c32c1-120">Cliquez sur **Alertes en temps réel**.</span><span class="sxs-lookup"><span data-stu-id="c32c1-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Portail de gestion CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="c32c1-122">liste de Hello des configurations d’alerte existantes (le cas échéant) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c32c1-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="c32c1-123">Cliquez sur hello **ajouter alertes** bouton.</span><span class="sxs-lookup"><span data-stu-id="c32c1-123">Click hello **Add Alert** button.</span></span>
   
    ![Bouton d’ajout d’alerte](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="c32c1-125">Un formulaire s’affiche pour créer une nouvelle alerte.</span><span class="sxs-lookup"><span data-stu-id="c32c1-125">A form for creating a new alert is displayed.</span></span>
   
    ![Formulaire de nouvelle alerte](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="c32c1-127">Si vous souhaitez que cette alerte toobe active lorsque vous cliquez sur **enregistrer**, vérifiez hello **alerte activée** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c32c1-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="c32c1-128">Entrez un nom descriptif pour votre alerte Bonjour **nom** champ.</span><span class="sxs-lookup"><span data-stu-id="c32c1-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="c32c1-129">Bonjour **le Type de média** liste déroulante, sélectionnez **LOB HTTP**.</span><span class="sxs-lookup"><span data-stu-id="c32c1-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Type de média avec HTTP Large Object sélectionné](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="c32c1-131">Vous devez sélectionner **LOB HTTP** comme hello **le Type de média**.</span><span class="sxs-lookup"><span data-stu-id="c32c1-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="c32c1-132">Hello autres choix n’est pas utilisés par **Azure CDN de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="c32c1-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="c32c1-133">Échec tooselect **LOB HTTP** entraîne votre alerte déclenchée toonever.</span><span class="sxs-lookup"><span data-stu-id="c32c1-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="c32c1-134">Créer un **Expression** toomonitor en sélectionnant un **métrique**, **opérateur**, et **déclencher la valeur**.</span><span class="sxs-lookup"><span data-stu-id="c32c1-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="c32c1-135">Pour **métrique**, sélectionnez le type hello de condition que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="c32c1-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="c32c1-136">**Mbits/s de bande passante** est la quantité de hello d’utilisation de la bande passante en mégabits par seconde.</span><span class="sxs-lookup"><span data-stu-id="c32c1-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="c32c1-137">**Nombre total de connexions** est nombre hello de tooour de connexions HTTP simultanée serveurs edge.</span><span class="sxs-lookup"><span data-stu-id="c32c1-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="c32c1-138">Pour les définitions de hello différents États de cache et les codes d’état, consultez [Codes d’état du Cache Azure CDN](https://msdn.microsoft.com/library/mt759237.aspx) et [Codes d’état HTTP Azure CDN](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="c32c1-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="c32c1-139">**Opérateur** est hello opérateur mathématique qui établit la relation hello entre les métriques de hello et valeur de déclenchement hello.</span><span class="sxs-lookup"><span data-stu-id="c32c1-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="c32c1-140">**Déclencher la valeur** est de valeur de seuil hello qui doit être remplie avant une notification est envoyée.</span><span class="sxs-lookup"><span data-stu-id="c32c1-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="c32c1-141">Bonjour exemple ci-dessous, expression hello, j’ai créé indique que j’aimerais toobe averti lorsque le nombre de hello des codes d’état 404 est supérieur à 25.</span><span class="sxs-lookup"><span data-stu-id="c32c1-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![Expression de l’exemple d’alerte en temps réel](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="c32c1-143">Pour **intervalle**, entrez la fréquence à laquelle vous souhaitez que l’expression hello évaluée.</span><span class="sxs-lookup"><span data-stu-id="c32c1-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="c32c1-144">Bonjour **notifier sur** liste déroulante, sélectionnez lorsque vous souhaitez toobe informé hello l’expression est vraie.</span><span class="sxs-lookup"><span data-stu-id="c32c1-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="c32c1-145">**Début de la condition** indique qu’une notification est envoyée lorsque hello spécifié de la première détection de condition.</span><span class="sxs-lookup"><span data-stu-id="c32c1-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="c32c1-146">**Fin de la condition** indique qu’une notification est envoyée lorsque hello spécifié la condition n’est plus détectée.</span><span class="sxs-lookup"><span data-stu-id="c32c1-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="c32c1-147">Cette notification ne peut être déclenchée une fois notre système de surveillance de réseau a détecté que hello spécifiée s’est produite lors d’une condition.</span><span class="sxs-lookup"><span data-stu-id="c32c1-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="c32c1-148">**Continue** indique qu’une notification sera envoyée chaque fois que hello système de surveillance réseau détecte hello spécifié condition.</span><span class="sxs-lookup"><span data-stu-id="c32c1-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="c32c1-149">Gardez à l’esprit ce réseau hello surveillance système sera uniquement cocher qu’une seule fois par intervalle hello pour les conditions spécifiées.</span><span class="sxs-lookup"><span data-stu-id="c32c1-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="c32c1-150">**Début de la condition et de fin** indique qu’une notification sera envoyée hello la première fois que hello la condition spécifiée est détecté et qu’une seule fois à nouveau lorsque la condition de hello n’est plus détectée.</span><span class="sxs-lookup"><span data-stu-id="c32c1-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="c32c1-151">Si vous voulez tooreceive notifications par courrier électronique, activez hello **notification par courrier électronique** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c32c1-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![Formulaire de notification par courrier électronique](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="c32c1-153">Bonjour **à** , entrez l’adresse de messagerie hello où vous souhaitez que les notifications envoyées.</span><span class="sxs-lookup"><span data-stu-id="c32c1-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="c32c1-154">Pour **sujet** et **corps**, vous pouvez laisser la valeur par défaut de hello, ou vous pouvez personnaliser le message de type hello à l’aide de hello **mots clés disponibles** liste toodynamically insérer des données d’alerte lorsque message de type Hello est envoyé.</span><span class="sxs-lookup"><span data-stu-id="c32c1-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c32c1-155">Vous pouvez tester la notification par courrier électronique de hello en cliquant sur hello **une Notification de Test** bouton, mais uniquement après l’enregistrement de configuration d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="c32c1-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="c32c1-156">Si vous souhaitez toobe notifications validée de serveur web de tooa, vérifiez hello **notifier par HTTP Post** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c32c1-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![Formulaire de notification par HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="c32c1-158">Bonjour **Url** , entrez l’URL hello où que vous voulez message de type hello HTTP validée.</span><span class="sxs-lookup"><span data-stu-id="c32c1-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="c32c1-159">Bonjour **en-têtes** zone de texte, entrez toobe d’en-têtes hello HTTP envoyé dans demande de hello.</span><span class="sxs-lookup"><span data-stu-id="c32c1-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="c32c1-160">Pour **corps** vous pouvez personnaliser le message de type hello à l’aide de hello **mots clés disponibles** liste toodynamically insérer des données d’alerte lorsque le message de type hello est envoyé.</span><span class="sxs-lookup"><span data-stu-id="c32c1-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="c32c1-161">**En-têtes** et **corps** par défaut toohello similaire de charge utile XML tooan exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c32c1-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="c32c1-162">Vous pouvez tester hello notification de requête HTTP Post en cliquant sur hello **une Notification de Test** bouton, mais uniquement après l’enregistrement de configuration d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="c32c1-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="c32c1-163">Cliquez sur hello **enregistrer** bouton toosave votre configuration d’alerte.</span><span class="sxs-lookup"><span data-stu-id="c32c1-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="c32c1-164">Si vous avez coché la case **Alerte activée** à l’étape 5, votre alerte est maintenant active.</span><span class="sxs-lookup"><span data-stu-id="c32c1-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c32c1-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c32c1-165">Next Steps</span></span>
* <span data-ttu-id="c32c1-166">Analyser des [statistiques en temps réel dans Azure CDN](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="c32c1-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="c32c1-167">Aller plus loin en vous familiarisant avec les [rapports HTTP avancés](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="c32c1-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="c32c1-168">Analysez les [modes d’utilisation](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="c32c1-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

