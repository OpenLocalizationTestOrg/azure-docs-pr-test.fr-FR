---
title: "aaaConfigure votre service de gestion des API à l’aide de Git - Azure | Documents Microsoft"
description: "Découvrez comment toosave et configurer votre configuration de service de gestion des API à l’aide de Git."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>Comment toosave et configurer votre configuration de service de gestion des API à l’aide de Git
> 
> 

Chaque instance de service de gestion des API gère une base de données de configuration qui contient des informations sur la configuration de hello et des métadonnées pour l’instance de service hello. Modifications peuvent être apportées à l’instance de service toohello en modifiant un paramètre dans le portail de publication hello, à l’aide d’une applet de commande PowerShell ou un appel d’API REST. En outre les méthodes toothese, vous pouvez également gérer votre configuration d’instance de service à l’aide de Git, permettant ainsi de scénarios de gestion de service tels que :

* Contrôle de version de la configuration : téléchargez et stockez différentes versions de votre configuration de service
* En bloc les modifications de configuration - apporter des modifications toomultiple des parties de votre configuration du service dans votre référentiel local et intégrer le serveur de toohello arrière de modifications de hello en une seule opération
* Chaîne d’outils Git et les flux de travail - familiers utiliser outils Git de hello et flux de travail que vous connaissez déjà

Hello suivant schéma montre une vue d’ensemble de tooconfigure de différentes façons hello votre instance de service de gestion des API.

![Configurer avec Git][api-management-git-configure]

Lorsque vous apportez des modifications service tooyour à l’aide du portail de publication hello, applets de commande PowerShell ou hello API REST, vous gérez votre base de données de configuration de service à l’aide de hello `https://{name}.management.azure-api.net` point de terminaison, comme indiqué dans le côté droit de hello du diagramme de hello. à gauche de Hello du diagramme de hello illustre comment vous pouvez gérer votre configuration de service à l’aide de Git et référentiel Git de votre service situé à `https://{name}.scm.azure-api.net`.

Hello suit fournit une vue d’ensemble de la gestion de votre instance de service de gestion des API à l’aide de Git.

1. Accéder à la configuration de Git dans votre service
2. Enregistrer votre référentiel Git tooyour de base de données de configuration service
3. Cloner l’ordinateur local du tooyour dépôt Git hello
4. Extraire le référentiel de dernière hello la machine locale de tooyour et validation et push référentiel tooyour arrière de modifications
5. Déployer les modifications de hello à partir de votre référentiel dans votre base de données de configuration de service

Cet article décrit comment tooenable et utiliser Git toomanage votre configuration de service et fournit une référence pour les fichiers de hello et des dossiers dans le référentiel Git de hello.

## <a name="access-git-configuration-in-your-service"></a>Accéder à la configuration de Git dans votre service
Vous pouvez rapidement afficher l’état hello de votre configuration Git en affichant l’icône de Git hello dans le coin supérieur droit de hello du portail de publication hello. Dans cet exemple, le message d’état hello indique qu’il n’y a référentiel toohello de modifications non enregistrées. Il s’agit, car la base de données de la configuration de service de hello gestion des API n’a pas encore été enregistré toohello référentiel.

![État de Git][api-management-git-icon-enable]

tooview et configurer vos paramètres de configuration Git, vous pouvez cliquez sur icône Git de hello, ou cliquez sur hello **sécurité** menu et accédez toohello **dépôt de Configuration** onglet.

![Activer GIT][api-management-enable-git]

> [!IMPORTANT]
> Les secrets ne sont pas définies comme propriétés seront stockées dans le référentiel de hello et restent dans son historique jusqu'à ce que vous désactivent et réactiver l’accès de Git. Propriétés fournissent un emplacement sécurisé de toomanage des valeurs de chaîne constante, y compris les clés secrètes, sur toutes les stratégies et de configuration de l’API, vous n’avez pas toostore directement dans vos instructions de stratégie. Pour plus d’informations, consultez [comment toouse des propriétés dans les stratégies de gestion des API Azure](api-management-howto-properties.md).
> 
> 

