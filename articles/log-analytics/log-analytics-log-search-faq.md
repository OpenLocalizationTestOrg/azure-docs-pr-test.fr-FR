---
title: Forum aux questions pour la nouvelle recherche dans les journaux Log Analytics | Documents Microsoft
description: "Cet article fournit le forum aux questions relatives à la mise à niveau de Log Analytics au nouveau langage de requête."
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
ms.openlocfilehash: d7bd0d780c265cc15ad09a73ede8c5a886005e37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Questions fréquentes (FAQ) sur la nouvelle recherche dans les journaux Log Analytics et problèmes connus

Cet article regroupe les questions fréquentes et les problèmes connus relatifs à la mise à niveau de [Log Analytics avec le nouveau langage de requête](log-analytics-log-search-upgrade.md).  Nous vous invitons à lire cet article dans son intégralité avant de vous décider à mettre à niveau votre espace de travail.


## <a name="alerts"></a>Alertes

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-to-create-them-again-in-the-new-language-after-i-upgrade"></a>Question : J’ai un grand nombre de règles d’alerte. Dois-je les recréer dans la nouvelle langue après la mise à niveau ?  
Non, vos règles d’alerte sont automatiquement converties en nouveau langage de recherche pendant la mise à niveau.  


## <a name="computer-groups"></a>Groupes d’ordinateurs

### <a name="question-im-getting-errors-when-trying-to-use-computer-groups--has-their-syntax-changed"></a>Question : J’obtiens des erreurs quand j’essaie d’utiliser des groupes d’ordinateurs.  Leur syntaxe a-t-elle changé ?
Oui, la syntaxe utilisée pour les groupes d’ordinateurs change du moment que votre espace de travail est mis à niveau.  Pour plus d’informations, consultez [Groupes d’ordinateurs dans les recherches dans les journaux Log Analytics](log-analytics-computer-groups.md).

### <a name="known-issue-groups-imported-from-active-directory"></a>Problème connu : Groupes importés à partir d’Active Directory
Il est actuellement impossible de créer une requête qui utilise un groupe d’ordinateurs importé à partir d’Active Directory.  Pour contourner ce problème en attendant sa correction, créez un groupe d’ordinateurs à partir du groupe Active Directory importé, puis utilisez ce nouveau groupe dans votre requête.

Voici un exemple de requête permettant de créer un groupe d’ordinateurs qui comprend un groupe Active Directory importé :

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Tableaux de bord

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Question : Puis-je toujours utiliser des tableaux de bord dans un espace de travail mis à niveau ?
Vous pouvez continuer d’utiliser les vignettes que vous avez ajoutées à **Mon tableau de bord** avant la mise à niveau de votre espace de travail, mais vous ne pouvez ni les modifier ni en ajouter de nouvelles.  Vous pouvez continuer de créer et modifier des vues à l’aide du [Concepteur de vues](log-analytics-view-designer.md) mais aussi créer des tableaux de bord dans le portail Azure.


## <a name="log-searches"></a>Recherches dans les journaux

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-to-the-new-search-language-automatically"></a>Question : J’ai enregistré des recherches en dehors de mon espace de travail mis à niveau. Puis-je les convertir automatiquement en nouveau langage de recherche ?
Vous pouvez utiliser l’outil de conversion de langage dans la page de recherche de journal pour convertir chacune d’elles.  Il n’existe aucune méthode pour la conversion automatique de plusieurs recherches sans mise à niveau de l’espace de travail.

