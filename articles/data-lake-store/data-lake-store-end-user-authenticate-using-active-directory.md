---
title: "Authentification d’utilisateur final : Data Lake Store à l’aide d’Azure Active Directory | Microsoft Docs"
description: "Découvrez comment l’authentification de l’utilisateur final de tooachieve avec Data Lake Store à l’aide d’Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="60b51-103">Authentification d’utilisateur final auprès de Data Lake Store à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60b51-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60b51-104">Authentification de service à service</span><span class="sxs-lookup"><span data-stu-id="60b51-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="60b51-105">Authentification de l’utilisateur final</span><span class="sxs-lookup"><span data-stu-id="60b51-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="60b51-106">Azure Data Lake Store utilise Azure Active Directory pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="60b51-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="60b51-107">Avant la création d’une application qui fonctionne avec Azure Data Lake Store ou Analytique de LAC de données Azure, vous devez d’abord déterminer comment vous voulez tooauthenticate votre application avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60b51-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="60b51-108">Hello deux options disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="60b51-108">hello two main options available are:</span></span>

* <span data-ttu-id="60b51-109">Authentification de l’utilisateur final (cet article)</span><span class="sxs-lookup"><span data-stu-id="60b51-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="60b51-110">Authentification de service à service</span><span class="sxs-lookup"><span data-stu-id="60b51-110">Service-to-service authentication</span></span>

