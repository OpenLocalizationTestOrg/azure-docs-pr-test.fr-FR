---
title: solutions de gestion par lots tooauthenticate aaaUse Azure Active Directory | Documents Microsoft
description: "Applications générées avec le Gestionnaire de ressources Azure et le fournisseur de ressources de traitement par lots hello s’authentifier auprès d’Azure AD."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>Authentification de solutions de gestion Batch avec Active Directory

Les applications qui appellent le service de gestion de traitement par lots Azure hello s’authentifier avec [Azure Active Directory] [ aad_about] (Azure AD). Azure AD est le service Microsoft de gestion des répertoires et des identités basé sur le cloud mutualisé. Azure lui-même utilise Azure AD pour l’authentification de hello de ses clients, les administrateurs de service et les utilisateurs professionnels.

bibliothèque de Batch Management .NET Hello expose les types pour l’utilisation des comptes Batch, des clés de compte, des applications et des packages d’applications. bibliothèque de Batch Management .NET Hello est un client de fournisseur de ressources Azure et est utilisée conjointement avec [Azure Resource Manager] [ resman_overview] toomanage ces ressources par programme. Azure AD est tooauthenticate requis les demandes effectuées via n’importe quel client de fournisseur de ressources Azure, y compris hello Batch Management .NET bibliothèque et [Azure Resource Manager][resman_overview].

Dans cet article, nous explorons à l’aide de tooauthenticate Azure AD à partir d’applications qui utilisent la bibliothèque de Batch Management .NET hello. Nous montrons comment toouse Azure AD tooauthenticate un administrateur de l’abonnement ou un coadministrateur, à l’aide intégrée d’authentification. Nous utilisons hello [AccountManagment] [ acct_mgmt_sample] exemple de projet, disponible sur GitHub, toowalk via l’utilisation d’Azure AD avec la bibliothèque de Batch Management .NET hello.

toolearn savoir plus sur à l’aide de la bibliothèque de Batch Management .NET hello et hello AccountManagement exemple, consultez [comptes Batch de gérer et quotas avec la bibliothèque cliente de gestion par lots hello pour .NET](batch-management-dotnet.md).

## <a name="register-your-application-with-azure-ad"></a>Inscrire votre application auprès d’Azure AD

