---
title: "aaaGet a démarré avec l’Analyseur de Azure | Documents Microsoft"
description: "Prise en main Azure moniteur toogain idée du fonctionnement de hello de vos ressources et d’agir sur la base de données."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a>Prise en main d’Azure Monitor
Moniteur Azure est un service de plateforme hello qui fournit une source unique pour l’analyse des ressources Azure. Dans le Gestionnaire d’Azure, vous pouvez visualiser, interroger, Router, archiver et agir en conséquence les métriques hello et journaux provenant des ressources dans Azure. Vous pouvez travailler avec ces données à l’aide du Panneau de portail analyse hello, [applets de commande PowerShell analyse](insights-powershell-samples.md), [inter-plateformes CLI](insights-cli-samples.md), ou [API REST de Azure analyse](https://msdn.microsoft.com/library/dn931943.aspx). Dans cet article, nous guider quelques composants clés de hello du moniteur d’Azure, à l’aide du portail de hello pour la démonstration.

1. Dans le portail de hello, accédez trop**davantage de services** et recherche hello **moniteur** option. Cliquez sur hello étoile tooadd cette liste de Favoris de l’option tooyour afin qu’il soit toujours facilement accessible à partir de la barre de navigation gauche hello.
   
    ![Analyser dans la liste des services hello](./media/monitoring-get-started/monitor-more-services.png)
2. Cliquez sur hello **moniteur** tooopen option des hello **moniteur** panneau. Ce panneau rassemble tous vos paramètres de surveillance et données dans une vue consolidée. Il commence par toohello **le journal d’activité** section.
   
    ![Navigation dans le panneau Monitor](./media/monitoring-get-started/monitor-blade-nav.png)
   
    Moniteur de Azure a trois catégories de base de données d’analyse : hello **le journal d’activité**, **métriques**, et **journaux de diagnostic**.
3. Cliquez sur **le journal d’activité** tooensure qui hello section journal d’activité s’affiche.
   
    ![Panneau Journal d’activité](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    Hello [ **le journal d’activité** ](monitoring-overview-activity-logs.md) décrit toutes les opérations effectuées sur les ressources dans votre abonnement. À l’aide de hello journal d’activité, vous pouvez déterminer hello », qui et à quel moment » pour les créer, mettre à jour ou supprimer des opérations sur les ressources dans votre abonnement. Par exemple, hello journal d’activité vous indique quand une application web a été arrêtée et qui s’est arrêté. Événements de journal d’activité sont stockés dans la plateforme de hello et tooquery disponible pendant 90 jours.
   
    Vous pouvez créer et enregistrer des requêtes pour les filtres communs, puis pin hello plus importante requêtes tooa portail du tableau de bord pour que vous sachiez toujours si les événements qui répondent à vos critères se sont produites.
4. Filtrer le groupe de ressources particulier hello vue tooa sur hello la semaine dernière, puis cliquez sur hello **enregistrer** bouton.
   
    ![Enregistrer la requête de journal d’activité](./media/monitoring-get-started/monitor-act-log-save.png)
5. Maintenant, cliquez sur hello **code confidentiel** bouton.
   
    ![Cliquer pour épingler le journal d’activité](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    La plupart des vues hello dans cette procédure pas à pas peut être épinglés tooa le tableau de bord. Cela vous permet de créer une seule source d’informations pour les données opérationnelles sur vos services. 
6. Tableau de bord tooyour de retour. Vous pouvez maintenant voir que la requête de hello (et le nombre de résultats) s’affiche dans votre tableau de bord. Cela est utile si vous souhaitez tooquickly voir toutes les actions de grande ampleur qui se sont produites récemment dans votre abonnement, par exemple. un nouveau rôle attribué ou une machine virtuelle supprimée.
   
    ![Activité journal épinglé toodashboard](./media/monitoring-get-started/monitor-act-log-db.png)
7. Retourner toohello **moniteur** vignette, puis cliquez sur hello **métriques** section. Vous devez tout d’abord tooselect une ressource en filtrant et en sélectionnant à l’aide de hello options de liste déroulante en haut de hello du Panneau de hello.
   
    ![Filtrer les ressources pour les mesures](./media/monitoring-get-started/monitor-met-filter.png)
   
    Toutes les ressources Azure émettent des [**mesures**](monitoring-overview-metrics.md). Cette vue réunit toutes les mesures dans un volet unique afin de pouvoir facilement comprendre le niveau de performance de vos ressources.
8. Une fois que vous avez sélectionné une ressource, toutes les métriques disponibles s’affichent sur hello gauche du Panneau de hello. Vous pouvez plusieurs métriques du graphique à la fois en sélectionnant des métriques et modifier hello graphique type et la plage horaire. Vous pouvez également afficher toutes les alertes de mesures définies pour cette ressource.
   
    ![Volet Metric](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > Certaines mesures sont uniquement disponibles en activant [Application Insights](../application-insights/app-insights-overview.md) et/ou Windows ou Linux Azure Diagnostics sur votre ressource.
   > 
   > 
9. Lorsque vous êtes satisfait de votre graphique, vous pouvez utiliser hello **code confidentiel** bouton toopin il tooyour le tableau de bord.
10. Retourner toohello **moniteur** panneau, cliquez sur **journaux de Diagnostic**.
    
    ![Panneau Journaux de diagnostic](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    [**Journaux de diagnostic** ](monitoring-overview-of-diagnostic-logs.md) journaux émis *par* une ressource qui fournissent des données relatives au fonctionnement de hello d’une ressource particulière. Par exemple, les compteurs de règle de groupe de sécurité réseau et les journaux de flux de travail d’application logique sont des types de journaux de diagnostic. Ces journaux peuvent être stockées dans un compte de stockage, en flux continu tooan concentrateur d’événements, et/ou envoyées trop[Analytique de journal](../log-analytics/log-analytics-overview.md). Log Analytics est le produit d’intelligence opérationnelle de Microsoft pour la recherche avancée et les alertes.
    
    Dans le portail de hello, vous pouvez afficher et filtrer une liste de toutes les ressources dans votre tooidentify abonnement s’ils ont activé les journaux de diagnostic.
11. Cliquez sur une ressource dans le panneau des journaux de diagnostic hello. Si les journaux de diagnostic sont stockés dans un compte de stockage, vous verrez une liste des journaux horaires que vous pouvez télécharger directement.
    
    ![Journaux de diagnostic pour une ressource](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    Vous pouvez également cliquer sur **les paramètres de Diagnostic**, ce qui vous permet de tooset haut ou modifier les paramètres de compte de stockage d’archivage tooa tooEvent concentrateurs de diffusion en continu, ou l’envoi d’espace de travail tooa Analytique de journal.
    
    ![Activer la journalisation des diagnostics](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    Si vous avez configuré des journaux de diagnostic tooLog Analytique, vous pouvez ensuite rechercher les Bonjour **recherche de journal** section du portail de hello.
12. Accédez toohello **alertes** section du panneau d’analyse hello.
    
    ![panneau alertes pour public](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    Ici, vous pouvez gérer toutes les [**alertes**](monitoring-overview-alerts.md) sur vos ressources Azure. Cela inclut les alertes sur les mesures, les événements de journal d’activité, les tests web Application Insights (emplacements) et les diagnostics proactifs Application Insights. Les alertes peuvent déclencher une toobe de courrier électronique envoyé ou de l’URL du webhook tooa HTTP POST.
13. Cliquez sur **ajouter une alerte métrique** toocreate une alerte.
    
    ![Ajouter une alerte de mesure](./media/monitoring-get-started/monitor-alerts-add.png)
    
    Vous pouvez épingler un tooeasily du tableau de bord tooyour alerte voir son état à tout moment.
14. Hello section Moniteur inclut également des liens trop[Application Insights](../application-insights/app-insights-overview.md) applications et [Analytique de journal](../log-analytics/log-analytics-overview.md) solutions de gestion. Ces autres produits Microsoft ont une intégration approfondie avec moniteur Azure Monitor.
15. Si vous n’utilisez pas Application Insights ou Log Analytics, il est possible qu’Azure Monitor ait un partenariat avec vos produits actuels d’analyse, de journalisation et d’alerte. Consultez notre [page des partenaires](monitoring-partners.md) pour obtenir la liste complète et des instructions toointegrate.

En suivant ces étapes et épingler le tableau de bord de tooa toutes les vignettes appropriées, vous pouvez créer des vues complètes de votre application et une infrastructure telle que celle-ci :

![Tableau de bord Azure Monitor](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>Étapes suivantes
* Hello de lecture [vue d’ensemble du moniteur de Windows Azure](monitoring-overview.md)

