---
title: "Authentification d’utilisateur final : Data Lake Store à l’aide d’Azure Active Directory | Microsoft Docs"
description: "Découvrez comment authentifier l’utilisateur final auprès de Data Lake Store à l’aide d’Azure Active Directory"
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
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="58ffa-103">Authentification d’utilisateur final auprès de Data Lake Store à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58ffa-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58ffa-104">Authentification de service à service</span><span class="sxs-lookup"><span data-stu-id="58ffa-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="58ffa-105">Authentification de l’utilisateur final</span><span class="sxs-lookup"><span data-stu-id="58ffa-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="58ffa-106">Azure Data Lake Store utilise Azure Active Directory pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="58ffa-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="58ffa-107">Avant de créer une application qui fonctionne avec Azure Data Lake Store ou Azure Data Lake Analytics, vous devez commencer par déterminer comment vous voulez authentifier votre application avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="58ffa-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="58ffa-108">Les deux options principales disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="58ffa-108">The two main options available are:</span></span>

* <span data-ttu-id="58ffa-109">Authentification de l’utilisateur final (cet article)</span><span class="sxs-lookup"><span data-stu-id="58ffa-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="58ffa-110">Authentification de service à service</span><span class="sxs-lookup"><span data-stu-id="58ffa-110">Service-to-service authentication</span></span>

