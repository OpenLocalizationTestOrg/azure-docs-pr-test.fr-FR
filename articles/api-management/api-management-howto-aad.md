---
title: "comptes de développeur aaaAuthorize à l’aide d’Azure Active Directory - gestion des API Azure | Documents Microsoft"
description: "Découvrez comment les utilisateurs de tooauthorize à l’aide d’Azure Active Directory dans la gestion des API."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="daf5f-103">Comment les développeurs tooauthorize comptes à l’aide Azure Active Directory dans la gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="daf5f-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="daf5f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="daf5f-104">Overview</span></span>
<span data-ttu-id="daf5f-105">Ce guide vous explique comment tooenable accéder au portail des développeurs toohello pour les utilisateurs d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="daf5f-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="daf5f-106">Ce guide vous montre également comment toomanage des groupes d’utilisateurs d’Azure Active Directory en ajoutant des groupes externes qui contiennent hello utilisateurs d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="daf5f-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="daf5f-107">les étapes toocomplete hello dans ce guide vous devez avoir un annuaire Azure Active Directory dans le toocreate une application.</span><span class="sxs-lookup"><span data-stu-id="daf5f-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="daf5f-108">Comment les développeurs tooauthorize comptes à l’aide Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="daf5f-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="daf5f-109">tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="daf5f-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="daf5f-110">Cela vous prend un portail de publication de gestion des API toohello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-110">This takes you toohello API Management publisher portal.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="daf5f-112">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="daf5f-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="daf5f-113">Cliquez sur **sécurité** de hello **gestion des API** menu hello gauche et cliquez sur **les identités externes**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![Identités externes][api-management-security-external-identities]

<span data-ttu-id="daf5f-115">Cliquez sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="daf5f-116">Prenez note de hello **URL de redirection** et basculer tooyour Azure Active Directory Bonjour portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="daf5f-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![Identités externes][api-management-security-aad-new]

<span data-ttu-id="daf5f-118">Cliquez sur hello **ajouter** bouton toocreate une application Azure Active Directory, puis choisissez **ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Ajouter de nouvelles applications Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="daf5f-120">Entrez un nom pour l’application hello, sélectionnez **Web application et/ou API Web**, puis cliquez sur le bouton suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![Nouvelle application Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="daf5f-122">Pour **URL de connexion**, entrez hello l’authentification sur l’URL de votre portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="daf5f-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="daf5f-123">Dans cet exemple, hello **URL de connexion** est `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="daf5f-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="daf5f-124">Pourquoi **URL ID d’application**, entrez le domaine par défaut de hello ou un domaine personnalisé pour hello Azure Active Directory et ajouter un tooit de chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="daf5f-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="daf5f-125">Dans cet exemple, hello domaine par défaut de **https://contoso5api.onmicrosoft.com** est utilisé avec le suffixe hello **/API** spécifié.</span><span class="sxs-lookup"><span data-stu-id="daf5f-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![Propriétés de la nouvelle application Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="daf5f-127">Cliquez sur toosave de bouton de vérification hello et créer l’application hello basculer toohello **configurer** onglet nouvelle application de tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![Nouvelle application Azure Active Directory créée][api-management-new-aad-app-created]

<span data-ttu-id="daf5f-129">Si plusieurs annuaires Azure Active Directory vont toobe utilisée pour cette application, cliquez sur **Oui** pour **Application est mutualisée**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="daf5f-130">valeur par défaut Hello est **non**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-130">hello default is **No**.</span></span>

![Application mutualisée][api-management-aad-app-multi-tenant]

<span data-ttu-id="daf5f-132">Hello de copie **URL de redirection** de hello **Azure Active Directory** section Hello **les identités externes** onglet dans le portail de publication hello et collez-le dans hello **URL de réponse** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="daf5f-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![URL de réponse][api-management-aad-reply-url]

<span data-ttu-id="daf5f-134">Défiler vers le bas de hello toohello configurer onglet, sélectionnez hello **autorisations d’Application** liste déroulante, puis vérifiez **lire les données d’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Autorisations de l’application][api-management-aad-app-permissions]

<span data-ttu-id="daf5f-136">Sélectionnez hello **déléguer des autorisations** liste déroulante, puis vérifiez **activer l’authentification et de lire les profils utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Autorisations déléguées][api-management-aad-delegated-permissions]

> <span data-ttu-id="daf5f-138">Pour plus d’informations sur l’application et des autorisations déléguées, consultez [hello d’accès à l’API Graph][Accessing hello Graph API].</span><span class="sxs-lookup"><span data-stu-id="daf5f-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="daf5f-139">Hello de copie **Id Client** toohello Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="daf5f-139">Copy hello **Client Id** toohello clipboard.</span></span>

