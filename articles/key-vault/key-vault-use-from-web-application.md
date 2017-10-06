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
# <a name="use-azure-key-vault-from-a-web-application"></a>Utilisation d'Azure Key Vault à partir d'une application web
## <a name="introduction"></a>Introduction
Utilisez ce didacticiel toohelp vous apprendre comment toouse Azure Key Vault à partir d’une application web dans Azure. Il vous guide tout au long des processus de hello d’accès à une clé secrète à partir d’un coffre de clés Azure afin qu’il peut être utilisé dans votre application web.

**Estimation du temps toocomplete :** 15 minutes

Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez avoir hello suivant :

* Un secret de tooa URI dans un coffre de clés Azure
* Un ID Client et une clé secrète du Client pour une application web inscrit auprès d’Azure Active Directory qui a accès tooyour le coffre de clés
* une application web. Nous vous exécutez les étapes hello pour une application ASP.NET MVC déployé dans Azure comme une application Web.

> [!NOTE]
> Il est essentiel que vous avez effectué les étapes de hello répertoriés dans [prise en main d’Azure Key Vault](key-vault-get-started.md) pour ce didacticiel afin que vous ayez hello hello ID Client et secret de tooa URI et une clé secrète pour une application web.
> 
> 

application web Hello qui accédera à hello coffre de clés est hello un qui est inscrit dans Azure Active Directory et a accès tooyour le coffre de clés. Si ce n’est pas le cas de hello, revenir en arrière tooRegister une Application dans le didacticiel de mise en route de hello et répétez les étapes de hello répertoriées.

