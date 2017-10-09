---
title: "identité aaaCreate pour une application Azure dans le portail | Documents Microsoft"
description: "Décrit le mode d’accès des toocreate une application Azure Active Directory et le service principal qui peut être utilisé avec le contrôle d’accès basé sur rôle hello dans Azure Resource Manager toomanage tooresources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>Utilisez le portail toocreate une application Azure Active Directory et le principal du service qui peut accéder aux ressources

Lorsque vous avez une application qui doit tooaccess ou modifier des ressources, vous devez configurer une application Azure Active Directory (AD) et affecter tooit d’autorisations hello requis. Cette approche est préférable toorunning hello application vos propres informations d’identification, car :

* Vous pouvez affecter des autorisations identité d’application toohello différents de vos propres autorisations. En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo.
* Vous n’avez pas les informations d’identification de l’application toochange hello si vos responsabilités changent. 
* Vous pouvez utiliser une authentification de tooautomate certificat lors de l’exécution d’un script sans assistance.

Cette rubrique vous montre comment tooperform ces étapes via le portail de hello. Il se concentre sur une application à locataire unique où application hello est prévue toorun au sein d’une seule organisation. Les applications à locataire unique sont généralement utilisées pour les applications métier exécutées au sein de votre organisation.
 
## <a name="required-permissions"></a>Autorisations requises
toocomplete cette rubrique, vous devez disposer d’une application tooregister d’autorisations suffisantes à votre client Azure AD et affecter le rôle de tooa d’application hello dans votre abonnement Azure. Assurons-nous que vous avez hello autorisations appropriées tooperform ces étapes.

