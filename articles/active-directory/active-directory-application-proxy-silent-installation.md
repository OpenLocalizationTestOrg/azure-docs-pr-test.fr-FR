---
title: "aaaSilent installer le connecteur de Proxy d’application Azure AD | Documents Microsoft"
description: "Décrit comment tooperform une installation sans assistance de connecteur Proxy d’Application Azure AD tooprovide sécuriser l’accès à distance tooyour localement les applications."
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
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="8388c-103">Installer en mode silencieux hello connecteur Proxy d’Application Azure AD</span><span class="sxs-lookup"><span data-stu-id="8388c-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="8388c-104">Vous souhaitez toosend en mesure de toobe une installation de script toomultiple des serveurs Windows ou les serveurs tooWindows qui n’ont pas l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8388c-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="8388c-105">Cette rubrique vous aide à créer un script Windows PowerShell qui active l’installation sans assistance pour l’installation et l’inscription de votre connecteur de Proxy d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8388c-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="8388c-106">Cette fonctionnalité est utile lorsque vous souhaitez :</span><span class="sxs-lookup"><span data-stu-id="8388c-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="8388c-107">Installer le connecteur de hello sur les ordinateurs avec aucune couche d’interface utilisateur, ou lorsque vous ne pouvez pas la machine de toohello RDP.</span><span class="sxs-lookup"><span data-stu-id="8388c-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="8388c-108">Installer et inscrire beaucoup de connecteurs à la fois.</span><span class="sxs-lookup"><span data-stu-id="8388c-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="8388c-109">Intégrer l’installation du connecteur hello et l’inscription en tant que partie d’une autre procédure.</span><span class="sxs-lookup"><span data-stu-id="8388c-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="8388c-110">Créer une image serveur standard qui contient des bits de connecteur hello mais n’est pas inscrit.</span><span class="sxs-lookup"><span data-stu-id="8388c-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="8388c-111">Le Proxy d’application fonctionne en installant un service Windows Server Compact appelé hello connecteur à l’intérieur de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="8388c-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="8388c-112">Pour toowork de connecteur Proxy d’Application hello, il a toobe inscrit avec votre annuaire Azure AD à l’aide d’un administrateur global et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8388c-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="8388c-113">Généralement, ces informations sont saisies pendant l'installation du connecteur dans une boîte de dialogue contextuelle.</span><span class="sxs-lookup"><span data-stu-id="8388c-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="8388c-114">Toutefois, vous pouvez utiliser Windows PowerShell toocreate un tooenter d’objet d’informations d’identification vos informations d’inscription.</span><span class="sxs-lookup"><span data-stu-id="8388c-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="8388c-115">Ou vous pouvez créer votre propre jeton et l’utiliser tooenter vos informations d’inscription.</span><span class="sxs-lookup"><span data-stu-id="8388c-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="8388c-116">Installer le connecteur de hello</span><span class="sxs-lookup"><span data-stu-id="8388c-116">Install hello connector</span></span>
<span data-ttu-id="8388c-117">Installer les fichiers MSI du connecteur hello sans enregistrer les hello connecteur comme suit :</span><span class="sxs-lookup"><span data-stu-id="8388c-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="8388c-118">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="8388c-118">Open a command prompt.</span></span>
2. <span data-ttu-id="8388c-119">Exécutez hello dans le hello /q implique l’installation silencieuse de commande suivante : hello installation ne vous demande pas tooaccept hello contrat de licence utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="8388c-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="8388c-120">Inscrire le connecteur de hello avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="8388c-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="8388c-121">Il existe deux méthodes, vous pouvez utiliser le connecteur de hello tooregister :</span><span class="sxs-lookup"><span data-stu-id="8388c-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="8388c-122">Inscrire le connecteur hello à l’aide d’un objet d’informations d’identification Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8388c-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="8388c-123">Inscrire le connecteur hello à l’aide d’un jeton créé hors connexion</span><span class="sxs-lookup"><span data-stu-id="8388c-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="8388c-124">Inscrire le connecteur hello à l’aide d’un objet d’informations d’identification Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8388c-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="8388c-125">Créer l’objet d’informations d’identification de Windows PowerShell hello en exécutant cette commande.</span><span class="sxs-lookup"><span data-stu-id="8388c-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="8388c-126">Remplacez  *\<nom d’utilisateur\>*  et  *\<mot de passe\>*  avec le nom d’utilisateur hello et un mot de passe pour votre annuaire :</span><span class="sxs-lookup"><span data-stu-id="8388c-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="8388c-127">Accédez trop**C:\Program Files\Microsoft AAD application Proxy Connector** et exécuter le script hello à l’aide de hello PowerShell informations d’identification de l’objet vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="8388c-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="8388c-128">Remplacez *$cred* avec nom hello Hello PowerShell d’informations d’identification d’objet vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="8388c-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="8388c-129">Inscrire le connecteur hello à l’aide d’un jeton créé hors connexion</span><span class="sxs-lookup"><span data-stu-id="8388c-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="8388c-130">Créer un jeton hors connexion à l’aide de la classe AuthenticationContext de hello à l’aide des valeurs de hello dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="8388c-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
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


2. <span data-ttu-id="8388c-131">Une fois que vous avez jeton de hello, créez une SecureString à l’aide du jeton de hello :</span><span class="sxs-lookup"><span data-stu-id="8388c-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="8388c-132">Exécution hello suivant de commande Windows PowerShell, en remplaçant \<locataire GUID\> avec votre ID d’annuaire :</span><span class="sxs-lookup"><span data-stu-id="8388c-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="8388c-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8388c-133">Next steps</span></span> 
* [<span data-ttu-id="8388c-134">Publier des applications avec votre propre nom de domaine</span><span class="sxs-lookup"><span data-stu-id="8388c-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="8388c-135">Activer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8388c-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="8388c-136">Résoudre les problèmes rencontrés avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="8388c-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


