---
title: "identité aaaCreate pour une application Azure avec Azure CLI | Documents Microsoft"
description: "Décrit comment contrôlent les toouse CLI d’Azure toocreate une application Azure Active Directory et principal du service et accordez il accéder tooresources via l’accès en fonction du rôle. Il montre comment application tooauthenticate avec un mot de passe ou un certificat."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>Utilisez Azure CLI toocreate une ressources tooaccess principal du service

Lorsque vous avez une application ou un script nécessitant des ressources de tooaccess, vous pouvez configurer une identité pour l’application hello et authentifier l’application hello avec ses propres informations d’identification. Cette identité est connue en tant que principal de service. Cette approche vous permet d’effectuer les opérations suivantes :

* Affecter des autorisations identité d’application toohello différents de vos propres autorisations. En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo.
* Utilisez un certificat pour l’authentification lors de l’exécution d’un script sans assistance.

Cet article vous montre comment toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset d’un toorun application sous ses propres informations d’identification et l’identité. Installer la version la plus récente de hello [Azure CLI 1.0](../cli-install-nodejs.md) toomake que votre environnement correspond aux exemples hello dans cet article.

## <a name="required-permissions"></a>Autorisations requises
toocomplete cette rubrique, vous devez disposer des autorisations suffisantes dans Azure Active Directory et votre abonnement Azure. Plus précisément, vous devez être en mesure de toocreate une application Bonjour Azure Active Directory et affecter des rôle tooa principal du service hello. 

