---
title: "comptes de développeur aaaAuthorize à l’aide d’OAuth 2.0 dans Gestion des API Azure | Documents Microsoft"
description: "Découvrez comment les utilisateurs de tooauthorize à l’aide d’OAuth 2.0 dans Gestion des API."
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
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="674ed-103">Comment les développeurs tooauthorize comptes à l’aide OAuth 2.0 dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="674ed-103">How tooauthorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="674ed-104">Prend en charge de nombreuses API [OAuth 2.0](http://oauth.net/2/) toosecure hello API et garantir que seuls les utilisateurs autorisés ont accès, et ils peuvent accéder uniquement aux ressources toowhich auxquelles ils ont droit.</span><span class="sxs-lookup"><span data-stu-id="674ed-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) toosecure hello API and ensure that only valid users have access, and they can only access resources toowhich they're entitled.</span></span> <span data-ttu-id="674ed-105">Dans interactive Console de commande toouse Azure API Management de développement avec ces API, hello service vous permet de tooconfigure votre toowork d’instance de service avec votre OAuth 2.0 activé API.</span><span class="sxs-lookup"><span data-stu-id="674ed-105">In order toouse Azure API Management's interactive Developer Console with such APIs, hello service allows you tooconfigure your service instance toowork with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="674ed-106"><a name="prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="674ed-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="674ed-107">Ce guide vous montre comment tooconfigure votre toouse instance du service Gestion des API d’autorisation d’OAuth 2.0 pour développeur comptes, mais ne pas vous montre comment le fournisseur de tooconfigure un OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="674ed-107">This guide shows you how tooconfigure your API Management service instance toouse OAuth 2.0 authorization for developer accounts, but does not show you how tooconfigure an OAuth 2.0 provider.</span></span> <span data-ttu-id="674ed-108">configuration de Hello pour chaque fournisseur est différent, même si hello étapes sont semblables, et nombre hello requis d’informations de configuration d’OAuth 2.0 dans votre instance de service de gestion des API de OAuth 2.0 hello identiques.</span><span class="sxs-lookup"><span data-stu-id="674ed-108">hello configuration for each OAuth 2.0 provider is different, although hello steps are similar, and hello required pieces of information used in configuring OAuth 2.0 in your API Management service instance are hello same.</span></span> <span data-ttu-id="674ed-109">Cette rubrique inclut des exemples d'utilisation de Azure Active Directory en tant que fournisseur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="674ed-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="674ed-110">Pour plus d’informations sur la configuration d’OAuth 2.0 à l’aide d’Azure Active Directory, consultez hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] exemple.</span><span class="sxs-lookup"><span data-stu-id="674ed-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see hello [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="674ed-111"><a name="step1"></a>Configuration du serveur d’autorisation OAuth 2.0 dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="674ed-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="674ed-112">tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="674ed-112">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="674ed-114">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="674ed-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="674ed-115">Cliquez sur **sécurité** de hello **gestion des API** menu de gauche, cliquez sur à hello **OAuth 2.0**, puis cliquez sur **ajouter un serveur d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="674ed-115">Click **Security** from hello **API Management** menu on hello left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="674ed-117">Après avoir cliqué sur **ajouter un serveur d’autorisation**, nouveau formulaire de serveur d’autorisation hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="674ed-117">After clicking **Add authorization server**, hello new authorization server form is displayed.</span></span>

![Nouveau serveur][api-management-oauth2-server-1]

<span data-ttu-id="674ed-119">Entrez un nom et une description facultative dans hello **nom** et **Description** champs.</span><span class="sxs-lookup"><span data-stu-id="674ed-119">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="674ed-120">Ces champs sont le serveur de d’autorisation hello OAuth 2.0 tooidentify utilisés au sein de l’instance de service de gestion des API actuelle hello et leurs valeurs ne proviennent pas de serveur de hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="674ed-120">These fields are used tooidentify hello OAuth 2.0 authorization server within hello current API Management service instance and their values do not come from hello OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="674ed-121">Entrez hello **URL de la page d’inscription Client**.</span><span class="sxs-lookup"><span data-stu-id="674ed-121">Enter hello **Client registration page URL**.</span></span> <span data-ttu-id="674ed-122">Cette page est où les utilisateurs peuvent créer et gérer leurs comptes et varie en fonction du fournisseur de hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="674ed-122">This page is where users can create and manage their accounts, and varies depending on hello OAuth 2.0 provider used.</span></span> <span data-ttu-id="674ed-123">Hello **URL de la page d’inscription Client** points toohello page que les utilisateurs peuvent utiliser toocreate et configurer leurs propres comptes pour les fournisseurs OAuth 2.0 qui prennent en charge la gestion des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="674ed-123">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="674ed-124">Certaines organisations ne configurer ou utiliser cette fonctionnalité, même si le fournisseur de hello OAuth 2.0 prend en charge.</span><span class="sxs-lookup"><span data-stu-id="674ed-124">Some organizations do not configure or use this functionality even if hello OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="674ed-125">Si votre fournisseur OAuth 2.0 n’a pas de gestion des utilisateurs de comptes configurés, entrez une URL d’espace réservé en ici, par exemple hello URL de votre société, ou comme `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="674ed-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as hello URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="674ed-126">section suivante de Hello sous forme de hello contient hello **types d’octroi de code d’autorisation**, **URL de point de terminaison d’autorisation**, et **méthode de demande d’autorisation** paramètres.</span><span class="sxs-lookup"><span data-stu-id="674ed-126">hello next section of hello form contains hello **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Nouveau serveur][api-management-oauth2-server-2]

<span data-ttu-id="674ed-128">Spécifiez hello **types d’octroi de code d’autorisation** en vérifiant les types hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="674ed-128">Specify hello **Authorization code grant types** by checking hello desired types.</span></span> <span data-ttu-id="674ed-129">**code d'autorisation** est spécifié par défaut.</span><span class="sxs-lookup"><span data-stu-id="674ed-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="674ed-130">Entrez hello **URL de point de terminaison d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="674ed-130">Enter hello **Authorization endpoint URL**.</span></span> <span data-ttu-id="674ed-131">Pour Azure Active Directory, cette URL sera similaire toohello suivant URL, où `<client_id>` est remplacée par l’id de client hello qui identifie votre serveur d’applications toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="674ed-131">For Azure Active Directory, this URL will be similar toohello following URL, where `<client_id>` is replaced with hello client id that identifies your application toohello OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="674ed-132">Hello **méthode de demande d’autorisation** spécifie comment la demande d’autorisation de hello est envoyée toohello OAuth 2.0 server.</span><span class="sxs-lookup"><span data-stu-id="674ed-132">hello **Authorization request method** specifies how hello authorization request is sent toohello OAuth 2.0 server.</span></span> <span data-ttu-id="674ed-133">Par défaut, la méthode **GET** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="674ed-133">By default **GET** is selected.</span></span>

<span data-ttu-id="674ed-134">la section suivante Hello est où hello **URL de point de terminaison de jeton**, **méthodes d’authentification Client**, **jeton d’accès méthode d’envoi**, et **étenduepardéfaut** sont spécifiés.</span><span class="sxs-lookup"><span data-stu-id="674ed-134">hello next section is where hello **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Nouveau serveur][api-management-oauth2-server-3]

<span data-ttu-id="674ed-136">Pour un serveur Azure Active Directory OAuth 2.0, hello **URL de point de terminaison de jeton** aura hello suivant le format, où `<APPID>` a le format hello de `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="674ed-136">For an Azure Active Directory OAuth 2.0 server, hello **Token endpoint URL** will have hello following format, where `<APPID>`  has hello format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="674ed-137">Hello du paramètre par défaut pour **méthodes d’authentification Client** est **base**, et **jeton d’accès méthode d’envoi** est **l’en-tête d’autorisation**.</span><span class="sxs-lookup"><span data-stu-id="674ed-137">hello default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="674ed-138">Ces valeurs sont configurés sur cette section du formulaire hello, ainsi que de hello **étendue par défaut**.</span><span class="sxs-lookup"><span data-stu-id="674ed-138">These values are configured on this section of hello form, along with hello **Default scope**.</span></span>

<span data-ttu-id="674ed-139">Hello **informations d’identification Client** section contient hello **ID Client** et **clé secrète Client**, qui sont obtenu au cours hello les processus de création et la configuration de votre OAuth 2.0 serveur.</span><span class="sxs-lookup"><span data-stu-id="674ed-139">hello **Client credentials** section contains hello **Client ID** and **Client secret**, which are obtained during hello creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="674ed-140">Une fois hello **ID Client** et **clé secrète Client** sont spécifiés, hello **redirect_uri** pour hello **code d’autorisation** est généré.</span><span class="sxs-lookup"><span data-stu-id="674ed-140">Once hello **Client ID** and **Client secret** are specified, hello **redirect_uri** for hello **authorization code** is generated.</span></span> <span data-ttu-id="674ed-141">Cet URI est l’URL de réponse hello tooconfigure utilisés dans votre configuration de serveur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="674ed-141">This URI is used tooconfigure hello reply URL in your OAuth 2.0 server configuration.</span></span>

![Nouveau serveur][api-management-oauth2-server-4]

<span data-ttu-id="674ed-143">Si **types d’octroi de code d’autorisation** est défini trop**mot de passe de propriétaire de la ressource**, hello **informations d’identification de mot de passe de propriétaire de la ressource** section est toospecify utilisé les informations d’identification ; Sinon, vous pouvez laisser vide.</span><span class="sxs-lookup"><span data-stu-id="674ed-143">If **Authorization code grant types** is set too**Resource owner password**, hello **Resource owner password credentials** section is used toospecify those credentials; otherwise you can leave it blank.</span></span>

![Nouveau serveur][api-management-oauth2-server-5]

<span data-ttu-id="674ed-145">Une fois le formulaire de hello est terminée, cliquez sur **enregistrer** configuration du serveur d’autorisation toosave hello API Management OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="674ed-145">Once hello form is complete, click **Save** toosave hello API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="674ed-146">Une fois la configuration du serveur hello est enregistrée, vous pouvez configurer API toouse cette configuration, comme indiqué dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="674ed-146">Once hello server configuration is saved, you can configure APIs toouse this configuration, as shown in hello next section.</span></span>

## <span data-ttu-id="674ed-147"><a name="step2"></a>Configurer un toouse API autorisation de l’utilisateur OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="674ed-147"><a name="step2"> </a>Configure an API toouse OAuth 2.0 user authorization</span></span>
<span data-ttu-id="674ed-148">Cliquez sur **API** de hello **gestion des API** hello menu gauche, cliquez sur nom hello de hello souhaité API **sécurité**, puis activez case hello pour **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="674ed-148">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, click **Security**, and then check hello box for **OAuth 2.0**.</span></span>

![Autorisation utilisateur][api-management-user-authorization]

<span data-ttu-id="674ed-150">Sélectionnez hello souhaité **serveur d’autorisation** à partir de la liste déroulante de hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="674ed-150">Select hello desired **Authorization server** from hello drop-down list, and click **Save**.</span></span>

![Autorisation utilisateur][api-management-user-authorization-save]

## <span data-ttu-id="674ed-152"><a name="step3"></a>Tester l’autorisation de l’utilisateur hello OAuth 2.0 Bonjour portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="674ed-152"><a name="step3"> </a>Test hello OAuth 2.0 user authorization in hello Developer Portal</span></span>
<span data-ttu-id="674ed-153">Après avoir configuré votre serveur d’autorisation OAuth 2.0 et configuré votre toouse API ce serveur, vous pouvez le tester en accédant toohello portail des développeurs et en appelant une API.</span><span class="sxs-lookup"><span data-stu-id="674ed-153">Once you have configured your OAuth 2.0 authorization server and configured your API toouse that server, you can test it by going toohello Developer Portal and calling an API.</span></span>  <span data-ttu-id="674ed-154">Cliquez sur **portail des développeurs** dans le menu supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="674ed-154">Click **Developer portal** in hello top right menu.</span></span>

![Portail des développeurs][api-management-developer-portal-menu]

<span data-ttu-id="674ed-156">Cliquez sur **API** dans le menu du haut hello et sélectionnez **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="674ed-156">Click **APIs** in hello top menu and select **Echo API**.</span></span>

![API Echo][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="674ed-158">Si vous n'avez qu’une seule API configurée ou tooyour visible compte, puis en cliquant sur API vous amène directement operations toohello pour cette API.</span><span class="sxs-lookup"><span data-stu-id="674ed-158">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="674ed-159">Sélectionnez hello **obtenir une ressource** opération, cliquez sur **ouvrir la Console**, puis sélectionnez **code d’autorisation** dans hello de liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="674ed-159">Select hello **GET Resource** operation, click **Open Console**, and then select **Authorization code** from hello drop-down.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="674ed-161">Lorsque **code d’autorisation** est sélectionnée, une fenêtre contextuelle s’affiche avec hello-formulaire de connexion du fournisseur de hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="674ed-161">When **Authorization code** is selected, a pop-up window is displayed with hello sign-in form of hello OAuth 2.0 provider.</span></span> <span data-ttu-id="674ed-162">Dans cet exemple hello-formulaire de connexion est fournie par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="674ed-162">In this example hello sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="674ed-163">Si vous avez les fenêtres contextuelles désactivée, vous serez invité à entrer tooenable par le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="674ed-163">If you have pop-ups disabled you will be prompted tooenable them by hello browser.</span></span> <span data-ttu-id="674ed-164">Une fois que vous les activez, sélectionnez **code d’autorisation** hello et nouveau formulaire de connexion s’affichera.</span><span class="sxs-lookup"><span data-stu-id="674ed-164">After you enable them, select **Authorization code** again and hello sign-in form will be displayed.</span></span>
> 
> 

![de connexion][api-management-oauth2-signin]

<span data-ttu-id="674ed-166">Une fois que vous êtes connecté, hello **en-têtes de demande** sont renseignées avec une `Authorization : Bearer` en-tête qui autorise la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="674ed-166">Once you have signed in, hello **Request headers** are populated with an `Authorization : Bearer` header that authorizes hello request.</span></span>

![Jeton d'en-tête de demande][api-management-request-header-token]

<span data-ttu-id="674ed-168">À ce stade, vous pouvez configurer les valeurs hello souhaité pour hello restant de paramètres et soumettre la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="674ed-168">At this point you can configure hello desired values for hello remaining parameters, and submit hello request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="674ed-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="674ed-169">Next steps</span></span>
<span data-ttu-id="674ed-170">Pour plus d’informations sur l’utilisation de OAuth 2.0 et gestion des API, voir hello vidéo et d’accompagnement [article](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="674ed-170">For more information about using OAuth 2.0 and API Management, see hello following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

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


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

