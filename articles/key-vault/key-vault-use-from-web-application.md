---
title: "aaaUse à partir d’une Application Web d’Azure Key Vault | Documents Microsoft"
description: "Utilisez ce didacticiel toohelp vous apprendre comment toouse Azure Key Vault à partir d’une application web."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="d9b04-103">Utilisation d'Azure Key Vault à partir d'une application web</span><span class="sxs-lookup"><span data-stu-id="d9b04-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="d9b04-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="d9b04-104">Introduction</span></span>
<span data-ttu-id="d9b04-105">Utilisez ce didacticiel toohelp vous apprendre comment toouse Azure Key Vault à partir d’une application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b04-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="d9b04-106">Il vous guide tout au long des processus de hello d’accès à une clé secrète à partir d’un coffre de clés Azure afin qu’il peut être utilisé dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="d9b04-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="d9b04-107">**Estimation du temps toocomplete :** 15 minutes</span><span class="sxs-lookup"><span data-stu-id="d9b04-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="d9b04-108">Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d9b04-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9b04-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d9b04-109">Prerequisites</span></span>
<span data-ttu-id="d9b04-110">toocomplete ce didacticiel, vous devez avoir hello suivant :</span><span class="sxs-lookup"><span data-stu-id="d9b04-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="d9b04-111">Un secret de tooa URI dans un coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="d9b04-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="d9b04-112">Un ID Client et une clé secrète du Client pour une application web inscrit auprès d’Azure Active Directory qui a accès tooyour le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="d9b04-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="d9b04-113">une application web.</span><span class="sxs-lookup"><span data-stu-id="d9b04-113">A web application.</span></span> <span data-ttu-id="d9b04-114">Nous vous exécutez les étapes hello pour une application ASP.NET MVC déployé dans Azure comme une application Web.</span><span class="sxs-lookup"><span data-stu-id="d9b04-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="d9b04-115">Il est essentiel que vous avez effectué les étapes de hello répertoriés dans [prise en main d’Azure Key Vault](key-vault-get-started.md) pour ce didacticiel afin que vous ayez hello hello ID Client et secret de tooa URI et une clé secrète pour une application web.</span><span class="sxs-lookup"><span data-stu-id="d9b04-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="d9b04-116">application web Hello qui accédera à hello coffre de clés est hello un qui est inscrit dans Azure Active Directory et a accès tooyour le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d9b04-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="d9b04-117">Si ce n’est pas le cas de hello, revenir en arrière tooRegister une Application dans le didacticiel de mise en route de hello et répétez les étapes de hello répertoriées.</span><span class="sxs-lookup"><span data-stu-id="d9b04-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="d9b04-118">Ce didacticiel est conçu pour les développeurs web qui comprennent les principes fondamentaux de hello de création d’applications web sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b04-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="d9b04-119">Pour plus d'informations sur Azure Web Apps, consultez [Vue d'ensemble de Web Apps](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9b04-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="d9b04-120"><a id="packages"></a>Ajout de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="d9b04-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="d9b04-121">Il existe deux packages de votre application web doit toohave installé.</span><span class="sxs-lookup"><span data-stu-id="d9b04-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="d9b04-122">Bibliothèque d'authentification Active Directory : contient des méthodes pour interagir avec Azure Active Directory et gérer l'identité de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="d9b04-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="d9b04-123">Bibliothèque Azure Key Vault : contient des méthodes pour interagir avec Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d9b04-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="d9b04-124">Les deux de ces packages peuvent être installés à l’aide de hello Console du Gestionnaire de Package à l’aide de la commande hello Install-Package.</span><span class="sxs-lookup"><span data-stu-id="d9b04-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="d9b04-125"><a id="webconfig"></a>Modification du fichier Web.Config</span><span class="sxs-lookup"><span data-stu-id="d9b04-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="d9b04-126">Il existe trois paramètres d’application nécessitant un fichier web.config de toohello ajouté toobe comme suit.</span><span class="sxs-lookup"><span data-stu-id="d9b04-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="d9b04-127">Si vous ne souhaitez pas toohost votre application comme une application Web Azure, vous devez ajouter hello réel ClientId, une clé secrète Client et Secret URI valeurs toohello web.config. Sinon, laissez ces valeurs factices, car nous allons ajouter les valeurs réelles hello Bonjour portail Azure pour un niveau supplémentaire de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d9b04-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="d9b04-128"><a id="gettoken"></a>Ajouter tooGet méthode un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="d9b04-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="d9b04-129">Bonjour toouse de commande API coffre de clés, vous avez besoin d’un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="d9b04-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="d9b04-130">Hello clé de coffre Client gère les appels toohello API coffre de clés, mais vous devez toosupply avec une fonction qui obtient le jeton d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="d9b04-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="d9b04-131">Tooget de code hello un jeton d’accès d’Azure Active Directory sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="d9b04-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="d9b04-132">Ce code peut être placé n'importe où dans votre application.</span><span class="sxs-lookup"><span data-stu-id="d9b04-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="d9b04-133">J’aime tooadd un Utils ou EncryptionHelper classe.</span><span class="sxs-lookup"><span data-stu-id="d9b04-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="d9b04-134">À l’aide d’un ID Client et la clé secrète du Client est tooauthenticate de façon plus simple hello une application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9b04-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="d9b04-135">L'utiliser dans votre application Web permet une séparation des tâches et davantage de contrôle sur la gestion de clés.</span><span class="sxs-lookup"><span data-stu-id="d9b04-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="d9b04-136">Mais il s’appuie sur le placement de hello question secrète du Client dans vos paramètres de configuration qui, pour certaines, comme présente des risques en plaçant secret hello que vous souhaitez tooprotect dans vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="d9b04-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="d9b04-137">Voir ci-dessous pour en savoir plus sur la façon dont toouse un ID Client et le certificat au lieu de l’ID Client et une clé secrète tooauthenticate hello application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9b04-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="d9b04-138"><a id="appstart"></a>Récupérez secret hello sur Démarrer l’Application</span><span class="sxs-lookup"><span data-stu-id="d9b04-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="d9b04-139">Nous devons maintenant toocall hello API coffre de clés de code et récupérez hello secret.</span><span class="sxs-lookup"><span data-stu-id="d9b04-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="d9b04-140">Hello de code suivant peut être placé n’importe où tant qu’il est appelé avant que vous avez besoin de toouse il.</span><span class="sxs-lookup"><span data-stu-id="d9b04-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="d9b04-141">J’ai placer ce code dans l’événement de démarrer l’Application hello Bonjour Global.asax afin qu’elle s’exécute une seule fois au démarrage et rend hello secret disponible pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d9b04-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="d9b04-142"><a id="portalsettings"></a>Ajouter des paramètres de l’application Bonjour portail Azure (facultatif)</span><span class="sxs-lookup"><span data-stu-id="d9b04-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="d9b04-143">Si vous avez une application Web Azure vous pouvez maintenant ajouter des valeurs réelles de hello pour hello AppSettings Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b04-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="d9b04-144">Ce faisant, les valeurs réelles hello ne seront pas dans le fichier web.config de hello mais protégé via hello portail où vous disposez des fonctionnalités de contrôle d’accès distincts.</span><span class="sxs-lookup"><span data-stu-id="d9b04-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="d9b04-145">Ces valeurs seront remplacées pour les valeurs hello que vous avez entré dans votre fichier web.config. Assurez-vous que les noms de hello sont hello identiques.</span><span class="sxs-lookup"><span data-stu-id="d9b04-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Paramètres de l'application affichés dans le portail Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="d9b04-147">Authentification avec un certificat et non une clé secrète client</span><span class="sxs-lookup"><span data-stu-id="d9b04-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="d9b04-148">Une autre façon tooauthenticate une application Azure AD est à l’aide d’un ID Client et un certificat au lieu d’un ID Client et la clé secrète du Client.</span><span class="sxs-lookup"><span data-stu-id="d9b04-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="d9b04-149">Suivantes sont hello étapes toouse un certificat dans une application Web Azure :</span><span class="sxs-lookup"><span data-stu-id="d9b04-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="d9b04-150">obtenir ou créer un certificat ;</span><span class="sxs-lookup"><span data-stu-id="d9b04-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="d9b04-151">Associer hello certificat avec une application Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9b04-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="d9b04-152">Ajouter hello de toouse code tooyour application Web certificat</span><span class="sxs-lookup"><span data-stu-id="d9b04-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="d9b04-153">Ajouter un certificat de tooyour Web App</span><span class="sxs-lookup"><span data-stu-id="d9b04-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="d9b04-154">**Obtenir ou créer un certificat** Dans notre cas, nous utiliserons un certificat de test.</span><span class="sxs-lookup"><span data-stu-id="d9b04-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="d9b04-155">Voici quelques exemples de commandes que vous pouvez utiliser dans une invite de commandes développeur de toocreate un certificat.</span><span class="sxs-lookup"><span data-stu-id="d9b04-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="d9b04-156">Modifiez toowhere directory que Hello cert fichiers est créé.</span><span class="sxs-lookup"><span data-stu-id="d9b04-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="d9b04-157">En outre, pour hello de début et de fin du certificat de hello, utilisez hello date actuelle plu 1 an.</span><span class="sxs-lookup"><span data-stu-id="d9b04-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="d9b04-158">Prenez note de la date de fin hello et le mot de passe hello hello .pfx (dans cet exemple : 31/07/2016 et test123).</span><span class="sxs-lookup"><span data-stu-id="d9b04-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="d9b04-159">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="d9b04-159">You will need them below.</span></span>

<span data-ttu-id="d9b04-160">Pour plus d’informations sur la création d’un certificat de test, consultez [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="d9b04-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="d9b04-161">**Associer hello certificat avec une application Azure AD** maintenant que vous avez un certificat, vous devez tooassociate avec une application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9b04-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="d9b04-162">Actuellement, hello portail Azure ne prend pas en charge ce flux de travail ; Cette opération peut être effectuée via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9b04-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="d9b04-163">Exécutez hello suivant le certificat de hello tooassoicate de commandes avec l’application hello Azure AD :</span><span class="sxs-lookup"><span data-stu-id="d9b04-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="d9b04-164">Après avoir exécuté ces commandes, vous pouvez voir l’application hello dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9b04-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="d9b04-165">Lors de la recherche, veillez à que sélectionner « Ma société possède des Applications » au lieu de « Applications ma société utilise » dans la boîte de dialogue de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="d9b04-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="d9b04-166">toolearn en savoir plus sur les objets d’Application Azure AD et les objets de principal du service, consultez [objets de Principal du Service et Application](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="d9b04-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="d9b04-167">**Ajouter hello de toouse Web application code tooyour certificat** maintenant nous allons ajouter le code tooyour Web App tooaccess hello cert et l’utiliser pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="d9b04-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="d9b04-168">Tout d’abord est cert de code tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="d9b04-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="d9b04-169">Notez que hello StoreLocation est CurrentUser au lieu de l’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d9b04-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="d9b04-170">Et que nous sommes en fournissant toohello 'false' Find (méthode), car nous utilisons un certificat de test.</span><span class="sxs-lookup"><span data-stu-id="d9b04-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="d9b04-171">L’élément suivant est le code qui utilise hello CertificateHelper et crée un ClientAssertionCertificate qui est nécessaire pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="d9b04-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="d9b04-172">Voici le jeton d’accès hello nouveau code tooget hello.</span><span class="sxs-lookup"><span data-stu-id="d9b04-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="d9b04-173">Cette opération remplace hello GetToken, méthode ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d9b04-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="d9b04-174">Elle a un nom différent pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="d9b04-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="d9b04-175">J'ai inséré tout ce code dans la classe Utils de mon projet d’application Web pour plus de facilité d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="d9b04-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="d9b04-176">dernière modification de code Hello est Bonjour méthode Application_Start.</span><span class="sxs-lookup"><span data-stu-id="d9b04-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="d9b04-177">Tout d’abord, nous devons toocall hello hello tooload de méthode GetCert() ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="d9b04-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="d9b04-178">Puis nous modifiez la méthode de rappel hello qui nous fournir lors de la création d’un nouveau KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="d9b04-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="d9b04-179">Notez que cette opération remplace code hello que nous avions ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d9b04-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="d9b04-180">**Ajouter une application Web de tooyour certificat via hello portail Azure** Ajout d’un certificat de tooyour application Web est un processus en deux étapes simples.</span><span class="sxs-lookup"><span data-stu-id="d9b04-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="d9b04-181">Tout d’abord, accédez toohello portail Azure et accédez tooyour application Web.</span><span class="sxs-lookup"><span data-stu-id="d9b04-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="d9b04-182">Dans le panneau des paramètres hello pour votre application Web, cliquez sur entrée hello pour « les domaines personnalisés et SSL ».</span><span class="sxs-lookup"><span data-stu-id="d9b04-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="d9b04-183">Sur hello panneau qui s’ouvre vous seront hello de tooupload en mesure de certificat que vous avez créé précédemment, KVWebApp.pfx, assurez-vous que vous n’oubliez pas le mot de passe hello hello pfx.</span><span class="sxs-lookup"><span data-stu-id="d9b04-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![Ajout d’une application Web de tooa certificat Bonjour portail Azure][2]

<span data-ttu-id="d9b04-185">dernière chose que toodo Hello est tooadd un tooyour de paramètre d’Application Web application disposant du site Web de noms hello\_charge\_certificats et la valeur *.</span><span class="sxs-lookup"><span data-stu-id="d9b04-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="d9b04-186">Cela garantit que tous les certificats sont chargés.</span><span class="sxs-lookup"><span data-stu-id="d9b04-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="d9b04-187">Si vous souhaitiez hello uniquement de tooload certificats que vous avez téléchargé, puis vous pouvez entrer une liste séparée par des virgules de leurs empreintes numériques.</span><span class="sxs-lookup"><span data-stu-id="d9b04-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="d9b04-188">toolearn plus sur l’ajout d’un certificat de tooa Web App, consultez [à l’aide de certificats dans les Applications de sites Web Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="d9b04-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="d9b04-189">**Ajouter un certificat de tooKey coffre en tant que secret** au lieu de charger votre certificat de toohello service d’application Web directement, vous pouvez stocker dans le coffre de clés en tant que secret et le déployer à partir de là.</span><span class="sxs-lookup"><span data-stu-id="d9b04-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="d9b04-190">Il s’agit d’un processus en deux étapes est décrite dans hello suivant le billet de blog, [déploiement Azure certificat l’application Web via le coffre de clés](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="d9b04-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="d9b04-191"><a id="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9b04-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="d9b04-192">Pour les références de programmation, consultez la page [Référence de l'API cliente C# du coffre de clés](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9b04-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
