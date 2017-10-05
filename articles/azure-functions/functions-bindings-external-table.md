---
title: "Liaisons de table externe Azure Functions (préversion) | Microsoft Docs"
description: Utilisation de liaisons de tables externes dans Azure Functions
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 716438e5ea490f6716999813112305499dbe61a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="097f7-103">Liaisons de table externe Azure Functions (préversion)</span><span class="sxs-lookup"><span data-stu-id="097f7-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="097f7-104">Cet article montre comment manipuler les données tabulaires sur des fournisseurs SaaS (par exemple, SharePoint, Dynamics) au sein de votre fonction en utilisant des liaisons intégrées.</span><span class="sxs-lookup"><span data-stu-id="097f7-104">This article shows how to manipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="097f7-105">Azure Functions prend en charge des liaisons d’entrée et de sortie pour les tables externes.</span><span class="sxs-lookup"><span data-stu-id="097f7-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="097f7-106">Connexions d’API</span><span class="sxs-lookup"><span data-stu-id="097f7-106">API Connections</span></span>

<span data-ttu-id="097f7-107">Les liaisons de table tirent parti des connexions d’API externes pour s’authentifier auprès des fournisseurs SaaS tiers.</span><span class="sxs-lookup"><span data-stu-id="097f7-107">Table bindings leverage external API connections to authenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="097f7-108">Lors de l’attribution d’une liaison, vous pouvez créer une connexion d’API ou utiliser une API existante au sein du même groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="097f7-108">When assigning a binding you can either create a new API connection or use an existing API connection within the same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="097f7-109">Tableau des connexions d’API prises en charge</span><span class="sxs-lookup"><span data-stu-id="097f7-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="097f7-110">Connecteur</span><span class="sxs-lookup"><span data-stu-id="097f7-110">Connector</span></span>|<span data-ttu-id="097f7-111">Déclencheur</span><span class="sxs-lookup"><span data-stu-id="097f7-111">Trigger</span></span>|<span data-ttu-id="097f7-112">Entrée</span><span class="sxs-lookup"><span data-stu-id="097f7-112">Input</span></span>|<span data-ttu-id="097f7-113">Sortie</span><span class="sxs-lookup"><span data-stu-id="097f7-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="097f7-114">DB2</span><span class="sxs-lookup"><span data-stu-id="097f7-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="097f7-115">x</span><span class="sxs-lookup"><span data-stu-id="097f7-115">x</span></span>|<span data-ttu-id="097f7-116">x</span><span class="sxs-lookup"><span data-stu-id="097f7-116">x</span></span>
|[<span data-ttu-id="097f7-117">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="097f7-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="097f7-118">x</span><span class="sxs-lookup"><span data-stu-id="097f7-118">x</span></span>|<span data-ttu-id="097f7-119">x</span><span class="sxs-lookup"><span data-stu-id="097f7-119">x</span></span>
|[<span data-ttu-id="097f7-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="097f7-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="097f7-121">x</span><span class="sxs-lookup"><span data-stu-id="097f7-121">x</span></span>|<span data-ttu-id="097f7-122">x</span><span class="sxs-lookup"><span data-stu-id="097f7-122">x</span></span>
|[<span data-ttu-id="097f7-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="097f7-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="097f7-124">x</span><span class="sxs-lookup"><span data-stu-id="097f7-124">x</span></span>|<span data-ttu-id="097f7-125">x</span><span class="sxs-lookup"><span data-stu-id="097f7-125">x</span></span>
|[<span data-ttu-id="097f7-126">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="097f7-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="097f7-127">x</span><span class="sxs-lookup"><span data-stu-id="097f7-127">x</span></span>|<span data-ttu-id="097f7-128">x</span><span class="sxs-lookup"><span data-stu-id="097f7-128">x</span></span>
|[<span data-ttu-id="097f7-129">Informix</span><span class="sxs-lookup"><span data-stu-id="097f7-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="097f7-130">x</span><span class="sxs-lookup"><span data-stu-id="097f7-130">x</span></span>|<span data-ttu-id="097f7-131">x</span><span class="sxs-lookup"><span data-stu-id="097f7-131">x</span></span>
|[<span data-ttu-id="097f7-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="097f7-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="097f7-133">x</span><span class="sxs-lookup"><span data-stu-id="097f7-133">x</span></span>|<span data-ttu-id="097f7-134">x</span><span class="sxs-lookup"><span data-stu-id="097f7-134">x</span></span>
|[<span data-ttu-id="097f7-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="097f7-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="097f7-136">x</span><span class="sxs-lookup"><span data-stu-id="097f7-136">x</span></span>|<span data-ttu-id="097f7-137">x</span><span class="sxs-lookup"><span data-stu-id="097f7-137">x</span></span>
|[<span data-ttu-id="097f7-138">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="097f7-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="097f7-139">x</span><span class="sxs-lookup"><span data-stu-id="097f7-139">x</span></span>|<span data-ttu-id="097f7-140">x</span><span class="sxs-lookup"><span data-stu-id="097f7-140">x</span></span>
|[<span data-ttu-id="097f7-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="097f7-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="097f7-142">x</span><span class="sxs-lookup"><span data-stu-id="097f7-142">x</span></span>|<span data-ttu-id="097f7-143">x</span><span class="sxs-lookup"><span data-stu-id="097f7-143">x</span></span>
|[<span data-ttu-id="097f7-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="097f7-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="097f7-145">x</span><span class="sxs-lookup"><span data-stu-id="097f7-145">x</span></span>|<span data-ttu-id="097f7-146">x</span><span class="sxs-lookup"><span data-stu-id="097f7-146">x</span></span>
|[<span data-ttu-id="097f7-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="097f7-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="097f7-148">x</span><span class="sxs-lookup"><span data-stu-id="097f7-148">x</span></span>|<span data-ttu-id="097f7-149">x</span><span class="sxs-lookup"><span data-stu-id="097f7-149">x</span></span>
|[<span data-ttu-id="097f7-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="097f7-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="097f7-151">x</span><span class="sxs-lookup"><span data-stu-id="097f7-151">x</span></span>|<span data-ttu-id="097f7-152">x</span><span class="sxs-lookup"><span data-stu-id="097f7-152">x</span></span>
|[<span data-ttu-id="097f7-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="097f7-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="097f7-154">x</span><span class="sxs-lookup"><span data-stu-id="097f7-154">x</span></span>|<span data-ttu-id="097f7-155">x</span><span class="sxs-lookup"><span data-stu-id="097f7-155">x</span></span>
|<span data-ttu-id="097f7-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="097f7-156">UserVoice</span></span>||<span data-ttu-id="097f7-157">x</span><span class="sxs-lookup"><span data-stu-id="097f7-157">x</span></span>|<span data-ttu-id="097f7-158">x</span><span class="sxs-lookup"><span data-stu-id="097f7-158">x</span></span>
|<span data-ttu-id="097f7-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="097f7-159">Zendesk</span></span>||<span data-ttu-id="097f7-160">x</span><span class="sxs-lookup"><span data-stu-id="097f7-160">x</span></span>|<span data-ttu-id="097f7-161">x</span><span class="sxs-lookup"><span data-stu-id="097f7-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="097f7-162">Les connexions aux tables externes peuvent également servir dans les applications [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="097f7-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="097f7-163">Création pas à pas d’une connexion d’API</span><span class="sxs-lookup"><span data-stu-id="097f7-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="097f7-164">Créer une fonction > fonction personnalisée ![Créer une fonction personnalisée](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="097f7-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="097f7-165">Scénario `Experimental` > `ExternalTable-CSharp` Modèle > Créer `External Table connection`
![Choisir un modèle d’entrée de table](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="097f7-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="097f7-166">Choisir votre fournisseur SaaS > Choisir/créer une connexion ![Configurer un connexion SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="097f7-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="097f7-167">Sélectionner votre connexion d’API > Créer la fonction ![Créer une fonction de table](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="097f7-167">Select your API connection > create the function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="097f7-168">Sélectionnez `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="097f7-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="097f7-169">Configurez la connexion pour utiliser la table cible.</span><span class="sxs-lookup"><span data-stu-id="097f7-169">Configure the connection to use your target table.</span></span> <span data-ttu-id="097f7-170">Ces paramètres varient selon les fournisseurs SaaS.</span><span class="sxs-lookup"><span data-stu-id="097f7-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="097f7-171">Ils sont décrits ci-dessous dans [Paramètres de la source de données](#datasourcesettings)
![Configurer la table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="097f7-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="097f7-172">Usage</span><span class="sxs-lookup"><span data-stu-id="097f7-172">Usage</span></span>

<span data-ttu-id="097f7-173">Cet exemple se connecte à une table nommée « Contact » qui comporte les colonnes ID, LastName et FirstName.</span><span class="sxs-lookup"><span data-stu-id="097f7-173">This example connects to a table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="097f7-174">Le code répertorie les entités Contact dans la table et journalise les noms et les prénoms.</span><span class="sxs-lookup"><span data-stu-id="097f7-174">The code lists the Contact entities in the table and logs the first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="097f7-175">Liaisons</span><span class="sxs-lookup"><span data-stu-id="097f7-175">Bindings</span></span>
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
<span data-ttu-id="097f7-176">`entityId` doit être vide pour les liaisons de table.</span><span class="sxs-lookup"><span data-stu-id="097f7-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="097f7-177">`ConnectionAppSettingsKey` identifie le paramètre d’application qui stocke la chaîne de connexion d’API.</span><span class="sxs-lookup"><span data-stu-id="097f7-177">`ConnectionAppSettingsKey` identifies the app setting that stores the API connection string.</span></span> <span data-ttu-id="097f7-178">Le paramètre d’application est créé automatiquement lorsque vous ajoutez une connexion d’API dans l’interface utilisateur d’intégration.</span><span class="sxs-lookup"><span data-stu-id="097f7-178">The app setting is created automatically when you add an API connection in the integrate UI.</span></span>

<span data-ttu-id="097f7-179">Un connecteur sous forme de tableau fournit des jeux de données et chaque jeu de données contient des tables.</span><span class="sxs-lookup"><span data-stu-id="097f7-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="097f7-180">Le nom du jeu de données par défaut est « default ».</span><span class="sxs-lookup"><span data-stu-id="097f7-180">The name of the default data set is “default.”</span></span> <span data-ttu-id="097f7-181">Les titres de jeux de données et de tables de différents fournisseurs SaaS sont répertoriés ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="097f7-181">The titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="097f7-182">Connecteur</span><span class="sxs-lookup"><span data-stu-id="097f7-182">Connector</span></span>|<span data-ttu-id="097f7-183">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="097f7-183">Dataset</span></span>|<span data-ttu-id="097f7-184">Table</span><span class="sxs-lookup"><span data-stu-id="097f7-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="097f7-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="097f7-185">**SharePoint**</span></span>|<span data-ttu-id="097f7-186">Site</span><span class="sxs-lookup"><span data-stu-id="097f7-186">Site</span></span>|<span data-ttu-id="097f7-187">Liste SharePoint</span><span class="sxs-lookup"><span data-stu-id="097f7-187">SharePoint List</span></span>
|<span data-ttu-id="097f7-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="097f7-188">**SQL**</span></span>|<span data-ttu-id="097f7-189">Base de données</span><span class="sxs-lookup"><span data-stu-id="097f7-189">Database</span></span>|<span data-ttu-id="097f7-190">Table</span><span class="sxs-lookup"><span data-stu-id="097f7-190">Table</span></span> 
|<span data-ttu-id="097f7-191">**Google Sheet**</span><span class="sxs-lookup"><span data-stu-id="097f7-191">**Google Sheet**</span></span>|<span data-ttu-id="097f7-192">Feuille de calcul</span><span class="sxs-lookup"><span data-stu-id="097f7-192">Spreadsheet</span></span>|<span data-ttu-id="097f7-193">Feuille de calcul</span><span class="sxs-lookup"><span data-stu-id="097f7-193">Worksheet</span></span> 
|<span data-ttu-id="097f7-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="097f7-194">**Excel**</span></span>|<span data-ttu-id="097f7-195">Fichier Excel</span><span class="sxs-lookup"><span data-stu-id="097f7-195">Excel file</span></span>|<span data-ttu-id="097f7-196">Feuille</span><span class="sxs-lookup"><span data-stu-id="097f7-196">Sheet</span></span> 

<!--
See the language-specific sample that copies the input file to the output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="097f7-197">Utilisation en C#</span><span class="sxs-lookup"><span data-stu-id="097f7-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound to the incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in the source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<span data-ttu-id="097f7-198"><!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
##Paramètres de la source de données</span><span class="sxs-lookup"><span data-stu-id="097f7-198"><!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="097f7-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="097f7-199">SQL Server</span></span>

<span data-ttu-id="097f7-200">Le script qui permet de créer et de remplir la table Contact est affiché ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="097f7-200">The script to create and populate the Contact table is below.</span></span> <span data-ttu-id="097f7-201">dataSetName est défini sur « default ».</span><span class="sxs-lookup"><span data-stu-id="097f7-201">dataSetName is “default.”</span></span>

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a><span data-ttu-id="097f7-202">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="097f7-202">Google Sheets</span></span>
<span data-ttu-id="097f7-203">Dans Google Docs, créez une feuille de calcul nommée `Contact`.</span><span class="sxs-lookup"><span data-stu-id="097f7-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="097f7-204">Le connecteur ne peut pas utiliser le nom d’affichage de la feuille de calcul.</span><span class="sxs-lookup"><span data-stu-id="097f7-204">The connector cannot use the spreadsheet display name.</span></span> <span data-ttu-id="097f7-205">Le nom interne (en gras) doit servir en tant que dataSetName, par exemple : `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Ajoutez les noms de colonne `Id`, `LastName`, `FirstName` à la première ligne, puis remplissez les données sur les lignes suivantes.</span><span class="sxs-lookup"><span data-stu-id="097f7-205">The internal name (in bold) needs to be used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add the column names `Id`, `LastName`, `FirstName` to the first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="097f7-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="097f7-206">Salesforce</span></span>
<span data-ttu-id="097f7-207">dataSetName est défini sur « default ».</span><span class="sxs-lookup"><span data-stu-id="097f7-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="097f7-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="097f7-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
