---
title: aaaAuthenticating et autorisation avec Power BI Embedded
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
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="d8490-103">Authentification et autorisation avec Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d8490-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="d8490-104">Hello service Power BI Embedded utilise **clés** et **application jetons** pour l’authentification et d’autorisation, au lieu de l’authentification de l’utilisateur final explicite.</span><span class="sxs-lookup"><span data-stu-id="d8490-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="d8490-105">Dans ce modèle, votre application gère l’authentification et l’autorisation de vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="d8490-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="d8490-106">Lorsque cela est nécessaire, votre application crée et envoie les jetons d’application hello qui indique à notre toorender service hello rapport demandé.</span><span class="sxs-lookup"><span data-stu-id="d8490-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="d8490-107">Cette conception ne requiert pas votre toouse application Azure Active Directory pour l’authentification des utilisateurs et l’autorisation, bien que vous puissiez toujours.</span><span class="sxs-lookup"><span data-stu-id="d8490-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="d8490-108">Deux façons tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="d8490-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="d8490-109">**Clé** : vous pouvez utiliser des clés pour tous les appels d’API REST Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="d8490-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="d8490-110">les clés Hello se trouvent dans hello **portail Azure** en cliquant sur **tous les paramètres** , puis **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="d8490-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="d8490-111">Traitez toujours votre clé comme s’il s’agissait d’un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d8490-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="d8490-112">Ces clés ont toomake autorisations toute API REST appeler sur une collection de l’espace de travail particulier.</span><span class="sxs-lookup"><span data-stu-id="d8490-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="d8490-113">toouse une clé sur un appel REST, ajoutez hello suivant l’en-tête d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="d8490-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="d8490-114">**Jeton d’application** : les jetons d’application sont utilisés pour toutes les demandes d’incorporation.</span><span class="sxs-lookup"><span data-stu-id="d8490-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="d8490-115">Ils sont conçus toobe exécuter côté client, afin qu’elles soient restreints tooa unique tooset de pratique meilleur rapport et son délai d’expiration.</span><span class="sxs-lookup"><span data-stu-id="d8490-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="d8490-116">Les jetons d’application sont un JWT (JSON Web Token) signé par l’une de vos clés.</span><span class="sxs-lookup"><span data-stu-id="d8490-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="d8490-117">Votre jeton d’application peut contenir hello suivant revendications :</span><span class="sxs-lookup"><span data-stu-id="d8490-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="d8490-118">Revendication</span><span class="sxs-lookup"><span data-stu-id="d8490-118">Claim</span></span> | <span data-ttu-id="d8490-119">Description</span><span class="sxs-lookup"><span data-stu-id="d8490-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d8490-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="d8490-120">**ver**</span></span> |<span data-ttu-id="d8490-121">version de Hello du jeton d’application hello.</span><span class="sxs-lookup"><span data-stu-id="d8490-121">hello version of hello app token.</span></span> <span data-ttu-id="d8490-122">0.2.0 est la version actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d8490-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="d8490-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="d8490-123">**aud**</span></span> |<span data-ttu-id="d8490-124">Hello destiné destinataire du jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="d8490-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="d8490-125">Pour Power BI Embedded, utilisez : https://analysis.windows.net/powerbi/api.</span><span class="sxs-lookup"><span data-stu-id="d8490-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="d8490-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="d8490-126">**iss**</span></span> |<span data-ttu-id="d8490-127">Chaîne indiquant l’application hello qui a émis le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="d8490-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="d8490-128">**type**</span><span class="sxs-lookup"><span data-stu-id="d8490-128">**type**</span></span> |<span data-ttu-id="d8490-129">type Hello du jeton d’application en cours de création.</span><span class="sxs-lookup"><span data-stu-id="d8490-129">hello type of app token which is being created.</span></span> <span data-ttu-id="d8490-130">Type hello uniquement pris en charge en cours est **incorporer**.</span><span class="sxs-lookup"><span data-stu-id="d8490-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="d8490-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="d8490-131">**wcn**</span></span> |<span data-ttu-id="d8490-132">Jeton hello de nom d’espace de travail collection est émise.</span><span class="sxs-lookup"><span data-stu-id="d8490-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="d8490-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="d8490-133">**wid**</span></span> |<span data-ttu-id="d8490-134">Le jeton d’espace de travail ID hello est envoyée.</span><span class="sxs-lookup"><span data-stu-id="d8490-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="d8490-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="d8490-135">**rid**</span></span> |<span data-ttu-id="d8490-136">Le jeton d’état ID hello est envoyée.</span><span class="sxs-lookup"><span data-stu-id="d8490-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="d8490-137">**username** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="d8490-137">**username** (optional)</span></span> |<span data-ttu-id="d8490-138">Utilisé avec la sécurité RLS, ceci est une chaîne qui peut aider à identifier l’utilisateur de hello lors de l’application des règles RLS.</span><span class="sxs-lookup"><span data-stu-id="d8490-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="d8490-139">**roles** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="d8490-139">**roles** (optional)</span></span> |<span data-ttu-id="d8490-140">Chaîne contenant le hello rôles tooselect lors de l’application des règles de sécurité de niveau ligne.</span><span class="sxs-lookup"><span data-stu-id="d8490-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="d8490-141">Si vous transmettez plusieurs rôles, ils doivent l’être en tant que table de chaînes.</span><span class="sxs-lookup"><span data-stu-id="d8490-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="d8490-142">**scp** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="d8490-142">**scp** (optional)</span></span> |<span data-ttu-id="d8490-143">Chaîne qui contient les étendues d’autorisations hello.</span><span class="sxs-lookup"><span data-stu-id="d8490-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="d8490-144">Si vous transmettez plusieurs rôles, ils doivent l’être en tant que table de chaînes.</span><span class="sxs-lookup"><span data-stu-id="d8490-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="d8490-145">**exp** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="d8490-145">**exp** (optional)</span></span> |<span data-ttu-id="d8490-146">Indique le temps hello dans le hello jeton expire.</span><span class="sxs-lookup"><span data-stu-id="d8490-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="d8490-147">Les heures doivent être transmises en tant qu’horodatages Unix.</span><span class="sxs-lookup"><span data-stu-id="d8490-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="d8490-148">**nbf** (facultatif)</span><span class="sxs-lookup"><span data-stu-id="d8490-148">**nbf** (optional)</span></span> |<span data-ttu-id="d8490-149">Indique le temps hello dans le hello jeton commence en cours valide.</span><span class="sxs-lookup"><span data-stu-id="d8490-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="d8490-150">Les heures doivent être transmises en tant qu’horodatages Unix.</span><span class="sxs-lookup"><span data-stu-id="d8490-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="d8490-151">Un exemple de jeton d’application doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="d8490-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="d8490-152">Lorsqu’il est décodé, il doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="d8490-152">When decoded, it will look something like this:</span></span>

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

