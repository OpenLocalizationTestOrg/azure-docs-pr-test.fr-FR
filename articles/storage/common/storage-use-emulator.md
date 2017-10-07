---
title: "émulateur de stockage Azure hello aaaUse pour le développement et test | Documents Microsoft"
description: "émulateur de stockage Azure Hello fournit un environnement de développement local libre pour développer et tester vos applications de stockage Azure. En savoir plus le mode d’authentification des demandes d’émulateur de toohello tooconnect à partir de votre application, et comment toouse hello outil de ligne de commande."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: f480b059-df8a-4a63-b05a-7f2f5d1f5c2a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: marsma
ms.openlocfilehash: 7cbe6ef5f172bb526c9d8a329b2fe9e6c0ec59d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-storage-emulator-for-development-and-testing"></a>Utiliser l’émulateur de stockage Azure hello pour le développement et test

l’émulateur de stockage Microsoft Azure Hello fournit un environnement local qui émule les services de Azure Blob, file d’attente et Table hello à des fins de développement. À l’aide de l’émulateur de stockage hello, vous pouvez tester votre application auprès des services de stockage hello localement, sans créer un abonnement Azure ou de subir les coûts. Lorsque vous êtes satisfait du fonctionne de votre application dans l’émulateur de hello, vous pouvez basculer toousing un compte de stockage Azure dans le cloud de hello.

