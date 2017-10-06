---
title: solutions de gestion par lots tooauthenticate aaaUse Azure Active Directory | Documents Microsoft
description: "Applications générées avec le Gestionnaire de ressources Azure et le fournisseur de ressources de traitement par lots hello s’authentifier auprès d’Azure AD."
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
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="9fff8-103">Authentification de solutions de gestion Batch avec Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fff8-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="9fff8-104">Les applications qui appellent le service de gestion de traitement par lots Azure hello s’authentifier avec [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9fff8-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="9fff8-105">Azure AD est le service Microsoft de gestion des répertoires et des identités basé sur le cloud mutualisé.</span><span class="sxs-lookup"><span data-stu-id="9fff8-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="9fff8-106">Azure lui-même utilise Azure AD pour l’authentification de hello de ses clients, les administrateurs de service et les utilisateurs professionnels.</span><span class="sxs-lookup"><span data-stu-id="9fff8-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="9fff8-107">bibliothèque de Batch Management .NET Hello expose les types pour l’utilisation des comptes Batch, des clés de compte, des applications et des packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="9fff8-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="9fff8-108">bibliothèque de Batch Management .NET Hello est un client de fournisseur de ressources Azure et est utilisée conjointement avec [Azure Resource Manager] [ resman_overview] toomanage ces ressources par programme.</span><span class="sxs-lookup"><span data-stu-id="9fff8-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="9fff8-109">Azure AD est tooauthenticate requis les demandes effectuées via n’importe quel client de fournisseur de ressources Azure, y compris hello Batch Management .NET bibliothèque et [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="9fff8-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="9fff8-110">Dans cet article, nous explorons à l’aide de tooauthenticate Azure AD à partir d’applications qui utilisent la bibliothèque de Batch Management .NET hello.</span><span class="sxs-lookup"><span data-stu-id="9fff8-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="9fff8-111">Nous montrons comment toouse Azure AD tooauthenticate un administrateur de l’abonnement ou un coadministrateur, à l’aide intégrée d’authentification.</span><span class="sxs-lookup"><span data-stu-id="9fff8-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="9fff8-112">Nous utilisons hello [AccountManagment] [ acct_mgmt_sample] exemple de projet, disponible sur GitHub, toowalk via l’utilisation d’Azure AD avec la bibliothèque de Batch Management .NET hello.</span><span class="sxs-lookup"><span data-stu-id="9fff8-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="9fff8-113">toolearn savoir plus sur à l’aide de la bibliothèque de Batch Management .NET hello et hello AccountManagement exemple, consultez [comptes Batch de gérer et quotas avec la bibliothèque cliente de gestion par lots hello pour .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9fff8-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="9fff8-114">Inscrire votre application auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fff8-114">Register your application with Azure AD</span></span>

<span data-ttu-id="9fff8-115">Bonjour Azure [bibliothèque d’authentification Active Directory] [ aad_adal] (ADAL) fournit une interface de programmation de tooAzure AD pour les utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="9fff8-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="9fff8-116">toocall ADAL à partir de votre application, vous devez inscrire votre application dans un locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fff8-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="9fff8-117">Lorsque vous inscrivez votre application, vous fournissez Azure AD avec des informations relatives à votre application, y compris son nom dans le locataire Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="9fff8-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="9fff8-118">Azure AD puis fournit un ID d’application que vous utilisez tooassociate votre application auprès d’Azure AD lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="9fff8-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="9fff8-119">toolearn savoir plus sur les ID d’application hello, consultez [Application et les objets principal du service dans Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="9fff8-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="9fff8-120">tooregister hello AccountManagement exemple d’application, suivez les étapes de hello Bonjour [Ajout d’une Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section [intégration d’applications avec Azure Active Directory] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="9fff8-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="9fff8-121">Spécifiez **Application cliente Native** de type hello d’application.</span><span class="sxs-lookup"><span data-stu-id="9fff8-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="9fff8-122">Hello industry standard URI OAuth 2.0 hello **URI de redirection** est `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="9fff8-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="9fff8-123">Toutefois, vous pouvez spécifier n’importe quel URI valide (tel que `http://myaccountmanagementsample`) pour hello **URI de redirection**, comme il n’a pas besoin de toobe un point de terminaison réel :</span><span class="sxs-lookup"><span data-stu-id="9fff8-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="9fff8-124">Après avoir terminé le processus d’inscription de hello, vous voyez les ID de l’application hello et hello ID d’objet (principal du service) répertorié pour votre application.</span><span class="sxs-lookup"><span data-stu-id="9fff8-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="9fff8-125">Accorder hello API Azure Resource Manager accès tooyour application</span><span class="sxs-lookup"><span data-stu-id="9fff8-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="9fff8-126">Ensuite, vous devez tooyour d’accès toodelegate toohello application API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9fff8-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="9fff8-127">Identificateur Hello Azure AD pour hello API du Gestionnaire de ressources est **API de gestion Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="9fff8-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="9fff8-128">Suivez ces étapes dans hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="9fff8-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="9fff8-129">Dans le volet de navigation gauche hello Hello portail Azure, choisissez **plus Services**, cliquez sur **inscriptions d’application**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9fff8-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="9fff8-130">Recherchez le nom hello de votre application dans la liste de hello d’inscriptions d’application :</span><span class="sxs-lookup"><span data-stu-id="9fff8-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Rechercher le nom de votre application](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="9fff8-132">Hello d’affichage **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="9fff8-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="9fff8-133">Bonjour **l’accès aux API** section, sélectionnez **autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="9fff8-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="9fff8-134">Cliquez sur **ajouter** tooadd une nouvelle autorisation requise.</span><span class="sxs-lookup"><span data-stu-id="9fff8-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="9fff8-135">Dans l’étape 1, entrez **API de gestion Windows Azure**, sélectionnez cette API à partir de la liste de hello des résultats, cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="9fff8-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="9fff8-136">À l’étape 2, sélectionnez hello case ensuite trop**modèle de déploiement classique d’accès Azure en tant qu’utilisateurs de l’organisation**, puis cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="9fff8-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="9fff8-137">Cliquez sur hello **fait** bouton.</span><span class="sxs-lookup"><span data-stu-id="9fff8-137">Click hello **Done** button.</span></span>

<span data-ttu-id="9fff8-138">Hello **autorisations requises** panneau maintenant montre que les applications de tooyour autorisations sont accordées tooboth hello ADAL et l’API du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="9fff8-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="9fff8-139">Les autorisations sont accordées tooADAL par défaut lorsque vous enregistrez tout d’abord votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fff8-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![Déléguer des autorisations toohello API Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="9fff8-141">Points de terminaison Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fff8-141">Azure AD endpoints</span></span>

<span data-ttu-id="9fff8-142">tooauthenticate vos solutions de gestion par lots avec Azure AD, vous aurez besoin de deux points de terminaison connus.</span><span class="sxs-lookup"><span data-stu-id="9fff8-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="9fff8-143">Hello **point de terminaison Azure AD commun** fournit des informations d’identification génériques collecte interface lorsqu’un client spécifique n’est pas fourni, comme dans les cas de hello de l’authentification intégrée :</span><span class="sxs-lookup"><span data-stu-id="9fff8-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="9fff8-144">Hello **point de terminaison Azure Resource Manager** est tooacquire utilisé un jeton d’authentification de service de gestion des demandes toohello Batch :</span><span class="sxs-lookup"><span data-stu-id="9fff8-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="9fff8-145">Hello AccountManagement, exemple d’application définit des constantes pour ces points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="9fff8-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="9fff8-146">Laissez ces constantes telles quelles :</span><span class="sxs-lookup"><span data-stu-id="9fff8-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="9fff8-147">Référencer votre ID d’application</span><span class="sxs-lookup"><span data-stu-id="9fff8-147">Reference your application ID</span></span> 

<span data-ttu-id="9fff8-148">Votre application cliente utilise tooaccess de ID (également désignée tooas hello client ID) d’application hello Azure AD lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="9fff8-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="9fff8-149">Une fois que vous avez enregistré votre application Bonjour portail Azure, mettre à jour votre code toouse hello ID de l’application d’Azure AD pour votre application inscrite.</span><span class="sxs-lookup"><span data-stu-id="9fff8-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="9fff8-150">Bonjour AccountManagement, exemple d’application, copiez votre ID d’application à partir de la constante appropriée de hello toohello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="9fff8-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="9fff8-151">Copiez également l’URI que vous avez spécifié au cours du processus d’inscription de hello de redirection hello.</span><span class="sxs-lookup"><span data-stu-id="9fff8-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="9fff8-152">redirection Hello QU'URI spécifié dans votre code doit correspondre à l’URI que vous avez fourni lorsque vous avez inscrit l’application hello de redirection hello.</span><span class="sxs-lookup"><span data-stu-id="9fff8-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="9fff8-153">Acquérir un jeton d’authentification Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fff8-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="9fff8-154">Une fois que vous inscrivez hello AccountManagement exemple dans le locataire Azure AD de hello et mettre à jour les exemples de code source hello avec vos valeurs, exemple hello est tooauthenticate prêt à l’aide d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fff8-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="9fff8-155">Lorsque vous exécutez exemple hello, hello ADAL tentatives tooacquire un jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="9fff8-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="9fff8-156">À ce stade, vous êtes invité à renseigner vos informations d’identification Microsoft :</span><span class="sxs-lookup"><span data-stu-id="9fff8-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="9fff8-157">Après avoir fourni vos informations d’identification, exemple d’application hello peut continuer tooissue authentifié demandes toohello service de gestion de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="9fff8-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9fff8-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fff8-158">Next steps</span></span>

<span data-ttu-id="9fff8-159">Pour plus d’informations sur l’exécution de hello [AccountManagement, exemple d’application][acct_mgmt_sample], consultez [comptes Batch de gérer et quotas avec la bibliothèque cliente de gestion par lots hello pour .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9fff8-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="9fff8-160">toolearn en savoir plus sur Azure AD, consultez hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="9fff8-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="9fff8-161">Approfondie exemples montrant comment toouse ADAL sont disponibles dans hello [exemples de Code Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="9fff8-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="9fff8-162">applications de service de traitement par lots tooauthenticate à l’aide d’Azure AD, consultez [solutions de service de traitement par lots de s’authentifier auprès d’Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="9fff8-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "Qu’est-ce qu’Azure Active Directory ?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scénarios d’authentification pour Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Intégration d’applications dans Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
