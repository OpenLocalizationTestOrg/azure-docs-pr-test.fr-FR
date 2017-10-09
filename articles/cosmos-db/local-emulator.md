---
title: "aaaDevelop localement avec hello Azure Cosmos DB émulateur | Documents Microsoft"
description: "À l’aide de hello Azure Cosmos DB émulateur, vous pouvez développer et tester votre application localement pour gratuitement, sans créer un abonnement Azure."
services: cosmos-db
documentationcenter: 
keywords: "Émulateur Azure Cosmos DB"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Utilisez hello Azure Cosmos DB émulateur pour développement local et le test

<table>
<tr>
  <td><strong>Fichiers binaires</strong></td>
  <td>[Télécharger MSI](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Docker Hub](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Source Docker</strong></td>
  <td>[Github](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
Bonjour Azure Cosmos DB émulateur fournit un environnement local qui émule hello service de base de données Azure Cosmos à des fins de développement. Hello Azure Cosmos DB émulateur vous pouvez de développer et tester votre application localement, sans créer un abonnement Azure ou de subir les coûts. Lorsque vous êtes satisfait de la façon dont votre application fonctionne Bonjour Azure Cosmos DB émulateur, vous pouvez basculer toousing un compte de base de données Azure Cosmos dans le cloud de hello.

Cet article traite des hello tâches suivantes : 

> [!div class="checklist"]
> * Lors de l’installation hello émulateur
> * Hello émulateur en cours d’exécution sur Docker pour Windows
> * Authentification des demandes
> * À l’aide de hello Explorateur de données dans l’émulateur de hello
> * Exportation de certificats SSL
> * Appel de hello émulateur à partir de la ligne de commande hello
> * Collecte des fichiers de trace

Nous vous recommandons de mise en route en regardant hello suivant vidéo, où Kirill Gavrylyuk montre comment tooget démarrer avec hello Azure Cosmos DB émulateur. Notez que la vidéo de hello sous l’appellation toohello émulateur hello DocumentDB émulateur, mais outil hello lui-même a été renommé Bonjour Azure Cosmos DB émulateur depuis touchant vidéo de hello. Toutes les informations Bonjour vidéo sont toujours exactes pour hello Azure Cosmos DB émulateur. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>Fonctionne de hello émulateur
Bonjour Azure Cosmos DB émulateur fournit une émulation haute fidélité de hello service de base de données Azure Cosmos. Il prend en charge les mêmes fonctionnalités qu’Azure Cosmos DB, notamment la prise en charge de la création et de l’interrogation des documents JSON, la configuration et la mise à l’échelle des collections, et l’exécution des procédures stockées et des déclencheurs. Vous pouvez développer et tester des applications à l’aide de hello Azure Cosmos DB émulateur et les déployer tooAzure à une échelle globale faisant simplement une seule configuration modifier le point de terminaison de connexion toohello pour la base de données Azure Cosmos.

Pendant que nous avons créé une émulation locale haute fidélité du service de base de données Azure Cosmos réel hello, implémentation hello Hello Azure Cosmos DB émulateur est différente de celui du service de hello. Par exemple, hello Azure Cosmos DB émulateur utilise les composants du système d’exploitation standard tels que système de fichiers local hello pour la persistance et la pile de protocole HTTPS pour la connectivité. Cela signifie que certaines fonctionnalités qui s’appuie sur l’infrastructure Azure telles que réplication globale, une latence chiffre millisecondes pour les lectures/écritures et les niveaux de cohérence paramétrables ne sont pas disponibles via hello Azure Cosmos DB émulateur.

> [!NOTE]
> À ce hello temps Explorateur de données Bonjour émulateur prend uniquement en charge la création des collections de l’API DocumentDB et MongoDB hello. Hello Explorateur de données dans l’émulateur de hello ne prend pas en charge la création de tables et graphiques hello. 

## <a name="system-requirements"></a>Conditions requises pour le système
Bonjour Azure Cosmos DB émulateur a hello suivant les exigences matérielles et logicielles :

* Configuration logicielle requise
  * Windows Server 2012 R2, Windows Server 2016 ou Windows 10
*   Conditions matérielles minimales requises
  * 2 Go de RAM
  * 10 Go d’espace disque disponible

## <a name="installation"></a>Installation
Vous pouvez télécharger et installer hello Azure Cosmos DB émulateur à partir de hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> tooinstall, configurer et exécuter hello Azure Cosmos DB émulateur, vous devez disposer des privilèges d’administrateur sur l’ordinateur de hello.

## <a name="running-on-docker-for-windows"></a>Exécution de Docker pour Windows

Bonjour Azure Cosmos DB émulateur peut être exécuté sur Docker pour Windows. Hello émulateur ne fonctionne pas sur Docker pour Oracle Linux.

Une fois que vous avez [Docker pour Windows](https://www.docker.com/docker-windows) installé, vous pouvez extraire image de l’émulateur hello à partir du Hub d’ancrage en exécutant hello de commande suivante à partir de votre favori interpréteur de commandes (cmd.exe, PowerShell, etc..).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
image de hello toostart, exécutez hello suivant les commandes.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

réponse de Hello semble similaire toohello suivantes :

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Fermeture hello shell interactif une fois hello émulateur a été démarré sera le conteneur de l’émulateur arrêt hello.

Utiliser le point de terminaison hello et la clé principale dans à partir de la réponse de hello dans votre client et importer le certificat SSL de hello dans votre hôte. tooimport hello certificat SSL, procédez comme hello suivant à partir d’une invite de commandes administrateur :

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>Démarrer l’émulateur de hello

toostart hello Azure Cosmos DB émulateur, sélectionnez le bouton Démarrer de hello ou appuyez sur Windows hello. Commencez à taper **Azure Cosmos DB émulateur**et l’émulateur hello select à partir de la liste des applications hello. 

![Sélectionnez hello bouton ou appuyez sur hello Windows touche, commencez à taper ** Azure Cosmos DB émulateur ** et émulateur hello select à partir de la liste des applications hello](./media/local-emulator/database-local-emulator-start.png)

Lors de l’émulateur de hello est en cours d’exécution, vous verrez une icône Bonjour zone de notification de la barre des tâches Windows. ![Notification dans la barre des tâches de l'émulateur local Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

Bonjour Azure Cosmos DB émulateur par défaut s’exécute sur l’ordinateur local hello (« localhost ») à l’écoute sur le port 8081.

Émulateur de base de données Azure Cosmos Hello est installé par défaut toohello `C:\Program Files\Azure Cosmos DB Emulator` active. Vous pouvez également démarrer et arrêter l’émulateur hello hello de ligne de commande. Pour plus d’informations, consultez la section [Référence de l’outil en ligne de commande](#command-line).

## <a name="start-data-explorer"></a>Démarrer l’Explorateur de données

Lancement de l’émulateur de base de données Azure Cosmos hello s’ouvre automatiquement hello Explorateur de données de base de données Azure Cosmos dans votre navigateur. adresse de Hello apparaîtront en tant que [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Si vous fermez hello explorer et aimeriez toore-open il ultérieurement, vous pouvez ouvrir les URL de hello dans votre navigateur ou lancer à partir de hello Azure Cosmos DB émulateur Bonjour icône Windows comme indiqué ci-dessous.

![Lanceur de l’Explorateur de données de l’émulateur local Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Recherche de mises à jour
L’Explorateur de données indique si une nouvelle mise à jour est disponible en téléchargement. 

> [!NOTE]
> Les données créées dans une version de hello Azure Cosmos DB émulateur ne sont pas garanties toobe accessible lorsque vous utilisez une version différente. Si vous avez besoin à toopersist vos données à long terme la hello, il est recommandé que vous stockez ces données dans un compte de base de données Azure Cosmos, plutôt que dans hello Azure Cosmos DB émulateur. 

## <a name="authenticating-requests"></a>Authentification des demandes
Tout comme avec la base de données Azure Cosmos dans le cloud de hello, chaque demande que vous apportez sur hello Azure Cosmos DB émulateur doit être authentifiée. Bonjour Azure Cosmos DB émulateur prend en charge un seul compte fixe et une clé d’authentification connu pour l’authentification de clé principale. Ce compte et la clé sont hello seules informations d’identification autorisées pour une utilisation avec hello Azure Cosmos DB émulateur. Il s'agit de :

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> clé principale de Hello pris en charge par hello Azure Cosmos DB émulateur est destinée à être utilisé uniquement avec l’émulateur de hello. Vous ne pouvez pas utiliser votre compte de base de données Azure Cosmos de production et votre clé avec hello Azure Cosmos DB émulateur. 

> [!NOTE] 
> Si vous avez démarré l’émulateur de hello avec hello option / Key, puis utiliser une clé hello généré au lieu de « C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == »

En outre, tout comme hello service de base de données Azure Cosmos, hello Azure Cosmos DB émulateur prend en charge uniquement une communication sécurisée via SSL.

## <a name="running-hello-emulator-on-a-local-network"></a>Émulateur de hello en cours d’exécution sur un réseau local

Vous pouvez exécuter l’émulateur de hello sur un réseau local. tooenable accès réseau, spécifiez l’option /AllowNetworkAccess hello au hello [ligne de commande](#command-line-syntax), ce qui nécessite également que vous spécifiez/KEY = key_string ou/keyfile = nom_fichier. Vous pouvez utiliser /GenKeyFile = nom_fichier toogenerate un fichier avec une clé aléatoire dès le départ.  Vous pouvez passer ce trop/KeyFile = nom_fichier ou/Key = contents_of_file.

un accès réseau pour l’utilisateur hello hello tooenable doit arrêter l’émulateur hello et supprimer le répertoire de données de l’émulateur hello (C:\Users\user_name\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-hello-emulator"></a>Développement avec hello émulateur
Une fois que vous avez hello Azure Cosmos DB émulateur en cours d’exécution sur votre bureau, vous pouvez utiliser une prise en charge [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) ou hello [API REST de Azure Cosmos DB](/rest/api/documentdb/) toointeract avec hello émulateur. Bonjour Azure Cosmos DB émulateur inclut également un Explorateur de données intégrés qui vous permet de créer des regroupements pour hello DocumentDB MongoDB APIs et d’afficher et modifier des documents sans écrire de code.   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Si vous utilisez [prise en charge de base de données Azure Cosmos protocole pour MongoDB](mongodb-introduction.md), utilisez hello suivant de chaîne de connexion :

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

Vous pouvez utiliser les outils existants tels que [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB émulateur. Vous pouvez également migrer des données entre hello Azure Cosmos DB émulateur et le service de base de données Azure Cosmos hello à l’aide de hello [outil de Migration de données Azure Cosmos DB](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Si vous avez démarré l’émulateur de hello avec hello option / Key, puis utiliser une clé hello généré au lieu de « C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == »

À l’aide d’émulateur de base de données Azure Cosmos hello, par défaut, vous pouvez créer des collections de partitions uniques too25 ou 1 collection partitionnée. Pour plus d’informations sur la modification de cette valeur, consultez [définition hello PartitionCount valeur](#set-partitioncount).

## <a name="export-hello-ssl-certificate"></a>Exporter le certificat SSL de hello

Langages .NET et toosecurely de magasin de certificats Windows runtime utilisez hello connectent émulateur local de base de données Azure Cosmos toohello. D’autres langages ont leur propre méthode de gestion et de l’utilisation des certificats. Java utilise son propre [magasin de certificats](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), tandis que Python utilise des [wrappers de socket](https://docs.python.org/2/library/ssl.html).

Dans l’ordre tooobtain un toouse de certificat avec les langues et runtimes qui ne s’intègrent pas avec hello magasin de certificats Windows vous en aurez besoin tooexport à l’aide de hello Gestionnaire de certificats Windows. Vous pouvez démarrer, exécutez certlm.msc ou suivez les instructions étape par étape de hello dans [exporter hello Azure Cosmos DB émulateur certificats](./local-emulator-export-ssl-certificates.md). Une fois que le Gestionnaire de certificats hello est en cours d’exécution, hello ouvrir les certificats personnels comme indiqué ci-dessous et l’exportation hello certificat avec le nom convivial hello « DocumentDBEmulatorCertificate » comme fichier X.509 (.cer) d’encodé en BASE-64.

![Certificat SSL de l’émulateur local Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

certificat X.509 de Hello peut être importé dans le magasin de certificats hello Java en suivant les instructions de hello dans [Ajout d’un toohello certificat magasin de certificats d’autorité de certification Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store). Une fois que le certificat de hello est importé dans le magasin de certificats hello, des applications Java et MongoDB sera en mesure de tooconnect toohello Azure Cosmos DB émulateur.

Lors de la connexion toohello émulateur à partir de Python et Node.js kits de développement logiciel, la vérification SSL est désactivée.

## <a id="command-line"></a>Référence sur l’outil en ligne de commande
À partir de l’emplacement d’installation hello, vous pouvez utiliser toostart de ligne de commande de hello et arrêter l’émulateur de hello, configurer les options et effectuer d’autres opérations.

### <a name="command-line-syntax"></a>Syntaxe de ligne de commande

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

liste de hello tooview des options de type `CosmosDB.Emulator.exe /?` à l’invite de commandes hello.

<table>
<tr>
  <td><strong>Option</strong></td>
  <td><strong>Description</strong></td>
  <td><strong>Commande</strong></td>
  <td><strong>Arguments</strong></td>
</tr>
<tr>
  <td>[aucun argument]</td>
  <td>Démarre hello Azure Cosmos DB émulateur avec les paramètres par défaut.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Aide]</td>
  <td>Affiche la liste hello de prise en charge des arguments de ligne de commande.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Shutdown</td>
  <td>Bonjour Azure Cosmos DB émulateur s’arrête.</td>
  <td>CosmosDB.Emulator.exe /Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>DataPath</td>
  <td>Spécifie le chemin d’accès hello dans les fichiers de données toostore. La valeur par défaut est %LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</td>
  <td>&lt;datapath&gt; : un chemin accessible</td>
</tr>
<tr>
  <td>Port</td>
  <td>Spécifie les toouse de numéro de port hello pour l’émulateur de hello.  La valeur par défaut est 8081.</td>
  <td>CosmosDB.Emulator.exe /Port=&lt;port&gt;</td>
  <td>&lt;port&gt; : numéro de port unique</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Spécifie les toouse de numéro de port hello pour la compatibilité MongoDB API. La valeur par défaut est 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt; : numéro de port unique</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Spécifie les toouse de ports hello pour une connectivité directe. Les valeurs par défaut sont 10251,10252,10253,10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt; : liste séparée par des virgules de 4 ports</td>
</tr>
<tr>
  <td>Clé</td>
  <td>Clé d’autorisation de l’émulateur de hello. Clé doit être hello codage en base 64 d’un vecteur de 64 octets.</td>
  <td>CosmosDB.Emulator.exe /Key:&lt;key&gt;</td>
  <td>&lt;clé&gt;: la clé doit être hello codage en base 64 d’un vecteur de 64 octets</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>Spécifie que le comportement de limitation de taux de demandes est activé.</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>Spécifie que le comportement de limitation de taux de demandes est désactivé.</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>Ne pas afficher les émulateur hello interface utilisateur.</td>
  <td>CosmosDB.Emulator.exe /NoUI</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>Ne pas afficher l’Explorateur de documents au démarrage.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>PartitionCount</td>
  <td>Spécifie le nombre maximal de hello de collections partitionnées. Consultez [modifier nombre hello de collections](#set-partitioncount) pour plus d’informations.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</td>
  <td>&lt;partitioncount&gt; : nombre maximal autorisé de collections à partition unique. Valeur par défaut : 25. Valeur maximale autorisée : 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Spécifie le nombre de partitions pour une collection partitionnée par défaut de hello.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; La valeur par défaut est 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Permet l’accès toohello émulateur sur un réseau. Vous devez également passer/Key =&lt;key_string&gt; ou/keyfile =&lt;nom_fichier&gt; tooenable un accès au réseau.</td>
  <td>CosmosDB.Emulator.exe AllowNetworkAccess /Key =&lt;key_string&gt;<br><br>ou<br><br>CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>Ne pas ajuster les règles de pare-feu lors de l’utilisation de /AllowNetworkAccess.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>Générer une clé d’autorisation de fichier et enregistrez-le toohello spécifié. clé de Hello généré peut être utilisée avec hello/KEY ou les options/keyfile.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;tookey de chemin d’accès fichier&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Cohérence</td>
  <td>Définir le niveau de cohérence hello par défaut pour le compte de hello.</td>
  <td>CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</td>
  <td>&lt;cohérence&gt;: valeur doit être un des éléments suivants de hello [niveaux de cohérence](consistency-levels.md): Session, fort, Eventual ou BoundedStaleness.  valeur par défaut de Hello est la Session.</td>
</tr>
<tr>
  <td>?</td>
  <td>Afficher le message d’aide hello.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Différences entre hello Azure Cosmos DB émulateur et la base de données Azure Cosmos 
Étant donné que hello Azure Cosmos DB émulateur fournit un environnement émulé en cours d’exécution sur une station de travail de développement local, il existe quelques différences de fonctionnalités entre l’émulateur de hello et un compte de base de données Azure Cosmos dans le cloud de hello :

* Bonjour Azure Cosmos DB émulateur prend en charge un seul compte fixe et une clé principale connue.  Régénération de la clé n’est pas possible dans hello Azure Cosmos DB émulateur.
* Hello Azure Cosmos DB émulateur n’est pas un service évolutif et ne prendra pas en charge un grand nombre de collections.
* Bonjour Azure Cosmos DB émulateur ne simule pas différents [niveaux de cohérence de base de données Azure Cosmos](consistency-levels.md).
* Bonjour Azure Cosmos DB émulateur ne simule pas [multizone réplication](distribute-data-globally.md).
* Hello Azure Cosmos DB émulateur ne prend pas en charge les remplacements de quota de service hello qui sont disponibles dans le service de base de données Azure Cosmos hello (par exemple, les limites de taille de document, stockage de la collection partitionnée accrue).
* Comme votre copie de hello Azure Cosmos DB émulateur peut-être pas des toodate avec les modifications les plus récentes avec le service de base de données Azure Cosmos hello hello, veuillez [Planificateur de capacité de base de données Azure Cosmos](https://www.documentdb.com/capacityplanner) tooaccurately estimation débit de production (RUs) besoins de votre application.

## <a id="set-partitioncount"></a>Modifier le nombre de hello de collections

Par défaut, vous pouvez créer des collections de partitions uniques too25 ou 1 collection partitionnée à l’aide de hello Azure Cosmos DB émulateur. En modifiant hello **PartitionCount** valeur, vous pouvez créer des collections de partitions uniques too250 ou les collections partitionnées 10, ou n’importe quelle combinaison de hello deux qui ne dépasse pas 250 unique partitionne (où 1 partitionné collection = 25 collection de partition unique).

Si vous essayez de toocreate une collection après que le nombre de partitions hello actuel a été dépassé, émulateur de hello lève une exception de ServiceUnavailable, avec hello message suivant.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

nombre de hello toochange de toohello de collections disponibles Azure Cosmos DB émulateur, hello suivant :

1. Supprimer toutes les données Azure Cosmos DB émulateur locales en double-cliquant sur hello **Azure Cosmos DB émulateur** icône dans la barre d’état système hello, puis sur **réinitialiser les données en cours...** .
2. Supprimez toutes les données de l’émulateur dans le dossier C:\Users\user_name\AppData\Local\CosmosDBEmulator.
3. Quittez toutes les instances ouvertes en cliquant sur hello **Azure Cosmos DB émulateur** icône dans la barre d’état système hello, puis sur **Exit**. Il peut prendre une minute pour toutes les instances tooexit.
4. Installer la version la plus récente de hello hello [Azure Cosmos DB émulateur](https://aka.ms/cosmosdb-emulator).
5. Lancez l’émulateur hello avec hello PartitionCount indicateur en définissant une valeur < = 250. Par exemple : `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Résolution des problèmes

Utilisez hello suivant les conseils toohelp résoudre les problèmes que vous rencontrez avec l’émulateur de base de données Azure Cosmos hello :

- Si vous avez installé une nouvelle version de hello émulateur rencontrent des erreurs, vérifiez que vous réinitialisez vos données. Vous pouvez réinitialiser vos données, icône hello Azure Cosmos DB émulateur sur la barre d’état système hello, puis cliquez sur Réinitialiser les données en cours... Si cela ne résout pas les erreurs de hello, vous pouvez désinstaller et réinstaller l’application hello. Consultez [désinstaller l’émulateur local de hello](#uninstall) pour obtenir des instructions.

- Si l’émulateur de base de données Azure Cosmos hello tombe en panne, collecter des fichiers de vidage à partir du dossier c:\Users\user_name\AppData\Local\CrashDumps les compresser et les joindre par courrier électronique tooan trop[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Si vous rencontrez des blocages dans CosmosDB.StartupEntryPoint.exe, exécutez hello de commande suivante à partir d’une invite de commandes administrateur :`lodctr /R` 

- Si vous rencontrez un problème de connectivité, [collecter des fichiers de trace](#trace-files), de compresser et de les joindre par courrier électronique tooan trop[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Si vous recevez un **Service indisponible** message, hello émulateur peut échouer la pile réseau tooinitialize hello. Vérification toosee si vous avez hello Pulse secure client ou Juniper réseaux client est installé, comme leurs pilotes de filtre réseau peuvent entraîner des problème de hello. Désinstallation des pilotes de filtre réseau tiers généralement de résout le problème de hello.

### <a id="trace-files"></a>Collecter les fichiers de trace

toocollect suivis, exécutez hello suivant les commandes à partir d’une invite de commandes d’administration de débogage :

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Espion hello système toomake vraiment hello programme s’est arrêté, il peut prendre une minute. Vous pouvez également cliquer sur **Exit** dans l’interface utilisateur de hello Azure Cosmos DB émulateur.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Reproduisez le problème de hello. Si l’Explorateur de données ne fonctionne pas, vous devez uniquement toowait pour tooopen de navigateur hello pour erreur hello de toocatch quelques secondes.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Accédez trop`%ProgramFiles%\Azure Cosmos DB Emulator` et de trouver le fichier de docdbemulator_000001.etl hello.
7. Envoyer le fichier .etl de hello, ainsi que les étapes de reproduction trop[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) pour le débogage.

### <a id="uninstall"></a>Désinstaller hello émulateur local

1. Quittez toutes les instances ouvertes de hello émulateur local, icône hello Azure Cosmos DB émulateur sur la barre d’état système hello, puis cliquez sur Quitter. Il peut prendre une minute pour toutes les instances tooexit.
2. Dans la zone de recherche de Windows hello, tapez **applications & fonctionnalités** , puis cliquez sur hello **caractéristiques (paramètres système) et les applications** résultat.
3. Dans la liste de hello des applications, faites défiler trop**Azure Cosmos DB émulateur**, sélectionnez-la, cliquez sur **désinstallation**, puis confirmer, cliquez sur **désinstallation** à nouveau.
4. Lors de l’application hello est désinstallée, accédez à tooC:\Users\<utilisateur > \AppData\Local\CosmosDBEmulator et supprimer le dossier hello. 

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Installé hello émulateur local
> * RAND hello émulateur sur Docker pour Windows
> * Authentifié des requêtes
> * Utilisé hello Explorateur de données dans l’émulateur de hello
> * Exporté des certificats SSL
> * Appelée hello émulateur à partir de la ligne de commande hello
> * Collecté les fichiers de trace

Dans ce didacticiel, vous avez appris comment toouse hello émulateur local pour le développement local gratuit. Vous pouvez maintenant continuer le didacticiel suivant de toohello et savoir comment les certificats SSL de l’émulateur tooexport. 

> [!div class="nextstepaction"]
> [Exporter des certificats d’émulateur de base de données Azure Cosmos hello](local-emulator-export-ssl-certificates.md)
