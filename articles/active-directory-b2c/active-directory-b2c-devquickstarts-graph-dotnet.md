---
title: "Azure Active Directory B2C : utilisation de l’API Graph | Microsoft Docs"
description: "Comment appeler l’API Graph pour un client B2C à l’aide d’une identité d’application pour automatiser le processus."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: c838fcad21875c4f813159ad78d4c87129a40a86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="010b1-103">Azure AD B2C : utilisation de l’API Graph</span><span class="sxs-lookup"><span data-stu-id="010b1-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="010b1-104">Les clients Azure Active Directory (Azure AD) B2C sont souvent très volumineux.</span><span class="sxs-lookup"><span data-stu-id="010b1-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="010b1-105">Par conséquent, de nombreuses tâches courantes de gestion de client doivent être effectuées par programmation.</span><span class="sxs-lookup"><span data-stu-id="010b1-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="010b1-106">La gestion des utilisateurs en est un parfait exemple.</span><span class="sxs-lookup"><span data-stu-id="010b1-106">A primary example is user management.</span></span> <span data-ttu-id="010b1-107">Il se peut que vous ayez besoin de migrer un magasin d’utilisateurs existant vers un client B2C</span><span class="sxs-lookup"><span data-stu-id="010b1-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="010b1-108">ou que vous souhaitiez héberger l’inscription des utilisateurs sur votre page et créer des comptes d’utilisateur dans votre répertoire Azure AD B2C en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="010b1-108">You may want to host user registration on your own page and create user accounts in your Azure AD B2C directory behind the scenes.</span></span> <span data-ttu-id="010b1-109">Pour effectuer ces types de tâches, vous devez être en mesure de créer, de lire, de mettre à jour et de supprimer des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="010b1-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="010b1-110">Vous pouvez faire tout cela à l’aide de l’API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="010b1-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="010b1-111">Pour les clients B2C, il existe deux modes principaux de communication avec l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="010b1-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="010b1-112">Pour les tâches interactives, à exécution unique, vous devez agir comme un compte d’administrateur dans le client B2C lorsque vous exécutez ces tâches.</span><span class="sxs-lookup"><span data-stu-id="010b1-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="010b1-113">Avec ce mode, un administrateur doit se connecter à l’aide de ses informations d’identification avant de pouvoir effectuer des appels à l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="010b1-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="010b1-114">Pour les tâches automatisées, en continu, vous devez utiliser un compte de service doté des privilèges nécessaires pour effectuer des tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="010b1-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="010b1-115">Dans Azure AD, vous pouvez le faire en inscrivant une application et en l’authentifiant auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="010b1-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="010b1-116">à l’aide d’un **ID d’application** qui utilise [l’octroi des informations d’identification du client OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="010b1-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="010b1-117">Dans ce cas, l’application joue son propre rôle, et non celui d’un utilisateur, pour appeler l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="010b1-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="010b1-118">Dans cet article, nous allons expliquer comment exécuter le cas d’utilisation automatisée.</span><span class="sxs-lookup"><span data-stu-id="010b1-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="010b1-119">Pour cette démonstration, nous allons créer un `B2CGraphClient` .NET 4.5 qui effectuera les opérations de création, de lecture, de mise à jour et de suppression (CRUD) d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="010b1-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="010b1-120">Le client aura une interface de ligne de commande (CLI) Windows permettant d’appeler des méthodes différentes.</span><span class="sxs-lookup"><span data-stu-id="010b1-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="010b1-121">Toutefois, le code est écrit pour se comporter de façon non interactive et automatisée.</span><span class="sxs-lookup"><span data-stu-id="010b1-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="010b1-122">Obtention d’un client Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="010b1-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="010b1-123">Avant de pouvoir créer des applications ou des utilisateurs, ou interagir avec Azure AD, vous avez besoin d’un client Azure AD B2C comportant un compte d’administrateur général.</span><span class="sxs-lookup"><span data-stu-id="010b1-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="010b1-124">Si vous n’avez pas encore de client, suivez le guide de [prise en main d’Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="010b1-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="010b1-125">Inscrire votre application dans votre locataire</span><span class="sxs-lookup"><span data-stu-id="010b1-125">Register your application in your tenant</span></span>
<span data-ttu-id="010b1-126">Une fois que vous avez un locataire B2C, vous devez inscrire votre application par le biais du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="010b1-126">After you have a B2C tenant, you need to register your application via the [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="010b1-127">Pour utiliser l’API Graph avec votre locataire B2C, vous allez devoir inscrire une application dédiée à l’aide du panneau générique *Inscriptions d’applications* sur le portail Azure, et **NON** à l’aide du panneau *Applications* d’Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="010b1-127">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using the generic *App Registrations* blade in the Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="010b1-128">Vous ne pouvez pas réutiliser les applications B2C existantes que vous avez inscrites dans le panneau *Applications* d’Azure AD B2C .</span><span class="sxs-lookup"><span data-stu-id="010b1-128">You can't reuse the already-existing B2C applications that you registered in the Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="010b1-129">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="010b1-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="010b1-130">Choisissez votre client Azure AD B2C en sélectionnant votre compte dans le coin supérieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="010b1-130">Choose your Azure AD B2C tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="010b1-131">Dans le volet de navigation de gauche, choisissez **Plus de services**, cliquez sur **Inscriptions d’application**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="010b1-131">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="010b1-132">Suivez les invites et créez une application.</span><span class="sxs-lookup"><span data-stu-id="010b1-132">Follow the prompts and create a new application.</span></span> 
    1. <span data-ttu-id="010b1-133">Sélectionnez **Application web/API** en tant que Type d’application.</span><span class="sxs-lookup"><span data-stu-id="010b1-133">Select **Web App / API** as the Application Type.</span></span>    
    2. <span data-ttu-id="010b1-134">Fournissez **les URI de redirection** (par exemple, https://B2CGraphAPI) dans la mesure où cela n’est pas pertinent pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="010b1-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="010b1-135">L’application va maintenant s’afficher dans la liste des applications. Cliquez sur celle-ci pour obtenir l’**ID de l’application** (également appelé ID client).</span><span class="sxs-lookup"><span data-stu-id="010b1-135">The application will now show up in the list of applications, click on it to obtain the **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="010b1-136">Copiez-le, car vous en aurez besoin dans une section ultérieure.</span><span class="sxs-lookup"><span data-stu-id="010b1-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="010b1-137">Dans le panneau Paramètres, cliquez sur **Clés** et ajoutez une nouvelle clé (également appelée clé secrète client).</span><span class="sxs-lookup"><span data-stu-id="010b1-137">In the Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="010b1-138">Copiez-la également pour une utilisation dans une section ultérieure.</span><span class="sxs-lookup"><span data-stu-id="010b1-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="010b1-139">Configurer les autorisations Créer, Lire et Mettre à jour pour votre application</span><span class="sxs-lookup"><span data-stu-id="010b1-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="010b1-140">Vous devez maintenant configurer votre application pour obtenir toutes les autorisations requises pour créer, lire, mettre à jour et supprimer des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="010b1-140">Now you need to configure your application to get all the required permissions to create, read, update and delete users.</span></span>

1. <span data-ttu-id="010b1-141">Toujours dans le panneau Inscriptions d’applications du portail Azure, sélectionnez votre application.</span><span class="sxs-lookup"><span data-stu-id="010b1-141">Continuing in the Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="010b1-142">Dans le panneau Paramètres d’application, cliquez sur **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="010b1-142">In the Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="010b1-143">Dans le panneau Autorisations requises, cliquez sur **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="010b1-143">In the Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="010b1-144">Dans le panneau Activer l’accès, sélectionnez l’autorisation **Accéder en lecture et en écriture aux données de l’annuaire** dans **Autorisations d’application** et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="010b1-144">In the Enable Access  blade, select the **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="010b1-145">Enfin, dans le panneau Autorisations requises, cliquez sur le bouton **Accorder des autorisations**.</span><span class="sxs-lookup"><span data-stu-id="010b1-145">Finally, back in the Required permissions blade, click on the **Grant Permissions** button.</span></span>

<span data-ttu-id="010b1-146">Vous disposez maintenant d’une application autorisée à créer, lire et mettre à jour des utilisateurs de votre client B2C.</span><span class="sxs-lookup"><span data-stu-id="010b1-146">You now have an application that has permission to create, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="010b1-147">Configurer les autorisations de suppression pour votre application</span><span class="sxs-lookup"><span data-stu-id="010b1-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="010b1-148">Actuellement, l’autorisation *Accéder en lecture et en écriture aux données de l’annuaire* n’inclut **PAS** la possibilité d’effectuer des suppressions telles que la suppression des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="010b1-148">Currently, the *Read and write directory data* permission does **NOT** include the ability to do any deletions such as deleting users.</span></span> <span data-ttu-id="010b1-149">Si vous souhaitez donner à votre application la possibilité de supprimer des utilisateurs, vous devez effectuer ces étapes supplémentaires impliquant PowerShell. Dans le cas contraire, vous pouvez passer à la section suivante.</span><span class="sxs-lookup"><span data-stu-id="010b1-149">If you want to give your application the ability to delete users, you'll need to do these extra steps that involve PowerShell, otherwise, you can skip to the next section.</span></span>

<span data-ttu-id="010b1-150">Premièrement, téléchargez et installez [l’Assistant de connexion Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="010b1-150">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="010b1-151">Ensuite, téléchargez et installez le [Module Azure Active Directory 64 bits pour Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="010b1-151">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="010b1-152">Une fois le module PowerShell installé, ouvrez PowerShell et connectez-vous à votre client B2C.</span><span class="sxs-lookup"><span data-stu-id="010b1-152">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="010b1-153">Après avoir exécuté `Get-Credential`, vous serez invité à fournir un nom d’utilisateur et un mot de passe. Entrez le nom d’utilisateur et le mot de passe du compte d’administrateur de votre client B2C.</span><span class="sxs-lookup"><span data-stu-id="010b1-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="010b1-154">Vous devez utiliser un compte d’administrateur de locataire B2C qui est **local** pour le locataire B2C.</span><span class="sxs-lookup"><span data-stu-id="010b1-154">You need to use a B2C tenant administrator account that is **local** to the B2C tenant.</span></span> <span data-ttu-id="010b1-155">Ces comptes se présentent comme suit : myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="010b1-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="010b1-156">Maintenant, nous allons utiliser l’**ID d’application** dans le script ci-dessous pour affecter à l’application le rôle d’administrateur de compte utilisateur qui va lui permettre de supprimer des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="010b1-156">Now we'll use the **Application ID** in the script below to assign the application the user account administrator role which will allow it to delete users.</span></span> <span data-ttu-id="010b1-157">Comme ces rôles ont des identificateurs bien connus, il vous suffit d’entrer votre **ID d’application** dans le script ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="010b1-157">These roles have well-known identifiers, so all you need to do is input your **Application ID** in the script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="010b1-158">À présent, votre application dispose également des autorisations pour supprimer des utilisateurs sur votre locataire B2C.</span><span class="sxs-lookup"><span data-stu-id="010b1-158">Your application now also has permissions to delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="010b1-159">Téléchargement, configuration et création de l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="010b1-159">Download, configure, and build the sample code</span></span>
<span data-ttu-id="010b1-160">Tout d’abord, téléchargez l’exemple de code et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="010b1-160">First, download the sample code and get it running.</span></span> <span data-ttu-id="010b1-161">Nous l’examinerons ensuite plus en détail.</span><span class="sxs-lookup"><span data-stu-id="010b1-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="010b1-162">Vous pouvez [télécharger l’exemple de code en tant que fichier .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="010b1-162">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="010b1-163">Vous pouvez également le cloner dans un répertoire de votre choix :</span><span class="sxs-lookup"><span data-stu-id="010b1-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="010b1-164">Ouvrez la solution `B2CGraphClient\B2CGraphClient.sln` Visual Studio dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="010b1-164">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="010b1-165">Dans le projet `B2CGraphClient`, ouvrez le fichier `App.config`.</span><span class="sxs-lookup"><span data-stu-id="010b1-165">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="010b1-166">Remplacez les trois paramètres de l’application par vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="010b1-166">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="010b1-167">Ensuite, cliquez avec le bouton droit sur la solution `B2CGraphClient` et générez à nouveau l’exemple.</span><span class="sxs-lookup"><span data-stu-id="010b1-167">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="010b1-168">Si l’opération aboutit, vous devez maintenant disposer d’un fichier exécutable `B2C.exe` dans le répertoire `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="010b1-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="010b1-169">Création d’opérations CRUD d’utilisateurs à l’aide de l’API Graph</span><span class="sxs-lookup"><span data-stu-id="010b1-169">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="010b1-170">Pour utiliser le B2CGraphClient, ouvrez une invite de commandes Windows `cmd` et remplacez votre répertoire par le répertoire `Debug`.</span><span class="sxs-lookup"><span data-stu-id="010b1-170">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="010b1-171">Exécutez ensuite la commande `B2C Help` .</span><span class="sxs-lookup"><span data-stu-id="010b1-171">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="010b1-172">Ceci affiche une brève description de chaque commande.</span><span class="sxs-lookup"><span data-stu-id="010b1-172">This will display a brief description of each command.</span></span> <span data-ttu-id="010b1-173">À chaque fois que vous appelez une de ces commandes, `B2CGraphClient` envoie une demande à l’API Azure AD Graph .</span><span class="sxs-lookup"><span data-stu-id="010b1-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="010b1-174">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="010b1-174">Get an access token</span></span>
<span data-ttu-id="010b1-175">Toute demande envoyée à l’API Graph requiert un jeton d’accès pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="010b1-175">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="010b1-176">`B2CGraphClient` utilise la bibliothèque d’authentification Active Directory (ADAL) open source pour vous aider à acquérir des jetons d’accès.</span><span class="sxs-lookup"><span data-stu-id="010b1-176">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="010b1-177">La bibliothèque ADAL facilite l’acquisition des jetons en fournissant une API simple et en prenant soin de certains détails importants, tels que la mise en cache des jetons d’accès.</span><span class="sxs-lookup"><span data-stu-id="010b1-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="010b1-178">Cependant, vous n’êtes pas obligé d’utiliser la bibliothèque ADAL pour obtenir des jetons.</span><span class="sxs-lookup"><span data-stu-id="010b1-178">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="010b1-179">Vous pouvez également en obtenir en créant des requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="010b1-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="010b1-180">Cet exemple de code utilise la bibliothèque ADAL v2 afin de communiquer avec l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="010b1-180">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="010b1-181">Vous devez utiliser la bibliothèque ADAL v2 ou v3 afin d’obtenir des jetons d’accès qui peuvent être utilisés avec l’API Azure AD Graph .</span><span class="sxs-lookup"><span data-stu-id="010b1-181">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="010b1-182">Lorsque `B2CGraphClient` est exécuté, il crée une instance de la classe `B2CGraphClient`.</span><span class="sxs-lookup"><span data-stu-id="010b1-182">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="010b1-183">Le constructeur de cette classe définit une structure d’authentification de la bibliothèque ADAL :</span><span class="sxs-lookup"><span data-stu-id="010b1-183">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="010b1-184">Nous allons utiliser la commande `B2C Get-User` à titre d’exemple.</span><span class="sxs-lookup"><span data-stu-id="010b1-184">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="010b1-185">Lorsque `B2C Get-User` est appelé sans entrées supplémentaires, l’interface de ligne de commande appelle la méthode `B2CGraphClient.GetAllUsers(...)`.</span><span class="sxs-lookup"><span data-stu-id="010b1-185">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="010b1-186">Cette méthode appelle `B2CGraphClient.SendGraphGetRequest(...)`, qui envoie une requête HTTP GET à l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="010b1-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="010b1-187">Avant d’envoyer la demande GET, `B2CGraphClient.SendGraphGetRequest(...)` obtient un jeton d’accès à l’aide de la bibliothèque ADAL :</span><span class="sxs-lookup"><span data-stu-id="010b1-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="010b1-188">Vous pouvez obtenir un jeton d’accès pour l’API Graph en appelant la méthode `AuthenticationContext.AcquireToken(...)` de la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="010b1-188">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="010b1-189">La bibliothèque ADAL renvoie un `access_token` qui représente l’identité de l’application.</span><span class="sxs-lookup"><span data-stu-id="010b1-189">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="010b1-190">Lecture des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="010b1-190">Read users</span></span>
<span data-ttu-id="010b1-191">Pour obtenir la liste des utilisateurs ou un utilisateur particulier à partir de l’API Graph, vous pouvez envoyer une demande HTTP `GET` au point de terminaison `/users`.</span><span class="sxs-lookup"><span data-stu-id="010b1-191">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="010b1-192">Une requête pour obtenir tous les utilisateurs d’un client se présente ainsi :</span><span class="sxs-lookup"><span data-stu-id="010b1-192">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="010b1-193">Pour afficher cette requête, exécutez :</span><span class="sxs-lookup"><span data-stu-id="010b1-193">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="010b1-194">Deux points importants sont à prendre en considération :</span><span class="sxs-lookup"><span data-stu-id="010b1-194">There are two important things to note:</span></span>

* <span data-ttu-id="010b1-195">Le jeton d’accès acquis via la bibliothèque ADAL est ajouté à l’en-tête `Authorization` à l’aide du schéma `Bearer`.</span><span class="sxs-lookup"><span data-stu-id="010b1-195">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="010b1-196">Pour les clients B2C, vous devez utiliser le paramètre de requête `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="010b1-196">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="010b1-197">Ces détails sont gérés dans la méthode `B2CGraphClient.SendGraphGetRequest(...)` :</span><span class="sxs-lookup"><span data-stu-id="010b1-197">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="010b1-198">Création de comptes d’utilisateurs clients</span><span class="sxs-lookup"><span data-stu-id="010b1-198">Create consumer user accounts</span></span>
<span data-ttu-id="010b1-199">Quand vous créez des comptes d’utilisateur dans votre client B2C, vous pouvez envoyer une demande HTTP `POST` au point de terminaison `/users` :</span><span class="sxs-lookup"><span data-stu-id="010b1-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="010b1-200">La plupart des propriétés de cette requête sont requises pour créer des utilisateurs clients.</span><span class="sxs-lookup"><span data-stu-id="010b1-200">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="010b1-201">Cliquez [ici](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser)pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="010b1-201">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="010b1-202">Veuillez noter que les commentaires `//` ont été inclus à des fins d’illustration.</span><span class="sxs-lookup"><span data-stu-id="010b1-202">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="010b1-203">Ne les incluez pas dans une requête réelle.</span><span class="sxs-lookup"><span data-stu-id="010b1-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="010b1-204">Pour afficher la requête, exécutez l’une des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="010b1-204">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="010b1-205">La commande `Create-User` prend un fichier .json comme paramètre d’entrée.</span><span class="sxs-lookup"><span data-stu-id="010b1-205">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="010b1-206">Celui-ci contient une représentation JSON d’un objet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="010b1-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="010b1-207">L’exemple de code contient deux exemples de fichiers .json : `usertemplate-email.json` et `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="010b1-207">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="010b1-208">Vous pouvez modifier ces fichiers en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="010b1-208">You can modify these files to suit your needs.</span></span> <span data-ttu-id="010b1-209">Outre les champs obligatoires ci-dessus, ces fichiers incluent plusieurs champs facultatifs que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="010b1-209">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="010b1-210">Vous trouverez plus d’informations sur ces champs facultatifs dans la [référence d’entité API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="010b1-210">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="010b1-211">Vous pouvez voir comment la demande POST est construite dans `B2CGraphClient.SendGraphPostRequest(...)`, qui :</span><span class="sxs-lookup"><span data-stu-id="010b1-211">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="010b1-212">attache un jeton d’accès à l’en-tête `Authorization` de la demande ;</span><span class="sxs-lookup"><span data-stu-id="010b1-212">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="010b1-213">définit le paramètre `api-version=1.6`;</span><span class="sxs-lookup"><span data-stu-id="010b1-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="010b1-214">inclut l’objet utilisateur JSON dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="010b1-214">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="010b1-215">Si les comptes que vous souhaitez migrer à partir d’un magasin d’utilisateurs existant ont un mot de passe moins fort que les [règles de mot de passe fort d’Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), vous pouvez désactiver la condition de mot de passe fort à l’aide de la valeur `DisableStrongPassword` dans la propriété `passwordPolicies`.</span><span class="sxs-lookup"><span data-stu-id="010b1-215">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="010b1-216">Par exemple, vous pouvez modifier la demande de création d’utilisateur fournie ci-dessus comme suit : `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="010b1-216">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="010b1-217">Mise à jour de comptes d’utilisateurs clients</span><span class="sxs-lookup"><span data-stu-id="010b1-217">Update consumer user accounts</span></span>
<span data-ttu-id="010b1-218">Le processus de mise à jour d’objets utilisateur est similaire à celui utilisé pour créer des objets utilisateur.</span><span class="sxs-lookup"><span data-stu-id="010b1-218">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="010b1-219">Cependant, ce processus fait appel à la méthode HTTP `PATCH` :</span><span class="sxs-lookup"><span data-stu-id="010b1-219">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="010b1-220">Essayez de mettre à jour un utilisateur en mettant à jour vos fichiers JSON avec de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="010b1-220">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="010b1-221">Vous pouvez ensuite utiliser `B2CGraphClient` pour exécuter l’une des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="010b1-221">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="010b1-222">Inspectez la méthode `B2CGraphClient.SendGraphPatchRequest(...)` pour plus d’informations sur l’envoi de cette requête.</span><span class="sxs-lookup"><span data-stu-id="010b1-222">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="010b1-223">Rechercher des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="010b1-223">Search users</span></span>
<span data-ttu-id="010b1-224">Vous pouvez rechercher des utilisateurs dans votre client B2C de deux façons.</span><span class="sxs-lookup"><span data-stu-id="010b1-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="010b1-225">En utilisant l’ID objet de l’utilisateur ou l’identificateur de connexion de l’utilisateur (par exemple, la propriété `signInNames` ).</span><span class="sxs-lookup"><span data-stu-id="010b1-225">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="010b1-226">Exécutez l’une des commandes suivantes pour rechercher un utilisateur spécifique :</span><span class="sxs-lookup"><span data-stu-id="010b1-226">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="010b1-227">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="010b1-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="010b1-228">Suppression d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="010b1-228">Delete users</span></span>
<span data-ttu-id="010b1-229">Le processus de suppression d’un utilisateur est simple.</span><span class="sxs-lookup"><span data-stu-id="010b1-229">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="010b1-230">Utilisez la méthode HTTP `DELETE` et construisez l’URL avec l’ID objet correct :</span><span class="sxs-lookup"><span data-stu-id="010b1-230">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="010b1-231">Pour obtenir un exemple, saisissez la commande suivante et consultez la requête de suppression affichée dans la console :</span><span class="sxs-lookup"><span data-stu-id="010b1-231">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="010b1-232">Inspectez la méthode `B2CGraphClient.SendGraphDeleteRequest(...)` pour plus d’informations sur l’envoi de cette requête.</span><span class="sxs-lookup"><span data-stu-id="010b1-232">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="010b1-233">L’API Azure AD Graph permet d’effectuer de nombreuses actions en plus de la gestion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="010b1-233">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="010b1-234">La [référence de l’API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) fournit des informations détaillées sur chaque action, ainsi que des exemples de demande.</span><span class="sxs-lookup"><span data-stu-id="010b1-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="010b1-235">Utilisation d’attributs personnalisés</span><span class="sxs-lookup"><span data-stu-id="010b1-235">Use custom attributes</span></span>
<span data-ttu-id="010b1-236">La plupart des applications grand public doivent stocker un certain type d’informations de profil utilisateur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="010b1-236">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="010b1-237">Pour ce faire, une solution consiste à définir un attribut personnalisé dans votre client B2C.</span><span class="sxs-lookup"><span data-stu-id="010b1-237">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="010b1-238">Vous pouvez ensuite traiter cet attribut de la même façon que toute autre propriété d’un objet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="010b1-238">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="010b1-239">Vous pouvez mettre à jour l’attribut, le supprimer, l’interroger, l’envoyer en tant que revendication dans les jetons de connexion, etc.</span><span class="sxs-lookup"><span data-stu-id="010b1-239">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="010b1-240">Pour définir un attribut personnalisé dans votre client B2C, consultez la [référence d’attribut personnalisé dans B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="010b1-240">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="010b1-241">Vous pouvez afficher les attributs personnalisés définis dans votre client B2C à l’aide de `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="010b1-241">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="010b1-242">Le résultat de ces fonctions révèle les détails de chaque attribut personnalisé, tels que :</span><span class="sxs-lookup"><span data-stu-id="010b1-242">The output of these functions reveals the details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="010b1-243">Vous pouvez utiliser le nom complet, tel que `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, en tant que propriété de vos objets utilisateur.</span><span class="sxs-lookup"><span data-stu-id="010b1-243">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="010b1-244">Mettez à jour votre fichier .json avec la nouvelle propriété et une valeur pour la propriété, puis exécutez :</span><span class="sxs-lookup"><span data-stu-id="010b1-244">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="010b1-245">Avec `B2CGraphClient`, vous disposez d’une application de service capable de gérer les utilisateurs de votre client B2C par programmation.</span><span class="sxs-lookup"><span data-stu-id="010b1-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="010b1-246">`B2CGraphClient` utilise sa propre identité d’application pour s’authentifier auprès de l’API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="010b1-246">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="010b1-247">et acquiert des jetons à l’aide d’une clé secrète client.</span><span class="sxs-lookup"><span data-stu-id="010b1-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="010b1-248">Lorsque vous intégrez cette fonctionnalité dans votre application, prenez en considération les quelques points clés suivants pour les applications B2C :</span><span class="sxs-lookup"><span data-stu-id="010b1-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="010b1-249">Vous devez accorder les autorisations appropriées à l’application dans le client.</span><span class="sxs-lookup"><span data-stu-id="010b1-249">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="010b1-250">Pour le moment, vous devez utiliser la bibliothèque ADAL (pas MSAL) pour obtenir des jetons d’accès.</span><span class="sxs-lookup"><span data-stu-id="010b1-250">For now, you need to use ADAL (not MSAL) to get access tokens.</span></span> <span data-ttu-id="010b1-251">(vous pouvez également envoyer des messages de protocole directement, sans utiliser de bibliothèque).</span><span class="sxs-lookup"><span data-stu-id="010b1-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="010b1-252">Lorsque vous appelez l’API Graph, utilisez `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="010b1-252">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="010b1-253">Lorsque vous créez et mettez à jour des utilisateurs clients, certaines propriétés sont requises, comme décrit plus haut.</span><span class="sxs-lookup"><span data-stu-id="010b1-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="010b1-254">Si vous avez des questions ou souhaitez effectuer d’autres actions à l’aide de l’API Graph sur votre client B2C, laissez un commentaire sur cet article ou enregistrez un problème dans le référentiel d’exemples de code GitHub.</span><span class="sxs-lookup"><span data-stu-id="010b1-254">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>