## <a name="get-hello-storage-emulator"></a>Obtenir de l’émulateur de stockage hello
Hello émulateur de stockage est disponible dans le cadre de hello [Microsoft Azure SDK](https://azure.microsoft.com/downloads/). Vous pouvez également installer l’émulateur de stockage hello à l’aide de hello [programme d’installation autonome](https://go.microsoft.com/fwlink/?linkid=717179&clcid=0x409) (téléchargement direct). émulateur de stockage tooinstall hello, vous devez disposer des privilèges d’administrateur sur votre ordinateur.

actuellement, l’émulateur de stockage Hello s’exécute uniquement sous Windows. Pour ceux un émulateur de stockage pour Linux, une option est Communauté hello maintenue, émulateur de stockage open source [Azurite](https://github.com/arafato/azurite).

> [!NOTE]
> Les données créées dans une version de l’émulateur de stockage hello ne sont pas garanties toobe accessible lorsque vous utilisez une version différente. Si vous avez besoin à toopersist vos données à long terme la hello, nous vous recommandons de stocker ces données dans un compte de stockage Azure, plutôt que dans l’émulateur de stockage hello.
> <p/>
> l’émulateur de stockage Hello dépend des versions spécifiques de bibliothèques de OData hello. DLL d’OData hello utilisée par l’émulateur de stockage hello avec d’autres versions de remplacement non pris en charge et peut provoquer un comportement inattendu. Toutefois, n’importe quelle version d’OData prises en charge par le service de stockage hello peut être utilisé toosend demandes toohello émulateur.
>

## <a name="how-hello-storage-emulator-works"></a>Fonctionne de l’émulateur de stockage hello
l’émulateur de stockage Hello utilise une instance locale de Microsoft SQL Server et les services de stockage Azure tooemulate hello fichier local system. Par défaut, l’émulateur de stockage hello utilise une base de données dans Microsoft SQL Server 2012 Express LocalDB. Vous pouvez choisir tooconfigure hello stockage émulateur tooaccess une instance locale de SQL Server au lieu de l’instance de LocalDB hello. Pour plus d’informations, consultez hello [début et l’initialisation de l’émulateur de stockage hello](#start-and-initialize-the-storage-emulator) section plus loin dans cet article.

l’émulateur de stockage Hello connecte tooSQL serveur ou base de données locale à l’aide de l’authentification Windows.

Il existe quelques différences de fonctionnalités entre l’émulateur de stockage hello et les services de stockage Azure. Pour plus d’informations sur ces différences, consultez hello [les différences entre l’émulateur de stockage hello et le stockage Azure](#differences-between-the-storage-emulator-and-azure-storage) section plus loin dans cet article.

## <a name="start-and-initialize-hello-storage-emulator"></a>Démarrer et initialiser l’émulateur de stockage hello
émulateur de stockage Azure hello toostart :
1. Sélectionnez hello **Démarrer** hello bouton ou appuyez sur **Windows** clé.
1. Commencez à taper `Azure Storage Emulator`.
1. Sélectionnez les émulateur hello dans liste hello des applications affichées.

Au démarrage de l’émulateur de stockage hello, une fenêtre d’invite de commandes s’affiche. Vous pouvez utiliser cette console fenêtre toostart et arrêter hello émulateur de stockage, effacer les données, obtenir l’état et initialiser l’émulateur de hello. Pour plus d’informations, consultez hello [référence de l’outil de ligne de commande émulateur stockage](#storage-emulator-command-line-tool-reference) section plus loin dans cet article.

Lors de l’émulateur de hello est en cours d’exécution, vous verrez une icône Bonjour zone de notification de la barre des tâches Windows.

Lorsque vous fermez la fenêtre d’invite de commandes hello stockage émulateur, émulateur de stockage hello continue toorun. toobring la fenêtre de console l’émulateur de stockage hello suivez à nouveau, hello étapes précédentes, comme si vous démarriez l’émulateur de stockage hello.

Hello première fois que vous exécutez l’émulateur de stockage hello, environnement de stockage local hello est initialisé pour vous. processus d’initialisation Hello crée une base de données dans la base de données locale et réserve des ports HTTP pour chaque service de stockage local.

l’émulateur de stockage Hello est installé par défaut trop`C:\Program Files (x86)\Microsoft SDKs\Azure\Storage Emulator`.

> [!TIP]
> Vous pouvez utiliser hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork avec les ressources d’émulateur de stockage local. Recherchez « (Development) » sous « Comptes de stockage » dans l’arborescence de ressources de l’Explorateur de stockage de hello une fois que vous avez installé et démarré l’émulateur de stockage hello.
>

### <a name="initialize-hello-storage-emulator-toouse-a-different-sql-database"></a>Initialiser toouse émulateur de stockage hello une autre base de données SQL
Vous pouvez utiliser hello stockage émulateur outil de ligne de commande tooinitialize hello stockage émulateur toopoint tooa SQL de base de données instance autre que l’instance de LocalDB hello par défaut :

1. Fenêtre de console de l’émulateur de stockage hello ouverte comme décrit dans hello [début et l’initialisation de l’émulateur de stockage hello](#start-and-initialize-the-storage-emulator) section.
1. Dans la fenêtre de console hello, tapez Bonjour suivant de commande, où `<SQLServerInstance>` est le nom hello de l’instance de SQL Server hello. toouse LocalDB, spécifiez `(localdb)\MSSQLLocalDb` comme instance de SQL Server hello.

  `AzureStorageEmulator.exe init /server <SQLServerInstance>`

  Vous pouvez également utiliser hello commande, qui indique l’instance de SQL Server hello émulateur toouse hello par défaut suivante :

  `AzureStorageEmulator.exe init /server .\\`

  Ou bien, vous pouvez utiliser hello commande, qui réinitialise l’instance de base de données locale par défaut hello de base de données toohello suivante :

  `AzureStorageEmulator.exe init /forceCreate`

Pour plus d’informations sur ces commandes, consultez la section [Référence de l’outil en ligne de commande de l’émulateur de stockage](#storage-emulator-command-line-tool-reference).

> [!TIP]
> Vous pouvez utiliser hello [Microsoft SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) toomanage (SSMS) instances de votre serveur SQL Server, notamment l’installation de LocalDB hello. Bonjour SMSS **connecter tooServer** boîte de dialogue, spécifiez `(localdb)\MSSQLLocalDb` Bonjour **nom du serveur :** instance du champ tooconnect toohello base de données locale.

## <a name="authenticating-requests-against-hello-storage-emulator"></a>L’authentification des demandes sur l’émulateur de stockage hello
Une fois que vous avez installé et démarré l’émulateur de stockage hello, vous pouvez tester votre code par rapport à elle. Comme avec le stockage Azure dans le cloud de hello, chaque demande adressée par rapport à l’émulateur de stockage hello doit être authentifiée, sauf s’il est une demande anonyme. Vous pouvez authentifier les demandes sur l’émulateur de stockage à l’aide de l’authentification de clé partagée hello ou avec une signature d’accès partagé (SAS).

### <a name="authenticate-with-shared-key-credentials"></a>S’authentifier à l’aide d’informations d’identification de clé partagée
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

Pour plus d’informations sur les chaînes de connexion, consultez [Configuration des chaînes de connexion Stockage Azure](../storage-configure-connection-string.md).

### <a name="authenticate-with-a-shared-access-signature"></a>S’authentifier à l’aide d’une signature d’accès partagé
Certaines bibliothèques de client de stockage Azure, telle que la bibliothèque de Xamarin hello, prennent uniquement en charge l’authentification avec un jeton de signature (SAS) d’accès partagé. Vous pouvez créer un jeton SAS hello à l’aide d’un outil tel que hello [Explorateur de stockage](http://storageexplorer.com/) ou une autre application qui prend en charge l’authentification Shared Key.

Vous pouvez également générer un jeton SAP à l’aide d’Azure PowerShell. Hello exemple suivant génère un jeton SAS avec le conteneur d’objets blob tooa toutes les autorisations :

1. Installez Azure PowerShell si vous n’avez pas encore (à l’aide de la version la plus récente de hello applets de commande PowerShell de Azure hello est recommandé). Pour connaître la procédure d’installation, consultez l’article [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps) (Installation et configuration d’Azure PowerShell).
2. Ouvrez Azure PowerShell et exécutez hello suivant de commandes, en remplaçant `ACCOUNT_NAME` et `ACCOUNT_KEY==` avec vos propres informations d’identification, et `CONTAINER_NAME` avec un nom de votre choix :

```powershell
$context = New-AzureStorageContext -StorageAccountName "ACCOUNT_NAME" -StorageAccountKey "ACCOUNT_KEY=="

New-AzureStorageContainer CONTAINER_NAME -Permission Off -Context $context

$now = Get-Date

New-AzureStorageContainerSASToken -Name CONTAINER_NAME -Permission rwdl -ExpiryTime $now.AddDays(1.0) -Context $context -FullUri
```

signature d’accès partagé qui en résulte Hello URI pour le nouveau conteneur de hello doit être similaire à :

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2015-07-08T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3Dsss
```

signature d’accès partagé Hello créé avec cet exemple n’est valide pendant un jour. signature de Hello accorde tooblobs d’un accès complet (lecture, écriture, suppression,) dans le conteneur de hello.

Pour plus d’informations sur les signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP)](../storage-dotnet-shared-access-signature-part-1.md).

## <a name="addressing-resources-in-hello-storage-emulator"></a>Adressage des ressources dans l’émulateur de stockage hello
les points de terminaison de service Hello pour l’émulateur de stockage hello sont différentes de celles d’un compte de stockage Azure. différence de Hello est, car l’ordinateur local de hello n’effectue pas de résolution de noms de domaine, nécessitant hello stockage émulateur points de terminaison toobe les adresses locales.

Lorsque vous adressez une ressource dans un compte de stockage Azure, vous utilisez hello suivant le schéma. nom du compte Hello fait partie du nom d’hôte URI hello et ressource hello adressée fait partie du chemin de l’URI hello :

`<http|https>://<account-name>.<service-name>.core.windows.net/<resource-path>`

Par exemple, hello URI suivant est une adresse valide pour un objet blob dans un compte de stockage Azure :

`https://myaccount.blob.core.windows.net/mycontainer/myblob.txt`

Toutefois, hello émulateur de stockage, car l’ordinateur local de hello n’effectue pas de résolution de noms de domaine, nom du compte hello fait partie du chemin d’accès URI de hello au lieu du nom d’hôte hello. Utilisez hello suivant le format d’URI pour une ressource dans l’émulateur de stockage hello :

`http://<local-machine-address>:<port>/<account-name>/<resource-path>`

Par exemple, hello adresse suivante peut être utilisée pour accéder à un objet blob dans l’émulateur de stockage hello :

`http://127.0.0.1:10000/myaccount/mycontainer/myblob.txt`

les points de terminaison de service Hello pour l’émulateur de stockage hello sont :

* Service BLOB : `http://127.0.0.1:10000/<account-name>/<resource-path>`
* Service de File d’attente : `http://127.0.0.1:10001/<account-name>/<resource-path>`
* Service de Table : `http://127.0.0.1:10002/<account-name>/<resource-path>`

### <a name="addressing-hello-account-secondary-with-ra-grs"></a>Adressage compte hello secondaire avec RA-GRS
Depuis la version 3.1, émulateur de stockage hello prend en charge la réplication géographique redondante avec accès en lecture (RA-GRS). Pour les ressources de stockage dans le cloud de hello et dans l’émulateur local de hello, vous pouvez accéder à l’emplacement secondaire de hello en ajoutant - nom du compte secondaire toohello. Par exemple, hello adresse suivante peut être utilisé pour accéder à un objet blob à l’aide de hello en lecture seule base de données secondaire dans l’émulateur de stockage hello :

`http://127.0.0.1:10000/myaccount-secondary/mycontainer/myblob.txt`

> [!NOTE]
> Pour l’accès par programme le toohello secondaire avec l’émulateur de stockage hello, utilisez hello bibliothèque cliente de stockage pour .NET version 3.2 ou ultérieure. Consultez hello [bibliothèque cliente Microsoft Azure Storage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx) pour plus d’informations.
>
>

## <a name="storage-emulator-command-line-tool-reference"></a>Référence de l’outil en ligne de commande de l’émulateur de stockage
À partir de la version 3.0, une fenêtre de console s’affiche lorsque vous démarrez hello émulateur de stockage. Utiliser la ligne de commande hello hello console fenêtre toostart et arrêter hello émulateur ainsi que la requête pour l’état et effectuer d’autres opérations.

> [!NOTE]
> Si vous avez hello Microsoft Azure compute emulator installé, une icône de barre d’état système s’affiche lorsque vous lancez l’émulateur de stockage de hello. Avec le bouton droit sur hello icône tooreveal un menu qui fournit un moyen graphique de toostart et arrêter l’émulateur de stockage de hello.
>
>

### <a name="command-line-syntax"></a>Syntaxe de la ligne de commande
`AzureStorageEmulator.exe [start] [stop] [status] [clear] [init] [help]`

### <a name="options"></a>Options
liste de hello tooview des options de type `/help` à l’invite de commandes hello.

| Option | Description | Commande | Arguments |
| --- | --- | --- | --- |
| **Start** |Démarre l’émulateur de stockage hello. |`AzureStorageEmulator.exe start [-inprocess]` |*-inprocess*: démarrer l’émulateur de hello hello processus en cours au lieu de créer un nouveau processus. |
| **Stop** |Émulateur de stockage hello s’arrête. |`AzureStorageEmulator.exe stop` | |
| **État** |Commander des photos hello l’état de l’émulateur de stockage hello. |`AzureStorageEmulator.exe status` | |
| **Clear** |Efface les données hello dans tous les services spécifiés sur la ligne de commande hello. |`AzureStorageEmulator.exe clear [blob] [table] [queue] [all]                                                    ` |*blob*: efface les données d’objet blob. <br/>*queue*: efface les données de file d’attente. <br/>*table*: efface les données de table. <br/>*all*: efface toutes les données de tous les services. |
| **Init** |Effectue une initialisation unique des tooset émulateur de hello. |<code>AzureStorageEmulator.exe init [-server serverName] [-sqlinstance instanceName] [-forcecreate&#124;-skipcreate] [-reserveports&#124;-unreserveports] [-inprocess]</code> |*-server Nomserveur\nominstance*: Spécifie le serveur hello qui héberge l’instance SQL hello. <br/>*sqlinstance - instanceName*: Spécifie le nom hello de hello SQL instance toobe utilisé dans l’instance de serveur par défaut hello. <br/>*-forcecreate*: force la création de la base de données SQL hello, même s’il existe déjà. <br/>*-skipcreate*: ignore la création de la base de données SQL hello. Cet argument est prioritaire sur -forcecreate.<br/>*-reserveports*: tente de ports de hello HTTP tooreserve associés aux services de hello.<br/>*-unreserveports*: tente de réservations tooremove pour les ports hello HTTP associés aux services de hello. Cet argument est prioritaire sur -reserveports.<br/>*-inprocess*: effectue une initialisation dans le processus en cours hello au lieu de générer un nouveau processus. Si vous modifiez les réservations de port, les processus en cours Hello doivent être lancé avec des autorisations élevées. |

## <a name="differences-between-hello-storage-emulator-and-azure-storage"></a>Différences entre l’émulateur de stockage hello et le stockage Azure
Étant donné que l’émulateur de stockage hello est un environnement émulé en cours d’exécution dans une instance locale de SQL, il existe des différences de fonctionnalités entre l’émulateur de hello et un compte de stockage Azure dans le cloud de hello :

* l’émulateur de stockage Hello prend en charge un seul compte fixe et une clé d’authentification connue.
* l’émulateur de stockage Hello n’est pas un service de stockage évolutif et ne prend pas en charge un grand nombre de clients simultanés.
* Comme décrit dans [adresser les ressources dans l’émulateur de stockage hello](#addressing-resources-in-the-storage-emulator), les ressources sont adressées différemment dans l’émulateur de stockage hello par rapport à un compte de stockage Azure. Cette différence est, car la résolution de noms de domaine est disponible dans le cloud de hello, mais pas sur ordinateur local de hello.
* Depuis la version 3.1, le compte d’émulateur de stockage hello prend en charge la réplication géographique redondante avec accès en lecture (RA-GRS). Dans l’émulateur de hello, tous les comptes ont RA-GRS est activé, et il n’existe aucune latence entre les réplicas principal et secondaire hello. les opérations Get Blob Service Stats, obtenir des statistiques du Service file d’attente et obtenir des statistiques du Service Table Hello sont pris en charge sur le compte hello secondaire et renvoie toujours la valeur hello hello `LastSyncTime` élément de réponse comme hello sous-jacent au conséquente toohello des temps actuel Base de données SQL.
* Hello du service de fichiers et les points de terminaison service de protocole SMB ne sont pas pris en charge actuellement dans l’émulateur de stockage hello.
* Si vous utilisez une version des services de stockage hello qui n’est pas encore pris en charge par l’émulateur de hello, émulateur de stockage hello renvoie une erreur VersionNotSupportedByEmulator (code d’état HTTP 400 – demande incorrecte).

### <a name="differences-for-blob-storage"></a>Différences pour le stockage d’objets blob
Hello suivant différences applique tooBlob de stockage dans l’émulateur de hello :

* l’émulateur de stockage Hello prend uniquement en charge les tailles des objets blob des too2 go.
* Copie incrémentielle permet de captures instantanées de toobe BLOB remplacé copiés, ce qui retourne une erreur sur le service de hello.
* L’opération Get Page Ranges Diff ne fonctionne pas entre des instantanés copiés à l’aide de la copie incrémentielle d’objets blob.
* Une opération Put Blob peut réussir sur un objet blob qui existe dans l’émulateur de stockage hello avec un bail actif, même si l’ID de bail hello n’a pas été spécifié dans la demande hello.
* Ajouter des objets Blob opérations ne sont pas prises en charge par l’émulateur de hello. Toute tentative d’exécution d’une opération sur un objet blob d’ajout renvoie une erreur FeatureNotSupportedByEmulator (code d’état HTTP 400 – demande incorrecte).

### <a name="differences-for-table-storage"></a>Différences pour le stockage de tables
Hello suivant différences s’appliquent tooTable stockage dans l’émulateur de hello :

* Propriétés de date Bonjour service de Table dans l’émulateur de stockage hello prennent en charge la plage de hello uniquement pris en charge par SQL Server 2005 (ils sont au plus tard le 1er janvier 1753 toobe requis). Toutes les dates antérieures au 1er janvier 1753 sont modifiés toothis valeur. précision des dates Hello est précision toohello limitée de SQL Server 2005, ce qui signifie que les dates sont précises too1/300e de seconde.
* l’émulateur de stockage Hello prend en charge les valeurs de propriété de clé partition clé et de la ligne de moins de 512 octets chacune. En outre, hello taille totale du nom de compte hello, nom de la table et les noms de propriété de clé ensemble ne peut pas dépasser 900 octets.
* taille totale de Hello d’une ligne dans une table dans l’émulateur de stockage hello est accessible de sans limitée à 1 Mo.
* Dans l’émulateur de stockage hello, propriétés de données de type `Edm.Guid` ou `Edm.Binary` prise en charge uniquement hello `Equal (eq)` et `NotEqual (ne)` dans la requête, les opérateurs de comparaison des chaînes de filtrage.

### <a name="differences-for-queue-storage"></a>Différences pour le stockage de files d’attente
Il n’y a aucun stockage tooQueue spécifique de différences dans l’émulateur de hello.

## <a name="storage-emulator-release-notes"></a>Notes de publication de l’émulateur de stockage
### <a name="version-52"></a>Version 5.2
* l’émulateur de stockage Hello prend désormais en charge la version 2017-04-17 hello de services de stockage sur les points de terminaison de service Blob, file d’attente et Table.
* Correction d’un bogue impliquant le mauvais encodage des valeurs de propriété de table.

### <a name="version-51"></a>Version 5.1
* Correction d’un bogue dans lequel l’émulateur de stockage hello renvoyait hello `DataServiceVersion` en-tête dans certaines réponses où le service de hello n’a pas.

### <a name="version-50"></a>Version 5.0
* le programme d’installation de Hello stockage émulateur ne vérifie plus MSSQL existante et installe de .NET Framework.
* le programme d’installation de Hello stockage émulateur ne crée plus de la base de données hello dans le cadre de l’installation. Si nécessaire, la base de données sera toujours créée dans le cadre du démarrage.
* La création de la base de données ne nécessite plus une élévation de privilèges.
* Les réservations de ports ne sont plus nécessaires pour le démarrage.
* Ajoute hello options suivantes trop`init`: `-reserveports` (nécessite des privilèges élevés), `-unreserveports` (nécessite des privilèges élevés), `-skipcreate`.
* Hello option Storage Emulator UI sur l’icône de barre d’état système hello maintenant lance l’interface de ligne de commande hello. interface utilisateur graphique d’ancien Hello n’est plus disponible.
* Certaines DLL ont été supprimées ou renommées.

### <a name="version-46"></a>Version 4.6
* l’émulateur de stockage Hello prend désormais en charge la version 2016-05-31 hello de services de stockage sur les points de terminaison de service Blob, file d’attente et Table.

### <a name="version-45"></a>Version 4.5
* Correction d’un bogue qui a provoqué l’initialisation et l’installation de hello stockage émulateur toofail lorsque hello sauvegarde de base de données a été renommé.

### <a name="version-44"></a>Version 4.4
* l’émulateur de stockage Hello prend désormais en charge la version 2015-12-11 hello de services de stockage sur les points de terminaison de service Blob, file d’attente et Table.
* Hello nettoyage de l’émulateur de stockage des données blob est désormais plus efficace lorsque vous traitez avec un grand nombre d’objets BLOB.
* Correction d’un bogue qui a provoqué le conteneur toobe ACL XML validé légèrement différemment à partir de la façon dont le service de stockage hello fait.
* Correction d’un bogue qui entraînait parfois max et min DateTime valeurs toobe signalée dans le fuseau horaire incorrect de hello.

### <a name="version-43"></a>Version 4.3
* l’émulateur de stockage Hello prend désormais en charge la version 2015-07-08 hello de services de stockage sur les points de terminaison de service Blob, file d’attente et Table.

### <a name="version-42"></a>Version 4.2
* l’émulateur de stockage Hello prend désormais en charge la version 2015-04-05 hello de services de stockage sur les points de terminaison de service Blob, file d’attente et Table.

### <a name="version-41"></a>Version 4.1
* l’émulateur de stockage Hello prend désormais en charge la version 2015-02-21 hello de services de stockage sur l’objet Blob, file d’attente et Table de points de terminaison service, à l’exception des nouvelles fonctionnalités d’ajouter un objet Blob hello.
* Si vous utilisez une version des services de stockage hello qui n’est pas encore pris en charge par l’émulateur de hello, émulateur de hello renvoie un message d’erreur explicite. Nous recommandons d’utiliser la version la plus récente de l’émulateur de hello hello. Si vous rencontrez une erreur VersionNotSupportedByEmulator (code d’état HTTP 400 – demande incorrecte), téléchargez la version la plus récente de l’émulateur de stockage hello hello.
* Correction d’un bogue dans lequel une concurrence causé table entité données toobe incorrect lors des opérations de fusion simultanés.

### <a name="version-40"></a>Version 4.0
* l’émulateur de stockage Hello exécutable a été renommé trop*AzureStorageEmulator.exe*.

### <a name="version-32"></a>Version 3.2
* l’émulateur de stockage Hello prend désormais en charge la version 2014-02-14 des services de stockage hello sur les points de terminaison de service Blob, file d’attente et Table. Points de terminaison de service fichier ne sont pas pris en charge actuellement dans l’émulateur de stockage hello. Consultez [contrôle de version pour les Services de stockage Azure de hello](/rest/api/storageservices/Versioning-for-the-Azure-Storage-Services) pour plus d’informations sur la version 2014-02-14.

### <a name="version-31"></a>Version 3.1
* Stockage de géo-redondant avec accès en lecture (RA-GRS) est maintenant pris en charge dans l’émulateur de stockage hello. Get Table Service Stats API Hello Get Blob Service Stats et obtenir des statistiques du Service file d’attente sont pris en charge pour le compte hello secondaire et retournent toujours valeur hello d’élément de réponse LastSyncTime hello comme hello actuel toohello conséquente temps sous-jacent SQL base de données. Pour l’accès par programme le toohello secondaire avec l’émulateur de stockage hello, utilisez hello bibliothèque cliente de stockage pour .NET version 3.2 ou ultérieure. Pour plus d’informations, consultez hello bibliothèque cliente de Microsoft Azure Storage pour .NET Reference.

### <a name="version-30"></a>Version 3.0
* émulateur de stockage Azure Hello n’est plus inclu dans hello comme émulateur de calcul hello du même package.
* interface utilisateur graphique d’émulateur de stockage Hello est déconseillé en faveur d’une interface de ligne de commande scriptable. Pour plus d’informations sur l’interface de ligne de commande de hello, consultez la référence de l’outil de ligne de commande émulateur de stockage. interface graphique de Hello continuera toobe présent dans la version 3.0, mais il est accessible uniquement lors de l’émulateur de calcul de hello est installé en cliquant sur l’icône de barre d’état système hello et en sélectionnant Show Storage Emulator UI.
* La version 2013-08-15 des services de stockage Azure hello est maintenant entièrement pris en charge. (Auparavant, cette version était uniquement prise en charge par la version préliminaire de l’émulateur de stockage version 2.2.1.)

## <a name="next-steps"></a>Étapes suivantes

* Évaluer l’émulateur de stockage source ouvert gérée par la Communauté inter-plateformes hello [Azurite](https://github.com/arafato/azurite). 
* [Les exemples de stockage Azure à l’aide de .NET](../storage-samples-dotnet.md) contient des exemples de code tooseveral des liens vous pouvez utiliser lorsque vous développez votre application.
* Vous pouvez utiliser hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork avec des ressources dans votre compte de stockage cloud et dans l’émulateur de stockage hello.