<span data-ttu-id="58ffa-111">En raison de ces deux options, votre application est fournie avec un jeton OAuth 2.0, qui est attaché à chaque demande adressée à Azure Data Lake Store ou Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="58ffa-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="58ffa-112">Cet article traite de la création d’une **application native Azure AD pour l’authentification de l’utilisateur final**.</span><span class="sxs-lookup"><span data-stu-id="58ffa-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="58ffa-113">Pour obtenir des instructions sur la configuration de l’application Azure AD pour l’authentification de service à service, voir [Authentification de service à service avec Data Lake Store à l’aide d’Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="58ffa-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58ffa-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="58ffa-114">Prerequisites</span></span>
* <span data-ttu-id="58ffa-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="58ffa-115">An Azure subscription.</span></span> <span data-ttu-id="58ffa-116">Consultez [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58ffa-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="58ffa-117">Votre ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="58ffa-117">Your subscription ID.</span></span> <span data-ttu-id="58ffa-118">Vous pouvez le récupérer à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="58ffa-118">You can retrieve it from the Azure Portal.</span></span> <span data-ttu-id="58ffa-119">Par exemple, il est disponible à partir du panneau de compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="58ffa-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![Obtenir l’ID d’abonnement](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="58ffa-121">Votre nom de domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58ffa-121">Your Azure AD domain name.</span></span> <span data-ttu-id="58ffa-122">Vous pouvez le récupérer en pointant la souris dans le coin supérieur droit du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="58ffa-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span></span> <span data-ttu-id="58ffa-123">Dans la capture d’écran ci-dessous, le nom de domaine est **contoso.onmicrosoft.com**, et le GUID entre crochets est l’ID client.</span><span class="sxs-lookup"><span data-stu-id="58ffa-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![Obtenir le domaine AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="58ffa-125">Authentification de l’utilisateur final</span><span class="sxs-lookup"><span data-stu-id="58ffa-125">End-user authentication</span></span>
<span data-ttu-id="58ffa-126">Il s’agit de l’approche recommandée si vous souhaitez qu’un utilisateur final se connecte à votre application via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58ffa-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span></span> <span data-ttu-id="58ffa-127">Votre application sera en mesure d’accéder aux ressources Azure avec le même niveau d’accès que l’utilisateur final qui s’est connecté.</span><span class="sxs-lookup"><span data-stu-id="58ffa-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span></span> <span data-ttu-id="58ffa-128">Votre utilisateur final devra fournir ses informations d’identification régulièrement pour que votre application conserve l’accès.</span><span class="sxs-lookup"><span data-stu-id="58ffa-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="58ffa-129">Conséquence de la connexion de l’utilisateur final : votre application reçoit un jeton d’accès et un jeton d’actualisation.</span><span class="sxs-lookup"><span data-stu-id="58ffa-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="58ffa-130">Le jeton d’accès est lié à chaque demande adressée au Data Lake Store ou à Data Lake Analytics et, par défaut, il est valide pendant une heure.</span><span class="sxs-lookup"><span data-stu-id="58ffa-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="58ffa-131">Le jeton d’actualisation peut être utilisé pour obtenir un nouveau jeton d’accès et, par défaut, il est valide pendant deux semaines au maximum, s’il est régulièrement utilisé.</span><span class="sxs-lookup"><span data-stu-id="58ffa-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="58ffa-132">Vous pouvez utiliser deux approches différentes pour la connexion de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="58ffa-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="58ffa-133">Utilisation de la fenêtre contextuelle OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="58ffa-133">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="58ffa-134">Votre application peut déclencher une fenêtre contextuelle d’autorisation OAuth 2.0 dans laquelle l’utilisateur final peut entrer ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="58ffa-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span></span> <span data-ttu-id="58ffa-135">Cette fenêtre contextuelle fonctionne également avec le processus d’authentification à 2 facteurs Azure AD (TFA), si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="58ffa-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="58ffa-136">Cette méthode n’est pas encore prise en charge dans la bibliothèque d’authentification Azure AD (ADAL) pour Python ou Java.</span><span class="sxs-lookup"><span data-stu-id="58ffa-136">This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="58ffa-137">Transmission directe des informations d’identification de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="58ffa-137">Directly passing in user credentials</span></span>
<span data-ttu-id="58ffa-138">Votre application peut fournir directement des informations d’identification de l’utilisateur à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58ffa-138">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="58ffa-139">Cette méthode fonctionne uniquement avec les comptes d’utilisateur dotés d’ID d’organisation. Elle n’est pas compatible avec les comptes d’utilisateur personnels ou « live ID », notamment ceux se terminant par @outlook.com ou @live.com.</span><span class="sxs-lookup"><span data-stu-id="58ffa-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="58ffa-140">En outre, cette méthode n’est pas compatible avec les comptes d’utilisateur qui nécessitent l’authentification à 2 facteurs Azure AD (TFA).</span><span class="sxs-lookup"><span data-stu-id="58ffa-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-to-use-this-approach"></a><span data-ttu-id="58ffa-141">De quoi ai-je besoin pour utiliser cette approche ?</span><span class="sxs-lookup"><span data-stu-id="58ffa-141">What do I need to use this approach?</span></span>
* <span data-ttu-id="58ffa-142">Votre nom de domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58ffa-142">Azure AD domain name.</span></span> <span data-ttu-id="58ffa-143">Celui-ci est déjà répertorié dans les conditions préalables de cet article.</span><span class="sxs-lookup"><span data-stu-id="58ffa-143">This is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="58ffa-144">Application native **Azure AD**</span><span class="sxs-lookup"><span data-stu-id="58ffa-144">Azure AD **native application**</span></span>
* <span data-ttu-id="58ffa-145">ID de l’application native Azure AD</span><span class="sxs-lookup"><span data-stu-id="58ffa-145">Application ID for the Azure AD native application</span></span>
* <span data-ttu-id="58ffa-146">URI de redirection de l’application native Azure AD</span><span class="sxs-lookup"><span data-stu-id="58ffa-146">Redirect URI for the Azure AD native application</span></span>
* <span data-ttu-id="58ffa-147">Définir des autorisations déléguées</span><span class="sxs-lookup"><span data-stu-id="58ffa-147">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="58ffa-148">Étape 1 : Créer une application native Active Directory</span><span class="sxs-lookup"><span data-stu-id="58ffa-148">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="58ffa-149">Créez et configurez une application native Azure AD pour l’authentification de l’utilisateur final auprès d’Azure Data Lake Store à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="58ffa-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="58ffa-150">Pour obtenir des instructions, consultez la page [Créer une application Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="58ffa-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="58ffa-151">Si vous suivez les instructions du lien ci-dessus, veillez à sélectionner le type d’application **Native**, comme l’illustre la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="58ffa-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="58ffa-152">![Créer une application web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Créer une application native")</span><span class="sxs-lookup"><span data-stu-id="58ffa-152">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="58ffa-153">Étape 2 : Obtenir l’ID et l’URI de redirection de l’application</span><span class="sxs-lookup"><span data-stu-id="58ffa-153">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="58ffa-154">Consultez la page [Obtenir l’ID de l’application](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) pour récupérer l’ID de l’application (également appelé l’ID client dans le portail Azure Classic) de l’application native Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58ffa-154">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application id (also called the client ID in the Azure classic portal) of the Azure AD native application.</span></span>

<span data-ttu-id="58ffa-155">Pour récupérer l’URI de redirection, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="58ffa-155">To retrieve the redirect URI, follow the steps below.</span></span>

1. <span data-ttu-id="58ffa-156">Sur le Portail Azure, sélectionnez **Azure Active Directory**, cliquez sur **Inscriptions des applications**, puis recherchez et cliquez sur l’application native Azure AD que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="58ffa-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="58ffa-157">Dans le panneau **Paramètres** de l’application, cliquez sur **URI de redirection**.</span><span class="sxs-lookup"><span data-stu-id="58ffa-157">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![Obtenir un URI de redirection](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="58ffa-159">Copiez la valeur affichée.</span><span class="sxs-lookup"><span data-stu-id="58ffa-159">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="58ffa-160">Étape 3 : Définir des autorisations</span><span class="sxs-lookup"><span data-stu-id="58ffa-160">Step 3: Set permissions</span></span>

1. <span data-ttu-id="58ffa-161">Sur le Portail Azure, sélectionnez **Azure Active Directory**, cliquez sur **Inscriptions des applications**, puis recherchez et cliquez sur l’application native Azure AD que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="58ffa-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="58ffa-162">Dans le panneau **Paramètres** de l’application, cliquez sur **Autorisations requises**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="58ffa-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="58ffa-164">Dans le panneau **Ajouter l’accès des API**, cliquez sur **Sélectionner une API**, puis sur **Azure Data Lake** et enfin sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="58ffa-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="58ffa-166">Dans le panneau **Ajouter l’accès des API**, cliquez sur **Sélectionner des autorisations**, cochez la case pour accorder un **Accès complet à Data Lake Store**, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="58ffa-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="58ffa-168">Cliquez sur **Done**.</span><span class="sxs-lookup"><span data-stu-id="58ffa-168">Click **Done**.</span></span>

5. <span data-ttu-id="58ffa-169">Répétez les deux dernières étapes pour accorder également des autorisations à **l’API Gestion des services Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="58ffa-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="58ffa-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58ffa-170">Next steps</span></span>
<span data-ttu-id="58ffa-171">Dans cet article vous a créé une application native Azure AD et regroupé les informations nécessaires dans les applications clientes que vous créez à l’aide du Kit de développement logiciel (SDK) .NET, du Kit de développement logiciel (SDK) Java, de l’API REST, etc. Vous pouvez à présent passer aux articles suivants qui traitent de l’utilisation de l’application web Azure AD, d’abord pour vous authentifier auprès de Data Lake Store, et ensuite pour effectuer d’autres opérations sur le magasin.</span><span class="sxs-lookup"><span data-stu-id="58ffa-171">In this article you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="58ffa-172">Prise en main d'Azure Data Lake Store avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="58ffa-172">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="58ffa-173">Prise en main d’Azure Data Lake Store à l’aide du Kit de développement logiciel (SDK) Java</span><span class="sxs-lookup"><span data-stu-id="58ffa-173">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="58ffa-174">Prise en main d’Azure Data Lake Store à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="58ffa-174">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

