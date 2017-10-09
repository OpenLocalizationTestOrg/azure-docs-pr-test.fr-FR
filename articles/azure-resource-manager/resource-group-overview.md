---
title: "vue d’ensemble du Gestionnaire de ressources d’aaaAzure | Documents Microsoft"
description: "Décrit comment toouse Azure Resource Manager pour le déploiement, la gestion et le contrôle d’accès des ressources sur Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a>Présentation d’Azure Resource Manager
infrastructure Hello pour votre application est généralement constitué de nombreux composants – peut-être un ordinateur virtuel, compte de stockage et réseau virtuel, ou une application web, base de données, serveur de base de données et 3 services tiers. Vous ne voyez pas ces composants comme des entités distinctes, mais plutôt comme des parties associées et interdépendantes d’une seule et même entité. Vous souhaitez toodeploy, gérez et surveillez en tant que groupe. Le Gestionnaire de ressources Azure vous permet de toowork des ressources de hello dans votre solution en tant que groupe. Vous pouvez déployer, mettre à jour ou supprimer toutes les ressources hello pour votre solution dans une opération unique et coordonnée. Vous utilisez un modèle de déploiement pouvant fonctionner avec différents environnements (environnements de test, intermédiaire et de production). Gestionnaire de ressources fournit la sécurité, l’audit et le balisage des fonctionnalités toohelp gérer vos ressources après le déploiement. 

## <a name="terminology"></a>Terminologie
Si vous êtes tooAzure nouveau gestionnaire de ressources, il existe certains termes que vous ne connaissez peut-être pas.

