---
title: "Sorties Stream Analytics : options de stockage et d’analyse | Microsoft Docs"
description: "Découvrez les options de sorties de données Stream Analytics, notamment Power BI pour les résultats de l’analyse."
keywords: "transformation de données, résultats d’analyse, options de stockage de données"
services: stream-analytics,documentdb,sql-database,event-hubs,service-bus,storage
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ba6697ac-e90f-4be3-bafd-5cfcf4bd8f1f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 99f8113f0464960e898293397fbe3de90d669857
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-outputs-options-for-storage-analysis"></a>Sorties Stream Analytics : options de stockage, d’analyse
Lorsque vous créez une tâche de flux de données Analytique, pensez comment les données résultantes hello seront consommées. Comment vous allez afficher des résultats de la tâche de flux de données Analytique hello hello et où vous stockerez il ?

Dans l’ordre tooenable divers modèles d’application, Azure flux Analytique a différentes options permettant de stocker la sortie et l’affichage des résultats de l’analyse. Cela rend la sortie des tâches tooview facile et vous offre la souplesse nécessaire la consommation hello et de stockage de la sortie de tâche hello pour l’entreposage des données et d’autres fins. Toute sortie configurée dans la tâche de hello doit exister pour que la tâche hello est démarrée et événements de début circuler. Par exemple, si vous utilisez le stockage d’objets Blob comme sortie, le travail de hello ne crée pas un compte de stockage automatiquement. Il doit toobe créé par l’utilisateur de hello avant le démarrage du travail ASA hello.

## <a name="azure-data-lake-store"></a>Azure Data Lake Store
Stream Analytics prend en charge [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/). Ce système de stockage vous permet de toostore les données de n’importe quelle vitesse de taille, de type et de réception pour l’analytique opérationnelle et exploratoire. En outre, flux de données Analytique besoins toobe autorisé tooaccess hello Data Lake Store. Plus d’informations sur l’autorisation et comment toosign pour hello Data Lake Store (le cas échéant) sont abordés dans hello [lac de données de sortie article](stream-analytics-data-lake-output.md).

### <a name="authorize-an-azure-data-lake-store"></a>Autoriser un Azure Data Lake Store
Lorsque le stockage de LAC de données est sélectionné comme sortie Bonjour portail Azure, vous seront demandée tooauthorize un magasin de LAC de données existant connexion tooan.  

![Autoriser Data Lake Store](./media/stream-analytics-define-outputs/06-stream-analytics-define-outputs.png)  

Puis remplissez les propriétés hello pour hello Data Lake Store est sortie comme indiqué ci-dessous :

![Autoriser Data Lake Store](./media/stream-analytics-define-outputs/07-stream-analytics-define-outputs.png)  

Hello ci-dessous répertorie les noms de propriété hello et leur description nécessaires pour créer une sortie Data Lake Store.

