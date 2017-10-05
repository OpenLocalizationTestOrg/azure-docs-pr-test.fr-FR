---
title: "Utiliser Azure Active Directory pour l’authentification de solutions de service Azure Batch | Microsoft Docs"
description: "Batch prend en charge Azure AD pour l’authentification auprès du service Batch."
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
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="64ba9-103">Authentification de solutions de service Batch avec Active Directory</span><span class="sxs-lookup"><span data-stu-id="64ba9-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="64ba9-104">Azure Batch prend en charge l’authentification avec [Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64ba9-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="64ba9-105">Azure AD est le service Microsoft de gestion des répertoires et des identités basé sur le cloud mutualisé.</span><span class="sxs-lookup"><span data-stu-id="64ba9-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="64ba9-106">Azure lui-même utilise Azure AD pour authentifier ses clients, ses administrateurs de services fédérés et ses utilisateurs professionnels.</span><span class="sxs-lookup"><span data-stu-id="64ba9-106">Azure itself uses Azure AD to authenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="64ba9-107">Lorsque vous utilisez l’authentification Azure AD avec Azure Batch, vous pouvez vous authentifier de deux manières :</span><span class="sxs-lookup"><span data-stu-id="64ba9-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="64ba9-108">À l’aide de l’**authentification intégrée** pour authentifier un utilisateur qui interagit avec l’application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-108">By using **integrated authentication** to authenticate a user that is interacting with the application.</span></span> <span data-ttu-id="64ba9-109">Une application utilisant l’authentification intégrée collecte les informations d’identification d’un utilisateur et les utilise pour authentifier l’accès aux ressources Batch.</span><span class="sxs-lookup"><span data-stu-id="64ba9-109">An application using integrated authentication gathers a user's credentials and uses those credentials to authenticate access to Batch resources.</span></span>
- <span data-ttu-id="64ba9-110">À l’aide d’un **principal de service** pour authentifier une application sans assistance.</span><span class="sxs-lookup"><span data-stu-id="64ba9-110">By using a **service principal** to authenticate an unattended application.</span></span> <span data-ttu-id="64ba9-111">Un principal de service définit la stratégie et les autorisations pour une application afin de représenter l’application lors de l’accès aux ressources au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="64ba9-111">A service principal defines the policy and permissions for an application in order to represent the application when accessing resources at runtime.</span></span>

