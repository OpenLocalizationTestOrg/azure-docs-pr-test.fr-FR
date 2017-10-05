---
title: "Utiliser Azure Active Directory pour l’authentification de solutions de gestion Batch | Microsoft Docs"
description: "Les applications créées avec Azure Resource Manager et le fournisseur de ressources Batch s’authentifient auprès d’Azure AD."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="05ed3-103">Authentification de solutions de gestion Batch avec Active Directory</span><span class="sxs-lookup"><span data-stu-id="05ed3-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="05ed3-104">Les applications qui appellent le service de gestion Azure Batch s’authentifient auprès d’[Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05ed3-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="05ed3-105">Azure AD est le service Microsoft de gestion des répertoires et des identités basé sur le cloud mutualisé.</span><span class="sxs-lookup"><span data-stu-id="05ed3-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="05ed3-106">Azure lui-même utilise Azure AD pour l’authentification de ses clients, de ses administrateurs de services fédérés et de ses utilisateurs professionnels.</span><span class="sxs-lookup"><span data-stu-id="05ed3-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="05ed3-107">La bibliothèque .NET de gestion Batch expose des types pour l’utilisation des packages d’application, des applications, des clés de compte et des comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="05ed3-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="05ed3-108">La bibliothèque .NET de gestion Batch est un client de fournisseur de ressources Azure, qui est utilisée avec [Azure Resource Manager][resman_overview] pour gérer ces ressources par programme.</span><span class="sxs-lookup"><span data-stu-id="05ed3-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="05ed3-109">Azure AD est requis pour authentifier les demandes effectuées par le biais des clients de fournisseur de ressources Azure, y compris la bibliothèque Batch Management .NET et d’[Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="05ed3-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="05ed3-110">Dans cet article, nous découvrons comment utiliser Azure AD pour l’authentification à partir des applications qui utilisent la bibliothèque .NET de gestion Batch.</span><span class="sxs-lookup"><span data-stu-id="05ed3-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="05ed3-111">Nous montrons comment utiliser Azure AD pour authentifier un administrateur ou un coadministrateur d’abonnement avec l’authentification intégrée.</span><span class="sxs-lookup"><span data-stu-id="05ed3-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="05ed3-112">Nous utilisons l’exemple de projet [AccountManagment][acct_mgmt_sample], disponible sur GitHub, pour parcourir la bibliothèque .NET de gestion Batch avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05ed3-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="05ed3-113">Pour en savoir plus sur l’utilisation de la bibliothèque .NET de gestion Batch et l’exemple AccountManagement, consultez [Gérer les quotas et comptes Batch avec la bibliothèque cliente Batch Management pour .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="05ed3-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="05ed3-114">Inscrire votre application auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="05ed3-114">Register your application with Azure AD</span></span>

<span data-ttu-id="05ed3-115">La [bibliothèque d’authentification Azure Active Directory][aad_adal] (ADAL) fournit une interface de programmation à Azure AD, que vous pouvez utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="05ed3-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="05ed3-116">Pour appeler ADAL à partir de votre application, vous devez inscrire votre application dans un locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05ed3-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="05ed3-117">Lorsque vous inscrivez votre application, vous fournissez des informations relatives à votre application à Azure AD, y compris un nom au sein du locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05ed3-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="05ed3-118">Azure AD fournit ensuite un ID d’application que vous utilisez pour associer votre application à Azure AD lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="05ed3-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="05ed3-119">Pour en savoir plus sur l’ID d’application, consultez [Objets application et principal du service dans Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="05ed3-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="05ed3-120">Suivez les étapes de la section [Ajout d’une application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) dans [Intégration d’applications dans Azure Active Directory][aad_integrate] pour inscrire l’exemple d’application AccountManagement.</span><span class="sxs-lookup"><span data-stu-id="05ed3-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="05ed3-121">Indiquez **Application cliente native** comme type d’application.</span><span class="sxs-lookup"><span data-stu-id="05ed3-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="05ed3-122">L’URI conforme au standard OAuth 2.0 de l’**URI de redirection** est `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="05ed3-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="05ed3-123">Pour `http://myaccountmanagementsample`l’URI de redirection**, vous pouvez toutefois spécifier n’importe quel URI valide (tel que** ), puisqu’il n’est pas nécessaire que ce soit un point de terminaison réel :</span><span class="sxs-lookup"><span data-stu-id="05ed3-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="05ed3-124">Lorsque vous avez terminé le processus d’inscription, l’ID d’application et l’ID d’objet (principal de service) sont répertoriés pour votre application.</span><span class="sxs-lookup"><span data-stu-id="05ed3-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="05ed3-125">Accorder l’accès à l’API Azure Resource Manager à votre application</span><span class="sxs-lookup"><span data-stu-id="05ed3-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="05ed3-126">Ensuite, vous devez déléguer l’accès à votre application à l’API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="05ed3-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="05ed3-127">L’identificateur Azure AD pour l’API Resource Manager est **API Gestion des services Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="05ed3-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="05ed3-128">Suivez les étapes ci-dessous dans le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="05ed3-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="05ed3-129">Dans le volet de navigation de gauche du portail Azure, choisissez **Plus de services**, cliquez sur **Inscriptions d’application**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="05ed3-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="05ed3-130">Recherchez le nom de votre application dans la liste des inscriptions d’application :</span><span class="sxs-lookup"><span data-stu-id="05ed3-130">Search for the name of your application in the list of app registrations:</span></span>

    ![Rechercher le nom de votre application](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="05ed3-132">Affichez le panneau **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="05ed3-132">Display the **Settings** blade.</span></span> <span data-ttu-id="05ed3-133">Dans la section **Accès API**, sélectionnez **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="05ed3-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="05ed3-134">Cliquez sur **Ajouter** pour ajouter une autorisation requise.</span><span class="sxs-lookup"><span data-stu-id="05ed3-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="05ed3-135">À l’étape 1, entrez **API Gestion des services Windows Azure**, sélectionnez cette API dans la liste des résultats, puis cliquez sur le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="05ed3-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="05ed3-136">À l’étape 2, activez la case à cocher en regard de **Access Azure classic deployment model as organization users** (Accéder au modèle de déploiement Azure Classic en tant qu’utilisateurs de l’organisation), puis cliquez sur le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="05ed3-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="05ed3-137">Cliquez sur le bouton **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="05ed3-137">Click the **Done** button.</span></span>

<span data-ttu-id="05ed3-138">Le panneau **Autorisations requises** indique à présent que les autorisations pour votre application sont accordées aux API Resource Manager et à ADAL.</span><span class="sxs-lookup"><span data-stu-id="05ed3-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="05ed3-139">Les autorisations sont accordées par défaut à ADAL lorsque vous commencez par inscrire votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05ed3-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Déléguer des autorisations à l’API Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="05ed3-141">Points de terminaison Azure AD</span><span class="sxs-lookup"><span data-stu-id="05ed3-141">Azure AD endpoints</span></span>

<span data-ttu-id="05ed3-142">Pour authentifier vos solutions de gestion Batch avec Azure AD, vous devez inclure 2 points de terminaison connus.</span><span class="sxs-lookup"><span data-stu-id="05ed3-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="05ed3-143">Le **point de terminaison commun Azure AD** fournit une interface de collecte d’informations d’identification générique lorsqu’un client spécifique n’est pas spécifié, comme dans le cas de l’authentification intégrée :</span><span class="sxs-lookup"><span data-stu-id="05ed3-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="05ed3-144">Le **point de terminaison Azure Resource Manager** permet d’obtenir un jeton d’authentification des demandes transmises au service de gestion Batch :</span><span class="sxs-lookup"><span data-stu-id="05ed3-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="05ed3-145">L’exemple d’application AccountManagement définit des constantes pour ces points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="05ed3-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="05ed3-146">Laissez ces constantes telles quelles :</span><span class="sxs-lookup"><span data-stu-id="05ed3-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="05ed3-147">Référencer votre ID d’application</span><span class="sxs-lookup"><span data-stu-id="05ed3-147">Reference your application ID</span></span> 

<span data-ttu-id="05ed3-148">Votre application cliente utilise l’ID d’application (également appelé l’ID client) pour accéder à Azure AD lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="05ed3-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="05ed3-149">Une fois que vous avez inscrit votre application dans le portail Azure, mettez à jour votre code pour utiliser l’ID d’application fourni par Azure AD pour votre application inscrite.</span><span class="sxs-lookup"><span data-stu-id="05ed3-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="05ed3-150">Dans l’exemple d’application AccountManagement, copiez votre ID d’application à partir du portail Azure vers la constante appropriée :</span><span class="sxs-lookup"><span data-stu-id="05ed3-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="05ed3-151">Copiez également l’URI de redirection que vous avez spécifiée pendant l’inscription.</span><span class="sxs-lookup"><span data-stu-id="05ed3-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="05ed3-152">L’URI de redirection spécifié dans votre code doit correspondre à l’URI de redirection que vous avez fourni lors de l’inscription de l’application.</span><span class="sxs-lookup"><span data-stu-id="05ed3-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="05ed3-153">Acquérir un jeton d’authentification Azure AD</span><span class="sxs-lookup"><span data-stu-id="05ed3-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="05ed3-154">Après avoir inscrit l’exemple AccountManagement auprès du locataire Azure AD et mis à jour le code source de l’exemple avec vos valeurs, l’exemple est prêt pour une authentification avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05ed3-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="05ed3-155">Lorsque vous exécutez l’exemple, ADAL tente d’acquérir un jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="05ed3-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="05ed3-156">À ce stade, vous êtes invité à renseigner vos informations d’identification Microsoft :</span><span class="sxs-lookup"><span data-stu-id="05ed3-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="05ed3-157">Après avoir fourni vos informations d’identification, l’exemple d’application peut continuer à émettre des demandes authentifiées au service de gestion Batch.</span><span class="sxs-lookup"><span data-stu-id="05ed3-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="05ed3-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="05ed3-158">Next steps</span></span>

<span data-ttu-id="05ed3-159">Pour en savoir plus sur l’exécution de [l’exemple d’application AccountManagement][acct_mgmt_sample], consultez [Gérer les quotas et comptes Batch avec la bibliothèque cliente Batch Management pour .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="05ed3-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="05ed3-160">Pour en savoir plus sur Azure AD, consultez la [documentation sur Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="05ed3-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="05ed3-161">Des exemples détaillés illustrant l’utilisation d’ADAL sont disponibles dans la bibliothèque [Exemples de code Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="05ed3-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="05ed3-162">Pour authentifier des applications de service Batch à l’aide d’Azure AD, consultez [Authentifier des solutions de service Batch auprès d’Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="05ed3-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="05ed3-163">[aad_about]: ../active-directory/active-directory-whatis.md "Qu’est-ce qu’Azure Active Directory ?"</span><span class="sxs-lookup"><span data-stu-id="05ed3-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="05ed3-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scénarios d’authentification pour Azure AD"</span><span class="sxs-lookup"><span data-stu-id="05ed3-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="05ed3-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Intégration d’applications dans Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="05ed3-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
