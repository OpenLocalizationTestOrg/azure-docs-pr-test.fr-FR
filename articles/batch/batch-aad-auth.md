---
title: solutions de service Azure Batch aaaUse Azure Active Directory tooauthenticate | Documents Microsoft
description: "Traitement par lots prend en charge Azure AD pour l’authentification à partir de hello service Batch."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Authentification de solutions de service Batch avec Active Directory

Azure Batch prend en charge l’authentification avec [Azure Active Directory][aad_about] (Azure AD). Azure AD est le service Microsoft de gestion des répertoires et des identités basé sur le cloud mutualisé. Azure lui-même utilise Azure AD tooauthenticate ses clients, les administrateurs de service et les utilisateurs professionnels.

Lorsque vous utilisez l’authentification Azure AD avec Azure Batch, vous pouvez vous authentifier de deux manières :

- À l’aide de **l’authentification intégrée** tooauthenticate un utilisateur interagit avec l’application hello. Une application à l’aide de l’authentification intégrée de collecte des informations d’identification d’un utilisateur et utilise ces informations d’identification tooauthenticate accéder tooBatch à des ressources.
- En utilisant un **principal du service** tooauthenticate une application sans assistance. Un principal de service définit les stratégie hello et les autorisations pour une application dans l’application de commande toorepresent hello lors de l’accès aux ressources lors de l’exécution.

toolearn en savoir plus sur Azure AD, consultez hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).

## <a name="authentication-and-pool-allocation-mode"></a>Authentification et mode d’allocation de pool

Lorsque vous créez un compte Batch, vous pouvez spécifier où les pools créés pour ce compte doivent être alloués. Vous pouvez choisir les pools de tooallocate dans l’abonnement au service de traitement par lots hello par défaut ou dans un abonnement de l’utilisateur. Votre choix affecte la façon dont vous authentifier tooresources d’accès de ce compte.

- **Abonnement au service Batch**. Par défaut, les pools Batch sont alloués dans un abonnement au service Batch. Si vous choisissez cette option, vous pouvez vous authentifier tooresources d’accès de ce compte à l’aide [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) ou auprès d’Azure AD.
- **Abonnement utilisateur.** Vous pouvez choisir des pools de lot tooallocate dans un abonnement de l’utilisateur que vous spécifiez. Si vous choisissez cette option, vous devez vous authentifier auprès d’Azure AD.

## <a name="endpoints-for-authentication"></a>Points de terminaison pour l’authentification

applications de traitement par lots tooauthenticate avec Azure AD, vous devez tooinclude certains points de terminaison connus dans votre code.

### <a name="azure-ad-endpoint"></a>Point de terminaison Azure AD

Hello base point de terminaison autorité Azure AD est :

`https://login.microsoftonline.com/`

