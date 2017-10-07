---
title: "un service de fusion et fractionnement d’aaaDeploy | Documents Microsoft"
description: "Fractionnement et fusion avec les outils de bases de données élastiques"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>Déployer un service de fractionnement et de fusion
outil de fusion et fractionnement Hello vous permet de déplacer des données entre des bases de données partitionnées. Consultez [Déplacement de données entre des bases de données cloud montées en charge](sql-database-elastic-scale-overview-split-and-merge.md)

## <a name="download-hello-split-merge-packages"></a>Télécharger les packages de fusion et fractionnement hello
1. Télécharger la dernière version de NuGet hello à partir de [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).
2. Ouvrez une invite de commandes et accédez répertoire toohello où vous avez téléchargé nuget.exe. Hello inclut commmands de PowerShell.
3. Téléchargez hello dernière fusion et fractionnement dans l’annuaire actuel de hello avec hello commande ci-dessous :
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

fichiers de Hello sont placés dans un répertoire nommé **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** où *x.x.xxx.x* reflète le numéro de version hello. Recherche des fichiers de Service de fusion et fractionnement hello Bonjour **content\splitmerge\service** sous-répertoire et hello scripts PowerShell de fusion et fractionnement (et les DLL client requis) Bonjour **content\splitmerge\powershell** sous-répertoire.

