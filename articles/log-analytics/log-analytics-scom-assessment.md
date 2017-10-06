---
title: aaaOptimize votre environnement de System Center Operations Manager avec Analytique de journal Azure | Documents Microsoft
description: "Vous pouvez utiliser hello System Center Operations Manager évaluation solution tooassess hello des risques et l’intégrité de vos environnements de serveurs selon un intervalle régulier."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>Optimiser votre environnement avec hello solution de System Center Operations Manager évaluation (version préliminaire)

![Symbole de System Center Operations Manager Assessment](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

Vous pouvez utiliser hello System Center Operations Manager évaluation solution tooassess hello des risques et l’intégrité de vos environnements de serveur System Center Operations Manager sur un intervalle régulier. Cet article vous aide à installer, configurer et utiliser la solution de hello afin que vous puissiez prendre les actions correctives relatives à des problèmes potentiels.

Cette solution fournit une liste hiérarchisée de l’infrastructure de serveurs déployée recommandations tooyour spécifique. les recommandations de Hello sont réparties en focus quatre zones, qui vous permettent de rapidement comprennent hello risque et l’action corrective.

Hello recommandations sont basées sur les connaissances de hello et l’expérience acquises par les ingénieurs de Microsoft de milliers de visiteurs. Chaque recommandation explique pourquoi le problème peut concerner tooyou et comment les modifications suggérées tooimplement hello.

Vous pouvez choisir les domaines les plus importantes tooyour organisation et suivre votre progression vers un environnement sans risque et intègre.

Une fois que vous avez ajouté des solutions de hello et une évaluation est terminée, le résumé des informations pour les domaines d’intérêt s’affiche sur hello **System Center Operations Manager évaluation** tableau de bord pour votre infrastructure. Hello sections suivantes décrivent comment toouse hello plus d’informations sur hello **System Center Operations Manager évaluation** tableau de bord, où vous pouvez afficher et prenez les actions recommandées pour votre infrastructure SCOM.

![Mosaïque de la solution System Center Operations Manager](./media/log-analytics-scom-assessment/scom-tile.png)

![Tableau de bord System Center Operations Manager Assessment](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>L’installation et la configuration de solution de hello

solution de Hello fonctionne avec le système de Microsoft Operations Manager 2012 R2 et 2012 SP1.

Utilisez hello suivant tooinstall des informations et configurer une solution de hello.

 - Avant de pouvoir utiliser une solution d’évaluation dans OMS, vous devez avoir installé de solution de hello. Installer la solution hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) ou en suivant les instructions de hello dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).

 - Après l’ajout d’espace de travail toohello de solution hello, vignette de System Center Operations Manager évaluation hello sur le tableau de bord hello affiche le message de salutation une configuration supplémentaire requise. Cliquez sur la vignette de hello et suivez les étapes de configuration hello mentionnés dans la page de hello

 ![Mosaïque du tableau de bord System Center Operations Manager](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Configuration de hello System Center Operations Manager peut être effectuée via un script de hello en suivant les étapes de hello mentionnés dans la page de configuration hello de solution hello dans OMS.

 Au lieu de cela, évaluation de hello tooconfigure via la Console SCOM, hello suivez ci-dessous les étapes Bonjour même ordre
1. [Définir le compte d’identification hello pour System Center Operations Manager évaluation](#operations-manager-run-as-accounts-for-oms)  
2. [Configurer la règle de System Center Operations Manager évaluation hello](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>Détails de l’évaluation de la collecte de données System Center Operations Manager

Hello d’évaluation de System Center Operations Manager collecte des données WMI, données de Registre, les données de journal des événements, données d’Operations Manager via Windows PowerShell, les requêtes SQL, collecteur d’informations de fichier à l’aide de serveur hello que vous avez activés.

Hello tableau suivant indique les méthodes de collecte de données de System Center Operations Manager évaluation et la fréquence des données sont collectées par un agent.

| plateforme | Agent direct | Agent SCOM | Stockage Azure | SCOM requis ? | Données de l’agent SCOM envoyées via un groupe d’administration | fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | sept jours |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Comptes d’identification Operations Manager pour OMS

OMS s’appuie sur les packs d’administration pour les charges de travail tooprovide services à valeur ajoutée. Chaque charge de travail requiert des packs d’administration de toorun des privilèges spécifiques de la charge de travail dans un contexte de sécurité différent, tel qu’un compte de domaine. Configurer une identification Operations Manager compte tooprovide informations d’identification.

Utilisez hello tooset hello compte d’identification Operations Manager pour System Center Operations Manager évaluation des informations suivantes.

### <a name="set-hello-run-as-account"></a>Ensemble hello compte d’identification

1. Bonjour Console Operations Manager, accédez à toohello **Administration** onglet.
2. Sous hello **Configuration d’identification**, cliquez sur **comptes**.
3. Créer hello compte d’identification, par hello Assistant Création d’un compte Windows. Hello compte toouse est hello celui identifié et avoir toutes les conditions préalables hello ci-dessous :

    >[!NOTE]
    Hello compte Exécuter en tant que doive respecter les conditions suivantes :
    - Un membre du compte de domaine de hello groupe Administrateurs local sur tous les serveurs dans l’environnement hello (toutes les opérations de gestionnaire de rôles - serveur d’administration, de la base de données Operations Manager, entrepôt de données, Reporting, Console Web, passerelle)
    - Rôle administrateur d’opération pour le groupe d’administration hello en cours d’évaluation
    - Exécutez hello [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) compte de toohello toogrant autorisations granulaires sur l’instance SQL utilisé par Operations Manager.
      Remarque : Si ce compte dispose déjà des droits d’administrateur système, puis passez l’exécution du script hello.

4. Sous **Sécurité de la distribution**, sélectionnez **Plus sécurisé**.
5. Spécifiez le serveur d’administration hello où le compte de hello est distribué.
3. Revenir en arrière toohello Configuration d’identification et cliquez sur **profils**.
4. Recherchez hello *profil d’évaluation de SCOM*.
5. nom du profil Hello doit être : *Microsoft System Center Advisor SCOM évaluation profil d’identification*.
6. Avec le bouton droit et mettre à jour ses propriétés et ajouter hello récemment créé le compte d’identification créé à l’étape 3.

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>SQL script toogrant autorisations granulaires toohello compte d’identification

Exécutez hello suivant SQL script toogrant requis autorisations toohello compte d’identification sur l’instance SQL hello utilisé par Operations Manager.

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>Configurer la règle d’évaluation hello

Hello System Center Operations Manager évaluation Pack d’administration de la solution comprend une règle nommée *Microsoft System Center Advisor SCOM évaluation exécuter évaluation règle*. Cette règle est responsable de l’évaluation de hello en cours d’exécution. tooenable hello règle et configurer la fréquence de hello, utiliser des procédures hello ci-dessous.

Par défaut, hello Microsoft System Center Advisor SCOM évaluation exécuter évaluation la règle est désactivée. évaluation de hello toorun, vous devez activer règle hello sur un serveur d’administration. Utilisez hello comme suit.

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>Active la règle de hello pour un serveur d’administration spécifique

1. Bonjour **création** espace de travail de la console Operations Manager hello, recherchez la règle de hello *Microsoft System Center Advisor SCOM évaluation exécuter évaluation règle* Bonjour **règles** volet.
2. Dans les résultats de recherche hello, sélectionnez hello qui inclut le texte hello *Type : serveur d’administration*.
3. Avec le bouton droit de la règle de hello, puis cliquez sur **substitue** > **pour un objet spécifique de la classe : serveur d’administration**.
4.  Dans la liste des serveurs d’administration disponibles hello, sélectionnez serveur d’administration hello où la règle de hello doit s’exécuter.
5.  Assurez-vous de modifier la valeur de remplacement trop**True** pour hello **activé** la valeur du paramètre.  
    ![paramètre de substitution](./media/log-analytics-scom-assessment/rule.png)

Dans cette fenêtre, configurez la fréquence hello Hello exécutés à l’aide de la procédure suivante de hello.

#### <a name="configure-hello-run-frequency"></a>Configurer la fréquence de hello exécuter

l’évaluation de Hello est intervalle par défaut de hello toorun configuré chaque 10 080 minutes (ou sept jours). Vous pouvez remplacer la valeur minimale de tooa valeur hello de 1 440 minutes (ou un jour). la valeur de Hello représente l’intervalle de temps minimal hello requis entre les exécutions d’évaluation successives. intervalle de salutation toooverride, utilisez hello suit.

1. Bonjour **création** espace de travail de la console Operations Manager hello, recherchez la règle de hello *Microsoft System Center Advisor SCOM évaluation exécuter évaluation règle* Bonjour **règles** volet.
2. Dans les résultats de recherche hello, sélectionnez hello qui inclut le texte hello *Type : serveur d’administration*.
3. Avec le bouton droit de la règle de hello, puis cliquez sur **hello de remplacement de règle** > **pour tous les objets de classe : serveur d’administration**.
4. Hello de modification **intervalle** tooyour de valeur de paramètre souhaité de la valeur d’intervalle. Dans l’exemple hello ci-dessous, hello a la valeur too1440 minutes (1 jour).  
    ![paramètre d’intervalle](./media/log-analytics-scom-assessment/interval.png)  
    Si hello a la valeur accessible sans 1 440 minutes, la règle de hello s’exécute selon un intervalle d’une journée. Dans cet exemple, règle de hello ignore la valeur d’intervalle hello et s’exécute à la fréquence d’un jour.


## <a name="understanding-how-recommendations-are-prioritized"></a>Hiérarchisation des recommandations

Chaque recommandation reçoit une valeur de pondération qui identifie l’importance relative de hello de hello. Recommandations les plus importantes uniquement hello 10 sont affichées.

### <a name="how-weights-are-calculated"></a>Calcul des pondérations

Les pondérations sont des agrégations de valeurs basées sur trois facteurs clés :

- Hello *probabilité* qu’une anomalie identifiée cause des problèmes. Une plus grande probabilité attribue des tooa un score global supérieur pour la recommandation de hello.
- Hello *impact* du problème hello sur votre organisation si elle devait causer un problème. Un plus grand impact attribue tooa un score global supérieur pour la recommandation de hello.
- Hello *effort* requis recommandation de hello tooimplement. Un plus grand effort attribue tooa un score global inférieur pour la recommandation de hello.

Hello pondération de chaque recommandation est exprimée en pourcentage du score total de hello disponibles pour chaque domaine d’intérêt. Par exemple, si une recommandation dans hello domaine de la disponibilité et continuité des activités a un score de 5 %, l’implémentation de cette recommandation augmente votre global score 5 % de disponibilité et continuité d’activité.

### <a name="focus-areas"></a>Domaines

**Disponibilité et continuité d’activité** : ce domaine présente les recommandations relatives à la disponibilité du service, la résilience de votre infrastructure et la protection de votre activité.

**Performances et évolutivité** -cette zone de focus indique toohelp de recommandations de votre organisation informatique croissance, assurez-vous que votre environnement informatique répond aux exigences de performances actuelles et qu’il est en mesure de toorespond toochanging infrastructure a besoin.

**Mise à niveau, Migration et déploiement** - cette zone de focus indique toohelp recommandations vous mettez à niveau, migrer et déployer l’infrastructure existante de SQL Server tooyour.

**Opérations et surveillance** - cette zone de focus indique recommandations toohelp rationaliser vos opérations informatiques, mettre en œuvre de maintenance préventive et optimiser les performances.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Faut-il viser tooscore 100 % dans chaque domaine ?

Pas nécessairement. recommandations de Hello sont basées sur la base de connaissances hello et l’expérience acquises par les ingénieurs de Microsoft sur des milliers de visiteurs. Toutefois, aucune chaque infrastructure de serveur n’est même hello et certaines recommandations peuvent être plus ou moins pertinente tooyou. Par exemple, certaines recommandations de sécurité peuvent être moins appropriées si vos ordinateurs virtuels ne sont pas exposé toohello Internet. Certaines recommandations de disponibilité peuvent être moins pertinentes pour les services qui fournissent des rapports et des données ad hoc de faible priorité. Les problèmes entreprise tooa important peuvent être moins important tooa démarrage. Vous pouvez souhaitez tooidentify les domaines d’intérêt figurant parmi vos priorités et puis d’observer comment vos résultats changent au fil du temps.

Chaque recommandation inclut une justification de son importance. Utilisez cette tooevaluate conseils si la mise en œuvre hello recommandation vous convient, étant donné la nature hello de vos besoins informatiques hello et les services professionnels de votre organisation.

## <a name="use-assessment-focus-area-recommendations"></a>Utilisation des recommandations des domaines d'évaluation

Avant de pouvoir utiliser une solution d’évaluation dans OMS, vous devez avoir installé de solution de hello. tooread savoir plus sur l’installation de solutions, consultez [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md). Après son installation, vous pouvez afficher le résumé hello des recommandations à l’aide de la vignette de System Center Operations Manager évaluation hello sur la page de vue d’ensemble de hello dans OMS.

Hello d’affichage résumés des évaluations de conformité pour votre infrastructure, puis Explorez les recommandations.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recommandations tooview pour un focus zone et prendre une action corrective

1. Sur hello **vue d’ensemble** , cliquez sur hello **System Center Operations Manager évaluation** vignette.
2. Sur hello **System Center Operations Manager évaluation** , examinez les informations de résumé hello dans un des panneaux de domaine hello, puis cliquez sur une recommandations de tooview d’intérêt.
3. Sur les pages de zone de focus hello, vous pouvez afficher les recommandations hello hiérarchisé pour votre environnement. Cliquez sur une recommandation sous **objets affectés** tooview plus de détails sur pourquoi hello recommandation est faite.  
    ![domaine](./media/log-analytics-scom-assessment/focus-area.png)
4. Vous pouvez effectuer les actions correctives suggérées dans **Actions suggérées**. Lorsque l’élément de hello a été traité, évaluations ultérieures indiqueront les actions ont été prises et votre score de conformité augmentera qu’enregistre. Les éléments corrigés apparaissent comme **objets passés**.

## <a name="ignore-recommendations"></a>Ignorer les recommandations

Si vous avez des recommandations que vous souhaitez tooignore, vous pouvez créer un fichier texte qui OMS utilise tooprevent des recommandations d’apparaître dans les résultats d’évaluation.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>recommandations tooidentify que vous souhaitez tooignore

1. Connectez-vous à tooyour espace de travail et ouvrez recherche de journal. Utilisez hello requête toolist recommandations ayant échoué pour les ordinateurs de votre environnement.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    Voici une requête de recherche de journal de capture d’écran montrant hello :  
    ![recherche dans les journaux](./media/log-analytics-scom-assessment/scom-log-search.png)

2. Choisissez les recommandations que vous souhaitez tooignore. Vous utiliserez les valeurs hello pour RecommendationId dans la procédure suivante de hello.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate et utilisez un fichier texte IgnoreRecommendations.txt

1. Créez un fichier nommé IgnoreRecommendations.txt.
2. Collez ou tapez chaque RecommendationId de chaque recommandation que vous souhaitez tooignore OMS sur une ligne distincte, puis enregistrez et fermez le fichier de hello.
3. Fichier PUT hello Bonjour suivant du dossier sur chaque ordinateur où vous souhaitez les recommandations de tooignore OMS.
4. Sur le serveur d’administration Operations Manager de hello - *lecteur_système*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que les recommandations sont ignorées.

1. Après l’exécution de hello prochaine évaluation planifiée, par défaut, tous les sept jours, hello spécifié recommandations sont marquées comme étant des ignorées et n’apparaissent pas dans le tableau de bord évaluation hello.
2. Vous pouvez utiliser hello suivant toolist de requêtes de recherche de journal de toutes les recommandations hello ignoré.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. Si vous décidez ultérieurement que vous souhaitez les recommandations toosee ignorée, supprimez tous les fichiers IgnoreRecommendations.txt ou vous supprimez des RecommendationIDs dans les.

## <a name="system-center-operations-manager-assessment-solution-faq"></a>FAQ sur la solution System Center Operations Manager Assessment

*J’ai ajouté d’espace de travail hello évaluation solution toomy OMS. Mais je ne vois pas les recommandations hello. Pourquoi ?* Après avoir ajouté la solution de hello, utilisez hello suivant les étapes vue hello recommandations de tableau de bord OMS hello.  

- [Définir le compte d’identification hello pour System Center Operations Manager évaluation](#operations-manager-run-as-accounts-for-oms)  
- [Configurer la règle de System Center Operations Manager évaluation hello](#configure-the-assessment-rule)


*Existe-t-il un tooconfigure moyen la fréquence d’exécution des évaluations de hello ?* Oui. Consultez [hello configurer fréquence d’exécution](#configure-the-run-frequency).

*Si un autre serveur est découvert après que j’ai ajouté des solutions de System Center Operations Manager évaluation hello, est-il évalué ?* Oui, après la découverte, il sera évalué ; par défaut, tous les sept jours.

*Qu’est le nom de hello du processus hello hello collecte des données ?* AdvisorAssessment.exe

*Où le processus de AdvisorAssessment.exe hello est exécuté ?* AdvisorAssessment.exe s’exécute sous hello HealthService hello du serveur d’administration où les règles d’évaluation hello est activé. À l’aide de ce processus, la découverte de l’ensemble de votre environnement s’effectue par le biais de la collecte de données distante.

*Combien de temps la collecte de données prend-elle ?* Collecte de données sur le serveur de hello prend environ une heure. Elle peut prendre plus de temps dans les environnements comportant plusieurs bases de données ou instances d’Operations Manager.

*Que se passe-t-il si j’ai défini intervalle hello accessible sans évaluation de hello à 1 440 minutes ?*  évaluation de hello est préconfigurée de manière toorun au maximum une fois par jour. Si vous substituez valeur tooa valeur hello intervalle inférieur à 1 440 minutes, évaluation de hello utilise 1 440 minutes comme valeur d’intervalle hello.

*Comment tooknow s’il existe des défaillances préalables ?* Si l’exécution de l’évaluation de hello et vous ne voyez les résultats, il est probable que certaines des conditions préalables pour l’évaluation de hello hello a échoué. Vous pouvez exécuter des requêtes : `Type=Operation Solution=SCOMAssessment` et `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` hello toosee de recherche de journal a échoué conditions préalables.

*Il y a un message `Failed tooconnect toohello SQL Instance (….).` dans les échecs liés aux conditions préalables. Quel est le problème de hello ?* AdvisorAssessment.exe, processus hello qui collecte les données, s’exécute sous hello HealthService hello du serveur d’administration. Dans le cadre de l’évaluation de hello, processus de hello tentatives tooconnect toohello SQL Server où la base de données Operations Manager hello est présent. Cette erreur peut se produire lorsque les règles de pare-feu bloquent l’instance de SQL Server toohello hello connexion.

*Le type de données est collecté ?*  hello les types de données suivants est collecté : données d’Operations Manager : des données WMI : registre données - EventLog - via Windows PowerShell, les requêtes SQL et les fichiers collecteur d’informations.

*Pourquoi dois-je tooconfigure un compte d’identification ?* Plusieurs requêtes SQL sont exécutées pour un serveur Operations Manager. Pour qu’ils toorun, vous devez utiliser un compte d’identification avec les autorisations nécessaires. En outre, les informations d’identification d’administrateur local sont requis tooquery WMI.

*Pourquoi afficher uniquement hello 10 premières recommandations ?* Au lieu d’exploiter une liste exhaustive et écrasante de tâches, nous vous recommandons de vous concentrer sur les recommandations hello classés par priorité. Une fois que vous les aurez suivies, de nouvelles recommandations apparaîtront. Si vous préférez liste détaillée de hello toosee, vous pouvez afficher toutes les recommandations à l’aide de la recherche de journal.

*Existe-t-il un moyen tooignore une recommandation ?* Oui, voir hello [ignorer des recommandations](#Ignore-recommendations).


## <a name="next-steps"></a>Étapes suivantes

- [Rechercher des journaux](log-analytics-log-searches.md) tooview détaillées des données d’évaluation de System Center Operations Manager et les recommandations.
