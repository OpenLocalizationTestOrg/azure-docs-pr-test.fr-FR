---
title: aaaAzure Active Directory B2C | Documents Microsoft
description: "Comment toobuild une application web avec connexion-haut/connectez-vous, Profiler, de modification et mot de passe réinitialisé à l’aide d’Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="5e599-103">Créer une application web ASP.NET avec inscription, connexion, modification du profil et réinitialisation du mot de passe Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="5e599-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="5e599-104">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="5e599-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e599-105">Ajouter une application web de Azure AD B2C identité fonctionnalités tooyour</span><span class="sxs-lookup"><span data-stu-id="5e599-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="5e599-106">Inscrire votre application web auprès de votre répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="5e599-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="5e599-107">Créer une stratégie d’inscription/de connexion d’utilisateur, de modification du profil et de réinitialisation du mot de passe pour votre application web</span><span class="sxs-lookup"><span data-stu-id="5e599-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e599-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5e599-108">Prerequisites</span></span>

- <span data-ttu-id="5e599-109">Vous devez connecter votre tooan B2C locataire compte Azure.</span><span class="sxs-lookup"><span data-stu-id="5e599-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="5e599-110">Vous pouvez créer un compte Azure gratuit [ici](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="5e599-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="5e599-111">Vous devez [Microsoft Visual Studio](https://www.visualstudio.com/) ou un programme tooview et modifier l’exemple de code hello similaires.</span><span class="sxs-lookup"><span data-stu-id="5e599-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="5e599-112">Créer un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="5e599-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="5e599-113">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="5e599-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="5e599-114">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes et autres.</span><span class="sxs-lookup"><span data-stu-id="5e599-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="5e599-115">Si vous n’en possédez pas déjà un, créez un répertoire B2C avant d’aller plus loin dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="5e599-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="5e599-116">Vous devez tooconnect hello B2C locataire tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5e599-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="5e599-117">Après avoir sélectionné **créer**, sélectionnez hello **lien un B2C d’AD Azure existant locataire toomy abonnement Azure** option, puis dans hello **locataire d’Azure AD B2C** liste déroulante, sélectionnez client Hello souhaité tooassociate.</span><span class="sxs-lookup"><span data-stu-id="5e599-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="5e599-118">Créer et inscrire une application</span><span class="sxs-lookup"><span data-stu-id="5e599-118">Create and register an application</span></span>

<span data-ttu-id="5e599-119">Ensuite, vous devez toocreate et inscrivez l’application hello dans votre répertoire B2C.</span><span class="sxs-lookup"><span data-stu-id="5e599-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="5e599-120">Fournit des informations qu’Azure AD B2C doit toosecurely communiquer avec votre application.</span><span class="sxs-lookup"><span data-stu-id="5e599-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="5e599-121">Lorsque vous avez terminé, vous aurez une API et une application native dans vos paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="5e599-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="5e599-122">Créer des stratégies dans votre locataire B2C</span><span class="sxs-lookup"><span data-stu-id="5e599-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="5e599-123">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5e599-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5e599-124">Cet exemple de code contient trois expériences liées à l’identité : **l’inscription et la connexion**, la **modification du profil** et la **réinitialisation du mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5e599-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="5e599-125">Vous devez toocreate une stratégie de chaque type, comme décrit dans hello [article de référence de stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5e599-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5e599-126">Pour chaque stratégie, être toocopy nom hello de votre stratégie pour une utilisation ultérieure ou revendication et attribut de nom d’affichage tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="5e599-127">Ajouter vos fournisseurs d’identité</span><span class="sxs-lookup"><span data-stu-id="5e599-127">Add your identity providers</span></span>

<span data-ttu-id="5e599-128">À partir de vos paramètres, sélectionnez **Fournisseurs d’identité** et choisissez Abonnement par nom d’utilisateur ou Abonnement par e-mail.</span><span class="sxs-lookup"><span data-stu-id="5e599-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="5e599-129">Créer une stratégie d’inscription et de connexion</span><span class="sxs-lookup"><span data-stu-id="5e599-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="5e599-130">Création d’une stratégie de modification de profil</span><span class="sxs-lookup"><span data-stu-id="5e599-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="5e599-131">Création d’une stratégie de réinitialisation du mot de passe</span><span class="sxs-lookup"><span data-stu-id="5e599-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="5e599-132">Après avoir créé vos stratégies, vous êtes prêt toobuild votre application.</span><span class="sxs-lookup"><span data-stu-id="5e599-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="5e599-133">Télécharger l’exemple de code hello</span><span class="sxs-lookup"><span data-stu-id="5e599-133">Download hello sample code</span></span>

<span data-ttu-id="5e599-134">code Hello pour ce didacticiel est conservée sur [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="5e599-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="5e599-135">Vous pouvez cloner l’exemple hello en exécutant :</span><span class="sxs-lookup"><span data-stu-id="5e599-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="5e599-136">Après avoir téléchargé l’exemple de code hello, ouvrez hello tooget du fichier .sln de Visual Studio a démarré.</span><span class="sxs-lookup"><span data-stu-id="5e599-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="5e599-137">fichier de solution Hello contient deux projets : `TaskWebApp` et `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="5e599-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="5e599-138">`TaskWebApp`est hello application web MVC hello utilisateur interagit avec.</span><span class="sxs-lookup"><span data-stu-id="5e599-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="5e599-139">`TaskService`est web principal API de l’application hello qui stocke la liste des actions de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5e599-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="5e599-140">Cet article traite uniquement hello `TaskWebApp` application.</span><span class="sxs-lookup"><span data-stu-id="5e599-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="5e599-141">toolearn comment toobuild `TaskService` à l’aide d’Azure AD B2C, consultez [notre didacticiel de l’api web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5e599-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="5e599-142">Mettre à jour du code toouse votre locataire et les stratégies</span><span class="sxs-lookup"><span data-stu-id="5e599-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="5e599-143">Notre exemple est configuré toouse hello stratégies et ID de client de notre client de démonstration.</span><span class="sxs-lookup"><span data-stu-id="5e599-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="5e599-144">tooconnect il tooyour de locataire propre, vous devez tooopen `web.config` Bonjour `TaskWebApp` de projet et remplacez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="5e599-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="5e599-145">`ida:Tenant` par le nom de votre locataire</span><span class="sxs-lookup"><span data-stu-id="5e599-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="5e599-146">`ida:ClientId` par votre ID d’application web</span><span class="sxs-lookup"><span data-stu-id="5e599-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="5e599-147">`ida:ClientSecret` par votre clé secrète d’application web</span><span class="sxs-lookup"><span data-stu-id="5e599-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="5e599-148">`ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion</span><span class="sxs-lookup"><span data-stu-id="5e599-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="5e599-149">`ida:EditProfilePolicyId` par votre nom de stratégie « Modifier le profil »</span><span class="sxs-lookup"><span data-stu-id="5e599-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="5e599-150">`ida:ResetPasswordPolicyId` par votre nom de stratégie « Réinitialiser le mot de passe »</span><span class="sxs-lookup"><span data-stu-id="5e599-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="5e599-151">Lancer l’application hello</span><span class="sxs-lookup"><span data-stu-id="5e599-151">Launch hello app</span></span>
<span data-ttu-id="5e599-152">À partir de Visual Studio, lancez application hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="5e599-153">Accédez onglet de liste de tâches toohello et hello Remarque URl est : https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="5e599-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="5e599-154">Inscrivez-vous pour une application hello à l’aide de votre nom d’utilisateur ou une adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="5e599-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="5e599-155">Déconnectez-vous, puis reconnectez-vous et modifier le profil de hello ou réinitialiser le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="5e599-156">Déconnectez-vous et connectez-vous en tant qu’autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5e599-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="5e599-157">Ajout d’IDP sociaux</span><span class="sxs-lookup"><span data-stu-id="5e599-157">Add social IDPs</span></span>

<span data-ttu-id="5e599-158">Actuellement, application hello prend en charge uniquement les utilisateurs d’abonnement et de connexion à l’aide de **comptes locaux**; les comptes stockés dans votre répertoire B2C qui utilisent un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5e599-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="5e599-159">Avec Azure AD B2C, vous pouvez ajouter la prise en charge d’autres **fournisseurs d’identité** sans modifier votre code.</span><span class="sxs-lookup"><span data-stu-id="5e599-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="5e599-160">tooadd sociaux IDPs tooyour application, commencez par suivre hello des instructions dans ces articles.</span><span class="sxs-lookup"><span data-stu-id="5e599-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="5e599-161">Pour chaque IDP vous toosupport, vous devez tooregister une application de ce système et obtenez un ID client.</span><span class="sxs-lookup"><span data-stu-id="5e599-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="5e599-162">Définir Facebook en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="5e599-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="5e599-163">Définir Google en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="5e599-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="5e599-164">Définir Amazon en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="5e599-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="5e599-165">Définir LinkedIn en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="5e599-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="5e599-166">Après avoir ajouté tooyour de fournisseurs d’identité hello directory B2C, modification de votre tooinclude trois stratégies hello IDPs nouveau, comme décrit dans hello [article de référence de stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5e599-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5e599-167">Après avoir enregistré vos stratégies, exécutez à nouveau application hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="5e599-168">Vous devez voir hello Qu'idps nouveau ajoutés en tant qu’options de connexion et d’inscription dans chacun de vos expériences d’identité.</span><span class="sxs-lookup"><span data-stu-id="5e599-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="5e599-169">Vous pouvez faire des essais avec vos stratégies et observez l’effet hello sur votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="5e599-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="5e599-170">Ajoutez ou supprimez des fournisseurs d’identité, manipulez des revendications d’application ou modifiez des attributs d’inscription.</span><span class="sxs-lookup"><span data-stu-id="5e599-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="5e599-171">Faites des essais jusqu’à ce que vous compreniez la façon dont les stratégies, les requêtes d’authentification et la bibliothèque OWIN sont liées.</span><span class="sxs-lookup"><span data-stu-id="5e599-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="5e599-172">Exemple de code de procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="5e599-172">Sample code walkthrough</span></span>
<span data-ttu-id="5e599-173">Hello les sections suivantes vous montre comment le code de l’application exemple hello est configuré.</span><span class="sxs-lookup"><span data-stu-id="5e599-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="5e599-174">Vous pouvez les utiliser comme guide pour le développement de vos futures applications.</span><span class="sxs-lookup"><span data-stu-id="5e599-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="5e599-175">Ajouter le support de l’authentification</span><span class="sxs-lookup"><span data-stu-id="5e599-175">Add authentication support</span></span>

<span data-ttu-id="5e599-176">Vous pouvez maintenant configurer votre toouse application Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5e599-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="5e599-177">Votre application communique avec Azure AD B2C en envoyant des demandes d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="5e599-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="5e599-178">l’expérience utilisateur hello dictent Hello demandes votre application veut tooexecute en spécifiant une stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="5e599-179">Vous pouvez utiliser toosend de bibliothèque de Microsoft OWIN ces demandes, exécution des stratégies, gérer les sessions utilisateur et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="5e599-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="5e599-180">Installer OWIN</span><span class="sxs-lookup"><span data-stu-id="5e599-180">Install OWIN</span></span>

<span data-ttu-id="5e599-181">toobegin, ajouter le projet toohello des packages de NuGet hello OWIN intergiciel (middleware) à l’aide de hello Console du Gestionnaire de Package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5e599-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="5e599-182">Ajouter une classe de démarrage OWIN</span><span class="sxs-lookup"><span data-stu-id="5e599-182">Add an OWIN startup class</span></span>

<span data-ttu-id="5e599-183">Ajouter un toohello de classe de démarrage OWIN API appelée `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="5e599-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="5e599-184">Avec le bouton droit sur le projet hello, sélectionnez **ajouter** et **un nouvel élément**, puis recherchez OWIN.</span><span class="sxs-lookup"><span data-stu-id="5e599-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="5e599-185">intergiciel (middleware) OWIN de Hello appellera hello `Configuration(…)` méthode au démarrage de votre application.</span><span class="sxs-lookup"><span data-stu-id="5e599-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="5e599-186">Dans notre exemple, nous avons modifié trop déclaration de classe hello`public partial class Startup` et implémenté hello autre partie de la classe hello dans `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="5e599-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="5e599-187">À l’intérieur hello `Configuration` (méthode), nous avons ajouté un appel trop`ConfigureAuth`, qui est défini dans `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="5e599-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="5e599-188">Après modification de hello, `Startup.cs` ressemble à hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="5e599-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="5e599-189">Configurer hello intergiciel d’authentification</span><span class="sxs-lookup"><span data-stu-id="5e599-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="5e599-190">Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et implémenter hello `ConfigureAuth(...)` (méthode).</span><span class="sxs-lookup"><span data-stu-id="5e599-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="5e599-191">Hello les paramètres que vous fournissez dans `OpenIdConnectAuthenticationOptions` servent de coordonnées pour toocommunicate de votre application avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="5e599-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="5e599-192">Si vous ne spécifiez pas de certains paramètres, il utilisera la valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="5e599-193">Par exemple, nous ne spécifiez pas hello `ResponseType` dans l’exemple hello, donc hello valeur par défaut `code id_token` seront utilisées dans chaque tooAzure demande sortante AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5e599-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="5e599-194">Vous devez également tooset l’authentification de cookie.</span><span class="sxs-lookup"><span data-stu-id="5e599-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="5e599-195">intergiciel (middleware) Hello OpenID Connect utilise les sessions utilisateur toomaintain les cookies, entre autres choses.</span><span class="sxs-lookup"><span data-stu-id="5e599-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="5e599-196">Dans `OpenIdConnectAuthenticationOptions` ci-dessus, nous définissons un ensemble de fonctions de rappel pour les notifications spécifiques qui sont reçues par un intergiciel (middleware) hello OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="5e599-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="5e599-197">Ces comportements sont définis en utilisant un `OpenIdConnectAuthenticationNotifications` de l’objet et stocké dans hello `Notifications` variable.</span><span class="sxs-lookup"><span data-stu-id="5e599-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="5e599-198">Dans notre exemple, nous définissons trois rappels différents en fonction de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="5e599-199">Utilisation de différentes stratégies</span><span class="sxs-lookup"><span data-stu-id="5e599-199">Using different policies</span></span>

<span data-ttu-id="5e599-200">Hello `RedirectToIdentityProvider` notification est déclenchée chaque fois qu’une demande est faite tooAzure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5e599-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="5e599-201">Dans la fonction de rappel hello `OnRedirectToIdentityProvider`, nous vérifions Bonjour sortant appel si nous voulons que toouse une autre stratégie.</span><span class="sxs-lookup"><span data-stu-id="5e599-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="5e599-202">Dans l’ordre toodo réinitialisation de mot de passe ou modifier un profil, vous avez besoin de stratégie correspondante de hello toouse telles que la stratégie au lieu de la stratégie de « S’inscrire ou signe » hello par défaut de réinitialisation de mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="5e599-203">Dans notre exemple, lorsqu’un utilisateur souhaite que le mot de passe tooreset hello ou modifier le profil de hello, nous ajoutons stratégie hello nous préférons toouse dans le contexte OWIN de hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="5e599-204">Cela peut se faire de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="5e599-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="5e599-205">Et vous pouvez implémenter la fonction de rappel hello `OnRedirectToIdentityProvider` de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="5e599-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="5e599-206">Gestion des codes d’autorisation</span><span class="sxs-lookup"><span data-stu-id="5e599-206">Handling authorization codes</span></span>

<span data-ttu-id="5e599-207">Hello `AuthorizationCodeReceived` notification est déclenchée lors de la réception d’un code d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="5e599-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="5e599-208">intergiciel (middleware) Hello OpenID Connect ne prend pas en charge les codes d’échange pour les jetons d’accès.</span><span class="sxs-lookup"><span data-stu-id="5e599-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="5e599-209">Vous pouvez échanger manuellement les code hello pour le jeton hello dans une fonction de rappel.</span><span class="sxs-lookup"><span data-stu-id="5e599-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="5e599-210">Pour plus d’informations, consultez hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) qui explique comment.</span><span class="sxs-lookup"><span data-stu-id="5e599-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="5e599-211">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="5e599-211">Handling errors</span></span>

<span data-ttu-id="5e599-212">Hello `AuthenticationFailed` notification est déclenchée lorsque l’authentification échoue.</span><span class="sxs-lookup"><span data-stu-id="5e599-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="5e599-213">Dans sa méthode de rappel, vous pouvez gérer les erreurs de hello comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="5e599-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="5e599-214">Toutefois, vous devez ajouter une vérification pour le code d’erreur hello `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="5e599-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="5e599-215">Pendant l’exécution de hello Hello stratégie « S’inscrire ou se connecter », utilisateur de hello a hello opportunité tooselect un **votre mot de passe oublié ?** lien.</span><span class="sxs-lookup"><span data-stu-id="5e599-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="5e599-216">Dans ce cas, Azure AD B2C envoie votre application de ce code d’erreur indiquant que votre application doit effectuer une demande à l’aide de stratégie de réinitialisation du mot de passe hello à la place.</span><span class="sxs-lookup"><span data-stu-id="5e599-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="5e599-217">Envoyer tooAzure de demandes d’authentification Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e599-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="5e599-218">Votre application est maintenant toocommunicate correctement configuré avec Azure AD B2C à l’aide du protocole d’authentification OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="5e599-219">OWIN gère les détails de hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD B2C et la gestion de session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5e599-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="5e599-220">Tout ce qui reste est tooinitiate les flux de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5e599-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="5e599-221">Lorsqu’un utilisateur sélectionne **connexion à distance et à la connexion**, **modifier le profil**, ou **réinitialisation de mot de passe** dans hello web app, action de hello associé est appelée dans `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="5e599-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="5e599-222">Vous pouvez également utiliser toosign OWIN utilisateur hello à partir de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="5e599-223">Dans `Controllers\AccountController.cs`, voici ce que nous obtenons :</span><span class="sxs-lookup"><span data-stu-id="5e599-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="5e599-224">Dans tooexplicitly plus appel d’une stratégie, vous pouvez utiliser un `[Authorize]` sur vos contrôleurs de balise qui s’exécute une stratégie si l’utilisateur de hello n’est pas connecté.</span><span class="sxs-lookup"><span data-stu-id="5e599-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="5e599-225">Ouvrez `Controllers\HomeController.cs` et ajoutez hello `[Authorize]` balise toohello revendications contrôleur.</span><span class="sxs-lookup"><span data-stu-id="5e599-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="5e599-226">OWIN sélectionne hello dernière stratégie configurée lorsque hello `[Authorize]` balise est atteint.</span><span class="sxs-lookup"><span data-stu-id="5e599-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="5e599-227">Afficher les informations utilisateur</span><span class="sxs-lookup"><span data-stu-id="5e599-227">Display user information</span></span>

<span data-ttu-id="5e599-228">Lorsque vous authentifiez des utilisateurs à l’aide de OpenID Connect, Azure AD B2C retourne une application de jeton toohello ID contenant **revendications**.</span><span class="sxs-lookup"><span data-stu-id="5e599-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="5e599-229">Il s’agit des assertions sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="5e599-229">These are assertions about hello user.</span></span> <span data-ttu-id="5e599-230">Vous pouvez utiliser les revendications toopersonalize votre application.</span><span class="sxs-lookup"><span data-stu-id="5e599-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="5e599-231">Ouvrez hello `Controllers\HomeController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="5e599-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="5e599-232">Vous pouvez accéder aux revendications d’utilisateur dans vos contrôleurs via hello `ClaimsPrincipal.Current` objet principal de sécurité.</span><span class="sxs-lookup"><span data-stu-id="5e599-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="5e599-233">Vous pouvez accéder à toute revendication que votre application reçoit Bonjour même façon.</span><span class="sxs-lookup"><span data-stu-id="5e599-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="5e599-234">Une liste de toutes les revendications hello application hello reçoit est disponible pour vous sur hello **revendications** page.</span><span class="sxs-lookup"><span data-stu-id="5e599-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>
