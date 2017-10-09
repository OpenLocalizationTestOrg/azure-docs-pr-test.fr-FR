---
title: "aaaProtect un principal de l’API Web avec Azure Active Directory et gestion des API | Documents Microsoft"
description: "Découvrez comment tooprotect un principal de l’API Web avec Azure Active Directory et gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="6cb04-103">Comment tooprotect un principal de l’API Web avec Azure Active Directory et gestion des API</span><span class="sxs-lookup"><span data-stu-id="6cb04-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="6cb04-104">Hello suivant vidéo montre comment toobuild un principal de l’API Web et le protéger à l’aide du protocole OAuth 2.0 avec Azure Active Directory et gestion des API.</span><span class="sxs-lookup"><span data-stu-id="6cb04-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="6cb04-105">Cet article fournit une vue d’ensemble et des informations supplémentaires pour hello les étapes dans la vidéo de hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="6cb04-106">Cette vidéo 24 minutes vous montre comment faire pour :</span><span class="sxs-lookup"><span data-stu-id="6cb04-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="6cb04-107">générer un serveur principal d’API Web et le protéger avec AAD (début à 1:30) ;</span><span class="sxs-lookup"><span data-stu-id="6cb04-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="6cb04-108">Importer hello API de gestion des API - commençant à 7:10</span><span class="sxs-lookup"><span data-stu-id="6cb04-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="6cb04-109">Configurer hello développeur toocall portail hello API - commençant à 9:09</span><span class="sxs-lookup"><span data-stu-id="6cb04-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="6cb04-110">Configurer un Bonjour de toocall d’application de bureau API - commençant à 18:08</span><span class="sxs-lookup"><span data-stu-id="6cb04-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="6cb04-111">Configurer un toopre de stratégie de validation de jetons Web JSON-autoriser les demandes - en commençant à 20:47</span><span class="sxs-lookup"><span data-stu-id="6cb04-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="6cb04-112">Création d’un répertoire Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cb04-112">Create an Azure AD directory</span></span>
<span data-ttu-id="6cb04-113">toosecure votre API Web sauvegardé à l’aide d’Azure Active Directory vous devez avoir un un locataire AAD.</span><span class="sxs-lookup"><span data-stu-id="6cb04-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="6cb04-114">Dans cette vidéo, on utilise un client nommé **APIMDemo** .</span><span class="sxs-lookup"><span data-stu-id="6cb04-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="6cb04-115">toocreate un locataire AAD, connectez-vous toohello [portail classique Azure](https://manage.windowsazure.com) et cliquez sur **nouveau**->**des Services d’application**->**Active Répertoire**->**active**->**création personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="6cb04-117">Dans cet exemple, on crée un répertoire nommé **APIMDemo** avec un domaine par défaut nommé **DemoAPIM.onmicrosoft.com**. Ce répertoire est utilisé dans l’ensemble de vidéo de hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="6cb04-119">Création d’un service API web protégé par Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6cb04-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="6cb04-120">Dans cette étape, un serveur principal d’API web est créé à l’aide de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6cb04-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="6cb04-121">Cette étape de hello vidéo démarre à 1 h 30.</span><span class="sxs-lookup"><span data-stu-id="6cb04-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="6cb04-122">projet de service principal d’API Web toocreate dans, cliquez sur Visual Studio **fichier**->**nouveau**->**projet**, puis choisissez **Web ASP.NET Application** de hello **Web** liste de modèles.</span><span class="sxs-lookup"><span data-stu-id="6cb04-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="6cb04-123">Dans cette vidéo hello projet se nomme **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="6cb04-124">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="6cb04-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="6cb04-126">Cliquez sur **API Web** de hello **, sélectionnez un modèle de liste** toocreate un projet d’API Web.</span><span class="sxs-lookup"><span data-stu-id="6cb04-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="6cb04-127">Cliquez sur le tooconfigure Azure Active Authentication **modifier l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![Nouveau projet][api-management-new-project]

<span data-ttu-id="6cb04-129">Cliquez sur **comptes professionnels**et spécifiez hello **domaine** de votre locataire AAD.</span><span class="sxs-lookup"><span data-stu-id="6cb04-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="6cb04-130">Bonjour de cet exemple est domaine **DemoAPIM.onmicrosoft.com**. domaine hello de votre annuaire peut être obtenue à partir de hello **domaines** onglet de votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="6cb04-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![Domaines][api-management-aad-domains]

<span data-ttu-id="6cb04-132">Configurer les paramètres de hello souhaité Bonjour **modifier l’authentification** boîte de dialogue et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![Modifier l’authentification][api-management-change-authentication]

<span data-ttu-id="6cb04-134">Lorsque vous cliquez sur **OK** Visual Studio va tenter de tooregister votre application avec votre annuaire Azure AD et vous pouvez être invité à toosign dans par Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6cb04-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="6cb04-135">Connectez-vous à l’aide d’un compte administrateur de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="6cb04-135">Sign in using an administrative account for your directory.</span></span>

![Connectez-vous à tooVisual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="6cb04-137">zone de ce projet en tant qu’un hello de vérification Azure Web API tooconfigure pour **hôte hello cloud** puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![Nouveau projet][api-management-new-project-cloud]

<span data-ttu-id="6cb04-139">Vous pouvez être invité à toosign dans tooAzure, et vous pouvez ensuite configurer hello Web App.</span><span class="sxs-lookup"><span data-stu-id="6cb04-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![Configuration][api-management-configure-web-app]

<span data-ttu-id="6cb04-141">Dans cet exemple, on spécifie un nouveau **Plan App Service** nommé **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="6cb04-142">Cliquez sur **OK** tooconfigure hello Web App et créer le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="6cb04-143">Ajouter le projet d’API Web hello code toohello</span><span class="sxs-lookup"><span data-stu-id="6cb04-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="6cb04-144">étape suivante Hello vidéo de hello ajoute le projet d’API Web toohello hello code.</span><span class="sxs-lookup"><span data-stu-id="6cb04-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="6cb04-145">Cette étape démarre à 4’35’’.</span><span class="sxs-lookup"><span data-stu-id="6cb04-145">This step starts at 4:35.</span></span>

<span data-ttu-id="6cb04-146">Hello API Web dans cet exemple implémente un service de calculatrice de base à l’aide d’un modèle et un contrôleur.</span><span class="sxs-lookup"><span data-stu-id="6cb04-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="6cb04-147">avec le bouton droit de modèle de hello tooadd pour service de hello, **modèles** dans **l’Explorateur de solutions** et choisissez **ajouter**, **classe**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="6cb04-148">Nom de classe hello `CalcInput` et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="6cb04-149">Ajoutez hello suivant `using` haut de toohello d’instruction de hello `CalcInput.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="6cb04-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="6cb04-150">Remplacez classe hello généré par hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="6cb04-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="6cb04-151">Cliquez droit sur **Contrôleurs** dans l’**Explorateur de solutions** et choisissez **Ajouter**->**Contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="6cb04-152">Choisissez **Contrôleur API 2 web - Vide**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="6cb04-153">Type **CalcController** pour hello contrôleur nom, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![Ajouter un contrôleur][api-management-add-controller]

<span data-ttu-id="6cb04-155">Ajoutez hello suivant `using` haut de toohello d’instruction de hello `CalcController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="6cb04-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="6cb04-156">Remplacez classe de contrôleur hello généré par hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="6cb04-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="6cb04-157">Ce code implémente hello `Add`, `Subtract`, `Multiply`, et `Divide` opérations Hello API de calculatrice de base.</span><span class="sxs-lookup"><span data-stu-id="6cb04-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="6cb04-158">Appuyez sur **F6** toobuild et vérifiez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="6cb04-159">Publier hello projet tooAzure</span><span class="sxs-lookup"><span data-stu-id="6cb04-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="6cb04-160">Projet est publié tooAzure cette hello étape Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6cb04-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="6cb04-161">Cette étape de hello vidéo commence à 5 h 45.</span><span class="sxs-lookup"><span data-stu-id="6cb04-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="6cb04-162">toopublish hello tooAzure du projet, avec le bouton droit hello **APIMAADDemo** de projet dans Visual Studio et choisissez **publier**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="6cb04-163">Conserver les paramètres par défaut de hello Bonjour **publier le site Web** boîte de dialogue et cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![Publier un site web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="6cb04-165">Autoriser l’application de service principal toohello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cb04-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="6cb04-166">Une nouvelle application de service principal de hello est créée dans votre annuaire Azure AD en tant que partie de la configuration de hello et processus de publication de votre projet d’API Web.</span><span class="sxs-lookup"><span data-stu-id="6cb04-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="6cb04-167">Dans cette étape de hello vidéo, en commençant à 6:13, autorisations sont accordées de toohello API Web principal.</span><span class="sxs-lookup"><span data-stu-id="6cb04-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![Application][api-management-aad-backend-app]

<span data-ttu-id="6cb04-169">Cliquez sur nom hello hello autorisations des applications tooconfigure hello requis.</span><span class="sxs-lookup"><span data-stu-id="6cb04-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="6cb04-170">Accédez toohello **configurer** onglet et faites défiler toohello **autorisations tooother applications** section.</span><span class="sxs-lookup"><span data-stu-id="6cb04-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="6cb04-171">Cliquez sur hello **autorisations d’Application** liste déroulante en regard de **Windows** **Azure Active Directory**, la case hello pour **lire les données d’annuaire**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![Ajout d’autorisations][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="6cb04-173">Si **Windows** **Azure Active Directory** est ne pas répertorié sous autorisations tooother applications, cliquez sur **ajouter application** et l’ajouter à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="6cb04-174">Prenez note de hello **URI Id d’application** pour une utilisation dans une étape ultérieure lorsqu’une application Azure AD est configurée pour le portail des développeurs gestion des API hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![URI ID d’application][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="6cb04-176">Importer hello Web API de gestion des API</span><span class="sxs-lookup"><span data-stu-id="6cb04-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="6cb04-177">API est configurés à partir du portail de publication d’API hello, qui est accessible via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6cb04-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="6cb04-178">tooreach, cliquez sur **portail de publication** à partir de la barre d’outils hello de votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="6cb04-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="6cb04-179">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [gérer votre première API] [ Manage your first API] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6cb04-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![Portail des éditeurs][api-management-management-console]

<span data-ttu-id="6cb04-181">Les opérations peuvent être [ajoutés manuellement les tooAPIs](api-management-howto-add-operations.md), ou elles peuvent être importées.</span><span class="sxs-lookup"><span data-stu-id="6cb04-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="6cb04-182">Dans cette vidéo, à partir de 6’40’’, les opérations sont importées au format Swagger.</span><span class="sxs-lookup"><span data-stu-id="6cb04-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="6cb04-183">Créez un fichier nommé `calcapi.json` avec suivant le contenu et l’enregistrer tooyour ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6cb04-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="6cb04-184">Vérifiez que hello `host` attribut pointe tooyour API Web principal.</span><span class="sxs-lookup"><span data-stu-id="6cb04-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="6cb04-185">Dans cet exemple, on utilise `"host": "apimaaddemo.azurewebsites.net"` .</span><span class="sxs-lookup"><span data-stu-id="6cb04-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="6cb04-186">calcul de hello tooimport API, cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **API d’importation**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Bouton Importer l’API][api-management-import-api]

<span data-ttu-id="6cb04-188">Effectuer hello suivant les étapes tooconfigure hello calculatrice API.</span><span class="sxs-lookup"><span data-stu-id="6cb04-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="6cb04-189">Cliquez sur **à partir du fichier**, parcourir toohello `calculator.json` fichier que vous avez enregistré, puis cliquez sur hello **Swagger** case d’option.</span><span class="sxs-lookup"><span data-stu-id="6cb04-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="6cb04-190">Type **calc** dans hello **suffixe d’URL d’API Web** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="6cb04-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="6cb04-191">Cliquez sur Bonjour **produits (facultatifs)** et sélectionnez **Starter**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="6cb04-192">Cliquez sur **enregistrer** tooimport hello API.</span><span class="sxs-lookup"><span data-stu-id="6cb04-192">Click **Save** tooimport hello API.</span></span>

![Ajouter une nouvelle API][api-management-import-new-api]

<span data-ttu-id="6cb04-194">Une fois les API hello est importé, hello page Résumé pour l’API de hello s’affiche dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="6cb04-195">Appeler les API hello sans succès à partir du portail des développeurs hello</span><span class="sxs-lookup"><span data-stu-id="6cb04-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="6cb04-196">À ce stade, hello API a été importé dans la gestion des API, mais ne peut pas encore être appelée avec succès à partir du portail des développeurs hello, car le service principal de hello est protégé par l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6cb04-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="6cb04-197">Cela est illustré dans la vidéo hello commençant à 7:40 à l’aide de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="6cb04-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="6cb04-198">Cliquez sur **portail des développeurs** de hello en haut à droite du portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![Portail des développeurs][api-management-developer-portal-menu]

<span data-ttu-id="6cb04-200">Cliquez sur **API** et cliquez sur hello **calculatrice** API.</span><span class="sxs-lookup"><span data-stu-id="6cb04-200">Click **APIs** and click hello **Calculator** API.</span></span>

![Portail des développeurs][api-management-dev-portal-apis]

<span data-ttu-id="6cb04-202">Cliquez sur **Essayer**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-202">Click **Try it**.</span></span>

![Essayer][api-management-dev-portal-try-it]

<span data-ttu-id="6cb04-204">Cliquez sur **envoyer** et notez l’état de réponse hello de **401 non autorisé**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![Envoyer][api-management-dev-portal-send-401]

<span data-ttu-id="6cb04-206">demande de Hello n’est pas autorisé, car les API de service principal hello est protégé par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6cb04-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="6cb04-207">Avant d’appeler correctement les API de hello portail des développeurs hello doit être développeurs tooauthorize configuré à l’aide d’OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="6cb04-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="6cb04-208">Ce processus est décrit dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="6cb04-209">Portail des développeurs hello inscrire comme une application AAD</span><span class="sxs-lookup"><span data-stu-id="6cb04-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="6cb04-210">Hello première étape de configuration aux développeurs tooauthorize portail hello développeur à l’aide d’OAuth 2.0 est un portail des développeurs hello tooregister comme une application AAD.</span><span class="sxs-lookup"><span data-stu-id="6cb04-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="6cb04-211">Cela est illustré en commençant à 8:27 vidéo de hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="6cb04-212">Accédez locataire toohello Azure AD à partir de la première étape de hello de cette vidéo, dans cet exemple **APIMDemo** et accédez toohello **Applications** onglet.</span><span class="sxs-lookup"><span data-stu-id="6cb04-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![Nouvelle application][api-management-aad-new-application-devportal]

<span data-ttu-id="6cb04-214">Cliquez sur hello **ajouter** bouton toocreate une application Azure Active Directory, puis choisissez **ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Nouvelle application][api-management-new-aad-application-menu]

<span data-ttu-id="6cb04-216">Choisissez **Web application et/ou API Web**, entrez un nom et cliquez sur la flèche suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="6cb04-217">Dans cet exemple, on utilise **APIMDeveloperPortal** .</span><span class="sxs-lookup"><span data-stu-id="6cb04-217">In this example **APIMDeveloperPortal** is used.</span></span>

![Nouvelle application][api-management-aad-new-application-devportal-1]

<span data-ttu-id="6cb04-219">Pour **URL de connexion** entrez hello les URL de votre service de gestion des API et ajoutez `/signin`.</span><span class="sxs-lookup"><span data-stu-id="6cb04-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="6cb04-220">Dans cet exemple, on utilise `https://contoso5.portal.azure-api.net/signin` .</span><span class="sxs-lookup"><span data-stu-id="6cb04-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="6cb04-221">Pour **URL Id d’application** entrez hello les URL de votre service de gestion des API et l’ajout de caractères uniques.</span><span class="sxs-lookup"><span data-stu-id="6cb04-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="6cb04-222">Il peut s’agir des caractères de votre choix. Dans cet exemple, on utilise `https://contoso5.portal.azure-api.net/dp`.</span><span class="sxs-lookup"><span data-stu-id="6cb04-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="6cb04-223">Lorsque hello souhaité **propriétés de l’application** sont configurées, cliquez sur application de hello toocreate hello case à cocher.</span><span class="sxs-lookup"><span data-stu-id="6cb04-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![Nouvelle application][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="6cb04-225">Configuration du serveur d’autorisation OAuth 2.0 dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="6cb04-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="6cb04-226">étape suivante de Hello est tooconfigure un serveur d’autorisation OAuth 2.0 dans Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="6cb04-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="6cb04-227">Cette étape est illustrée dans hello vidéo en commençant à 9:43.</span><span class="sxs-lookup"><span data-stu-id="6cb04-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="6cb04-228">Cliquez sur **sécurité** à partir du menu Gestion des API hello hello gauche, cliquez sur **OAuth 2.0**, puis cliquez sur **ajouter une autorisation** server.</span><span class="sxs-lookup"><span data-stu-id="6cb04-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Ajouter un serveur d’autorisation][api-management-add-authorization-server]

<span data-ttu-id="6cb04-230">Entrez un nom et une description facultative dans hello **nom** et **Description** champs.</span><span class="sxs-lookup"><span data-stu-id="6cb04-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="6cb04-231">Ces champs sont le serveur de d’autorisation hello OAuth 2.0 tooidentify utilisés au sein de l’instance de service de gestion des API hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="6cb04-232">Dans cet exemple, on utilise **Démonstration de serveur d’autorisation** .</span><span class="sxs-lookup"><span data-stu-id="6cb04-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="6cb04-233">Plus tard lorsque vous spécifiez une toobe de serveur OAuth 2.0 utilisé pour l’authentification d’API, vous allez sélectionner ce nom.</span><span class="sxs-lookup"><span data-stu-id="6cb04-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="6cb04-234">Pourquoi **URL de la page d’inscription Client** Entrez une valeur d’espace réservé tel que `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="6cb04-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="6cb04-235">Hello **URL de la page d’inscription Client** points toohello page que les utilisateurs peuvent utiliser toocreate et configurer leurs propres comptes pour les fournisseurs OAuth 2.0 qui prennent en charge la gestion des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6cb04-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="6cb04-236">Dans cet exemple, les utilisateurs ne peuvent pas créer et configurer leurs propres comptes. Ainsi, on utilise un espace réservé.</span><span class="sxs-lookup"><span data-stu-id="6cb04-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Ajouter un serveur d’autorisation][api-management-add-authorization-server-1]

<span data-ttu-id="6cb04-238">Ensuite, spécifiez l’**URL de point de terminaison d’autorisation** et l’**URL de point de terminaison de jeton**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Serveur d’autorisation][api-management-add-authorization-server-1a]

<span data-ttu-id="6cb04-240">Ces valeurs peuvent être récupérées à partir de hello **points de terminaison** page Hello application AAD que vous avez créé pour le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="6cb04-241">points de terminaison tooaccess hello accédez toohello **configurer** onglet pour l’application de AAD hello et cliquez sur **afficher les points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![Application][api-management-aad-devportal-application]

![Afficher les points de terminaison][api-management-aad-view-endpoints]

<span data-ttu-id="6cb04-244">Hello de copie **point de terminaison d’autorisation OAuth 2.0** et collez-le dans hello **URL de point de terminaison d’autorisation** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="6cb04-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![Ajouter un serveur d’autorisation][api-management-add-authorization-server-2]

<span data-ttu-id="6cb04-246">Hello de copie **point de terminaison de jeton OAuth 2.0** et collez-le dans hello **URL de point de terminaison de jeton** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="6cb04-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![Ajouter un serveur d’autorisation][api-management-add-authorization-server-2a]

<span data-ttu-id="6cb04-248">En outre toopasting dans le point de terminaison de jeton hello, ajouter un paramètre de corps supplémentaire nommé **ressource** et pour la valeur de hello utiliser hello **URI Id d’application** de hello application AAD pour service hello principal qui a été créé lors de la publication de projet de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![URI ID d’application][api-management-aad-sso-uri]

<span data-ttu-id="6cb04-250">Ensuite, spécifiez les informations d’identification du client hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="6cb04-251">Ceux-ci sont des informations d’identification de hello pour la ressource hello tooaccess, hello dans ce cas le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="6cb04-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![Informations d'identification du client][api-management-client-credentials]

<span data-ttu-id="6cb04-253">tooget hello **Id Client**, accédez toohello **configurer** onglet Hello application AAD pour hello portal et la copie du développeur hello **Id Client**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="6cb04-254">tooget hello **clé secrète Client** cliquez sur hello **sélectionner une durée** déroulante Bonjour **clés** section et spécifiez un intervalle.</span><span class="sxs-lookup"><span data-stu-id="6cb04-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="6cb04-255">Dans cet exemple, on utilise la valeur 1 an.</span><span class="sxs-lookup"><span data-stu-id="6cb04-255">In this example 1 year is used.</span></span>

![ID client][api-management-aad-client-id]

<span data-ttu-id="6cb04-257">Cliquez sur **enregistrer** clé hello toosave hello configuration et l’affichage.</span><span class="sxs-lookup"><span data-stu-id="6cb04-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6cb04-258">Notez sa valeur.</span><span class="sxs-lookup"><span data-stu-id="6cb04-258">Make a note of this key.</span></span> <span data-ttu-id="6cb04-259">Une fois que vous fermez la fenêtre de configuration d’Azure Active Directory hello, clé de hello Impossible d’afficher à nouveau.</span><span class="sxs-lookup"><span data-stu-id="6cb04-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="6cb04-260">Copie hello toohello clé coller depuis le Presse-papiers, portail de publication commutateur toohello arrière, clé de hello en hello **clé secrète Client** zone de texte, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![Ajouter un serveur d’autorisation][api-management-add-authorization-server-3]

<span data-ttu-id="6cb04-262">Immédiatement après les informations d’identification du client hello est un octroi de code d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="6cb04-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="6cb04-263">Copiez le code d’autorisation et tooyour arrière du commutateur application du portail Azure AD développeur page, ainsi coller d’octroi de hello hello **URL de réponse** champ, puis cliquez sur **enregistrer** à nouveau.</span><span class="sxs-lookup"><span data-stu-id="6cb04-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![URL de réponse][api-management-aad-reply-url]

<span data-ttu-id="6cb04-265">étape suivante de Hello est tooconfigure les autorisations de hello pour le portail des développeurs hello application AAD.</span><span class="sxs-lookup"><span data-stu-id="6cb04-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="6cb04-266">Cliquez sur **autorisations d’Application** et hello la case pour **lire les données d’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="6cb04-267">Cliquez sur **enregistrer** toosave cette modification, puis cliquez sur **ajouter application**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![Ajout d’autorisations][api-management-add-devportal-permissions]

<span data-ttu-id="6cb04-269">Cliquez sur icône de recherche hello, type **APIM** dans hello commençant par, sélectionnez **APIMAADDemo**, puis cliquez sur toosave de case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![Ajout d’autorisations][api-management-aad-add-app-permissions]

<span data-ttu-id="6cb04-271">Cliquez sur **autorisations déléguées** pour **APIMAADDemo** et hello la case pour **accès APIMAADDemo**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="6cb04-272">Ainsi, développeur de hello service principal d’application de portail tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![Ajout d’autorisations][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="6cb04-274">Activer l’autorisation de l’utilisateur OAuth 2.0 pour hello calculatrice API</span><span class="sxs-lookup"><span data-stu-id="6cb04-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="6cb04-275">Maintenant que hello serveur OAuth 2.0 est configuré, vous pouvez le spécifier dans les paramètres de sécurité hello pour votre API.</span><span class="sxs-lookup"><span data-stu-id="6cb04-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="6cb04-276">Cette étape est illustrée dans hello vidéo en commençant à 14:30.</span><span class="sxs-lookup"><span data-stu-id="6cb04-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="6cb04-277">Cliquez sur **API** dans hello du menu de gauche, puis cliquez sur **calculatrice** tooview et configurer ses paramètres.</span><span class="sxs-lookup"><span data-stu-id="6cb04-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![API de calcul][api-management-calc-api]

<span data-ttu-id="6cb04-279">Accédez toohello **sécurité** onglet, vérifiez hello **OAuth 2.0** case à cocher, le serveur de l’autorisation souhaitée de hello sélectionnez à partir de hello **serveur d’autorisation** liste déroulante, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![API de calcul][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="6cb04-281">Appeler à partir du portail des développeurs hello hello calculatrice API</span><span class="sxs-lookup"><span data-stu-id="6cb04-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="6cb04-282">Maintenant que l’autorisation de hello OAuth 2.0 est configurée sur hello API, ses opérations peuvent être appelées avec succès à partir du centre de développement hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="6cb04-283">Cette étape est illustrée dans hello vidéo en commençant à 15:00.</span><span class="sxs-lookup"><span data-stu-id="6cb04-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="6cb04-284">Accédez arrière toohello **ajouter deux entiers** opération du service de calculatrice hello dans le portail des développeurs hello et cliquez sur **essayez-la**.</span><span class="sxs-lookup"><span data-stu-id="6cb04-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="6cb04-285">Remarque hello nouvel élément Bonjour **autorisation** section serveur d’autorisation toohello correspondant vous venez d’ajouter.</span><span class="sxs-lookup"><span data-stu-id="6cb04-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![API de calcul][api-management-calc-authorization-server]

<span data-ttu-id="6cb04-287">Sélectionnez **code d’autorisation** à partir de l’autorisation hello déroulante liste, puis entrez les informations d’identification hello de hello compte toouse.</span><span class="sxs-lookup"><span data-stu-id="6cb04-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="6cb04-288">Si vous êtes déjà connecté avec hello compte, vous ne pouvez pas invité.</span><span class="sxs-lookup"><span data-stu-id="6cb04-288">If you are already signed in with hello account you may not be prompted.</span></span>

![API de calcul][api-management-devportal-authorization-code]

<span data-ttu-id="6cb04-290">Cliquez sur **envoyer** et Remarque Bonjour **état de la réponse** de **200 OK** et des résultats d’opération hello dans le contenu de la réponse hello hello.</span><span class="sxs-lookup"><span data-stu-id="6cb04-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![API de calcul][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="6cb04-292">Configurer un Bonjour de toocall API application de bureau</span><span class="sxs-lookup"><span data-stu-id="6cb04-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="6cb04-293">procédure suivante de Hello Bonjour vidéo démarre à 16 h 30 et configure un Bonjour de toocall API simple application de bureau.</span><span class="sxs-lookup"><span data-stu-id="6cb04-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="6cb04-294">première étape de Hello est l’application de bureau tooregister hello dans Azure AD et lui donner accès toohello directory et toohello principal du service.</span><span class="sxs-lookup"><span data-stu-id="6cb04-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="6cb04-295">À 18:25, il existe une démonstration d’application de bureau hello appel d’opération de calculatrice de hello API.</span><span class="sxs-lookup"><span data-stu-id="6cb04-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="6cb04-296">Configurer un toopre de stratégie de validation de jetons Web JSON-autoriser les demandes</span><span class="sxs-lookup"><span data-stu-id="6cb04-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="6cb04-297">commence à 20:48 Hello procédure finale dans la vidéo de hello et vous montre comment toouse hello [valider les jetons Web JSON](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) stratégie toopre-autoriser les demandes en validant les jetons d’accès hello de chaque demande entrante.</span><span class="sxs-lookup"><span data-stu-id="6cb04-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="6cb04-298">Si la demande de hello n’est pas validé par hello stratégie de valider les jetons Web JSON, demande de hello est bloquée par la gestion des API et n’est pas passé toohello principal.</span><span class="sxs-lookup"><span data-stu-id="6cb04-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="6cb04-299">Pour une autre démonstration de configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : fonctionnalités de gestion des API plus](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too13:50.</span><span class="sxs-lookup"><span data-stu-id="6cb04-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="6cb04-300">Avance rapide too15:00 les stratégies de hello toosee configurées dans l’éditeur de stratégie hello et puis too18:50 pour une démonstration de l’appel d’une opération à partir du portail des développeurs hello avec et sans hello requis jeton d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="6cb04-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cb04-301">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6cb04-301">Next steps</span></span>
* <span data-ttu-id="6cb04-302">Découvrez plus de [vidéos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) sur Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="6cb04-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="6cb04-303">Pour les autres façons toosecure votre service principal, consultez [authentification mutuelle des certificats](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="6cb04-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
