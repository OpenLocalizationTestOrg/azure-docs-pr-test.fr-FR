---
title: "les zones DNS aaaCreate et jeux d’enregistrements à l’aide d’Azure DNS hello .NET SDK | Documents Microsoft"
description: "Comment les zones DNS toocreate et enregistrement définit dans Azure DNS à l’aide de hello du SDK .NET."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>Créer des zones DNS et des jeux d’enregistrements à l’aide de hello .NET SDK

Vous pouvez automatiser les opérations toocreate, supprimer ou mettre à jour les zones DNS, jeux d’enregistrements et les enregistrements à l’aide de DNS SDK avec la bibliothèque de gestion DNS de .NET. Un projet Visual Studio complet est disponible [ici.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)

## <a name="create-a-service-principal-account"></a>Créer un compte de principal du service

En règle générale, les ressources tooAzure de l’accès par programme est accordé via un compte dédié, au lieu de vos propres informations d’identification de l’utilisateur. Ces comptes dédiés sont appelés comptes de « principal du service ». toouse hello Azure SDK DNS exemple de projet, vous devez toocreate un compte de principal du service et lui attribuer les autorisations correctes de hello.

1. Suivez [ces instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate un compte de principal du service (exemple de projet de kit de développement logiciel Azure DNS hello suppose l’authentification basée sur mot de passe).
2. Créez un groupe de ressources ([procédure](../azure-resource-manager/resource-group-template-deploy-portal.md)).
3. Utilisez Azure RBAC toogrant hello principal groupe comptes de service « Collaborateur de Zone DNS » autorisations toohello ressource ([Voici comment](../active-directory/role-based-access-control-configure.md).)
4. Si l’exemple de projet de kit de développement logiciel Azure DNS hello, modifiez fichier de « program.cs » hello comme suit :

   * Insérer des valeurs correctes de hello pour hello tenantId, clientId (également appelé ID de compte), le secret (mot de passe de compte de principal du service) et ID d’abonnement utilisé à l’étape 1.
   * Entrez le nom de groupe de ressources hello choisi à l’étape 2.
   * Entrez le nom de zone DNS de votre choix.

## <a name="nuget-packages-and-namespace-declarations"></a>Packages NuGet et déclaration des espaces de noms

toouse hello DNS Azure .NET SDK, vous devez tooinstall hello **bibliothèque de gestion Azure DNS** package NuGet et autres requises des packages Azure.

1. Dans **Visual Studio**, ouvrez un projet existant ou un nouveau projet.
2. Accédez trop**outils**  **>**  **Gestionnaire de Package NuGet**  **>**  **gérer les Packages NuGet pour Solution...** .
3. Cliquez sur **Parcourir**, activer hello **inclure la version préliminaire** case à cocher et le type **Microsoft.Azure.Management.Dns** dans la zone de recherche hello.
4. Sélectionnez un package hello et cliquez sur **installer** tooadd il projet de Visual Studio tooyour.
5. Répétez les processus hello ci-dessus hello d’installation tooalso suivant des packages : **Microsoft.Rest.ClientRuntime.Azure.Authentication** et **Microsoft.Azure.Management.ResourceManager**.

## <a name="add-namespace-declarations"></a>Ajout de déclarations d'espaces de noms

Ajouter hello suivant des déclarations d’espace de noms

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Initialiser le client de gestion DNS hello

Hello *DnsManagementClient* contient les méthodes de hello et les propriétés nécessaires pour la gestion des zones DNS et les jeux d’enregistrements.  Bonjour de code suivant enregistre dans le compte de principal du service toohello et crée un objet DnsManagementClient.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>Créer ou mettre à jour une zone DNS

toocreate une zone DNS, tout d’abord un objet de la « Zone » est créé les paramètres de zone DNS toocontain hello. Étant donné que les zones DNS ne sont pas liés tooa une région spécifique, emplacement de hello a la valeur too'global'. Dans cet exemple, un [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) est également ajouté toohello zone.

tooactually créer ou de mise à jour hello zone DNS Azure, objet de fuseau hello qui contient les paramètres de zone hello est passé toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* (méthode).

> [!NOTE]
> DnsManagementClient prend en charge trois modes de fonctionnement : synchrone (« CreateOrUpdate »), asynchrone ('CreateOrUpdateAsync'), ou asynchrone avec la réponse de toohello HTTP d’accès (« CreateOrUpdateWithHttpMessagesAsync »).  Vous pouvez choisir l’un de ces modes, selon les besoins de votre application.

Azure DNS prend en charge l’accès simultané optimiste, appelé [ETags](dns-getstarted-create-dnszone.md). Dans cet exemple, en spécifiant « * » pour les en-tête hello 'If-None-Match' indique à Azure DNS toocreate une zone DNS s’il n’existe pas déjà.  appel de Hello échoue si une zone avec le nom donné de hello existe déjà dans hello groupe de ressources donné.

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a>Créer des jeux d’enregistrements et d’enregistrements DNS

Les enregistrements DNS sont gérés en tant que jeu d'enregistrements. Un jeu d’enregistrements est un ensemble d’enregistrements par hello même nommer et enregistrer le type dans une zone.  nom du jeu d’enregistrements Hello est le nom de la zone toohello relatif, ne Hello pas de nom DNS complet.

toocreate ou mise à jour un jeu d’enregistrements, un objet de paramètres de « RecordSet » est créé et passe trop*DnsManagementClient.RecordSets.CreateOrUpdateAsync*. Comme avec les zones DNS, il existe trois modes d’opération : synchrone (« CreateOrUpdate »), asynchrone ('CreateOrUpdateAsync'), ou asynchrone avec la réponse de toohello HTTP d’accès (« CreateOrUpdateWithHttpMessagesAsync »).

Comme avec les zones DNS, les opérations sur les jeux d’enregistrements prennent en charge l’accès concurrentiel optimiste.  Dans cet exemple, étant donné que ni 'If-Match' ni 'If-None-Match' est spécifiées, jeu d’enregistrements hello est toujours créé.  Cet appel remplace tout enregistrement existant avec hello même nommer et enregistrer le type de cette zone DNS.

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a>Obtenir des zones et des jeux d’enregistrements

Hello *DnsManagementClient.Zones.Get* et *DnsManagementClient.RecordSets.Get* méthodes récupèrent les zones individuelles et des jeux d’enregistrements, respectivement. Jeux d’enregistrements est identifiés par leur type, le nom et le groupe de zone et de ressources hello dans qu'elles existent. Les zones sont identifiées par leur groupe de ressources de nom et hello dans qu'elles existent.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>Mettre à jour un jeu d’enregistrements

tooupdate un enregistrement DNS existant défini, tout d’abord extraire jeu d’enregistrements hello, enregistrement hello de mise à jour le contenu du jeu, puis soumettez hello modification.  Dans cet exemple, nous spécifions hello 'Etag' à partir de hello récupérées ensemble d’enregistrements d’un paramètre de 'If-Match' hello. appel de Hello échoue si une opération simultanée a modifié hello ensemble d’enregistrements d’hello entre-temps.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>Répertorier les zones et les jeux d’enregistrements

les zones toolist, utilisez hello *DnsManagementClient.Zones.List...*  utilisent des méthodes qui prennent en charge la liste de toutes les zones d’un groupe de ressources donné ou toutes les zones d’un jeux d’enregistrements toolist abonnement Azure donné (sur les groupes de ressources.), *DnsManagementClient.RecordSets.List...*  méthodes qui prennent en charge de l’affichage de la liste tous les jeux d’enregistrements dans une zone donnée ou uniquement les jeux d’enregistrements d’un type spécifique.

Notez que les résultats peuvent être paginés lors du répertoriage des zones et des jeux d’enregistrements.  Hello suivant montre l’exemple de comment tooiterate via les pages hello de résultats. (Une taille de page artificiellement small de '2' est utilisé tooforce pagination ; dans la pratique, ce paramètre doit être omis et hello de taille de page par défaut utilisée).

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a>Étapes suivantes

Télécharger hello [exemple de projet Azure DNS .NET SDK](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), qui inclut d’autres exemples de la façon dont toouse hello Azure DNS .NET SDK, y compris des exemples pour les autres types d’enregistrements DNS.