![ID de client][api-management-aad-app-client-id]

<span data-ttu-id="daf5f-141">Basculer le portail de publication toohello différé et la coller dans hello **Id Client** copiés à partir de la configuration de l’application hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="daf5f-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![ID de client][api-management-client-id]

<span data-ttu-id="daf5f-143">Configuration d’Azure Active Directory toohello arrière du commutateur, puis cliquez sur hello **sélectionner une durée** déroulante Bonjour **clés** section et spécifiez un intervalle.</span><span class="sxs-lookup"><span data-stu-id="daf5f-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="daf5f-144">Dans cet exemple, la valeur **1 an** est utilisée.</span><span class="sxs-lookup"><span data-stu-id="daf5f-144">In this example, **1 year** is used.</span></span>

![Clé][api-management-aad-key-before-save]

<span data-ttu-id="daf5f-146">Cliquez sur **enregistrer** clé hello toosave hello configuration et l’affichage.</span><span class="sxs-lookup"><span data-stu-id="daf5f-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="daf5f-147">Copier le Presse-papiers toohello clé hello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="daf5f-148">Notez sa valeur.</span><span class="sxs-lookup"><span data-stu-id="daf5f-148">Make a note of this key.</span></span> <span data-ttu-id="daf5f-149">Une fois que vous fermez la fenêtre de configuration d’Azure Active Directory hello, clé de hello Impossible d’afficher à nouveau.</span><span class="sxs-lookup"><span data-stu-id="daf5f-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![Clé][api-management-aad-key-after-save]

<span data-ttu-id="daf5f-151">Commutateur toohello précédent portal et la coller hello clé publisher dans hello **clé secrète Client** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="daf5f-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![Clé secrète client][api-management-client-secret]

<span data-ttu-id="daf5f-153">**Autorisé locataires** spécifie les répertoires qui ont accès toohello API d’instance de service de gestion des API hello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="daf5f-154">Spécifier les domaines hello Hello toowhich d’instances Azure Active Directory vous souhaitez toogrant accéder.</span><span class="sxs-lookup"><span data-stu-id="daf5f-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="daf5f-155">Vous pouvez séparer plusieurs domaines par des sauts de ligne, des espaces ou des virgules.</span><span class="sxs-lookup"><span data-stu-id="daf5f-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Locataires autorisés][api-management-client-allowed-tenants]


<span data-ttu-id="daf5f-157">Une fois hello souhaitée de configuration est spécifiée, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-157">Once hello desired configuration is specified, click **Save**.</span></span>

![Enregistrer][api-management-client-allowed-tenants-save]

<span data-ttu-id="daf5f-159">Une fois que l’enregistrement des modifications de hello, les utilisateurs de hello Bonjour spécifiés Azure Active Directory peuvent se connecter dans le portail des développeurs toohello en suivant les étapes de hello dans [connectez-vous au portail des développeurs toohello à l’aide d’un compte Azure Active Directory] [Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="daf5f-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="daf5f-160">Plusieurs domaines peuvent être spécifiés dans hello **autorisé de locataires** section.</span><span class="sxs-lookup"><span data-stu-id="daf5f-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="daf5f-161">Avant de n’importe quel utilisateur peut se connecter à partir d’un autre domaine que hello d’origine où l’application hello a été enregistrée, un administrateur global de domaine différent de hello doit autoriser pour hello application tooaccess données d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="daf5f-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="daf5f-162">autorisation de toogrant, administrateur global de hello doit devenir trop`https://<URL of your developer portal>/aadadminconsent` (par exemple, https://contoso.portal.azure-api.net/aadadminconsent), type de nom de domaine hello Hello client Active Directory qu’ils souhaitent toogive accès tooand, cliquez sur Envoyer.</span><span class="sxs-lookup"><span data-stu-id="daf5f-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="daf5f-163">Suivant de hello exemple, un administrateur global de `miaoaad.onmicrosoft.com` tente de portail de développement particulier toothis toogive autorisation.</span><span class="sxs-lookup"><span data-stu-id="daf5f-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![Autorisations][api-management-aad-consent]

<span data-ttu-id="daf5f-165">Dans l’écran suivant de hello, administrateur global de hello sera invité à tooconfirm hello si vous autorisez.</span><span class="sxs-lookup"><span data-stu-id="daf5f-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![Autorisations][api-management-permissions-form]

> <span data-ttu-id="daf5f-167">Si un administrateur non global tente toolog dans avant les autorisations sont accordées par un administrateur global, tentative de connexion hello échoue et un écran d’erreur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="daf5f-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="daf5f-168">Comment tooadd groupe externe Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="daf5f-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="daf5f-169">Après l’activation de l’accès pour les utilisateurs dans Azure Active Directory, vous pouvez ajouter les groupes Azure Active Directory dans la gestion des API toomore gérer facilement l’association hello de hello les développeurs hello groupe avec les produits hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="daf5f-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="daf5f-170">tooconfigure un groupe Azure Active Directory externe, hello Azure Active Directory doit d’abord être configuré dans l’onglet d’identités hello en suivant la procédure hello dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="daf5f-171">Les groupes Azure Active Directory externes sont ajoutés à partir de hello **visibilité** onglet du produit hello pour laquelle vous souhaitez au groupe toohello toogrant accès.</span><span class="sxs-lookup"><span data-stu-id="daf5f-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="daf5f-172">Cliquez sur **produits**, puis cliquez sur nom hello de produit de votre choix hello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="daf5f-174">Commutateur toohello **visibilité** onglet, puis cliquez sur **ajouter des groupes à partir d’Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Ajouter des groupes][api-management-add-groups]

