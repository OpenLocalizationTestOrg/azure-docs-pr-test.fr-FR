---
title: solutions de service Azure Batch aaaUse Azure Active Directory tooauthenticate | Documents Microsoft
description: "Traitement par lots prend en charge Azure AD pour l’authentification à partir de hello service Batch."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="28647-103">Authentification de solutions de service Batch avec Active Directory</span><span class="sxs-lookup"><span data-stu-id="28647-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="28647-104">Azure Batch prend en charge l’authentification avec [Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28647-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="28647-105">Azure AD est le service Microsoft de gestion des répertoires et des identités basé sur le cloud mutualisé.</span><span class="sxs-lookup"><span data-stu-id="28647-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="28647-106">Azure lui-même utilise Azure AD tooauthenticate ses clients, les administrateurs de service et les utilisateurs professionnels.</span><span class="sxs-lookup"><span data-stu-id="28647-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="28647-107">Lorsque vous utilisez l’authentification Azure AD avec Azure Batch, vous pouvez vous authentifier de deux manières :</span><span class="sxs-lookup"><span data-stu-id="28647-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="28647-108">À l’aide de **l’authentification intégrée** tooauthenticate un utilisateur interagit avec l’application hello.</span><span class="sxs-lookup"><span data-stu-id="28647-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="28647-109">Une application à l’aide de l’authentification intégrée de collecte des informations d’identification d’un utilisateur et utilise ces informations d’identification tooauthenticate accéder tooBatch à des ressources.</span><span class="sxs-lookup"><span data-stu-id="28647-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="28647-110">En utilisant un **principal du service** tooauthenticate une application sans assistance.</span><span class="sxs-lookup"><span data-stu-id="28647-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="28647-111">Un principal de service définit les stratégie hello et les autorisations pour une application dans l’application de commande toorepresent hello lors de l’accès aux ressources lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="28647-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="28647-112">toolearn en savoir plus sur Azure AD, consultez hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="28647-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="28647-113">Authentification et mode d’allocation de pool</span><span class="sxs-lookup"><span data-stu-id="28647-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="28647-114">Lorsque vous créez un compte Batch, vous pouvez spécifier où les pools créés pour ce compte doivent être alloués.</span><span class="sxs-lookup"><span data-stu-id="28647-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="28647-115">Vous pouvez choisir les pools de tooallocate dans l’abonnement au service de traitement par lots hello par défaut ou dans un abonnement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="28647-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="28647-116">Votre choix affecte la façon dont vous authentifier tooresources d’accès de ce compte.</span><span class="sxs-lookup"><span data-stu-id="28647-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="28647-117">**Abonnement au service Batch**.</span><span class="sxs-lookup"><span data-stu-id="28647-117">**Batch service subscription**.</span></span> <span data-ttu-id="28647-118">Par défaut, les pools Batch sont alloués dans un abonnement au service Batch.</span><span class="sxs-lookup"><span data-stu-id="28647-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="28647-119">Si vous choisissez cette option, vous pouvez vous authentifier tooresources d’accès de ce compte à l’aide [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) ou auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28647-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="28647-120">**Abonnement utilisateur.**</span><span class="sxs-lookup"><span data-stu-id="28647-120">**User subscription.**</span></span> <span data-ttu-id="28647-121">Vous pouvez choisir des pools de lot tooallocate dans un abonnement de l’utilisateur que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="28647-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="28647-122">Si vous choisissez cette option, vous devez vous authentifier auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28647-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="28647-123">Points de terminaison pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="28647-123">Endpoints for authentication</span></span>

<span data-ttu-id="28647-124">applications de traitement par lots tooauthenticate avec Azure AD, vous devez tooinclude certains points de terminaison connus dans votre code.</span><span class="sxs-lookup"><span data-stu-id="28647-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="28647-125">Point de terminaison Azure AD</span><span class="sxs-lookup"><span data-stu-id="28647-125">Azure AD endpoint</span></span>