<span data-ttu-id="64ba9-112">Pour en savoir plus sur Azure AD, consultez la [documentation sur Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="64ba9-112">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="64ba9-113">Authentification et mode d’allocation de pool</span><span class="sxs-lookup"><span data-stu-id="64ba9-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="64ba9-114">Lorsque vous créez un compte Batch, vous pouvez spécifier où les pools créés pour ce compte doivent être alloués.</span><span class="sxs-lookup"><span data-stu-id="64ba9-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="64ba9-115">Vous pouvez choisir d’allouer des pools dans l’abonnement au service Batch par défaut ou dans un abonnement utilisateur.</span><span class="sxs-lookup"><span data-stu-id="64ba9-115">You can choose to allocate pools either in the default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="64ba9-116">Votre choix affecte la façon d’authentifier l’accès aux ressources de ce compte.</span><span class="sxs-lookup"><span data-stu-id="64ba9-116">Your choice affects how you authenticate access to resources in that account.</span></span>

- <span data-ttu-id="64ba9-117">**Abonnement au service Batch**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-117">**Batch service subscription**.</span></span> <span data-ttu-id="64ba9-118">Par défaut, les pools Batch sont alloués dans un abonnement au service Batch.</span><span class="sxs-lookup"><span data-stu-id="64ba9-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="64ba9-119">Si vous choisissez cette option, vous pouvez authentifier l’accès aux ressources de ce compte avec une [Clé partagée](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) ou avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-119">If you choose this option, you can authenticate access to resources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="64ba9-120">**Abonnement utilisateur.**</span><span class="sxs-lookup"><span data-stu-id="64ba9-120">**User subscription.**</span></span> <span data-ttu-id="64ba9-121">Vous pouvez choisir d’allouer des pools Batch dans un abonnement utilisateur que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="64ba9-121">You can choose to allocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="64ba9-122">Si vous choisissez cette option, vous devez vous authentifier auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="64ba9-123">Points de terminaison pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="64ba9-123">Endpoints for authentication</span></span>

<span data-ttu-id="64ba9-124">Pour authentifier des applications Batch avec Azure AD, vous devez inclure des points de terminaison connus dans votre code.</span><span class="sxs-lookup"><span data-stu-id="64ba9-124">To authenticate Batch applications with Azure AD, you need to include some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="64ba9-125">Point de terminaison Azure AD</span><span class="sxs-lookup"><span data-stu-id="64ba9-125">Azure AD endpoint</span></span>

<span data-ttu-id="64ba9-126">Le point de terminaison d’autorité Azure AD est :</span><span class="sxs-lookup"><span data-stu-id="64ba9-126">The base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="64ba9-127">Pour s’authentifier avec Azure AD, vous utilisez ce point de terminaison avec l’ID client (ID de répertoire).</span><span class="sxs-lookup"><span data-stu-id="64ba9-127">To authenticate with Azure AD, you use this endpoint together with the tenant ID (directory ID).</span></span> <span data-ttu-id="64ba9-128">L’ID client identifie le client Azure AD pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="64ba9-128">The tenant ID identifies the Azure AD tenant to use for authentication.</span></span> <span data-ttu-id="64ba9-129">Pour récupérer l’ID client, suivez les étapes décrites dans [Obtenir l’ID client pour Azure Active Directory](#get-the-tenant-id-for-your-active-directory) :</span><span class="sxs-lookup"><span data-stu-id="64ba9-129">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="64ba9-130">Le point de terminaison spécifique du client est requis lorsque vous vous authentifiez à l’aide d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="64ba9-130">The tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="64ba9-131">Le point de terminaison spécifique du client est facultatif lorsque vous vous authentifiez à l’aide de l’authentification intégrée, mais est recommandé.</span><span class="sxs-lookup"><span data-stu-id="64ba9-131">The tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="64ba9-132">Vous pouvez toutefois utiliser également le point de terminaison commun Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-132">However, you can also use the Azure AD common endpoint.</span></span> <span data-ttu-id="64ba9-133">Le point de terminaison commun fournit une interface de collecte d’informations d’identification générique lorsqu’un client spécifique n’est pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="64ba9-133">The common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="64ba9-134">Le point de terminaison commun est `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="64ba9-134">The common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="64ba9-135">Pour plus d’informations sur les points de terminaison Azure AD, consultez [Scénarios d’authentification pour Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="64ba9-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="64ba9-136">Point de terminaison de ressource Batch</span><span class="sxs-lookup"><span data-stu-id="64ba9-136">Batch resource endpoint</span></span>

<span data-ttu-id="64ba9-137">Utilisez le **point de terminaison de ressource Azure Batch** pour obtenir un jeton d’authentification des demandes au service Batch :</span><span class="sxs-lookup"><span data-stu-id="64ba9-137">Use the **Azure Batch resource endpoint** to acquire a token for authenticating requests to the Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="64ba9-138">Inscrire votre application avec un client</span><span class="sxs-lookup"><span data-stu-id="64ba9-138">Register your application with a tenant</span></span>

<span data-ttu-id="64ba9-139">La première étape d’utilisation d’Azure AD pour l’authentification consiste à inscrire votre application dans un client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-139">The first step in using Azure AD to authenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="64ba9-140">L’inscription de l’application vous permet d’appeler la [Bibliothèque d’authentification Active Directory][aad_adal] (ADAL) Azure à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="64ba9-140">Registering your application enables you to call the Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="64ba9-141">La bibliothèque ADAL fournit une API pour l’authentification avec Azure AD à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-141">The ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="64ba9-142">L’inscription de votre application est nécessaire si vous prévoyez d’utiliser l’authentification intégrée ou un principal de service.</span><span class="sxs-lookup"><span data-stu-id="64ba9-142">Registering your application is required whether you plan to use integrated authentication or a service principal.</span></span>

<span data-ttu-id="64ba9-143">Lorsque vous inscrivez votre application, vous fournissez des informations sur votre application à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-143">When you register your application, you supply information about your application to Azure AD.</span></span> <span data-ttu-id="64ba9-144">Azure AD fournit ensuite un ID d’application que vous utilisez pour associer votre application à Azure AD lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="64ba9-144">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="64ba9-145">Pour en savoir plus sur l’ID d’application, consultez [Objets application et principal du service dans Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="64ba9-145">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="64ba9-146">Suivez les étapes de la section [Ajout d’une application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) dans [Intégration d’applications dans Azure Active Directory][aad_integrate] pour inscrire votre application Batch.</span><span class="sxs-lookup"><span data-stu-id="64ba9-146">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="64ba9-147">Si vous inscrivez votre application en tant qu’application native, vous pouvez spécifier n’importe quel URI valide pour l’**URI de redirection**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-147">If you register your application as a Native Application, you can specify any valid URI for the **Redirect URI**.</span></span> <span data-ttu-id="64ba9-148">Aucun point de terminaison réel n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="64ba9-148">It does not need to be a real endpoint.</span></span>

<span data-ttu-id="64ba9-149">Une fois que vous avez inscrit votre application, vous verrez l’ID d’application :</span><span class="sxs-lookup"><span data-stu-id="64ba9-149">After you've registered your application, you'll see the application ID:</span></span>

![Inscrire votre application Batch auprès d’Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="64ba9-151">Pour plus d’informations sur l’inscription d’une application avec Azure AD, consultez [Scénarios d’authentification pour Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="64ba9-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-the-tenant-id-for-your-active-directory"></a><span data-ttu-id="64ba9-152">Obtenir l’ID client pour votre Active Directory</span><span class="sxs-lookup"><span data-stu-id="64ba9-152">Get the tenant ID for your Active Directory</span></span>

<span data-ttu-id="64ba9-153">L’ID client identifie le client Azure AD qui fournit des services d’authentification à votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-153">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="64ba9-154">Pour obtenir l’ID client, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="64ba9-154">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="64ba9-155">Dans le portail Azure, sélectionnez votre Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64ba9-155">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="64ba9-156">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-156">Click **Properties**.</span></span>
3. <span data-ttu-id="64ba9-157">Copiez la valeur GUID fournie pour l’ID de répertoire.</span><span class="sxs-lookup"><span data-stu-id="64ba9-157">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="64ba9-158">Cette valeur est également appelée l’ID client.</span><span class="sxs-lookup"><span data-stu-id="64ba9-158">This value is also called the tenant ID.</span></span>

![Copier l’ID de répertoire](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="64ba9-160">Utiliser l’authentification intégrée</span><span class="sxs-lookup"><span data-stu-id="64ba9-160">Use integrated authentication</span></span>

<span data-ttu-id="64ba9-161">Pour l’authentification avec l’authentification intégrée, vous devez autoriser votre application à se connecter à l’API de service Batch.</span><span class="sxs-lookup"><span data-stu-id="64ba9-161">To authenticate with integrated authentication, you need to grant your application permissions to connect to the Batch service API.</span></span> <span data-ttu-id="64ba9-162">Cette étape permet à votre application d’authentifier des appels de l’API de service Batch avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-162">This step enables your application to authenticate calls to the Batch service API with Azure AD.</span></span>

<span data-ttu-id="64ba9-163">Une fois que vous avez [inscrit votre application](#register-your-application-with-an-azure-ad-tenant), procédez comme suit dans le portail Azure pour lui accorder l’accès au service Batch :</span><span class="sxs-lookup"><span data-stu-id="64ba9-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in the Azure portal to grant it access to the Batch service:</span></span>

1. <span data-ttu-id="64ba9-164">Dans le volet de navigation de gauche du portail Azure, choisissez **Plus de services**, cliquez sur **Inscriptions d’application**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-164">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="64ba9-165">Recherchez le nom de votre application dans la liste des inscriptions d’application :</span><span class="sxs-lookup"><span data-stu-id="64ba9-165">Search for the name of your application in the list of app registrations:</span></span>

    ![Rechercher le nom de votre application](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="64ba9-167">Ouvrez le panneau **Paramètres** de votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-167">Open the **Settings** blade for your application.</span></span> <span data-ttu-id="64ba9-168">Dans la section **Accès API**, sélectionnez **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-168">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="64ba9-169">Dans le panneau **Autorisations requises**, cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-169">In the **Required permissions** blade, click the **Add** button.</span></span>
5. <span data-ttu-id="64ba9-170">À l’étape 1, recherchez l’API Batch.</span><span class="sxs-lookup"><span data-stu-id="64ba9-170">In step 1, search for the Batch API.</span></span> <span data-ttu-id="64ba9-171">Recherchez chacune de ces chaînes, jusqu’à ce que vous trouviez l’API :</span><span class="sxs-lookup"><span data-stu-id="64ba9-171">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="64ba9-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="64ba9-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="64ba9-174">Les locataires Azure AD les plus récents peuvent utiliser ce nom.</span><span class="sxs-lookup"><span data-stu-id="64ba9-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="64ba9-175">La chaîne **ddbf3205-c6bd-46ae-8127-60eb93363864** correspond à l’ID de l’API Batch.</span><span class="sxs-lookup"><span data-stu-id="64ba9-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 
6. <span data-ttu-id="64ba9-176">Une fois que vous avez trouvé l’API Batch, sélectionnez-la, puis cliquez sur le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-176">Once you find the Batch API, select it and click the **Select** button.</span></span>
6. <span data-ttu-id="64ba9-177">À l’étape 2, activez la case à cocher en regard de **Access Azure Batch Service** (Accéder au service Azure Batch) et cliquez sur le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-177">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
7. <span data-ttu-id="64ba9-178">Cliquez sur le bouton **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-178">Click the **Done** button.</span></span>

<span data-ttu-id="64ba9-179">Le panneau **Autorisations requises** indique à présent que votre application Azure AD autorise l’accès à la bibliothèque ADAL et à l’API de service Batch.</span><span class="sxs-lookup"><span data-stu-id="64ba9-179">The **Required Permissions** blade now shows that your Azure AD application has access to both ADAL and the Batch service API.</span></span> <span data-ttu-id="64ba9-180">Les autorisations sont accordées automatiquement à ADAL lorsque vous commencez par inscrire votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-180">Permissions are granted to ADAL automatically when you first register your app with Azure AD.</span></span>

![Accorder des autorisations d’API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="64ba9-182">Utiliser un principal de service</span><span class="sxs-lookup"><span data-stu-id="64ba9-182">Use a service principal</span></span> 

<span data-ttu-id="64ba9-183">Pour authentifier une application qui s’exécute sans assistance, vous utilisez un principal de service.</span><span class="sxs-lookup"><span data-stu-id="64ba9-183">To authenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="64ba9-184">Après avoir inscrit votre application, procédez comme suit dans le portail Azure pour configurer un principal de service :</span><span class="sxs-lookup"><span data-stu-id="64ba9-184">After you've registered your application, follow these steps in the Azure portal to configure a service principal:</span></span>

1. <span data-ttu-id="64ba9-185">Demandez une clé secrète pour votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="64ba9-186">Attribuez un rôle RBAC à votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-186">Assign an RBAC role to your application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="64ba9-187">Demander une clé secrète pour votre application</span><span class="sxs-lookup"><span data-stu-id="64ba9-187">Request a secret key for your application</span></span>

<span data-ttu-id="64ba9-188">Lorsque votre application s’authentifie avec un service principal, elle envoie l’ID d’application et une clé secrète à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-188">When your application authenticates with a service principal, it sends both the application ID and a secret key to Azure AD.</span></span> <span data-ttu-id="64ba9-189">Vous devez créer et copier la clé secrète à utiliser à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="64ba9-189">You'll need to create and copy the secret key to use from your code.</span></span>

<span data-ttu-id="64ba9-190">Suivez les étapes ci-dessous dans le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="64ba9-190">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="64ba9-191">Dans le volet de navigation de gauche du portail Azure, choisissez **Plus de services**, cliquez sur **Inscriptions d’application**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-191">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="64ba9-192">Recherchez le nom de votre application dans la liste des inscriptions d’application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-192">Search for the name of your application in the list of app registrations.</span></span>
3. <span data-ttu-id="64ba9-193">Affichez le panneau **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-193">Display the **Settings** blade.</span></span> <span data-ttu-id="64ba9-194">Dans la section **Accès API**, sélectionnez **Clés**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-194">In the **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="64ba9-195">Pour créer une clé, entrez une description de la clé.</span><span class="sxs-lookup"><span data-stu-id="64ba9-195">To create a key, enter a description for the key.</span></span> <span data-ttu-id="64ba9-196">Sélectionnez ensuite la durée de la clé, un ou deux ans.</span><span class="sxs-lookup"><span data-stu-id="64ba9-196">Then select a duration for the key of either one or two years.</span></span> 
5. <span data-ttu-id="64ba9-197">Cliquez sur le bouton **Enregistrer** pour créer et afficher la clé.</span><span class="sxs-lookup"><span data-stu-id="64ba9-197">Click the **Save** button to create and display the key.</span></span> <span data-ttu-id="64ba9-198">Copiez la valeur de clé dans un endroit sûr, car vous n’y avez plus accès lorsque vous quittez le panneau.</span><span class="sxs-lookup"><span data-stu-id="64ba9-198">Copy the key value to a safe place, as you won't be able to access it again after you leave the blade.</span></span> 

    ![Créer une clé secrète](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a><span data-ttu-id="64ba9-200">Attribuer un rôle RBAC à votre application</span><span class="sxs-lookup"><span data-stu-id="64ba9-200">Assign an RBAC role to your application</span></span>

<span data-ttu-id="64ba9-201">Pour s’authentifier avec un principal de service, vous devez attribuer un rôle RBAC à votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-201">To authenticate with a service principal, you need to assign an RBAC role to your application.</span></span> <span data-ttu-id="64ba9-202">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="64ba9-202">Follow these steps:</span></span>

1. <span data-ttu-id="64ba9-203">Dans le portail Azure, accédez au compte Batch utilisé par votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-203">In the Azure portal, navigate to the Batch account used by your application.</span></span>
2. <span data-ttu-id="64ba9-204">Dans le panneau **Paramètres** du compte Batch, sélectionnez **Contrôle d’accès (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-204">In the **Settings** blade for the Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="64ba9-205">Cliquez sur le bouton **Add** .</span><span class="sxs-lookup"><span data-stu-id="64ba9-205">Click the **Add** button.</span></span> 
4. <span data-ttu-id="64ba9-206">Dans la liste déroulante **Rôle**, choisissez le rôle _Collaborateur_ ou _Lecteur_ pour votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-206">From the **Role** drop-down, choose either the _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="64ba9-207">Pour plus d’informations sur ces rôles, consultez [Prise en main du contrôle d’accès en fonction du rôle dans le portail Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="64ba9-207">For more information on these roles, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="64ba9-208">Dans le champ **Sélectionner**, entrez le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-208">In the **Select** field, enter the name of your application.</span></span> <span data-ttu-id="64ba9-209">Sélectionnez votre application dans la liste, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-209">Select your application from the list, and click **Save**.</span></span>

<span data-ttu-id="64ba9-210">Votre application doit maintenant apparaître dans vos paramètres de contrôle d’accès avec un rôle RBAC qui lui est attribué.</span><span class="sxs-lookup"><span data-stu-id="64ba9-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Attribuer un rôle RBAC à votre application](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="64ba9-212">Obtenir l’ID client pour votre Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64ba9-212">Get the tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="64ba9-213">L’ID client identifie le client Azure AD qui fournit des services d’authentification à votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-213">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="64ba9-214">Pour obtenir l’ID client, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="64ba9-214">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="64ba9-215">Dans le portail Azure, sélectionnez votre Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64ba9-215">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="64ba9-216">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-216">Click **Properties**.</span></span>
3. <span data-ttu-id="64ba9-217">Copiez la valeur GUID fournie pour l’ID de répertoire.</span><span class="sxs-lookup"><span data-stu-id="64ba9-217">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="64ba9-218">Cette valeur est également appelée l’ID client.</span><span class="sxs-lookup"><span data-stu-id="64ba9-218">This value is also called the tenant ID.</span></span>

![Copier l’ID de répertoire](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="64ba9-220">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="64ba9-220">Code examples</span></span>

<span data-ttu-id="64ba9-221">Les exemples de code de cette section montrent comment s’authentifier avec Azure AD à l’aide de l’authentification intégrée et d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="64ba9-221">The code examples in this section show how to authenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="64ba9-222">Ces exemples de code utilisent .NET, mais les concepts sont similaires pour d’autres langages.</span><span class="sxs-lookup"><span data-stu-id="64ba9-222">These code examples use .NET, but the concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="64ba9-223">Un jeton d’authentification Azure AD expire au bout d’une heure.</span><span class="sxs-lookup"><span data-stu-id="64ba9-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="64ba9-224">Lorsque vous utilisez un objet **BatchClient** longue durée, nous vous recommandons de récupérer un jeton à partir d’ADAL à chaque demande pour garantir que vous disposez toujours d’un jeton valide.</span><span class="sxs-lookup"><span data-stu-id="64ba9-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="64ba9-225">Pour mettre cela en place dans .NET, écrivez une méthode qui récupère le jeton à partir d’Azure AD et qui transmet cette méthode à un objet **BatchTokenCredentials** en tant que délégué.</span><span class="sxs-lookup"><span data-stu-id="64ba9-225">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="64ba9-226">La méthode du délégué est appelée à chaque demande au service Batch pour garantir qu’un jeton valide est fourni.</span><span class="sxs-lookup"><span data-stu-id="64ba9-226">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="64ba9-227">Par défaut, ADAL met en cache des jetons pour qu’un nouveau jeton soit récupéré à partir d’Azure AD uniquement lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="64ba9-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="64ba9-228">Pour plus d’informations sur les jetons dans Azure AD, consultez [Scénarios d’authentification pour Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="64ba9-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="64ba9-229">Exemple de code : utilisation de l’authentification intégrée Azure AD avec Batch .NET</span><span class="sxs-lookup"><span data-stu-id="64ba9-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="64ba9-230">Pour s’authentifier avec l’authentification intégrée à partir de Batch .NET, vous devez référencer les packages [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) et [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="64ba9-230">To authenticate with integrated authentication from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="64ba9-231">Ajoutez les instructions `using` suivantes dans votre code :</span><span class="sxs-lookup"><span data-stu-id="64ba9-231">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="64ba9-232">Référencez le point de terminaison Azure AD dans votre code, y compris l’ID client.</span><span class="sxs-lookup"><span data-stu-id="64ba9-232">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="64ba9-233">Pour récupérer l’ID client, suivez les étapes décrites dans [Obtenir l’ID client pour Azure Active Directory](#get-the-tenant-id-for-your-active-directory) :</span><span class="sxs-lookup"><span data-stu-id="64ba9-233">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="64ba9-234">Référencez le point de terminaison de ressource de service Batch :</span><span class="sxs-lookup"><span data-stu-id="64ba9-234">Reference the Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="64ba9-235">Référencez votre compte Batch :</span><span class="sxs-lookup"><span data-stu-id="64ba9-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="64ba9-236">Spécifiez l’ID d’application (ID client) pour votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-236">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="64ba9-237">L’ID d’application est disponible dans votre inscription d’application dans le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="64ba9-237">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="64ba9-238">Copiez également l’URI de redirection que vous avez spécifiée pendant l’inscription.</span><span class="sxs-lookup"><span data-stu-id="64ba9-238">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="64ba9-239">L’URI de redirection spécifié dans votre code doit correspondre à l’URI de redirection que vous avez fourni lors de l’inscription de l’application :</span><span class="sxs-lookup"><span data-stu-id="64ba9-239">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="64ba9-240">Écrivez une méthode de rappel pour acquérir le jeton d’authentification à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-240">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="64ba9-241">La méthode de rappel **GetAuthenticationTokenAsync** illustrée appelle ici la bibliothèque ADAL pour authentifier un utilisateur qui interagit avec l’application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-241">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL to authenticate a user who is interacting with the application.</span></span> <span data-ttu-id="64ba9-242">La méthode **AcquireTokenAsync** fournie par la bibliothèque ADAL demande à l’utilisateur ses informations d’identification, et l’application continue une fois que l’utilisateur les a fournies (sauf si elle dispose déjà d’informations d’identification mises en cache) :</span><span class="sxs-lookup"><span data-stu-id="64ba9-242">The **AcquireTokenAsync** method provided by ADAL prompts the user for their credentials, and the application proceeds once the user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="64ba9-243">Créez un objet **BatchTokenCredentials** qui prend le délégué comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="64ba9-243">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="64ba9-244">Utilisez ces informations d’identification pour ouvrir un objet **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-244">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="64ba9-245">Vous pouvez utiliser cet objet **BatchClient** pour les opérations suivantes sur le service Batch :</span><span class="sxs-lookup"><span data-stu-id="64ba9-245">You can use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="64ba9-246">Exemple de code : utilisation d’un principal de service Azure AD avec Batch .NET</span><span class="sxs-lookup"><span data-stu-id="64ba9-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="64ba9-247">Pour s’authentifier avec un principal de service à partir de Batch .NET, vous devez référencer les packages [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) et [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="64ba9-247">To authenticate with a service principal from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="64ba9-248">Ajoutez les instructions `using` suivantes dans votre code :</span><span class="sxs-lookup"><span data-stu-id="64ba9-248">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="64ba9-249">Référencez le point de terminaison Azure AD dans votre code, y compris l’ID client.</span><span class="sxs-lookup"><span data-stu-id="64ba9-249">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="64ba9-250">Lorsque vous utilisez un principal de service, vous devez indiquer un point de terminaison spécifique du client.</span><span class="sxs-lookup"><span data-stu-id="64ba9-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="64ba9-251">Pour récupérer l’ID client, suivez les étapes décrites dans [Obtenir l’ID client pour Azure Active Directory](#get-the-tenant-id-for-your-active-directory) :</span><span class="sxs-lookup"><span data-stu-id="64ba9-251">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="64ba9-252">Référencez le point de terminaison de ressource de service Batch :</span><span class="sxs-lookup"><span data-stu-id="64ba9-252">Reference the Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="64ba9-253">Référencez votre compte Batch :</span><span class="sxs-lookup"><span data-stu-id="64ba9-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="64ba9-254">Spécifiez l’ID d’application (ID client) pour votre application.</span><span class="sxs-lookup"><span data-stu-id="64ba9-254">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="64ba9-255">L’ID d’application est disponible dans votre inscription d’application dans le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="64ba9-255">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="64ba9-256">Spécifiez la clé secrète que vous avez copiée à partir du portail Azure :</span><span class="sxs-lookup"><span data-stu-id="64ba9-256">Specify the secret key that you copied from the Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="64ba9-257">Écrivez une méthode de rappel pour acquérir le jeton d’authentification à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ba9-257">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="64ba9-258">La méthode de rappel **GetAuthenticationTokenAsync** illustrée ici appelle la bibliothèque ADAL pour l’authentification sans assistance :</span><span class="sxs-lookup"><span data-stu-id="64ba9-258">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="64ba9-259">Créez un objet **BatchTokenCredentials** qui prend le délégué comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="64ba9-259">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="64ba9-260">Utilisez ces informations d’identification pour ouvrir un objet **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="64ba9-260">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="64ba9-261">Vous pouvez ensuite utiliser cet objet **BatchClient** pour les opérations suivantes sur le service Batch :</span><span class="sxs-lookup"><span data-stu-id="64ba9-261">You can then use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="64ba9-262">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64ba9-262">Next steps</span></span>

<span data-ttu-id="64ba9-263">Pour en savoir plus sur Azure AD, consultez la [documentation sur Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="64ba9-263">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="64ba9-264">Des exemples détaillés illustrant l’utilisation d’ADAL sont disponibles dans la bibliothèque [Exemples de code Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="64ba9-264">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="64ba9-265">Pour en savoir plus sur les principaux de service, consultez [Objets application et principal de service dans Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="64ba9-265">To learn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="64ba9-266">Pour créer un principal de service à l’aide du portail Azure, consultez [Utiliser le portail Azure pour créer une application et un principal de service Active Directory pouvant accéder aux ressources](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="64ba9-266">To create a service principal using the Azure portal, see [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="64ba9-267">Vous pouvez également créer un principal de service avec PowerShell ou Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="64ba9-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="64ba9-268">Pour authentifier des applications de gestion Batch à l’aide d’Azure AD, consultez [Solutions de gestion Batch avec Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="64ba9-268">To authenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

<span data-ttu-id="64ba9-269">[aad_about]: ../active-directory/active-directory-whatis.md "Qu’est-ce qu’Azure Active Directory ?"</span><span class="sxs-lookup"><span data-stu-id="64ba9-269">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="64ba9-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scénarios d’authentification pour Azure AD"</span><span class="sxs-lookup"><span data-stu-id="64ba9-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="64ba9-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Intégration d’applications dans Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="64ba9-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[azure_portal]: http://portal.azure.com
