---
title: recherche de journal nouvelle aaaLog Analytique Forum aux questions | Documents Microsoft
description: "Cet article fournit des questions fréquemment posées concernant la mise à niveau hello d’Analytique de journal toohello nouveau langage de requête."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Questions fréquentes (FAQ) sur la nouvelle recherche dans les journaux Log Analytics et problèmes connus

Cet article contient des questions fréquemment posées et les problèmes connus concernant la mise à niveau hello de [Analytique de journal toohello nouveau langage de requête](log-analytics-log-search-upgrade.md).  Lisez cet article avant d’apporter hello décision tooupgrade votre espace de travail.


## <a name="alerts"></a>Alertes

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>Question : J’ai un grand nombre de règles d’alerte. Ai-je besoin toocreate à nouveau dans hello nouvelle langue après une mise à niveau ?  
Non, vos règles d’alerte sont automatiquement converties toohello nouveau langage de recherche pendant la mise à niveau.  


## <a name="computer-groups"></a>Groupes d’ordinateurs

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>Question : j’obtiens erreurs lors de la tentative de groupes d’ordinateurs toouse.  Leur syntaxe a-t-elle changé ?
Oui, syntaxe hello pour l’ordinateur à l’aide de regroupe les modifications lors de la mise à niveau de votre espace de travail.  Pour plus d’informations, consultez [Groupes d’ordinateurs dans les recherches dans les journaux Log Analytics](log-analytics-computer-groups.md).

### <a name="known-issue-groups-imported-from-active-directory"></a>Problème connu : Groupes importés à partir d’Active Directory
Il est actuellement impossible de créer une requête qui utilise un groupe d’ordinateurs importé à partir d’Active Directory.  Comme solution de contournement jusqu'à ce que ce problème est corrigé, créer un groupe d’ordinateurs à l’aide de groupe Active Directory de hello importé et ensuite utiliser ce nouveau groupe dans votre requête.

Un toocreate de requête d’exemple un groupe d’ordinateurs qui inclut un groupe Active Directory importé est comme suit :

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Tableaux de bord

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Question : Puis-je toujours utiliser des tableaux de bord dans un espace de travail mis à niveau ?
Vous pouvez continuer aux vignettes que vous avez ajouté trop toouse**mon tableau de bord** avant que votre espace de travail a été mis à niveau, mais vous ne peut pas modifier ces vignettes ou ajouter de nouveaux.  Vous pouvez continuer toocreate et modifier des vues avec [Concepteur de vue](log-analytics-view-designer.md) et également créer des tableaux de bord Bonjour portail Azure.


## <a name="log-searches"></a>Recherches dans les journaux

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>Question : J’ai enregistré des recherches en dehors de mon espace de travail mis à niveau. Est-il possible de convertir les toohello nouveau langage de recherche automatiquement ?
Vous pouvez utiliser outil de conversion de langage hello dans tooconvert de page de recherche de journal hello chacun d’eux.  Il n’existe aucune conversion de tooautomatically méthode plusieurs recherches sans mise à niveau d’espace de travail hello.

