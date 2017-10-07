---
title: "kit de développement logiciel aaaMFA pour les applications personnalisées | Documents Microsoft"
description: "Cet article vous explique comment toodownload et utilisez hello vérification d’en deux étapes tooenable SDK Azure MFA pour vos applications personnalisées."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="cc602-103">Création de Multi-Factor Authentication dans des applications personnalisées (SDK)</span><span class="sxs-lookup"><span data-stu-id="cc602-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="cc602-104">Hello Kit de développement logiciel (SDK) Azure multi-Factor Authentication vous permet de dans que créer vérification en deux étapes directement hello connexion ou transaction traite des applications dans votre locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc602-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="cc602-105">Hello SDK multi-Factor Authentication est disponible pour c#, Visual Basic (.NET), Java, Perl, PHP et Ruby.</span><span class="sxs-lookup"><span data-stu-id="cc602-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="cc602-106">Hello SDK fournit un wrapper mince entourant la vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="cc602-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="cc602-107">Il inclut tous les éléments que nécessaires toowrite votre code, y compris les fichiers de code source commentés, exemples de fichiers et un fichier Lisez-moi détaillé.</span><span class="sxs-lookup"><span data-stu-id="cc602-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="cc602-108">Chaque SDK inclut également un certificat et la clé privée pour chiffrer les transactions qui sont unique tooyour fournisseur d’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="cc602-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="cc602-109">Tant que vous disposez d’un fournisseur, vous pouvez télécharger hello SDK dans toutes les langues et formats dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="cc602-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="cc602-110">structure de Hello Hello API Bonjour SDK multi-Factor Authentication est simple.</span><span class="sxs-lookup"><span data-stu-id="cc602-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="cc602-111">Rendre une fonction unique d’appeler l’API tooan avec les paramètres d’option multifacteur hello (par exemple, le mode de vérification) et les données utilisateur (comme toocall numéro de téléphone hello ou toovalidate numéro de code confidentiel hello).</span><span class="sxs-lookup"><span data-stu-id="cc602-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="cc602-112">appel de fonction hello dans toohello de demandes de services web traduire Hello API Service nuage Azure multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="cc602-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="cc602-113">Tous les appels doivent inclure un certificat privé de toohello référence qui est inclus dans chaque SDK.</span><span class="sxs-lookup"><span data-stu-id="cc602-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="cc602-114">Car hello API n’ont pas toousers accès inscrit dans Azure Active Directory, vous devez fournir les informations utilisateur dans un fichier ou d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="cc602-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="cc602-115">En outre, hello API ne fournissent pas d’inscription ou l’utilisateur les fonctionnalités de gestion, par conséquent, vous devez toobuild ces processus dans votre application.</span><span class="sxs-lookup"><span data-stu-id="cc602-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc602-116">toodownload hello du Kit de développement logiciel, vous devez toocreate un fournisseur de d’authentification multifacteur Azure, même si vous disposez de licences Azure MFA, AAD Premium ou EMS.</span><span class="sxs-lookup"><span data-stu-id="cc602-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="cc602-117">Si vous créez un fournisseur d’authentification d’Azure multi-Factor à cet effet et que vous avez déjà des licences, assurez-vous que toocreate hello fournisseur avec hello **par utilisateur activé** modèle.</span><span class="sxs-lookup"><span data-stu-id="cc602-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="cc602-118">Ensuite, liez hello fournisseur toohello répertoire qui contient les licences Azure MFA, Azure AD Premium ou EMS hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="cc602-119">Cette configuration garantit que vous êtes facturé uniquement si vous avez plusieurs utilisateurs uniques à l’aide de hello SDK que nombre hello de licences que vous possédez.</span><span class="sxs-lookup"><span data-stu-id="cc602-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="cc602-120">Télécharger hello SDK</span><span class="sxs-lookup"><span data-stu-id="cc602-120">Download hello SDK</span></span>
<span data-ttu-id="cc602-121">Téléchargement hello SDK Azure multi-Factor nécessite un [fournisseur d’authentification multifacteur Azure](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="cc602-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="cc602-122">Cela requiert un abonnement Azure complet, même si vous possédez des licences Azure MFA, Azure AD Premium ou Enterprise Mobility Suite.</span><span class="sxs-lookup"><span data-stu-id="cc602-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="cc602-123">hello de toodownload SDK, accédez toohello portail de gestion multi-Factor.</span><span class="sxs-lookup"><span data-stu-id="cc602-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="cc602-124">Vous pouvez atteindre portal de hello en gérant hello du fournisseur multi-Factor Authentication directement, ou en cliquant sur hello **« Portail de toohello Go »** lien dans la page de paramètres de service de l’authentification Multifacteur hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="cc602-125">Télécharger à partir de hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="cc602-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="cc602-126">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cc602-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="cc602-127">Sur hello gauche, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc602-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="cc602-128">Page Active Directory hello, à sélectionner supérieur de hello **fournisseurs d’authentification multifacteur**</span><span class="sxs-lookup"><span data-stu-id="cc602-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="cc602-129">Au bas de hello sélectionnez **gérer**.</span><span class="sxs-lookup"><span data-stu-id="cc602-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="cc602-130">Une nouvelle page s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="cc602-130">A new page opens.</span></span>
5. <span data-ttu-id="cc602-131">Dans hello sur la gauche, en bas de hello, cliquez sur **SDK**.</span><span class="sxs-lookup"><span data-stu-id="cc602-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="cc602-132"><center>![Télécharger](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="cc602-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="cc602-133">Sélectionnez le langage hello et cliquez sur un liens de téléchargement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="cc602-134">Enregistrer le fichier téléchargé hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="cc602-135">Télécharger à partir des paramètres de service hello</span><span class="sxs-lookup"><span data-stu-id="cc602-135">Download from hello service settings</span></span>
1. <span data-ttu-id="cc602-136">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cc602-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="cc602-137">Sur hello gauche, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc602-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="cc602-138">Double-cliquez sur votre instance d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc602-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="cc602-139">Cliquez sur supérieur de hello **configurer**</span><span class="sxs-lookup"><span data-stu-id="cc602-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="cc602-140">Sous Authentification multifacteur, sélectionnez **Gérer les paramètres du service**
   ![Télécharger](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="cc602-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="cc602-141">Dans la page Paramètres de services hello, bas hello écran hello, cliquez sur **Go toohello portal**.</span><span class="sxs-lookup"><span data-stu-id="cc602-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="cc602-142">Une nouvelle page s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="cc602-142">A new page opens.</span></span>
   <span data-ttu-id="cc602-143">![Télécharger](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="cc602-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="cc602-144">Dans hello sur la gauche, en bas de hello, cliquez sur **SDK**.</span><span class="sxs-lookup"><span data-stu-id="cc602-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="cc602-145">Sélectionnez le langage hello et cliquez sur un liens de téléchargement de hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="cc602-146">Enregistrer le fichier téléchargé hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="cc602-147">Nouveautés dans hello SDK</span><span class="sxs-lookup"><span data-stu-id="cc602-147">What's in hello SDK</span></span>
<span data-ttu-id="cc602-148">Hello SDK inclut hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cc602-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="cc602-149">**LISEZ-MOI**.</span><span class="sxs-lookup"><span data-stu-id="cc602-149">**README**.</span></span> <span data-ttu-id="cc602-150">Explique comment toouse hello API d’authentification multifacteur dans une application nouvelle ou existante.</span><span class="sxs-lookup"><span data-stu-id="cc602-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="cc602-151">**Fichiers source** pour l'authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="cc602-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="cc602-152">**Certificat client** que vous utilisez toocommunicate avec hello service d’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="cc602-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="cc602-153">**Clé privée** pour le certificat de hello</span><span class="sxs-lookup"><span data-stu-id="cc602-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="cc602-154">**Résultats des appels**</span><span class="sxs-lookup"><span data-stu-id="cc602-154">**Call results.**</span></span> <span data-ttu-id="cc602-155">Une liste des codes de résultats d’appels.</span><span class="sxs-lookup"><span data-stu-id="cc602-155">A list of call result codes.</span></span> <span data-ttu-id="cc602-156">tooopen ce fichier, utilisez une application avec mise en forme, telle que WordPad.</span><span class="sxs-lookup"><span data-stu-id="cc602-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="cc602-157">Hello d’utilisation appeler tootest de codes de résultat et résoudre les problèmes de mise en œuvre de hello de l’authentification multifacteur dans votre application.</span><span class="sxs-lookup"><span data-stu-id="cc602-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="cc602-158">Ce ne sont pas des codes d'état de l'authentification.</span><span class="sxs-lookup"><span data-stu-id="cc602-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="cc602-159">**Exemples.**</span><span class="sxs-lookup"><span data-stu-id="cc602-159">**Examples.**</span></span> <span data-ttu-id="cc602-160">Exemple de code pour une implémentation fonctionnelle de base de l'authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="cc602-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="cc602-161">certificat de client Hello est un certificat privé unique qui a été généré spécialement pour vous.</span><span class="sxs-lookup"><span data-stu-id="cc602-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="cc602-162">Ne partagez pas ou n’égarez pas ce fichier.</span><span class="sxs-lookup"><span data-stu-id="cc602-162">Do not share or lose this file.</span></span> <span data-ttu-id="cc602-163">Il s’agit de sécurité de vos communications avec le service d’authentification multifacteur hello hello tooensuring clé.</span><span class="sxs-lookup"><span data-stu-id="cc602-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="cc602-164">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="cc602-164">Code sample</span></span>
<span data-ttu-id="cc602-165">Cet exemple de code montre comment toouse hello API Bonjour voix de mode standard SDK Azure multi-Factor Authentication tooadd appeler application tooyour de vérification.</span><span class="sxs-lookup"><span data-stu-id="cc602-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="cc602-166">Mode standard est un appel téléphonique auquel hello tooby répond d’utilisateur en appuyant sur la touche # de hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="cc602-167">Cet exemple utilise hello c# .NET 2.0 SDK multi-Factor Authentication dans une application ASP.NET de base avec une logique côté serveur c#, mais les processus hello sont similaire dans d’autres langages.</span><span class="sxs-lookup"><span data-stu-id="cc602-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="cc602-168">Car hello SDK inclut des fichiers sources, non des fichiers exécutables, vous pouvez générer des fichiers de hello et y fait référence ou les inclure directement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="cc602-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="cc602-169">Quand vous implémentez l’authentification multifacteur, utiliser des méthodes supplémentaires hello (appel téléphonique ou SMS) en tant que vérification secondaire ou tertiaire toosupplement votre méthode d’authentification principale (nom d’utilisateur et mot de passe).</span><span class="sxs-lookup"><span data-stu-id="cc602-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="cc602-170">Ces méthodes ne sont pas conçues comme des méthodes d’authentification principale.</span><span class="sxs-lookup"><span data-stu-id="cc602-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="cc602-171">Vue d'ensemble d’un exemple de code</span><span class="sxs-lookup"><span data-stu-id="cc602-171">Code Sample Overview</span></span>
<span data-ttu-id="cc602-172">Cet exemple de code pour une application de démonstration web simple utilise un appel téléphonique avec un # réponse de la clé tooverify hello authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc602-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="cc602-173">Ce facteur d'appel téléphonique est appelé mode standard dans l'authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="cc602-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="cc602-174">code côté client de Hello n’inclut pas tous les éléments spécifiques à l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="cc602-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="cc602-175">Étant donné que les facteurs d’authentification supplémentaires hello sont indépendantes de l’authentification principale de hello, vous pouvez les ajouter sans modifier l’interface de connexion existant hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="cc602-176">Hello API Bonjour SDK multi-Factor vous permettre de personnaliser l’expérience utilisateur hello, mais vous n’ayez pas toochange rien du tout.</span><span class="sxs-lookup"><span data-stu-id="cc602-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="cc602-177">code de Hello côté serveur ajoute l’authentification en mode standard à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="cc602-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="cc602-178">Il crée un objet PfAuthParams avec les paramètres de hello qui sont requis pour la vérification en mode standard : nom d’utilisateur, nombre et le mode de téléphone et hello du chemin d’accès toohello certificat client (CertFilePath), qui est requis pour chaque appel.</span><span class="sxs-lookup"><span data-stu-id="cc602-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="cc602-179">Pour une démonstration de tous les paramètres de PfAuthParams, voir fichier d’exemple hello Bonjour SDK.</span><span class="sxs-lookup"><span data-stu-id="cc602-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="cc602-180">Ensuite, le code de hello transmet hello PfAuthParams objet toohello pf_authenticate() une fonction.</span><span class="sxs-lookup"><span data-stu-id="cc602-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="cc602-181">valeur de retour Hello indique la réussite de hello ou l’échec d’authentification de hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="cc602-182">Bonjour des paramètres, callStatus et un code d’erreur, contiennent des informations de résultat d’appel supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="cc602-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="cc602-183">codes de résultat d’appel Hello sont documentées dans le fichier de résultats d’appel hello Bonjour SDK.</span><span class="sxs-lookup"><span data-stu-id="cc602-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="cc602-184">Cette implémentation minimale peut être écrite en quelques lignes.</span><span class="sxs-lookup"><span data-stu-id="cc602-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="cc602-185">Toutefois, dans le code de production, vous pouvez inclure une gestion plus sophistiquée des erreurs, un autre code de base de données et une expérience utilisateur améliorée.</span><span class="sxs-lookup"><span data-stu-id="cc602-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="cc602-186">Code du client Web</span><span class="sxs-lookup"><span data-stu-id="cc602-186">Web Client Code</span></span>
<span data-ttu-id="cc602-187">Hello Voici code du client web pour une page de démonstration.</span><span class="sxs-lookup"><span data-stu-id="cc602-187">hello following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="cc602-188">Code côté serveur</span><span class="sxs-lookup"><span data-stu-id="cc602-188">Server-Side Code</span></span>
<span data-ttu-id="cc602-189">Bonjour suivant le code côté serveur, l’authentification multifacteur est configurée et exécutée à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="cc602-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="cc602-190">Mode standard (MODE_STANDARD) est qu'un utilisateur de hello toowhich appel téléphonique répond en appuyant sur la touche # de hello.</span><span class="sxs-lookup"><span data-stu-id="cc602-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
