---
title: aaaFix une erreur de connexion SQL, erreur temporaire | Documents Microsoft
description: "Découvrez comment tootroubleshoot, diagnostiquer et empêcher une erreur de connexion SQL ou d’une erreur temporaire dans la base de données SQL Azure. "
keywords: "connexion SQL,chaîne de connexion,problèmes de connectivité,erreur temporaire,erreur de connexion"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a>Diagnostiquer, résoudre et empêcher les erreurs de connexion SQL et les erreurs temporaires de Base de données SQL
Cet article décrit comment tooprevent, résoudre les problèmes, diagnostiquer et limiter les erreurs de connexion et les erreurs temporaires que votre application cliente rencontre lorsqu’il interagit avec la base de données SQL Azure. Découvrez comment tooconfigure logique de nouvelle tentative, générer la chaîne de connexion hello et ajuster d’autres paramètres de connexion.

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a>Erreurs temporaires
Une erreur temporaire s’explique par une cause sous-jacente qui se résout d’elle-même en peu de temps. Une cause occasionnelle d’erreurs temporaires est hello système Azure déplace rapidement matériel ressources toobetter l’équilibrage de charge différentes charges de travail. La plupart de ces événements de reconfiguration se terminent souvent en moins de 60 secondes. Pendant ce laps de temps reconfiguration, peut avoir une connectivité émet tooAzure base de données SQL. Les applications se connectant tooAzure base de données SQL doit être générée tooexpect ces erreurs temporaires, handle en implémentant la logique dans leur code au lieu de les surfaces toousers comme des erreurs d’application de nouvelle tentative.

Si votre programme client utilise ADO.NET, votre programme est informé d’erreur temporaire de hello par throw hello d’un **SqlException**. Hello **nombre** propriété peut être comparée à la liste hello des erreurs temporaires haut hello de rubrique de hello : [codes d’erreur SQL pour les applications clientes de base de données SQL](sql-database-develop-error-messages.md).

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Connexion ou commande
Vous allez tentatives de connexion de SQL hello ou établir de nouveau, selon les éléments suivants de hello :

* **Une erreur temporaire se produit pendant une tentative de connexion**: connexion de hello doit être renouvelée après retarder pendant quelques secondes.
* **Une erreur temporaire se produit pendant une commande de requête SQL**: commande hello ne doit pas être réessayée immédiatement. Au lieu de cela, après un délai de connexion de hello fraîchement convient. Commande hello peut être retentée.

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a>Logique de nouvelle tentative pour les erreurs temporaires
Les programmes clients qui rencontrent occasionnellement une erreur temporaire sont plus solides lorsqu’ils contiennent une logique de nouvelle tentative.

Lorsque votre programme communique avec la base de données SQL Azure via un intergiciel (middleware) tiers 3e, obtenir des informations auprès du fournisseur de hello si hello intergiciel (middleware) contient la logique de nouvelle tentative pour les erreurs temporaires.

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a>Principes de nouvelle tentative
* Une tentative de tooopen une connexion doit être renouvelé si l’erreur de hello est temporaire.
* Une instruction SQL SELECT qui échoue avec une erreur temporaire ne doit pas être retentée directement.
  
  * Au lieu de cela, établir une nouvelle connexion et recommencez hello SELECT.
* Lorsqu’une instruction SQL UPDATE échoue avec une erreur temporaire, une nouvelle connexion doit être établie avant nouvelle tentative de mise à jour de hello.
  
  * logique de nouvelle tentative Hello doit s’assurer que, soit en utilisant transaction de base de données entière hello terminée que hello ensemble de la transaction est restaurée.

#### <a name="other-considerations-for-retry"></a>Autres considérations
* Un programme de traitement par lots qui est démarré automatiquement après les heures de travail, et qui s’achève avant matin, supportent patient toovery avec des périodes de temps entre les nouvelles tentatives.
* Un programme de l’interface utilisateur doit prendre en compte hello tendance toogive d’après une attente de trop longue.
  
  * Toutefois, hello solution ne doit pas être tooretry après quelques secondes, car cette stratégie peut inonder le système hello avec des requêtes.

