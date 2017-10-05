---
title: "Utilisation d’Azure Key Vault à partir d’une application web | Microsoft Docs"
description: "Utilisez ce didacticiel pour vous aider à apprendre comment utiliser Azure Key Vault à partir d'une application web."
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
ms.openlocfilehash: d095bcfe37baefa90cf79bb48bff3f703ce1dad7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="19d11-103">Utilisation d'Azure Key Vault à partir d'une application web</span><span class="sxs-lookup"><span data-stu-id="19d11-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="19d11-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="19d11-104">Introduction</span></span>
<span data-ttu-id="19d11-105">Utilisez ce didacticiel pour vous aider à comprendre comment utiliser Azure Key Vault à partir d'une application web.</span><span class="sxs-lookup"><span data-stu-id="19d11-105">Use this tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="19d11-106">Celui-ci vous guide dans le processus d'obtention d'une clé secrète à partir d'Azure Key Vault afin de pouvoir être utilisé dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="19d11-106">It walks you through the process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="19d11-107">**Durée estimée :** 15 minutes</span><span class="sxs-lookup"><span data-stu-id="19d11-107">**Estimated time to complete:** 15 minutes</span></span>

<span data-ttu-id="19d11-108">Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="19d11-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19d11-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="19d11-109">Prerequisites</span></span>
<span data-ttu-id="19d11-110">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="19d11-110">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="19d11-111">un URI pour une clé secrète dans Azure Key Vault,</span><span class="sxs-lookup"><span data-stu-id="19d11-111">A URI to a secret in an Azure Key Vault</span></span>
* <span data-ttu-id="19d11-112">un ID client et une clé secrète client pour une application Web enregistrés avec Azure Active Directory qui a accès à votre Key Vault,</span><span class="sxs-lookup"><span data-stu-id="19d11-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access to your Key Vault</span></span>
* <span data-ttu-id="19d11-113">une application web.</span><span class="sxs-lookup"><span data-stu-id="19d11-113">A web application.</span></span> <span data-ttu-id="19d11-114">Nous afficherons les étapes d'une application ASP.NET MVC déployée dans Azure en tant qu'application web.</span><span class="sxs-lookup"><span data-stu-id="19d11-114">We will be showing the steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="19d11-115">Il est essentiel que vous ayez effectué les étapes répertoriées dans [Prise en main d'Azure Key Vault](key-vault-get-started.md) pour ce didacticiel afin que vous ayez l'URI pour une clé secrète et un ID client ainsi qu'une clé secrète client pour une application web.</span><span class="sxs-lookup"><span data-stu-id="19d11-115">It is essential that you have completed the steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have the URI to a secret and the Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="19d11-116">L'application web qui accédera à Key Vault est celle qui est enregistrée dans Azure Active Directory et est autorisée à accéder à votre Key Vault.</span><span class="sxs-lookup"><span data-stu-id="19d11-116">The web application that will be accessing the Key Vault is the one that is registered in Azure Active Directory and has been given access to your Key Vault.</span></span> <span data-ttu-id="19d11-117">Si cela n'est pas le cas, revenez à Inscrire une Application dans le didacticiel de prise en main et répétez les étapes répertoriées.</span><span class="sxs-lookup"><span data-stu-id="19d11-117">If this is not the case, go back to Register an Application in the Get Started tutorial and repeat the steps listed.</span></span>

<span data-ttu-id="19d11-118">Ce didacticiel est conçu pour les développeurs web qui comprennent les principes fondamentaux de création d'applications web sur Azure.</span><span class="sxs-lookup"><span data-stu-id="19d11-118">This tutorial is designed for web developers that understand the basics of creating web applications on Azure.</span></span> <span data-ttu-id="19d11-119">Pour plus d'informations sur Azure Web Apps, consultez [Vue d'ensemble de Web Apps](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19d11-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="19d11-120"><a id="packages"></a>Ajout de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="19d11-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="19d11-121">Deux packages doivent être installés pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="19d11-121">There are two packages that your web application needs to have installed.</span></span>

* <span data-ttu-id="19d11-122">Bibliothèque d'authentification Active Directory : contient des méthodes pour interagir avec Azure Active Directory et gérer l'identité de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="19d11-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="19d11-123">Bibliothèque Azure Key Vault : contient des méthodes pour interagir avec Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="19d11-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="19d11-124">Ces deux packages peuvent être installés à l’aide de la console du Gestionnaire de Package en utilisant la commande Install-Package.</span><span class="sxs-lookup"><span data-stu-id="19d11-124">Both of these packages can be installed using the Package Manager Console using the Install-Package command.</span></span>

    // this is currently the latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="19d11-125"><a id="webconfig"></a>Modification du fichier Web.Config</span><span class="sxs-lookup"><span data-stu-id="19d11-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="19d11-126">Il existe trois paramètres d'application qui doivent être ajoutés au fichier web.config comme suit.</span><span class="sxs-lookup"><span data-stu-id="19d11-126">There are three application settings that need to be added to the web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer to the web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is the URI for the secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="19d11-127">Si vous ne souhaitez pas héberger votre application comme une application web d'Azure, vous devriez ajouter les valeurs réelles ID client, Clé secrète client et une clé secrèteURI au fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="19d11-127">If you are not going to host your application as an Azure Web App, then you should add the actual ClientId, Client Secret, and Secret URI values to the web.config.</span></span> <span data-ttu-id="19d11-128">Sinon, laissez ces valeurs factices ; nous ajouterons les valeurs réelles dans le portail Azure pour un niveau de sécurité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="19d11-128">Otherwise leave these dummy values because we will be adding the actual values in the Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="19d11-129"><a id="gettoken"></a>Ajout d'une méthode pour obtenir un jeton d'accès</span><span class="sxs-lookup"><span data-stu-id="19d11-129"><a id="gettoken"></a>Add Method to Get an Access Token</span></span>
<span data-ttu-id="19d11-130">Pour utiliser l'API Key Vault, vous avez besoin d'un jeton d'accès.</span><span class="sxs-lookup"><span data-stu-id="19d11-130">In order to use the Key Vault API you need an access token.</span></span> <span data-ttu-id="19d11-131">Le client Key Vault gère les appels de l'API Key Vault, mais vous devez lui fournir une fonction qui lui fait obtenir le jeton d'accès.</span><span class="sxs-lookup"><span data-stu-id="19d11-131">The Key Vault Client handles calls to the Key Vault API but you need to supply it with a function that gets the access token.</span></span>  

<span data-ttu-id="19d11-132">Voici le code pour obtenir un jeton d'accès avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="19d11-132">Following is the code to get an access token from Azure Active Directory.</span></span> <span data-ttu-id="19d11-133">Ce code peut être placé n'importe où dans votre application.</span><span class="sxs-lookup"><span data-stu-id="19d11-133">This code can go anywhere in your application.</span></span> <span data-ttu-id="19d11-134">Vous pouvez par exemple ajouter une classe Utils ou EncryptionHelper.</span><span class="sxs-lookup"><span data-stu-id="19d11-134">I like to add a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property to hold the secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //the method that will be provided to the KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed to obtain the JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="19d11-135">Le moyen le plus simple d’authentifier une application Azure AD est d’utiliser une clé secrète client et un ID client.</span><span class="sxs-lookup"><span data-stu-id="19d11-135">Using a Client ID and Client Secret is the easiest way to authenticate an Azure AD application.</span></span> <span data-ttu-id="19d11-136">L'utiliser dans votre application Web permet une séparation des tâches et davantage de contrôle sur la gestion de clés.</span><span class="sxs-lookup"><span data-stu-id="19d11-136">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="19d11-137">Toutefois, vous devez placer la clé secrète client dans vos paramètres de configuration, ce qui, dans certains cas, peut s’avérer aussi dangereux que placer le secret que vous souhaitez protéger dans vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="19d11-137">But it does rely on putting the Client Secret in your configuration settings which for some can be as risky as putting the secret that you want to protect in your configuration settings.</span></span> <span data-ttu-id="19d11-138">Consultez la section ci-dessous pour plus d'informations sur l'utilisation d'un ID client et d’un certificat au lieu de l’ID client et de la clé secrète client pour authentifier l'application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19d11-138">See below for a discussion on how to use a Client ID and Certificate instead of Client ID and Client Secret to authenticate the Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="19d11-139"><a id="appstart"></a>Récupération de la clé secrète dans Application Start</span><span class="sxs-lookup"><span data-stu-id="19d11-139"><a id="appstart"></a>Retrieve the secret on Application Start</span></span>
<span data-ttu-id="19d11-140">Nous avons maintenant besoin du code pour appeler l'API Key Vault et récupérer la clé secrète.</span><span class="sxs-lookup"><span data-stu-id="19d11-140">Now we need code to call the Key Vault API and retrieve the secret.</span></span> <span data-ttu-id="19d11-141">Le code suivant peut être placé n'importe où tant qu'il est appelé avant que vous ne deviez l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="19d11-141">The following code can be put anywhere as long as it is called before you need to use it.</span></span> <span data-ttu-id="19d11-142">Ce code a été créé dans l'événement Application Start dans Global.asax afin qu'il s'exécute au démarrage et rende la clé secrète disponible à l'application.</span><span class="sxs-lookup"><span data-stu-id="19d11-142">I have put this code in the Application Start event in the Global.asax so that it runs once on start and makes the secret available for the application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class to hold the secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="19d11-143"><a id="portalsettings"></a>Ajout de paramètres d'application dans le portail Azure (facultatif)</span><span class="sxs-lookup"><span data-stu-id="19d11-143"><a id="portalsettings"></a>Add App Settings in the Azure Portal (optional)</span></span>
<span data-ttu-id="19d11-144">Si vous avez une application web d'Azure, vous pouvez maintenant ajouter les valeurs réelles pour AppSettings dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="19d11-144">If you have an Azure Web App you can now add the actual values for the AppSettings in the Azure Portal.</span></span> <span data-ttu-id="19d11-145">Ce faisant, les valeurs réelles ne seront pas dans le fichier Web.config, mais protégés via le portail où vous avez des fonctionnalités de contrôle d'accès distinctes.</span><span class="sxs-lookup"><span data-stu-id="19d11-145">By doing this, the actual values will not be in the web.config but protected via the Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="19d11-146">Ces valeurs seront remplacées par les valeurs que vous avez entrées dans votre fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="19d11-146">These values will be substituted for the values that you entered in your web.config.</span></span> <span data-ttu-id="19d11-147">Assurez-vous que les noms sont identiques.</span><span class="sxs-lookup"><span data-stu-id="19d11-147">Make sure that the names are the same.</span></span>

![Paramètres de l'application affichés dans le portail Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="19d11-149">Authentification avec un certificat et non une clé secrète client</span><span class="sxs-lookup"><span data-stu-id="19d11-149">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="19d11-150">Il est également possible d'authentifier une application Azure AD à l'aide d'un ID client et d’un certificat, plutôt qu'un ID client et une clé secrète client.</span><span class="sxs-lookup"><span data-stu-id="19d11-150">Another way to authenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="19d11-151">Voici les étapes pour utiliser un certificat dans une application Web Azure :</span><span class="sxs-lookup"><span data-stu-id="19d11-151">Following are the steps to use a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="19d11-152">obtenir ou créer un certificat ;</span><span class="sxs-lookup"><span data-stu-id="19d11-152">Get or Create a Certificate</span></span>
2. <span data-ttu-id="19d11-153">associer le certificat à une application Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="19d11-153">Associate the Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="19d11-154">ajouter du code à votre application Web pour utiliser le certificat ;</span><span class="sxs-lookup"><span data-stu-id="19d11-154">Add code to your Web App to use the Certificate</span></span>
4. <span data-ttu-id="19d11-155">ajouter un certificat à votre application Web.</span><span class="sxs-lookup"><span data-stu-id="19d11-155">Add a Certificate to your Web App</span></span>

<span data-ttu-id="19d11-156">**Obtenir ou créer un certificat** Dans notre cas, nous utiliserons un certificat de test.</span><span class="sxs-lookup"><span data-stu-id="19d11-156">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="19d11-157">Voici quelques exemples de commandes que vous pouvez utiliser dans une invite de commandes de développeur pour créer un certificat.</span><span class="sxs-lookup"><span data-stu-id="19d11-157">Here are a couple of commands that you can use in a Developer Command Prompt to create a certificate.</span></span> <span data-ttu-id="19d11-158">Accédez au répertoire dans lequel vous souhaitez créer les fichiers de certificat.</span><span class="sxs-lookup"><span data-stu-id="19d11-158">Change directory to where you want the cert files created.</span></span>  <span data-ttu-id="19d11-159">En outre, pour les dates de début et de fin du certificat, utilisez la date actuelle plus un an.</span><span class="sxs-lookup"><span data-stu-id="19d11-159">Also, for the beginning and ending date of the certificate, use the current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="19d11-160">Prenez note de la date de fin et du mot de passe pour le fichier .pfx (dans cet exemple : 31/07/2016 et test123).</span><span class="sxs-lookup"><span data-stu-id="19d11-160">Make note of the end date and the password for the .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="19d11-161">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="19d11-161">You will need them below.</span></span>

<span data-ttu-id="19d11-162">Pour plus d’informations sur la création d’un certificat de test, consultez [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="19d11-162">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="19d11-163">**Associer le certificat à une application Azure AD** Maintenant que vous disposez d'un certificat, vous devez l'associer à une application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19d11-163">**Associate the Certificate with an Azure AD application** Now that you have a certificate, you need to associate it with an Azure AD application.</span></span> <span data-ttu-id="19d11-164">Actuellement, le Portail Azure ne prend pas en charge ce worklfow ; en revanche, PowerShell, oui.</span><span class="sxs-lookup"><span data-stu-id="19d11-164">Presently, the Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="19d11-165">Exécutez les commandes suivantes pour associer le certificat à l’application Azure AD :</span><span class="sxs-lookup"><span data-stu-id="19d11-165">Run the following commands to assoicate the certificate with the Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get the thumbprint to use in your app settings
    $x509.Thumbprint

<span data-ttu-id="19d11-166">Après avoir exécuté ces commandes, vous pouvez voir l'application dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19d11-166">After you have run these commands, you can see the application in Azure AD.</span></span> <span data-ttu-id="19d11-167">Lors de votre recherche, veillez à bien sélectionner « Applications que ma société possède » au lieu de « Applications que ma société utilise » dans la boîte de dialogue de recherche.</span><span class="sxs-lookup"><span data-stu-id="19d11-167">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in the search dialog.</span></span>

<span data-ttu-id="19d11-168">Pour plus d'informations sur les objets d'application AD Azure et ServicePrincipal, consultez [Objets principal du service et application](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="19d11-168">To learn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="19d11-169">**Ajouter du code à votre application Web pour utiliser le certificat** Nous allons maintenant ajouter du code à votre application Web pour accéder au certificat et l'utiliser pour l'authentification.</span><span class="sxs-lookup"><span data-stu-id="19d11-169">**Add code to your Web App to use the Certificate** Now we will add code to your Web App to access the cert and use it for authentication.</span></span>

<span data-ttu-id="19d11-170">Tout d'abord vient le code d'accès au certificat.</span><span class="sxs-lookup"><span data-stu-id="19d11-170">First there is code to access the cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since the test root isn't installed.
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


<span data-ttu-id="19d11-171">Notez que l'emplacement StoreLocation est CurrentUser, et non LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="19d11-171">Note that the StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="19d11-172">Et que nous choisissons « false » pour la méthode Find, car nous utilisons un certificat de test.</span><span class="sxs-lookup"><span data-stu-id="19d11-172">And that we are supplying 'false' to the Find method because we are using a test cert.</span></span>

<span data-ttu-id="19d11-173">Vient ensuite le code qui utilise le CertificateHelper et crée un ClientAssertionCertificate, nécessaire pour l'authentification.</span><span class="sxs-lookup"><span data-stu-id="19d11-173">Next is code that uses the CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="19d11-174">Voici le nouveau code pour obtenir le jeton d'accès.</span><span class="sxs-lookup"><span data-stu-id="19d11-174">Here is the new code to get the access token.</span></span> <span data-ttu-id="19d11-175">Cela remplace la méthode GetToken ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="19d11-175">This replaces the GetToken method above.</span></span> <span data-ttu-id="19d11-176">Elle a un nom différent pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="19d11-176">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="19d11-177">J'ai inséré tout ce code dans la classe Utils de mon projet d’application Web pour plus de facilité d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="19d11-177">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="19d11-178">La dernière modification de code a lieu dans la méthode Application_Start.</span><span class="sxs-lookup"><span data-stu-id="19d11-178">The last code change is in the Application_Start method.</span></span> <span data-ttu-id="19d11-179">Nous devons tout d'abord appeler la méthode GetCert() pour charger le ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="19d11-179">First we need to call the GetCert() method to load the ClientAssertionCertificate.</span></span> <span data-ttu-id="19d11-180">Nous modifions ensuite la méthode de rappel que nous transmettons lors de la création d'un nouveau KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="19d11-180">And then we change the callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="19d11-181">Notez que cela remplace le code que nous avions ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="19d11-181">Note that this replaces the code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="19d11-182">**Ajouter un certificat à votre application web via le portail Azure** L’ajout d’un certificat à votre application web est un processus simple en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="19d11-182">**Add a Certificate to your Web App through the Azure Portal** Adding a Certificate to your Web App is a simple two-step process.</span></span> <span data-ttu-id="19d11-183">Connectez-vous au portail Azure et accédez à votre application Web.</span><span class="sxs-lookup"><span data-stu-id="19d11-183">First, go to the Azure Portal and navigate to your Web App.</span></span> <span data-ttu-id="19d11-184">Sur le volet Paramètres de votre application Web, cliquez sur l'entrée « Custom domains and SSL ».</span><span class="sxs-lookup"><span data-stu-id="19d11-184">On the Settings blade for your Web App, click on the entry for "Custom domains and SSL".</span></span> <span data-ttu-id="19d11-185">Sur le nouveau panneau, vous pourrez télécharger le certificat que vous avez créé plus tôt, KVWebApp.pfx. Assurez-vous de vous souvenir du mot de passe pour le pfx.</span><span class="sxs-lookup"><span data-stu-id="19d11-185">On the blade that opens you will be able to upload the Certificate that you created above, KVWebApp.pfx, make sure that you remember the password for the pfx.</span></span>

![Ajout d'un certificat à une application Web dans le portail Azure][2]

<span data-ttu-id="19d11-187">La dernière chose que vous devez faire consiste à ajouter un paramètre d’application à votre application web, nommé WEBSITE\_LOAD\_CERTIFICATES et avec la valeur *.</span><span class="sxs-lookup"><span data-stu-id="19d11-187">The last thing that you need to do is to add an Application Setting to your Web App that has the name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="19d11-188">Cela garantit que tous les certificats sont chargés.</span><span class="sxs-lookup"><span data-stu-id="19d11-188">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="19d11-189">Si vous souhaitez charger uniquement les certificats que vous avez téléchargés, vous pouvez entrer une liste séparée par des virgules de leurs empreintes numériques.</span><span class="sxs-lookup"><span data-stu-id="19d11-189">If you wanted to load only the Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="19d11-190">Pour en savoir plus sur l'ajout d'un certificat à une application Web, consultez [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="19d11-190">To learn more about adding a Certificate to a Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="19d11-191">**Ajouter un certificat à un coffre de clés en tant que clé secrète** Au lieu de télécharger votre certificat pour le service d’application web directement, vous pouvez le stocker dans le coffre de clés en tant que clé secrète et le déployer depuis cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="19d11-191">**Add a Certificate to Key Vault as a secret** Instead of uploading your certificate to the Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="19d11-192">Il s’agit d’un processus en deux étapes décrit dans le billet de blog suivant [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="19d11-192">This is a two-step process that is outlined in the following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="19d11-193"><a id="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19d11-193"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="19d11-194">Pour les références de programmation, consultez la page [Référence de l'API cliente C# du coffre de clés](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="19d11-194">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