Hello toocheck de façon plus simple si votre compte dispose des autorisations adéquates est via le portail de hello. Consultez [Vérifier l’autorisation requise dans le portail](resource-group-create-service-principal-portal.md#required-permissions).

Maintenant, soit poursuivre tooa section [mot de passe](#create-service-principal-with-password) ou [certificat](#create-service-principal-with-certificate) l’authentification.

## <a name="create-service-principal-with-password"></a>Créer un principal du service avec un mot de passe
Dans cette section, vous effectuez hello étapes toocreate hello application AD avec un mot de passe et assigner de principal du service toohello hello lecture du rôle.

1. Tooyour compte de connexion.
   
   ```azurecli
   azure login
   ```
2. toocreate une identité de l’application, fournir nom hello de l’application hello et un mot de passe, comme indiqué dans hello de commande suivante :
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   nouveau service Hello principal est retourné. Hello, Id d’objet est nécessaire lors de l’octroi d’autorisations. guid Hello répertorié par hello noms principaux de Service est nécessaire lors de la connexion. Ce guid est hello même valeur que l’id de l’application hello. Dans les exemples d’applications hello, cette valeur est désignée tooas hello `Client ID`. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. Accorder des autorisations de principal de service hello sur votre abonnement. Dans cet exemple, vous ajoutez hello service principal toohello rôle Lecteur, qui accorde l’autorisation tooread toutes les ressources dans l’abonnement de hello. Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md). Pour le paramètre objectid de hello, fournir hello Id d’objet que vous avez utilisé lors de la création d’application hello. Avant d’exécuter cette commande, vous devez laissez-lui du temps hello de nouveau service principal toopropagate dans Azure Active Directory. Lorsque vous exécutez ces commandes manuellement, en général il s’est écoulé suffisamment de temps entre les tâches. Dans un script, vous devez ajouter un toosleep étape entre commandes hello (comme `sleep 15`). Si vous voyez qu'un hello indiquant erreur principal n’existe pas dans le répertoire de hello, réexécutez la commande hello.
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
Et voilà ! Votre application Active Directory et votre principal du service sont maintenant configurés. section suivante de Hello vous montre comment toolog avec hello des informations d’identification via l’interface CLI d’Azure. Si vous souhaitez que les informations d’identification de toouse hello dans votre application de code, il est inutile toocontinue avec cette rubrique. Vous pouvez également accéder directement toohello [exemples d’applications](#sample-applications) pour obtenir des exemples de connexion avec votre id d’application et le mot de passe. 

### <a name="provide-credentials-through-azure-cli"></a>Fournir des informations d’identification via Azure CLI
Maintenant, vous devez toolog dans en tant qu’opérations de tooperform application hello.

1. Chaque fois que vous êtes connecté en tant que service principal, vous avez besoin d’id de client hello tooprovide du répertoire de hello pour votre application AD. Un locataire est une instance d’Azure Active Directory. id de client tooretrieve hello pour votre abonnement actuellement authentifié, utilisez :
   
   ```azurecli
   azure account show
   ```
   
   Résultat :
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     Si vous avez besoin d’id de client hello tooget d’un autre abonnement, utilisez hello de commande suivante :
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. Si vous devez tooretrieve hello client id toouse pour la connexion, utilisez :
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     toouse de valeur Hello pour la connexion est un guid hello répertoriée dans les noms principaux de service hello.
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. Ouvrez une session en tant que principal du service hello.
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    Vous êtes invité au mot de passe hello. Fournissent un mot de passe hello spécifié lors de la création d’application hello AD.
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

Vous êtes désormais authentifié en tant que principal du service hello de principal du service hello que vous avez créé.

Ou bien, vous pouvez appeler des opérations REST à partir de toolog de ligne de commande hello dans. À partir de la réponse d’authentification hello, vous pouvez récupérer le jeton d’accès hello pour une utilisation avec d’autres opérations. Pour obtenir un exemple de la récupération du jeton d’accès hello en appelant les opérations REST, consultez [générer un jeton d’accès](resource-manager-rest-api.md#generating-an-access-token).

## <a name="create-service-principal-with-certificate"></a>Créer un principal du service avec un certificat
Dans cette section, vous les étapes hello pour :

* créer un certificat auto-signé ;
* créer hello application AD avec hello et de certificat principal de service hello
* affecter le principal du service toohello hello lecture du rôle

toocomplete ces étapes, vous devez avoir [OpenSSL](http://www.openssl.org/) installé.

1. Vous pouvez créer un certificat auto-signé.
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. Hello précédant étape créé deux fichiers - privkey.pem et cert.pem. Combiner les clés publiques et privées hello dans un seul fichier.

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. Ouvrez hello **examplecert.pem** de fichiers et recherchez hello longue séquence de caractères entre **---BEGIN CERTIFICATE---** et **---END CERTIFICATE---**. Copiez les données de certificat hello. Vous passez ces données en tant que paramètre lors de la création de hello principal du service.

4. Tooyour compte de connexion.

   ```azurecli
   azure login
   ```
5. principal du service toocreate hello, fournir nom hello de l’application hello et les données de certificat hello, comme indiqué dans hello de commande suivante :
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   nouveau service Hello principal est retourné. Hello, Id d’objet est nécessaire lors de l’octroi d’autorisations. guid Hello répertorié par hello noms principaux de Service est nécessaire lors de la connexion. Ce guid est hello même valeur que l’id de l’application hello. Dans les exemples d’applications hello, cette valeur est désignée tooas hello ID Client. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. Accorder des autorisations de principal de service hello sur votre abonnement. Dans cet exemple, vous ajoutez hello service principal toohello rôle Lecteur, qui accorde l’autorisation tooread toutes les ressources dans l’abonnement de hello. Pour les autres rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md). Pour le paramètre objectid de hello, fournir hello Id d’objet que vous avez utilisé lors de la création d’application hello. Avant d’exécuter cette commande, vous devez laissez-lui du temps hello de nouveau service principal toopropagate dans Azure Active Directory. Lorsque vous exécutez ces commandes manuellement, en général il s’est écoulé suffisamment de temps entre les tâches. Dans un script, vous devez ajouter un toosleep étape entre commandes hello (comme `sleep 15`). Si vous voyez qu'un hello indiquant erreur principal n’existe pas dans le répertoire de hello, réexécutez la commande hello.
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>Fournir un certificat via un script Azure CLI automatisé
Maintenant, vous devez toolog dans en tant qu’opérations de tooperform application hello.

1. Chaque fois que vous êtes connecté en tant que service principal, vous avez besoin d’id de client hello tooprovide du répertoire de hello pour votre application AD. Un locataire est une instance d’Azure Active Directory. id de client tooretrieve hello pour votre abonnement actuellement authentifié, utilisez :
   
   ```azurecli
   azure account show
   ```
   
   Résultat :
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   Si vous avez besoin d’id de client hello tooget d’un autre abonnement, utilisez hello de commande suivante :
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve hello empreinte numérique du certificat et supprimez les caractères inutiles, utilisez :
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   Vous obtenez alors une valeur d’empreinte semblable à ce qui suit :
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. Si vous devez tooretrieve hello client id toouse pour la connexion, utilisez :
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   toouse de valeur Hello pour la connexion est un guid hello répertoriée dans les noms principaux de service hello.
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. Ouvrez une session en tant que principal du service hello.
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

Vous êtes désormais authentifié en tant que principal de service hello pour hello application Azure Active Directory que vous avez créé.

## <a name="change-credentials"></a>Modifier les informations d’identification

informations d’identification de hello toochange pour une application AD, soit en raison d’une compromission de la sécurité ou une date d’expiration des informations d’identification, utilisent `azure ad app set`.

toochange un mot de passe, utilisez :

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

toochange une valeur de certificat, utilisez :

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>Déboguer

Vous pouvez rencontrer les erreurs suivantes lors de la création d’un principal de service de hello :

* **« Authentication_Unauthorized »** ou **« aucun abonnement ne trouvé dans le contexte de hello. »** -Vous recevez cette erreur lorsque votre compte ne dispose pas de hello [autorisations requises](#required-permissions) sur hello Azure Active Directory tooregister une application. En règle générale, vous obtenez cette erreur lorsque seuls des utilisateurs administrateurs dans votre annuaire Azure Active Directory peuvent inscrire des applications et que votre compte n’est pas un compte d’administrateur. Demandez à votre tooeither administrateur affecter le rôle administrateur tooan ou tooenable utilisateurs tooregister applications.

* Votre compte **« n’a pas action de tooperform d’autorisation 'Microsoft.Authorization/roleAssignments/write' sur l’étendue '/ subscriptions / {guid}'. »**  -Vous recevez cette erreur lorsque votre compte n’a pas suffisamment autorisations tooassign une identité tooan du rôle. Demandez à votre tooadd d’administrateur abonnement rôle administrateur de l’accès tooUser.

## <a name="sample-applications"></a>Exemples d'applications
Pour plus d’informations sur la connexion en tant qu’application hello via différentes plateformes, consultez :

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.JS](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des instructions détaillées sur l’intégration d’une application dans Azure pour la gestion des ressources, consultez [tooauthorization du guide du développeur avec hello API Azure Resource Manager](resource-manager-api-authentication.md).
* tooget plus d’informations sur l’utilisation de certificats et CLI d’Azure, consultez [l’authentification basée sur le certificat avec les principaux du Service Azure à partir de la ligne de commande Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx). 
* Pour obtenir la liste des actions disponibles qui peuvent être accordées ou refusées toousers, consultez [opérations du fournisseur de ressources Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).
