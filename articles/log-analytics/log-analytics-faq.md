---
title: aaaLog Analytique FAQ | Documents Microsoft
description: "Elles en sonttrop de réponses aux questions posées hello service de l’Analytique des journaux Azure."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>FAQ sur Log Analytics
Ce FAQ Microsoft est une liste des questions fréquemment posées concernant Log Analytics dans Microsoft Operations Management Suite (OMS). Si vous avez d’autres questions sur Analytique de journal, accédez à toohello [forum de discussion](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) et publiez vos questions. Lorsqu’une question est fréquemment posée, nous ajouter toothis article afin qu’il peut trouver rapidement et facilement.

## <a name="general"></a>Généralités

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>Q : Analytique de journal utilise-t-il hello même agent comme Azure Security Center ?

R : Dans les premières juin 2017, Azure Security Center a commencé à l’aide de Microsoft Monitoring Agent toocollect et le magasin de données d’hello. toolearn, voir [Azure Security Center Platform Migration FAQ](../security-center/security-center-platform-migration-faq.md).

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>Q : Les vérifications sont effectuées par hello AD et les solutions d’évaluation de SQL ?

R : Hello requête suivante affiche une description de toutes les vérifications actuellement effectuées :

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

Hello résultats peuvent ensuite être exportée tooExcel pour un examen plus approfondi.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>Q : Pourquoi vois-je autre chose *qu’OMS* dans la console System Center Operations Manager ?

R : Selon le correctif cumulatif d’Operations Manager que vous utilisez, vous pouvez voir un nœud pour *System Center Advisor*, *Operational Insights* ou *Log Analytics*.

Hello mise à jour de chaîne de texte trop*OMS* est inclus dans un Pack d’administration, qui doit toobe importé manuellement. texte de toosee hello actuel et les fonctionnalités, suivez les instructions de hello hello dernière mise à jour cumul Ko de System Center Operations Manager article et actualisation hello console.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>Q : Existe-t-il une version *locale* de Log Analytics ?

R : Non. Log Analytics traite et stocke de grandes quantités de données. Comme un service cloud, Analytique de journal est en mesure de tooscale à distance si nécessaire et éviter de n’importe quel environnement de tooyour d’impact sur les performances.

En voici d’autres avantages :
- Microsoft s’exécute l’infrastructure hello Analytique de journal, vous évitant les coûts
- Des correctifs et des mises à jour des fonctionnalités sont régulièrement déployés.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>Q : Si Log Analytics ne collecte plus de données, comment détecter le problème ?

R : Si vous êtes sur hello libre de niveau de tarification et que vous avez envoyés plus de 500 Mo de données dans un jour, la collecte de données s’arrête pour rest hello du jour de hello. Après avoir atteint limite quotidienne de hello est une raison courante Analytique de journal arrête la collecte de données ou les données apparaissent toobe manquant.

Log Analytics crée un événement de type *Operation* lorsque la collecte de données démarre et s’arrête. 

Exécutez hello suivant la requête de recherche toocheck si vous êtes atteint la limite quotidienne de hello et données manquantes :`Type=Operation OperationCategory="Data Collection Status"`

Lorsque la collecte de données s’arrête, hello *OperationStatus* est **avertissement**. Lorsque la collecte de données démarre, hello *OperationStatus* est **Succeeded**. 

Hello tableau suivant décrit les raisons pour lesquelles l’arrêt de la collecte de données et une collection de données tooresume action suggérée :

| Raison pour laquelle la collecte de données s’arrête                       | collecte des données tooresume |
| -------------------------------------------------- | ----------------  |
| Limite quotidienne de données gratuites atteinte<sup>1</sup>       | Attendez que hello suivant jour pour le redémarrage de tooautomatically de collection, ou<br> Modification tooa payé niveau tarifaire |
| Abonnement Azure à l’état interrompu pour la raison suivante : <br> Fin de l’essai gratuit <br> Expiration du Pass Azure <br> Limite de dépense mensuelle atteinte (par exemple, sur un abonnement MSDN ou Visual Studio)                          | Convertir tooa abonnement payée <br> Convertir tooa abonnement payée <br> Supprimer la limite ou attendre sa réinitialisation |

