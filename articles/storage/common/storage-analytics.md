---
title: "aaaUse données des journaux et des mesures toocollect Analytique de stockage Azure | Documents Microsoft"
description: "Analytique de stockage vous permet de tootrack les données de métriques pour tous les services de stockage et toocollect les journaux pour le stockage Blob, file d’attente et Table."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7894993b-ca42-4125-8f17-8f6dfe3dca76
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: aba1a236cb69fa2e60bcb8fda5d34841e36e379a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-analytics"></a>Storage Analytics

Azure Storage Analytics effectue la journalisation et fournit des données de métriques pour un compte de stockage. Vous pouvez utiliser cette tootrace des demandes de données, analyser les tendances d’utilisation et diagnostiquer les problèmes avec votre compte de stockage.

toouse Analytique de stockage, vous devez l’activer individuellement pour chaque service, vous souhaitez toomonitor. Vous pouvez l’activer à partir de hello [Azure Portal](https://portal.azure.com). Pour plus d’informations, consultez [surveiller un compte de stockage Bonjour Azure Portal](storage-monitor-storage-account.md). Vous pouvez également activer Analytique de stockage par programme via l’API REST de hello ou de la bibliothèque cliente de hello. Hello d’utilisation [Get Blob Service Properties](https://msdn.microsoft.com/library/hh452239.aspx), [obtenir les propriétés de Service de file d’attente](https://msdn.microsoft.com/library/hh452243.aspx), [Get Table Service Properties](https://msdn.microsoft.com/library/hh452238.aspx), et [obtenir des propriétés du Service fichier](https://msdn.microsoft.com/library/mt427369.aspx) operations tooenable Analytique de stockage pour chaque service.

données agrégées Hello sont stockées dans un objet blob connu (pour la journalisation) et dans des tables connues (pour les métriques), qui est accessible à l’aide des API du service de Table et de service d’objets Blob hello.

Analytique de stockage a une limite de 20 To montant hello des données stockées qui est indépendantes de la limite totale de hello pour votre compte de stockage. Pour plus d'informations sur les stratégies de facturation et de rétention de données, consultez [Storage Analytics et facturation](https://msdn.microsoft.com/library/hh360997.aspx). Pour plus d'informations sur les limites des comptes de stockage, consultez la page [Objectifs d'évolutivité et de performances d'Azure Storage](storage-scalability-targets.md).

Pour des instructions détaillées sur l’utilisation de stockage Analytique et les autres outils tooidentify, diagnostiquer et résoudre les problèmes liés au stockage Azure, consultez [moniteur, diagnostiquer et résoudre les problèmes de Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="about-storage-analytics-logging"></a>À propos de la journalisation Storage Analytics
Stockage Analytique enregistre des informations détaillées sur le service de stockage tooa demandes réussies et ayant échoué. Ces informations peuvent être utilisées toomonitor des requêtes individuelles et les problèmes de toodiagnose avec un service de stockage. Les demandes sont enregistrées sur la base du meilleur effort.

Les entrées de journal sont créées uniquement s'il existe une activité du service de stockage. Par exemple, si un compte de stockage a l’activité dans son service Blob, mais pas dans ses services de Table ou de la file d’attente, seuls les journaux appartenant toohello service Blob seront créés.

La journalisation Storage Analytics n’est pas disponible pour le stockage de fichiers Azure.

### <a name="logging-authenticated-requests"></a>Enregistrement des demandes authentifiées
Hello, les types de demandes authentifiées suivants est enregistré :

* Demandes ayant réussi.
* Demandes ayant échoué, y compris les erreurs de délai d'expiration, limitation, réseau, autorisation et autres erreurs.
* Demandes utilisant une signature d'accès partagé (SAS), y compris les demandes ayant réussi et ayant échoué.
* Demande des données tooanalytics.

Les demandes effectuées par Storage Analytics lui-même, telles que la création ou la suppression d'un journal, ne sont pas enregistrées. Une liste complète des données de salutation connectée est documentée dans hello [les Messages d’état et les opérations de journalisation de stockage Analytique](https://msdn.microsoft.com/library/hh343260.aspx) et [le Format de journal Analytique stockage](https://msdn.microsoft.com/library/hh343259.aspx) rubriques.

### <a name="logging-anonymous-requests"></a>Journalisation des demandes anonymes
Hello, les types de demandes anonymes suivants est enregistré :

* Demandes ayant réussi.
* Erreurs de serveur.
* Erreurs de délai d'expiration pour le client et le serveur.
* Demandes GET ayant échoué avec le code d'erreur 304 (non modifié).

Aucune autre demande anonyme ayant échoué n'est enregistrée. Une liste complète des données de salutation connectée est documentée dans hello [les Messages d’état et les opérations de journalisation de stockage Analytique](https://msdn.microsoft.com/library/hh343260.aspx) et [le Format de journal Analytique stockage](https://msdn.microsoft.com/library/hh343259.aspx) rubriques.

### <a name="how-logs-are-stored"></a>Mode de stockage des journaux
Tous les journaux sont stockés dans des objets blob de blocs dans un conteneur nommé $logs, qui est automatiquement créé lorsque Storage Analytics est activé pour un compte de stockage. conteneur de Hello $logs se trouve dans l’espace de noms blob hello hello du compte de stockage, par exemple : `http://<accountname>.blob.core.windows.net/$logs`. Ce conteneur ne peut pas être supprimé une fois Storage Analytics activé, mais son contenu peut l'être.

> [!NOTE]
> conteneur de Hello $logs n’est pas affiché lors d’une opération de liste de conteneurs, tels que hello [ListContainers](https://msdn.microsoft.com/library/azure/dd179352.aspx) (méthode). Vous devez y accéder directement. Par exemple, vous pouvez utiliser hello [ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx) méthode tooaccess hello des objets BLOB hello `$logs` conteneur.
> À mesure que des demandes sont enregistrées, Storage Analytics télécharge les résultats intermédiaires en tant que blocs. Périodiquement, Storage Analytics valide ces blocs et les rend accessibles sous forme d'objets blob.
> 
> 

Enregistrements en double peuvent exister pour les journaux créés Bonjour la même heure. Vous pouvez déterminer si un enregistrement est un double en vérifiant hello **RequestId** et **opération** nombre.

### <a name="log-naming-conventions"></a>Conventions d'appellation de journal
Chaque journal est écrit dans hello suivant le format.

    <service-name>/YYYY/MM/DD/hhmm/<counter>.log

Hello tableau suivant décrit chaque attribut de nom de journal hello.

| Attribut | Description |
| --- | --- |
| <service-name> |nom Hello hello du service de stockage. Par exemple : blob, table ou file d'attente. |
| YYYY |année à quatre chiffres de Hello pour les journaux hello. Par exemple : 2011. |
| MM |mois à deux chiffres de Hello pour les journaux hello. Par exemple : 07. |
| DD |mois à deux chiffres de Hello pour les journaux hello. Par exemple : 07. |
| hh |heure à deux chiffres Hello indiquant hello commence heure hello pour les journaux, au format de 24 heures UTC. Par exemple : 18. |
| MM |nombre à deux chiffres Hello indiquant hello démarrage minute pour les journaux de hello. Cette valeur est pris en charge dans la version actuelle de hello de stockage Analytique, et sa valeur sera toujours 00. |
| <counter> |Compteur de base zéro avec six chiffres qui indique le nombre de hello d’objets BLOB de journal générée pour le service de stockage hello dans une période d’heure. Ce compteur commence à 000000. Par exemple : 000001. |

Hello Voici un nom de journal exemple complet qui combine les exemples précédents hello.

    blob/2011/07/31/1800/000001.log

Hello Voici un exemple d’URI qui peut être utilisé tooaccess journal précédent si hello.

    https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log

Lorsqu’une demande de stockage est enregistrée, nom de journal résultant hello met en corrélation l’heure toohello lorsque hello a demandé l’opération s’est terminée. Par exemple, si une demande GetBlob a été traitée à 18 h 30 31/7/2011, hello journal est écrit avec hello préfixe :`blob/2011/07/31/1800/`

### <a name="log-metadata"></a>Métadonnées du journal
Tous les objets BLOB de journal sont stockés avec des métadonnées qui peuvent être utilisé tooidentify à quel objet blob de journalisation des données hello contient. Hello tableau suivant décrit chaque attribut de métadonnées.

| Attribut | Description |
| --- | --- |
| LogType |Décrit si journal de hello contient des informations concernant les opérations de suppression, d’écriture ou tooread. Cette valeur peut inclure un type ou une combinaison des trois, séparés par des virgules. Exemple 1 : write ; Exemple 2 : read,write ; Exemple 3 : read,write,delete. |
| StartTime |Hello tôt d’une entrée de journal hello, hello format AAAA-MM-JJThh. Par exemple : 2011-07-31T18:21:46Z. |
| EndTime |Hello dernière heure d’une entrée de journal hello, hello format AAAA-MM-JJThh. Par exemple : 2011-07-31T18:22:09Z. |
| LogVersion |version de Hello du format de journal hello. Actuellement, valeur de hello uniquement pris en charge est 1.0. |

Hello liste suivante affiche les métadonnées exemple complet à l’aide des exemples précédents de hello.

* LogType=write
* StartTime=2011-07-31T18:21:46Z
* EndTime=2011-07-31T18:22:09Z
* LogVersion=1.0

### <a name="accessing-logging-data"></a>Accès aux données de journalisation
Toutes les données de hello `$logs` conteneur sont accessibles à l’aide des API du service Blob hello, notamment hello API .NET fournies par hello Azure managée bibliothèque. administrateur de compte de stockage Hello pour lire et supprimer les journaux, mais ne peut pas créer ou mettre à jour. Les métadonnées du journal hello et nom du fichier journal peuvent être utilisés lors de l’interrogation d’un journal. Il est possible pour tooappear de journaux d’une heure donnée en désordre, mais les métadonnées hello spécifient toujours timespan hello des entrées de journal dans un journal. Par conséquent, vous pouvez utiliser une combinaison de noms de journaux et de métadonnées lors de la recherche d'un journal particulier.

## <a name="about-storage-analytics-metrics"></a>À propos des métriques de Storage Analytics
Stockage Analytique peut stocker des métriques qui incluent des données de la capacité et les statistiques groupées des transactions sur le service de stockage tooa de demandes. Les transactions sont déclarées au niveau opération hello API ainsi qu’au niveau de service de stockage hello, et la capacité est signalée au niveau de service de stockage hello. Les données de métriques peuvent être des tooanalyze utilisé d’utilisation de service de stockage, diagnostiquer les problèmes avec les demandes effectuées sur le service de stockage hello et les performances de hello tooimprove des applications qui utilisent un service.

toouse Analytique de stockage, vous devez l’activer individuellement pour chaque service, vous souhaitez toomonitor. Vous pouvez l’activer à partir de hello [Azure Portal](https://portal.azure.com). Pour plus d’informations, consultez [surveiller un compte de stockage Bonjour Azure Portal](storage-monitor-storage-account.md). Vous pouvez également activer Analytique de stockage par programme via l’API REST de hello ou de la bibliothèque cliente de hello. Hello d’utilisation **obtenir les propriétés de Service** opérations tooenable Analytique de stockage pour chaque service.

### <a name="transaction-metrics"></a>Métriques de transaction
Un ensemble fiable de données est enregistré toutes les heures ou chaque minute pour chaque service de stockage et opération d'API demandée, notamment les entrées/sorties, la disponibilité, les erreurs et les pourcentages de demande triés par catégorie. Vous pouvez voir une liste complète des détails de la transaction hello Bonjour [schéma de Table de métriques Storage Analytique](https://msdn.microsoft.com/library/hh343264.aspx) rubrique.

Les données de transaction sont enregistrées à deux niveaux : le niveau de service hello et niveau de l’opération API hello. Au niveau de service hello, statistiques résumant toutes les a demandé d’opérations d’API sont écrites entité de table tooa toutes les heures même si aucune demande n’a été apportée toohello service. Au niveau d’opération hello API, les statistiques sont tooan écrit uniquement entité si l’opération de hello a été demandée dans l’heure.

Par exemple, si vous effectuez un **GetBlob** opération sur votre service Blob, des indicateurs de stockage Analytique journaliser hello demande et l’inclure dans les données agrégée de hello pour les deux hello service Blob, ainsi que hello **GetBlob** opération. Toutefois, si aucun **GetBlob** est demandée pendant les heures hello, une entité ne pas être écrite toohello `$MetricsTransactionsBlob` pour cette opération.

Les métriques de transaction sont enregistrées pour les demandes utilisateur et les demandes effectuées par Storage Analytics. Par exemple, les demandes par stockage Analytique toowrite journaux et les entités de table sont enregistrés. Pour plus d'informations sur la façon dont ces demandes sont facturées, consultez [Storage Analytics et facturation](https://msdn.microsoft.com/library/hh360997.aspx).

### <a name="capacity-metrics"></a>Métriques de capacité
> [!NOTE]
> Actuellement, les métriques de capacité sont uniquement disponibles pour hello service Blob. Les métriques de capacité pour le service de Table hello et le service de file d’attente seront disponibles dans les versions futures de stockage Analytique.
> 
> 

Les données de capacité sont enregistrées quotidiennement pour le service BLOB d’un compte de stockage, et deux entités de table sont écrites. Une entité fournit des statistiques pour les données utilisateur et hello autres fournit des statistiques sur hello `$logs` conteneur d’objets blob utilisé par stockage Analytique. Hello `$MetricsCapacityBlob` table inclut hello suivant statistiques :

* **Capacité**: quantité hello de stockage utilisé par le service Blob du compte de stockage hello, en octets.
* **ContainerCount**: hello le nombre de conteneurs d’objets blob dans le service Blob du compte de stockage hello.
* **ObjectCount**: hello nombre de BLOB de blocs ou de pages validés et non validés dans le service Blob du compte de stockage hello.

Pour plus d’informations sur les métriques de capacité hello, consultez [schéma de Table de métriques Storage Analytique](https://msdn.microsoft.com/library/hh343264.aspx).

### <a name="how-metrics-are-stored"></a>Stockage des métriques
Toutes les données de métriques pour chacun des services de stockage hello sont stockées dans trois tables réservées à ce service : une table pour les informations de transaction, une table pour les informations sur les transactions par minute et une autre table pour les informations de capacité. Les informations relatives aux transactions et aux transactions par minute se composent des données de demande et de réponse, et les informations de capacité se composent des données d'utilisation du stockage. Les métriques par heure, métriques par minute et la capacité d’un service d’objets Blob d’un compte de stockage sont accessibles dans les tables qui sont nommées comme décrit dans hello tableau suivant.

| Niveau de métriques | Noms de tables | Versions prises en charge |
| --- | --- | --- |
| Métriques toutes les heures, emplacement principal |$MetricsTransactionsBlob  <br/>$MetricsTransactionsTable <br/> $MetricsTransactionsQueue |Les versions antérieures too2013-08-15 uniquement. Ces noms sont toujours prises en charge, il est recommandé que vous basculez les tables de hello toousing répertoriées ci-dessous. |
| Métriques toutes les heures, emplacement principal |$MetricsHourPrimaryTransactionsBlob <br/>$MetricsHourPrimaryTransactionsTable <br/>$MetricsHourPrimaryTransactionsQueue |Toutes les versions, y compris celle du 15 août 2013. |
| Métriques par minute, emplacement principal |$MetricsMinutePrimaryTransactionsBlob <br/>$MetricsMinutePrimaryTransactionsTable <br/>$MetricsMinutePrimaryTransactionsQueue |Toutes les versions, y compris celle du 15 août 2013. |
| Métriques toutes les heures, emplacement secondaire |$MetricsHourSecondaryTransactionsBlob  <br/>$MetricsHourSecondaryTransactionsTable <br/>$MetricsHourSecondaryTransactionsQueue |Toutes les versions, y compris celle du 15 août 2013. La géo-réplication redondante avec accès en lecture doit être activée. |
| Métriques par minute, emplacement secondaire |$MetricsMinuteSecondaryTransactionsBlob  <br/>$MetricsMinuteSecondaryTransactionsTable <br/>$MetricsMinuteSecondaryTransactionsQueue |Toutes les versions, y compris celle du 15 août 2013. La géo-réplication redondante avec accès en lecture doit être activée. |
| Capacité (service Blob uniquement) |$MetricsCapacityBlob |Toutes les versions, y compris celle du 15 août 2013. |

Ces tables sont automatiquement créées lorsque Storage Analytics est activé pour un compte de stockage. Ils sont accessibles via l’espace de noms hello hello du compte de stockage, par exemple :`https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`

### <a name="accessing-metrics-data"></a>Accès aux données de métriques
Toutes les données dans les tables de métriques hello sont accessibles à l’aide des API de service de Table hello, notamment hello API .NET fournies par hello Azure managée bibliothèque. administrateur de compte de stockage Hello pour lire et supprimer des entités de table, mais ne peut pas créer ou mettre à jour.

## <a name="billing-for-storage-analytics"></a>Facturation pour Storage Analytics
Toutes les données de métriques sont écrites par les services de hello d’un compte de stockage. En conséquence, chaque opération d'écriture effectuée par Storage Analytics est facturable. En outre, hello quantité de stockage utilisé par les données de métriques est également facturable.

Hello suit les actions effectuées par stockage Analytique est facturable :

* Toocreate d’objets BLOB pour la journalisation pour la demande. 
* Entités de table demandes toocreate pour les mesures.

Si vous avez configuré une stratégie de rétention des données, vous n'êtes pas facturé pour les transactions de suppression lorsque Storage Analytics supprime les anciennes données de journalisation et de métriques. Toutefois, les transactions de suppression d'un client sont facturables. Pour plus d'informations sur les stratégies de rétention, consultez [Définition d'une stratégie de rétention des données Storage Analytics](https://msdn.microsoft.com/library/azure/hh343263.aspx).

### <a name="understanding-billable-requests"></a>Présentation des demandes facturables
Chaque demande adressée service de stockage du compte tooan est facturable ou non facturable. Stockage Analytique enregistre chaque demande individuelle effectuée tooa service, y compris un message d’état qui indique les modalités de demande de hello. De même, Analytique de stockage stocke des métriques pour les opérations d’API de service et de hello de ce service, y compris les pourcentages de hello et le nombre de certains messages d’état. Ensemble, ces fonctionnalités peuvent vous aider à analyser vos demandes facturables, apporter des améliorations dans votre application et diagnostiquer les problèmes avec les services de tooyour de demandes. Pour plus d'informations sur la facturation, consultez [Présentation de la facturation d’Azure Storage - bande passante, transactions et capacité](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

En examinant les données Analytique de stockage, vous pouvez utiliser les tables hello Bonjour [les Messages d’état et les opérations de journalisation de stockage Analytique](https://msdn.microsoft.com/library/azure/hh343260.aspx) toodetermine rubrique identifier les demandes qui sont facturables. Vous pouvez ensuite comparer vos journaux et les mesures données toohello état messages toosee si vous avez été facturé pour une requête particulière. Vous pouvez également utiliser des tables de hello hello précédente rubrique tooinvestigate groupe à haute disponibilité pour un service de stockage ou d’une opération individuelle de l’API.

## <a name="next-steps"></a>Étapes suivantes
### <a name="setting-up-storage-analytics"></a>Configuration de Storage Analytics
* [Surveillance d’un compte de stockage Bonjour portail Azure](storage-monitor-storage-account.md)
* [Activation et configuration de Storage Analytics](https://msdn.microsoft.com/library/hh360996.aspx)

### <a name="storage-analytics-logging"></a>Journalisation Storage Analytics
* [À propos de la journalisation Storage Analytics](https://msdn.microsoft.com/library/hh343262.aspx)
* [Format de journal de Storage Analytics](https://msdn.microsoft.com/library/hh343259.aspx)
* [Opérations et messages d'état enregistrés Storage Analytics](https://msdn.microsoft.com/library/hh343260.aspx)

### <a name="storage-analytics-metrics"></a>Métriques de Storage Analytics
* [À propos des métriques de Storage Analytics](https://msdn.microsoft.com/library/hh343258.aspx)
* [Schéma de table de métriques Storage Analytics](https://msdn.microsoft.com/library/hh343264.aspx)
* [Opérations et messages d'état enregistrés Storage Analytics](https://msdn.microsoft.com/library/hh343260.aspx)  

