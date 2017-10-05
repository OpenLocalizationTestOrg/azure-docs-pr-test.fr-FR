---
title: Installation sans assistance du connecteur Azure AD App Proxy | Documents Microsoft
description: "Explique comment effectuer une installation silencieuse du connecteur du Proxy d’application Azure AD pour offrir un accès à distance sécurisé à vos applications locales."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9e28c89d8f64f0ae3d4150017ca544e606075c45
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="246d7-103">Installer silencieusement le connecteur du Proxy d'application Azure AD</span><span class="sxs-lookup"><span data-stu-id="246d7-103">Silently install the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="246d7-104">Vous souhaitez pouvoir envoyer un script d’installation vers plusieurs serveurs Windows ou vers des serveurs Windows sans interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="246d7-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="246d7-105">Cette rubrique vous aide à créer un script Windows PowerShell qui active l’installation sans assistance pour l’installation et l’inscription de votre connecteur de Proxy d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="246d7-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="246d7-106">Cette fonctionnalité est utile lorsque vous souhaitez :</span><span class="sxs-lookup"><span data-stu-id="246d7-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="246d7-107">Installer le connecteur sur des machines sans couche d’interface utilisateur ou quand vous ne pouvez pas vous connecter à l’ordinateur via RDP.</span><span class="sxs-lookup"><span data-stu-id="246d7-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span></span>
* <span data-ttu-id="246d7-108">Installer et inscrire beaucoup de connecteurs à la fois.</span><span class="sxs-lookup"><span data-stu-id="246d7-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="246d7-109">Intégrer l’installation et l’inscription du connecteur dans le cadre d’une autre procédure.</span><span class="sxs-lookup"><span data-stu-id="246d7-109">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="246d7-110">Créer une image de serveur standard qui contient les exécutables du connecteur, mais qui n’est pas inscrite.</span><span class="sxs-lookup"><span data-stu-id="246d7-110">Create a standard server image that contains the connector bits but is not registered.</span></span>

<span data-ttu-id="246d7-111">Le Proxy d’application fonctionne avec un service Windows Server léger appelé connecteur, à l’intérieur de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="246d7-111">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span></span> <span data-ttu-id="246d7-112">Pour que le connecteur du Proxy d'application puisse fonctionner, il doit être inscrit auprès de votre annuaire Azure AD à l'aide d'un identifiant d’administrateur global et d’un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="246d7-112">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="246d7-113">Généralement, ces informations sont saisies pendant l'installation du connecteur dans une boîte de dialogue contextuelle.</span><span class="sxs-lookup"><span data-stu-id="246d7-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="246d7-114">Toutefois, vous pouvez utiliser Windows PowerShell pour créer un objet d’informations d’identification pour entrer vos informations d’inscription.</span><span class="sxs-lookup"><span data-stu-id="246d7-114">However, you can use Windows PowerShell to create a credential object to enter your registration information.</span></span> <span data-ttu-id="246d7-115">Ou vous pouvez créer votre propre jeton et l’utiliser pour entrer vos informations d’inscription.</span><span class="sxs-lookup"><span data-stu-id="246d7-115">Or you can create your own token and use it to enter your registration information.</span></span>

## <a name="install-the-connector"></a><span data-ttu-id="246d7-116">Installation du connecteur</span><span class="sxs-lookup"><span data-stu-id="246d7-116">Install the connector</span></span>
<span data-ttu-id="246d7-117">Pour installer les MSI du connecteur sans inscrire le connecteur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="246d7-117">Install the Connector MSIs without registering the Connector as follows:</span></span>

1. <span data-ttu-id="246d7-118">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="246d7-118">Open a command prompt.</span></span>
2. <span data-ttu-id="246d7-119">Exécutez la commande suivante dans laquelle /q signifie une installation silencieuse : l’installation ne vous demande pas d’accepter le Contrat de licence d’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="246d7-119">Run the following command in which the /q means quiet installation - the installation doesn't prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a><span data-ttu-id="246d7-120">Inscription du connecteur sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="246d7-120">Register the connector with Azure AD</span></span>
<span data-ttu-id="246d7-121">Deux méthodes permettent d’inscrire le connecteur :</span><span class="sxs-lookup"><span data-stu-id="246d7-121">There are two methods you can use to register the connector:</span></span>

* <span data-ttu-id="246d7-122">Inscription du connecteur à l’aide d’un objet d’informations d’identification Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="246d7-122">Register the connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="246d7-123">Inscription du connecteur à l’aide d’un jeton créé hors connexion</span><span class="sxs-lookup"><span data-stu-id="246d7-123">Register the connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="246d7-124">Inscription du connecteur à l’aide d’un objet d’informations d’identification Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="246d7-124">Register the connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="246d7-125">Créez l’objet d’informations d’identification de Windows PowerShell en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="246d7-125">Create the Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="246d7-126">Remplacez *\<username\>* et *\<password\>* par le nom d’utilisateur et le mot de passe de votre répertoire :</span><span class="sxs-lookup"><span data-stu-id="246d7-126">Replace *\<username\>* and *\<password\>* with the username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="246d7-127">Accédez à **C:\Program Files\Microsoft AAD App Proxy Connector** et exécutez le script en utilisant l’objet d’informations d’identification PowerShell que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="246d7-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created.</span></span> <span data-ttu-id="246d7-128">Remplacez *$cred* par le nom de l’objet d’informations d’identification PowerShell que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="246d7-128">Replace *$cred* with the name of the PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="246d7-129">Inscription du connecteur à l’aide d’un jeton créé hors connexion</span><span class="sxs-lookup"><span data-stu-id="246d7-129">Register the connector using a token created offline</span></span>
1. <span data-ttu-id="246d7-130">Créez un jeton hors connexion à l’aide de la classe AuthenticationContext, en utilisant les valeurs de l’extrait de code :</span><span class="sxs-lookup"><span data-stu-id="246d7-130">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// The application ID of the connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// The reply address of the connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// The AppIdUri of the registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. <span data-ttu-id="246d7-131">Une fois que vous disposez du jeton, créez une chaîne SecureString en utilisant le jeton :</span><span class="sxs-lookup"><span data-stu-id="246d7-131">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="246d7-132">Exécuter la commande Windows PowerShell suivante, en remplaçant \<locataire GUID\> avec votre ID de répertoire :</span><span class="sxs-lookup"><span data-stu-id="246d7-132">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="246d7-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="246d7-133">Next steps</span></span> 
* [<span data-ttu-id="246d7-134">Publier des applications avec votre propre nom de domaine</span><span class="sxs-lookup"><span data-stu-id="246d7-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="246d7-135">Activer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="246d7-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="246d7-136">Résoudre les problèmes rencontrés avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="246d7-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