<span data-ttu-id="d8490-153">Méthodes sont disponibles dans les kits de développement logiciel qui facilitent la création d’apptokens de hello.</span><span class="sxs-lookup"><span data-stu-id="d8490-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="d8490-154">Par exemple, pour .NET vous pouvez examiner hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) classe et hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) méthodes.</span><span class="sxs-lookup"><span data-stu-id="d8490-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="d8490-155">Pour hello .NET SDK, vous pouvez vous reporter trop[étendues](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="d8490-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="d8490-156">Étendues</span><span class="sxs-lookup"><span data-stu-id="d8490-156">Scopes</span></span>

<span data-ttu-id="d8490-157">Lorsque vous utilisez les jetons incorporé, vous souhaiterez toorestrict de l’utilisation d’hello que vous autoriser à accéder.</span><span class="sxs-lookup"><span data-stu-id="d8490-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="d8490-158">Dans cette optique, vous pouvez générer un jeton avec des autorisations étendues.</span><span class="sxs-lookup"><span data-stu-id="d8490-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="d8490-159">Hello Voici étendues disponibles de hello pour Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="d8490-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="d8490-160">Scope</span><span class="sxs-lookup"><span data-stu-id="d8490-160">Scope</span></span>|<span data-ttu-id="d8490-161">Description</span><span class="sxs-lookup"><span data-stu-id="d8490-161">Description</span></span>|
|---|---|
|<span data-ttu-id="d8490-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="d8490-162">Dataset.Read</span></span>|<span data-ttu-id="d8490-163">Fournit l’autorisation tooread hello spécifié le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="d8490-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="d8490-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="d8490-164">Dataset.Write</span></span>|<span data-ttu-id="d8490-165">Fournit des toohello de toowrite d’autorisation spécifié jeu de données.</span><span class="sxs-lookup"><span data-stu-id="d8490-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="d8490-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="d8490-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="d8490-167">Fournit le dataset sont recompilé toohello autorisation tooread et en écriture.</span><span class="sxs-lookup"><span data-stu-id="d8490-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="d8490-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="d8490-168">Report.Read</span></span>|<span data-ttu-id="d8490-169">Fournit l’autorisation tooview hello spécifié de rapport.</span><span class="sxs-lookup"><span data-stu-id="d8490-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="d8490-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="d8490-170">Report.ReadWrite</span></span>|<span data-ttu-id="d8490-171">Fournit la modifier et autorisation tooview hello rapport spécifié.</span><span class="sxs-lookup"><span data-stu-id="d8490-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="d8490-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="d8490-172">Workspace.Report.Create</span></span>|<span data-ttu-id="d8490-173">Fournit des autorisation toocreate un nouveau rapport dans hello spécifié espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d8490-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="d8490-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="d8490-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="d8490-175">Fournit des autorisation tooclone un rapport existant dans hello spécifié espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d8490-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="d8490-176">Vous pouvez fournir plusieurs étendues à l’aide d’un espace entre les portées hello hello suivante.</span><span class="sxs-lookup"><span data-stu-id="d8490-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="d8490-177">**Revendications requises - Étendues**</span><span class="sxs-lookup"><span data-stu-id="d8490-177">**Required claims - scopes**</span></span>

<span data-ttu-id="d8490-178">SCP : {scopesClaim} scopesClaim peut être une chaîne ou un tableau de chaînes, en notant hello les autorisations accordées tooworkspace ressources (rapports, jeu de données, etc.).</span><span class="sxs-lookup"><span data-stu-id="d8490-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="d8490-179">Un jeton décodé, avec des étendues définies, se présenterait comme toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="d8490-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

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

### <a name="operations-and-scopes"></a><span data-ttu-id="d8490-180">Opérations et étendues</span><span class="sxs-lookup"><span data-stu-id="d8490-180">Operations and scopes</span></span>

|<span data-ttu-id="d8490-181">Opération</span><span class="sxs-lookup"><span data-stu-id="d8490-181">Operation</span></span>|<span data-ttu-id="d8490-182">Ressource cible</span><span class="sxs-lookup"><span data-stu-id="d8490-182">Target resource</span></span>|<span data-ttu-id="d8490-183">Autorisations du jeton</span><span class="sxs-lookup"><span data-stu-id="d8490-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="d8490-184">Créer (en mémoire) un rapport basé sur un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="d8490-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="d8490-185">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="d8490-185">Dataset</span></span>|<span data-ttu-id="d8490-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="d8490-186">Dataset.Read</span></span>|
|<span data-ttu-id="d8490-187">Créer (mémoire) un rapport basé sur un jeu de données et enregistrer le rapport de hello.</span><span class="sxs-lookup"><span data-stu-id="d8490-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="d8490-188">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="d8490-188">Dataset</span></span>|<span data-ttu-id="d8490-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="d8490-189">* Dataset.Read</span></span><br><span data-ttu-id="d8490-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="d8490-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="d8490-191">Afficher et explorer/modifier (en mémoire) un rapport existant.</span><span class="sxs-lookup"><span data-stu-id="d8490-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="d8490-192">Report.Read implies Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="d8490-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="d8490-193">Cela n’autorise pas les autorisations toosave modifications.</span><span class="sxs-lookup"><span data-stu-id="d8490-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="d8490-194">Rapport</span><span class="sxs-lookup"><span data-stu-id="d8490-194">Report</span></span>|<span data-ttu-id="d8490-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="d8490-195">Report.Read</span></span>|
|<span data-ttu-id="d8490-196">Modifier et enregistrer un rapport existant.</span><span class="sxs-lookup"><span data-stu-id="d8490-196">Edit and save an existing report.</span></span>|<span data-ttu-id="d8490-197">Rapport</span><span class="sxs-lookup"><span data-stu-id="d8490-197">Report</span></span>|<span data-ttu-id="d8490-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="d8490-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="d8490-199">Enregistrer la copie d’un rapport (Enregistrer sous).</span><span class="sxs-lookup"><span data-stu-id="d8490-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="d8490-200">Rapport</span><span class="sxs-lookup"><span data-stu-id="d8490-200">Report</span></span>|<span data-ttu-id="d8490-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="d8490-201">* Report.Read</span></span><br><span data-ttu-id="d8490-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="d8490-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="d8490-203">Voici comment fonctionne les flux de hello</span><span class="sxs-lookup"><span data-stu-id="d8490-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="d8490-204">Copiez hello API clés tooyour application.</span><span class="sxs-lookup"><span data-stu-id="d8490-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="d8490-205">Vous pouvez obtenir les clés hello **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="d8490-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="d8490-206">Le jeton envoie une revendication et comporte un délai d'expiration.</span><span class="sxs-lookup"><span data-stu-id="d8490-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="d8490-207">Le jeton est signé à l’aide des clés d'accès API.</span><span class="sxs-lookup"><span data-stu-id="d8490-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="d8490-208">Utilisateur demande tooview un rapport.</span><span class="sxs-lookup"><span data-stu-id="d8490-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="d8490-209">Le jeton est validé à l’aide d’une clé d'accès API.</span><span class="sxs-lookup"><span data-stu-id="d8490-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="d8490-210">Power BI Embedded envoie un rapport toouser.</span><span class="sxs-lookup"><span data-stu-id="d8490-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="d8490-211">Après avoir **Power BI Embedded** envoie un utilisateur toohello de rapports, utilisateur de hello peut afficher des rapports de hello dans votre application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d8490-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="d8490-212">Par exemple, si vous avez importé hello [exemple d’analyse de vente données PBIX](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello exemple d’application web ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="d8490-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="d8490-213">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d8490-213">See Also</span></span>

[<span data-ttu-id="d8490-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="d8490-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="d8490-215">Prise en main de l’exemple Microsoft Power BI Embedded Preview</span><span class="sxs-lookup"><span data-stu-id="d8490-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="d8490-216">Scénarios Microsoft Power BI Embedded courants</span><span class="sxs-lookup"><span data-stu-id="d8490-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="d8490-217">Prise en main de Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d8490-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="d8490-218">Dépôt Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="d8490-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="d8490-219">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="d8490-219">More questions?</span></span> [<span data-ttu-id="d8490-220">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="d8490-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

