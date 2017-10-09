---
title: "aaaOptimize votre environnement SQL Server avec l’Analytique des journaux Azure | Documents Microsoft"
description: "Avec Azure Analytique de journal, vous pouvez utiliser hello évaluation SQL solution tooassess hello des risques et l’intégrité de vos environnements SQL server selon un intervalle régulier."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a>Optimiser votre environnement SQL Server avec hello solution d’évaluation SQL dans le journal Analytique

![Symbole de SQL Assessment](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

Vous pouvez utiliser hello évaluation SQL solution tooassess hello des risques et l’intégrité de vos environnements de serveurs selon un intervalle régulier. Cet article va vous aider à installer la solution de hello afin que vous puissiez prendre les actions correctives relatives à des problèmes potentiels.

Cette solution fournit une liste hiérarchisée de l’infrastructure de serveurs déployée recommandations tooyour spécifique. recommandations de Hello sont classées en six focus domaines, ce qui vous aider à rapidement comprennent hello risque et l’action corrective.

Hello recommandations sont basées sur les connaissances de hello et l’expérience acquises par les ingénieurs de Microsoft de milliers de visiteurs. Chaque recommandation explique pourquoi le problème peut concerner tooyou et comment les modifications suggérées tooimplement hello.

Vous pouvez choisir les domaines les plus importantes tooyour organisation et suivre votre progression vers un environnement sans risque et intègre.

Une fois que vous avez ajouté des solutions de hello et une évaluation est terminée, le résumé des informations pour les domaines d’intérêt s’affiche sur hello **évaluation SQL** tableau de bord pour l’infrastructure hello dans votre environnement. Hello sections suivantes décrivent comment toouse hello plus d’informations sur hello **évaluation SQL** tableau de bord, où vous pouvez afficher et prenez les actions recommandées pour votre infrastructure SQL server.

![image de la vignette d’évaluation de SQL](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![image du tableau de bord d’évaluation de SQL](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a>L’installation et la configuration de solution de hello
Évaluation de SQL fonctionne avec toutes les versions actuellement prises en charge de SQL Server pour les éditions Standard, Developer et Enterprise hello.

Utilisez hello suivant tooinstall des informations et configurer une solution de hello.

* Les agents doivent être installés sur des serveurs sur lesquels SQL Server est installé.
* Hello solution SQL Assessment requiert une version prise en charge de .NET Framework 4 est installé sur chaque ordinateur qui dispose d’un agent OMS.
* Dans une solution de commandes tooinstall hello, utilisateur de hello doit être un abonnement Azure de toohello administrateur ou collaborateur lorsqu’à l’aide de hello portail Azure. En outre, utilisateur de hello doit être un membre hello OMS espace de travail administrateur ou collaborateur rôle dans portail OMS : hello.
* Lors de l’utilisation de l’agent Operations Manager de hello avec l’évaluation de SQL, vous devez toouse un compte d’Operations Manager Run-As. Consultez la rubrique [Comptes d’identification Operations Manager pour OMS](#operations-manager-run-as-accounts-for-oms) ci-dessous pour plus d’informations.

  > [!NOTE]
  > l’agent de Hello MMA ne prend pas en charge les comptes Operations Manager Run-As.
  >
  >
* Ajouter hello évaluation SQL solution tooyour espace de travail OMS à l’aide du processus de hello décrit dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md). Aucune configuration supplémentaire n’est requise.

> [!NOTE]
> Une fois que vous avez ajouté des solutions de hello, fichier AdvisorAssessment.exe de hello est ajouté tooservers avec des agents. Données de configuration sont lu, puis envoyées service OMS de toohello dans le cloud hello pour le traitement. Logique est appliqué toohello reçu données et service de cloud de hello enregistre les données de salutation.

## <a name="sql-assessment-data-collection-details"></a>Détails de l'évaluation SQL de la collection de données
Évaluation de SQL collecte les données WMI, données de Registre, les données de performances et les résultats de vue de gestion dynamique SQL Server à l’aide d’agents hello que vous avez activés.

Hello tableau suivant présente les méthodes de collecte de données pour les agents, Operations Manager (SCOM) est requis et la façon dont souvent les données sont collectées par un agent.

| plateforme | Agent direct | Agent SCOM | Stockage Azure | SCOM requis ? | Données de l’agent SCOM envoyées via un groupe d’administration | fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  | &#8226; |7 jours |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Comptes d’identification Operations Manager pour OMS
Analytique de journal d’OMS utilise hello agent Operations Manager et toocollect de groupe d’administration et envoyer le service de données toohello OMS. OMS utilise les packs d’administration pour les charges de travail tooprovide services à valeur ajoutée. Chaque charge de travail requiert des packs d’administration de toorun des privilèges spécifiques de la charge de travail dans un contexte de sécurité différent, tel qu’un compte de domaine. Vous avez besoin des informations d’identification de tooprovide en configurant un compte d’identification Operations Manager.

Utilisez hello suivant informations tooset hello exécuter en tant que compte d’Operations Manager pour l’évaluation SQL.

### <a name="set-hello-run-as-account-for-sql-assessment"></a>Définir hello compte d’identification pour l’évaluation SQL
 Si vous utilisez déjà hello Pack d’administration de SQL Server, vous devez utiliser ce compte d’identification.

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a>tooconfigure hello SQL comme compte d’identification dans la console opérateur de hello
> [!NOTE]
> Si vous utilisez hello OMS diriger l’agent, plutôt que l’agent SCOM de hello, pack d’administration hello s’exécute toujours dans le contexte de sécurité hello Hello compte système Local. Skip étapes 1 à 5 ci-dessous et exécution hello soit exemple T-SQL ou de Powershell, en spécifiant NT AUTHORITY\SYSTEM en tant que nom d’utilisateur hello.
>
>

1. Dans Operations Manager, ouvrez la console opérateur de hello, puis cliquez sur **Administration**.
2. Sous **Configuration d’identification**, cliquez sur **Profils**, puis ouvrez **Profil d’identification de l’évaluation SQL OMS**.
3. Sur hello **comptes d’identification** , cliquez sur **ajouter**.
4. Sélectionnez un compte d’identification Windows qui contient les informations d’identification hello nécessaires pour SQL Server, ou cliquez sur **nouveau** toocreate une.

   > [!NOTE]
   > Hello exécuter en tant que le type de compte doit être Windows. Hello compte d’identification doit également faire partie du groupe Administrateurs Local sur tous les serveurs Windows hébergeant des Instances de SQL Server.
   >
   >
5. Cliquez sur **Enregistrer**.
6. Modifier, puis exécutez hello suivant l’exemple T-SQL sur chaque tooRun requis l’Instance SQL Server toogrant autorisations minimales en tant que compte tooperform évaluation SQL. Toutefois, vous n’avez pas besoin toodo cela si un compte d’identification fait déjà partie du rôle de serveur sysadmin hello sur les Instances de SQL Server.

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a>tooconfigure hello SQL exécuter en tant que compte à l’aide de Windows PowerShell
Ouvrez une fenêtre PowerShell et exécutez hello script suivant une fois que vous avez la mise à jour avec vos informations :

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a>Hiérarchisation des recommandations
Chaque recommandation reçoit une valeur de pondération qui identifie l’importance relative de hello de hello. Uniquement hello dix recommandations les plus importantes sont affichées.

### <a name="how-weights-are-calculated"></a>Calcul des pondérations
Les pondérations sont des agrégations de valeurs basées sur trois facteurs clés :

* Hello *probabilité* qu’une anomalie identifiée cause des problèmes. Une plus grande probabilité attribue des tooa un score global supérieur pour la recommandation de hello.
* Hello *impact* du problème hello sur votre organisation si elle devait causer un problème. Un plus grand impact attribue tooa un score global supérieur pour la recommandation de hello.
* Hello *effort* requis recommandation de hello tooimplement. Un plus grand effort attribue tooa un score global inférieur pour la recommandation de hello.

Hello pondération de chaque recommandation est exprimée en pourcentage du score total de hello disponibles pour chaque domaine d’intérêt. Par exemple, si une recommandation dans hello sécurité et de domaine de la conformité a un score de 5 %, implémentation de cette recommandation augmentera votre global score à 5 % de conformité et de sécurité.

### <a name="focus-areas"></a>Domaines
**Sécurité et conformité** : ce domaine présente les recommandations relatives aux menaces de sécurité potentielles et violations de stratégies d’entreprise, ainsi qu’aux exigences techniques, juridiques et réglementaires.

**Disponibilité et continuité d’activité** : ce domaine présente les recommandations relatives à la disponibilité du service, la résilience de votre infrastructure et la protection de votre activité.

**Performances et évolutivité** -cette zone de focus indique toohelp de recommandations de votre organisation informatique croissance, assurez-vous que votre environnement informatique répond aux exigences de performances actuelles et qu’il est en mesure de toorespond toochanging infrastructure a besoin.

**Mise à niveau, Migration et déploiement** - cette zone de focus indique toohelp recommandations vous mettez à niveau, migrer et déployer l’infrastructure existante de SQL Server tooyour.

**Opérations et surveillance** - cette zone de focus indique recommandations toohelp rationaliser vos opérations informatiques, mettre en œuvre de maintenance préventive et optimiser les performances.

**Gestion des modifications et Configuration** -ce domaine d’intérêt présente des recommandations toohelp protéger les opérations quotidiennes, assurez-vous que modifications n’a un impact négatif affectent votre infrastructure, établissez des procédures de contrôle des modifications et tootrack et d’audit configurations système.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Faut-il viser tooscore 100 % dans chaque domaine ?
Pas nécessairement. recommandations de Hello sont basées sur la base de connaissances hello et l’expérience acquises par les ingénieurs de Microsoft sur des milliers de visiteurs. Toutefois, aucune chaque infrastructure de serveur n’est même hello et certaines recommandations peuvent être plus ou moins pertinente tooyou. Par exemple, certaines recommandations de sécurité peuvent être moins appropriées si vos ordinateurs virtuels ne sont pas exposé toohello Internet. Certaines recommandations de disponibilité peuvent être moins pertinentes pour les services qui fournissent des rapports et des données ad hoc de faible priorité. Les problèmes entreprise tooa important peuvent être moins important tooa démarrage. Vous pouvez souhaitez tooidentify les domaines d’intérêt figurant parmi vos priorités et puis d’observer comment vos résultats changent au fil du temps.

Chaque recommandation inclut une justification de son importance. Vous devez utiliser cette tooevaluate conseils si la mise en œuvre hello recommandation vous convient, étant donné la nature hello de vos besoins informatiques hello et les services professionnels de votre organisation.

## <a name="use-assessment-focus-area-recommendations"></a>Utilisation des recommandations des domaines d'évaluation
Avant de pouvoir utiliser une solution d’évaluation dans OMS, vous devez avoir installé de solution de hello. tooread savoir plus sur l’installation de solutions, consultez [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md). Après son installation, vous pouvez afficher le résumé hello des recommandations à l’aide de la vignette d’évaluation SQL hello sur la page de vue d’ensemble de hello dans OMS.

Hello d’affichage résumés des évaluations de conformité pour votre infrastructure, puis Explorez les recommandations.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recommandations tooview pour un focus zone et prendre une action corrective
1. Sur hello **vue d’ensemble** , cliquez sur hello **évaluation SQL** vignette.
2. Sur hello **évaluation SQL** , examinez les informations de résumé hello dans un des panneaux de domaine hello, puis cliquez sur une recommandations de tooview d’intérêt.
3. Sur les pages de zone de focus hello, vous pouvez afficher les recommandations hello hiérarchisé pour votre environnement. Cliquez sur une recommandation sous **objets affectés** tooview plus de détails sur pourquoi hello recommandation est faite.  
    ![Image des recommandations de l’évaluation SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)
4. Vous pouvez effectuer les actions correctives suggérées dans **Actions suggérées**. Lorsque l’élément de hello a été traité, évaluations ultérieures indiqueront les actions ont été prises et votre score de conformité augmentera qu’enregistre. Les éléments corrigés apparaissent comme **objets passés**.

## <a name="ignore-recommendations"></a>Ignorer les recommandations
Si vous avez des recommandations que vous souhaitez tooignore, vous pouvez créer un fichier texte qu’OMS utilisera tooprevent des recommandations d’apparaître dans les résultats d’évaluation.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>recommandations de tooidentify vous ignorera
1. Connectez-vous à tooyour espace de travail et ouvrez recherche de journal. Utilisez hello requête toolist recommandations ayant échoué pour les ordinateurs de votre environnement.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   Voici une requête de recherche de journal de capture d’écran montrant hello : ![Échec de recommandations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)
2. Choisissez les recommandations que vous souhaitez tooignore. Vous utiliserez les valeurs hello pour RecommendationId dans la procédure suivante de hello.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate et utilisez un fichier texte IgnoreRecommendations.txt
1. Créez un fichier nommé IgnoreRecommendations.txt.
2. Collez ou tapez chaque RecommendationId de chaque recommandation que vous souhaitez tooignore OMS sur une ligne distincte, puis enregistrez et fermez le fichier de hello.
3. Fichier PUT hello Bonjour suivant du dossier sur chaque ordinateur où vous souhaitez les recommandations de tooignore OMS.
   * Sur les ordinateurs avec hello Microsoft Monitoring Agent (connecté directement ou via Operations Manager) - *lecteur_système*: \Program Files\Microsoft Monitoring Agent\Agent
   * Sur le serveur d’administration Operations Manager de hello - *lecteur_système*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que les recommandations sont ignorées.
1. Après l’exécution de hello prochaine évaluation planifiée, par défaut, tous les 7 jours, hello spécifié recommandations sont marquées comme étant des ignorées et n’apparaissent pas dans le tableau de bord évaluation hello.
2. Vous pouvez utiliser hello suivant toolist de requêtes de recherche de journal de toutes les recommandations hello ignoré.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. Si vous décidez ultérieurement que vous souhaitez les recommandations toosee ignorée, supprimez tous les fichiers IgnoreRecommendations.txt ou vous supprimez des RecommendationIDs dans les.

## <a name="sql-assessment-solution-faq"></a>FAQ sur les solutions d'évaluation de SQL
*Quelle est la fréquence d'exécution des évaluations ?*

* évaluation de Hello s’exécute tous les 7 jours.

*Existe-t-il un tooconfigure moyen la fréquence d’exécution des évaluations de hello ?*

* Pas pour l'instant.

*Si un autre serveur est découvert après que j’ai ajouté hello solution d’évaluation SQL, est-il évalué ?*

* Oui, une fois découverts, les nouveaux serveurs sont évalués tous les 7 jours.

*Si un serveur est mis hors service, quand il soustrait de l’évaluation de hello ?*

* Si un serveur n'envoie pas de données pendant 3 semaines, il est supprimé.

*Qu’est le nom de hello du processus hello hello collecte des données ?*

* AdvisorAssessment.exe

*Combien de temps faut-il pour toobe des données collectée ?*

* collecte de données réelles Hello sur le serveur de hello prend environ 1 heure. Cela peut prendre plus de temps sur les serveurs dotés d'un grand nombre d'instances SQL ou de bases de données.

*Quels types de données sont collectés ?*

* Hello, les types de données suivants est collecté :
  * WMI
  * Registre
  * Compteurs de performances
  * Vues de gestion dynamique (DMV) SQL

*Existe-t-il un moyen tooconfigure lorsque les données sont collectées ?*

* Pas pour l'instant.

*Pourquoi dois-je tooconfigure un compte d’identification ?*

* Pour SQL Server, un petit nombre de requêtes SQL est exécuté. Pour qu’ils toorun, un compte d’identification avec tooSQL des autorisations VIEW SERVER STATE doit être utilisé.  En outre, en ordre tooquery WMI, les informations d’identification d’administrateur local sont requises.

*Pourquoi afficher uniquement hello 10 premières recommandations ?*

* Au lieu d’exploiter une liste exhaustive et écrasante de tâches, nous vous recommandons de vous concentrer sur les recommandations hello classés par priorité. Une fois que vous les aurez suivies, de nouvelles recommandations apparaîtront. Si vous préférez liste détaillée de hello toosee, vous pouvez afficher toutes les recommandations à l’aide de la recherche des journaux OMS hello.

*Existe-t-il un moyen tooignore une recommandation ?*

* Oui, consultez la section [Ignorer les recommandations](#ignore-recommendations) ci-dessus.

## <a name="next-steps"></a>Étapes suivantes
* [Rechercher des journaux](log-analytics-log-searches.md) tooview détaillées des données d’évaluation de SQL et les recommandations.