tooauthenticate avec Azure AD, vous utilisez ce point de terminaison avec l’ID de client hello (ID de répertoire). ID de client Hello identifie hello toouse de locataire Azure AD pour l’authentification. tooretrieve hello ID client, suivez les étapes de hello décrites dans [obtenir l’ID hello pour Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> point de terminaison spécifiques du client Hello est requis lorsque vous authentifiez à l’aide d’un principal de service. 
> 
> point de terminaison spécifiques du client Hello est facultatif lorsque vous authentifiez à l’aide de l’authentification intégrée, mais recommandé. Toutefois, vous pouvez également utiliser point de terminaison commun hello Azure AD. point de terminaison commun Hello fournit des informations d’identification génériques collecte interface lorsqu’un client spécifique n’est fourni. point de terminaison commun Hello est `https://login.microsoftonline.com/common`.
>
>

Pour plus d’informations sur les points de terminaison Azure AD, consultez [Scénarios d’authentification pour Azure AD][aad_auth_scenarios].

### <a name="batch-resource-endpoint"></a>Point de terminaison de ressource Batch

Hello d’utilisation **point de terminaison de ressources Azure Batch** tooacquire un jeton d’authentification des demandes de service de traitement par lots toohello :

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>Inscrire votre application avec un client

Hello première étape à l’aide d’Azure AD tooauthenticate consiste à inscrire votre application dans un locataire Azure AD. Enregistrement de votre application vous permet de toocall hello Azure [bibliothèque d’authentification Active Directory] [ aad_adal] (ADAL) à partir de votre code. Hello ADAL fournit une API pour l’authentification auprès d’Azure AD à partir de votre application. Enregistrement de votre application est obligatoire si vous envisagez de l’authentification intégrée de toouse ou un principal de service.

Lorsque vous inscrivez votre application, vous fournissez des informations concernant votre tooAzure application AD. Azure AD puis fournit un ID d’application que vous utilisez tooassociate votre application auprès d’Azure AD lors de l’exécution. toolearn savoir plus sur les ID d’application hello, consultez [Application et les objets principal du service dans Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

tooregister votre application de traitement par lots, suivez les étapes hello Bonjour [Ajout d’une Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section [intégration d’applications avec Azure Active Directory][aad_integrate]. Si vous inscrivez votre application comme une Application Native, vous pouvez spécifier n’importe quel URI valide pour hello **URI de redirection**. Il n’a pas besoin toobe un point de terminaison réel.

Une fois que vous avez enregistré votre application, vous verrez l’ID de l’application hello :

![Inscrire votre application Batch auprès d’Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

Pour plus d’informations sur l’inscription d’une application avec Azure AD, consultez [Scénarios d’authentification pour Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).

## <a name="get-hello-tenant-id-for-your-active-directory"></a>Obtenir l’ID hello pour votre annuaire Active Directory

ID de client Hello identifie le locataire Azure AD hello qui fournit l’application tooyour de services d’authentification. tooget hello ID client, procédez comme suit :

1. Bonjour portail Azure, sélectionnez votre annuaire Active Directory.
2. Cliquez sur **Propriétés**.
3. Copier la valeur GUID hello fourni pour l’ID de répertoire hello. Cette valeur est également appelée ID de client hello.

![Copiez l’ID de répertoire hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>Utiliser l’authentification intégrée

tooauthenticate avec une authentification intégrée, vous devez toogrant votre toohello de tooconnect autorisations application API de service de traitement par lots. Cette étape permet à votre application tooauthenticate appelle toohello lot service API avec Azure AD.

Une fois que vous avez [inscrit votre application](#register-your-application-with-an-azure-ad-tenant), suivez ces étapes dans hello Azure toogrant portail il accéder au service de traitement par lots toohello :

1. Dans le volet de navigation gauche hello Hello portail Azure, choisissez **plus Services**, cliquez sur **inscriptions d’application**.
2. Recherchez le nom hello de votre application dans la liste de hello d’inscriptions d’application :

    ![Rechercher le nom de votre application](./media/batch-aad-auth/search-app-registration.png)

3. Ouvrez hello **paramètres** panneau pour votre application. Bonjour **l’accès aux API** section, sélectionnez **autorisations requises**.
4. Bonjour **autorisations requises** panneau, cliquez sur hello **ajouter** bouton.
5. À l’étape 1, recherchez hello API de lot. Recherche de chacune de ces chaînes jusqu'à ce que vous trouviez hello API :
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. Les locataires Azure AD les plus récents peuvent utiliser ce nom.
    3. **ddbf3205-c6bd-46AE-8127-60eb93363864** ID de hello pour hello API de lot. 
6. Une fois que vous trouvez hello API de lot, sélectionnez-la, puis cliquez sur hello **sélectionnez** bouton.
6. À l’étape 2, sélectionnez hello case ensuite trop**Service de traitement par lots Azure accès** et cliquez sur hello **sélectionnez** bouton.
7. Cliquez sur hello **fait** bouton.

Hello **autorisations requises** panneau maintenant indique que votre application Azure AD a accès tooboth ADAL et hello API de service de traitement par lots. Les autorisations sont accordées automatiquement tooADAL lorsque vous enregistrez tout d’abord votre application auprès d’Azure AD.

![Accorder des autorisations d’API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>Utiliser un principal de service 

tooauthenticate une application qui s’exécute sans assistance, vous utilisez un principal de service. Une fois que vous avez enregistré votre application, procédez comme suit dans hello tooconfigure portail Azure principal d’un service :

1. Demandez une clé secrète pour votre application.
2. Affecter une application de tooyour rôle RBAC.

### <a name="request-a-secret-key-for-your-application"></a>Demander une clé secrète pour votre application

Lorsque votre application s’authentifie avec un principal de service, il envoie l’ID de l’application hello et un tooAzure clé secrète AD. Vous devez toocreate et copiez hello toouse de clé secrète à partir de votre code.

Suivez ces étapes dans hello portail Azure :

1. Dans le volet de navigation gauche hello Hello portail Azure, choisissez **plus Services**, cliquez sur **inscriptions d’application**.
2. Recherchez le nom hello de votre application dans la liste de hello d’inscriptions de l’application.
3. Hello d’affichage **paramètres** panneau. Bonjour **l’accès aux API** section, sélectionnez **clés**.
4. toocreate une clé, entrez une description pour la clé de hello. Sélectionnez ensuite une durée de clé hello d’un ou deux ans. 
5. Cliquez sur hello **enregistrer** bouton toocreate et afficher la clé de hello. Copier hello valeur de clé tooa lieu sûr, car vous ne serez pas en mesure de tooaccess à nouveau après que vous laissez le panneau de hello. 

    ![Créer une clé secrète](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>Affecter une application de tooyour rôle RBAC

tooauthenticate avec un principal de service, vous devez tooassign une application de tooyour rôle RBAC. Procédez comme suit :

1. Bonjour portail Azure, accédez à toohello du compte Batch utilisé par votre application.
2. Bonjour **paramètres** panneau pour le compte Batch hello, sélectionnez **contrôle d’accès (IAM)**.
3. Cliquez sur hello **ajouter** bouton. 
4. À partir de hello **rôle** liste déroulante, choisissez soit hello _collaborateur_ ou _lecteur_ rôle pour votre application. Pour plus d’informations sur ces rôles, consultez [prise en main le contrôle d’accès en fonction du rôle Bonjour Azure portal](../active-directory/role-based-access-control-what-is.md).  
5. Bonjour **sélectionnez** , entrez le nom hello de votre application. Sélectionnez votre application à partir de la liste de hello, puis cliquez sur **enregistrer**.

Votre application doit maintenant apparaître dans vos paramètres de contrôle d’accès avec un rôle RBAC qui lui est attribué. 

![Affecter une application de tooyour rôle RBAC](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>Obtenir l’ID hello pour Azure Active Directory

ID de client Hello identifie le locataire Azure AD hello qui fournit l’application tooyour de services d’authentification. tooget hello ID client, procédez comme suit :

1. Bonjour portail Azure, sélectionnez votre annuaire Active Directory.
2. Cliquez sur **Propriétés**.
3. Copier la valeur GUID hello fourni pour l’ID de répertoire hello. Cette valeur est également appelée ID de client hello.

![Copiez l’ID de répertoire hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>Exemples de code

les exemples de code Hello dans cette section montrent comment tooauthenticate avec Azure AD à l’aide de l’authentification intégrée et avec un principal de service. Ces exemples de code utilisent .NET, mais les concepts de hello sont similaires pour d’autres langues.

> [!NOTE]
> Un jeton d’authentification Azure AD expire au bout d’une heure. Lorsque vous utilisez une durée de vie longue **BatchClient** de l’objet, nous vous recommandons de récupération d’un jeton à partir de la bibliothèque ADAL sur tooensure de chaque demande, vous devez toujours un jeton valide. 
>
>
> tooachieve dans .NET, écrivez une méthode qui Récupère hello jeton d’Azure AD et qu’il passe ce tooa méthode **BatchTokenCredentials** objet en tant que délégué. méthode de délégué Hello est appelée sur chaque tooensure service Batch toohello demande un jeton valide fourni. Par défaut, ADAL met en cache des jetons pour qu’un nouveau jeton soit récupéré à partir d’Azure AD uniquement lorsque cela est nécessaire. Pour plus d’informations sur les jetons dans Azure AD, consultez [Scénarios d’authentification pour Azure AD][aad_auth_scenarios].
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>Exemple de code : utilisation de l’authentification intégrée Azure AD avec Batch .NET

tooauthenticate avec l’authentification intégrée à partir de lot .NET, hello de référence [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package et hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.

Suivants de hello `using` instructions dans votre code :

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

ID de client hello de référence point de terminaison Azure AD dans votre code, y compris hello tooretrieve hello ID client, suivez les étapes de hello décrites dans [obtenir l’ID hello pour Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Référence de point de terminaison de la ressource de service de hello lot :

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Référencez votre compte Batch :

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Spécifiez l’ID d’application hello (ID client) pour votre application. ID de l’application Hello est disponible à partir de votre inscription d’une application Bonjour portail Azure :

```csharp
private const string ClientId = "<application-id>";
```

Copiez également l’URI que vous avez spécifié au cours du processus d’inscription de hello de redirection hello. redirection Hello QU'URI spécifié dans votre code doit correspondre à l’URI que vous avez fourni lorsque vous avez inscrit l’application hello de redirection hello :

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Écrire un jeton d’authentification rappel méthode tooacquire hello d’Azure AD. Hello **GetAuthenticationTokenAsync** appels de méthode de rappel indiqué ici tooauthenticate ADAL un utilisateur qui interagit avec l’application hello. Hello **AcquireTokenAsync** méthode fournie par la bibliothèque ADAL invites hello leurs informations d’identification utilisateur et application hello passe une fois les utilisateurs hello fournit les (sauf si elle a déjà mis en cache les informations d’identification) :

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

Construire un **BatchTokenCredentials** objet qui prend le délégué hello en tant que paramètre. Utilisez ces informations d’identification tooopen un **BatchClient** objet. Vous pouvez l’utiliser **BatchClient** objet pour les opérations suivantes sur hello service Batch :

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>Exemple de code : utilisation d’un principal de service Azure AD avec Batch .NET

tooauthenticate avec un principal de service à partir de lot .NET, hello de référence [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package et hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.

Suivants de hello `using` instructions dans votre code :

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

ID de client hello de référence point de terminaison Azure AD dans votre code, y compris hello Lorsque vous utilisez un principal de service, vous devez indiquer un point de terminaison spécifique du client. tooretrieve hello ID client, suivez les étapes de hello décrites dans [obtenir l’ID hello pour Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Référence de point de terminaison de la ressource de service de hello lot :  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Référencez votre compte Batch :

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Spécifiez l’ID d’application hello (ID client) pour votre application. ID de l’application Hello est disponible à partir de votre inscription d’une application Bonjour portail Azure :

```csharp
private const string ClientId = "<application-id>";
```

Spécifiez la clé secrète hello que vous avez copié à partir de hello portail Azure :

```csharp
private const string ClientKey = "<secret-key>";
```

Écrire un jeton d’authentification rappel méthode tooacquire hello d’Azure AD. Hello **GetAuthenticationTokenAsync** méthode de rappel ci-après appelle la bibliothèque ADAL pour l’authentification en mode sans assistance :

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

Construire un **BatchTokenCredentials** objet qui prend le délégué hello en tant que paramètre. Utilisez ces informations d’identification tooopen un **BatchClient** objet. Vous pouvez ensuite utiliser qui **BatchClient** objet pour les opérations suivantes sur hello service Batch :

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur Azure AD, consultez hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/). Approfondie exemples montrant comment toouse ADAL sont disponibles dans hello [exemples de Code Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliothèque.

toolearn savoir plus sur les principaux de service, consultez [Application et les objets principal du service dans Azure Active Directory](../active-directory/develop/active-directory-application-objects.md). un principal de service à l’aide de toocreate hello Azure portail, consultez [utiliser une application de portail toocreate Active Directory et de principal du service qui peut accéder aux ressources](../resource-group-create-service-principal-portal.md). Vous pouvez également créer un principal de service avec PowerShell ou Azure CLI. 

les applications de gestion par lots tooauthenticate à l’aide d’Azure AD, consultez [des solutions de gestion de traitement par lots s’authentifier avec Active Directory](batch-aad-auth-management.md). 

[aad_about]: ../active-directory/active-directory-whatis.md "Qu’est-ce qu’Azure Active Directory ?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scénarios d’authentification pour Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Intégration d’applications dans Azure Active Directory"
[azure_portal]: http://portal.azure.com
