---
title: "analyse d’aaaLog d’Azure CDN | Documents Microsoft"
description: "Le client peut activer l’analyse des journaux pour Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Journaux de diagnostic pour Azure CDN

Après avoir activé le CDN pour votre application, vous serez probablement choix de l’utilisation de toomonitor hello CDN, vérifier l’intégrité de hello de remise de votre et résoudre les problèmes potentiels. Azure CDN fournit ces fonctionnalités avec [l’Analytique principale CDN](cdn-analyze-usage-patterns.md) et les [journaux de diagnostic](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).

## <a name="cdn-core-analytics"></a>Analytique principale CDN
Comme un utilisateur d’Azure CDN actuel avec Verizon standard ou un profil de premium, vous êtes déjà analytique de noyaux tooview en mesure de dans le portail supplémentaire du hello accessible via l’option de « Gérer » hello de hello portail Azure. 

## <a name="azure-diagnostic-logs"></a>Journaux de diagnostic Azure

Avec cette nouvelle fonctionnalité, vous pouvez maintenant afficher l’analytique principale et l’enregistrer dans une ou plusieurs destinations, dont les suivantes :

 - Compte de Stockage Azure
 - Hubs d'événements Azure
 - [Référentiel OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 Cette fonctionnalité est disponible pour tous les points de terminaison CDN appartenant tooVerizon (Standard et Premium) et les profils du CDN Akamai (Standard).

Les journaux de diagnostic permettent de tooexport les métriques de l’utilisation de base à partir de votre CDN point de terminaison tooa de diverses sources afin que vous pouvez les utiliser de façon personnalisée. Par exemple, vous pouvez effectuer hello les types d’exportation de données suivants :

- Exporter le stockage des données tooblob, exporter tooCSV et générer des graphiques dans excel.
- Exporter des concentrateurs tooevent de données et mettre en corrélation avec des données provenant d’autres services azure.
- Exporter des données toolog analytique et afficher les données dans votre propre espace de travail OMS

Hello figure suivante montre une vue Analytique de noyaux CDN classique dans les données.

![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Figure 1 : vue avec l’analytique principale CDN*

Hello, procédure pas à pas passe par schéma hello de données analytique de hello core, les étapes impliquées dans l’activation de fonctionnalité de hello et leur remise toovarious destinations et la consommation de ces destinations.

## <a name="enable-logging-with-azure-portal"></a>Activation de la journalisation avec le portail Azure

> [!NOTE]
> Hello les journaux de diagnostic sont activés **hors** par défaut. 

Suivez les étapes de hello ci-après journalisation tooenable avec CDN Core Analytique :

Connectez-vous à toohello [portail Azure](http://portal.azure.com). Si vous n’avez pas activé CDN pour votre flux de travail, [activez Azure CDN](cdn-create-new-endpoint.md) avant de continuer.

1. Dans le portail de hello, accédez trop**profil CDN**.
2. Sélectionnez un profil CDN, puis sélectionnez le point de terminaison CDN hello que vous souhaitez tooenable **les journaux de diagnostic**.

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Accédez trop**les journaux de diagnostic** panneau sous **analyse** section, puis modifier le statut de hello trop**sur**.

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Activation de la journalisation avec Stockage Azure
    
journaux de hello toostore toouse le stockage Azure, sélectionnez **archiver le compte de stockage tooa**, sélectionnez les jours de rétention, puis cliquez sur **CoreAnalytics** sous **journal**.

![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Figure 2 : activation de la journalisation avec Stockage Azure*

### <a name="logging-with-oms-log-analytics"></a>Journalisation avec OMS Log Analytics

journaux de hello toostore toouse Analytique des journaux OMS, procédez comme suit :

1. À partir de hello **les journaux de diagnostic** panneau sous **analyse**, sélectionnez **envoyer tooLog Analytique** à partir de 

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Configurer l’enregistrement de journal Analytique de hello en cliquant sur Configurer. Vous accédez tooa la boîte de dialogue où vous pouvez sélectionner un espace de travail précédent ou créez-en un.

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Cliquez sur **Créer un espace de travail**.

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/07_Create-new.png)

4. Ensuite, vous devez sélectionner un nouveau nom d’espace de travail, un abonnement existant, un groupe de ressources (nouveau ou existant), un emplacement et un niveau tarifaire. Vous pouvez hello épinglage de ce tableau de bord de tooyour de configuration. Cliquez sur OK toocomplete hello configuration.

    Votre espace de travail doit ensuite apparaître, avec vos noms de groupe de ressources et d’espace de travail OMS. Les noms doivent être uniques et ne peuvent contenir que des lettres, des chiffres et des traits d’union. Les espaces et les traits de soulignement ne sont pas autorisés. 

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. Ensuite, vous obtenez un bref message indiquant que votre espace de travail a été créé et que vous retournez tooyour journalisation de l’écran de configuration. Vous pouvez vérifier le nom hello de votre espace de travail Analytique de journal.

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Une fois la configuration du journal Analytique hello, assurez-vous que vous également case hello CoreAnalytics pour la journalisation du CDN.

6. Si tout est tooyour convenance, cliquez sur hello **enregistrer** bouton en haut de hello de boîte de dialogue de configuration hello.

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/10_Save-me.png)

    Hello **enregistrer** bouton n’est plus actif et que hello/désactiver le bouton est désormais ON mais bleu au lieu de violet.

7. Si vous souhaitez toosee votre nouvel espace de travail OMS, accédez tooyour portail Azure tableau de bord, cliquez sur nom hello votre espace de travail Analytique de journal. Ensuite, vous verrez votre espace de travail (Assurez-vous qu’espace de travail OMS est mis en surbrillance sur hello gauche). Cliquez sur hello portail OMS vignette toosee votre espace de travail dans le référentiel d’OMS hello. 

    ![Portail - Journaux de diagnostics](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    Votre référentiel OMS est maintenant prêt toolog données. Dans commande tooconsume que les données, vous devez utiliser un [Solution OMS](#consuming-oms-log-analytics-data), couvert plus loin dans cet article.

Vous trouverez plus d’informations sur les retards des données de journal [ici](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>Activation de la journalisation avec PowerShell

Voici un exemple sur la façon dont les journaux de Diagnostic tooenable et get via hello applets de commande PowerShell Azure.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Activation des journaux de diagnostic dans un compte de stockage

Commencez par vous connecter et sélectionner un abonnement :

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


tooEnable journaux de Diagnostic dans un compte de stockage, utilisez cette commande :

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable des journaux de Diagnostics dans un espace de travail OMS, utilisez cette commande :

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Utilisation des journaux de diagnostic à partir de Stockage Azure
Cette section décrit le schéma hello d’analytique de noyaux hello CDN et comment elles sont organisées à l’intérieur d’un compte de stockage Azure et fournit les journaux de hello de toodownload code exemple dans un fichier CSV tooa.

### <a name="using-microsoft-azure-storage-explorer"></a>Utilisation de l’explorateur de stockage Microsoft Azure
Vous pouvez accéder aux hello core analytique données hello compte de stockage Azure, vous devez tout d’abord un contenu de hello outil tooaccess dans un compte de stockage. Lorsqu’il existe plusieurs outils disponibles dans le marché de hello, hello un que nous recommandons est hello Microsoft Azure Storage Explorer. Vous pouvez télécharger hello à partir [ici](http://storageexplorer.com/). Une fois le téléchargement et l’installation des logiciels de hello, configurez-le toouse hello même compte de stockage Azure qui a été configuré comme un toohello destination CDN les journaux de diagnostic.

1.  Ouvrez **l’explorateur de stockage Microsoft Azure**
2.  Recherchez le compte de stockage hello
3.  Accédez toohello **« Conteneurs d’objets Blob »** nœud sous stockage de ce compte et développez le nœud de hello
4.  Conteneur de sélection hello nommé **« insights-journaux coreanalytics »** et double-cliquez dessus
5.  Afficher les résultats sur hello volet de droite en commençant avec hello premier niveau, qui ressemble à **« resourceId = «**. Continuez de cliquer sur tous les moyen de hello jusqu'à ce que vous voyez hello fichier **PT1H.json**. Consultez hello Remarque pour une explication du chemin d’accès hello suivante.
6.  Chaque objet blob **PT1H.json** représente hello journaux d’analytique pendant une heure pour un point de terminaison CDN spécifique ou de son domaine personnalisé.
7.  schéma de Hello du contenu hello de ce fichier JSON est décrit dans la section hello schéma Hello Core, Analytique des journaux


> [!NOTE]
> **Format du chemin d’accès des objets blob**
> 
> Les journaux Core Analytics sont générés toutes les heures. Toutes les données pendant une heure sont collectées et stockées à l’intérieur d’un objet blob Azure en tant que charge utile JSON. chemin d’accès de Hello toothis objets Blob Azure apparaît comme s’il est une structure hiérarchique. Étant donné que l’outil Explorateur de stockage hello interprète « / » comme séparateur de répertoires, affiche la hiérarchie de hello pour des raisons pratiques. En fait, chemin d’accès complet de hello représente simplement des nom d’objet blob hello. Ce nom d’objet blob de hello suit hello respectent les conventions d’affectation de noms 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Description des champs :**

|value|description|
|-------|---------|
|Identifiant d’abonnement    |ID de hello abonnement Azure. Il est au format de Guid hello.|
|Ressource |Nom de groupe de ressources du CDN hello toowhich groupe de ressources hello appartient.|
|Nom de profil |Nom de hello profil CDN|
|Nom du point de terminaison |Nom du point de terminaison CDN de hello|
|Year|  représentation sous forme de 4 chiffres de l’année hello 2017, par exemple,|
|Mois| représentation sous forme de 2 chiffres du numéro du mois hello. 01 = Janvier ... 12 = Décembre|
|jour|   représentation sous forme de 2 chiffres de la journée hello du mois de hello|
|PT1H.json| Fichier JSON réel où sont stockées les données d’analytique hello|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Exportation de données Analytique de noyaux de hello tooa fichier CSV

toomake informatique tooaccess facile hello Core Analytique, nous fournissons un exemple de code pour un outil qui permet de télécharger les fichiers JSON hello au format de fichier de plat séparées par des virgules, qui peut être utilisé tooeasily créer des graphiques ou autres agrégations.

Voici comment vous pouvez utiliser l’outil de hello :

1.  Lien de github hello : [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Télécharger le code de hello
3.  Suivez les instructions toocompile et configurer
4.  Exécutez l’outil de hello
5.  Fichier CSV résultant affiche les données d’analytique hello dans une hiérarchie de plate simple.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Utilisation des journaux de diagnostics à partir d’un référentiel OMS Log Analytics
Analytique de journal est un service dans Operations Management Suite (OMS) qui surveille votre toomaintain environnements locaux et cloud leur disponibilité et les performances. Il collecte les données générées par les ressources dans vos environnements locaux et cloud et à partir d’autres analyses de tooprovide outils analyse à plusieurs sources. 

toouse Analytique de journal, vous devez [activer la journalisation](#enable-logging-with-azure-storage) référentiel toohello Analytique de journal Azure OMS, qui est décrite plus haut dans cet article.

### <a name="using-hello-oms-repository"></a>À l’aide de hello référentiel OMS

 Hello suivant schéma montre l’architecture hello d’entrées de hello et les sorties de référentiel de hello :

![Référentiel OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Figure 3 : référentiel OMS Log Analytics*

Vous pouvez afficher les données de salutation de manières différentes à l’aide de Solutions de gestion. Vous pouvez obtenir des Solutions de gestion à partir de hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Vous pouvez installer des solutions de gestion à partir d’Azure marketplace en cliquant sur hello **maintenant** lien en bas de hello de chaque solution.

### <a name="adding-an-oms-cdn-management-solution"></a>Ajout d’une solution de gestion CDN d’OMS

Suivez ces étapes de tooadd une Solution de gestion :

1.   Si vous n’avez pas déjà fait, connectez-vous toohello portail Azure à l’aide de votre abonnement Azure et accédez tooyour du tableau de bord.
    ![Tableau de bord Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. Bonjour **nouveau** panneau sous **Marketplace**, sélectionnez **analyse + gestion**.

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. Bonjour **analyse + gestion** panneau, cliquez sur **afficher tous les**.

    ![Afficher tout](./media/cdn-diagnostics-log/15_See-all.png)

4.  Recherchez le CDN dans la zone de recherche hello.

    ![Afficher tout](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Sélectionnez **Analytique principale Azure CDN**. 

    ![Afficher tout](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  Après avoir cliqué sur **créer**, vous serez invité toocreate un espace de travail OMS ou utilisez-en un existant. 

    ![Afficher tout](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Sélectionnez l’espace de travail hello créé avant. Vous devez ensuite tooadd un compte automation.

    ![Afficher tout](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Hello d’écran suivante affiche hello automation compte formulaire que vous devez remplir. 

    ![Afficher tout](./media/cdn-diagnostics-log/20_Automation.png)

9. Une fois que vous avez créé le compte d’automatisation hello, vous êtes prêt tooadd votre solution. Cliquez sur hello **créer** bouton.

    ![Afficher tout](./media/cdn-diagnostics-log/21_Ready.png)

10. Espace de travail tooyour a maintenant été ajoutée à votre solution. Revenir en arrière tooyour du tableau de bord de portail Azure.

    ![Afficher tout](./media/cdn-diagnostics-log/22_Dashboard.png)

    Cliquez sur hello Analytique de journal espace de travail créé toogo tooyour espace de travail. 

11. Cliquez sur hello **portail OMS** vignette toosee votre nouvelle solution dans le portail OMS est hello.

    ![Afficher tout](./media/cdn-diagnostics-log/23_workspace.png)

12. Votre portail OMS doit maintenant ressembler à hello suivant d’écran :

    ![Afficher tout](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Cliquez sur une de hello vignettes toosee plusieurs vues de vos données.

    ![Afficher tout](./media/cdn-diagnostics-log/25_Interior-view.png)

    Vous pouvez faire défiler à gauche ou droite toosee davantage les vignettes représentant des vues dans les données de salutation. 

    En cliquant sur une des vignettes de hello vous donne plus de détails sur vos données.

     ![Afficher tout](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Offres et niveaux tarifaires

Vous pouvez voir des offres et des niveaux tarifaires pour les solutions de gestion OMS [ici](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Personnalisation des vues

Vous pouvez personnaliser hello afficher vos données à l’aide de hello **Concepteur de vue**. Atteindre l’espace de travail OMS tooyour et commencez à créer en cliquant sur hello **Concepteur de vue** vignette.

![Concepteur de vues](./media/cdn-diagnostics-log/27_Designer.png)

Vous pouvez faire glisser et supprimer les types de graphiques de hello gauche et renseignez hello données détails tooanalyze sur hello gauche.

![Concepteur de vues](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Retards des données de journal

Retards des données de journal Verizon | Retards des données de journal Akamai
--- | ---
Les données de journal Verizon sont retardées de 1 heure et prennent toostart d’heures too2 qui apparaissent après l’achèvement de la propagation de point de terminaison. | Les données de journal Akamai sont retardées de 24 heures et occupe toostart d’heures too2 apparaissant si elle a été créé il y a plus de 24 heures. Si elle a été créé récemment, peut prendre des heures de too25 pour toostart de journaux hello qui apparaissent.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>Types de journaux de diagnostic pour l’analytique principale CDN

Nous proposons actuellement uniquement Core Analytique des journaux, qui contiennent des métriques affichant les statistiques de réponse HTTP et sortie comme hello CDN POP/bords.

### <a name="core-analytics-metrics-details"></a>Détails des métriques de Core Analytics
Hello tableau suivant affiche une liste des mesures disponibles dans hello que Core Analytique se connecte. Toutes les métriques ne sont pas disponibles auprès tous les fournisseurs, même si ces différences sont minimes. Hello tableau suivant également indique si une mesure donnée est disponible à partir d’un fournisseur. Veuillez noter que les métriques de hello sont disponibles pour uniquement ces points de terminaison CDN que le trafic sur ces derniers.


|Mesure                     | Description   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |Nombre total d’occurrences de requêtes pendant cette période| Oui  |Oui   |
| RequestCountHttpStatus2xx |Nombre de toutes les requêtes qui ont abouti à un code 2xx (par ex. 200, 202)              | Oui  |Oui   |
| RequestCountHttpStatus3xx | Nombre de toutes les requêtes qui ont abouti à un code 3xx (par ex. 300, 302)              | Oui  |Oui   |
| RequestCountHttpStatus4xx |Nombre de toutes les requêtes qui ont abouti à un code 4xx (par ex. 400, 404)               | Oui   |Oui   |
| RequestCountHttpStatus5xx | Nombre de toutes les requêtes qui ont abouti à un code 5xx (par ex. 500, 504)              | Oui  |Oui   |
| RequestCountHttpStatusOthers |  Nombre d’occurrences de tous les autres codes HTTP (en dehors de 2xx-5xx) | Oui  |Oui   |
| RequestCountHttpStatus200 | Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 200              |Non   |Oui   |
| RequestCountHttpStatus206 | Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 206              |Non   |Oui   |
| RequestCountHttpStatus302 | Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 302              |Non   |Oui   |
| RequestCountHttpStatus304 |  Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 304             |Non   |Oui   |
| RequestCountHttpStatus404 | Nombre de toutes les requêtes qui ont abouti au code de réponse HTTP 404              |Non   |Oui   |
| RequestCountCacheHit |Nombre de toutes les requêtes qui ont abouti à un accès au cache. Cela signifie que les actifs hello honorée directement à partir de hello POP toohello Client.               | Oui  |Non   |
| RequestCountCacheMiss | Nombre de toutes les requêtes qui ont abouti à un échec de cache. Cela signifie que les biens de hello sont introuvable sur le client de toohello hello POP le plus proche et par conséquent, a été récupéré à partir de l’origine de hello.              |Oui   | Non  |
| RequestCountCacheNoCache | Nombre de toutes les demandes tooan actifs qui ne peuvent pas être mis en cache en raison de la configuration de l’utilisateur tooa sur les bords de hello.              |Oui   | Non  |
| RequestCountCacheUncacheable | Nombre total de demandes tooassets ne peuvent pas être mis en cache par Cache-Control l’élément multimédia hello et en-têtes, ce qui indiquent qu’il ne doit pas être mis en cache sur un POP ou hello HTTP client arrive à expiration                |Oui   |Non   |
| RequestCountCacheOthers | Nombre de toutes les requêtes avec un état du cache non traité ci-dessus.              |Oui   | Non  |
| EgressTotal | Transfert de données sortantes en Go              |Oui   |Oui   |
| EgressHttpStatus2xx | Transfert de données sortantes * pour les réponses avec des codes d’état HTTP 2xx en Go            |Oui   |Non   |
| EgressHttpStatus3xx | Transfert de données sortantes pour les réponses avec des codes d’état HTTP 3xx en Go              |Oui   |Non   |
| EgressHttpStatus4xx | Transfert de données sortantes pour les réponses avec des codes d’état HTTP 4xx en Go               |Oui   | Non  |
| EgressHttpStatus5xx | Transfert de données sortantes pour les réponses avec des codes d’état HTTP 5xx en Go               |Oui   |  Non |
| EgressHttpStatusOthers | Transfert de données sortantes pour les réponses avec d’autres codes d’état HTTP en Go                |Oui   |Non   |
| EgressCacheHit |  Transfert de données sortantes pour les réponses qui ont été remis directement à partir du cache CDN hello sur hello CDN POP/bords  |Oui   |  Non |
| EgressCacheMiss | Transfert de données sortantes pour les réponses qui ont été pas été trouvées sur hello plus proche du serveur POP et récupérées à partir du serveur d’origine hello              |Oui   |  Non |
| EgressCacheNoCache | Transfert de données sortantes pour les ressources qui ne peuvent pas être mis en cache en raison de la configuration de l’utilisateur tooa sur les bords de hello.                |Oui   |Non   |
| EgressCacheUncacheable | Transfert de données sortantes pour les ressources qui ne peuvent pas être mis en cache par l’élément multimédia hello Cache-Control et/ou en-têtes expire, ce qui indiquent qu’il ne doit pas être mis en cache sur un POP ou hello HTTP client                    |Oui   | Non  |
| EgressCacheOthers |  Transfère les données sortantes pour d’autres scénarios de cache.             |Oui   | Non  |

* Transfert de données sortant fait référence tootraffic remis à partir du client de toohello serveurs serveur POP du CDN.


### <a name="schema-of-hello-core-analytics-logs"></a>Schéma de hello Core, Analytique des journaux 

Tous les journaux sont stockés au format JSON, et chaque entrée comporte des champs de chaîne suivant hello schéma ci-dessous :

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

Où « temps de hello » représente hello heure de début de limite d’heure hello pour laquelle les statistiques hello sont signalée. Quand une métrique n’est pas prise en charge par un fournisseur CDN, il y a une valeur null au lieu d’un entier ou d’un double. Cette valeur null indique l’absence de hello d’une mesure, et il diffère de la valeur 0. Notez également qu’il y aura un ensemble de ces mesures par domaine configuré sur le point de terminaison hello.

Exemple de propriétés ci-dessous :

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>Ressources supplémentaires

* [Journaux de diagnostic Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Core Analytics via le portail supplémentaire Azure CDN](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Azure OMS Log Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [API REST Azure Log Analytics](https://docs.microsoft.com/en-us/rest/api/loganalytics)