<span data-ttu-id="60b51-111">Ces deux options entraîner dans votre application qui est fournie avec un jeton OAuth 2.0, qui obtient tooeach attaché demande faite tooAzure Data Lake Store ou Analytique de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="60b51-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="60b51-112">Cet article traite de la création d’une **application native Azure AD pour l’authentification de l’utilisateur final**.</span><span class="sxs-lookup"><span data-stu-id="60b51-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="60b51-113">Pour obtenir des instructions sur la configuration de l’application Azure AD pour l’authentification de service à service, voir [Authentification de service à service avec Data Lake Store à l’aide d’Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="60b51-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60b51-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="60b51-114">Prerequisites</span></span>
* <span data-ttu-id="60b51-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="60b51-115">An Azure subscription.</span></span> <span data-ttu-id="60b51-116">Consultez [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60b51-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="60b51-117">Votre ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="60b51-117">Your subscription ID.</span></span> <span data-ttu-id="60b51-118">Vous pouvez le récupérer à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="60b51-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="60b51-119">Par exemple, il est disponible à partir du Panneau de compte Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="60b51-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![Obtenir l’ID d’abonnement](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="60b51-121">Votre nom de domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60b51-121">Your Azure AD domain name.</span></span> <span data-ttu-id="60b51-122">Vous pouvez le récupérer par pointage de souris hello en hello en haut à droite de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="60b51-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="60b51-123">À partir de la capture d’écran de hello ci-dessous, nom de domaine hello est **contoso.onmicrosoft.com**, et hello GUID entre crochets est l’ID de client hello.</span><span class="sxs-lookup"><span data-stu-id="60b51-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![Obtenir le domaine AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="60b51-125">Authentification de l’utilisateur final</span><span class="sxs-lookup"><span data-stu-id="60b51-125">End-user authentication</span></span>
<span data-ttu-id="60b51-126">Il s’agit de hello approche recommandée si vous souhaitez une toolog par l’utilisateur dans l’application tooyour via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60b51-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="60b51-127">Votre application peut être en mesure de tooaccess ressources Windows Azure avec hello même niveau d’accès en tant qu’utilisateur final hello qui connecté.</span><span class="sxs-lookup"><span data-stu-id="60b51-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="60b51-128">Vos utilisateurs finaux devez tooprovide leurs informations d’identification régulièrement dans l’ordre pour votre application l’accès toomaintain.</span><span class="sxs-lookup"><span data-stu-id="60b51-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="60b51-129">résultat de Hello d’avoir à l’utilisateur final hello connectez-vous est que votre application reçoit un jeton d’accès et un jeton d’actualisation.</span><span class="sxs-lookup"><span data-stu-id="60b51-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="60b51-130">jeton d’accès Hello obtient demande attaché tooeach tooData Lake Store ou Analytique lac de données, et il n’est valide pendant une heure par défaut.</span><span class="sxs-lookup"><span data-stu-id="60b51-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="60b51-131">jeton d’actualisation Hello peut être utilisé tooobtain un nouveau jeton d’accès et il n’est valide pour les semaines tootwo par défaut, si utiliser régulièrement.</span><span class="sxs-lookup"><span data-stu-id="60b51-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="60b51-132">Vous pouvez utiliser deux approches différentes pour la connexion de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="60b51-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="60b51-133">À l’aide de la fenêtre contextuelle de hello OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="60b51-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="60b51-134">Votre application peut déclencher une fenêtre de d’autorisation OAuth 2.0, les Bonjour par l’utilisateur peut entrer leurs informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="60b51-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="60b51-135">Cette fenêtre contextuelle fonctionne également avec les processus d’authentification à deux facteurs Azure AD (2FA) hello, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="60b51-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="60b51-136">Cette méthode n’est pas encore prise en charge dans la bibliothèque d’authentification Azure AD (ADAL) de hello pour Python ou Java.</span><span class="sxs-lookup"><span data-stu-id="60b51-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="60b51-137">Transmission directe des informations d’identification de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="60b51-137">Directly passing in user credentials</span></span>
<span data-ttu-id="60b51-138">Votre application peut fournir directement tooAzure des informations d’identification utilisateur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60b51-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="60b51-139">Cette méthode fonctionne uniquement avec les comptes d’utilisateur dotés d’ID d’organisation. Elle n’est pas compatible avec les comptes d’utilisateur personnels ou « live ID », notamment ceux se terminant par @outlook.com ou @live.com. En outre, cette méthode n’est pas compatible avec les comptes d’utilisateur qui nécessitent l’authentification à 2 facteurs Azure AD (TFA).</span><span class="sxs-lookup"><span data-stu-id="60b51-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="60b51-140">Comment dois-je toouse cette approche ?</span><span class="sxs-lookup"><span data-stu-id="60b51-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="60b51-141">Votre nom de domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60b51-141">Azure AD domain name.</span></span> <span data-ttu-id="60b51-142">Cette figure déjà dans la condition préalable de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="60b51-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="60b51-143">Application native **Azure AD**</span><span class="sxs-lookup"><span data-stu-id="60b51-143">Azure AD **native application**</span></span>
* <span data-ttu-id="60b51-144">ID d’application pour l’application native de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="60b51-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="60b51-145">URI de redirection de hello application native d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="60b51-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="60b51-146">Définir des autorisations déléguées</span><span class="sxs-lookup"><span data-stu-id="60b51-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="60b51-147">Étape 1 : Créer une application native Active Directory</span><span class="sxs-lookup"><span data-stu-id="60b51-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="60b51-148">Créez et configurez une application native Azure AD pour l’authentification de l’utilisateur final auprès d’Azure Data Lake Store à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60b51-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="60b51-149">Pour obtenir des instructions, consultez la page [Créer une application Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="60b51-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="60b51-150">Tout en suivant les instructions de hello en hello au-dessus de lien, veillez à sélectionner **natif** pour le type d’application, comme indiqué dans la capture d’écran hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="60b51-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="60b51-151">![Créer une application web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Créer une application native")</span><span class="sxs-lookup"><span data-stu-id="60b51-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="60b51-152">Étape 2 : Obtenir l’ID et l’URI de redirection de l’application</span><span class="sxs-lookup"><span data-stu-id="60b51-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="60b51-153">Consultez [obtenir l’ID de l’application hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello id d’application (également appelé ID de client hello Bonjour portail Azure classic) d’application native de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60b51-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="60b51-154">tooretrieve hello URI de redirection, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="60b51-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="60b51-155">À partir de hello portail Azure, sélectionnez **Azure Active Directory**, cliquez sur **inscriptions d’application**, recherchez et cliquez sur application native hello Azure AD que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="60b51-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="60b51-156">À partir de hello **paramètres** panneau pour l’application hello, cliquez sur **URI de redirection**.</span><span class="sxs-lookup"><span data-stu-id="60b51-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![Obtenir un URI de redirection](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="60b51-158">Copiez la valeur hello affichée.</span><span class="sxs-lookup"><span data-stu-id="60b51-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="60b51-159">Étape 3 : Définir des autorisations</span><span class="sxs-lookup"><span data-stu-id="60b51-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="60b51-160">À partir de hello portail Azure, sélectionnez **Azure Active Directory**, cliquez sur **inscriptions d’application**, recherchez et cliquez sur application native hello Azure AD que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="60b51-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="60b51-161">À partir de hello **paramètres** panneau pour l’application hello, cliquez sur **autorisations requises**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="60b51-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="60b51-163">Bonjour **ajouter l’accès aux API** panneau, cliquez sur **sélectionner une API**, cliquez sur **Azure Data Lake**, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="60b51-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="60b51-165">Bonjour **ajouter l’accès aux API** panneau, cliquez sur **sélectionner les autorisations**, sélectionnez hello case à cocher toogive **accès total tooData Lake Store**, puis cliquez sur **sélectionner** .</span><span class="sxs-lookup"><span data-stu-id="60b51-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="60b51-167">Cliquez sur **Done**.</span><span class="sxs-lookup"><span data-stu-id="60b51-167">Click **Done**.</span></span>

5. <span data-ttu-id="60b51-168">Répétition hello dernières étapes de deux autorisations toogrant pour **API de gestion Windows Azure** également.</span><span class="sxs-lookup"><span data-stu-id="60b51-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="60b51-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60b51-169">Next steps</span></span>
<span data-ttu-id="60b51-170">Dans cet article vous créé une application native d’Azure AD et collecté les informations de hello que vous avez besoin dans vos applications clientes que vous créez à l’aide du Kit de développement .NET, Java SDK, les API REST, etc.. Vous pouvez maintenant toohello suivant des articles de parler de la façon dont toouse hello AD Azure web application toofirst s’authentifient avec Data Lake Store et autres opérations sur le magasin de hello.</span><span class="sxs-lookup"><span data-stu-id="60b51-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="60b51-171">Prise en main d'Azure Data Lake Store avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="60b51-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="60b51-172">Prise en main d’Azure Data Lake Store à l’aide du Kit de développement logiciel (SDK) Java</span><span class="sxs-lookup"><span data-stu-id="60b51-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="60b51-173">Prise en main d’Azure Data Lake Store à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="60b51-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