### <a name="check-azure-active-directory-permissions"></a>Vérifier les autorisations Azure Active Directory
1. Connectez-vous à tooyour compte Azure via hello [portail Azure](https://portal.azure.com).
2. Sélectionnez **Azure Active Directory**.

     ![sélectionner azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. Dans Azure Active Directory, sélectionnez **Paramètres utilisateur**.

     ![sélectionner les paramètres utilisateur](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. Vérifiez hello **inscriptions d’application** paramètre. Si défini trop**Oui**, les utilisateurs non administrateurs peuvent inscrire des applications AD. Ce paramètre signifie que n’importe quel utilisateur dans le locataire Azure AD de hello peut inscrire une application. Vous pouvez passer trop[autorisations d’abonnement Azure de vérifier](#check-azure-subscription-permissions).

     ![afficher les inscriptions d’applications](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. Si les inscriptions d’application hello paramètre est défini trop**non**, seuls les utilisateurs administrateurs peuvent inscrire des applications. Vous devez toocheck si votre compte est un administrateur de locataire Azure AD de hello. Sélectionnez **Vue d’ensemble** et **Rechercher un utilisateur** dans Tâches rapides.

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/find-user.png)
6. Recherchez votre compte et sélectionnez-le lorsque vous l’avez trouvé.

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/show-user.png)
7. Pour votre compte, sélectionnez **Rôle Directory**. 

     ![rôle directory](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. Affichez le rôle de répertoire qui vous a été affecté dans Azure AD. Si toohello rôle d’utilisateur est affecté à votre compte, mais hello paramètres d’inscription d’application (à partir des étapes précédentes de hello) est limitée tooadmin utilisateurs, demandez à votre tooeither administrateur affecter le rôle administrateur tooan ou tooenable utilisateurs tooregister applications.

     ![afficher le rôle](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>Vérifier les autorisations d’abonnement Azure
Dans votre abonnement Azure, votre compte doit avoir `Microsoft.Authorization/*/Write` tooassign un rôle tooa d’application AD d’accès. Cette action est accordée via hello [propriétaire](../active-directory/role-based-access-built-in-roles.md#owner) rôle ou [administrateur de l’accès utilisateur](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) rôle. Si votre compte est affecté toohello **collaborateur** rôle, vous n’avez pas les autorisations adéquates. Vous recevrez une erreur lors de la tentative de rôle de principal tooa tooassign hello service. 

toocheck vos autorisations d’abonnement :

1. Si vous ne sont pas déjà dans votre compte Azure AD à partir des étapes précédentes de hello, sélectionnez **Azure Active Directory** hello volet de gauche.

2. Recherchez votre compte Azure AD. Sélectionnez **Vue d’ensemble** et **Rechercher un utilisateur** dans Tâches rapides.

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/find-user.png)
2. Recherchez votre compte et sélectionnez-le lorsque vous l’avez trouvé.

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. Sélectionnez **Ressources Azure**.

     ![sélectionner des ressources](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. Afficher vos rôles sont affectés et déterminer si vous disposez des autorisations adéquates tooassign un rôle tooa d’application AD. Dans le cas contraire, demandez à votre tooadd d’administrateur abonnement rôle administrateur de l’accès tooUser. Utilisateur de hello hello suivant l’image, est rôle de propriétaire toohello attribué pour les deux abonnements, ce qui signifie que l’utilisateur dispose des autorisations adéquates. 

     ![afficher les autorisations](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>Créer une application Azure Active Directory
1. Connectez-vous à tooyour compte Azure via hello [portail Azure](https://portal.azure.com).
2. Sélectionnez **Azure Active Directory**.

     ![sélectionner azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. Sélectionnez **Inscriptions d’applications**.   

     ![sélectionner des inscriptions d’applications](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. Sélectionnez **Ajouter**.

     ![ajouter une application](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Fournissez un nom et une URL pour l’application hello. Sélectionnez **application Web / API** ou **natif** de type hello d’application, vous souhaitez toocreate. Après avoir défini les valeurs hello, sélectionnez **créer**.

     ![nommer l’application](./media/resource-group-create-service-principal-portal/create-app.png)

Vous avez créé votre application.

## <a name="get-application-id-and-authentication-key"></a>Obtenir un ID d’application et une clé d’authentification
Lors de la connexion par programme, vous devez hello ID pour votre application et une clé d’authentification. tooget ces valeurs, hello utilisation comme suit :

1. Dans **Inscriptions d’applications** dans Azure Active Directory, sélectionnez votre application.

     ![sélectionner une application](./media/resource-group-create-service-principal-portal/select-app.png)
2. Hello de copie **ID d’Application** et stockez-le dans votre code d’application. Hello applications Bonjour [exemples d’applications](#sample-applications) section font référence à valeur toothis en tant qu’id de client hello.

     ![ID CLIENT](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. toogenerate une clé d’authentification, sélectionnez **clés**.

     ![sélectionner des clés](./media/resource-group-create-service-principal-portal/select-keys.png)
4. Fournir une description de la clé de hello et une durée de clé de hello. Lorsque vous avez terminé, sélectionnez **Enregistrer**.

     ![enregistrer une clé](./media/resource-group-create-service-principal-portal/save-key.png)

     Après avoir enregistré la clé de hello, hello clé de hello est affichée. Copiez cette valeur, car vous sont pas en mesure de tooretrieve hello clé plus tard. Vous fournissez les valeur de clé hello hello application ID toolog dans en tant qu’application hello. Stockez la valeur de clé hello où votre application peut les récupérer.

     ![clé enregistrée](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>Obtenir l’ID de locataire
Lors de la connexion par programme, vous avez besoin d’ID de client hello toopass avec votre demande d’authentification. 

1. ID de client tooget hello, sélectionnez **propriétés** pour votre locataire Azure AD. 

     ![Sélectionnez les propriétés Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. Hello de copie **ID de répertoire**. Cette valeur est votre ID de locataire.

     ![ID client](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>Affecter l’application toorole
tooaccess des ressources dans votre abonnement, vous devez attribuer le rôle de tooa application hello. Décider quel rôle représente les autorisations de droite hello pour une application hello. toolearn sur les rôles disponibles de hello, consultez [RBAC : générées dans les rôles](../active-directory/role-based-access-built-in-roles.md).

Vous pouvez définir l’étendue de hello au niveau hello d’abonnement de hello, groupe de ressources ou ressource. Les autorisations sont héritées toolower des niveaux de portée. Par exemple, ajout d’un rôle de lecteur application toohello pour un groupe de ressources signifie qu’il peut lire toutes les ressources qu’il contient et groupe de ressources hello.

1. Accédez au niveau du toohello de portée qu'application hello tooassign vous le souhaitez. Par exemple, tooassign un rôle au niveau de l’étendue de l’abonnement hello, sélectionnez **abonnements**. Vous pouvez également sélectionner un groupe de ressources ou une ressource.

     ![sélectionner l'abonnement](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. Sélectionnez un abonnement spécifique (groupe de ressources ou ressource) tooassign hello application hello pour.

     ![sélectionner l’abonnement pour l’affectation](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. Sélectionnez **Contrôle d’accès (IAM)**.

     ![sélectionner l’accès](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. Sélectionnez **Ajouter**.

     ![sélectionner ajouter](./media/resource-group-create-service-principal-portal/select-add.png)
6. Sélectionnez le rôle hello vous souhaitez tooassign toohello application. Hello image suivante montre hello **lecteur** rôle.

     ![sélectionner un rôle](./media/resource-group-create-service-principal-portal/select-role.png)

8. Recherchez votre application et sélectionnez-la.

     ![rechercher une application](./media/resource-group-create-service-principal-portal/search-app.png)
9. Sélectionnez **OK** toofinish affectation hello rôle. Vous consultez votre application dans la liste de hello des utilisateurs affectés du rôle tooa pour cette étendue.

## <a name="log-in-as-hello-application"></a>Connectez-vous en tant qu’application hello

Votre application est maintenant configurée dans Azure Active Directory. Vous avez un ID et la clé toouse pour vous connecter en tant qu’application hello. application Hello rôle tooa qui lui donne certaines actions, qu'il peut effectuer. Pour plus d’informations sur la connexion en tant qu’application hello via différentes plateformes, consultez :

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [Interface de ligne de commande Azure](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.JS](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>Étapes suivantes
* tooset d’une application mutualisée, consultez [tooauthorization du guide du développeur avec hello API Azure Resource Manager](resource-manager-api-authentication.md).
* toolearn sur la spécification des stratégies de sécurité, consultez [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).  
* Pour obtenir la liste des actions disponibles qui peuvent être accordées ou refusées toousers, consultez [opérations du fournisseur de ressources Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).