### <a name="question-why-are-my-query-results-not-sorted"></a>Question : Pourquoi mes résultats de requête ne sont pas triés ?
Par défaut, les résultats ne sont pas triés dans le nouveau langage de requête.  Utilisez l’[opérateur de tri](https://go.microsoft.com/fwlink/?linkid=856079) pour trier vos résultats selon une ou plusieurs propriétés.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Problème connu : Les résultats de recherche figurant dans une liste peuvent inclure des propriétés sans données
Les résultats des recherches dans les journaux figurant dans une liste peuvent présenter des propriétés sans données.  Avant la mise à niveau, ces propriétés n’auraient pas été incluses.  Ce problème sera corrigé pour que les propriétés vides ne s’affichent pas.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Problème connu : Le fait de sélectionner une valeur dans un graphique n’a pas pour effet d’afficher des résultats détaillés
Avant la mise à niveau, quand vous sélectionniez une valeur dans un graphique, vous obteniez en retour une liste détaillée d’enregistrements correspondant à la valeur sélectionnée.  Après la mise à niveau, seule la ligne résumée est retournée.  Ce problème est actuellement examiné.

## <a name="log-search-api"></a>API Recherche de journal

### <a name="question-does-the-log-search-api-get-updated-after-i-upgrade"></a>Question : L’API Recherche dans les journaux est-elle mise à jour après la mise à niveau ?
L’[API Recherche dans les journaux](log-analytics-log-search-api.md) n’a pas encore été mise à niveau avec le nouveau langage de recherche.  Continuez d’utiliser le langage de requête existant avec cette API, même après avoir mis à niveau votre espace de travail.  Une documentation mise à jour de l’API Recherche dans les journaux sera mise à disposition quand celle-ci sera mise à jour.


## <a name="portals"></a>Portails

### <a name="question-should-i-use-the-new-advanced-analytics-portal-or-keep-using-the-log-search-portal"></a>Question : Dois-je utiliser le nouveau portail Analytique avancée ou doit-je continuer à utiliser le portail Recherche dans les journaux ?
Vous pouvez consulter un comparatif des deux portails dans [Portails servant à la création et la modification des requêtes de journal dans Azure Log Analytics](log-analytics-log-search-portals.md).  Chacun présentant des avantages particuliers, vous pouvez choisir celui qui répond le mieux à vos besoins.  Il est courant d’écrire des requêtes dans le portail Analytique avancée et de les coller à d’autres endroits comme le Concepteur de vue.  Avant d’effectuer une telle opération, prenez connaissance des [problèmes potentiels](log-analytics-log-search-portals.md#advanced-analytics-portal).


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Question : Existe-t-il des changements suite à l’intégration de Power BI ?
Oui.  Une fois votre espace de travail mis à niveau, puis le processus d’exportation des données de Log Analytics à Power BI ne fonctionne plus.  Toutes les planifications existantes que vous avez créées avant la mise à niveau sont alors désactivées.  Après la mise à niveau, Azure Log Analytics utilise la même plateforme qu’Application Insights et vous devez utiliser le même processus vous permettant d’exporter des requêtes de Log Analytics vers Power BI comme [processus d’exportation des requêtes d’Application Insights vers Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Problème connu : Limite de la taille des demandes Power BI
L’exportation d’une requête Log Analytics vers Power BI est actuellement limitée à une taille de 8 Mo.  Cette limite sera prochainement rehaussée.


##<a name="powershell-cmdlets"></a>Applets de commande PowerShell

### <a name="question-does-the-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Question : L’applet de commande PowerShell de recherche dans les journaux est-elle mise à jour après la mise à niveau ?
L’applet de commande [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) n’a pas encore été mise à niveau avec le nouveau langage de recherche.  Continuez d’utiliser le langage de requête existant avec cette applet de commande, même après avoir mis à niveau votre espace de travail.  Une documentation mise à jour de l’applet de commande sera mise à disposition quand celle-ci sera mise à jour.


## <a name="resource-manager-templates"></a>Modèles Resource Manager

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Question : Puis-je créer un espace de travail mis à niveau avec un modèle Resource Manager ?
Oui.  Vous devez utiliser la version d’API 2017-03-15-preview et ajouter une section **features** dans votre modèle, comme dans l’exemple suivant.

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

### <a name="question-will-my-solutions-continue-to-work"></a>Question : Mes solutions continueront-elles de fonctionner ?
Toutes les solutions continueront de fonctionner dans un espace de travail mis à niveau. Cependant, en les convertissant dans le nouveau langage de requête, vous bénéficierez de meilleures performances.  Certaines solutions existantes décrites dans cette section font face à des problèmes connus.

### <a name="known-issue-capacity-and-performance-solution"></a>Problème connu : Solution Capacity and Performance
Certaines parties de la vue [Capacity and Performance](log-analytics-capacity.md) peuvent être vides.  Ce problème sera prochainement corrigé.

### <a name="known-issue-device-health-solution"></a>Problème connu : Solution Intégrité de l’appareil
La [solution Intégrité de l’appareil](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) ne collecte pas de données dans un espace de travail mis à niveau.  Ce problème sera prochainement corrigé.

### <a name="known-issue-application-insights-connector"></a>Problème connu : Application Insights Connector
Dans la [solution Application Insights Connector](log-analytics-app-insights-connector.md), les perspectives ne sont pas prises en charge dans un espace de travail mis à niveau pour l’instant.  Un correctif permettant de résoudre ce problème est en cours d’analyse.

## <a name="upgrade-process"></a>Mise à niveau

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-the-same-time"></a>Question : Je dispose de plusieurs espaces de travail. Puis-je mettre à niveau tous mes espaces de travail simultanément ?  
Non.  La mise à niveau s’applique à un seul espace de travail à la fois. Actuellement, il n’existe aucun moyen de la mise à niveau de nombreux espaces de travail à la fois. Notez que les autres utilisateurs de l’espace de travail mis à niveau seront également affectés.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Question : Les données de journal collectées dans mon espace de travail seront-elles modifiées en cas de mise à niveau ?  
Non. Les données de journal disponibles pour vos recherches d’espace de travail ne sont pas affectées par la mise à niveau. Les recherches enregistrées, les alertes et les vues seront converties vers le nouveau langage de recherche automatiquement.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Question : Que se passe-t-il si je ne mets pas à niveau mon espace de travail ?  
La recherche de journal héritée sera déconseillée dans les prochains mois. Les espaces de travail qui ne sont pas mis à niveau à ce moment-là seront automatiquement mis à niveau.

### <a name="question-i-didnt-choose-to-upgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Question : Je n’ai pas opté pour la mise à niveau, mais mon espace de travail a quand même été mis à niveau. Que s’est-il passé ?  
Un autre administrateur de cet espace de travail peut l’avoir mis à niveau. Veuillez noter que tous les espaces de travail sont mis à niveau automatiquement lorsque la nouvelle langue est rendue publique.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-to-cancel-it-and-restore-everything-back-what-should-i-do"></a>Question : J’ai effectué par erreur la mise à niveau et dois à présent l’annuler et tout restaurer. Que dois-je faire ?  
Pas de problème.  Nous créons une capture instantanée de votre espace de travail avant la mise à niveau, afin de pouvoir le restaurer. Toutefois, gardez à l’esprit que les recherches, alertes ou images que vous avez enregistrées après la mise à niveau seront perdues.  Pour restaurer l’environnement de votre espace de travail, suivez la procédure décrite dans la section [Puis-je revenir en arrière après la mise à niveau ?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade).


## <a name="views"></a>Views

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Question : Comment créer une vue avec le Concepteur de vues ?
Avant la mise à niveau, il était possible de créer une vue avec le Concepteur de vues à partir d’une vignette du tableau de bord principal.  Quand l’espace de travail est mis à niveau, cette vignette est supprimée.  Vous pouvez créer une vue à l’aide du Concepteur de vues dans le portail OMS en cliquant sur le bouton + vert dans le menu de gauche.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Problème connu : L’option Afficher tout pour les graphiques en courbes située dans les vues ne génère pas de graphique en courbes
Quand vous cliquez sur l’option *Afficher tout* au bas d’un graphique en courbes dans une vue, vous obtenez un tableau.  Avant la mise à niveau, vous obteniez un graphique en courbes.  Ce problème est en cours d’analyse en vue d’une possible modification.


## <a name="next-steps"></a>Étapes suivantes

- Plus d’informations sur la [mise à niveau de votre espace de travail vers le nouveau langage de requête de Log Analytics](log-analytics-log-search-upgrade.md).