Pour plus d’informations sur l’activation ou désactivation Git l’accès à l’aide de hello API REST, consultez [activer ou désactiver l’accès Git à l’aide des API REST de hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>référentiel Git de toosave hello service configuration toohello
première étape de Hello avant le clonage du référentiel de hello est toosave hello capables de référentiel de toohello de configuration de service hello. Cliquez sur **enregistrer la configuration toorepository**.

![Enregistrer la configuration][api-management-save-configuration]

Apportez les modifications souhaitées sur l’écran de confirmation hello et cliquez sur **Ok** toosave.

![Enregistrer la configuration][api-management-save-configuration-confirm]

Après quelques instants configuration de hello est enregistrée et état de la configuration du référentiel de hello hello s’affiche, y compris la date de hello et l’heure de dernière modification de configuration hello et hello dernière synchronisation entre la configuration du service hello et hello espace de stockage.

![État de la configuration][api-management-configuration-status]

Une fois la configuration de hello est enregistrée toohello référentiel, il peut être cloné.

Pour plus d’informations sur la réalisation de cette opération à l’aide de hello API REST, consultez [configuration de la validation d’instantané à l’aide des API REST de hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>ordinateur local de tooclone hello référentiel tooyour
tooclone un référentiel, vous devez référentiel de tooyour hello URL, un nom d’utilisateur et un mot de passe. Hello nom d’utilisateur et les URL sont affichés haut hello Hello **dépôt de Configuration** onglet.

![Clonage Git][api-management-configuration-git-clone]

mot de passe Hello est généré au bas de hello de hello **dépôt de Configuration** onglet.

![Générer un mot de passe][api-management-generate-password]

toogenerate un mot de passe, commencez par vous assurer que hello **expiration** est défini toohello souhaité date d’expiration et l’heure, puis cliquez sur **générer le jeton**.

![Mot de passe][api-management-password]

> [!IMPORTANT]
> Notez ce mot de passe. Une fois que vous conservez ce mot de passe de hello de page ne s’affiche plus.
> 
> 

Hello suivant des exemples d’utilisation hello interpréteur de commandes Git outil à partir de [Git pour Windows](http://www.git-scm.com/downloads) mais vous pouvez utiliser n’importe quel outil Git qui vous sont familières.

Ouvrir votre outil de Git dans le dossier de votre choix hello et exécutez hello suivant commande tooclone hello git référentiel tooyour ordinateur local, à l’aide de la commande hello fournie par le portail de publication hello.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Fournir le nom d’utilisateur hello et le mot de passe lorsque vous y êtes invité.

Si vous recevez des erreurs, essayez de modifier votre `git clone` commande tooinclude hello nom d’utilisateur, comme indiqué dans hello l’exemple suivant.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Si cela fournit une erreur, essayez de mot de passe hello de commande hello de codage d’URL. Un moyen rapide toodo il s’agit de tooopen Visual Studio et de commande suivant de hello problème Bonjour **fenêtre exécution**. tooopen hello **fenêtre exécution**, ouvrez la solution ou le projet dans Visual Studio (ou créer une application console vide), puis choisissez **Windows**, **exécution** à partir de Hello **déboguer** menu.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

Utilisez le mot de passe de hello encodé en même temps que votre nom et le référentiel emplacement tooconstruct hello git commande utilisateur.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Une fois le référentiel de hello est cloné, vous pouvez afficher et utiliser dans votre système de fichiers local. Pour plus d’informations, consultez [Référence de la structure des fichiers et des dossiers du dépôt Git local](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate votre référentiel local avec la configuration de l’instance hello plus récente service
Si vous effectuez l’instance de service de gestion des API tooyour modifications dans le portail de publication hello ou à l’aide des API REST de hello, vous devez enregistrer ces référentiel toohello de modifications avant que vous pouvez mettre à jour votre référentiel local avec les modifications les plus récentes hello. toodo, cliquez sur **enregistrer la configuration toorepository** sur hello **dépôt de Configuration** onglet dans le portail de publication hello et puis exécutez hello suivant de commande dans votre référentiel local.

```
git pull
```

Avant d’exécuter `git pull` vous assurer que vous êtes dans le dossier de hello pour votre référentiel local. Si vous venez d’effectuer hello `git clone` commande, vous devez modifier le référentiel de tooyour hello active en exécutant une commande hello suivante.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>modifications toopush à partir de votre référentiel de serveur toohello dépôt local
toopush passe de votre référentiel de serveur toohello référentiel local, vous devez valider vos modifications et les transmettre toohello référentiel du serveur. toocommit vos modifications, ouvrez votre outil de commande Git, directory toohello du commutateur de votre référentiel local et hello du problème suivant les commandes.

```
git add --all
git commit -m "Description of your changes"
```

toopush tous hello valide toohello serveur, exécutez hello la commande suivante.

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy n’importe quelle instance du service de gestion des API service configuration modifications toohello
Une fois vos modifications locales sont validées et envoyées toohello référentiel du serveur, vous pouvez les déployer instance de service de gestion des API tooyour.

![Déployer][api-management-configuration-deploy]

Pour plus d’informations sur la réalisation de cette opération à l’aide de hello API REST, consultez [Git de déploiement change tooconfiguration de base de données à l’aide des API REST de hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Référence de la structure des fichiers et des dossiers du dépôt Git local
Hello fichiers et dossiers dans le référentiel git local de hello contiennent des informations de configuration de hello sur l’instance de service hello.

| Item | Description |
| --- | --- |
| Dossier api-management racine |Contient la configuration de niveau supérieur pour l’instance de service hello |
| Dossier apis |Contient la configuration hello pour les API de hello dans l’instance de service hello |
| Dossier groups |Contient la configuration de hello pour les groupes de hello dans l’instance de service hello |
| Dossier policies |Contient des stratégies de hello dans l’instance de service hello |
| Dossier portalStyles |Contient la configuration hello pour les personnalisations de portail de développement hello dans l’instance de service hello |
| Dossier products |Contient la configuration hello pour les produits hello dans l’instance de service hello |
| Dossier templates |Contient la configuration hello pour les modèles de messagerie hello dans l’instance de service hello |

Chaque dossier peut contenir un ou plusieurs fichiers et, dans certains cas, un ou plusieurs dossiers, par exemple un dossier par API, produit ou groupe. fichiers Hello dans chaque dossier sont spécifiques pour le type d’entité hello décrite par le nom du dossier hello.

| Type de fichier | Objectif |
| --- | --- |
| json |Informations de configuration sur l’entité correspondante de hello |
| html |Description de l’entité hello, souvent affiché dans le portail des développeurs hello |
| xml |Policy statements |
| css |Feuilles de style pour la personnalisation du portail des développeurs |

Ces fichiers peuvent être créés, supprimés, modifiés et gérés sur votre système de fichiers local, et les modifications de hello déployées toohello arrière de votre instance de service de gestion des API.

> [!NOTE]
> Bonjour entités suivantes ne figurent pas dans le référentiel Git de hello et ne peut pas être configurées à l’aide de Git.
> 
> * Utilisateurs
> * Abonnements
> * Propriétés
> * Entités du portail des développeur autres que les styles
> 
> 

### <a name="root-api-management-folder"></a>Dossier api-management racine
racine de Hello `api-management` dossier contient un `configuration.json` fichier qui contient le niveau supérieur d’informations sur l’instance de service hello Bonjour suivant le format.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

Hello les quatre premiers paramètres (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, et `UserRegistrationTermsConsentRequired`) mapper toohello suivant les paramètres de hello **identités** onglet Bonjour **sécurité** section.

| Paramètre d’identité | Mappe trop|
| --- | --- |
| RegistrationEnabled |**Les utilisateurs anonymes toosign dans la page de redirection** case à cocher |
| UserRegistrationTerms |**Conditions d’utilisation liées à l’inscription de l’utilisateur** |
| UserRegistrationTermsEnabled |**Afficher les conditions d’utilisation dans la page d’abonnement** |
| UserRegistrationTermsConsentRequired |**Exiger le consentement** |

![Paramètres d’identité][api-management-identity-settings]

Hello quatre paramètres (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, et `DelegationValidationKey`) mapper toohello suivant les paramètres de hello **délégation** onglet Bonjour **sécurité** section.

| Paramètre de délégation | Mappe trop|
| --- | --- |
| DelegationEnabled |Case à cocher **Déléguer la connexion et l’inscription** |
| DelegationUrl |**URL de point de terminaison de la délégation** |
| DelegatedSubscriptionEnabled |**Déléguer l’abonnement au produit** |
| DelegationValidationKey |**Déléguer la clé de validation** |

![Paramètres de délégation][api-management-delegation-settings]

Hello paramètre final, `$ref-policy`, mappe le fichier d’instructions de la stratégie globale toohello pour l’instance de service hello.

### <a name="apis-folder"></a>Dossier apis
Hello `apis` dossier contient un dossier pour chaque API dans l’instance de service hello qui contient les éléments suivants de hello.

* `apis\<api name>\configuration.json`-Cette configuration hello pour hello API et contient des informations sur l’URL du service principal hello et les opérations de hello. Il s’agit de hello mêmes informations qui doit être retournées si vous étiez toocall [obtenir une API spécifique](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) avec `export=true` dans `application/json` format.
* `apis\<api name>\api.description.html`-Il s’agit de description hello Hello API et correspond toohello `description` propriété Hello [entité API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\`-ce dossier contient `<operation name>.description.html` fichiers que les opérations de mappage toohello dans hello API. Chaque fichier contient la description hello d’une seule opération Bonjour API qui mappe toohello `description` propriété Hello [entité opération](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) Bonjour API REST.

### <a name="groups-folder"></a>Dossier groups
Hello `groups` dossier contient un dossier pour chaque groupe défini dans l’instance de service hello.

* `groups\<group name>\configuration.json`-configuration hello pour le groupe de hello. Il s’agit de hello mêmes informations qui doit être retournées si vous étiez toocall hello [obtenir un groupe spécifique](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) opération.
* `groups\<group name>\description.html`-Il s’agit de description hello du groupe de hello et correspond toohello `description` propriété Hello [groupe entité](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>Dossier policies
Hello `policies` dossier contient des instructions de stratégie hello pour votre instance de service.

* `policies\global.xml` : contient les stratégies définies dans l’étendue globale de votre instance de service.
* `policies\apis\<api name>\` : si des stratégies sont définies à l’échelle de l’API, elles se trouvent dans ce dossier.
* `policies\apis\<api name>\<operation name>\`dossier - si vous disposez de toutes les stratégies définies dans le cadre de l’opération, elles sont contenues dans ce dossier dans `<operation name>.xml` fichiers qui mappent des instructions de stratégie toohello pour chaque opération.
* `policies\products\`-Si vous disposez de toutes les stratégies définies au niveau de portée du produit, elles sont contenues dans ce dossier, qui contient `<product name>.xml` fichiers qui mappent toohello les instructions de stratégie pour chaque produit.

### <a name="portalstyles-folder"></a>Dossier portalStyles
Hello `portalStyles` dossier contient les feuilles de style et de configuration pour les personnalisations de portail de développement pour l’instance de service hello.

* `portalStyles\configuration.json`-contient les noms de hello hello de feuilles de style utilisées par le portail des développeurs hello
* `portalStyles\<style name>.css`-chaque `<style name>.css` fichier contient des styles pour le portail des développeurs hello (`Preview.css` et `Production.css` par défaut).

### <a name="products-folder"></a>Dossier products
Hello `products` dossier contient un dossier pour chaque produit défini dans l’instance de service hello.

* `products\<product name>\configuration.json`-configuration hello pour le produit de hello. Il s’agit de hello mêmes informations qui doit être retournées si vous étiez toocall hello [obtenir un produit spécifique](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) opération.
* `products\<product name>\product.description.html`-Il s’agit de description hello du produit de hello et correspond toohello `description` propriété Hello [entité product](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) Bonjour API REST.

### <a name="templates"></a>modèles
Hello `templates` dossier contient la configuration de hello [modèles de messagerie](api-management-howto-configure-notifications.md) hello des instances de service.

* `<template name>\configuration.json`-configuration hello hello modèle de courrier électronique.
* `<template name>\body.html`-corps hello du modèle d’e-mail hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les autres façons de toomanage votre instance de service, consultez :

* Gérer votre instance de service à l’aide de hello suivant d’applets de commande PowerShell
  * [Référence sur les applets de commande PowerShell de déploiement des services](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Référence sur les applets de commande PowerShell de gestion des services](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Gérer votre instance de service dans le portail de publication hello
  * [Gérer votre première API](api-management-get-started.md)
* Gérer votre instance de service à l’aide des API REST de hello
  * [Référence de l’API REST Gestion des API](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>Regarder une vidéo de présentation
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