<table>
<tbody>
<tr>
<td><B>NOM DE LA PROPRIÉTÉ</B></td>
<td><B>DESCRIPTION</B></td>
</tr>
<tr>
<td>Alias de sortie</td>
<td>Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requête sortie toothis Data Lake Store.</td>
</tr>
<tr>
<td>Nom du compte</td>
<td>nom Hello Hello compte de stockage de LAC de données où vous envoyez votre sortie. Vous verrez une liste déroulante des comptes Data Lake Store toowhich hello consignés dans le portail de toohello a accès.</td>
</tr>
<tr>
<td>Séquence d’octets préfixe du chemin d’accès [<I>facultative</I>]</td>
<td>Hello toowrite de chemin d’accès du fichier vos fichiers au sein de hello spécifié le compte de magasin Data Lake. <BR>{date}, {time}<BR>Exemple 1 : dossier1/journaux/{date}/{heure}<BR>Exemple 2 : dossier1/journaux/{date}</td>
</tr>
<tr>
<td>Format de la date [<I>facultatif</I>]</td>
<td>Si le jeton de date hello est utilisé dans le chemin d’accès de hello préfixe, vous pouvez sélectionner le format de date hello dans lequel vos fichiers sont organisés. Exemple : JJ/MM/AAAA</td>
</tr>
<tr>
<td>Format de l’heure [<I>facultatif</I>]</td>
<td>Si le jeton de durée hello est utilisé dans le chemin d’accès de hello préfixe, spécifiez le format d’heure hello dans lequel vos fichiers sont organisés. Valeur de hello uniquement pris en charge actuellement est HH.</td>
</tr>
<tr>
<td>Format de sérialisation de l’événement</td>
<td>Format de sérialisation pour les données de sortie. JSON, CSV et Avro sont pris en charge.</td>
</tr>
<tr>
<td>Encodage</td>
<td>S’il s’agit du format CSV ou JSON, un encodage doit être spécifié. UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant.</td>
</tr>
<tr>
<td>Délimiteur</td>
<td>Applicable uniquement pour la sérialisation CSV. Stream Analytics prend en charge un certain nombre de délimiteurs communs pour sérialiser des données CSV. Valeurs prises en charge : virgule, point-virgule, espace, tabulation et barre verticale.</td>
</tr>
<tr>
<td>Format</td>
<td>Applicable uniquement pour la sérialisation JSON. Ligne séparée spécifie la sortie de hello sera formatée en par chaque objet JSON séparé par une nouvelle ligne. Le tableau spécifie que sortie de hello sera mise en forme en tant que tableau d’objets JSON.</td>
</tr>
</tbody>
</table>

### <a name="renew-data-lake-store-authorization"></a>Renouveler une autorisation Data Lake Store
Vous devez toore-authentifier votre compte Data Lake Store si son mot de passe a changé depuis la création ou de dernière authentification de votre travail.

![Autoriser Data Lake Store](./media/stream-analytics-define-outputs/08-stream-analytics-define-outputs.png)  

