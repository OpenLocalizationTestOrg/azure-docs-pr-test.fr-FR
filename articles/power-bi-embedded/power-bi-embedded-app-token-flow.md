---
title: Authentification et autorisation avec Power BI Embedded
description: Authentification et autorisation avec Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 93027f0f5467e0b21c47bbcbc84c67cdd50b26b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="e44c6-103">Authentification et autorisation avec Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="e44c6-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="e44c6-104">Le service Power BI Embedded utilise des **clés** et des **jetons d’application** pour l’authentification et l’autorisation. Il n’utilise pas l’authentification explicite des utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="e44c6-104">The Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="e44c6-105">Dans ce modèle, votre application gère l’authentification et l’autorisation de vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="e44c6-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="e44c6-106">Quand cela est nécessaire, votre application crée et envoie les jetons d’application à notre service pour lui indiquer d’afficher le rendu du rapport demandé.</span><span class="sxs-lookup"><span data-stu-id="e44c6-106">When necessary, your app creates and sends the App Tokens that tells our service to render the requested report.</span></span> <span data-ttu-id="e44c6-107">Avec cette conception, votre application peut gérer l’authentification et l’autorisation des utilisateurs sans passer par Azure Active Directory. Cette option est toutefois possible.</span><span class="sxs-lookup"><span data-stu-id="e44c6-107">This design doesn't require your app to use Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-to-authenticate"></a><span data-ttu-id="e44c6-108">Deux méthodes d’authentification</span><span class="sxs-lookup"><span data-stu-id="e44c6-108">Two ways to authenticate</span></span>

<span data-ttu-id="e44c6-109">**Clé** : vous pouvez utiliser des clés pour tous les appels d’API REST Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="e44c6-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="e44c6-110">Les clés se trouvent sur le **portail Azure** en cliquant sur **Tous les paramètres**, puis sur **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="e44c6-110">The keys can be found in the **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="e44c6-111">Traitez toujours votre clé comme s’il s’agissait d’un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e44c6-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="e44c6-112">Ces clés ont des autorisations pour appeler toutes les API REST sur une collection d’espaces de travail donnée.</span><span class="sxs-lookup"><span data-stu-id="e44c6-112">These keys have permissions to make any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="e44c6-113">Pour utiliser une clé sur un appel REST, ajoutez l’en-tête d’autorisation suivant :</span><span class="sxs-lookup"><span data-stu-id="e44c6-113">To use a key on a REST call, add the following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="e44c6-114">**Jeton d’application** : les jetons d’application sont utilisés pour toutes les demandes d’incorporation.</span><span class="sxs-lookup"><span data-stu-id="e44c6-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="e44c6-115">Ils sont conçus pour être exécutés côté client, afin qu’ils soient limités à un rapport unique. Il est également recommandé de définir un délai d’expiration.</span><span class="sxs-lookup"><span data-stu-id="e44c6-115">They’re designed to be run client-side, so they're restricted to a single report and it’s best practice to set an expiration time.</span></span>

<span data-ttu-id="e44c6-116">Les jetons d’application sont un JWT (JSON Web Token) signé par l’une de vos clés.</span><span class="sxs-lookup"><span data-stu-id="e44c6-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="e44c6-117">Votre jeton d’application peut contenir les revendications suivantes :</span><span class="sxs-lookup"><span data-stu-id="e44c6-117">Your app token can contain the following claims:</span></span>