Bonjour Azure [bibliothèque d’authentification Active Directory] [ aad_adal] (ADAL) fournit une interface de programmation de tooAzure AD pour les utiliser dans vos applications. toocall ADAL à partir de votre application, vous devez inscrire votre application dans un locataire Azure AD. Lorsque vous inscrivez votre application, vous fournissez Azure AD avec des informations relatives à votre application, y compris son nom dans le locataire Azure AD de hello. Azure AD puis fournit un ID d’application que vous utilisez tooassociate votre application auprès d’Azure AD lors de l’exécution. toolearn savoir plus sur les ID d’application hello, consultez [Application et les objets principal du service dans Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

tooregister hello AccountManagement exemple d’application, suivez les étapes de hello Bonjour [Ajout d’une Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section [intégration d’applications avec Azure Active Directory] [ aad_integrate]. Spécifiez **Application cliente Native** de type hello d’application. Hello industry standard URI OAuth 2.0 hello **URI de redirection** est `urn:ietf:wg:oauth:2.0:oob`. Toutefois, vous pouvez spécifier n’importe quel URI valide (tel que `http://myaccountmanagementsample`) pour hello **URI de redirection**, comme il n’a pas besoin de toobe un point de terminaison réel :

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

Après avoir terminé le processus d’inscription de hello, vous voyez les ID de l’application hello et hello ID d’objet (principal du service) répertorié pour votre application.  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>Accorder hello API Azure Resource Manager accès tooyour application

Ensuite, vous devez tooyour d’accès toodelegate toohello application API Azure Resource Manager. Identificateur Hello Azure AD pour hello API du Gestionnaire de ressources est **API de gestion Windows Azure**.

Suivez ces étapes dans hello portail Azure :

1. Dans le volet de navigation gauche hello Hello portail Azure, choisissez **plus Services**, cliquez sur **inscriptions d’application**, puis cliquez sur **ajouter**.
2. Recherchez le nom hello de votre application dans la liste de hello d’inscriptions d’application :

    ![Rechercher le nom de votre application](./media/batch-aad-auth-management/search-app-registration.png)

3. Hello d’affichage **paramètres** panneau. Bonjour **l’accès aux API** section, sélectionnez **autorisations requises**.
4. Cliquez sur **ajouter** tooadd une nouvelle autorisation requise. 
5. Dans l’étape 1, entrez **API de gestion Windows Azure**, sélectionnez cette API à partir de la liste de hello des résultats, cliquez sur hello **sélectionnez** bouton.
6. À l’étape 2, sélectionnez hello case ensuite trop**modèle de déploiement classique d’accès Azure en tant qu’utilisateurs de l’organisation**, puis cliquez sur hello **sélectionnez** bouton.
7. Cliquez sur hello **fait** bouton.

Hello **autorisations requises** panneau maintenant montre que les applications de tooyour autorisations sont accordées tooboth hello ADAL et l’API du Gestionnaire de ressources. Les autorisations sont accordées tooADAL par défaut lorsque vous enregistrez tout d’abord votre application auprès d’Azure AD.

![Déléguer des autorisations toohello API Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Points de terminaison Azure AD

tooauthenticate vos solutions de gestion par lots avec Azure AD, vous aurez besoin de deux points de terminaison connus.

- Hello **point de terminaison Azure AD commun** fournit des informations d’identification génériques collecte interface lorsqu’un client spécifique n’est pas fourni, comme dans les cas de hello de l’authentification intégrée :

    `https://login.microsoftonline.com/common`

- Hello **point de terminaison Azure Resource Manager** est tooacquire utilisé un jeton d’authentification de service de gestion des demandes toohello Batch :

    `https://management.core.windows.net/`

Hello AccountManagement, exemple d’application définit des constantes pour ces points de terminaison. Laissez ces constantes telles quelles :

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>Référencer votre ID d’application 

Votre application cliente utilise tooaccess de ID (également désignée tooas hello client ID) d’application hello Azure AD lors de l’exécution. Une fois que vous avez enregistré votre application Bonjour portail Azure, mettre à jour votre code toouse hello ID de l’application d’Azure AD pour votre application inscrite. Bonjour AccountManagement, exemple d’application, copiez votre ID d’application à partir de la constante appropriée de hello toohello portail Azure :

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
Copiez également l’URI que vous avez spécifié au cours du processus d’inscription de hello de redirection hello. redirection Hello QU'URI spécifié dans votre code doit correspondre à l’URI que vous avez fourni lorsque vous avez inscrit l’application hello de redirection hello.

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>Acquérir un jeton d’authentification Azure AD

Une fois que vous inscrivez hello AccountManagement exemple dans le locataire Azure AD de hello et mettre à jour les exemples de code source hello avec vos valeurs, exemple hello est tooauthenticate prêt à l’aide d’Azure AD. Lorsque vous exécutez exemple hello, hello ADAL tentatives tooacquire un jeton d’authentification. À ce stade, vous êtes invité à renseigner vos informations d’identification Microsoft : 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

Après avoir fourni vos informations d’identification, exemple d’application hello peut continuer tooissue authentifié demandes toohello service de gestion de traitement par lots. 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’exécution de hello [AccountManagement, exemple d’application][acct_mgmt_sample], consultez [comptes Batch de gérer et quotas avec la bibliothèque cliente de gestion par lots hello pour .NET](batch-management-dotnet.md).

toolearn en savoir plus sur Azure AD, consultez hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/). Approfondie exemples montrant comment toouse ADAL sont disponibles dans hello [exemples de Code Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliothèque.

applications de service de traitement par lots tooauthenticate à l’aide d’Azure AD, consultez [solutions de service de traitement par lots de s’authentifier auprès d’Active Directory](batch-aad-auth.md). 


[aad_about]: ../active-directory/active-directory-whatis.md "Qu’est-ce qu’Azure Active Directory ?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scénarios d’authentification pour Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Intégration d’applications dans Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
