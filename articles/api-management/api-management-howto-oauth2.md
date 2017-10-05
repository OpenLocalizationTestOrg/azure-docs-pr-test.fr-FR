---
title: "Autoriser des comptes de développeurs à l’aide d’OAuth 2.0 dans Gestion des API Azure | Microsoft Docs"
description: "Apprenez à autoriser les utilisateurs à l'aide d'OAuth 2.0 dans Gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a19c453bb3271374b587f3d0b35adad55863b490
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-authorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="31982-103">Comment autoriser des comptes de développeurs à l'aide de OAuth 2.0 dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="31982-103">How to authorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="31982-104">De nombreuses API prennent en charge [OAuth 2.0](http://oauth.net/2/) pour sécuriser les API et assurer que seuls les utilisateurs valides y ont accès et peuvent accéder uniquement aux ressources pour lesquelles ils y sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="31982-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) to secure the API and ensure that only valid users have access, and they can only access resources to which they're entitled.</span></span> <span data-ttu-id="31982-105">Pour utiliser la console de développement interactive de Gestion des API Azure avec ces API, le service vous permet de configurer votre instance de service pour travailler avec votre API compatible OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="31982-105">In order to use Azure API Management's interactive Developer Console with such APIs, the service allows you to configure your service instance to work with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="31982-106"><a name="prerequisites"> </a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="31982-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="31982-107">Ce guide explique comment configurer votre instance de service Gestion des API pour utiliser l'autorisation OAuth 2.0 dans des comptes de développeur, mais n'explique pas comment configurer un fournisseur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="31982-107">This guide shows you how to configure your API Management service instance to use OAuth 2.0 authorization for developer accounts, but does not show you how to configure an OAuth 2.0 provider.</span></span> <span data-ttu-id="31982-108">La configuration de chaque fournisseur OAuth 2.0 est différente, bien que la procédure soit similaire et que les informations requises pour configurer OAuth 2.0 dans votre instance de service Gestion des API soient identiques.</span><span class="sxs-lookup"><span data-stu-id="31982-108">The configuration for each OAuth 2.0 provider is different, although the steps are similar, and the required pieces of information used in configuring OAuth 2.0 in your API Management service instance are the same.</span></span> <span data-ttu-id="31982-109">Cette rubrique inclut des exemples d'utilisation de Azure Active Directory en tant que fournisseur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="31982-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="31982-110">Pour plus d’informations sur la configuration d’OAuth 2.0 à l’aide d’Azure Active Directory, consultez l’exemple [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet].</span><span class="sxs-lookup"><span data-stu-id="31982-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see the [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="31982-111"><a name="step1"> </a>Configuration du serveur d’autorisation OAuth 2.0 dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="31982-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="31982-112">Pour commencer, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="31982-112">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="31982-114">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="31982-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="31982-115">Cliquez sur **Sécurité** dans le menu **Gestion des API** de gauche, cliquez sur **OAuth 2.0**, puis sur **Ajouter au serveur d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="31982-115">Click **Security** from the **API Management** menu on the left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="31982-117">Après avoir cliqué sur **Ajouter au serveur d'autorisation**, le formulaire de nouveau serveur d'autorisation s'affiche.</span><span class="sxs-lookup"><span data-stu-id="31982-117">After clicking **Add authorization server**, the new authorization server form is displayed.</span></span>

![Nouveau serveur][api-management-oauth2-server-1]

<span data-ttu-id="31982-119">Entrez un nom et une description facultative dans les champs **Nom** et **Description**.</span><span class="sxs-lookup"><span data-stu-id="31982-119">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="31982-120">Ces champs sont utilisés pour identifier le serveur d'autorisation OAuth 2.0 dans l'instance de service Gestion des API actuelle, et leurs valeurs ne proviennent pas du serveur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="31982-120">These fields are used to identify the OAuth 2.0 authorization server within the current API Management service instance and their values do not come from the OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="31982-121">Entrez l' **URL de la page d'enregistrement client**.</span><span class="sxs-lookup"><span data-stu-id="31982-121">Enter the **Client registration page URL**.</span></span> <span data-ttu-id="31982-122">Cette page est l'endroit où les utilisateurs créent et gèrent leurs comptes ; elle varie en fonction du fournisseur OAuth 2.0 utilisé.</span><span class="sxs-lookup"><span data-stu-id="31982-122">This page is where users can create and manage their accounts, and varies depending on the OAuth 2.0 provider used.</span></span> <span data-ttu-id="31982-123">L’ **URL de la page d’enregistrement client** pointe vers la page que les utilisateurs peuvent utiliser pour créer et configurer leurs propres comptes pour les fournisseurs OAuth 2.0 qui prennent en charge la gestion des comptes utilisateur.</span><span class="sxs-lookup"><span data-stu-id="31982-123">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="31982-124">Certaines organisations ne configurent pas cette fonctionnalité ou ne l’utilisent pas, même si le fournisseur OAuth 2.0 la prend en charge.</span><span class="sxs-lookup"><span data-stu-id="31982-124">Some organizations do not configure or use this functionality even if the OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="31982-125">Si la gestion des utilisateurs de comptes de votre fournisseur OAuth 2.0 n’a pas été configurée, entrez un espace réservé d’URL ici, par exemple l’URL de votre société ou une URL comme `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="31982-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as the URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="31982-126">La section suivante du formulaire inclut les paramètres **Types d’accès accordé aux codes d’autorisation**, **URL de point de terminaison d’autorisation** et **Méthode de demande d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="31982-126">The next section of the form contains the **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Nouveau serveur][api-management-oauth2-server-2]

<span data-ttu-id="31982-128">Spécifiez le paramètre **Types d'accès accordé aux codes d'autorisation** en sélectionnant les types souhaités.</span><span class="sxs-lookup"><span data-stu-id="31982-128">Specify the **Authorization code grant types** by checking the desired types.</span></span> <span data-ttu-id="31982-129">**code d'autorisation** est spécifié par défaut.</span><span class="sxs-lookup"><span data-stu-id="31982-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="31982-130">Entrez l' **URL de point de terminaison d'autorisation**.</span><span class="sxs-lookup"><span data-stu-id="31982-130">Enter the **Authorization endpoint URL**.</span></span> <span data-ttu-id="31982-131">Pour Azure Active Directory, cette URL est similaire à l’URL suivante, où `<client_id>` est remplacé par l’ID client qui identifie votre application sur le serveur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="31982-131">For Azure Active Directory, this URL will be similar to the following URL, where `<client_id>` is replaced with the client id that identifies your application to the OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="31982-132">La **Méthode de demande d’autorisation** spécifie comment la demande d'autorisation est envoyée au serveur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="31982-132">The **Authorization request method** specifies how the authorization request is sent to the OAuth 2.0 server.</span></span> <span data-ttu-id="31982-133">Par défaut, la méthode **GET** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="31982-133">By default **GET** is selected.</span></span>

<span data-ttu-id="31982-134">La section suivante permet de spécifier les paramètres **URL de point de terminaison de jeton**, **Méthodes d’authentification du client**, **Méthode d’envoi des jetons d’accès** et **Étendue par défaut**.</span><span class="sxs-lookup"><span data-stu-id="31982-134">The next section is where the **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Nouveau serveur][api-management-oauth2-server-3]

