---
title: stockage de froid aaaAzure pour les objets BLOB | Documents Microsoft
description: "Niveaux de stockage d’objets blob Azure pour un stockage économique des données d’objet basé sur les modèles d’accès. couche de stockage froid Hello est optimisé pour les données qui sont moins sollicitées."
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 56fae3fdae31a6958ebae01fd96a0366e70ae938
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-and-cool-storage-tiers"></a>Stockage des objets blob Azure : niveaux de stockage chauds et froids
## <a name="overview"></a>Vue d'ensemble
Le stockage Azure offre deux niveaux de stockage d’objets blob afin que vous puissiez stocker vos données de manière plus économique en fonction de leur utilisation. Bonjour Azure **niveau de stockage à chaud** est optimisé pour stocker les données fréquemment sollicitées. Bonjour Azure **niveau de stockage froid** est optimisé pour le stockage des données qui sont rarement sollicitées et à long terme. Les données dans la couche de stockage froid hello peuvent tolérer disponibilité légèrement inférieure, mais il demande une durabilité élevée et des caractéristiques de débit et le temps d’accès similaires sous forme de données à chaud. Concernant les données froides, un contrat SLA de disponibilité légèrement inférieure et des coûts d’accès supérieurs sont des compromis acceptables pour des coûts de stockage beaucoup plus faibles.

Aujourd'hui, les données stockées dans le cloud de hello augmente à un rythme exponentiels. toomanage des coûts en termes de vos besoins de stockage en expansion, il est utile tooorganize vos données en fonction des attributs comme la fréquence d’accès et planifié la période de rétention. Les données stockées dans le cloud de hello peuvent être différentes en termes de comment il est généré, traitée et accessible via sa durée de vie. Certaines données sont activement sollicitées et modifiées tout au long de leur durée de vie. Certaines données sont accessible fréquemment tôt dans sa durée de vie, avec accès suppression considérablement en tant que l’âge des données hello. Certaines données restent inactives dans le cloud de hello et sont rarement, si jamais, accessibles une fois stockés.

Chacun des scénarios d’accès aux données décrits ci-dessus peut bénéficier des avantages d’un niveau de stockage différencié, gage d’optimisation pour un modèle d’accès particulier. Avec l’introduction de hello de niveaux de stockage des sauvegardes à chaud et à froid, Azure Blob storage désormais répond à ce besoin pour des niveaux de stockage différenciés avec séparer les modèles de tarification.

## <a name="blob-storage-accounts"></a>Comptes de stockage d’objets blob
Les **comptes de stockage d’objets blob** sont des comptes de stockage spécialisés pour le stockage des données non structurées en tant qu’objets blob dans Azure Storage. Avec les comptes de stockage d’objets Blob, vous pouvez maintenant choisir entre toostore des niveaux de stockage des sauvegardes à chaud et à froid vos données auxquelles on accès moins fréquemment froid à moindre coût de stockage et magasin plus fréquemment les données à chaud à un faible coût d’accès. Comptes de stockage d’objets BLOB sont similaires tooyour des comptes de stockage à usage général existants et partagent tous les durabilité élevée de hello, disponibilité, évolutivité et des fonctionnalités de performances que vous utilisez aujourd'hui, y compris la cohérence d’API de 100 % pour les objets BLOB de blocs et objets BLOB d’ajout.

> [!NOTE]
> Les comptes de stockage d’objets blob prennent en charge uniquement les objets blob de blocs et d’ajout, mais pas les objets blob de pages.
> 
> 

Comptes de stockage d’objets BLOB exposent hello **couche d’accès aux** attribut, qui vous permet de niveau de stockage toospecify hello en tant que **à chaud** ou **froid** selon les données hello stockées Bonjour compte. S’il existe une modification dans le modèle d’utilisation hello de vos données, vous pouvez également basculer entre ces niveaux de stockage à tout moment.

