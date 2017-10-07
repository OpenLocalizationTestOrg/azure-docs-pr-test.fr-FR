---
title: "liaison de Table externe de fonctions aaaAzure (version préliminaire) | Documents Microsoft"
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
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="8921f-103">Liaisons de table externe Azure Functions (préversion)</span><span class="sxs-lookup"><span data-stu-id="8921f-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="8921f-104">Cet article explique comment toomanipulate des données tabulaires sur les fournisseurs SaaS (par exemple, Sharepoint, Dynamics) dans votre fonction de liaisons intégrées.</span><span class="sxs-lookup"><span data-stu-id="8921f-104">This article shows how toomanipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="8921f-105">Azure Functions prend en charge des liaisons d’entrée et de sortie pour les tables externes.</span><span class="sxs-lookup"><span data-stu-id="8921f-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="8921f-106">Connexions d’API</span><span class="sxs-lookup"><span data-stu-id="8921f-106">API Connections</span></span>

<span data-ttu-id="8921f-107">Liaisons de table exploitent tooauthenticate de connexions externe API avec les fournisseurs SaaS tiers 3e.</span><span class="sxs-lookup"><span data-stu-id="8921f-107">Table bindings leverage external API connections tooauthenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="8921f-108">Lors de l’attribution d’une liaison vous pouvez créer une nouvelle connexion de l’API ou utiliser une connexion d’API existante dans hello même groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="8921f-108">When assigning a binding you can either create a new API connection or use an existing API connection within hello same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="8921f-109">Tableau des connexions d’API prises en charge</span><span class="sxs-lookup"><span data-stu-id="8921f-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="8921f-110">Connecteur</span><span class="sxs-lookup"><span data-stu-id="8921f-110">Connector</span></span>|<span data-ttu-id="8921f-111">Déclencheur</span><span class="sxs-lookup"><span data-stu-id="8921f-111">Trigger</span></span>|<span data-ttu-id="8921f-112">Entrée</span><span class="sxs-lookup"><span data-stu-id="8921f-112">Input</span></span>|<span data-ttu-id="8921f-113">Sortie</span><span class="sxs-lookup"><span data-stu-id="8921f-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="8921f-114">DB2</span><span class="sxs-lookup"><span data-stu-id="8921f-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="8921f-115">x</span><span class="sxs-lookup"><span data-stu-id="8921f-115">x</span></span>|<span data-ttu-id="8921f-116">x</span><span class="sxs-lookup"><span data-stu-id="8921f-116">x</span></span>
|[<span data-ttu-id="8921f-117">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="8921f-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="8921f-118">x</span><span class="sxs-lookup"><span data-stu-id="8921f-118">x</span></span>|<span data-ttu-id="8921f-119">x</span><span class="sxs-lookup"><span data-stu-id="8921f-119">x</span></span>
|[<span data-ttu-id="8921f-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="8921f-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="8921f-121">x</span><span class="sxs-lookup"><span data-stu-id="8921f-121">x</span></span>|<span data-ttu-id="8921f-122">x</span><span class="sxs-lookup"><span data-stu-id="8921f-122">x</span></span>
|[<span data-ttu-id="8921f-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="8921f-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="8921f-124">x</span><span class="sxs-lookup"><span data-stu-id="8921f-124">x</span></span>|<span data-ttu-id="8921f-125">x</span><span class="sxs-lookup"><span data-stu-id="8921f-125">x</span></span>
|[<span data-ttu-id="8921f-126">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="8921f-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="8921f-127">x</span><span class="sxs-lookup"><span data-stu-id="8921f-127">x</span></span>|<span data-ttu-id="8921f-128">x</span><span class="sxs-lookup"><span data-stu-id="8921f-128">x</span></span>
|[<span data-ttu-id="8921f-129">Informix</span><span class="sxs-lookup"><span data-stu-id="8921f-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="8921f-130">x</span><span class="sxs-lookup"><span data-stu-id="8921f-130">x</span></span>|<span data-ttu-id="8921f-131">x</span><span class="sxs-lookup"><span data-stu-id="8921f-131">x</span></span>
|[<span data-ttu-id="8921f-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="8921f-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="8921f-133">x</span><span class="sxs-lookup"><span data-stu-id="8921f-133">x</span></span>|<span data-ttu-id="8921f-134">x</span><span class="sxs-lookup"><span data-stu-id="8921f-134">x</span></span>
|[<span data-ttu-id="8921f-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="8921f-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="8921f-136">x</span><span class="sxs-lookup"><span data-stu-id="8921f-136">x</span></span>|<span data-ttu-id="8921f-137">x</span><span class="sxs-lookup"><span data-stu-id="8921f-137">x</span></span>
|[<span data-ttu-id="8921f-138">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="8921f-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="8921f-139">x</span><span class="sxs-lookup"><span data-stu-id="8921f-139">x</span></span>|<span data-ttu-id="8921f-140">x</span><span class="sxs-lookup"><span data-stu-id="8921f-140">x</span></span>
|[<span data-ttu-id="8921f-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="8921f-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="8921f-142">x</span><span class="sxs-lookup"><span data-stu-id="8921f-142">x</span></span>|<span data-ttu-id="8921f-143">x</span><span class="sxs-lookup"><span data-stu-id="8921f-143">x</span></span>
|[<span data-ttu-id="8921f-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="8921f-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="8921f-145">x</span><span class="sxs-lookup"><span data-stu-id="8921f-145">x</span></span>|<span data-ttu-id="8921f-146">x</span><span class="sxs-lookup"><span data-stu-id="8921f-146">x</span></span>
|[<span data-ttu-id="8921f-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="8921f-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="8921f-148">x</span><span class="sxs-lookup"><span data-stu-id="8921f-148">x</span></span>|<span data-ttu-id="8921f-149">x</span><span class="sxs-lookup"><span data-stu-id="8921f-149">x</span></span>
|[<span data-ttu-id="8921f-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8921f-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="8921f-151">x</span><span class="sxs-lookup"><span data-stu-id="8921f-151">x</span></span>|<span data-ttu-id="8921f-152">x</span><span class="sxs-lookup"><span data-stu-id="8921f-152">x</span></span>
|[<span data-ttu-id="8921f-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="8921f-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="8921f-154">x</span><span class="sxs-lookup"><span data-stu-id="8921f-154">x</span></span>|<span data-ttu-id="8921f-155">x</span><span class="sxs-lookup"><span data-stu-id="8921f-155">x</span></span>
|<span data-ttu-id="8921f-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="8921f-156">UserVoice</span></span>||<span data-ttu-id="8921f-157">x</span><span class="sxs-lookup"><span data-stu-id="8921f-157">x</span></span>|<span data-ttu-id="8921f-158">x</span><span class="sxs-lookup"><span data-stu-id="8921f-158">x</span></span>
|<span data-ttu-id="8921f-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="8921f-159">Zendesk</span></span>||<span data-ttu-id="8921f-160">x</span><span class="sxs-lookup"><span data-stu-id="8921f-160">x</span></span>|<span data-ttu-id="8921f-161">x</span><span class="sxs-lookup"><span data-stu-id="8921f-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="8921f-162">Les connexions aux tables externes peuvent également servir dans les applications [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="8921f-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="8921f-163">Création pas à pas d’une connexion d’API</span><span class="sxs-lookup"><span data-stu-id="8921f-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="8921f-164">Créer une fonction > fonction personnalisée ![Créer une fonction personnalisée](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="8921f-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="8921f-165">Scénario `Experimental` > `ExternalTable-CSharp` Modèle > Créer `External Table connection`
![Choisir un modèle d’entrée de table](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="8921f-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="8921f-166">Choisir votre fournisseur SaaS > Choisir/créer une connexion ![Configurer un connexion SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="8921f-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="8921f-167">Sélectionnez votre connexion API > créer la fonction hello ![créer la fonction de table](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="8921f-167">Select your API connection > create hello function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="8921f-168">Sélectionnez `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="8921f-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="8921f-169">Configurer hello connexion toouse la table cible.</span><span class="sxs-lookup"><span data-stu-id="8921f-169">Configure hello connection toouse your target table.</span></span> <span data-ttu-id="8921f-170">Ces paramètres varient selon les fournisseurs SaaS.</span><span class="sxs-lookup"><span data-stu-id="8921f-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="8921f-171">Ils sont décrits ci-dessous dans [Paramètres de la source de données](#datasourcesettings)
![Configurer la table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="8921f-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="8921f-172">Usage</span><span class="sxs-lookup"><span data-stu-id="8921f-172">Usage</span></span>

<span data-ttu-id="8921f-173">Cet exemple connecte table tooa nommé « Contact » avec des colonnes Id, nom et prénom.</span><span class="sxs-lookup"><span data-stu-id="8921f-173">This example connects tooa table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="8921f-174">code de Hello répertorie les entités de Contact hello dans la table de hello et journaux hello prénom et nom.</span><span class="sxs-lookup"><span data-stu-id="8921f-174">hello code lists hello Contact entities in hello table and logs hello first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="8921f-175">Liaisons</span><span class="sxs-lookup"><span data-stu-id="8921f-175">Bindings</span></span>
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
<span data-ttu-id="8921f-176">`entityId` doit être vide pour les liaisons de table.</span><span class="sxs-lookup"><span data-stu-id="8921f-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="8921f-177">`ConnectionAppSettingsKey`identifie un paramètre d’application hello qui stocke la chaîne de connexion API hello.</span><span class="sxs-lookup"><span data-stu-id="8921f-177">`ConnectionAppSettingsKey` identifies hello app setting that stores hello API connection string.</span></span> <span data-ttu-id="8921f-178">Hello paramètre d’application est créé automatiquement lorsque vous ajoutez une API connexion Bonjour intégrer l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8921f-178">hello app setting is created automatically when you add an API connection in hello integrate UI.</span></span>

<span data-ttu-id="8921f-179">Un connecteur sous forme de tableau fournit des jeux de données et chaque jeu de données contient des tables.</span><span class="sxs-lookup"><span data-stu-id="8921f-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="8921f-180">nom Hello hello par défaut du jeu de données est « default ».</span><span class="sxs-lookup"><span data-stu-id="8921f-180">hello name of hello default data set is “default.”</span></span> <span data-ttu-id="8921f-181">titres Hello pour un jeu de données et une table dans différents fournisseurs SaaS sont répertoriées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8921f-181">hello titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="8921f-182">Connecteur</span><span class="sxs-lookup"><span data-stu-id="8921f-182">Connector</span></span>|<span data-ttu-id="8921f-183">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="8921f-183">Dataset</span></span>|<span data-ttu-id="8921f-184">Table</span><span class="sxs-lookup"><span data-stu-id="8921f-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="8921f-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="8921f-185">**SharePoint**</span></span>|<span data-ttu-id="8921f-186">Site</span><span class="sxs-lookup"><span data-stu-id="8921f-186">Site</span></span>|<span data-ttu-id="8921f-187">Liste SharePoint</span><span class="sxs-lookup"><span data-stu-id="8921f-187">SharePoint List</span></span>
|<span data-ttu-id="8921f-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8921f-188">**SQL**</span></span>|<span data-ttu-id="8921f-189">Base de données</span><span class="sxs-lookup"><span data-stu-id="8921f-189">Database</span></span>|<span data-ttu-id="8921f-190">Table</span><span class="sxs-lookup"><span data-stu-id="8921f-190">Table</span></span> 
|<span data-ttu-id="8921f-191">**Google Sheet**</span><span class="sxs-lookup"><span data-stu-id="8921f-191">**Google Sheet**</span></span>|<span data-ttu-id="8921f-192">Feuille de calcul</span><span class="sxs-lookup"><span data-stu-id="8921f-192">Spreadsheet</span></span>|<span data-ttu-id="8921f-193">Feuille de calcul</span><span class="sxs-lookup"><span data-stu-id="8921f-193">Worksheet</span></span> 
|<span data-ttu-id="8921f-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="8921f-194">**Excel**</span></span>|<span data-ttu-id="8921f-195">Fichier Excel</span><span class="sxs-lookup"><span data-stu-id="8921f-195">Excel file</span></span>|<span data-ttu-id="8921f-196">Feuille</span><span class="sxs-lookup"><span data-stu-id="8921f-196">Sheet</span></span> 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="8921f-197">Utilisation en C#</span><span class="sxs-lookup"><span data-stu-id="8921f-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
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

<span data-ttu-id="8921f-198"><!--
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
##Paramètres de la source de données</span><span class="sxs-lookup"><span data-stu-id="8921f-198"><!--
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

### <a name="sql-server"></a><span data-ttu-id="8921f-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8921f-199">SQL Server</span></span>

<span data-ttu-id="8921f-200">Hello toocreate de script et de remplir le tableau de Contact hello est inférieur.</span><span class="sxs-lookup"><span data-stu-id="8921f-200">hello script toocreate and populate hello Contact table is below.</span></span> <span data-ttu-id="8921f-201">dataSetName est défini sur « default ».</span><span class="sxs-lookup"><span data-stu-id="8921f-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="8921f-202">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="8921f-202">Google Sheets</span></span>
<span data-ttu-id="8921f-203">Dans Google Docs, créez une feuille de calcul nommée `Contact`.</span><span class="sxs-lookup"><span data-stu-id="8921f-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="8921f-204">connecteur de Hello ne peut pas utiliser le nom complet de feuille de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="8921f-204">hello connector cannot use hello spreadsheet display name.</span></span> <span data-ttu-id="8921f-205">le nom interne de Hello (en gras) doit toobe utilisé en tant que dataSetName, par exemple : `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  ajouter des noms de colonne hello `Id`, `LastName`, `FirstName` toohello première ligne, puis remplir les données sur lignes suivantes.</span><span class="sxs-lookup"><span data-stu-id="8921f-205">hello internal name (in bold) needs toobe used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add hello column names `Id`, `LastName`, `FirstName` toohello first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="8921f-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="8921f-206">Salesforce</span></span>
<span data-ttu-id="8921f-207">dataSetName est défini sur « default ».</span><span class="sxs-lookup"><span data-stu-id="8921f-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="8921f-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8921f-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