<span data-ttu-id="31982-136">Pour un serveur OAuth 2.0 Azure Active Directory, l’**URL de point de terminaison de jeton** a le format suivant, où `<APPID>` a le format `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="31982-136">For an Azure Active Directory OAuth 2.0 server, the **Token endpoint URL** will have the following format, where `<APPID>`  has the format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="31982-137">Le paramètre par défaut pour **Méthodes d’authentification du client** est **De base**, et le paramètre par défaut pour **Méthode d’envoi des jetons d’accès** est **En-tête d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="31982-137">The default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="31982-138">Ces valeurs sont configurées dans cette section du formulaire, ainsi que le paramètre **Étendue par défaut**.</span><span class="sxs-lookup"><span data-stu-id="31982-138">These values are configured on this section of the form, along with the **Default scope**.</span></span>

<span data-ttu-id="31982-139">La section **Informations d’identification du client** inclut les paramètres **ID client** et **Clé secrète client**, qui sont obtenus lors du processus de création et de configuration de votre serveur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="31982-139">The **Client credentials** section contains the **Client ID** and **Client secret**, which are obtained during the creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="31982-140">Une fois que les paramètres **ID client** et **Clé secrète client** ont été spécifiés, le **redirect_uri** pour le **code d’autorisation** est généré.</span><span class="sxs-lookup"><span data-stu-id="31982-140">Once the **Client ID** and **Client secret** are specified, the **redirect_uri** for the **authorization code** is generated.</span></span> <span data-ttu-id="31982-141">Cette URI est utilisée pour configurer l'URL de réponse dans la configuration de votre serveur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="31982-141">This URI is used to configure the reply URL in your OAuth 2.0 server configuration.</span></span>

![Nouveau serveur][api-management-oauth2-server-4]

<span data-ttu-id="31982-143">Si le paramètre **Types d’accès accordés aux codes d’autorisation** est défini sur **Mot de passe du propriétaire des ressources**, la section **Informations d’identification du mot de passe du propriétaire des ressources** permet de spécifier ces informations d’identification ; sinon, vous pouvez la laisser vide.</span><span class="sxs-lookup"><span data-stu-id="31982-143">If **Authorization code grant types** is set to **Resource owner password**, the **Resource owner password credentials** section is used to specify those credentials; otherwise you can leave it blank.</span></span>

![Nouveau serveur][api-management-oauth2-server-5]

<span data-ttu-id="31982-145">Une fois le formulaire complété, cliquez sur **Enregistrer** pour enregistrer la configuration du serveur d'autorisation OAuth 2.0 de Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="31982-145">Once the form is complete, click **Save** to save the API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="31982-146">Après l'enregistrement de la configuration du serveur, vous pouvez configurer les API pour utiliser cette configuration, tel qu'expliqué dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="31982-146">Once the server configuration is saved, you can configure APIs to use this configuration, as shown in the next section.</span></span>

## <span data-ttu-id="31982-147"><a name="step2"> </a>Configuration d’une API pour utiliser l’autorisation utilisateur OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="31982-147"><a name="step2"> </a>Configure an API to use OAuth 2.0 user authorization</span></span>
<span data-ttu-id="31982-148">Cliquez sur **API** dans le menu **Gestion des API** de gauche, cliquez sur le nom de l’API désirée, cliquez sur l’onglet **Sécurité**, puis cochez la case **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="31982-148">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, click **Security**, and then check the box for **OAuth 2.0**.</span></span>

![Autorisation utilisateur][api-management-user-authorization]

<span data-ttu-id="31982-150">Sélectionnez le **Serveur d’autorisation** souhaité dans la liste déroulante, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="31982-150">Select the desired **Authorization server** from the drop-down list, and click **Save**.</span></span>

![Autorisation utilisateur][api-management-user-authorization-save]

## <span data-ttu-id="31982-152"><a name="step3"> </a>Tests de l’autorisation utilisateur OAuth 2.0 dans le portail de développement</span><span class="sxs-lookup"><span data-stu-id="31982-152"><a name="step3"> </a>Test the OAuth 2.0 user authorization in the Developer Portal</span></span>
<span data-ttu-id="31982-153">Une fois que vous avez configuré votre serveur d'autorisation OAuth 2.0 et votre API pour utiliser ce serveur, vous pouvez le tester en accédant au portail de développement et en appelant une API.</span><span class="sxs-lookup"><span data-stu-id="31982-153">Once you have configured your OAuth 2.0 authorization server and configured your API to use that server, you can test it by going to the Developer Portal and calling an API.</span></span>  <span data-ttu-id="31982-154">Cliquez sur **Portail de développement** dans le menu supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="31982-154">Click **Developer portal** in the top right menu.</span></span>

![Portail des développeurs][api-management-developer-portal-menu]

<span data-ttu-id="31982-156">Cliquez sur **API** dans le menu supérieur et sélectionnez **API Echo**.</span><span class="sxs-lookup"><span data-stu-id="31982-156">Click **APIs** in the top menu and select **Echo API**.</span></span>

![API Echo][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="31982-158">Si vous n'avez qu'une API configurée ou visible dans votre compte, cliquez sur des API pour accéder directement aux opérations associées.</span><span class="sxs-lookup"><span data-stu-id="31982-158">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="31982-159">Sélectionnez l’opération **Ressource GET**, cliquez sur **Ouvrir la console**, puis sélectionnez **Code d’autorisation** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="31982-159">Select the **GET Resource** operation, click **Open Console**, and then select **Authorization code** from the drop-down.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="31982-161">Lorsque **Code d'autorisation** est sélectionné, une fenêtre contextuelle s'affiche, avec le formulaire d'inscription du fournisseur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="31982-161">When **Authorization code** is selected, a pop-up window is displayed with the sign-in form of the OAuth 2.0 provider.</span></span> <span data-ttu-id="31982-162">Dans cet exemple, le formulaire d'inscription est fourni par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31982-162">In this example the sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="31982-163">Si l'utilisation des fenêtres contextuelles est désactivée, vous êtes invité à l'activer par le navigateur.</span><span class="sxs-lookup"><span data-stu-id="31982-163">If you have pop-ups disabled you will be prompted to enable them by the browser.</span></span> <span data-ttu-id="31982-164">Après l'activation, sélectionnez à nouveau **Code d'autorisation** , et le formulaire d'inscription s'affiche.</span><span class="sxs-lookup"><span data-stu-id="31982-164">After you enable them, select **Authorization code** again and the sign-in form will be displayed.</span></span>
> 
> 

![de connexion][api-management-oauth2-signin]

<span data-ttu-id="31982-166">Une fois que vous êtes connecté, les **En-têtes de demandes`Authorization : Bearer` sont renseignés avec un en-tête** qui autorise la demande.</span><span class="sxs-lookup"><span data-stu-id="31982-166">Once you have signed in, the **Request headers** are populated with an `Authorization : Bearer` header that authorizes the request.</span></span>

![Jeton d'en-tête de demande][api-management-request-header-token]

<span data-ttu-id="31982-168">À présent, vous pouvez configurer les valeurs souhaitées pour les paramètres restants, puis soumettre la demande.</span><span class="sxs-lookup"><span data-stu-id="31982-168">At this point you can configure the desired values for the remaining parameters, and submit the request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="31982-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31982-169">Next steps</span></span>
<span data-ttu-id="31982-170">Pour plus d’informations sur l’utilisation d’OAuth 2.0 et la gestion des API, regardez la vidéo suivante et l’article qui l’ [accompagne](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="31982-170">For more information about using OAuth 2.0 and API Management, see the following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