Ce didacticiel est conçu pour les développeurs web qui comprennent les principes fondamentaux de hello de création d’applications web sur Azure. Pour plus d'informations sur Azure Web Apps, consultez [Vue d'ensemble de Web Apps](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Ajout de packages NuGet
Il existe deux packages de votre application web doit toohave installé.

* Bibliothèque d'authentification Active Directory : contient des méthodes pour interagir avec Azure Active Directory et gérer l'identité de l'utilisateur
* Bibliothèque Azure Key Vault : contient des méthodes pour interagir avec Azure Key Vault

Les deux de ces packages peuvent être installés à l’aide de hello Console du Gestionnaire de Package à l’aide de la commande hello Install-Package.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Modification du fichier Web.Config
Il existe trois paramètres d’application nécessitant un fichier web.config de toohello ajouté toobe comme suit.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Si vous ne souhaitez pas toohost votre application comme une application Web Azure, vous devez ajouter hello réel ClientId, une clé secrète Client et Secret URI valeurs toohello web.config. Sinon, laissez ces valeurs factices, car nous allons ajouter les valeurs réelles hello Bonjour portail Azure pour un niveau supplémentaire de sécurité.

## <a id="gettoken"></a>Ajouter tooGet méthode un jeton d’accès
Bonjour toouse de commande API coffre de clés, vous avez besoin d’un jeton d’accès. Hello clé de coffre Client gère les appels toohello API coffre de clés, mais vous devez toosupply avec une fonction qui obtient le jeton d’accès hello.  

Tooget de code hello un jeton d’accès d’Azure Active Directory sont les suivants : Ce code peut être placé n'importe où dans votre application. J’aime tooadd un Utils ou EncryptionHelper classe.  

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
> À l’aide d’un ID Client et la clé secrète du Client est tooauthenticate de façon plus simple hello une application Azure AD. L'utiliser dans votre application Web permet une séparation des tâches et davantage de contrôle sur la gestion de clés. Mais il s’appuie sur le placement de hello question secrète du Client dans vos paramètres de configuration qui, pour certaines, comme présente des risques en plaçant secret hello que vous souhaitez tooprotect dans vos paramètres de configuration. Voir ci-dessous pour en savoir plus sur la façon dont toouse un ID Client et le certificat au lieu de l’ID Client et une clé secrète tooauthenticate hello application Azure AD.
> 
> 

## <a id="appstart"></a>Récupérez secret hello sur Démarrer l’Application
Nous devons maintenant toocall hello API coffre de clés de code et récupérez hello secret. Hello de code suivant peut être placé n’importe où tant qu’il est appelé avant que vous avez besoin de toouse il. J’ai placer ce code dans l’événement de démarrer l’Application hello Bonjour Global.asax afin qu’elle s’exécute une seule fois au démarrage et rend hello secret disponible pour l’application hello.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Ajouter des paramètres de l’application Bonjour portail Azure (facultatif)
Si vous avez une application Web Azure vous pouvez maintenant ajouter des valeurs réelles de hello pour hello AppSettings Bonjour portail Azure. Ce faisant, les valeurs réelles hello ne seront pas dans le fichier web.config de hello mais protégé via hello portail où vous disposez des fonctionnalités de contrôle d’accès distincts. Ces valeurs seront remplacées pour les valeurs hello que vous avez entré dans votre fichier web.config. Assurez-vous que les noms de hello sont hello identiques.

![Paramètres de l'application affichés dans le portail Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Authentification avec un certificat et non une clé secrète client
Une autre façon tooauthenticate une application Azure AD est à l’aide d’un ID Client et un certificat au lieu d’un ID Client et la clé secrète du Client. Suivantes sont hello étapes toouse un certificat dans une application Web Azure :

1. obtenir ou créer un certificat ;
2. Associer hello certificat avec une application Azure AD
3. Ajouter hello de toouse code tooyour application Web certificat
4. Ajouter un certificat de tooyour Web App

**Obtenir ou créer un certificat** Dans notre cas, nous utiliserons un certificat de test. Voici quelques exemples de commandes que vous pouvez utiliser dans une invite de commandes développeur de toocreate un certificat. Modifiez toowhere directory que Hello cert fichiers est créé.  En outre, pour hello de début et de fin du certificat de hello, utilisez hello date actuelle plu 1 an.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Prenez note de la date de fin hello et le mot de passe hello hello .pfx (dans cet exemple : 31/07/2016 et test123). Vous en aurez besoin ultérieurement.

Pour plus d’informations sur la création d’un certificat de test, consultez [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)

**Associer hello certificat avec une application Azure AD** maintenant que vous avez un certificat, vous devez tooassociate avec une application Azure AD. Actuellement, hello portail Azure ne prend pas en charge ce flux de travail ; Cette opération peut être effectuée via PowerShell. Exécutez hello suivant le certificat de hello tooassoicate de commandes avec l’application hello Azure AD :

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

Après avoir exécuté ces commandes, vous pouvez voir l’application hello dans Azure AD. Lors de la recherche, veillez à que sélectionner « Ma société possède des Applications » au lieu de « Applications ma société utilise » dans la boîte de dialogue de recherche hello.

toolearn en savoir plus sur les objets d’Application Azure AD et les objets de principal du service, consultez [objets de Principal du Service et Application](../active-directory/active-directory-application-objects.md)

**Ajouter hello de toouse Web application code tooyour certificat** maintenant nous allons ajouter le code tooyour Web App tooaccess hello cert et l’utiliser pour l’authentification.

Tout d’abord est cert de code tooaccess hello.

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


Notez que hello StoreLocation est CurrentUser au lieu de l’ordinateur local. Et que nous sommes en fournissant toohello 'false' Find (méthode), car nous utilisons un certificat de test.

L’élément suivant est le code qui utilise hello CertificateHelper et crée un ClientAssertionCertificate qui est nécessaire pour l’authentification.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Voici le jeton d’accès hello nouveau code tooget hello. Cette opération remplace hello GetToken, méthode ci-dessus. Elle a un nom différent pour des raisons pratiques.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

J'ai inséré tout ce code dans la classe Utils de mon projet d’application Web pour plus de facilité d'utilisation.

dernière modification de code Hello est Bonjour méthode Application_Start. Tout d’abord, nous devons toocall hello hello tooload de méthode GetCert() ClientAssertionCertificate. Puis nous modifiez la méthode de rappel hello qui nous fournir lors de la création d’un nouveau KeyVaultClient. Notez que cette opération remplace code hello que nous avions ci-dessus.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Ajouter une application Web de tooyour certificat via hello portail Azure** Ajout d’un certificat de tooyour application Web est un processus en deux étapes simples. Tout d’abord, accédez toohello portail Azure et accédez tooyour application Web. Dans le panneau des paramètres hello pour votre application Web, cliquez sur entrée hello pour « les domaines personnalisés et SSL ». Sur hello panneau qui s’ouvre vous seront hello de tooupload en mesure de certificat que vous avez créé précédemment, KVWebApp.pfx, assurez-vous que vous n’oubliez pas le mot de passe hello hello pfx.

![Ajout d’une application Web de tooa certificat Bonjour portail Azure][2]

dernière chose que toodo Hello est tooadd un tooyour de paramètre d’Application Web application disposant du site Web de noms hello\_charge\_certificats et la valeur *. Cela garantit que tous les certificats sont chargés. Si vous souhaitiez hello uniquement de tooload certificats que vous avez téléchargé, puis vous pouvez entrer une liste séparée par des virgules de leurs empreintes numériques.

toolearn plus sur l’ajout d’un certificat de tooa Web App, consultez [à l’aide de certificats dans les Applications de sites Web Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Ajouter un certificat de tooKey coffre en tant que secret** au lieu de charger votre certificat de toohello service d’application Web directement, vous pouvez stocker dans le coffre de clés en tant que secret et le déployer à partir de là. Il s’agit d’un processus en deux étapes est décrite dans hello suivant le billet de blog, [déploiement Azure certificat l’application Web via le coffre de clés](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Étapes suivantes
Pour les références de programmation, consultez la page [Référence de l'API cliente C# du coffre de clés](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
