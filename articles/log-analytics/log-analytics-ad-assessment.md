---
title: aaaOptimize votre environnement Active Directory avec Azure journal Analytique | Documents Microsoft
description: "Vous pouvez utiliser hello Active Directory évaluation solution tooassess hello des risques et l’intégrité de vos environnements de serveurs selon un intervalle régulier."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>Optimiser votre environnement Active Directory avec hello solution d’évaluation d’Active Directory dans le journal Analytique

![Symbole d’AD Assessment](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

Vous pouvez utiliser hello Active Directory évaluation solution tooassess hello des risques et l’intégrité de vos environnements de serveurs selon un intervalle régulier. Cet article vous aide à installer et utiliser la solution de hello afin que vous puissiez prendre les actions correctives relatives à des problèmes potentiels.

Cette solution fournit une liste hiérarchisée de l’infrastructure de serveurs déployée recommandations tooyour spécifique. les recommandations de Hello sont réparties en focus quatre zones, qui vous permettent de rapidement comprennent hello risque et prenez les mesures.

recommandations de Hello sont basées sur les connaissances de hello et l’expérience acquises par les ingénieurs de Microsoft de milliers de visiteurs. Chaque recommandation explique pourquoi le problème peut concerner tooyou et comment les modifications suggérées tooimplement hello.

Vous pouvez choisir les domaines les plus importantes tooyour organisation et suivre votre progression vers un environnement sans risque et intègre.

Une fois que vous avez ajouté des solutions de hello et une évaluation est terminée, le résumé des informations pour les domaines d’intérêt s’affiche sur hello **évaluation d’Active Directory** tableau de bord pour l’infrastructure hello dans votre environnement. Hello sections suivantes décrivent comment toouse hello plus d’informations sur hello **évaluation d’Active Directory** tableau de bord, où vous pouvez afficher et prenez les actions recommandées pour votre infrastructure de serveur Active Directory.

![image de la vignette d’évaluation de SQL](./media/log-analytics-ad-assessment/ad-tile.png)

![image du tableau de bord d’évaluation de SQL](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>L’installation et la configuration de solution de hello
Utilisez hello suivant informations tooinstall et configurer les solutions hello.

* Agents doivent être installés sur les contrôleurs de domaine qui sont membres de hello domaine toobe est évaluée.
* Hello Active Directory évaluation solution nécessite une version prise en charge de .NET Framework 4 (4.5.2 ou version ultérieure) installé sur chaque ordinateur qui dispose d’un agent OMS.
* Ajouter hello Active Directory évaluation solution tooyour espace de travail OMS à partir de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).  Aucune configuration supplémentaire n’est requise.

  > [!NOTE]
  > Une fois que vous avez ajouté des solutions de hello, fichier AdvisorAssessment.exe de hello est ajouté tooservers avec des agents. Données de configuration sont lu, puis envoyées service OMS de toohello dans le cloud hello pour le traitement. Logique est appliqué toohello reçu données et service de cloud de hello enregistre les données de salutation.
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Détails de la collecte de données d’évaluation Active Directory

Évaluation d’Active Directory collecte des données à partir de hello en utilisant des agents hello que vous avez activé les sources suivantes :

- Collecteurs du Registre
- Collecteurs LDAP
- .NET Framework
- Collecteurs de journaux des événements
- Interfaces ADSI (Active Directory Service Interface)
- Windows PowerShell
- Collecteurs de données de fichier
- Windows Management Instrumentation (WMI)
- API de l’outil DCDIAG
- API de service de réplication de fichiers (NTFRS)
- Code C# personnalisé


Hello tableau suivant présente les méthodes de collecte de données pour les agents, Operations Manager (SCOM) est requis et la façon dont souvent les données sont collectées par un agent.

| plateforme | Agent direct | Agent SCOM | Stockage Azure | SCOM requis ? | Données de l’agent SCOM envoyées via un groupe d’administration | fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 jours |

## <a name="understanding-how-recommendations-are-prioritized"></a>Hiérarchisation des recommandations
Chaque recommandation reçoit une valeur de pondération qui identifie l’importance relative de hello de hello. Recommandations les plus importantes uniquement hello 10 sont affichées.

### <a name="how-weights-are-calculated"></a>Calcul des pondérations
Les pondérations sont des agrégations de valeurs basées sur trois facteurs clés :

* Hello *probabilité* qu’une anomalie identifiée cause des problèmes. Une plus grande probabilité attribue des tooa un score global supérieur pour la recommandation de hello.
* Hello *impact* du problème hello sur votre organisation si elle devait causer un problème. Un plus grand impact attribue tooa un score global supérieur pour la recommandation de hello.
* Hello *effort* requis recommandation de hello tooimplement. Un plus grand effort attribue tooa un score global inférieur pour la recommandation de hello.

Hello pondération de chaque recommandation est exprimée en pourcentage du score total de hello disponibles pour chaque domaine d’intérêt. Par exemple, si une recommandation dans hello sécurité et de domaine de la conformité a un score de 5 %, l’implémentation de cette recommandation augmente votre global score à 5 % de conformité et de sécurité.

### <a name="focus-areas"></a>Domaines
**Sécurité et conformité** : ce domaine présente les recommandations relatives aux menaces de sécurité potentielles et violations de stratégies d’entreprise, ainsi qu’aux exigences techniques, juridiques et réglementaires.

**Disponibilité et continuité d’activité** : ce domaine présente les recommandations relatives à la disponibilité du service, la résilience de votre infrastructure et la protection de votre activité.

**Performances et évolutivité** -cette zone de focus indique toohelp de recommandations de votre organisation informatique croissance, assurez-vous que votre environnement informatique répond aux exigences de performances actuelles et qu’il est en mesure de toorespond toochanging infrastructure a besoin.

**Mise à niveau, Migration et déploiement** - cette zone de focus indique toohelp recommandations vous mettez à niveau, migrer et déployer l’infrastructure existante de tooyour Active Directory.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Faut-il viser tooscore 100 % dans chaque domaine ?
Pas nécessairement. recommandations de Hello sont basées sur la base de connaissances hello et l’expérience acquises par les ingénieurs de Microsoft sur des milliers de visiteurs. Toutefois, aucune chaque infrastructure de serveur n’est même hello et certaines recommandations peuvent être plus ou moins pertinente tooyou. Par exemple, certaines recommandations de sécurité peuvent être moins appropriées si vos ordinateurs virtuels ne sont pas exposé toohello Internet. Certaines recommandations de disponibilité peuvent être moins pertinentes pour les services qui fournissent des rapports et des données ad hoc de faible priorité. Les problèmes entreprise tooa important peuvent être moins important tooa démarrage. Vous pouvez souhaitez tooidentify les domaines d’intérêt figurant parmi vos priorités et puis d’observer comment vos résultats changent au fil du temps.

Chaque recommandation inclut une justification de son importance. Vous devez utiliser cette tooevaluate conseils si la mise en œuvre hello recommandation vous convient, étant donné la nature hello de vos besoins informatiques hello et les services professionnels de votre organisation.

## <a name="use-assessment-focus-area-recommendations"></a>Utilisation des recommandations des domaines d'évaluation
Avant de pouvoir utiliser une solution d’évaluation dans OMS, vous devez avoir installé de solution de hello. tooread savoir plus sur l’installation de solutions, consultez [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md). Après son installation, vous pouvez afficher le résumé hello des recommandations à l’aide de la vignette d’évaluation hello sur la page de vue d’ensemble de hello dans OMS.

Hello d’affichage résumés des évaluations de conformité pour votre infrastructure, puis Explorez les recommandations.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recommandations tooview pour un focus zone et prendre une action corrective
1. Sur hello **vue d’ensemble** , cliquez sur hello **évaluation** vignette pour votre infrastructure de serveur.
2. Sur hello **évaluation** , examinez les informations de résumé hello dans un des panneaux de domaine hello, puis cliquez sur une recommandations de tooview d’intérêt.
3. Sur les pages de zone de focus hello, vous pouvez afficher les recommandations hello hiérarchisé pour votre environnement. Cliquez sur une recommandation sous **objets affectés** tooview plus de détails sur pourquoi hello recommandation est faite.  
    ![image des recommandations d'évaluation](./media/log-analytics-ad-assessment/ad-focus.png)
4. Vous pouvez effectuer les actions correctives suggérées dans **Actions suggérées**. Lorsque l’élément de hello a été traité, les enregistrements d’évaluations que les actions recommandées ont été prises et votre score de conformité augmentera. Les éléments corrigés apparaissent comme **objets passés**.

## <a name="ignore-recommendations"></a>Ignorer les recommandations
Si vous avez des recommandations que vous souhaitez tooignore, vous pouvez créer un fichier texte qu’OMS utilisera tooprevent des recommandations d’apparaître dans les résultats d’évaluation.

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>recommandations de tooidentify vous ignorera
1. Connectez-vous à tooyour espace de travail et ouvrez recherche de journal. Utilisez hello requête toolist recommandations ayant échoué pour les ordinateurs de votre environnement.

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello au-dessus de requête pourrait être modifié toohello suivant.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   Voici une requête de recherche de journal de capture d’écran montrant hello : ![Échec de recommandations](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. Choisissez les recommandations que vous souhaitez tooignore. Vous utiliserez les valeurs hello pour RecommendationId dans la procédure suivante de hello.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate et utilisez un fichier texte IgnoreRecommendations.txt
1. Créez un fichier nommé IgnoreRecommendations.txt.
2. Collez ou tapez chaque RecommendationId de chaque recommandation que vous souhaitez tooignore Analytique de journal sur une ligne distincte, puis enregistrez et fermez le fichier de hello.
3. Fichier PUT hello Bonjour suivant du dossier sur chaque ordinateur où vous souhaitez les recommandations de tooignore OMS.
   * Sur les ordinateurs avec hello Microsoft Monitoring Agent (connecté directement ou via Operations Manager) - *lecteur_système*: \Program Files\Microsoft Monitoring Agent\Agent
   * Sur le serveur d’administration Operations Manager de hello - *lecteur_système*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que les recommandations sont ignorées.
Après l’exécution de hello prochaine évaluation planifiée, par défaut, tous les 7 jours, hello spécifié recommandations sont marquées *ignoré* et n’apparaissent pas dans le tableau de bord évaluation hello.

1. Vous pouvez utiliser hello suivant toolist de requêtes de recherche de journal de toutes les recommandations hello ignoré.

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello au-dessus de requête pourrait être modifié toohello suivant.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. Si vous décidez ultérieurement que vous souhaitez les recommandations toosee ignorée, supprimez tous les fichiers IgnoreRecommendations.txt ou vous supprimez des RecommendationIDs dans les.

## <a name="ad-assessment-solutions-faq"></a>FAQ sur les solutions d'évaluation AD
*Quelle est la fréquence d'exécution des évaluations ?*

* évaluation de Hello s’exécute tous les 7 jours.

*Existe-t-il un tooconfigure moyen la fréquence d’exécution des évaluations de hello ?*

* Pas pour l'instant.

*Si un autre serveur est découvert après l'ajout d'une solution d'évaluation, ce serveur sera-t-il évalué ?*

* Oui, une fois découverts, les nouveaux serveurs sont évalués tous les 7 jours.

*Si un serveur est mis hors service, quand il soustrait de l’évaluation de hello ?*

* Si un serveur n'envoie pas de données pendant 3 semaines, il est supprimé.

*Qu’est le nom de hello du processus hello hello collecte des données ?*

* AdvisorAssessment.exe

*Combien de temps faut-il pour toobe des données collectée ?*

* collecte de données réelles Hello sur le serveur de hello prend environ 1 heure. Cela peut prendre plus de temps sur les serveurs dotés d'un grand nombre de serveurs Active Directory.

*Existe-t-il un moyen tooconfigure lorsque les données sont collectées ?*

* Pas pour l'instant.

*Pourquoi afficher uniquement hello 10 premières recommandations ?*

* Au lieu d’exploiter une liste exhaustive et écrasante de tâches, nous vous recommandons de vous concentrer sur les recommandations hello classés par priorité. Une fois que vous les aurez suivies, de nouvelles recommandations apparaîtront. Si vous préférez liste détaillée de hello toosee, vous pouvez afficher toutes les recommandations à l’aide de la recherche de journal.

*Existe-t-il un moyen tooignore une recommandation ?*

* Oui, consultez la section [Ignorer les recommandations](#ignore-recommendations) ci-dessus.

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [connecter recherche Analytique de journal](log-analytics-log-searches.md) tooview détaillées des données d’évaluation d’Active Directory et les recommandations.