* **ressource** : élément gérable disponible dans Azure. Les ressources telles que les machines virtuelles, les comptes de stockage, les applications web, les bases de données et les réseaux virtuels sont courantes, mais il en existe beaucoup d’autres.
* **groupe de ressources** : conteneur réunissant les ressources associées d’une solution Azure. groupe de ressources Hello peut inclure toutes les ressources de hello pour les solutions hello, ou uniquement les ressources que vous souhaitez toomanage en tant que groupe. Vous décidez comment vous souhaitez que les ressources de tooallocate tooresource groupes en fonction de ce que hello plus logique pour votre organisation. Voir [Groupes de ressources](#resource-groups).
* **fournisseur de ressources** -service qui fournit des ressources de hello vous pouvez déployer et gérer par le biais du Gestionnaire de ressources. Chaque fournisseur de ressources offre des opérations pour l’utilisation des ressources hello qui sont déployés. Des fournisseurs de ressources communes sont Microsoft.Compute, qui fournit des ressources d’ordinateurs virtuels hello, Microsoft.Storage, qui fournit des ressources de compte de stockage hello, et Microsoft.Web, qui fournit des ressources connexes tooweb applications. Voir [Fournisseurs de ressources](#resource-providers).
* **Modèle de gestionnaire de ressources** -fichier A JavaScript Objet Notation (JSON) qui définit une ou plusieurs ressources toodeploy tooa groupe de ressources. Il définit également les dépendances hello entre les ressources de hello déployé. modèle de Hello peut être utilisé toodeploy hello ressources régulièrement et à plusieurs reprises. Voir [Déploiement de modèle](#template-deployment).
* **la syntaxe déclarative** -état de la syntaxe qui vous permet de « Voici ce que vous avez l’intention toocreate » sans avoir de séquence de hello toowrite de commandes toocreate de programmation il. modèle de gestionnaire de ressources Hello est un exemple de la syntaxe déclarative. Dans le fichier de hello, vous définissez les propriétés hello pour hello infrastructure toodeploy tooAzure. 

## <a name="hello-benefits-of-using-resource-manager"></a>avantages de Hello d’à l’aide du Gestionnaire de ressources
Resource Manager offre plusieurs avantages :

* Vous pouvez déployer, gérer et surveiller toutes les ressources hello pour votre solution en tant qu’un groupe, au lieu de gérer ces ressources individuellement.
* Vous pouvez à plusieurs reprises déployer votre solution tout au long du cycle de vie de développement hello et avez confiance que vos ressources sont déployées dans un état cohérent.
* Vous pouvez gérer votre infrastructure à l’aide de modèles déclaratifs plutôt que de scripts.
* Vous pouvez définir des dépendances de hello entre les ressources de sorte qu’ils sont déployés dans l’ordre correct de hello.
* Vous pouvez appliquer l’accès contrôle tooall services dans votre groupe de ressources, car le contrôle d’accès en fonction du rôle (RBAC) est en mode natif intégré à la plate-forme de gestion hello.
* Vous pouvez appliquer des balises tooresources toologically organiser toutes les ressources hello dans votre abonnement.
* Vous pouvez de clarifier la facturation de votre organisation en consultant les coûts pour un groupe de ressources de partage hello même balise.  

Le Gestionnaire de ressources fournit un nouveau toodeploy de façon et gérer vos solutions. Si vous avez utilisé hello classiques de déploiement et souhaitez toolearn sur les modifications de hello, consultez [déploiement du Gestionnaire de ressources de présentation et déploiement classique](resource-manager-deployment-model.md).

## <a name="consistent-management-layer"></a>Couche de gestion cohérente
Le Gestionnaire de ressources fournit une couche de gestion cohérente pour hello tâches via Azure PowerShell, CLI d’Azure, Azure portal, API REST et outils de développement. Tous les outils hello utilisent un ensemble commun d’opérations. Vous utilisez les outils hello qui vous convient le mieux et peuvent les utiliser indifféremment sans confusion. 

Hello image suivante montre comment tous les outils hello interagissent avec hello même API Azure Resource Manager. Hello API transfère les demandes toohello Gestionnaire de ressources du service, qui authentifie et autorise les demandes hello. Le Gestionnaire de ressources achemine ensuite les fournisseurs de ressources approprié toohello hello demandes.

![Modèle de requête Resource Manager](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>Assistance
Hello suggestions suivantes vous aident à tirer pleinement parti du Gestionnaire de ressources lorsque vous travaillez avec vos solutions.

1. Définir et déployer votre infrastructure via la syntaxe déclarative hello dans les modèles de gestionnaire de ressources, plutôt que via des commandes impératives.
2. Définir toutes les étapes de déploiement et de configuration dans le modèle de hello. Aucune étape manuelle ne devrait intervenir dans la configuration de votre solution.
3. Exécuter des commandes impératives toomanage vos ressources, telles que toostart ou arrêter une application ou un ordinateur.
4. Organiser les ressources par hello même cycle de vie dans un groupe de ressources. Utilisez des balises pour toute organisation des ressources.

Pour des recommandations sur les modèles, voir [Bonnes pratiques relatives à la création de modèles Azure Resource Manager](resource-manager-template-best-practices.md).

Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

## <a name="resource-groups"></a>Groupes de ressources
Il existe certains tooconsider des facteurs importants lors de la définition de votre groupe de ressources :

1. Toutes les ressources de hello dans votre groupe doivent partager hello même cycle de vie. Les opérations de déploiement, de mise à jour et de suppression porteront sur toutes les ressources du groupe. Si une ressource, tel qu’un serveur de base de données, doit tooexist sur un cycle de déploiement différentes, il doit être dans un autre groupe de ressources.
2. Chaque ressource ne peut exister que dans un seul groupe de ressources.
3. Vous pouvez ajouter ou supprimer un groupe de ressources tooa à tout moment.
4. Vous pouvez déplacer une ressource à partir d’un groupe de tooanother de groupe de ressources. Pour plus d’informations, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](resource-group-move-resources.md).
5. Un groupe de ressources peut contenir des ressources figurant dans différentes régions.
6. Un groupe de ressources peut être utilisée tooscope le contrôle d’accès pour les actions d’administration.
7. Une ressource peut interagir avec celles d’autres groupes de ressources. Cette interaction est courant lorsque des ressources de hello deux sont liées, mais ne partagent pas hello même cycle de vie (par exemple, des applications web connexion tooa de base de données).

Lorsque vous créez un groupe de ressources, vous devez tooprovide un emplacement pour ce groupe de ressources. Vous vous demandez peut-être « Pourquoi un groupe de ressources a-t-il besoin un emplacement ? Et, si les ressources hello peuvent avoir différents emplacements que le groupe de ressources hello, pourquoi emplacement du groupe de ressources hello a d’importance du tout ? » groupe de ressources Hello stocke les métadonnées sur les ressources de hello. Par conséquent, lorsque vous spécifiez un emplacement pour le groupe de ressources hello, vous spécifiez que les métadonnées de stockage. Pour des raisons de compatibilité, vous devrez peut-être tooensure que vos données sont stockées dans une région particulière.

## <a name="resource-providers"></a>Fournisseurs de ressources
Chaque fournisseur de ressources propose un ensemble de ressources et d’opérations permettant de gérer un service Azure. Par exemple, si vous souhaitez toostore clés et les clés secrètes, vous travaillez avec hello **Microsoft.KeyVault** fournisseur de ressources. Ce fournisseur de ressources fournit un type de ressource appelé **coffres** pour la création de coffre de clés hello. 

nom de Hello d’un type de ressource est au format de hello : **{fournisseur de ressources} / {type_ressource}**. Par exemple, le type de coffre de clés hello est **Microsoft.KeyVault/vaults**.

Mise en route avec le déploiement de vos ressources, vous devez comprendre hello disponibles des fournisseurs de ressources. Connaître les noms de ressource hello fournisseurs et des ressources permet de définir des ressources que vous souhaitiez toodeploy tooAzure. En outre, vous devez les emplacements valides au tooknow hello et versions d’API pour chaque type de ressource. Pour plus d’informations, consultez [les types et les fournisseurs de ressources](resource-manager-supported-services.md).

## <a name="template-deployment"></a>Déploiement de modèle
Avec le Gestionnaire de ressources, vous pouvez créer un modèle (en format JSON) qui définit l’infrastructure de hello et la configuration de votre solution Azure. Un modèle vous permet de déployer votre solution à plusieurs reprises tout au long de son cycle de vie pour avoir la garantie que vos ressources présentent un état cohérent lors de leur déploiement. Lorsque vous créez une solution à partir du portail de hello, solution de hello inclut automatiquement un modèle de déploiement. Vous n’avez pas toocreate votre modèle à partir de zéro, car vous pouvez commencer avec le modèle de hello pour votre solution et le personnaliser toomeet vos besoins spécifiques. Vous pouvez récupérer un modèle pour un groupe de ressources existant à exporter l’état actuel de hello hello du groupe de ressources, ou affichage modèle hello utilisé pour un déploiement particulier. Affichage hello [exporté modèle](resource-manager-export-template.md) est un toolearn moyen utile sur la syntaxe de modèle hello.

toolearn sur format hello hello modèle d’et comment vous construisez, consultez [créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md). tooview hello syntaxe JSON pour les types de ressources, consultez [définir des ressources dans les modèles Azure Resource Manager](/azure/templates/).

Le Gestionnaire de ressources traite le modèle hello comme toute autre requête (voir image hello pour [couche de gestion cohérente](#consistent-management-layer)). Il analyse le modèle de hello et convertit les opérations d’API REST pour les fournisseurs de ressources approprié hello sa syntaxe. Par exemple, lorsque le Gestionnaire de ressources reçoit un modèle avec hello après la définition de ressource :

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

Il convertit hello toohello de définition opération d’API REST, qui est envoyée de fournisseur de ressources Microsoft.Storage toohello suivante :

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

La définition de modèles et des groupes de ressources est entièrement des tooyou et la façon dont vous souhaitez que toomanage votre solution. Par exemple, vous pouvez déployer votre application à trois niveaux via un seul modèle tooa seul groupe de ressources.

![modèle à trois niveaux](./media/resource-group-overview/3-tier-template.png)

Toutefois, vous n’avez pas toodefine toute votre infrastructure d’un modèle unique. Souvent, il est logique toodivide vos exigences de déploiement dans un ensemble de modèles ciblés, usage particulier. Vous pouvez facilement réutiliser ces modèles pour différentes solutions. toodeploy une solution spécifique, vous créez un modèle maître qui lie tous les modèles hello requis. Hello image suivante montre comment toodeploy imbriqué une solution à trois niveaux via un modèle parent qui inclut trois modèles.

![modèle à niveaux imbriqués](./media/resource-group-overview/nested-tiers-template.png)

Si vous envisagez de vos niveaux d’avoir des cycles de vie distincts, vous pouvez déployer vos groupes de ressources tooseparate trois niveaux. Avis hello ressources peuvent toujours être lié tooresources dans d’autres groupes de ressources.

![modèle niveau](./media/resource-group-overview/tier-templates.png)

Pour obtenir plus de conseils sur la conception de vos modèles, consultez [Schémas de conception des modèles Azure Resource Manager](best-practices-resource-manager-design-templates.md). Pour plus d’informations sur les modèles imbriqués, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).

Azure Resource Manager analyse les dépendances des ressources de tooensure sont créés dans l’ordre correct de hello. Si une ressource dépend d’une valeur d’une autre ressource (par exemple, une machine virtuelle ayant besoin d’un compte de stockage pour les disques), vous devez définir une dépendance. Pour plus d’informations, consultez [Définition de dépendances dans des modèles Azure Resource Manager](resource-group-define-dependencies.md).

Vous pouvez également utiliser le modèle de hello pour infrastructure toohello des mises à jour. Par exemple, vous pouvez ajouter une solution tooyour de ressources et ajouter des règles de configuration pour les ressources de hello qui sont déjà déployées. Si le modèle de hello spécifie la création d’une ressource, mais que la ressource existe déjà, le Gestionnaire de ressources Azure effectue une mise à jour au lieu de créer un nouvel élément multimédia. Azure Resource Manager les mises à jour hello existant asset toohello même état tel qu’il serait en tant que nouveaux.  

Le Gestionnaire de ressources fournit des extensions pour les scénarios lorsque vous avez besoin d’autres opérations telles que l’installation d’un logiciel particulier qui n’est pas inclus dans le programme d’installation hello. Si vous utilisez déjà un service de gestion de configuration, comme DSC, Chef ou Puppet, vous pouvez continuer à travailler avec ce service en utilisant des extensions. Pour plus d’informations sur les extensions de machines virtuelles, consultez la page [À propos des extensions et des fonctionnalités des machines virtuelles](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Enfin, hello devient partie intégrante du code source de hello pour votre application. Vous pouvez vérifier dans le référentiel de code source tooyour et mettre à jour à mesure que votre application évolue. Vous pouvez modifier le modèle hello via Visual Studio.

Après avoir défini votre modèle, vous êtes prêt toodeploy hello ressources tooAzure. Pour les ressources de hello hello commandes toodeploy, voir :

* [Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell](resource-group-template-deploy.md)
* [Déployer des ressources à l’aide de modèles Resource Manager et de l’interface de ligne de commande Azure](resource-group-template-deploy-cli.md)
* [Déployer des ressources à l’aide de modèles Resource Manager et du Portail Azure](resource-group-template-deploy-portal.md)
* [Déployer des ressources à l’aide de modèles Resource Manager et de l’API REST Resource Manager](resource-group-template-deploy-rest.md)

## <a name="tags"></a>Tags
Gestionnaire de ressources fournit une fonctionnalité de marquage qui vous permet de ressources toocategorize selon les exigences de tooyour pour gérer ou de facturation. Utiliser des balises lorsque vous avez un ensemble complexe de groupes de ressources et de ressources, devez toovisualize ces ressources de manière hello qui rend hello la plupart des tooyou de sens. Par exemple, vous pouvez baliser des ressources qui servent un rôle similaire dans votre organisation ou appartiennent toohello même service. Sans les balises, les utilisateurs de votre organisation peuvent créer plusieurs ressources qui peuvent être difficile toolater identifient et gérer. Par exemple, vous souhaiterez toodelete toutes les ressources hello pour un projet particulier. Si ces ressources ne sont pas marqués pour le projet de hello, vous avez toomanually les trouver. Le balisage peut être un moyen important pour vous tooreduce des coûts inutiles dans votre abonnement. 

Ressources n’est pas nécessaire de tooreside Bonjour tooshare de groupe de ressources même une balise. Vous pouvez créer votre propre tooensure de taxonomie balise que tous les utilisateurs de votre organisation utilisent courantes balises plutôt que les utilisateurs de l’application par inadvertance des balises légèrement différentes (par exemple, « dept » au lieu de « département »).

Hello, l’exemple suivant montre un ordinateur virtuel de tooa étiquette appliquée.

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

utilisation de toutes les ressources hello avec une valeur de balise, tooretrieve hello suivant l’applet de commande PowerShell :

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

Ou bien, hello Azure CLI 2.0 commande suivante :

```azurecli
az resource list --tag costCenter=Finance
```

Vous pouvez également afficher des ressources avec balises via hello portail Azure.

Hello [rapport d’utilisation](../billing/billing-understand-your-bill.md) pour votre abonnement inclut les noms de balise et les valeurs, qui vous permet de toobreak les coûts par des balises. Pour plus d’informations sur les balises, consultez [à l’aide des balises tooorganize vos ressources Azure](resource-group-using-tags.md).

## <a name="access-control"></a>Contrôle d’accès
Le Gestionnaire de ressources vous permet de toocontrol qui a des actions de toospecific d’accès pour votre organisation. En mode natif, il intègre le contrôle d’accès basé sur un rôle (RBAC) à la plate-forme de gestion hello et s’applique à ce contrôle accès tooall les services dans votre groupe de ressources. 

Il existe deux principaux concepts toounderstand lorsque vous travaillez avec le contrôle d’accès basé sur le rôle :

* Définitions des rôles : décrivent un jeu d’autorisations et peuvent être utilisées dans plusieurs affectations.
* Attributions de rôles : associer une définition à une identité (utilisateur ou groupe) pour une portée spécifique (abonnement, groupe de ressources ou ressource). attribution de Hello est héritée par portées inférieures.

Vous pouvez ajouter la plateforme de toopre définies par les utilisateurs et les rôles propres à la ressource. Par exemple, vous pouvez tirer parti des rôles prédéfinis de hello appelé lecteur qui permet aux utilisateurs tooview ressources mais pas les modifier. Ajouter des utilisateurs de votre organisation qui a besoin de ce type de rôle de lecteur accès toohello et appliquer l’abonnement de toohello rôle hello, groupe de ressources ou ressource.

Azure fournit hello suivant quatre rôles de plateforme :

1. Propriétaire : peut tout gérer, y compris les accès
2. Collaborateur : peut tout gérer, sauf les accès
3. Lecteur : peut tout afficher sans pouvoir apporter de modifications
4. Administrateur de l’accès utilisateur - peuvent gérer des ressources de tooAzure d’accès utilisateur

Azure fournit également plusieurs rôles spécifiques à la ressource, notamment :

1. Contributeur de l’ordinateur virtuel - peut gérer des ordinateurs virtuels, mais pas accorder l’accès toothem et ne peut pas gérer hello virtuel réseau ou stockage compte toowhich qu’ils sont connectés
2. Collaborateurs de réseau - peut gérer toutes les ressources réseau, mais pas accorder l’accès toothem
3. Collaborateur du compte de stockage - peuvent gérer les comptes de stockage, mais pas accorder l’accès toothem
4. Collaborateur de serveurs SQL : peut gérer les serveurs et bases de données SQL, mais pas leurs stratégies de sécurité
5. Contributeur du site Web - peut gérer des sites Web, mais pas hello toowhich de plans web qu’ils sont connectés

Pour hello une liste complète des rôles et des actions autorisées, consultez [RBAC : générées dans les rôles](../active-directory/role-based-access-built-in-roles.md). Pour plus d’informations sur le contrôle d’accès en fonction du rôle, consultez [Contrôle d’accès en fonction du rôle d’Azure](../active-directory/role-based-access-control-configure.md). 

Dans certains cas, vous le souhaitez toorun code ou un script qui accède aux ressources, mais vous ne souhaitez pas toorun sous les informations d’identification d’un utilisateur. Au lieu de cela, vous souhaitez toocreate une identité appelée un service principal pour l’application hello et attribuez hello le rôle approprié pour le principal du service hello. Le Gestionnaire de ressources vous permet de toocreate les informations d’identification pour l’application hello et authentifier par programmation des application hello. toolearn sur la création des principaux de service, consultez une des rubriques suivantes :

* [Utiliser Azure PowerShell toocreate une ressources tooaccess principal du service](resource-group-authenticate-service-principal.md)
* [Utilisez Azure CLI toocreate une ressources tooaccess principal du service](resource-group-authenticate-service-principal-cli.md)
* [Utiliser une application de portail toocreate Azure Active Directory et de principal du service qui peut accéder aux ressources](resource-group-create-service-principal-portal.md)

Vous pouvez également explicitement verrouiller les ressources critiques tooprevent que les utilisateurs de supprimer ou de les modifier. Pour plus d’informations, consultez [Verrouiller des ressources avec Azure Resource Manager](resource-group-lock-resources.md).

## <a name="activity-logs"></a>Journaux d’activité
Resource Manager consigne dans un journal toutes les opérations de création, de modification ou de suppression d’une ressource. Vous pouvez utiliser hello activité journaux toofind une erreur lors de la résolution des problèmes ou toomonitor comment un utilisateur dans votre organisation a modifié une ressource. toosee hello journaux, sélectionnez **journaux d’activité** Bonjour **paramètres** panneau pour un groupe de ressources. Vous pouvez filtrer les journaux de hello par nombreuses valeurs différentes, y compris l’opération de hello initiée par l’utilisateur. Pour plus d’informations sur l’utilisation des journaux d’activité hello, consultez [toomanage Azure des journaux d’activité de la vue ressources](resource-group-audit.md).

## <a name="customized-policies"></a>Stratégies personnalisées
Le Gestionnaire de ressources vous permet de stratégies toocreate personnalisé pour la gestion de vos ressources. types de Hello de stratégies que vous créez peuvent inclure des scénarios différents. Vous pouvez appliquer une convention de dénomination des ressources, limiter les types et les instances de ressources qui peuvent être déployées ou limiter les régions qui peuvent héberger un type de ressource. Vous pouvez demander une valeur de balise sur la facturation de tooorganize de ressources par les services. Créer des stratégies toohelp réduire les coûts et assurer la cohérence de votre abonnement. 

Vous pouvez définir des stratégies au format JSON, puis les appliquer à votre abonnement ou dans un groupe de ressources. Stratégies sont différentes de contrôle d’accès basé sur le rôle, car ils sont des types de tooresource appliquée.

Bonjour à l’exemple suivant montre une stratégie qui garantit la cohérence des balises en spécifiant que toutes les ressources incluent une balise de centre de coût.

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

Il existe de nombreux autres types de stratégies que vous pouvez créer. Pour plus d’informations, consultez [ressources toomanage de stratégie d’utilisation et de contrôler l’accès](resource-manager-policy.md).

## <a name="sdks"></a>Kits de développement logiciel (SDK)
Des kits de développement logiciel (SDK) Azure sont disponibles en plusieurs langues sur plusieurs plates-formes. Chacune de ces langues est disponible via le gestionnaire de package d’écosystème correspondant et GitHub.

Voici nos référentiels de Kit de développement logiciel (SDK) open source. N’hésitez pas à nous faire part de vos commentaires, des problèmes rencontrés et de vos demandes d’extraction.

* [Kit de développement logiciel (SDK) Azure pour .NET](https://github.com/Azure/azure-sdk-for-net)
* [Bibliothèques de gestion Azure pour Java](https://github.com/Azure/azure-sdk-for-java)
* [Kit de développement logiciel (SDK) Azure pour Node.js](https://github.com/Azure/azure-sdk-for-node)
* [Kit de développement logiciel (SDK) Azure pour PHP](https://github.com/Azure/azure-sdk-for-php)
* [Kit de développement logiciel (SDK) Azure pour Python](https://github.com/Azure/azure-sdk-for-python)
* [Kit de développement logiciel (SDK) Azure pour Ruby](https://github.com/Azure/azure-sdk-for-ruby)

Pour plus d’informations sur l’utilisation de ces langages avec vos ressources, consultez :

* [Azure for .NET developers](/dotnet/azure/?view=azure-dotnet) (Azure pour les développeurs .NET)
* [Azure for Java developers](/java/azure/) (Azure pour les développeurs Java)
* [Azure for Node.js developers](/nodejs/azure/) (Azure pour les développeurs Node.js)
* [Azure for Python developers](/python/azure/) (Azure pour les développeurs Python)

> [!NOTE]
> Si hello SDK ne fournit pas les fonctionnalités hello requis, vous pouvez également appeler toohello [API REST Azure](https://docs.microsoft.com/rest/api/resources/) directement.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction simple tooworking avec des modèles, consultez [exporter un modèle Azure Resource Manager à partir de ressources existants](resource-manager-export-template.md).
* Pour une procédure plus détaillée de création d’un modèle, voir [Créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).
* les fonctions hello toounderstand que vous pouvez utiliser dans un modèle, consultez [fonctions de modèle](resource-group-template-functions.md)
* Pour plus d’informations sur l’utilisation de Visual Studio avec Resource Manager, consultez [Création et déploiement de groupes de ressources Azure à l’aide de Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

Voici une vidéo de cette présentation :

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