<span data-ttu-id="daf5f-176">Sélectionnez hello **client Azure Active Directory** de liste de déroulante hello, puis hello nom de type groupe hello Bonjour **groupes** toobe ajouté la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="daf5f-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![Sélectionner un groupe][api-management-select-group]

<span data-ttu-id="daf5f-178">Ce nom de groupe se trouvent dans hello **groupes** liste pour Azure Active Directory, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="daf5f-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Liste des groupes Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="daf5f-180">Cliquez sur **ajouter** toovalidate hello nom du groupe et ajouter un groupe hello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="daf5f-181">Dans cet exemple, hello **les développeurs de Contoso 5** groupe externe est ajouté.</span><span class="sxs-lookup"><span data-stu-id="daf5f-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![Group added][api-management-aad-group-added]

<span data-ttu-id="daf5f-183">Cliquez sur **enregistrer** toosave hello nouvelle sélection de groupe.</span><span class="sxs-lookup"><span data-stu-id="daf5f-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="daf5f-184">Une fois qu’un groupe Azure Active Directory a été configuré à partir d’un produit, il est disponible toobe vérifiée sur hello **visibilité** onglet hello autres produits dans l’instance de service de gestion des API hello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="daf5f-185">tooreview et configurer les propriétés de hello pour les groupes externes une fois qu’ils ont été ajoutés, cliquez sur nom hello du groupe hello de hello **groupes** onglet.</span><span class="sxs-lookup"><span data-stu-id="daf5f-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![Gérer les groupes][api-management-groups]

<span data-ttu-id="daf5f-187">À partir d’ici, vous pouvez modifier hello **nom** et hello **Description** du groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="daf5f-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![Modifier un groupe][api-management-edit-group]

<span data-ttu-id="daf5f-189">Les utilisateurs de hello configuré Azure Active Directory peuvent se connecter en mode et le portail des développeurs toohello et d’abonnement tooany les groupes pour lesquels ils disposent de visibilité en suivant les instructions de hello Bonjour suivant la section.</span><span class="sxs-lookup"><span data-stu-id="daf5f-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="daf5f-190">Comment toolog dans le portail des développeurs toohello à l’aide d’un compte Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="daf5f-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="daf5f-191">toolog portail des développeurs hello à l’aide d’un compte Azure Active Directory configuré dans les sections précédentes hello, ouvrez une nouvelle fenêtre de navigateur à l’aide de hello **URL de connexion** à partir de la configuration de l’application hello Active Directory, puis cliquez sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portail des développeurs][api-management-dev-portal-signin]

<span data-ttu-id="daf5f-193">Entrez les informations d’identification hello de l’un des utilisateurs de hello dans Azure Active Directory, puis cliquez sur **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![de connexion][api-management-aad-signin]

<span data-ttu-id="daf5f-195">Un formulaire d’inscription peut vous être présenté si certaines informations supplémentaires sont requises.</span><span class="sxs-lookup"><span data-stu-id="daf5f-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="daf5f-196">Complétez le formulaire d’inscription de hello et cliquez sur **inscrire**.</span><span class="sxs-lookup"><span data-stu-id="daf5f-196">Complete hello registration form and click **Sign up**.</span></span>

![Inscription][api-management-complete-registration]

<span data-ttu-id="daf5f-198">Votre utilisateur est maintenant connecté dans le portail des développeurs hello pour votre instance de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="daf5f-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

![Inscription terminée][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

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
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

