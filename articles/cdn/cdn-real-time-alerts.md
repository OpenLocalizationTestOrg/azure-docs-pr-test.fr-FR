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
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a>Alertes en temps réel dans Microsoft Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Vue d'ensemble
Ce document explique les alertes en temps réel dans Microsoft Azure CDN. Cette fonctionnalité fournit des notifications en temps réel sur les performances de hello de points de terminaison hello dans votre profil CDN.  Vous pouvez configurer des alertes par courrier électronique ou HTTP en fonction des éléments suivants :

* Bande passante
* Codes d’état
* États du cache
* Connexions

## <a name="creating-a-real-time-alert"></a>Création d’une alerte en temps réel
1. Bonjour [Azure Portal](https://portal.azure.com), recherchez le profil CDN tooyour.
   
    ![Panneau du profil CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    portail de gestion CDN Hello s’ouvre.
3. Placez votre curseur sur hello **Analytique** tab, puis pointez sur hello **les statistiques en temps réel** menu volant.  Cliquez sur **Alertes en temps réel**.
   
    ![Portail de gestion CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    liste de Hello des configurations d’alerte existantes (le cas échéant) s’affiche.
4. Cliquez sur hello **ajouter alertes** bouton.
   
    ![Bouton d’ajout d’alerte](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    Un formulaire s’affiche pour créer une nouvelle alerte.
   
    ![Formulaire de nouvelle alerte](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. Si vous souhaitez que cette alerte toobe active lorsque vous cliquez sur **enregistrer**, vérifiez hello **alerte activée** case à cocher.
6. Entrez un nom descriptif pour votre alerte Bonjour **nom** champ.
7. Bonjour **le Type de média** liste déroulante, sélectionnez **LOB HTTP**.
   
    ![Type de média avec HTTP Large Object sélectionné](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > Vous devez sélectionner **LOB HTTP** comme hello **le Type de média**.  Hello autres choix n’est pas utilisés par **Azure CDN de Verizon**.  Échec tooselect **LOB HTTP** entraîne votre alerte déclenchée toonever.
   > 
   > 
8. Créer un **Expression** toomonitor en sélectionnant un **métrique**, **opérateur**, et **déclencher la valeur**.
   
   * Pour **métrique**, sélectionnez le type hello de condition que vous souhaitez analyser.  **Mbits/s de bande passante** est la quantité de hello d’utilisation de la bande passante en mégabits par seconde.  **Nombre total de connexions** est nombre hello de tooour de connexions HTTP simultanée serveurs edge.  Pour les définitions de hello différents États de cache et les codes d’état, consultez [Codes d’état du Cache Azure CDN](https://msdn.microsoft.com/library/mt759237.aspx) et [Codes d’état HTTP Azure CDN](https://msdn.microsoft.com/library/mt759238.aspx)
   * **Opérateur** est hello opérateur mathématique qui établit la relation hello entre les métriques de hello et valeur de déclenchement hello.
   * **Déclencher la valeur** est de valeur de seuil hello qui doit être remplie avant une notification est envoyée.
     
     Bonjour exemple ci-dessous, expression hello, j’ai créé indique que j’aimerais toobe averti lorsque le nombre de hello des codes d’état 404 est supérieur à 25.
     
     ![Expression de l’exemple d’alerte en temps réel](./media/cdn-real-time-alerts/cdn-expression.png)
9. Pour **intervalle**, entrez la fréquence à laquelle vous souhaitez que l’expression hello évaluée.
10. Bonjour **notifier sur** liste déroulante, sélectionnez lorsque vous souhaitez toobe informé hello l’expression est vraie.
    
    * **Début de la condition** indique qu’une notification est envoyée lorsque hello spécifié de la première détection de condition.
    * **Fin de la condition** indique qu’une notification est envoyée lorsque hello spécifié la condition n’est plus détectée. Cette notification ne peut être déclenchée une fois notre système de surveillance de réseau a détecté que hello spécifiée s’est produite lors d’une condition.
    * **Continue** indique qu’une notification sera envoyée chaque fois que hello système de surveillance réseau détecte hello spécifié condition. Gardez à l’esprit ce réseau hello surveillance système sera uniquement cocher qu’une seule fois par intervalle hello pour les conditions spécifiées.
    * **Début de la condition et de fin** indique qu’une notification sera envoyée hello la première fois que hello la condition spécifiée est détecté et qu’une seule fois à nouveau lorsque la condition de hello n’est plus détectée.
11. Si vous voulez tooreceive notifications par courrier électronique, activez hello **notification par courrier électronique** case à cocher.  
    
    ![Formulaire de notification par courrier électronique](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    Bonjour **à** , entrez l’adresse de messagerie hello où vous souhaitez que les notifications envoyées. Pour **sujet** et **corps**, vous pouvez laisser la valeur par défaut de hello, ou vous pouvez personnaliser le message de type hello à l’aide de hello **mots clés disponibles** liste toodynamically insérer des données d’alerte lorsque message de type Hello est envoyé.
    
    > [!NOTE]
    > Vous pouvez tester la notification par courrier électronique de hello en cliquant sur hello **une Notification de Test** bouton, mais uniquement après l’enregistrement de configuration d’alerte hello.
    > 
    > 
12. Si vous souhaitez toobe notifications validée de serveur web de tooa, vérifiez hello **notifier par HTTP Post** case à cocher.
    
    ![Formulaire de notification par HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    Bonjour **Url** , entrez l’URL hello où que vous voulez message de type hello HTTP validée. Bonjour **en-têtes** zone de texte, entrez toobe d’en-têtes hello HTTP envoyé dans demande de hello.  Pour **corps** vous pouvez personnaliser le message de type hello à l’aide de hello **mots clés disponibles** liste toodynamically insérer des données d’alerte lorsque le message de type hello est envoyé.  **En-têtes** et **corps** par défaut toohello similaire de charge utile XML tooan exemple ci-dessous.
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > Vous pouvez tester hello notification de requête HTTP Post en cliquant sur hello **une Notification de Test** bouton, mais uniquement après l’enregistrement de configuration d’alerte hello.
    > 
    > 
13. Cliquez sur hello **enregistrer** bouton toosave votre configuration d’alerte.  Si vous avez coché la case **Alerte activée** à l’étape 5, votre alerte est maintenant active.

## <a name="next-steps"></a>Étapes suivantes
* Analyser des [statistiques en temps réel dans Azure CDN](cdn-real-time-stats.md)
* Aller plus loin en vous familiarisant avec les [rapports HTTP avancés](cdn-advanced-http-reports.md)
* Analysez les [modes d’utilisation](cdn-analyze-usage-patterns.md)