### <a name="question-why-are-my-query-results-not-sorted"></a>Question : Pourquoi mes résultats de requête ne sont pas triés ?
Résultats ne sont pas triés par défaut dans un nouveau langage de requête hello.  Hello d’utilisation [opérateur de tri](https://go.microsoft.com/fwlink/?linkid=856079) toosort vos résultats par une ou plusieurs propriétés.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Problème connu : Les résultats de recherche figurant dans une liste peuvent inclure des propriétés sans données
Les résultats des recherches dans les journaux figurant dans une liste peuvent présenter des propriétés sans données.  Tooupgrade antérieur, ces propriétés ne sont pas incluses.  Ce problème sera corrigé pour que les propriétés vides ne s’affichent pas.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Problème connu : Le fait de sélectionner une valeur dans un graphique n’a pas pour effet d’afficher des résultats détaillés
Tooupgrade préalable, lorsque vous avez sélectionné une valeur dans un graphique, il retourne une liste détaillée des enregistrements correspondant à cette valeur de hello sélectionné.  Après la mise à niveau, uniquement hello synthétisées ligne unique est retournée.  Ce problème est actuellement examiné.

## <a name="log-search-api"></a>API Recherche de journal

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>Question : Hello API de recherche de journal mis à jour après une mise à niveau ?
Hello [API de recherche de journal](log-analytics-log-search-api.md) n’a pas encore été mis à niveau toohello nouveau langage de recherche.  Continuer le langage de requête hérité hello toouse avec cette API, même une fois que vous mettez à niveau votre espace de travail.  Documentation mise à jour sera disponible pour hello API de recherche de journal lorsqu’il est mis à jour.


## <a name="portals"></a>Portails

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>Question : Dois-je utiliser hello nouveau avancé d’Analytique portail ou conserver à l’aide du portail de recherche de journal hello ?
Vous pouvez voir une comparaison de portails hello deux au [portails pour créer et modifier des requêtes de journal dans Azure journal Analytique](log-analytics-log-search-portals.md).  Chacune présente des avantages pour vous pouvez de choisir hello une meilleure pour vos besoins.  Il est des requêtes de toowrite courantes dans le portail d’Analytique de Advanced hello et les coller dans d’autres emplacements tels que le Concepteur de vue.  Vous devez examiner [émet tooconsider](log-analytics-log-search-portals.md#advanced-analytics-portal) lors de l’exécution qui.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Question : Existe-t-il des changements suite à l’intégration de Power BI ?
Oui.  Une fois que votre espace de travail a été mis à niveau puis processus hello pour l’exportation des données de journal Analytique tooPower BI ne fonctionnera plus.  Toutes les planifications existantes que vous avez créées avant la mise à niveau sont alors désactivées.  Après la mise à niveau, les utilisations Analytique de journal Azure hello même plateforme en tant qu’Application Insights et que vous utilisez hello même processus tooexport Analytique de journal des requêtes tooPower BI en tant que [hello processus tooexport Application Insights interroge tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Problème connu : Limite de la taille des demandes Power BI
Il est actuellement une limite de taille de 8 Mo pour une requête Analytique de journal qui peut être exporté tooPower BI.  Cette limite sera prochainement rehaussée.


##<a name="powershell-cmdlets"></a>Applets de commande PowerShell

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Question : Applet de commande PowerShell de recherche de journal hello mis à jour après une mise à niveau ?
Hello [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) n’a pas encore été mis à niveau toohello nouveau langage de recherche.  Continuer le langage de requête hérité hello toouse avec cette applet de commande, même une fois que vous mettez à niveau votre espace de travail.  Documentation mise à jour sera disponible pour l’applet de commande hello lorsqu’il est mis à jour.


## <a name="resource-manager-templates"></a>Modèles Resource Manager

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Question : Puis-je créer un espace de travail mis à niveau avec un modèle Resource Manager ?
Oui.  Vous devez utiliser une version de l’API de 2017-03-15-preview et inclure une **fonctionnalités** section dans votre modèle, comme dans l’exemple suivant de hello.

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>Solutions

### <a name="question-will-my-solutions-continue-toowork"></a>Question : Mes solutions continue toowork ?
Toutes les solutions continue toowork dans un espace de travail mis à niveau, bien que leurs performances seront meilleures si elles sont converties toohello nouveau langage de requête.  Certaines solutions existantes décrites dans cette section font face à des problèmes connus.

### <a name="known-issue-capacity-and-performance-solution"></a>Problème connu : Solution Capacity and Performance
Certaines parties de hello Bonjour [la capacité et performances](log-analytics-capacity.md) la vue peut être vide.  Un problème de toothis correctif sera bientôt disponible.

### <a name="known-issue-device-health-solution"></a>Problème connu : Solution Intégrité de l’appareil
Hello [solution de contrôle d’intégrité de l’appareil](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) ne collectera pas les données dans un espace de travail mis à niveau.  Un problème de toothis correctif sera bientôt disponible.

### <a name="known-issue-application-insights-connector"></a>Problème connu : Application Insights Connector
Dans la [solution Application Insights Connector](log-analytics-app-insights-connector.md), les perspectives ne sont pas prises en charge dans un espace de travail mis à niveau pour l’instant.  Un problème de toothis correctif est en cours analysis.

## <a name="upgrade-process"></a>Mise à niveau

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>Question : Je dispose de plusieurs espaces de travail. Puis-je mettre à niveau tous les espaces de travail à hello même temps ?  
Non.  Mise à niveau s’applique tooa seul espace de travail à chaque fois. Actuellement, il n’existe aucun moyen de la mise à niveau de nombreux espaces de travail à la fois. Notez que les autres utilisateurs de l’espace de travail hello mis à niveau seront affectés également.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Question : Les données de journal collectées dans mon espace de travail seront-elles modifiées en cas de mise à niveau ?  
Non. recherches de Hello journal données disponibles tooyour espace de travail n’est pas affectée par la mise à niveau hello. Les recherches enregistrées, les alertes et les vues sera converti toohello nouveau langage de recherche automatiquement.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Question : Que se passe-t-il si je ne mets pas à niveau mon espace de travail ?  
recherche de journal hérité Hello sera déconseillée dans hello mois à venir. Les espaces de travail qui ne sont pas mis à niveau à ce moment-là seront automatiquement mis à niveau.

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Question : vous n’avez pas choisi tooupgrade, mais mon espace de travail a été mis à niveau quand même ! Que s’est-il passé ?  
Un autre administrateur de cet espace de travail peut avoir mis à niveau espace de travail hello. Notez que tous les espaces de travail seront mis à niveau automatiquement lors de la nouvelle langue de hello rendue publique.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>Question : j’ont mis à niveau par erreur et vous devez maintenant toocancel il et la restauration de tout sauvegarder. Que dois-je faire ?  
Pas de problème.  Nous créons une capture instantanée de votre espace de travail avant la mise à niveau, afin de pouvoir le restaurer. Gardez à l’esprit que la recherche, les alertes ou les vues que vous avez enregistré après que la mise à niveau hello seront perdue si.  toorestore votre environnement d’espace de travail, suivez les procédures de hello au [puis-je accéder après l’exécution d’une mise à niveau ?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Views

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Question : Comment créer une vue avec le Concepteur de vues ?
Tooupgrade préalable, vous pouvez créer une nouvelle vue concepteur de vues à partir d’une vignette de tableau de bord principal hello.  Quand l’espace de travail est mis à niveau, cette vignette est supprimée.  Vous pouvez créer une nouvelle vue avec le Concepteur de vue dans le portail OMS de hello en cliquant sur le bouton dans le menu de gauche hello + de hello vert.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Problème connu : L’option Afficher tout pour les graphiques en courbes située dans les vues ne génère pas de graphique en courbes
Lorsque vous cliquez sur hello *afficher tous les* option bas hello d’une partie du graphique de ligne dans une vue, vous sont présentées avec une table.  Tooupgrade préalable, vous êtes présenté avec un graphique en courbes.  Ce problème est en cours d’analyse en vue d’une possible modification.


## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur [toohello de votre espace de travail de la mise à niveau de langage de requête Analytique de journal nouvelle](log-analytics-log-search-upgrade.md).
