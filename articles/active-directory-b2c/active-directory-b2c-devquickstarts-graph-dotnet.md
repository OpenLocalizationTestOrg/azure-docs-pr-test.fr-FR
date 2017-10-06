---
title: "Azure B2C Active Directory : Hello d’utiliser API Graph | Documents Microsoft"
description: "Comment toocall hello API Graph pour un locataire B2C à l’aide d’un processus identité tooautomate hello."
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
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="22bfb-103">Azure AD B2C : Utilisez hello API Graph</span><span class="sxs-lookup"><span data-stu-id="22bfb-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="22bfb-104">Les clients Azure Active Directory (Azure AD) B2C ont tendance à toobe très volumineux.</span><span class="sxs-lookup"><span data-stu-id="22bfb-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="22bfb-105">Cela signifie que plusieurs tâches courantes de gestion client doivent toobe effectuée par programme.</span><span class="sxs-lookup"><span data-stu-id="22bfb-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="22bfb-106">La gestion des utilisateurs en est un parfait exemple.</span><span class="sxs-lookup"><span data-stu-id="22bfb-106">A primary example is user management.</span></span> <span data-ttu-id="22bfb-107">Vous devrez peut-être toomigrate un client utilisateur magasin tooa B2C.</span><span class="sxs-lookup"><span data-stu-id="22bfb-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="22bfb-108">Vous pouvez souhaitez toohost d’inscription des utilisateurs sur votre page et créer des comptes d’utilisateur dans votre annuaire Azure AD B2C coulisses hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="22bfb-109">Ces types de tâches nécessitent hello capacité toocreate, lecture, mise à jour et supprimer des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22bfb-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="22bfb-110">Vous pouvez effectuer ces tâches à l’aide des API d’Azure AD Graph hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="22bfb-111">Pour les locataires B2C, il existe deux modes de communication avec l’API Graph de hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="22bfb-112">Pour les tâches interactives, exécution unique, vous devez agir comme un compte d’administrateur de client de B2C hello lorsque vous effectuez des tâches de hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="22bfb-113">Ce mode requiert une toosign administrateur avec informations d’identification avant de l’administrateur peut effectuer n’importe quel toohello appelle l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="22bfb-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="22bfb-114">Pour les tâches automatisés en continu, vous devez utiliser un type de compte de service que vous fournissez avec les tâches de gestion tooperform hello des privilèges nécessaires.</span><span class="sxs-lookup"><span data-stu-id="22bfb-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="22bfb-115">Dans Azure AD, cela par enregistrez une application et l’authentification tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="22bfb-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="22bfb-116">Cela en utilisant un **ID d’Application** qui utilise hello [accorder des informations d’identification du client OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="22bfb-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="22bfb-117">Dans ce cas, application hello joue le rôle lui-même, pas en tant qu’utilisateur, toocall hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="22bfb-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="22bfb-118">Dans cet article, nous expliquerons comment tooperform hello cas d’usage automatisée.</span><span class="sxs-lookup"><span data-stu-id="22bfb-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="22bfb-119">toodemonstrate, nous allons construire un .NET 4.5 `B2CGraphClient` qui effectue l’utilisateur créer, lire, mettre à jour et suppression (CRUD).</span><span class="sxs-lookup"><span data-stu-id="22bfb-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="22bfb-120">client de Hello aura une interface de ligne de commande de Windows (CLI) qui vous permet de tooinvoke différentes méthodes.</span><span class="sxs-lookup"><span data-stu-id="22bfb-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="22bfb-121">Cependant, le code de hello est écrite toobehave de manière non interactive et automatisée.</span><span class="sxs-lookup"><span data-stu-id="22bfb-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="22bfb-122">Obtention d’un client Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="22bfb-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="22bfb-123">Avant de pouvoir créer des applications ou utilisateurs, ou interagir avec Azure AD du tout, vous devez un locataire Azure AD B2C et un compte d’administrateur général dans le locataire de hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="22bfb-124">Si vous n’avez pas encore de client, suivez le guide de [prise en main d’Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="22bfb-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="22bfb-125">Inscrire votre application dans votre locataire</span><span class="sxs-lookup"><span data-stu-id="22bfb-125">Register your application in your tenant</span></span>
<span data-ttu-id="22bfb-126">Une fois que vous avez un locataire B2C, vous devez tooregister votre application via hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22bfb-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22bfb-127">API de Graph toouse hello avec votre client B2C, vous devez tooregister une application dédiée à l’aide de hello générique *inscriptions d’application* panneau Bonjour Azure Portal, **pas** de B2C Azure AD  *Applications* panneau.</span><span class="sxs-lookup"><span data-stu-id="22bfb-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="22bfb-128">Vous ne pouvez pas réutiliser hello existante B2C applications que vous avez enregistré dans hello du B2C Azure AD *Applications* panneau.</span><span class="sxs-lookup"><span data-stu-id="22bfb-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="22bfb-129">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22bfb-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="22bfb-130">Choisissez votre locataire Azure AD B2C en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="22bfb-131">Dans le volet de navigation gauche hello, choisissez **plus Services**, cliquez sur **inscriptions d’application**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="22bfb-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="22bfb-132">Suivez les invites hello et créez une nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="22bfb-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="22bfb-133">Sélectionnez **application Web / API** comme hello du Type d’Application.</span><span class="sxs-lookup"><span data-stu-id="22bfb-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="22bfb-134">Fournissez **les URI de redirection** (par exemple, https://B2CGraphAPI) dans la mesure où cela n’est pas pertinent pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="22bfb-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="22bfb-135">Hello application va maintenant s’affichent dans la liste de hello des applications, cliquez sur cette tooobtain hello **ID de l’Application** (également appelé ID de Client).</span><span class="sxs-lookup"><span data-stu-id="22bfb-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="22bfb-136">Copiez-le, car vous en aurez besoin dans une section ultérieure.</span><span class="sxs-lookup"><span data-stu-id="22bfb-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="22bfb-137">Dans le panneau des paramètres de hello, cliquez sur **clés** et ajoutez une nouvelle clé (également appelé clé secrète du client).</span><span class="sxs-lookup"><span data-stu-id="22bfb-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="22bfb-138">Copiez-la également pour une utilisation dans une section ultérieure.</span><span class="sxs-lookup"><span data-stu-id="22bfb-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="22bfb-139">Configurer les autorisations Créer, Lire et Mettre à jour pour votre application</span><span class="sxs-lookup"><span data-stu-id="22bfb-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="22bfb-140">Maintenant vous devez tooconfigure votre tooget application que tous hello requis toocreate d’autorisations, lire, mettre à jour et supprimer des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="22bfb-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="22bfb-141">Continuer dans hello panneau d’inscriptions d’application du portail Azure, sélectionnez votre application.</span><span class="sxs-lookup"><span data-stu-id="22bfb-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="22bfb-142">Dans le panneau des paramètres de hello, cliquez sur **autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="22bfb-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="22bfb-143">Dans le panneau des autorisations requises hello, cliquez sur **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="22bfb-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="22bfb-144">Dans le panneau d’activer l’accès hello, sélectionnez hello **les données d’annuaire en lecture et écriture** autorisation **autorisations d’Application** et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="22bfb-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="22bfb-145">Enfin, dans le panneau des autorisations requises hello, cliquez sur hello **accorder des autorisations** bouton.</span><span class="sxs-lookup"><span data-stu-id="22bfb-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="22bfb-146">Vous avez maintenant une application qui a l’autorisation toocreate, lecture et mise à jour les utilisateurs de votre client B2C.</span><span class="sxs-lookup"><span data-stu-id="22bfb-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="22bfb-147">Configurer les autorisations de suppression pour votre application</span><span class="sxs-lookup"><span data-stu-id="22bfb-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="22bfb-148">Actuellement, hello *les données d’annuaire en lecture et écriture* autorisation est **pas** inclure hello capacité toodo toutes les suppressions, telles que la suppression des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="22bfb-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="22bfb-149">Si vous souhaitez toogive vos utilisateurs de toodelete application hello possibilité, vous devez toodo ces étapes supplémentaires qui impliquent de PowerShell, dans le cas contraire, vous pouvez ignorer la section suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="22bfb-150">Tout d’abord, téléchargez et installez hello [Assistant Microsoft Online Services Sign-In](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="22bfb-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="22bfb-151">Puis téléchargez et installez hello [64 bits du module Active Directory de Azure pour Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="22bfb-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="22bfb-152">Après avoir installé le module PowerShell de hello, ouvrez PowerShell et se connecter tooyour B2C locataire.</span><span class="sxs-lookup"><span data-stu-id="22bfb-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="22bfb-153">Après avoir exécuté `Get-Credential`, être invité à entrer un nom d’utilisateur et mot de passe, entrée hello nom d’utilisateur et mot de passe de votre compte d’administrateur client B2C.</span><span class="sxs-lookup"><span data-stu-id="22bfb-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22bfb-154">Vous devez le compte d’administrateur de client toouse un B2C est **local** toohello B2C locataire.</span><span class="sxs-lookup"><span data-stu-id="22bfb-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="22bfb-155">Ces comptes se présentent comme suit : myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="22bfb-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="22bfb-156">Maintenant, nous allons utiliser hello **ID d’Application** dans le script hello ci-dessous tooassign hello application hello compte administrateur rôle d’utilisateur qui lui permettront de toodelete utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="22bfb-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="22bfb-157">Ces rôles ont des identificateurs connus, donc vous devez toodo est entrée votre **ID d’Application** dans le script hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="22bfb-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="22bfb-158">Votre application maintenant possède également des autorisations accordées aux utilisateurs de toodelete à partir de votre client B2C.</span><span class="sxs-lookup"><span data-stu-id="22bfb-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="22bfb-159">Télécharger, configurer et générer l’exemple de code hello</span><span class="sxs-lookup"><span data-stu-id="22bfb-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="22bfb-160">Tout d’abord, téléchargez l’exemple de code hello et pouvoir l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="22bfb-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="22bfb-161">Nous l’examinerons ensuite plus en détail.</span><span class="sxs-lookup"><span data-stu-id="22bfb-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="22bfb-162">Vous pouvez [télécharger l’exemple de code hello sous forme de fichier .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="22bfb-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="22bfb-163">Vous pouvez également le cloner dans un répertoire de votre choix :</span><span class="sxs-lookup"><span data-stu-id="22bfb-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="22bfb-164">Ouvrez hello `B2CGraphClient\B2CGraphClient.sln` solution Visual Studio dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22bfb-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="22bfb-165">Bonjour `B2CGraphClient` projet, les fichiers ouverts hello `App.config`.</span><span class="sxs-lookup"><span data-stu-id="22bfb-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="22bfb-166">Remplacez les trois paramètres d’application hello par vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="22bfb-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="22bfb-167">Ensuite, avec le bouton droit sur hello `B2CGraphClient` hello, exemple solution et de reconstruction.</span><span class="sxs-lookup"><span data-stu-id="22bfb-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="22bfb-168">Si l’opération aboutit, vous devez maintenant disposer d’un fichier exécutable `B2C.exe` dans le répertoire `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="22bfb-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="22bfb-169">Générer des opérations CRUD de l’utilisateur à l’aide de l’API Graph de hello</span><span class="sxs-lookup"><span data-stu-id="22bfb-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="22bfb-170">toouse hello B2CGraphClient, ouvrez un `cmd` de commande Windows invite de commandes et modifiez votre toohello active `Debug` active.</span><span class="sxs-lookup"><span data-stu-id="22bfb-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="22bfb-171">Puis exécutez hello `B2C Help` commande.</span><span class="sxs-lookup"><span data-stu-id="22bfb-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="22bfb-172">Ceci affiche une brève description de chaque commande.</span><span class="sxs-lookup"><span data-stu-id="22bfb-172">This will display a brief description of each command.</span></span> <span data-ttu-id="22bfb-173">Chaque fois que vous appelez une de ces commandes, `B2CGraphClient` rend un toohello demande API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="22bfb-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="22bfb-174">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="22bfb-174">Get an access token</span></span>
<span data-ttu-id="22bfb-175">N’importe quel toohello demande API Graph nécessite un jeton d’accès pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="22bfb-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="22bfb-176">`B2CGraphClient`utilise hello open source Active Directory Authentication Library (ADAL) toohelp d’acquisition de jetons d’accès.</span><span class="sxs-lookup"><span data-stu-id="22bfb-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="22bfb-177">La bibliothèque ADAL facilite l’acquisition des jetons en fournissant une API simple et en prenant soin de certains détails importants, tels que la mise en cache des jetons d’accès.</span><span class="sxs-lookup"><span data-stu-id="22bfb-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="22bfb-178">Vous n’avez toouse tooget ADAL jetons, cependant.</span><span class="sxs-lookup"><span data-stu-id="22bfb-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="22bfb-179">Vous pouvez également en obtenir en créant des requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="22bfb-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="22bfb-180">Cet exemple de code utilise la bibliothèque ADAL v2 dans toocommunicate ordre avec hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="22bfb-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="22bfb-181">Vous devez utiliser la bibliothèque ADAL v2 ou v3 dans les jetons d’accès ordre tooget qui peuvent être utilisés avec hello API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="22bfb-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="22bfb-182">Lorsque `B2CGraphClient` s’exécute, il crée une instance de hello `B2CGraphClient` classe.</span><span class="sxs-lookup"><span data-stu-id="22bfb-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="22bfb-183">constructeur Hello pour cette classe définit une structure de l’authentification ADAL :</span><span class="sxs-lookup"><span data-stu-id="22bfb-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="22bfb-184">Nous allons utiliser hello `B2C Get-User` commande par exemple.</span><span class="sxs-lookup"><span data-stu-id="22bfb-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="22bfb-185">Lorsque `B2C Get-User` est appelé sans des entrées supplémentaires, hello CLI appels hello `B2CGraphClient.GetAllUsers(...)` (méthode).</span><span class="sxs-lookup"><span data-stu-id="22bfb-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="22bfb-186">Cette méthode appelle `B2CGraphClient.SendGraphGetRequest(...)`, qui envoie une API Graph toohello de demande HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="22bfb-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="22bfb-187">Avant de `B2CGraphClient.SendGraphGetRequest(...)` envoie hello demande GET, il tout d’abord Obtient un jeton d’accès à l’aide de la bibliothèque ADAL :</span><span class="sxs-lookup"><span data-stu-id="22bfb-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="22bfb-188">Vous pouvez obtenir un jeton accès pour hello API Graph en appelant hello ADAL `AuthenticationContext.AcquireToken(...)` (méthode).</span><span class="sxs-lookup"><span data-stu-id="22bfb-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="22bfb-189">La bibliothèque ADAL retourne ensuite un `access_token` qui représente l’identité de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="22bfb-190">Lecture des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="22bfb-190">Read users</span></span>
<span data-ttu-id="22bfb-191">Lorsque vous souhaitez tooget une liste d’utilisateurs ou obtenez un utilisateur particulier de hello API Graph, vous pouvez envoyer un HTTP `GET` demande toohello `/users` point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="22bfb-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="22bfb-192">Une demande pour tous les utilisateurs de hello dans un locataire ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="22bfb-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="22bfb-193">toosee cette requête, exécutez :</span><span class="sxs-lookup"><span data-stu-id="22bfb-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="22bfb-194">Il existe deux éléments importants toonote :</span><span class="sxs-lookup"><span data-stu-id="22bfb-194">There are two important things toonote:</span></span>

* <span data-ttu-id="22bfb-195">Hello jeton d’accès obtenu via la bibliothèque ADAL est ajouté toohello `Authorization` en-tête à l’aide de hello `Bearer` schéma.</span><span class="sxs-lookup"><span data-stu-id="22bfb-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="22bfb-196">Pour les locataires B2C, vous devez utiliser le paramètre de requête hello `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="22bfb-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="22bfb-197">Les deux de ces informations sont gérées dans hello `B2CGraphClient.SendGraphGetRequest(...)` méthode :</span><span class="sxs-lookup"><span data-stu-id="22bfb-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="22bfb-198">Création de comptes d’utilisateurs clients</span><span class="sxs-lookup"><span data-stu-id="22bfb-198">Create consumer user accounts</span></span>
<span data-ttu-id="22bfb-199">Lorsque vous créez des comptes d’utilisateur dans votre client B2C, vous pouvez envoyer un HTTP `POST` demande toohello `/users` point de terminaison :</span><span class="sxs-lookup"><span data-stu-id="22bfb-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="22bfb-200">La plupart de ces propriétés dans cette demande est des utilisateurs de consommateur toocreate requis.</span><span class="sxs-lookup"><span data-stu-id="22bfb-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="22bfb-201">est de plus, cliquez sur toolearn [ici](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="22bfb-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="22bfb-202">Notez que hello `//` commentaires ont été ajoutés à titre d’illustration.</span><span class="sxs-lookup"><span data-stu-id="22bfb-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="22bfb-203">Ne les incluez pas dans une requête réelle.</span><span class="sxs-lookup"><span data-stu-id="22bfb-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="22bfb-204">demande de hello toosee, exécutez une des hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="22bfb-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="22bfb-205">Hello `Create-User` commande accepte un fichier .json comme paramètre d’entrée.</span><span class="sxs-lookup"><span data-stu-id="22bfb-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="22bfb-206">Celui-ci contient une représentation JSON d’un objet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22bfb-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="22bfb-207">Il existe deux exemples de fichiers .json dans l’exemple de code hello : `usertemplate-email.json` et `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="22bfb-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="22bfb-208">Vous pouvez modifier ces toosuit de fichiers à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="22bfb-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="22bfb-209">En outre toohello requis des champs ci-dessus, plusieurs champs facultatifs que vous pouvez utiliser sont inclus dans ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="22bfb-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="22bfb-210">Vous trouverez plus d’informations sur les champs facultatifs hello Bonjour [référence d’entité API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="22bfb-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="22bfb-211">Vous pouvez voir comment la requête POST de hello est construit dans `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="22bfb-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="22bfb-212">Attache un toohello de jeton d’accès `Authorization` en-tête de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="22bfb-213">définit le paramètre `api-version=1.6`;</span><span class="sxs-lookup"><span data-stu-id="22bfb-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="22bfb-214">Il inclut objet utilisateur JSON hello dans les corps de hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="22bfb-215">Si hello comptes que vous souhaitez toomigrate à partir d’un magasin d’utilisateur existant a le niveau inférieur de mot de passe que hello [force du mot de passe fort appliquée par Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), vous pouvez désactiver l’exigence de mot de passe fort hello à l’aide de hello `DisableStrongPassword`valeur Bonjour `passwordPolicies` propriété.</span><span class="sxs-lookup"><span data-stu-id="22bfb-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="22bfb-216">Par exemple, vous pouvez modifier hello créer une demande d’utilisateur fourni ci-dessus comme suit : `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="22bfb-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="22bfb-217">Mise à jour de comptes d’utilisateurs clients</span><span class="sxs-lookup"><span data-stu-id="22bfb-217">Update consumer user accounts</span></span>
<span data-ttu-id="22bfb-218">Lorsque vous mettez à jour les objets utilisateur, les processus de hello est similaire toohello celui que vous utilisez des objets de l’utilisateur toocreate.</span><span class="sxs-lookup"><span data-stu-id="22bfb-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="22bfb-219">Mais ce processus utilise hello HTTP `PATCH` méthode :</span><span class="sxs-lookup"><span data-stu-id="22bfb-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="22bfb-220">Essayez de tooupdate un utilisateur en mettant à jour vos fichiers JSON avec de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="22bfb-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="22bfb-221">Vous pouvez ensuite utiliser `B2CGraphClient` toorun une des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="22bfb-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="22bfb-222">Inspecter hello `B2CGraphClient.SendGraphPatchRequest(...)` méthode pour plus d’informations sur la façon de toosend cette demande.</span><span class="sxs-lookup"><span data-stu-id="22bfb-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="22bfb-223">Rechercher des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="22bfb-223">Search users</span></span>
<span data-ttu-id="22bfb-224">Vous pouvez rechercher des utilisateurs dans votre client B2C de deux façons.</span><span class="sxs-lookup"><span data-stu-id="22bfb-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="22bfb-225">Un, à l’aide des ID d’objet ou les deux, à l’aide de connectez-vous identificateur l’utilisateur hello de l’utilisateur hello (c'est-à-dire hello `signInNames` propriété).</span><span class="sxs-lookup"><span data-stu-id="22bfb-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="22bfb-226">Exécutez une des hello suivant toosearch de commandes pour un utilisateur spécifique :</span><span class="sxs-lookup"><span data-stu-id="22bfb-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="22bfb-227">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="22bfb-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="22bfb-228">Suppression d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="22bfb-228">Delete users</span></span>
<span data-ttu-id="22bfb-229">processus Hello pour la suppression d’un utilisateur est simple.</span><span class="sxs-lookup"><span data-stu-id="22bfb-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="22bfb-230">Hello d’utiliser HTTP `DELETE` méthode et la construction des URL de hello avec hello corriger l’ID d’objet :</span><span class="sxs-lookup"><span data-stu-id="22bfb-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="22bfb-231">toosee un exemple, entrez cette commande et vue hello supprimer chaque requête qui est imprimée toohello console :</span><span class="sxs-lookup"><span data-stu-id="22bfb-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="22bfb-232">Inspecter hello `B2CGraphClient.SendGraphDeleteRequest(...)` méthode pour plus d’informations sur la façon de toosend cette demande.</span><span class="sxs-lookup"><span data-stu-id="22bfb-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="22bfb-233">Vous pouvez effectuer beaucoup d’autres actions avec hello API Azure AD Graph dans la gestion de toouser Ajout.</span><span class="sxs-lookup"><span data-stu-id="22bfb-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="22bfb-234">La [référence de l’API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) fournit des informations détaillées sur chaque action, ainsi que des exemples de demande.</span><span class="sxs-lookup"><span data-stu-id="22bfb-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="22bfb-235">Utilisation d’attributs personnalisés</span><span class="sxs-lookup"><span data-stu-id="22bfb-235">Use custom attributes</span></span>
<span data-ttu-id="22bfb-236">La plupart des applications consommateur devez toostore tout type d’informations de profil utilisateur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="22bfb-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="22bfb-237">Pour ce faire consiste toodefine un attribut personnalisé dans votre client B2C.</span><span class="sxs-lookup"><span data-stu-id="22bfb-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="22bfb-238">Vous pouvez ensuite traiter ce hello attribut identique à traiter de toute autre propriété sur un objet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22bfb-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="22bfb-239">Vous pouvez mettre à jour les attributs de hello, supprimer l’attribut hello, requête par attribut de hello, envoyer les attributs hello comme revendication dans les jetons d’authentification et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="22bfb-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="22bfb-240">toodefine un attribut personnalisé dans votre locataire B2C, consultez hello [référence de l’attribut personnalisé B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="22bfb-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="22bfb-241">Vous pouvez afficher les attributs personnalisés de hello définis dans votre client B2C à l’aide de `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="22bfb-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="22bfb-242">sortie Hello de ces fonctions révèle détails hello de chaque attribut personnalisé, tel que :</span><span class="sxs-lookup"><span data-stu-id="22bfb-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

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

<span data-ttu-id="22bfb-243">Vous pouvez utiliser hello nom complet, comme `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, en tant que propriété sur vos objets de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22bfb-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="22bfb-244">Mettre à jour votre fichier .json avec la nouvelle propriété de hello et une valeur pour la propriété de hello, puis exécutez :</span><span class="sxs-lookup"><span data-stu-id="22bfb-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="22bfb-245">Avec `B2CGraphClient`, vous disposez d’une application de service capable de gérer les utilisateurs de votre client B2C par programmation.</span><span class="sxs-lookup"><span data-stu-id="22bfb-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="22bfb-246">`B2CGraphClient`utilise son propre toohello de tooauthenticate d’identité application API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="22bfb-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="22bfb-247">et acquiert des jetons à l’aide d’une clé secrète client.</span><span class="sxs-lookup"><span data-stu-id="22bfb-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="22bfb-248">Lorsque vous intégrez cette fonctionnalité dans votre application, prenez en considération les quelques points clés suivants pour les applications B2C :</span><span class="sxs-lookup"><span data-stu-id="22bfb-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="22bfb-249">Vous devez toogrant hello application hello autorisations appropriées dans le locataire de hello.</span><span class="sxs-lookup"><span data-stu-id="22bfb-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="22bfb-250">Pour l’instant, vous devez les jetons d’accès tooget toouse ADAL (pas MSAL).</span><span class="sxs-lookup"><span data-stu-id="22bfb-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="22bfb-251">(vous pouvez également envoyer des messages de protocole directement, sans utiliser de bibliothèque).</span><span class="sxs-lookup"><span data-stu-id="22bfb-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="22bfb-252">Lorsque vous appelez hello API Graph, utilisez `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="22bfb-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="22bfb-253">Lorsque vous créez et mettez à jour des utilisateurs clients, certaines propriétés sont requises, comme décrit plus haut.</span><span class="sxs-lookup"><span data-stu-id="22bfb-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="22bfb-254">Si vous avez des questions ou des demandes pour les actions que vous aimeriez tooperform à l’aide de hello API Graph sur votre client B2C, laissez un commentaire sur cet article ou un problème de fichier dans le dépôt d’exemples code hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="22bfb-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>