## <a name="prerequisites"></a>Composants requis
1. Créer une base de données de la base de données SQL Azure qui sera utilisé comme base de données de fusion et fractionnement état hello. Accédez toohello [portail Azure](https://portal.azure.com). Créez une **base de données SQL**. Donnez un nom à base de données hello et créer un nouvel administrateur et un mot de passe. Être assuré que nom de hello toorecord et le mot de passe pour une utilisation ultérieure.
2. Vérifiez que votre serveur de base de données SQL Azure autorise des Services Azure tooconnect tooit. Dans le portail de hello hello **les paramètres de pare-feu**, vérifiez que hello **autoriser l’accès des Services de tooAzure** est défini trop**sur**. Cliquez sur hello « enregistrer » de l’icône.
   
   ![Services autorisés][1]
3. Créez un compte de Stockage Azure qui sera utilisé comme emplacement de destination pour les diagnostics. Accédez toohello portail Azure. Dans la barre de gauche hello, cliquez sur **nouveau**, cliquez sur **données + stockage**, puis **stockage**.
4. Créez un service cloud Azure qui contient votre service de fractionnement/fusion.  Accédez toohello portail Azure. Dans la barre de gauche hello, cliquez sur **nouveau**, puis **de calcul**, **Service Cloud**, et **créer**. 

## <a name="configure-your-split-merge-service"></a>Configurer votre service de fractionnement et de fusion
### <a name="split-merge-service-configuration"></a>Configuration du service de fractionnement/fusion
1. Dans le dossier hello où vous avez téléchargé les assemblys hello fusion et fractionnement, créer une copie de hello **ServiceConfiguration.Template.cscfg** fichier livré avec **SplitMergeService.cspkg** et renommez-la **ServiceConfiguration.cscfg**.
2. Ouvrez **ServiceConfiguration.cscfg** dans un éditeur de texte tel que Visual Studio qui valide les entrées telles que format hello des empreintes numériques de certificat.
3. Créer une base de données ou choisissez un tooserve de base de données existante comme base de données de statut hello pour les opérations de fusion et fractionnement et récupérer la chaîne de connexion hello de cette base de données. 
   
   > [!IMPORTANT]
   > À ce stade, base de données de statut hello doit utiliser classement Latin de hello (SQL\_Latin1\_général\_CP1\_CI\_AS). Pour plus d'informations, consultez la rubrique [Nom de classement Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).
   >

   Avec la base de données SQL Azure, chaîne de connexion hello est généralement sous forme de hello :
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. Entrez cette chaîne de connexion dans le fichier cscfg de hello dans les deux hello **SplitMergeWeb** et **SplitMergeWorker** sections de rôle dans le paramètre de ElasticScaleMetadata hello.
5. Pourquoi **SplitMergeWorker** rôle, entrez un stockage de tooAzure de chaîne de connexion valide pour hello **WorkerRoleSynchronizationStorageAccountConnectionString** paramètre.

### <a name="configure-security"></a>Configurer la sécurité
Pour obtenir des instructions détaillées tooconfigure hello sécurité hello service, consultez toohello [configuration de sécurité de fusion et fractionnement](sql-database-elastic-scale-split-merge-security-configuration.md).

Pour des raisons de hello d’un déploiement de test simple pour ce didacticiel, un ensemble minimal de configuration des étapes seront effectuées service de hello tooget haut et en cours d’exécution. Les étapes suivantes permettent uniquement hello un ordinateur/compte qui exécute les toocommunicate avec le service de hello.

### <a name="create-a-self-signed-certificate"></a>Créer un certificat auto-signé
Créer un nouveau répertoire et à partir de cette hello execute de répertoire suivant à l’aide de la commande une [invite de commandes développeur pour Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) fenêtre :

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

Vous êtes invité à entrer une clé privée de mot de passe tooprotect hello. Entrez un mot de passe fort et confirmez-le. Vous êtes ensuite invité pour hello toobe de mot de passe utilisé après une fois de plus. Cliquez sur **Oui** à hello fin tooimport il magasin racine des autorités de Certification approuvées de toohello.

### <a name="create-a-pfx-file"></a>Création d’un fichier PFX
Exécutez hello de commande suivante à partir de hello même fenêtre où makecert a été exécuté ; Utilisez hello même mot de passe que vous toocreate utilisé hello le certificat :

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Importer un certificat client hello dans le magasin personnel de hello
1. Dans l’Explorateur Windows, double-cliquez sur **MyCert.pfx**.
2. Bonjour **Assistant Importation de certificat** sélectionnez **utilisateur actuel** et cliquez sur **suivant**.
3. Vérifiez le chemin d’accès du fichier hello et cliquez sur **suivant**.
4. Type hello un mot de passe, laissez le champ **inclure toutes les propriétés étendues** activée et cliquez sur **suivant**.
5. Laissez **magasin de certificats de sélectionner automatiquement hello [...]**  activée et cliquez sur **suivant**.
6. Cliquez sur **Terminer** et sur **OK**.

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>Télécharger le service cloud toohello hello PFX fichier
1. Accédez toohello [Azure Portal](https://portal.azure.com).
2. Sélectionnez **Services Cloud**.
3. Sélectionnez le service de cloud computing hello que vous avez créé précédemment pour le service de fractionnement/fusion hello.
4. Cliquez sur **certificats** sur le menu du haut hello.
5. Cliquez sur **télécharger** dans la barre inférieure de hello.
6. Sélectionnez le fichier PFX hello et entrez hello même mot de passe comme indiqué ci-dessus.
7. Une fois terminé, copiez l’empreinte numérique du certificat hello hello nouvelle entrée dans la liste de hello.

### <a name="update-hello-service-configuration-file"></a>Mettre à jour le fichier de configuration de service hello
Collez l’empreinte numérique du certificat hello copié ci-dessus dans l’attribut de valeur d’empreinte numérique hello de ces paramètres.
Pour le rôle de travail hello :
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Pour le rôle web hello :

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Notez que pour les déploiements de production des certificats doivent être utilisées pour hello autorité de certification pour le chiffrement, hello du certificat de serveur et les certificats clients. Pour plus d’informations, consultez la rubrique [Configuration de la sécurité](sql-database-elastic-scale-split-merge-security-configuration.md).

## <a name="deploy-your-service"></a>Déployer votre service
1. Accédez toohello [portail Azure](https://manage.windowsazure.com).
2. Cliquez sur hello **Services de cloud computing** sur hello gauche et sélectionnez le service de cloud computing hello que vous avez créé précédemment.
3. Cliquez sur **Dashboard**.
4. Choisissez hello environnement intermédiaire, puis cliquez sur **Téléchargez un nouveau déploiement intermédiaire**.
   
   ![Staging][3]
5. Dans la boîte de dialogue hello, entrez une étiquette de déploiement. « Package » et « Configuration », cliquez sur 'À partir de Local', puis choisissez hello **SplitMergeService.cspkg** de fichiers et votre fichier .cscfg que vous avez configuré précédemment.
6. Vérifiez cette case à cocher hello **déployer même si un ou plusieurs rôles contiennent une seule instance** est activée.
7. Hello graduation bouton dans le déploiement de hello hello bas toobegin droit d’accès. Tootake attendez quelques minutes toocomplete.

   ![Télécharger][4]

## <a name="troubleshoot-hello-deployment"></a>Résoudre les problèmes de déploiement de hello
Si votre rôle web échoue toocome en ligne, il est probablement un problème de configuration de sécurité hello. Vérifiez que hello que SSL est configuré comme décrit ci-dessus.

Si votre rôle de travail échoue toocome en ligne, mais il se peut que votre rôle web réussit, il est très probablement un problème de connexion toohello état de base de données que vous avez créé précédemment.

* Assurez-vous que la chaîne de connexion hello dans votre fichier .cscfg est exact.
* Vérification de la base de données et serveur de hello existent et que l’id d’utilisateur hello et le mot de passe sont corrects.
* Pour la base de données SQL Azure, la chaîne de connexion hello doit être sous forme de hello :

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* Vérifiez que nom de serveur hello ne commence pas par **https://**.
* Vérifiez que votre serveur de base de données SQL Azure autorise des Services Azure tooconnect tooit. toodo, ouvrez https://manage.windowsazure.com et cliquez sur « Bases de données SQL » sur hello gauche, cliquez sur « Serveurs » en haut de hello, sélectionnez votre serveur. Cliquez sur **configurer** à hello principaux et vous assurer que hello **Services Azure** est défini trop « Oui ». (Consultez les conditions préalables de hello section haut hello de cet article).

## <a name="test-hello-service-deployment"></a>Tester le déploiement du service hello
### <a name="connect-with-a-web-browser"></a>Se connecter avec un navigateur Web
Déterminer le point de terminaison hello web de votre service de fusion et fractionnement. Vous pouvez le trouver dans hello portail classique Azure en accédant de toohello **tableau de bord** de votre service cloud et sous **URL du Site** sur le côté droit de hello. Remplacez **http://** avec **https://** étant donné que les paramètres de sécurité par défaut hello désactivent le point de terminaison hello HTTP. Charger la page hello pour cette URL dans votre navigateur.

### <a name="test-with-powershell-scripts"></a>Effectuer des tests avec des scripts PowerShell
déploiement de Hello et votre environnement peuvent être testés en exécutant des scripts PowerShell d’exemple hello inclus.

les fichiers de script Hello inclus sont :

1. **SetupSampleSplitMergeEnvironment.ps1** : configure une couche de données de test pour la fusion et le fractionnement (voir le tableau ci-dessous pour obtenir une description détaillée)
2. **ExecuteSampleSplitMerge.ps1** -exécute des opérations de test sur le test de hello couche données (voir le tableau ci-dessous pour une description détaillée)
3. **GetMappings.ps1** - niveau supérieur exemple de script qui imprime état actuel de hello de mappages de partition hello.
4. **ShardManagement.psm1** -script d’assistance qui encapsule hello ShardManagement API
5. **SqlDatabaseHelpers.psm1** : script d’assistance pour la création et la gestion des bases de données SQL
   
   <table style="width:100%">
     <tr>
       <th>Fichier PowerShell</th>
       <th>Étapes</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    Crée une base de données pour le Gestionnaire de cartes de partitions</td>
     </tr>
     <tr>
       <td>2.    Crée 2&#160;bases de données de partition.
     </tr>
     <tr>
       <td>3.    Crée une carte de partitions pour les bases de données concernées (supprime les cartes de partitions existantes sur ces dernières). </td>
     </tr>
     <tr>
       <td>4.    Crée un petit exemple de table dans les deux partitions hello et remplit la table hello dans une des partitions de hello.</td>
     </tr>
     <tr>
       <td>5.    Déclare hello SchemaInfo pour une table partitionnée de hello.</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>Fichier PowerShell</th>
       <th>Étapes</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    Envoie un fractionnement demande toohello fusion et fractionnement Service serveur web frontal, qui fractionne les données de salutation moitié à partir de la partition deuxième hello première partition toohello.</td>
     </tr>
     <tr>
       <td>2.    Interroge hello serveur web frontal pour hello fractionner le statut de la demande et attend jusqu'à ce que la demande de hello se termine.</td>
     </tr>
     <tr>
       <td>3.    Envoie un fusion demande toohello fusion et fractionnement Service serveur web frontal, ce qui déplace les données de salutation à partir de la partition première hello deuxième partition toohello précédent.</td>
     </tr>
     <tr>
       <td>4.    Interroge hello serveur web frontal pour l’état de demande de fusion de hello et attend la fin de la demande de hello.</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>Utilisez PowerShell tooverify votre déploiement
1. Ouvrez une nouvelle fenêtre PowerShell et accédez répertoire toohello où vous avez téléchargé le package de fusion et fractionnement hello puis naviguez jusqu’au répertoire de « powershell » hello.
2. Créer un serveur de base de données SQL Azure (ou choisissez un serveur existant) où le Gestionnaire de carte de partitions hello et partitions seront créées.
   
   > [!NOTE]
   > Hello SetupSampleSplitMergeEnvironment.ps1 script crée ces bases de données sur hello même serveur par le script de hello tookeep par défaut simple. Cela n’est pas une restriction de hello fusion et fractionnement Service lui-même.
   >
   
   Une connexion d’authentification SQL avec toohello d’accès en lecture/écriture qu'aux bases de données seront nécessaires pour hello toomove données du service de fusion et fractionnement et de la carte de partitions hello mise à jour. Étant donné que hello fusion et fractionnement Service s’exécute dans le cloud de hello, il ne prend pas en charge l’authentification intégrée.
   
   Vérifiez que hello Azure SQL server est configuré tooallow l’accès à partir de l’adresse IP de hello d’ordinateur hello ces scripts en cours d’exécution. Vous pouvez trouver ce paramètre sous hello Azure SQL server / configuration / adresses IP autorisées.
3. Exécutez hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello exemple d’environnement.
   
   Ce script en cours d’exécution sera effacer toutes les données de gestion de carte partitions existantes des structures sur la base de données du gestionnaire carte hello partitions et les partitions hello. Il peut être script de hello toorerun utile si vous le souhaitez carte de partitions hello toore d’initialiser ou de partitions.
   
   Exemple de ligne de commande :

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Exécutez hello Getmappings.ps1 tooview hello mappages de script qui existent actuellement dans l’environnement d’exemple hello.
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. Exécutez hello ExecuteSampleSplitMerge.ps1 script tooexecute une opération split (déplacement de données de hello moitié sur les partitions deuxième hello première partition toohello), puis une opération de fusion (déplacement des données de hello sur les partitions première hello). Si vous avez configuré SSL et le point de terminaison http hello gauche désactivé, assurez-vous que vous utilisez point de terminaison hello https:// à la place.
   
   Exemple de ligne de commande :

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   Si vous recevez hello erreur ci-dessous, il s’agit probablement d’un problème avec le certificat du votre point de terminaison Web. Essayez de vous connecter le point de terminaison toohello Web avec votre navigateur Web favoris et vérifier s’il existe une erreur de certificat.
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   Si elle a réussi, sortie de hello doit ressembler à hello ci-dessous :
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. Faites des essais avec d’autres types de données. Tous ces scripts prennent un paramètre - ShardKeyType facultatif qui vous permet de type de clé toospecify hello. valeur par défaut Hello est Int32, mais vous pouvez également spécifier Int64, Guid ou binaire.

## <a name="create-requests"></a>Créer des requêtes
service de Hello peut être utilisé à l’aide de l’interface utilisateur web de hello ou par l’importation et à l’aide du module de SplitMerge.psm1 PowerShell hello qui envoie vos demandes via le rôle web de hello.

service de Hello peut déplacer des données dans les tables partitionnées et les tables de référence. Une table partitionnée possède une colonne de clés de partitionnement et comporte des données de ligne différentes sur chaque partition. Une table de référence n’est pas partitionnée afin qu’il contient hello même ligne de données sur chaque partition. Tables de référence sont utiles pour les données qui ne changent pas souvent et sont tooJOIN utilisé avec des tables partitionnées dans les requêtes.

Dans l’ordre tooperform une opération de fusion et fractionnement, vous devez déclarer les tables partitionnées hello et les tables de référence que vous souhaitez toohave déplacé. Cela est accompli par hello **SchemaInfo** API. Cette API méthode est Bonjour **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** espace de noms.

1. Pour chaque table partitionnée, créez un **ShardedTableInfo** objet décrivant le nom de schéma de la table hello parent (facultatif, par défaut est trop « dbo »), hello du nom de la table et hello nom de colonne dans la table qui contient la clé de partitionnement hello.
2. Pour chaque table de référence, créez un **ReferenceTableInfo** objet décrivant le nom de schéma de la table hello parent (facultatif, par défaut est trop « dbo ») et le nom de la table hello.
3. Ajouter hello ci-dessus tooa d’objets TableInfo nouvelle **SchemaInfo** objet.
4. Obtenir une référence tooa **ShardMapManager** objet, puis appelez **GetSchemaInfoCollection**.
5. Ajouter hello **SchemaInfo** toohello **SchemaInfoCollection**, en fournissant le nom de mappage de partitions hello.

Un exemple de cette peut être consulté dans hello SetupSampleSplitMergeEnvironment.ps1 script.

service de fusion et fractionnement de Hello ne crée pas de base de données cible hello (ou le schéma des tables de base de données hello) pour vous. Ils doivent être créés au préalable avant l’envoi d’un service de toohello de demande.

## <a name="troubleshooting"></a>Résolution des problèmes
Vous pouvez voir hello message ci-après lors de l’exécution des scripts powershell hello exemple :

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

Cette erreur signifie que votre certificat SSL n’est pas correctement configuré. Suivez les instructions de hello dans la section « Connexion avec un navigateur web ».

Si vous ne pouvez pas soumettre les demandes, vous pouvez voir ceci :

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

Dans ce cas, recherchez votre fichier de configuration, dans le paramètre hello particulier pour **WorkerRoleSynchronizationStorageAccountConnectionString**. Cette erreur indique en général, que ce rôle de travail hello a pas pu initialiser la base de données des métadonnées de hello sur la première utilisation. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