## <a name="sql-database"></a>Base de données SQL
[base de données SQL Azure](https://azure.microsoft.com/services/sql-database/) comme sortie pour les données relationnelles ou pour les applications qui dépendent de contenus hébergés dans une base de données relationnelle. Tâches de flux de données Analytique permet d’écrire tooan les table existante dans une base de données SQL Azure.  Notez que ce schéma de table hello doit correspondre exactement aux champs de hello et leurs types de sortie à partir de votre travail. Un [Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/) peut également être spécifié comme une sortie via hello de base de données SQL option de sortie ainsi (il s’agit d’une fonctionnalité en version préliminaire). Hello ci-dessous répertorie les noms de propriété hello et leur description pour la création d’une sortie de la base de données SQL.

| Nom de la propriété | Description |
| --- | --- |
| Alias de sortie |Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requêtes sortie toothis base de données. |
| Base de données |nom Hello de base de données hello où vous envoyez votre sortie. |
| Nom du serveur |nom du serveur de base de données SQL Hello |
| Nom d’utilisateur |nom d’utilisateur qui a la base de données access toowrite toohello de Hello |
| Mot de passe |base de données toohello Hello mot de passe tooconnect |
| Table |nom de la table Hello où écrire la sortie de hello. nom de la table Hello respecte la casse et schéma hello de cette table doit correspondre exactement toohello nombre de champs et leurs types générés par votre sortie de travail. |

> [!NOTE]
> Offre de base de données SQL Azure hello est actuellement pris en charge pour une sortie de tâche de flux de données Analytique. Toutefois, une machine virtuelle de Azure exécutant SQL Server avec une base de données associée n’est pas pris en charge. Il s’agit de toochange sujet dans les versions futures.
> 
> 

## <a name="blob-storage"></a>Stockage d'objets blob
Stockage d’objets BLOB offre une solution économique et évolutive pour stocker de grandes quantités de données non structurées dans le cloud de hello.  Pour une présentation de stockage d’objets Blob Azure et son utilisation, consultez documentation hello [comment les objets BLOB toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

Hello ci-dessous répertorie les noms de propriété hello et leur description pour la création d’une sortie de l’objet blob.

<table>
<tbody>
<tr>
<td>Nom de la propriété</td>
<td>Description</td>
</tr>
<tr>
<td>Alias de sortie</td>
<td>Il s’agit d’un nom convivial utilisé dans le stockage blob de requêtes toodirect hello requête sortie toothis.</td>
</tr>
<tr>
<td>Compte de stockage</td>
<td>nom Hello hello du compte de stockage où vous envoyez votre sortie.</td>
</tr>
<tr>
<td>Clé du compte de stockage</td>
<td>clé secrète de Hello associée au compte de stockage hello.</td>
</tr>
<tr>
<td>Conteneur de stockage</td>
<td>Les conteneurs fournissent un regroupement logique des objets BLOB stockés dans hello service Microsoft Azure Blob. Lorsque vous téléchargez un objet blob de toohello service Blob, vous devez spécifier un conteneur pour cet objet blob.</td>
</tr>
<tr>
<td>Séquence d’octets préfixe du chemin d’accès [facultatif]</td>
<td>chemin d’accès du fichier Hello utilisé toowrite vos objets BLOB dans le conteneur spécifié de hello.<BR>Dans le chemin d’accès de hello, vous pouvez choisir toouse une ou plusieurs instances de hello suivant 2 fréquence hello variables toospecify qui concernent les objets BLOB :<BR>{date}, {time}<BR>Exemple 1 : cluster1/logs/{date}/{time}<BR>Exemple 2 : cluster1/logs/{date}</td>
</tr>
<tr>
<td>Format de la date [facultatif]</td>
<td>Si le jeton de date hello est utilisé dans le chemin d’accès de hello préfixe, vous pouvez sélectionner le format de date hello dans lequel vos fichiers sont organisés. Exemple : JJ/MM/AAAA</td>
</tr>
<tr>
<td>Format de l’heure [facultatif]</td>
<td>Si le jeton de durée hello est utilisé dans le chemin d’accès de hello préfixe, spécifiez le format d’heure hello dans lequel vos fichiers sont organisés. Valeur de hello uniquement pris en charge actuellement est HH.</td>
</tr>
<tr>
<td>Format de sérialisation de l’événement</td>
<td>Format de sérialisation pour les données de sortie.  JSON, CSV et Avro sont pris en charge.</td>
</tr>
<tr>
<td>Encodage</td>
<td>S’il s’agit du format CSV ou JSON, un encodage doit être spécifié. UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant.</td>
</tr>
<tr>
<td>Délimiteur</td>
<td>Applicable uniquement pour la sérialisation CSV. Stream Analytics prend en charge un certain nombre de délimiteurs communs pour sérialiser des données CSV. Valeurs prises en charge : virgule, point-virgule, espace, tabulation et barre verticale.</td>
</tr>
<tr>
<td>Format</td>
<td>Applicable uniquement pour la sérialisation JSON. Ligne séparée spécifie la sortie de hello sera formatée en par chaque objet JSON séparé par une nouvelle ligne. Le tableau spécifie que sortie de hello sera mise en forme en tant que tableau d’objets JSON. Ce tableau va être fermé uniquement lorsque hello tâche s’arrête ou Analytique de flux de données a été déplacé sur la fenêtre de temps suivant toohello. En règle générale, il est ligne toouse préférable JSON séparée, car il ne nécessite aucun traitement spécial pendant que le fichier de sortie hello est en cours d’écriture à.</td>
</tr>
</tbody>
</table>

## <a name="event-hub"></a>Event Hub
[Event Hubs](https://azure.microsoft.com/services/event-hubs/) est un service de réception d’événements de publication/d’abonnement hautement évolutif. Il peut collecter des millions d’événements par seconde.  Une utilisation d’un concentrateur d’événements en tant que sortie est lors de la sortie de hello d’une tâche de flux de données Analytique sera entrée hello d’une autre tâche de diffusion en continu.

Il existe quelques paramètres qui sont des flux de données du concentrateur d’événements nécessaires tooconfigure comme sortie.

| Nom de la propriété | Description |
| --- | --- |
| Alias de sortie |Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requête sortie toothis concentrateur d’événements. |
| Espace de noms Service Bus |Un espace de noms Service Bus est un conteneur pour un jeu d’entités de messagerie. En créant un Event Hub, vous avez également créé un espace de noms Service Bus |
| Event Hub |nom de Hello de votre sortie de concentrateur d’événements |
| Nom de la stratégie Event Hub |Bonjour la stratégie d’accès partagé, qui peut être créé sur l’onglet de configuration du Hub d’événements hello. Chaque stratégie d’accès partagé a un nom, les autorisations que vous définissez ainsi que des clés d’accès |
| Clé de la stratégie Event Hub |clé d’accès partagé Hello utilisé l’espace de noms Service Bus tooauthenticate access toohello |
| Colonne de clé de partition [facultatif] |Cette colonne contient la clé de partition hello pour la sortie du Hub d’événements. |
| Format de sérialisation de l’événement |Format de sérialisation pour les données de sortie.  JSON, CSV et Avro sont pris en charge. |
| Encodage |Pour CSV et JSON, UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant |
| Délimiteur |Applicable uniquement pour la sérialisation CSV. Stream Analytics prend en charge un certain nombre de délimiteurs communs pour sérialiser des données dans un format CSV. Valeurs prises en charge : virgule, point-virgule, espace, tabulation et barre verticale. |
| Format |Applicable uniquement pour le type JSON. Ligne séparée spécifie la sortie de hello sera formatée en par chaque objet JSON séparé par une nouvelle ligne. Le tableau spécifie que sortie de hello sera mise en forme en tant que tableau d’objets JSON. |

## <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com/) utilisable comme une sortie pour un tooprovide de travail Analytique des flux de données pour une expérience enrichie de visualisation des résultats de l’analyse. Cette fonctionnalité peut être utilisée pour les tableaux de bord opérationnels, la génération de rapports et la création de rapports pilotés par des métriques.

### <a name="authorize-a-power-bi-account"></a>Autorisation d’un compte Power BI
1. Lorsque Power BI est sélectionné comme sortie Bonjour portail Azure, vous allez être invité à tooauthorize utilisateur Power BI existant ou toocreate un nouveau compte Power BI.  
   
   ![Autoriser un utilisateur de Power BI](./media/stream-analytics-define-outputs/01-stream-analytics-define-outputs.png)  
2. Créez un compte si vous n’en avez pas déjà un, puis cliquez sur Autoriser maintenant.  Un écran hello suivante s’affiche.  
   
   ![Compte Azure Power BI](./media/stream-analytics-define-outputs/02-stream-analytics-define-outputs.png)  
3. Dans cette étape, fournissez le travail de hello compte ou scolaire pour autoriser la sortie de Power BI hello. Si vous n’êtes pas déjà inscrit à Power BI, choisissez S’inscrire maintenant. Hello compte professionnel ou scolaire que vous utilisez pour Power BI peut différer de hello compte d’abonnement Azure qui vous êtes actuellement connecté.

### <a name="configure-hello-power-bi-output-properties"></a>Configurer les propriétés de sortie hello Power BI
Une fois que vous avez hello Power BI compte est authentifié, vous pouvez configurer les propriétés de hello par votre sortie Power BI. tableau Hello ci-dessous est liste hello de noms de propriétés et leur tooconfigure description votre sortie Power BI.

| Nom de la propriété | Description |
| --- | --- |
| Alias de sortie |Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requête sortie toothis sortie de Power BI. |
| Espace de travail de groupe |tooenable partage des données avec d’autres utilisateurs de Power BI, vous pouvez sélectionner les groupes à l’intérieur de votre Power BI compte ou choisissez « Mon espace de travail » si vous ne souhaitez pas toowrite tooa groupe.  Mise à jour d’un groupe existant nécessite le renouvellement de l’authentification de hello Power BI. |
| Nom du jeu de données |Fournissez un nom de jeu de données qu’il est souhaité pour hello Power BI sortie toouse |
| Nom de la table |Fournissez un nom de table dans le dataset hello Hello que Power BI de sortie. Actuellement, la sortie Power BI des tâches Stream Analytics peut avoir une table uniquement dans un jeu de données. |

Pour une vue d’ensemble de la configuration d’un tableau de bord et la sortie Power BI, consultez hello [Analytique de flux de données Azure et Power BI](stream-analytics-power-bi-dashboard.md) l’article.

> [!NOTE]
> Ne créez pas explicitement hello le jeu de données et la table dans le tableau de bord Power BI hello. Hello jeu de données et la table seront automatiquement renseignés lorsque la tâche hello est démarrée et hello programmée de sortie pompage dans Power BI. Notez que si la requête de travail hello ne génère des résultats, hello dataset et table ne sera pas créée. Sachez également que si Power BI a déjà un jeu de données et une table avec hello identique à celui hello celui fourni dans cette tâche de flux de données Analytique, hello les données existantes seront remplacées.
> 
> 

### <a name="schema-creation"></a>Création d’un schéma
Analytique de flux de données Azure crée un jeu de données Power BI et une table pour le compte d’utilisateur de hello si elle n’existe pas déjà. Dans tous les autres cas, table de hello est mise à jour avec de nouvelles valeurs. Actuellement, il n’existe une limitation hello ce qu’une seule table peut exister dans un jeu de données.

### <a name="data-type-conversion-from-asa-toopower-bi"></a>Conversion de ASA tooPower BI de type de données
Analytique de flux de données Azure met à jour le modèle de données hello dynamiquement au moment de l’exécution si les modifications de schéma de sortie hello. Toutes les modifications de nom de colonne, modifications de type de colonne et hello Ajout ou la suppression de colonnes sont suivies.

Ce tableau présente hello conversions de types de données à partir de [les types de données de flux de données Analytique](https://msdn.microsoft.com/library/azure/dn835065.aspx) tooPower BRI [types du modèle EDM (Entity Data Model)](https://powerbi.microsoft.com/documentation/powerbi-developer-walkthrough-push-data/) si un jeu de données POWER BI et une table n’existent pas.


De Stream Analytics | tooPower BI
-----|-----|------------
bigint | Int64
nvarchar(max) | String
datetime | DateTime
float | Double
Tableau d’enregistrements | Type chaîne, valeur constante « IRecord » ou « IArray »

### <a name="schema-update"></a>Mise à jour d’un schéma
Flux de données Analytique déduit le schéma de modèle de données hello basé sur le premier jeu d’événements dans la sortie de hello de hello. Ultérieurement, si nécessaire, le schéma de modèle de données hello est tooaccommodate mis à jour les événements entrants qui peut ne pas correspondre dans le schéma d’origine de hello.

Hello `SELECT *` requête doit être évitée mise à jour de schéma dynamique tooprevent dans des lignes. En outre toopotential en matière de performances, il peut également entraîner indeterminacy d’hello nécessaire pour les résultats hello. les champs exacts Hello nécessitant toobe affiché dans le tableau de bord Power BI doivent être sélectionnées. En outre, les valeurs de données hello doivent être conformes à hello choisi le type de données.


Précédent/Actuel | Int64 | String | DateTime | Double
-----------------|-------|--------|----------|-------
Int64 | Int64 | String | String | Double
Double | Double | String | String | Double
String | Chaîne | Chaîne | Chaîne |  | String | 
DateTime | String | String |  DateTime | String


### <a name="renew-power-bi-authorization"></a>Renouvellement de l’autorisation Power BI
Vous devez toore-authentifier votre compte Power BI si son mot de passe a changé depuis la création ou de dernière authentification de votre travail. Si l’authentification multifacteur (MFA) est configuré sur votre client Azure Active Directory (AAD), vous devez également l’autorisation de Power BI de toorenew toutes les 2 semaines. Un symptôme de ce problème est aucune sortie de travail et une « erreur d’utilisateur de Authenticate » dans les journaux des opérations de hello :

  ![Erreur de jeton d’actualisation Power BI](./media/stream-analytics-define-outputs/03-stream-analytics-define-outputs.png)  

tooresolve ce problème, arrêtez votre travail en cours d’exécution et accédez tooyour Power BI sortie.  Cliquez sur le lien de « Renouveler l’autorisation » hello et redémarrez votre travail à partir de la perte de données heure du dernier arrêt tooavoid de hello.

  ![Renouvellement de l’autorisation Power BI](./media/stream-analytics-define-outputs/04-stream-analytics-define-outputs.png)  

## <a name="table-storage"></a>Stockage de tables
[Stockage de Table Azure](../storage/common/storage-introduction.md) offre un stockage hautement disponible et très évolutif, afin qu’une application peut automatiquement mettre à l’échelle à la demande de toomeet utilisateur. Stockage de table est de NoSQL/attribut key banque celui qui peut tirer parti des données structurées avec moins de contraintes sur le schéma de hello. Stockage de Table Azure peut être des données de toostore utilisé pour la persistance et la récupération efficace.

Hello ci-dessous répertorie les noms de propriété hello et leur description pour la création d’une sortie de la table.

| Nom de la propriété | Description |
| --- | --- |
| Alias de sortie |Il s’agit d’un nom convivial utilisé dans le stockage de table toothis sortie de requête de requêtes toodirect hello. |
| Compte de stockage |nom Hello hello du compte de stockage où vous envoyez votre sortie. |
| Clé du compte de stockage |clé d’accès Hello associé au compte de stockage hello. |
| Nom de la table |nom de Hello de table de hello. table de Hello sera créée si elle n’existe pas. |
| Partition Key |nom Hello de clé de partition hello contenant hello sortie colonne. clé de partition Hello est un identificateur unique pour la partition hello dans une table donnée constitue hello première partie de la clé primaire d’une entité. Il est une valeur de chaîne qui peut être up too1 Ko. |
| Row Key |nom de Hello de clé de ligne hello contenant hello sortie colonne. clé de ligne Hello est un identificateur unique pour une entité dans une partition donnée. Il forme hello deuxième partie de clé primaire d’une entité. clé de ligne Hello est une valeur de chaîne qui peut être up too1 Ko. |
| Taille du lot |nombre de Hello d’enregistrements pour un traitement par lots. En général, la valeur par défaut de la hello est suffisant pour la plupart des tâches, consultez toohello [spécification de l’opération de traitement par lots de Table](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx) pour plus d’informations sur la modification de ce paramètre. |

## <a name="service-bus-queues"></a>Files d'attente Service Bus
[Les files d’attente de service Bus](https://msdn.microsoft.com/library/azure/hh367516.aspx) offrent une, tooone de remise de message de premier sorti (FIFO) ou plusieurs consommateurs concurrents. En règle générale, les messages sont attendu toobe reçu et traité par les récepteurs hello dans l’ordre temporel de hello dans lequel ils ont été ajoutés à la file d’attente de toohello, et chaque message est reçu et traité par un consommateur d’un seul message.

Hello ci-dessous répertorie les noms de propriété hello et leur description pour la création d’une sortie de la file d’attente.

| Nom de la propriété | Description |
| --- | --- |
| Alias de sortie |Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requête sortie toothis file d’attente du Bus de Service. |
| Espace de noms Service Bus |Un espace de noms Service Bus est un conteneur pour un jeu d’entités de messagerie. |
| Nom de la file d’attente |nom Hello Hello file d’attente du Bus de Service. |
| Nom de la stratégie de file d’attente |Lorsque vous créez une file d’attente, vous pouvez également créer des stratégies d’accès partagé sur l’onglet configurer de la file d’attente de hello. Chaque stratégie d’accès partagé a un nom, les autorisations que vous définissez ainsi que des clés d’accès. |
| Clé de la stratégie de file d’attente |clé d’accès partagé Hello utilisé l’espace de noms Service Bus tooauthenticate access toohello |
| Format de sérialisation de l’événement |Format de sérialisation pour les données de sortie.  JSON, CSV et Avro sont pris en charge. |
| Encodage |Pour CSV et JSON, UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant |
| Délimiteur |Applicable uniquement pour la sérialisation CSV. Stream Analytics prend en charge un certain nombre de délimiteurs communs pour sérialiser des données dans un format CSV. Valeurs prises en charge : virgule, point-virgule, espace, tabulation et barre verticale. |
| Format |Applicable uniquement pour le type JSON. Ligne séparée spécifie la sortie de hello sera formatée en par chaque objet JSON séparé par une nouvelle ligne. Le tableau spécifie que sortie de hello sera mise en forme en tant que tableau d’objets JSON. |

## <a name="service-bus-topics"></a>Rubriques de Service Bus
Tandis que les files d’attente de Service Bus fournissent une méthode de communication tooone à partir de l’expéditeur tooreceiver, [rubriques Service Bus](https://msdn.microsoft.com/library/azure/hh367516.aspx) offrent une forme de type un-à-plusieurs de communication.

Hello ci-dessous répertorie les noms de propriété hello et leur description pour la création d’une sortie de la table.

| Nom de la propriété | Description |
| --- | --- |
| Alias de sortie |Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requête sortie toothis rubrique Service Bus. |
| Espace de noms Service Bus |Un espace de noms Service Bus est un conteneur pour un jeu d’entités de messagerie. En créant un Event Hub, vous avez également créé un espace de noms Service Bus |
| Nom de la rubrique |Rubriques sont entités de messagerie, similaires tooevent concentrateurs et les files d’attente. Ils sont conçus toocollect flux d’événements provenant de différents appareils et services. Quand une rubrique est créée, elle reçoit également un nom. envoi de messages Hello tooa rubrique ne sera pas disponible, sauf si un abonnement est créé, assurez-vous il existe un ou plusieurs abonnements sous la rubrique de hello |
| Nom de la stratégie de rubrique |Lorsque vous créez une rubrique, vous pouvez également créer des stratégies d’accès partagé sur l’onglet de configuration de la rubrique hello. Chaque stratégie d’accès partagé a un nom, les autorisations que vous définissez ainsi que des clés d’accès |
| Clé de la stratégie de rubrique |clé d’accès partagé Hello utilisé l’espace de noms Service Bus tooauthenticate access toohello |
| Format de sérialisation de l’événement |Format de sérialisation pour les données de sortie.  JSON, CSV et Avro sont pris en charge. |
| Encodage |S’il s’agit du format CSV ou JSON, un encodage doit être spécifié. UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant |
| Délimiteur |Applicable uniquement pour la sérialisation CSV. Stream Analytics prend en charge un certain nombre de délimiteurs communs pour sérialiser des données dans un format CSV. Valeurs prises en charge : virgule, point-virgule, espace, tabulation et barre verticale. |

## <a name="azure-cosmos-db"></a>Azure Cosmos DB
[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) est un service de base de données de documents NoSQL entièrement géré qui permet d'utiliser des données de requêtes et de transactions sans schéma, offre des performances prévisibles et fiables, et permet un développement rapide.

Hello sous les noms de propriété de liste détails hello et leur description pour la création d’une sortie de la base de données Azure Cosmos.

* **Alias de sortie** – un toorefer alias cette sortie dans votre requête ASA  
* **Nom de compte** – nom de hello ou point de terminaison de l’URI de hello Cosmos DB compte.  
* **Clé de compte** – clé d’accès partagé hello pour hello Cosmos DB compte.  
* **Base de données** – nom de base de données de base de données Cosmos hello.  
* **Modèle de nom de collection** – nom de la collection hello ou leur modèle pour hello collections toobe est utilisé. format du nom de collection Hello peut être construite à l’aide de jeton {partition} facultatif de hello, où les partitions commencent à 0. Voici des exemples d’entrées valides :  
  1\) MyCollection : il doit exister une collection nommée « MyCollection ».  
  2\) MyCollection{partition} : vous devez créer les collections « MyCollection0 », « MyCollection1 », « MyCollection2 », etc.  
* **Clé de partition** : facultative. Nécessaire uniquement si vous utilisez un jeton {partition} dans votre modèle de nom de collection. nom Hello du champ hello dans la clé de hello toospecify sortie événements utilisés pour le partitionnement de sortie entre les collections. Pour une sortie de collection unique, une colonne de sortie arbitraire peut être utilisée (par exemple, PartitionId).  
* **ID de document** : facultatif. nom de Hello du champ hello dans les événements de sortie utilisé clé primaire de toospecify hello basées sur les insert ou la mise à jour operations.  


## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
Vous avez été introduite tooStream Analytique, un service géré de diffusion en continu d’analytique sur les données à partir de hello Internet des objets. toolearn en savoir plus sur ce service, consultez :

* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