> [!NOTE]
> Niveau de stockage hello modification peut entraîner des frais supplémentaires. Consultez hello [tarification et facturation](storage-blob-storage-tiers.md#pricing-and-billing) section pour plus d’informations.
> 
> 

Exemples de scénarios d’utilisation pour le niveau de stockage à chaud hello sont les suivantes :

* Données dans l’utilisation active ou toobe attendu (lecture à partir d’et écrites sur) fréquemment sollicitées.
* Données qui sont préparées pour une éventuelle transformation et de la couche de stockage froid migration toohello.

Exemples de scénarios d’utilisation pour le niveau de stockage froid hello sont les suivantes :

* Sauvegarde, archivage et récupération d’urgence d’ensembles de données.
* Le contenu multimédia antérieur pas consulté fréquemment plus, mais est attendu toobe disponible immédiatement lors de l’accès.
* Grands jeux de données qui doivent toobe stockées coût efficacement tandis que d’autres données sont rassemblées pour un traitement ultérieur. (*par exemple*, le stockage à long terme de données scientifiques, les données de télémétrie brute d’un site de production)
* Données d’origine (brutes) qui doivent être conservées, même après leur traitement sous un format final exploitable (*par exemple*, des fichiers multimédias bruts après transcodage dans d’autres formats)
* Conformité et les données d’archivage dont a besoin de toobe stockée pendant une longue période et se trouve très peu. (*par exemple*, séquences vidéo de sécurité, anciens clichés de radiographie ou d’IRM pour des organismes de santé ou enregistrements audio et transcriptions d’appels de clients pour des services financiers)

Pour plus d’informations sur les comptes de stockage, consultez [À propos des comptes de stockage Azure](storage-create-storage-account.md) .

Pour les applications nécessitant uniquement bloquent ou ajouter le stockage d’objets blob, nous recommandons d’utiliser des comptes de stockage d’objets Blob, parti tootake Hello différenciés modèle de tarification du stockage hiérarchisé. Toutefois, nous comprendre que cela sera peut-être pas possible dans certaines circonstances où l’utilisation du stockage à usage général comptes serait y hello moyen toogo, telles que :

* Vous devez toouse tables, files d’attente, ou les fichiers et vous souhaitez que vos objets BLOB stockés dans hello même compte de stockage. Notez qu’il n’existe aucun toostoring technique parti dans hello que même compte autre qu’ayant hello même des clés partagées.
* Vous devez toujours le modèle de déploiement classique toouse hello. Comptes de stockage d’objets BLOB sont uniquement disponibles via le modèle de déploiement du Gestionnaire de ressources Azure hello.
* Vous avez besoin d’objets BLOB de pages toouse. Les comptes de stockage d’objets blob ne gèrent pas les objets blob de pages. En général, nous recommandons d’utiliser des objets blob de blocs, sauf si vous avez spécifiquement besoin d’objets blob de pages.
* Vous utilisez une version de hello [API REST des Services de stockage](https://msdn.microsoft.com/library/azure/dd894041.aspx) qui est antérieur à 2014-02-14 ou une bibliothèque cliente avec une version inférieure à 4.x et ne peut pas de mettre à niveau votre application.

> [!NOTE]
> Les comptes de stockage d’objets blob sont actuellement pris en charge dans toutes les régions Azure.
> 
> 

## <a name="comparison-between-hello-storage-tiers"></a>Comparaison entre les niveaux de stockage hello
Hello tableau suivant met en évidence comparaison hello entre deux niveaux de stockage hello :

<table border="1" cellspacing="0" cellpadding="0" style="border: 1px solid #000000;">
<col width="250">
<col width="250">
<col width="250">
<tbody>
<tr>
    <td><strong><center></center></strong></td>
    <td><strong><center>Niveau de stockage chaud</center></strong></td>
    <td><strong><center>Niveau de stockage froid</center></strong></td
</tr>
<tr>
    <td><strong><center>Disponibilité</center></strong></td>
    <td><center>99.9%</center></td>
    <td><center>99%</center></td>
</tr>
<tr>
    <td><strong><center>Disponibilité<br>(Lectures RA-GRS)</center></strong></td>
    <td><center>99.99%</center></td>
    <td><center>99.9%</center></td>
</tr>
<tr>
    <td><strong><center>Frais d’utilisation</center></strong></td>
    <td><center>Coûts de stockage supérieurs<br>Coûts d’accès et de transaction inférieurs</center></td>
    <td><center>Coûts de stockage inférieurs<br>Coûts d’accès et de transaction supérieurs</center></td>
</tr>
<tr>
    <td><strong><center>Taille minimale des objets<center></strong></td>
    <td colspan="2"><center>N/A</center></td>
</tr>
<tr>
    <td><strong><center>Durée de stockage minimale<center></strong></td>
    <td colspan="2"><center>N/A</center></td>
</tr>
<tr>
    <td><strong><center>Latence<br>(Octets toofirst de temps)<center></strong></td>
    <td colspan="2"><center>millisecondes</center></td>
</tr>
<tr>
    <td><strong><center>Cibles de performance et d’évolutivité<center></strong></td>
    <td colspan="2"><center>Identiques aux comptes de stockage à usage général</center></td>
</tr>
</tbody>
</table>

> [!NOTE]
> Stockage d’objets BLOB comptes hello de prise en charge des cibles de performances et évolutivité mêmes en tant que comptes de stockage à usage général. Pour plus d’informations, consultez la page [Objectifs de performance et évolutivité d'Azure Storage](storage-scalability-targets.md) .
> 
> 

## <a name="pricing-and-billing"></a>Tarification et facturation
Comptes de stockage d’objets BLOB utilisent un nouveau modèle de tarification pour le stockage d’objets blob selon le niveau de stockage hello. Lorsque vous utilisez un compte de stockage d’objets Blob, hello suivant des considérations relatives à la facturation s’appliquent :

* **Les coûts de stockage**: toohello le volume de données stockées, en outre coût hello du stockage des données varie selon le niveau de stockage hello. coût par gigaoctet de Hello est plus faible pour le niveau de stockage froid hello que pour le niveau de stockage à chaud hello.
* **Les coûts d’accès aux données**: pour les données dans la couche de stockage froid hello, vous serez facturé au gigaoctet données accès frais pour les lectures et écritures.
* **Coûts de transaction**: des frais par transaction s’appliquent pour les deux niveaux. Toutefois, le coût par transaction de hello pour le niveau de stockage froid hello est supérieur à celui pour le niveau de stockage à chaud hello.
* **Les coûts de transfert de données de géo-réplication**: cela s’applique uniquement tooaccounts avec géo-réplication configurée, y compris GRS et RA-GRS. Le transfert de données de géoréplication implique des frais par gigaoctet.
* **Coûts de transfert de données sortantes** : les transferts de données sortantes (données transférées hors d’une région Azure) sont facturés pour l’utilisation de la bande passante par gigaoctet. Cette facturation est cohérente avec les comptes de stockage à usage général.
* **Niveau de stockage hello modification**: remplaçant la couche de stockage hello toohot froid entraînent un tooreading égal charge toutes les données hello existant dans le compte de stockage hello pour chaque transition. Hello autre part, en remplaçant la couche de stockage hello toocool à chaud sera gratuitement.

> [!NOTE]
> Dans commande tootry d’utilisateurs tooallow out hello nouveaux niveaux de stockage et valider les fonctionnalités après lancement, frais hello pour modifier le niveau de stockage hello de toohot froid seront annulés désactivé jusqu’au 30 juin 2016. Depuis le 1er juillet 2016, les frais de hello seront transitions tooall appliqués à partir de toohot froid. Pour plus d’informations sur hello tarification pour les comptes de stockage d’objets Blob, consultez [tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/) page. Pour plus d’informations sur les données sortantes hello frais de transfert de voir, [détails de tarification des transferts de données](https://azure.microsoft.com/pricing/details/data-transfers/) page.
> 
> 

## <a name="quick-start"></a>Démarrage rapide
Dans cette section, nous allons vous montrer hello à l’aide de hello portail Azure les scénarios suivants :

* Comment toocreate un compte de stockage d’objets Blob.
* Comment toomanage un compte de stockage d’objets Blob.

### <a name="using-hello-azure-portal"></a>À l’aide de hello portail Azure
#### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Créer un compte de stockage d’objets Blob à l’aide de hello portail Azure
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, sélectionnez **nouveau** > **données + stockage** > **compte de stockage**.
3. Entrez un nom pour votre compte de stockage.
   
    Ce nom doit être globalement unique ; Il est utilisé comme partie de l’URL de hello utilisé les objets hello tooaccess hello compte de stockage.  
4. Sélectionnez **le Gestionnaire de ressources** en tant que modèle de déploiement hello.
   
    Stockage hiérarchisé est utilisable uniquement avec les comptes de stockage du Gestionnaire de ressources ; Il s’agit de hello recommandé de modèle de déploiement de nouvelles ressources. Pour plus d’informations, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md).  
5. Dans la liste déroulante de type de compte hello, sélectionnez **stockage d’objets Blob**.
   
    Il s’agit où vous sélectionnez le type hello du compte de stockage. À plusieurs niveaux de stockage n’est pas disponible dans le stockage à usage général ; Il est uniquement disponible dans hello compte de type de stockage Blob.     
   
    Notez que lorsque vous sélectionnez cette option, niveau de performances de hello a la valeur tooStandard. À plusieurs niveaux de stockage n’est pas disponible avec le niveau de performance Premium hello.
6. Sélectionnez l’option de réplication hello pour le compte de stockage hello : **LRS**, **GRS**, ou **RA-GRS**. valeur par défaut Hello est **RA-GRS**.
   
    LRS = stockage localement redondant ; GRS = stockage géo-redondant (2 régions) ; RA-GRS est un stockage géo-redondant avec accès en lecture (2 régions avec lecture accéder ensuite toohello).
   
    Pour plus d’informations sur les options de réplication d’Azure Storage, voir [Réplication Azure Storage](storage-redundancy.md).
7. Sélectionnez hello bon niveau de stockage de vos besoins : ensemble hello **couche d’accès aux** tooeither **froid** ou **à chaud**. valeur par défaut Hello est **à chaud**.
8. Sélectionnez l’abonnement hello dans lequel vous souhaitez toocreate hello nouveau compte de stockage.
9. Spécifiez un nouveau groupe de ressources ou sélectionnez un groupe de ressources existant. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
10. Sélectionnez la région de hello pour votre compte de stockage.
11. Cliquez sur **créer** compte de stockage toocreate hello.

#### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Modifier le niveau de stockage hello d’un compte de stockage d’objets Blob à l’aide de hello portail Azure
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. compte de stockage toonavigate tooyour, sélectionnez toutes les ressources, puis sélectionnez votre compte de stockage.
3. Dans le panneau des paramètres de hello, cliquez sur **Configuration** tooview et/ou de la modification de configuration de compte hello.
4. Sélectionnez hello bon niveau de stockage de vos besoins : ensemble hello **couche d’accès aux** tooeither **froid** ou **à chaud**.
5. Cliquez sur Enregistrer en haut de hello du Panneau de hello.

> [!NOTE]
> Niveau de stockage hello modification peut entraîner des frais supplémentaires. Consultez hello [tarification et facturation](storage-blob-storage-tiers.md#pricing-and-billing) section pour plus d’informations.
> 
> 

## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>L’évaluation et la migration des comptes de stockage tooBlob
objectif de cette section Hello est toohelp utilisateurs toomake un smooth comptes de stockage d’objets Blob toousing la transition. Il existe deux scénarios utilisateur :

* Vous disposez d’un compte de stockage à usage général et que vous souhaitez tooevaluate un tooa de modifier le compte de stockage Blob avec hello bon niveau de stockage.
* Vous avez décidé de toouse un compte de stockage d’objets Blob ou encore et souhaitez tooevaluate si vous devez utiliser le niveau de stockage à chaud ou à froid hello.

Dans les deux cas, hello première chose est le coût de hello tooestimate du stockage et de l’accès à vos données stockées dans un compte de stockage d’objets Blob et que comparer les coûts en cours.

### <a name="evaluating-blob-storage-account-tiers"></a>Évaluation des niveaux de compte de stockage d’objets blob
Commande tooestimate hello le coût de stockage et l’accès aux données stockées dans un compte de stockage d’objets Blob, vous devez tooevaluate votre modèle d’utilisation existants ou être proche de votre modèle d’utilisation attendu. En règle générale, vous pouvez tooknow :

* Votre consommation de stockage : quel est le volume de données stockées et quelle est son évolution mensuelle ?
* Votre modèle d’accès stockage - la quantité de données sont en cours pour la lecture et compte toohello écrite (y compris les nouvelles données) ? Le nombre et le type de transactions utilisées pour accéder aux données.

#### <a name="monitoring-existing-storage-accounts"></a>Analyse des comptes de stockage existants
toomonitor des comptes de votre stockage existant et rassembler ces données, vous pouvez vous servir d’Analytique de stockage Azure qui effectue la journalisation et fournit des données de métriques pour un compte de stockage.
Stockage Analytique peut stocker des métriques qui incluent des données de la capacité et les statistiques groupées des transactions sur les demandes toohello service de stockage d’objets Blob pour les comptes de stockage à usage général ainsi que des comptes de stockage d’objets Blob.
Ces données sont stockées dans des tables connues Bonjour même compte de stockage.

Pour plus d’informations, consultez [À propos des métriques de Storage Analytics](https://msdn.microsoft.com/library/azure/hh343258.aspx) et [Schéma de table de métriques Storage Analytics](https://msdn.microsoft.com/library/azure/hh343264.aspx)

> [!NOTE]
> Comptes de stockage d’objets BLOB exposent un point de terminaison du service hello table uniquement pour le stockage et l’accès aux données de métriques hello pour ce compte.
> 
> 

consommation du stockage hello toomonitor pourquoi le service de stockage d’objets Blob, vous aurez besoin des métriques de capacité tooenable hello.
Avec cette option est activée, les données de capacité sont enregistrées quotidiennement pour service d’objets Blob d’un compte de stockage et enregistrées comme une entrée de table qui est écrit toohello *$MetricsCapacityBlob* de table dans hello même compte de stockage.

modèle d’accès aux données toomonitor hello pour hello service de stockage d’objets Blob, vous devez tooenable hello horaire métriques de transaction au niveau de l’API.
Avec cette option est activée, par l’API de transactions sont agrégées toutes les heures et enregistrées comme une entrée de table qui est écrit toohello *$MetricsHourPrimaryTransactionsBlob* de table dans hello même compte de stockage. Hello *$MetricsHourSecondaryTransactionsBlob* enregistrements de la table hello de point de terminaison transactions toohello secondaire en cas de comptes de stockage RA-GRS.

> [!NOTE]
> Ce processus d’estimation n’est pas applicable si vous avez un compte de stockage à usage général dans lequel vous avez stocké des objets blob de pages et des disques de machines virtuelles en même temps que des données d’objets blob de blocs et d’ajout. Il s’agit, car vous n’avez aucun moyen de capacité distinctive et transaction mesures basées uniquement sur le type hello d’objet blob de bloquent et ajouter des objets BLOB qui peut être migrée tooa compte de stockage d’objets Blob.
> 
> 

tooget une bonne approximation de votre consommation de données et le modèle d’accès, nous vous recommandons de vous choisissez une période de rétention pour les métriques de hello est représentative de votre utilisation régulière et extrapolez.
Une option consiste à des données de métriques hello tooretain pour 7 jours et les données de salutation collecter chaque semaine, pour l’analyse à fin hello du mois de hello.
Une autre option est tooretain les données de métriques hello pour hello 30 derniers jours et collecter et analyser les données de hello à fin hello de hello 30 jours.

Pour plus d’informations sur l’activation, la collecte et l’affichage des données de métriques, voir [Activation des métriques Azure Storage et affichage des données associées](storage-enable-and-view-metrics.md).

> [!NOTE]
> Le stockage, l’accès et le téléchargement des données d’analyse sont également facturés comme des données utilisateur standard.
> 
> 

#### <a name="utilizing-usage-metrics-tooestimate-costs"></a>Utilisation des coûts tooestimate métriques d’utilisation
##### <a name="storage-costs"></a>Coûts de stockage
Hello entrée la plus récente dans la table de métriques de capacité hello *$MetricsCapacityBlob* avec la clé de ligne hello *'data'* affiche hello la capacité de stockage consommée par les données utilisateur.
Hello entrée la plus récente dans la table de métriques de capacité hello *$MetricsCapacityBlob* avec la clé de ligne hello *'analytique'* affiche hello la capacité de stockage consommée par les journaux d’analytique hello.

Cette capacité totale consommée par les deux journaux d’analytique et les données utilisateur (si activé) peut ensuite être utilisé le coût de hello tooestimate du stockage des données dans le compte de stockage hello.
Hello même méthode peut également être utilisée pour estimer les coûts de stockage de bloc et ajouter des objets BLOB dans les comptes de stockage à usage général.

##### <a name="transaction-costs"></a>Coûts de transaction
somme Hello de *'TotalBillableRequests'*, pour toutes les entrées d’API dans les transactions hello table des métriques indique le nombre total de hello de transactions pour cette API particulière. *par exemple,*, hello nombre total de *'GetBlob'* transactions pendant une période donnée peuvent être calculées par somme hello du nombre total de demandes facturable pour toutes les entrées avec la clé de ligne hello *' utilisateur ; GetBlob'*.

Commande tooestimate coûts de transaction pour les comptes de stockage d’objets Blob, vous devez toobreak vers le bas les transactions hello en trois groupes dans la mesure où ils sont tarifées différemment.

* Les transactions d’écriture telles que *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* et *'CopyBlob'*.
* Les transactions de suppression telles que *'DeleteBlob'* et *'DeleteContainer'*.
* Toutes les autres transactions.

Commande tooestimate coûts de transaction pour les comptes de stockage à usage général, vous devez tooaggregate toutes les transactions, quelles que soient les hello opération/API.

##### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Coûts d’accès aux données et de transfert de données de géoréplication
Lors de l’analytique de stockage ne fournit pas lire quantité hello de données et écrit le compte de stockage tooa, il peut être estimée approximativement en examinant la table de métriques de transactions hello.
somme Hello de *'TotalIngress'* pour toutes les entrées d’API dans les métriques de transaction hello tableau indique la quantité totale de hello des données d’entrée en octets pour cette API particulière.
De même hello s’élevant *'TotalEgress'* indique hello la quantité totale de données sortantes, en octets.

Dans les coûts d’accès aux données ordre tooestimate hello pour les comptes de stockage d’objets Blob, vous devez toobreak vers le bas les transactions hello en deux groupes.

* quantité de Hello des données récupérées à partir du compte de stockage hello peut être estimée en examinant la somme hello de *'TotalEgress'* pour principalement hello *'GetBlob'* et *'CopyBlob'* opérations.
* quantité de Hello écritures de compte de stockage toohello de données peut être estimée en examinant la somme hello de *'TotalIngress'* pour principalement hello *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* et *'AppendBlock'* operations.

Bonjour coût de transfert de données de géo-réplication pour l’objet Blob de comptes de stockage peuvent également être calculées à l’aide d’estimation de hello pour les données écrites en cas d’un compte de stockage GRS ou RA-GRS durée hello.

> [!NOTE]
> Pour obtenir un exemple plus détaillé sur le calcul des coûts hello pour à l’aide de la couche de stockage à chaud ou à froid hello, veuillez examiner hello FAQ intitulée *« quels sont les niveaux d’accès à chaud et à froid et comment dois-je pour déterminer quels un toouse ? »* Bonjour [Page de tarification de stockage Azure](https://azure.microsoft.com/pricing/details/storage/).
> 
> 

### <a name="migrating-existing-data"></a>Migration des données existantes
Un compte de stockage d’objets blob est un compte spécialisé pour stocker uniquement les objets blob de blocs et d’ajout. Les comptes de stockage à usage général existants, ce qui vous toostore tables, files d’attente, les fichiers et disques, ainsi que d’objets BLOB, ne peut pas être convertie tooBlob les comptes de stockage. toouse hello des niveaux de stockage, vous avez besoin de nouveaux comptes de stockage d’objets Blob toocreate et migrer vos données dans les comptes hello nouvellement créé.

Vous pouvez utiliser hello suivant toomigrate données existant dans les comptes de stockage d’objets Blob à partir de périphériques de stockage local, à partir des fournisseurs de stockage cloud de tiers ou à partir de vos comptes de stockage à usage général existants dans Azure :

#### <a name="azcopy"></a>AzCopy
AzCopy est un utilitaire de ligne de commande Windows destiné à hautes performances, copie des données tooand depuis le stockage Azure. Vous pouvez utiliser AzCopy toocopy importer votre compte de stockage d’objets Blob à partir de vos comptes de stockage à usage général existant, ou tooupload données à partir de vos périphériques de stockage local dans votre compte de stockage d’objets Blob.

Pour plus d’informations, consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).

#### <a name="data-movement-library"></a>Bibliothèque de déplacement des données
Azure bibliothèque le déplacement des données de stockage pour .NET est basée sur l’infrastructure de déplacement de données de base de hello alimente AzCopy. bibliothèque de Hello est conçu pour des performances élevées, tooAzCopy similaire d’opérations de transfert de données simple et fiables. Cela vous permet de tootake pleinement parti des fonctionnalités de hello fournies par AzCopy dans votre application en mode natif sans avoir toodeal en cours d’exécution et l’analyse des instances externes de AzCopy.

Pour plus d’informations, voir [Azure Storage Data Movement Library for .Net](https://github.com/Azure/azure-storage-net-data-movement)

#### <a name="rest-api-or-client-library"></a>API REST ou bibliothèque cliente
Vous pouvez créer une application personnalisée de toomigrate vos données dans un compte de stockage d’objets Blob à l’aide d’une des bibliothèques de client Azure hello ou hello API REST de services de stockage Azure. Azure Storage offre des bibliothèques clientes enrichies pour une diversité de langages et plateformes, par exemple .NET, Java, C++, Node.JS, PHP, Ruby et Python. les bibliothèques clientes Hello proposent des fonctionnalités avancées telles que des téléchargements parallèles, la journalisation et la logique de nouvelle tentative. Vous pouvez également développer directement sur hello API REST, ce qui peut être appelée par n’importe quel langage qui rend les requêtes HTTP/HTTPS.

Pour plus d’informations, voir [Prise en main du stockage d’objets blob Azure](storage-dotnet-how-to-use-blobs.md).

> [!NOTE]
> Objets BLOB chiffré à l’aide du chiffrement côté client stockage les métadonnées relatives au chiffrement stockée avec l’objet blob de hello. Il est absolument essentiel que n’importe quel mécanisme de copie assure qui hello des métadonnées d’objet blob et particulièrement hello relatives au chiffrement des métadonnées, sont conservés. Si vous copiez des objets BLOB de hello sans ces métadonnées, hello blob contenu n’est plus récupérable à nouveau. Pour plus d’informations concernant les métadonnées liées au chiffrement, voir [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](storage-client-side-encryption.md).
> 
> 

## <a name="faqs"></a>FAQ
1. **Les comptes de stockage existants restent-ils disponibles ?**
   
    Oui. Les comptes de stockage existants restent disponibles, avec les mêmes tarifs et fonctionnalités.  Ils n’ont pas de hello capacité toochoose un niveau de stockage et que vous ne disposez pas de fonctions de hiérarchisation Bonjour futures.
2. **Quand et pourquoi dois-je commencer à utiliser des comptes de stockage d’objets blob ?**
   
    Comptes de stockage d’objets BLOB sont spécialisées pour le stockage BLOB et nous permettent de toointroduce de nouvelles fonctionnalités centrées sur l’objet blob. À l’avenir, les comptes de stockage d’objets Blob sont hello recommandé de manière pour le stockage d’objets BLOB, comme des fonctionnalités futures, telles que de stockage hiérarchique et hiérarchisation est introduite en fonction de ce type de compte. Toutefois, c’est tooyou si vous voulez que toomigrate selon les besoins de votre entreprise.
3. **Puis-je convertir mon tooa de compte de stockage existant compte de stockage Blob ?**
   
    Non. Compte de stockage BLOB est un autre type de compte de stockage et vous devez toocreate il est nouveau et migrer vos données, comme expliqué ci-dessus.
4. **Puis-je stocker des objets dans les deux niveaux de stockage Bonjour même compte ?**
   
    Hello *« Niveau d’accès »* attribut qui indique le niveau de stockage hello est définie à un niveau de compte et applique des objets tooall dans ce compte. Impossible de définir des attributs de niveau accès hello au niveau de l’objet.
5. **Puis-je modifier le niveau de stockage hello de mon compte de stockage Blob ?**
   
    Oui. Vous serez toochange en mesure de niveau de stockage hello en définissant un hello *« Niveau d’accès »* attribut sur le compte de stockage hello. Niveau de stockage hello modification s’appliquera tooall les objets stockés dans le compte de hello. Niveau de stockage hello de modification à partir de toocool à chaud ne mobilise pas tous les frais, tandis que remplaçant toohot froid entraîne un par coût en Go pour la lecture de toutes les données hello dans le compte de hello.
6. **La fréquence à laquelle puis-je modifier le niveau de stockage hello de mon compte de stockage Blob ?**
   
    Pendant que nous n’appliquent pas une limite sur la fréquence à laquelle le niveau de stockage hello peut être modifié, sachez que remplaçant la couche de stockage hello toohot froid occasionnent des frais significatifs. Il est déconseillé de modifier le niveau de stockage hello fréquemment.
7. **BLOB hello dans la couche de stockage froid hello seront comporte différemment de ceux de la couche de stockage à chaud hello hello ?**
   
    Objets BLOB dans la couche de stockage à chaud hello ont hello même latence en tant qu’objets BLOB dans les comptes de stockage à usage général. Objets BLOB dans la couche de stockage froid hello dont la latence similaire (en millisecondes) en tant qu’objets BLOB dans les comptes de stockage à usage général.
   
    Objets BLOB dans la couche de stockage froid hello aura légèrement disponibilité service inférieurs (SLA) que BLOB hello stockées dans la couche de stockage à chaud hello. Pour plus d’informations, voir [SLA pour Storage](https://azure.microsoft.com/support/legal/sla/storage).
8. **Puis-je stocker des objets blob de pages et des disques de machine virtuelle dans les comptes de stockage d’objets blob ?**
   
    Les comptes de stockage d’objets blob prennent en charge uniquement les objets blob de blocs et d’ajout, mais pas les objets blob de pages. Disques de machine virtuelle Azure sont soutenus par des objets BLOB de page et par conséquent les comptes de stockage Blob ne peut pas être utilisé toostore les disques de machine virtuelle. Toutefois, il est possible toostore les sauvegardes de disques de machine virtuelle hello en tant qu’objets BLOB de blocs dans un compte de stockage d’objets Blob.
9. **Dois-je toochange mes comptes de stockage d’objets Blob de toouse applications existants ?**
   
    Les comptes de stockage d’objets blob sont cohérents à 100 % avec l’API avec les comptes de stockage à usage général pour les objets blob de blocs et d’ajout. Tant que votre application est à l’aide d’objets BLOB de blocs ou ajouter des objets BLOB, et que vous utilisez la version 2014-02-14 de hello de hello [API REST des Services de stockage](https://msdn.microsoft.com/library/azure/dd894041.aspx) ou supérieur votre application doit fonctionner. Si vous utilisez une ancienne version de protocole de hello, puis vous devez tooupdate votre application toouse hello nouvelle version ainsi en toowork en toute transparence avec les deux types de comptes de stockage. En général, nous recommandons toujours à l’aide de la version la plus récente hello quel que soit le type de compte de stockage que vous utilisez.
10. **L’expérience utilisateur changera-t-elle ?**
    
    Comptes de stockage d’objets BLOB sont des comptes de stockage à usage général tooa très similaire pour le stockage de bloc et ajouter des objets BLOB et prennent en charge toutes les fonctionnalités clés hello du stockage Azure, y compris la durabilité élevée et disponibilité, évolutivité, performances et sécurité. Autres que les comptes de stockage spécifique tooBlob fonctionnalités et restrictions des hello et ses niveaux de stockage présentées ci-dessus, tout autre reste hello identiques.

## <a name="next-steps"></a>Étapes suivantes
### <a name="evaluate-blob-storage-accounts"></a>Évaluer des comptes de stockage d’objets blob
[Vérifier la disponibilité de comptes de stockage d’objets blob par région](https://azure.microsoft.com/regions/#services)

[Évaluer l’utilisation des comptes de stockage actuels en activant les métriques Azure Storage](storage-enable-and-view-metrics.md)

[Vérifier le prix du stockage d’objets blob par région](https://azure.microsoft.com/pricing/details/storage/)

[Vérifier la tarification des transferts de données](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Commencer à utiliser des comptes de stockage d’objets blob
[Prise en main du stockage d’objets blob Azure](storage-dotnet-how-to-use-blobs.md)

[Déplacement des données tooand depuis le stockage Azure](storage-moving-data.md)

[Transfert de données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md)

[Parcourez et explorez vos comptes de stockage](http://storageexplorer.com/)