#### <a name="interval-increase-between-retries"></a>Augmentation de l’intervalle entre les tentatives
Nous vous recommandons de patienter 5 secondes avant votre première tentative. Une nouvelle tentative après un délai inférieur à 5 secondes risque de service de cloud hello insurmontable. Pour chaque nouvelle tentative ultérieure délai de hello doit croître de manière exponentielle, jusqu'à tooa maximale de 60 secondes.

En savoir plus sur hello *la période de blocage* pour les clients qui utilisent ADO.NET est disponible dans [le regroupement de connexion SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

Vous pouvez également vous tooset un nombre maximal de tentatives avant que le programme de hello s’arrête automatiquement.

#### <a name="code-samples-with-retry-logic"></a>Exemples de code avec la logique de nouvelle tentative
Vous trouverez des exemples de code avec logique de nouvelle tentative dans divers langages de programmation ici :

* [Bibliothèques de connexions pour SQL Database et SQL Server](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a>Tester votre logique de nouvelle tentative
tootest votre logique de nouvelle tentative, vous devez simuler ou provoquer une erreur que peuvent être corrigées pendant que votre programme est en cours d’exécution.

##### <a name="test-by-disconnecting-from-hello-network"></a>En déconnectant hello réseau de test
Vous pouvez tester votre logique de nouvelle tentative consiste toodisconnect votre ordinateur client à partir de hello réseau pendant l’exécution du programme de hello. Erreur de Hello sera :

* **SqlException.Number** = 11001
* Message : « Hôte inconnu »

Comme tout d’abord, la partie de hello nouvelle tentative, votre programme peut corriger des fautes d’orthographe hello et tentez ensuite tooconnect.

toomake ce pratique, vous déconnecter votre ordinateur à partir du réseau de hello avant de commencer votre programme. Ensuite, votre programme reconnaît un paramètre d’exécution qui provoque hello du programme :

1. Ajoutez temporairement 11001 liste tooits des erreurs tooconsider comme temporaire.
2. Tente sa première connexion comme d’habitude.
3. Une fois l’erreur de hello est interceptée, supprimez 11001 hello liste.
4. Afficher un message indiquant l’ordinateur de hello tooplug hello utilisateur dans un réseau de hello.
   * Suspendre davantage d’exécution à l’aide soit hello **Console.ReadLine** méthode ou une boîte de dialogue avec un bouton OK. utilisateur de Hello appuie sur la touche hello une fois que l’ordinateur de hello connecté hello réseau.
5. Essayez à nouveau tooconnect, attendu de réussite.

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a>Lors de la connexion de test par le nom de base de données hello faute d’orthographe
Votre programme peut faire volontairement mal orthographié le nom d’utilisateur hello avant la première tentative de connexion hello. Erreur de Hello sera :

* **SqlException.Number** = 18456
* Message : « Échec de la connexion pour l’utilisateur 'WRONG_MyUserName' »

Comme tout d’abord, la partie de hello nouvelle tentative, votre programme peut corriger des fautes d’orthographe hello et tentez ensuite tooconnect.

toomake ce pratique, votre programme peut reconnaître un paramètre d’exécution qui provoque hello du programme :

1. Ajoutez temporairement 18456 liste tooits des erreurs tooconsider comme temporaire.
2. Ajouter volontairement les nom d’utilisateur toohello 'WRONG_'.
3. Une fois l’erreur de hello est interceptée, supprimez 18456 hello liste.
4. Supprimez 'WRONG_' hello nom d’utilisateur.
5. Essayez à nouveau tooconnect, attendu de réussite.

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a>Paramètres de connexion .NET Sql pour les nouvelles tentatives de connexion
Si votre programme client connecte tootooAzure base de données SQL à l’aide de la classe de .NET Framework hello **System.Data.SqlClient.SqlConnection**, vous devez utiliser .NET 4.6.1 ou version ultérieure (ou .NET Core) afin de vous pouvez tirer parti de sa fonctionnalité de nouvelle tentative de connexion. Détails de la fonctionnalité de hello sont [ici](http://go.microsoft.com/fwlink/?linkid=393996).

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


Lorsque vous générez hello [chaîne de connexion](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) pour votre **SqlConnection** de l’objet, vous devez coordonner les valeurs hello entre hello paramètres suivants :

* ConnectRetryCount &nbsp;&nbsp;*(La valeur par défaut est 1. La plage s’étend de 0 à 255.)*
* ConnectRetryInterval &nbsp;&nbsp;*(La valeur par défaut est 1 seconde. La plage s’étend de 1 à 60.)*
* Délai d’expiration de connexion &nbsp;&nbsp;*(La valeur par défaut est 15 secondes. La plage s’étend de 0 à 2147483647.)*

Plus précisément, vos valeurs choisies doivent rendre hello suivant true d’égalité :

* Délai d’expiration de connexion = ConnectRetryCount × ConnectionRetryInterval

Par exemple, si hello count = 3 et l’intervalle = 10 secondes, un délai d’expiration uniquement 29 secondes pas assez donnerait système de hello suffisamment de temps pour son nouvelle 3e et dernière tentative de connexion : 29 < 3 * 10.

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Connexion ou commande
Hello **ConnectRetryCount** et **ConnectRetryInterval** paramètres permettent de votre **SqlConnection** opération hello de nouvelle tentative d’objet de connexion sans indiquant ou déranger votre programme, telle que le programme de contrôle de tooyour de retour. nouvelles tentatives de Hello peuvent se produire dans hello suivant situations :

* Appel de méthode mySqlConnection.Open
* Appel de méthode mySqlConnection.Execute

Il existe une subtilité. Si une erreur temporaire se produit pendant que votre *requête* est en cours d’exécution, votre **SqlConnection** ne l’opération de connexion pas de nouvelle tentative hello et certainement qu’il ne tente pas de votre requête de l’objet. Toutefois, **SqlConnection** très rapidement les vérifications hello connexion avant d’envoyer votre requête pour l’exécution. Si la vérification rapide de hello détecte un problème de connexion, **SqlConnection** l’opération hello de nouvelles tentatives de connexion. Si la nouvelle tentative de hello réussit, vous interrogez est envoyé pour l’exécution.

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a>Le paramètre ConnectRetryCount doit-il être combiné avec la logique de nouvelle tentative d’application ?
Supposons que votre application possède une logique de nouvelle tentative personnalisée robuste. Il peut réessayer hello 4 fois l’opération de connexion. Si vous ajoutez **ConnectRetryInterval** et **ConnectRetryCount** = 3 tooyour chaîne de connexion, vous augmenterez too4 de nombre de nouvelles tentatives hello * 3 = 12 effectue une nouvelle tentative. Vous ne souhaitez peut-être pas un si grand nombre de nouvelles tentatives.

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a>TooAzure de connexions de base de données SQL
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a>Connexion : chaîne de connexion
chaîne de connexion Hello nécessaire pour la connexion tooAzure base de données SQL est légèrement différente de la chaîne hello pour la connexion tooMicrosoft SQL Server. Vous pouvez copier la chaîne de connexion hello pour votre base de données à partir de hello [portail Azure](https://portal.azure.com/).

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a>Connexion : adresse IP
Vous devez configurer hello de base de données SQL server tooaccept communication à partir de l’adresse IP de hello d’ordinateur hello qui héberge votre programme client. Pour ce faire, modification des paramètres de pare-feu hello via hello [portail Azure](https://portal.azure.com/).

Si vous oubliez d’adresse IP de hello tooconfigure, votre programme échouera avec un message d’erreur pratique qui indique les adresses IP nécessaires hello.

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

Pour plus d’informations, consultez [Procédure : configuration des paramètres du pare-feu sur SQL Database](sql-database-configure-firewall-settings.md)

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a>Connexion : ports
En règle générale, vous devez uniquement tooensure que le port 1433 est ouvert pour les communications sortantes sur ordinateur hello hébergeant programme client.

Par exemple, lorsque votre programme client est hébergé sur un ordinateur Windows, hello le pare-feu Windows sur l’ordinateur hôte de hello vous permet de tooopen le port 1433 :

1. Ouvrez le panneau de configuration de hello
2. &gt; Tous les éléments du Panneau de configuration
3. &gt; Pare-feu Windows
4. &gt; Paramètres avancés
5. &gt; Règles de trafic sortant
6. &gt; Actions
7. &gt; Nouvelle règle

Si votre programme client est hébergé sur une machine virtuelle Azure, consultez <br/>[Ports au-delà de 1433 pour ADO .NET 4.5 et SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).

Pour obtenir des informations générales sur la configuration des ports et l’adresse IP, voir [Pare-feu Azure SQL Database](sql-database-firewall-configure.md)

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a>Connexion : ADO.NET 4.6.1
Si votre programme utilise les classes ADO.NET comme **System.Data.SqlClient.SqlConnection** tooconnect tooAzure base de données SQL, nous vous recommandons d’utiliser .NET Framework version 4.6.1 ou une version ultérieure.

ADO.NET 4.6.1 :

* Pour la base de données SQL Azure, il existe une meilleure fiabilité, lorsque vous ouvrez une connexion à l’aide de hello **SqlConnection.Open** (méthode). Hello **ouvrir** méthode intègre désormais une meilleure mécanismes de nouvelle tentative efforts dans les erreurs de tootransient de réponse, pour certaines erreurs au sein de la période de délai de connexion hello.
* Prend en charge le regroupement de connexions. Cela inclut une vérification efficace qui hello connexion fonctionne objet il donne à votre programme.

Lorsque vous utilisez un objet de connexion à partir d’un pool de connexions, nous recommandons que votre programme Fermez temporairement les connexion hello lorsque vous l’utilisez pas immédiatement. Ouvrir une connexion n’est pas coûteuse hello création d’une connexion consiste.

Si vous utilisez ADO.NET 4.0 ou version antérieure, nous vous conseillons toohello dernière ADO.NET.

* Depuis novembre 2015, [ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx)est disponible au téléchargement.

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a>Diagnostics
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a>Diagnostic : vérifier si les utilitaires peuvent se connecter
Si votre programme échoue tooconnect tooAzure base de données SQL, une option de diagnostic est tooconnect tootry avec un programme de l’utilitaire. Dans l’idéal, l’utilitaire de hello se connecte à l’aide de hello même bibliothèque que votre programme utilise.

Sur un ordinateur Windows, vous pouvez essayer ces utilitaires :

* SQL Server Management Studio (ssms.exe), qui se connecte à l’aide d’ADO.NET.
* sqlcmd.exe, qui se connecte à l’aide d’ [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).

Une fois connecté, faites un test avec une courte requête SQL SELECT.

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a>Diagnostics : Vérifiez les ports ouverts hello
Supposons que vous pensez que les tentatives de connexion échouent en raison de problèmes de tooport. Sur votre ordinateur, vous pouvez exécuter un utilitaire qui génère un rapport sur les configurations de port hello.

Sur Linux hello utilitaires suivants peuvent être utiles :

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * (Remplacez hello exemple valeur toobe votre adresse IP.)

Sur Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utilitaire peut être utile. Voici une exécution de l’exemple qui interrogées situation de port hello sur un serveur de base de données SQL Azure, et qui a été exécuté sur un ordinateur portable :

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a>Diagnostic : consignation des erreurs dans un journal
Un problème intermittent est parfois mieux diagnostiqué par la détection d’une tendance générale observée sur plusieurs jours ou semaines.

Votre client peut aider à consigner toutes les erreurs qu’il rencontre un diagnostic. Vous pouvez être entrées de journal en mesure de toocorrelate hello avec les données d’erreur base de données SQL Azure se connecte lui-même en interne.

Enterprise Library 6 (EntLib60) offre tooassist de classes managée .NET avec la journalisation :

* [5 - en tant que simple comme relevant hors tension un journal : à l’aide de hello bloc d’Application de journalisation](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a>Diagnostics : examinez les journaux d’erreur système
Voici certaines instructions Transact-SQL SELECT qui permettent d’interroger les journaux d’erreur et d’autres informations.

| Interrogation de journaux | Description |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |Hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) affichage propose des informations sur les événements individuels, y compris celles qui peut provoquer des erreurs temporaires ou des défaillances de connectivité.<br/><br/>Dans l’idéal, vous pouvez mettre en corrélation hello **heure_début** ou **end_time** valeurs avec des informations lorsque votre programme client a rencontré des problèmes.<br/><br/>**Conseil :** vous devez vous connecter toohello **master** de base de données toorun cela. |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |Hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) affichage offre le décompte agrégé des types d’événements de diagnostic supplémentaires.<br/><br/>**Conseil :** vous devez vous connecter toohello **master** de base de données toorun cela. |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a>Diagnostics : Rechercher des événements de problème dans le journal de base de données SQL hello
Vous pouvez rechercher des entrées sur les événements du problème dans le journal hello de base de données SQL Azure. Essayez de hello suivant l’instruction Transact-SQL SELECT Bonjour **master** base de données :

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a>quelques-unes d’entre elles ont renvoyé des lignes de sys.fn_xe_telemetry_blob_target_read_file
Vous trouverez plus loin une ligne renvoyée qui ressemble à ce qui suit . les valeurs null Hello indiquées ne sont pas souvent null dans d’autres lignes.

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a>Enterprise Library 6
Enterprise Library 6 (EntLib60) est une infrastructure de classes .NET qui vous permet d’implémenter des clients robustes de services de cloud computing, y compris service de base de données SQL Azure hello. Vous pouvez localiser la zone tooeach dédié de rubriques dans lequel EntLib60 peut aider en premier sur le site :

* [Enterprise Library 6 - avril 2013](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

La logique de nouvelle tentative pour la gestion des erreurs temporaires est un domaine où EntLib60 peut être utile :

* [4 - perseverance, le Secret de toutes les luttes : à l’aide de hello bloc applicatif de défaillance de gestion](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> Hello code source pour EntLib60 est disponible pour le public [télécharger](http://go.microsoft.com/fwlink/p/?LinkID=290898). Microsoft n’a aucune fonctionnalité supplémentaire de plans toomake mises à jour ou la maintenance des mises à jour tooEntLib.
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a>Classes EntLib60 pour les erreurs temporaires et les nouvelles tentatives
Hello EntLib60 classes suivantes est particulièrement utile pour la logique de nouvelle tentative. Tous ces sont dans ou sont encore plus sous, hello d’espace de noms **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:

*Dans l’espace de noms hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*

* **RetryPolicy**
  
  * **ExecuteAction**
* **ExponentialBackoff**
* **SqlDatabaseTransientErrorDetectionStrategy**
* **ReliableSqlConnection**
  
  * **ExecuteCommand**

Dans l’espace de noms hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:

* **AlwaysTransientErrorDetectionStrategy**
* **NeverTransientErrorDetectionStrategy**

Voici tooinformation liens sur EntLib60 :

* Libre [télécharger de Book : tooMicrosoft Guide du développeur Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)
* Meilleures pratiques : [Conseils généraux sur les nouvelles tentatives](../best-practices-retry-general.md) comprend une excellente présentation approfondie de la logique de nouvelle tentative.
* Téléchargement NuGet de [Bibliothèque d’entreprise - Bloc applicatif de gestion des erreurs 6.0 temporaires de Microsoft](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a>EntLib60 : bloc de journalisation hello
* bloc de journalisation Hello est une solution souple et configurable qui vous permet de :
  
  * Créer et stocker des messages du journal dans de nombreux emplacements.
  * Classer et filtrer les messages.
  * Recueillir des informations contextuelles utiles pour le débogage et le suivi, ainsi que pour les exigences d’audit et de journalisation en général.
* bloc de journalisation Hello résume hello journalisation des fonctionnalités à partir de la destination du journal hello afin que le code de l’application hello est cohérent, quelle que soit l’emplacement de hello et le type de banque de journalisation hello cible.

Pour plus d’informations, consultez : [5 - en tant que simple comme relevant hors tension un journal : à l’aide de hello bloc d’Application de journalisation](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a>Code source de la méthode EntLib60 IsTransient
Ensuite, à partir de hello **SqlDatabaseTransientErrorDetectionStrategy** de classe, est le code source hello c# hello **IsTransient** (méthode). code source de Hello clarifie les erreurs ont été analysés toobe temporaire et worthy de nouvelle tentative, à compter d’avril 2013.

Nombreuses **//comment** lignes ont été supprimées de cette lisibilité tooemphasize de copie.

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a>Étapes suivantes
* Pour le dépannage d’autres problèmes de connexion de base de données SQL Azure courants, visitez [connexion de résoudre les problèmes tooAzure base de données SQL](sql-database-troubleshoot-common-connection-issues.md).
* [Regroupement de connexions SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [*Une nouvelle tentative* est une Apache 2.0 concédé sous licence général d’une nouvelle tentative de la bibliothèque, écrite **Python**, tâche de hello toosimplify d’ajout de toojust de comportement de nouvelle tentative sur quoi que ce soit.](https://pypi.python.org/pypi/retrying)

