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
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a>Installer en mode silencieux hello connecteur Proxy d’Application Azure AD
Vous souhaitez toosend en mesure de toobe une installation de script toomultiple des serveurs Windows ou les serveurs tooWindows qui n’ont pas l’interface utilisateur. Cette rubrique vous aide à créer un script Windows PowerShell qui active l’installation sans assistance pour l’installation et l’inscription de votre connecteur de Proxy d’application Azure AD.

Cette fonctionnalité est utile lorsque vous souhaitez :

* Installer le connecteur de hello sur les ordinateurs avec aucune couche d’interface utilisateur, ou lorsque vous ne pouvez pas la machine de toohello RDP.
* Installer et inscrire beaucoup de connecteurs à la fois.
* Intégrer l’installation du connecteur hello et l’inscription en tant que partie d’une autre procédure.
* Créer une image serveur standard qui contient des bits de connecteur hello mais n’est pas inscrit.

Le Proxy d’application fonctionne en installant un service Windows Server Compact appelé hello connecteur à l’intérieur de votre réseau. Pour toowork de connecteur Proxy d’Application hello, il a toobe inscrit avec votre annuaire Azure AD à l’aide d’un administrateur global et un mot de passe. Généralement, ces informations sont saisies pendant l'installation du connecteur dans une boîte de dialogue contextuelle. Toutefois, vous pouvez utiliser Windows PowerShell toocreate un tooenter d’objet d’informations d’identification vos informations d’inscription. Ou vous pouvez créer votre propre jeton et l’utiliser tooenter vos informations d’inscription.

## <a name="install-hello-connector"></a>Installer le connecteur de hello
Installer les fichiers MSI du connecteur hello sans enregistrer les hello connecteur comme suit :

1. Ouvrez une invite de commandes.
2. Exécutez hello dans le hello /q implique l’installation silencieuse de commande suivante : hello installation ne vous demande pas tooaccept hello contrat de licence utilisateur final.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a>Inscrire le connecteur de hello avec Azure AD
Il existe deux méthodes, vous pouvez utiliser le connecteur de hello tooregister :

* Inscrire le connecteur hello à l’aide d’un objet d’informations d’identification Windows PowerShell
* Inscrire le connecteur hello à l’aide d’un jeton créé hors connexion

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a>Inscrire le connecteur hello à l’aide d’un objet d’informations d’identification Windows PowerShell
1. Créer l’objet d’informations d’identification de Windows PowerShell hello en exécutant cette commande. Remplacez  *\<nom d’utilisateur\>*  et  *\<mot de passe\>*  avec le nom d’utilisateur hello et un mot de passe pour votre annuaire :
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Accédez trop**C:\Program Files\Microsoft AAD application Proxy Connector** et exécuter le script hello à l’aide de hello PowerShell informations d’identification de l’objet vous avez créé. Remplacez *$cred* avec nom hello Hello PowerShell d’informations d’identification d’objet vous avez créé :
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a>Inscrire le connecteur hello à l’aide d’un jeton créé hors connexion
1. Créer un jeton hors connexion à l’aide de la classe AuthenticationContext de hello à l’aide des valeurs de hello dans l’extrait de code hello :

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


2. Une fois que vous avez jeton de hello, créez une SecureString à l’aide du jeton de hello :

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Exécution hello suivant de commande Windows PowerShell, en remplaçant \<locataire GUID\> avec votre ID d’annuaire :

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Étapes suivantes 
* [Publier des applications avec votre propre nom de domaine](active-directory-application-proxy-custom-domains.md)
* [Activer l’authentification unique](active-directory-application-proxy-sso-using-kcd.md)
* [Résoudre les problèmes rencontrés avec le proxy d’application](active-directory-application-proxy-troubleshoot.md)