<sup>1</sup> si votre espace de travail se trouve sur hello libre de niveau de tarification, vous êtes limité toosending 500 Mo de données par le service de toohello jour. Lorsque vous atteignez la limite quotidienne de hello, collecte de données s’arrête jusqu'à hello jour suivant. Les données envoyées pendant l’arrêt de la collecte de données ne sont pas indexées et ne sont pas accessibles à la recherche. Lorsque la collecte de données reprend, le traitement se produit uniquement pour les nouvelles données envoyées. 

Log Analytics utilise l’heure UTC ; chaque jour commence à minuit UTC. Si l’espace de travail hello atteint la limite quotidienne de hello, le traitement reprend pendant hello première heure Hello jour UTC suivant.

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>Q : Comment être informé de l’arrêt de la collecte de données ?

R : utilisez les étapes de hello décrites dans [créer une règle d’alerte](log-analytics-alerts-creating.md#create-an-alert-rule) toobe informé de l’arrêt de la collecte de données.

Lors de la création d’alerte hello arrêt de la collecte de données, définissez le :
- **Nom** trop*arrêtée la collecte de données*
- **Gravité** trop*avertissement*
- **Requête de recherche** trop`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **Fenêtre de temps** trop*2 heures*.
- **Fréquence des alertes** toobe une heure dans la mesure où les données d’utilisation hello met à jour uniquement une fois par heure.
- **Générer une alerte en fonction de** toobe *nombre de résultats*
- **Nombre de résultats** toobe *supérieur à 0*

Utilisez les étapes hello décrites dans [ajouter des actions tooalert règles](log-analytics-alerts-actions.md) configurer une action de courrier électronique, webhook ou runbook pour la règle d’alerte hello.


## <a name="configuration"></a>Configuration
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>Q : Modifier le nom hello de hello objets blob ou table conteneur utilisé tooread à partir de Azure Diagnostics (WAD) ?

R : Non, il n’est pas possible actuellement tooread à partir de tables arbitraires ou des conteneurs dans le stockage Azure.

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>Q : Les adresses IP hello utilisation du service journal Analytique ? Comment s’assurer que mon pare-feu autorise uniquement les services d’Analytique des journaux de trafic toohello ?

R : Hello service d’Analytique de journal s’appuie sur Azure. Adresses IP de l’Analytique de journal sont Bonjour [plages d’adresses IP Microsoft Azure Datacenter](http://www.microsoft.com/download/details.aspx?id=41653).

Lors des déploiements de service, hello adresses IP de service de l’Analytique des journaux de hello changent. Hello tooallow de noms DNS dans votre pare-feu sont documentés dans [configurer les paramètres de pare-feu et de proxy dans le journal Analytique](log-analytics-proxy-firewall.md).

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>Q : J’utilise ExpressRoute pour la connexion tooAzure. Mon trafic Log Analytics utilise-t-il ma connexion ExpressRoute ?

R : Hello de différents types de trafic ExpressRoute est décrits dans hello [documentation d’ExpressRoute](../expressroute/expressroute-faqs.md#supported-services).

Le trafic tooLog Analytique utilise le circuit de ExpressRoute d’homologation publique hello.

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>Q : Existe-t-il un moyen simple et facile de toomove un tooanother d’espace de travail existant Analytique de journal Analytique de journal espace de travail/abonnement Azure ?

R : Hello `Move-AzureRmResource` applet de commande vous permet de déplacer un espace de travail Analytique de journal et un compte Automation à partir d’un abonnement Azure tooanother. Pour plus d’informations, consultez [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).

Cette modification peut également avoir lieu dans hello portail Azure.

Vous ne peut pas déplacer les données d’une tooanother d’espace de travail Analytique des journaux ou modifier les données Analytique de journal sont stockées dans la région hello.

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>Q : comment ajouter des journaux Analytique tooSystem Center Operations Manager ?

R : mise à jour toohello dernier correctif cumulatif de mise à jour et de l’importation des packs d’administration vous permettent de tooconnect Operations Manager tooLog Analytique.

>[!NOTE]
>tooLog de connexion d’Operations Manager Hello Analytique n’est disponible que pour System Center Operations Manager 2012 SP1 et versions ultérieures.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>Q : Comment puis-je vérifier qu’un agent est en mesure de toocommunicate avec Analytique de journal ?

R : tooensure que l’agent hello peut communiquer avec OMS, accédez à : le panneau de configuration, de sécurité et de paramètres, **Microsoft Monitoring Agent**.

Sous hello **Analytique des journaux (OMS) Azure** onglet, recherchez une coche verte. Une icône de coche verte confirme que l’agent hello est en mesure de toocommunicate avec hello service OMS.

Une icône d’avertissement jaune signifie hello agent rencontre des problèmes de communication avec OMS. L’une des raisons courantes sont hello service Microsoft Monitoring Agent s’est arrêté. Utiliser service manager toorestart hello service de contrôle de.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>Q : Comment empêcher un agent de communiquer avec Log Analytics ?

R : dans System Center Operations Manager, supprimez ordinateur de hello à partir de la liste des ordinateurs gérés hello Advisor. Mises à jour de Operations Manager hello configuration de hello agent toono plus rapport tooLog Analytique. Pour les agents directement connectés tooLog Analytique, vous pouvez les arrêter de communiquer via : le panneau de configuration, de sécurité et de paramètres, **Microsoft Monitoring Agent**.
Sous **Azure Log Analytics (OMS)**, supprimez tous les espaces de travail répertoriés.

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>Q : pourquoi une erreur lors de le toomove mon espace de travail à partir d’un abonnement Azure tooanother ?

R : Si vous utilisez hello portail Azure, n'assurez-vous qu’espace de travail hello est sélectionné pour hello de déplacement. Ne sélectionnez pas les solutions hello--il va passer automatiquement une fois l’espace de travail hello déplace. 

Vérifiez que vous disposez de l’autorisation nécessaire dans les deux abonnements Azure.

## <a name="agent-data"></a>Données de l’agent
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>Q : La quantité de données puis-je envoyer via hello agent tooLog Analytique ? Existe-t-il une quantité maximale de données par client ?
R : un plan gratuit Hello définit une limite quotidienne de 500 Mo par espace de travail. Hello standard et les plans de premium n’ont aucune limite de quantité hello de données qui sont téléchargées. Comme un service cloud, Analytique de journal est conçu échelle tooautomatically volume de hello toohandle provenant d’un client, même si elle est de plusieurs téraoctets par jour.

agent d’Analytique de journal Hello a été tooensure conçue, il a un faible encombrement mémoire. Un de nos clients a écrit un blog sur les tests hello qu’il a effectués sur notre agent, impressionnantes. volume de données Hello varie en fonction des solutions hello que vous activez. Vous pouvez trouver des informations détaillées sur le volume de données hello et voir les limites de hello par solution Bonjour [utilisation](log-analytics-usage.md) page.

Pour plus d’informations, vous pouvez lire un [client blog](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) sur hello faible encombrement de l’agent OMS de hello.

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>Q : Quantité de bande passante réseau est utilisé par hello Microsoft Management Agent (MMA) lors de l’envoi des données tooLog Analytique ?

R : La bande passante est fonction de quantité hello de données envoyées. Données sont compressées lors de leur envoi réseau hello.

### <a name="q-how-much-data-is-sent-per-agent"></a>Q : Quelle est la quantité de données envoyées par agent ?

R : Hello des données envoyées par agent dépend :

* vous avez activé des solutions Hello
* nombre de Hello de journaux et des compteurs de performances collectés
* volume Hello de données dans les journaux de hello

Hello libre niveau tarifaire est un bon moyen tooonboard plusieurs serveurs et évaluer le volume de données de type hello. L’utilisation globale est affichée sur hello [utilisation](log-analytics-usage.md) page.

Pour les ordinateurs qui sont en mesure de toorun hello par l’agent WireData, utilisez hello suivant toosee requête la quantité de données envoyée :

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>Étapes suivantes
* [Prise en main Analytique de journal](log-analytics-get-started.md) toolearn plus d’informations sur le journal Analytique et get opérationnel en quelques minutes.