<span data-ttu-id="28647-126">Hello base point de terminaison autorité Azure AD est :</span><span class="sxs-lookup"><span data-stu-id="28647-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="28647-127">tooauthenticate avec Azure AD, vous utilisez ce point de terminaison avec l’ID de client hello (ID de répertoire).</span><span class="sxs-lookup"><span data-stu-id="28647-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="28647-128">ID de client Hello identifie hello toouse de locataire Azure AD pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="28647-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="28647-129">tooretrieve hello ID client, suivez les étapes de hello décrites dans [obtenir l’ID hello pour Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="28647-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="28647-130">point de terminaison spécifiques du client Hello est requis lorsque vous authentifiez à l’aide d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="28647-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="28647-131">point de terminaison spécifiques du client Hello est facultatif lorsque vous authentifiez à l’aide de l’authentification intégrée, mais recommandé.</span><span class="sxs-lookup"><span data-stu-id="28647-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="28647-132">Toutefois, vous pouvez également utiliser point de terminaison commun hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28647-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="28647-133">point de terminaison commun Hello fournit des informations d’identification génériques collecte interface lorsqu’un client spécifique n’est fourni.</span><span class="sxs-lookup"><span data-stu-id="28647-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="28647-134">point de terminaison commun Hello est `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="28647-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="28647-135">Pour plus d’informations sur les points de terminaison Azure AD, consultez [Scénarios d’authentification pour Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="28647-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="28647-136">Point de terminaison de ressource Batch</span><span class="sxs-lookup"><span data-stu-id="28647-136">Batch resource endpoint</span></span>

<span data-ttu-id="28647-137">Hello d’utilisation **point de terminaison de ressources Azure Batch** tooacquire un jeton d’authentification des demandes de service de traitement par lots toohello :</span><span class="sxs-lookup"><span data-stu-id="28647-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="28647-138">Inscrire votre application avec un client</span><span class="sxs-lookup"><span data-stu-id="28647-138">Register your application with a tenant</span></span>

<span data-ttu-id="28647-139">Hello première étape à l’aide d’Azure AD tooauthenticate consiste à inscrire votre application dans un locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28647-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="28647-140">Enregistrement de votre application vous permet de toocall hello Azure [bibliothèque d’authentification Active Directory] [ aad_adal] (ADAL) à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="28647-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="28647-141">Hello ADAL fournit une API pour l’authentification auprès d’Azure AD à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="28647-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="28647-142">Enregistrement de votre application est obligatoire si vous envisagez de l’authentification intégrée de toouse ou un principal de service.</span><span class="sxs-lookup"><span data-stu-id="28647-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="28647-143">Lorsque vous inscrivez votre application, vous fournissez des informations concernant votre tooAzure application AD.</span><span class="sxs-lookup"><span data-stu-id="28647-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="28647-144">Azure AD puis fournit un ID d’application que vous utilisez tooassociate votre application auprès d’Azure AD lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="28647-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="28647-145">toolearn savoir plus sur les ID d’application hello, consultez [Application et les objets principal du service dans Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="28647-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="28647-146">tooregister votre application de traitement par lots, suivez les étapes hello Bonjour [Ajout d’une Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section [intégration d’applications avec Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="28647-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="28647-147">Si vous inscrivez votre application comme une Application Native, vous pouvez spécifier n’importe quel URI valide pour hello **URI de redirection**.</span><span class="sxs-lookup"><span data-stu-id="28647-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="28647-148">Il n’a pas besoin toobe un point de terminaison réel.</span><span class="sxs-lookup"><span data-stu-id="28647-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="28647-149">Une fois que vous avez enregistré votre application, vous verrez l’ID de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="28647-149">After you've registered your application, you'll see hello application ID:</span></span>

![Inscrire votre application Batch auprès d’Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="28647-151">Pour plus d’informations sur l’inscription d’une application avec Azure AD, consultez [Scénarios d’authentification pour Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="28647-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="28647-152">Obtenir l’ID hello pour votre annuaire Active Directory</span><span class="sxs-lookup"><span data-stu-id="28647-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="28647-153">ID de client Hello identifie le locataire Azure AD hello qui fournit l’application tooyour de services d’authentification.</span><span class="sxs-lookup"><span data-stu-id="28647-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="28647-154">tooget hello ID client, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="28647-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="28647-155">Bonjour portail Azure, sélectionnez votre annuaire Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28647-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="28647-156">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="28647-156">Click **Properties**.</span></span>
3. <span data-ttu-id="28647-157">Copier la valeur GUID hello fourni pour l’ID de répertoire hello.</span><span class="sxs-lookup"><span data-stu-id="28647-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="28647-158">Cette valeur est également appelée ID de client hello.</span><span class="sxs-lookup"><span data-stu-id="28647-158">This value is also called hello tenant ID.</span></span>

![Copiez l’ID de répertoire hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="28647-160">Utiliser l’authentification intégrée</span><span class="sxs-lookup"><span data-stu-id="28647-160">Use integrated authentication</span></span>

<span data-ttu-id="28647-161">tooauthenticate avec une authentification intégrée, vous devez toogrant votre toohello de tooconnect autorisations application API de service de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="28647-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="28647-162">Cette étape permet à votre application tooauthenticate appelle toohello lot service API avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28647-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="28647-163">Une fois que vous avez [inscrit votre application](#register-your-application-with-an-azure-ad-tenant), suivez ces étapes dans hello Azure toogrant portail il accéder au service de traitement par lots toohello :</span><span class="sxs-lookup"><span data-stu-id="28647-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="28647-164">Dans le volet de navigation gauche hello Hello portail Azure, choisissez **plus Services**, cliquez sur **inscriptions d’application**.</span><span class="sxs-lookup"><span data-stu-id="28647-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="28647-165">Recherchez le nom hello de votre application dans la liste de hello d’inscriptions d’application :</span><span class="sxs-lookup"><span data-stu-id="28647-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Rechercher le nom de votre application](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="28647-167">Ouvrez hello **paramètres** panneau pour votre application.</span><span class="sxs-lookup"><span data-stu-id="28647-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="28647-168">Bonjour **l’accès aux API** section, sélectionnez **autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="28647-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="28647-169">Bonjour **autorisations requises** panneau, cliquez sur hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="28647-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="28647-170">À l’étape 1, recherchez hello API de lot.</span><span class="sxs-lookup"><span data-stu-id="28647-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="28647-171">Recherche de chacune de ces chaînes jusqu'à ce que vous trouviez hello API :</span><span class="sxs-lookup"><span data-stu-id="28647-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="28647-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="28647-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="28647-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="28647-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="28647-174">Les locataires Azure AD les plus récents peuvent utiliser ce nom.</span><span class="sxs-lookup"><span data-stu-id="28647-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="28647-175">**ddbf3205-c6bd-46AE-8127-60eb93363864** ID de hello pour hello API de lot.</span><span class="sxs-lookup"><span data-stu-id="28647-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="28647-176">Une fois que vous trouvez hello API de lot, sélectionnez-la, puis cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="28647-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="28647-177">À l’étape 2, sélectionnez hello case ensuite trop**Service de traitement par lots Azure accès** et cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="28647-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="28647-178">Cliquez sur hello **fait** bouton.</span><span class="sxs-lookup"><span data-stu-id="28647-178">Click hello **Done** button.</span></span>

<span data-ttu-id="28647-179">Hello **autorisations requises** panneau maintenant indique que votre application Azure AD a accès tooboth ADAL et hello API de service de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="28647-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="28647-180">Les autorisations sont accordées automatiquement tooADAL lorsque vous enregistrez tout d’abord votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28647-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![Accorder des autorisations d’API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="28647-182">Utiliser un principal de service</span><span class="sxs-lookup"><span data-stu-id="28647-182">Use a service principal</span></span> 

<span data-ttu-id="28647-183">tooauthenticate une application qui s’exécute sans assistance, vous utilisez un principal de service.</span><span class="sxs-lookup"><span data-stu-id="28647-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="28647-184">Une fois que vous avez enregistré votre application, procédez comme suit dans hello tooconfigure portail Azure principal d’un service :</span><span class="sxs-lookup"><span data-stu-id="28647-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="28647-185">Demandez une clé secrète pour votre application.</span><span class="sxs-lookup"><span data-stu-id="28647-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="28647-186">Affecter une application de tooyour rôle RBAC.</span><span class="sxs-lookup"><span data-stu-id="28647-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="28647-187">Demander une clé secrète pour votre application</span><span class="sxs-lookup"><span data-stu-id="28647-187">Request a secret key for your application</span></span>

<span data-ttu-id="28647-188">Lorsque votre application s’authentifie avec un principal de service, il envoie l’ID de l’application hello et un tooAzure clé secrète AD.</span><span class="sxs-lookup"><span data-stu-id="28647-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="28647-189">Vous devez toocreate et copiez hello toouse de clé secrète à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="28647-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="28647-190">Suivez ces étapes dans hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="28647-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="28647-191">Dans le volet de navigation gauche hello Hello portail Azure, choisissez **plus Services**, cliquez sur **inscriptions d’application**.</span><span class="sxs-lookup"><span data-stu-id="28647-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="28647-192">Recherchez le nom hello de votre application dans la liste de hello d’inscriptions de l’application.</span><span class="sxs-lookup"><span data-stu-id="28647-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="28647-193">Hello d’affichage **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="28647-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="28647-194">Bonjour **l’accès aux API** section, sélectionnez **clés**.</span><span class="sxs-lookup"><span data-stu-id="28647-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="28647-195">toocreate une clé, entrez une description pour la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="28647-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="28647-196">Sélectionnez ensuite une durée de clé hello d’un ou deux ans.</span><span class="sxs-lookup"><span data-stu-id="28647-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="28647-197">Cliquez sur hello **enregistrer** bouton toocreate et afficher la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="28647-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="28647-198">Copier hello valeur de clé tooa lieu sûr, car vous ne serez pas en mesure de tooaccess à nouveau après que vous laissez le panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="28647-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![Créer une clé secrète](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="28647-200">Affecter une application de tooyour rôle RBAC</span><span class="sxs-lookup"><span data-stu-id="28647-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="28647-201">tooauthenticate avec un principal de service, vous devez tooassign une application de tooyour rôle RBAC.</span><span class="sxs-lookup"><span data-stu-id="28647-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="28647-202">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="28647-202">Follow these steps:</span></span>

1. <span data-ttu-id="28647-203">Bonjour portail Azure, accédez à toohello du compte Batch utilisé par votre application.</span><span class="sxs-lookup"><span data-stu-id="28647-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="28647-204">Bonjour **paramètres** panneau pour le compte Batch hello, sélectionnez **contrôle d’accès (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="28647-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="28647-205">Cliquez sur hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="28647-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="28647-206">À partir de hello **rôle** liste déroulante, choisissez soit hello _collaborateur_ ou _lecteur_ rôle pour votre application.</span><span class="sxs-lookup"><span data-stu-id="28647-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="28647-207">Pour plus d’informations sur ces rôles, consultez [prise en main le contrôle d’accès en fonction du rôle Bonjour Azure portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="28647-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="28647-208">Bonjour **sélectionnez** , entrez le nom hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="28647-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="28647-209">Sélectionnez votre application à partir de la liste de hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="28647-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="28647-210">Votre application doit maintenant apparaître dans vos paramètres de contrôle d’accès avec un rôle RBAC qui lui est attribué.</span><span class="sxs-lookup"><span data-stu-id="28647-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Affecter une application de tooyour rôle RBAC](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="28647-212">Obtenir l’ID hello pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28647-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="28647-213">ID de client Hello identifie le locataire Azure AD hello qui fournit l’application tooyour de services d’authentification.</span><span class="sxs-lookup"><span data-stu-id="28647-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="28647-214">tooget hello ID client, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="28647-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="28647-215">Bonjour portail Azure, sélectionnez votre annuaire Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28647-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="28647-216">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="28647-216">Click **Properties**.</span></span>
3. <span data-ttu-id="28647-217">Copier la valeur GUID hello fourni pour l’ID de répertoire hello.</span><span class="sxs-lookup"><span data-stu-id="28647-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="28647-218">Cette valeur est également appelée ID de client hello.</span><span class="sxs-lookup"><span data-stu-id="28647-218">This value is also called hello tenant ID.</span></span>

![Copiez l’ID de répertoire hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="28647-220">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="28647-220">Code examples</span></span>

<span data-ttu-id="28647-221">les exemples de code Hello dans cette section montrent comment tooauthenticate avec Azure AD à l’aide de l’authentification intégrée et avec un principal de service.</span><span class="sxs-lookup"><span data-stu-id="28647-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="28647-222">Ces exemples de code utilisent .NET, mais les concepts de hello sont similaires pour d’autres langues.</span><span class="sxs-lookup"><span data-stu-id="28647-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="28647-223">Un jeton d’authentification Azure AD expire au bout d’une heure.</span><span class="sxs-lookup"><span data-stu-id="28647-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="28647-224">Lorsque vous utilisez une durée de vie longue **BatchClient** de l’objet, nous vous recommandons de récupération d’un jeton à partir de la bibliothèque ADAL sur tooensure de chaque demande, vous devez toujours un jeton valide.</span><span class="sxs-lookup"><span data-stu-id="28647-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="28647-225">tooachieve dans .NET, écrivez une méthode qui Récupère hello jeton d’Azure AD et qu’il passe ce tooa méthode **BatchTokenCredentials** objet en tant que délégué.</span><span class="sxs-lookup"><span data-stu-id="28647-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="28647-226">méthode de délégué Hello est appelée sur chaque tooensure service Batch toohello demande un jeton valide fourni.</span><span class="sxs-lookup"><span data-stu-id="28647-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="28647-227">Par défaut, ADAL met en cache des jetons pour qu’un nouveau jeton soit récupéré à partir d’Azure AD uniquement lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="28647-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="28647-228">Pour plus d’informations sur les jetons dans Azure AD, consultez [Scénarios d’authentification pour Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="28647-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="28647-229">Exemple de code : utilisation de l’authentification intégrée Azure AD avec Batch .NET</span><span class="sxs-lookup"><span data-stu-id="28647-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="28647-230">tooauthenticate avec l’authentification intégrée à partir de lot .NET, hello de référence [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package et hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span><span class="sxs-lookup"><span data-stu-id="28647-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="28647-231">Suivants de hello `using` instructions dans votre code :</span><span class="sxs-lookup"><span data-stu-id="28647-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="28647-232">ID de client hello de référence point de terminaison Azure AD dans votre code, y compris hello</span><span class="sxs-lookup"><span data-stu-id="28647-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="28647-233">tooretrieve hello ID client, suivez les étapes de hello décrites dans [obtenir l’ID hello pour Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="28647-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="28647-234">Référence de point de terminaison de la ressource de service de hello lot :</span><span class="sxs-lookup"><span data-stu-id="28647-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="28647-235">Référencez votre compte Batch :</span><span class="sxs-lookup"><span data-stu-id="28647-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="28647-236">Spécifiez l’ID d’application hello (ID client) pour votre application.</span><span class="sxs-lookup"><span data-stu-id="28647-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="28647-237">ID de l’application Hello est disponible à partir de votre inscription d’une application Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="28647-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="28647-238">Copiez également l’URI que vous avez spécifié au cours du processus d’inscription de hello de redirection hello.</span><span class="sxs-lookup"><span data-stu-id="28647-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="28647-239">redirection Hello QU'URI spécifié dans votre code doit correspondre à l’URI que vous avez fourni lorsque vous avez inscrit l’application hello de redirection hello :</span><span class="sxs-lookup"><span data-stu-id="28647-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="28647-240">Écrire un jeton d’authentification rappel méthode tooacquire hello d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28647-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="28647-241">Hello **GetAuthenticationTokenAsync** appels de méthode de rappel indiqué ici tooauthenticate ADAL un utilisateur qui interagit avec l’application hello.</span><span class="sxs-lookup"><span data-stu-id="28647-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="28647-242">Hello **AcquireTokenAsync** méthode fournie par la bibliothèque ADAL invites hello leurs informations d’identification utilisateur et application hello passe une fois les utilisateurs hello fournit les (sauf si elle a déjà mis en cache les informations d’identification) :</span><span class="sxs-lookup"><span data-stu-id="28647-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="28647-243">Construire un **BatchTokenCredentials** objet qui prend le délégué hello en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="28647-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="28647-244">Utilisez ces informations d’identification tooopen un **BatchClient** objet.</span><span class="sxs-lookup"><span data-stu-id="28647-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="28647-245">Vous pouvez l’utiliser **BatchClient** objet pour les opérations suivantes sur hello service Batch :</span><span class="sxs-lookup"><span data-stu-id="28647-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="28647-246">Exemple de code : utilisation d’un principal de service Azure AD avec Batch .NET</span><span class="sxs-lookup"><span data-stu-id="28647-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="28647-247">tooauthenticate avec un principal de service à partir de lot .NET, hello de référence [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package et hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span><span class="sxs-lookup"><span data-stu-id="28647-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="28647-248">Suivants de hello `using` instructions dans votre code :</span><span class="sxs-lookup"><span data-stu-id="28647-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="28647-249">ID de client hello de référence point de terminaison Azure AD dans votre code, y compris hello</span><span class="sxs-lookup"><span data-stu-id="28647-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="28647-250">Lorsque vous utilisez un principal de service, vous devez indiquer un point de terminaison spécifique du client.</span><span class="sxs-lookup"><span data-stu-id="28647-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="28647-251">tooretrieve hello ID client, suivez les étapes de hello décrites dans [obtenir l’ID hello pour Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="28647-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="28647-252">Référence de point de terminaison de la ressource de service de hello lot :</span><span class="sxs-lookup"><span data-stu-id="28647-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="28647-253">Référencez votre compte Batch :</span><span class="sxs-lookup"><span data-stu-id="28647-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="28647-254">Spécifiez l’ID d’application hello (ID client) pour votre application.</span><span class="sxs-lookup"><span data-stu-id="28647-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="28647-255">ID de l’application Hello est disponible à partir de votre inscription d’une application Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="28647-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="28647-256">Spécifiez la clé secrète hello que vous avez copié à partir de hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="28647-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="28647-257">Écrire un jeton d’authentification rappel méthode tooacquire hello d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28647-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="28647-258">Hello **GetAuthenticationTokenAsync** méthode de rappel ci-après appelle la bibliothèque ADAL pour l’authentification en mode sans assistance :</span><span class="sxs-lookup"><span data-stu-id="28647-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="28647-259">Construire un **BatchTokenCredentials** objet qui prend le délégué hello en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="28647-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="28647-260">Utilisez ces informations d’identification tooopen un **BatchClient** objet.</span><span class="sxs-lookup"><span data-stu-id="28647-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="28647-261">Vous pouvez ensuite utiliser qui **BatchClient** objet pour les opérations suivantes sur hello service Batch :</span><span class="sxs-lookup"><span data-stu-id="28647-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="28647-262">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28647-262">Next steps</span></span>

<span data-ttu-id="28647-263">toolearn en savoir plus sur Azure AD, consultez hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="28647-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="28647-264">Approfondie exemples montrant comment toouse ADAL sont disponibles dans hello [exemples de Code Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="28647-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="28647-265">toolearn savoir plus sur les principaux de service, consultez [Application et les objets principal du service dans Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="28647-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="28647-266">un principal de service à l’aide de toocreate hello Azure portail, consultez [utiliser une application de portail toocreate Active Directory et de principal du service qui peut accéder aux ressources](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="28647-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="28647-267">Vous pouvez également créer un principal de service avec PowerShell ou Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="28647-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="28647-268">les applications de gestion par lots tooauthenticate à l’aide d’Azure AD, consultez [des solutions de gestion de traitement par lots s’authentifier avec Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="28647-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "Qu’est-ce qu’Azure Active Directory ?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scénarios d’authentification pour Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Intégration d’applications dans Azure Active Directory"
[azure_portal]: http://portal.azure.com