| <span data-ttu-id="e44c6-118">Revendication</span><span class="sxs-lookup"><span data-stu-id="e44c6-118">Claim</span></span> | <span data-ttu-id="e44c6-119">Description</span><span class="sxs-lookup"><span data-stu-id="e44c6-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e44c6-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="e44c6-120">**ver**</span></span> |<span data-ttu-id="e44c6-121">Version de jeton d’application.</span><span class="sxs-lookup"><span data-stu-id="e44c6-121">The version of the app token.</span></span> <span data-ttu-id="e44c6-122">La version actuelle est 0.2.0.</span><span class="sxs-lookup"><span data-stu-id="e44c6-122">0.2.0 is the current version.</span></span> |
| <span data-ttu-id="e44c6-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="e44c6-123">**aud**</span></span> |<span data-ttu-id="e44c6-124">Destinataire du jeton.</span><span class="sxs-lookup"><span data-stu-id="e44c6-124">The intended recipient of the token.</span></span> <span data-ttu-id="e44c6-125">Pour Power BI Embedded, utilisez : https://analysis.windows.net/powerbi/api.</span><span class="sxs-lookup"><span data-stu-id="e44c6-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="e44c6-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="e44c6-126">**iss**</span></span> |<span data-ttu-id="e44c6-127">Chaîne indiquant l’application qui a émis le jeton.</span><span class="sxs-lookup"><span data-stu-id="e44c6-127">A string indicating the application which issued the token.</span></span> |
| <span data-ttu-id="e44c6-128">**type**</span><span class="sxs-lookup"><span data-stu-id="e44c6-128">**type**</span></span> |<span data-ttu-id="e44c6-129">Type de jeton d’application en cours de création.</span><span class="sxs-lookup"><span data-stu-id="e44c6-129">The type of app token which is being created.</span></span> <span data-ttu-id="e44c6-130">Le seul type pris en charge pour l’instant est **embed**.</span><span class="sxs-lookup"><span data-stu-id="e44c6-130">Current the only supported type is **embed**.</span></span> |
| <span data-ttu-id="e44c6-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="e44c6-131">**wcn**</span></span> |<span data-ttu-id="e44c6-132">Nom de collection d’espace de travail pour lequel le jeton est émis.</span><span class="sxs-lookup"><span data-stu-id="e44c6-132">Workspace collection name the token is being issued for.</span></span> |
| <span data-ttu-id="e44c6-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="e44c6-133">**wid**</span></span> |<span data-ttu-id="e44c6-134">ID d’espace de travail pour lequel le jeton est émis.</span><span class="sxs-lookup"><span data-stu-id="e44c6-134">Workspace ID the token is being issued for.</span></span> |
| <span data-ttu-id="e44c6-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="e44c6-135">**rid**</span></span> |<span data-ttu-id="e44c6-136">ID de rapport pour lequel le jeton est émis.</span><span class="sxs-lookup"><span data-stu-id="e44c6-136">Report ID the token is being issued for.</span></span> |
| <span data-ttu-id="e44c6-137">**username** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="e44c6-137">**username** (optional)</span></span> |<span data-ttu-id="e44c6-138">Utilisé avec la fonction RLS, ceci est une chaîne qui peut aider à identifier l’utilisateur lors de l’application des règles RLS.</span><span class="sxs-lookup"><span data-stu-id="e44c6-138">Used with RLS, this is a string that can help identify the user when applying RLS rules.</span></span> |
| <span data-ttu-id="e44c6-139">**roles** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="e44c6-139">**roles** (optional)</span></span> |<span data-ttu-id="e44c6-140">Chaîne contenant les rôles à sélectionner lors de l’application des règles de sécurité au niveau des lignes.</span><span class="sxs-lookup"><span data-stu-id="e44c6-140">A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="e44c6-141">Si vous transmettez plusieurs rôles, ils doivent l’être en tant que table de chaînes.</span><span class="sxs-lookup"><span data-stu-id="e44c6-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="e44c6-142">**scp** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="e44c6-142">**scp** (optional)</span></span> |<span data-ttu-id="e44c6-143">Chaîne contenant les étendues d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="e44c6-143">A string containing the permissions scopes.</span></span> <span data-ttu-id="e44c6-144">Si vous transmettez plusieurs rôles, ils doivent l’être en tant que table de chaînes.</span><span class="sxs-lookup"><span data-stu-id="e44c6-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="e44c6-145">**exp** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="e44c6-145">**exp** (optional)</span></span> |<span data-ttu-id="e44c6-146">Indique l’heure d’expiration du jeton.</span><span class="sxs-lookup"><span data-stu-id="e44c6-146">Indicates the time in which the token will expire.</span></span> <span data-ttu-id="e44c6-147">Les heures doivent être transmises en tant qu’horodatages Unix.</span><span class="sxs-lookup"><span data-stu-id="e44c6-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="e44c6-148">**nbf** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="e44c6-148">**nbf** (optional)</span></span> |<span data-ttu-id="e44c6-149">Indique l’heure de début de validité du jeton.</span><span class="sxs-lookup"><span data-stu-id="e44c6-149">Indicates the time in which the token starts being valid.</span></span> <span data-ttu-id="e44c6-150">Les heures doivent être transmises en tant qu’horodatages Unix.</span><span class="sxs-lookup"><span data-stu-id="e44c6-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="e44c6-151">Un exemple de jeton d’application doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="e44c6-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="e44c6-152">Lorsqu’il est décodé, il doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="e44c6-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="e44c6-153">Il existe des méthodes disponibles dans les Kits de développement logiciel (SDK)qui facilitent la création de jetons d’application.</span><span class="sxs-lookup"><span data-stu-id="e44c6-153">There are methods available within the SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="e44c6-154">Par exemple, pour .NET vous pouvez consulter la classe [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) et les méthodes [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="e44c6-154">For example, for .NET you can look at the [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="e44c6-155">Pour le Kit de développement logiciel (SDK) .NET, vous pouvez vous référer à [Étendues](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="e44c6-155">For the .NET SDK, you can refer to [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="e44c6-156">Étendues</span><span class="sxs-lookup"><span data-stu-id="e44c6-156">Scopes</span></span>

<span data-ttu-id="e44c6-157">Si vous utilisez des jetons d’incorporation, vous souhaiterez peut-être limiter l’utilisation des ressources auxquelles vous donnez accès.</span><span class="sxs-lookup"><span data-stu-id="e44c6-157">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="e44c6-158">Pour cette raison, vous pouvez générer un jeton avec des étendues d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="e44c6-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="e44c6-159">Voici les étendues disponibles pour Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="e44c6-159">The following are the available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="e44c6-160">Étendue</span><span class="sxs-lookup"><span data-stu-id="e44c6-160">Scope</span></span>|<span data-ttu-id="e44c6-161">Description</span><span class="sxs-lookup"><span data-stu-id="e44c6-161">Description</span></span>|
|---|---|
|<span data-ttu-id="e44c6-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="e44c6-162">Dataset.Read</span></span>|<span data-ttu-id="e44c6-163">Fournit l’autorisation de lire un jeu de données spécifié.</span><span class="sxs-lookup"><span data-stu-id="e44c6-163">Provides permission to read the specified dataset.</span></span>|
|<span data-ttu-id="e44c6-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="e44c6-164">Dataset.Write</span></span>|<span data-ttu-id="e44c6-165">Fournit l’autorisation d’écrire sur un jeu de données spécifié.</span><span class="sxs-lookup"><span data-stu-id="e44c6-165">Provides permission to write to the specified dataset.</span></span>|
|<span data-ttu-id="e44c6-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="e44c6-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="e44c6-167">Fournit l’autorisation de lire et d’écrire sur un jeu de données spécifié.</span><span class="sxs-lookup"><span data-stu-id="e44c6-167">Provides permission to read and write to the specificed dataset.</span></span>|
|<span data-ttu-id="e44c6-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="e44c6-168">Report.Read</span></span>|<span data-ttu-id="e44c6-169">Fournit l’autorisation d’afficher un rapport spécifié.</span><span class="sxs-lookup"><span data-stu-id="e44c6-169">Provides permission to view the specified report.</span></span>|
|<span data-ttu-id="e44c6-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="e44c6-170">Report.ReadWrite</span></span>|<span data-ttu-id="e44c6-171">Fournit l’autorisation d’afficher et de modifier un rapport spécifié.</span><span class="sxs-lookup"><span data-stu-id="e44c6-171">Provides permission to view and edit the specified report.</span></span>|
|<span data-ttu-id="e44c6-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="e44c6-172">Workspace.Report.Create</span></span>|<span data-ttu-id="e44c6-173">Fournit une autorisation pour créer un rapport dans l’espace de travail spécifié.</span><span class="sxs-lookup"><span data-stu-id="e44c6-173">Provides permission to create a new report within the specified workspace.</span></span>|
|<span data-ttu-id="e44c6-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="e44c6-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="e44c6-175">Fournit une autorisation pour cloner un rapport existant dans l’espace de travail spécifié.</span><span class="sxs-lookup"><span data-stu-id="e44c6-175">Provides permission to clone an existing report within the specified workspace.</span></span>|

<span data-ttu-id="e44c6-176">Vous pouvez fournir plusieurs étendues à l’aide d’un espace entre les étendues comme suit.</span><span class="sxs-lookup"><span data-stu-id="e44c6-176">You can supply multiple scopes by using a space between the scopes like the following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="e44c6-177">**Revendications requises - Étendues**</span><span class="sxs-lookup"><span data-stu-id="e44c6-177">**Required claims - scopes**</span></span>

<span data-ttu-id="e44c6-178">scp: {scopesClaim} scopesClaim peut être une chaîne ou un tableau de chaînes répertoriant les permissions autorisées sur les ressources d’espace de travail (rapport, jeu de données, etc.)</span><span class="sxs-lookup"><span data-stu-id="e44c6-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting the allowed permissions to workspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="e44c6-179">Un jeton décodé, avec des étendues définies, ressemblerait à ceci :</span><span class="sxs-lookup"><span data-stu-id="e44c6-179">A decoded token, with scopes defined, would look similar to the following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="e44c6-180">Opérations et étendues</span><span class="sxs-lookup"><span data-stu-id="e44c6-180">Operations and scopes</span></span>

|<span data-ttu-id="e44c6-181">Opération</span><span class="sxs-lookup"><span data-stu-id="e44c6-181">Operation</span></span>|<span data-ttu-id="e44c6-182">Ressource cible</span><span class="sxs-lookup"><span data-stu-id="e44c6-182">Target resource</span></span>|<span data-ttu-id="e44c6-183">Autorisations du jeton</span><span class="sxs-lookup"><span data-stu-id="e44c6-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="e44c6-184">Créer (en mémoire) un rapport basé sur un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="e44c6-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="e44c6-185">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="e44c6-185">Dataset</span></span>|<span data-ttu-id="e44c6-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="e44c6-186">Dataset.Read</span></span>|
|<span data-ttu-id="e44c6-187">Créer (en mémoire) un rapport basé sur un jeu de données et enregistrez le rapport.</span><span class="sxs-lookup"><span data-stu-id="e44c6-187">Create (in-memory) a new report based on a dataset and save the report.</span></span>|<span data-ttu-id="e44c6-188">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="e44c6-188">Dataset</span></span>|<span data-ttu-id="e44c6-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="e44c6-189">* Dataset.Read</span></span><br><span data-ttu-id="e44c6-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="e44c6-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="e44c6-191">Afficher et explorer/modifier (en mémoire) un rapport existant.</span><span class="sxs-lookup"><span data-stu-id="e44c6-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="e44c6-192">Report.Read implies Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="e44c6-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="e44c6-193">Cela ne donne pas accès aux autorisations permettant d’enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="e44c6-193">This will not allow permissions to save edits.</span></span>|<span data-ttu-id="e44c6-194">Rapport</span><span class="sxs-lookup"><span data-stu-id="e44c6-194">Report</span></span>|<span data-ttu-id="e44c6-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="e44c6-195">Report.Read</span></span>|
|<span data-ttu-id="e44c6-196">Modifier et enregistrer un rapport existant.</span><span class="sxs-lookup"><span data-stu-id="e44c6-196">Edit and save an existing report.</span></span>|<span data-ttu-id="e44c6-197">Rapport</span><span class="sxs-lookup"><span data-stu-id="e44c6-197">Report</span></span>|<span data-ttu-id="e44c6-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="e44c6-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="e44c6-199">Enregistrer la copie d’un rapport (Enregistrer sous).</span><span class="sxs-lookup"><span data-stu-id="e44c6-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="e44c6-200">Rapport</span><span class="sxs-lookup"><span data-stu-id="e44c6-200">Report</span></span>|<span data-ttu-id="e44c6-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="e44c6-201">* Report.Read</span></span><br><span data-ttu-id="e44c6-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="e44c6-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-the-flow-works"></a><span data-ttu-id="e44c6-203">Voici comment fonctionne le flux :</span><span class="sxs-lookup"><span data-stu-id="e44c6-203">Here's how the flow works</span></span>
1. <span data-ttu-id="e44c6-204">Copiez les clés API dans votre application.</span><span class="sxs-lookup"><span data-stu-id="e44c6-204">Copy the API keys to your application.</span></span> <span data-ttu-id="e44c6-205">Vous pouvez obtenir les clés à partir du **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="e44c6-205">You can get the keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="e44c6-206">Le jeton envoie une revendication et comporte un délai d'expiration.</span><span class="sxs-lookup"><span data-stu-id="e44c6-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="e44c6-207">Le jeton est signé à l’aide des clés d'accès API.</span><span class="sxs-lookup"><span data-stu-id="e44c6-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="e44c6-208">L’utilisateur demande à consulter un rapport.</span><span class="sxs-lookup"><span data-stu-id="e44c6-208">User requests to view a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="e44c6-209">Le jeton est validé à l’aide d’une clé d'accès API.</span><span class="sxs-lookup"><span data-stu-id="e44c6-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="e44c6-210">Power BI Embedded envoie un rapport à l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e44c6-210">Power BI Embedded sends a report to user.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="e44c6-211">Après que **Power BI Embedded** envoie un rapport à l’utilisateur, ce dernier peut afficher le rapport dans votre application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="e44c6-211">After **Power BI Embedded** sends a report to the user, the user can view the report in your custom app.</span></span> <span data-ttu-id="e44c6-212">Par exemple, si vous avez importé l’ [exemple PBIX Analyse des données de vente](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), l’exemple d’application a l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="e44c6-212">For example, if you imported the [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="e44c6-213">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e44c6-213">See Also</span></span>

[<span data-ttu-id="e44c6-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="e44c6-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="e44c6-215">Prise en main de l’exemple Microsoft Power BI Embedded Preview</span><span class="sxs-lookup"><span data-stu-id="e44c6-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="e44c6-216">Scénarios Microsoft Power BI Embedded courants</span><span class="sxs-lookup"><span data-stu-id="e44c6-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="e44c6-217">Prise en main de Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="e44c6-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="e44c6-218">Dépôt Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="e44c6-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="e44c6-219">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="e44c6-219">More questions?</span></span> [<span data-ttu-id="e44c6-220">Essayer la communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="e44c6-220">Try the Power BI Community</span></span>](http://community.powerbi.com/)

