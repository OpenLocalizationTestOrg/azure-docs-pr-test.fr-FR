---
title: "aaaKey fonctionnalités et les concepts dans la pile de Azure | Documents Microsoft"
description: "En savoir plus sur les fonctionnalités clés hello et les concepts dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: Heathl17
manager: byronr
editor: 
ms.assetid: 09ca32b7-0e81-4a27-a6cc-0ba90441d097
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: helaw
ms.openlocfilehash: a9cb3b99dc67a12976ca61b6678f047caab48543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="key-features-and-concepts-in-azure-stack"></a>Fonctionnalités et concepts clés de Azure Stack
Si vous êtes tooMicrosoft nouvelle pile d’Azure, ces termes et les descriptions de la fonctionnalité peuvent être utiles.

## <a name="personas"></a>Rôles
Il existe deux types d’utilisateurs pour la pile Microsoft Azure, opérateur de cloud hello (fournisseur) et le client hello (consommateurs).

* A **opérateur cloud** pouvez configurer la pile de Azure et gérer des offres, des plans, services, quotas et des ressources tooprovide tarification pour leurs clients.  Les opérateurs cloud permet également de gérer la capacité et de répondent tooalerts.  
* A **client** (également désignée tooas un utilisateur) utilise des services qui hello offres d’administrateur de cloud. Les clients peuvent approvisionner, surveiller et gérer les services auxquels ils sont abonnés, tels que les Web Apps, le stockage et les machines virtuelles.

## <a name="portal"></a>Portail
Hello principales méthodes de l’interaction avec la pile de Microsoft Azure sont portail d’administration hello, portail de l’utilisateur et PowerShell.

les portails Azure pile Hello sont soutenues par des instances distinctes du Gestionnaire de ressources Azure.  Un opérateur cloud utilise hello administrateur toomanage portail Azure pile et des éléments tels que toodo créer client offres.  portail de l’utilisateur Hello (également désignée tooas hello portail de locataires) fournit une expérience de libre-service pour la consommation des ressources de cloud, tels que les ordinateurs virtuels, les comptes de stockage et les applications Web. Pour plus d’informations, consultez [à l’aide des portails d’administrateur et utilisateur Azure pile hello](azure-stack-manage-portals.md).

## <a name="identity"></a>Identité 
Azure Stack utilise Azure Active Directory (AAD) ou Active Directory Federation Services (AD FS) en tant que fournisseur d’identité.  

### <a name="azure-active-directory"></a>Azure Active Directory
Azure Active Directory est le fournisseur d’identité Microsoft multilocataire basé sur le cloud.  La plupart des scénarios hybrides utilisent Azure Active Directory comme magasin d’identités hello.

### <a name="active-directory-federation-services"></a>Services de fédération Active Directory (AD FS)
Vous pouvez choisir toouse Active Directory Federation Services (ADFS) pour les déploiements déconnectés de la pile de Azure.  Pile Azure, les fournisseurs de ressources et les autres applications fonctionnent bien hello même façon avec AD FS avec Azure Active Directory. Azure Stack inclut sa propre instance d’AD FS et d’Active Directory, ainsi qu’une API Graph Active Directory. Kit de développement de pile Azure prend en charge hello AD FS les scénarios suivants :

- Connectez-vous toohello déploiement à l’aide d’AD FS.
- Créer une machine virtuelle avec des secrets dans Key Vault
- Créer un coffre pour le stockage et l’accès aux secrets
- Créer des rôles RBAC personnalisés dans l’abonnement
- Affecter des utilisateurs tooRBAC les rôles sur les ressources
- Créer des rôles RBAC à l’échelle du système par le biais d’Azure PowerShell
- Se connecter en tant qu’utilisateur par le biais d’Azure PowerShell
- Créer des services principaux de les utilisent toosign tooAzure PowerShell


## <a name="regions-services-plans-offers-and-subscriptions"></a>Régions, services, plans, offres et abonnements
Dans la pile d’Azure, les services sont remis tootenants à l’aide de régions, les abonnements, les offres et les plans. Les clients peuvent s’abonner toomultiple offres. Les offres peuvent contenir un ou plusieurs plans, et les plans peuvent contenir un ou plusieurs services.

![](media/azure-stack-key-features/image4.png)

Exemple de hiérarchie de toooffers des abonnements d’un locataire, chacune avec différents plans et services.

### <a name="regions"></a>Régions
Les régions Azure Stack sont un élément de base de la mise à l’échelle et de la gestion. Une organisation peut avoir plusieurs régions avec des ressources disponibles dans chaque région. Les régions peuvent également avoir différentes offres de services disponibles. Dans le Kit de développement Azure Stack, une seule région est prise en charge. Elle est automatiquement nommée *local*.

### <a name="services"></a>Services
Pile de Microsoft Azure permet de fournisseurs toodeliver une grande variété de services et applications, telles que les machines virtuelles, les bases de données SQL Server, SharePoint, Exchange et bien plus encore.

### <a name="plans"></a>Abonnements
Les plans regroupent un ou plusieurs services. En tant que fournisseur, créer des plans toooffer tooyour locataires. À son tour, vos clients de s’abonner tooyour offres toouse hello plans et services qu’ils comprennent.

Chaque service ajouté tooa plan peut être configuré avec toohelp des paramètres de quota, vous gérez votre capacité du cloud. Les quotas peuvent inclure des restrictions, telles que des limites de machine virtuelle, de mémoire et d’unité centrale, appliquées par abonnement de l’utilisateur. Les quotas peuvent être différenciés par emplacement. Par exemple, un plan comprenant des services de calcul à partir de la région A peut avoir un quota de deux machines virtuelles, 4 Go de RAM et dix cœurs de processeur.

Lorsque vous créez une offre, l’administrateur de service hello peut inclure un **plan de base**. Ces plans de base sont inclus par défaut lorsqu’un locataire s’abonne toothat offre. Lorsqu’un utilisateur s’abonne (et création de l’abonnement hello), hello utilisateur dispose d’accès tooall hello les fournisseurs de ressources spécifiés dans les plans de base (avec les quotas correspondant hello).

administrateur de service Hello peut également inclure **plans de module complémentaire** dans une offre. Plans de module complémentaire ne sont pas inclus par défaut dans l’abonnement de hello. Les plans de modules complémentaires sont des plans supplémentaires (quotas) disponibles dans une offre qu’un propriétaire d’abonnement peut ajouter des abonnements de tootheir.

### <a name="offers"></a>Offres
Offres sont des groupes d’un ou plusieurs plans que toobuy tootenants présent de fournisseurs (s’abonner à). Par exemple, une offre Alpha peut contenir un plan A comportant un ensemble de services de calcul et un plan B comportant un ensemble de services de stockage et réseau.

Une offre est fourni avec un ensemble de plans de base, et les administrateurs de service peuvent créer des plans de module complémentaire que les clients peuvent ajouter tootheir abonnement.

### <a name="subscriptions"></a>Abonnements
Un abonnement est la forme sous laquelle les clients achètent vos offres. Un abonnement est la combinaison d’un client avec une offre. Un locataire peut avoir des abonnements toomultiple offres. Chaque abonnement s’applique à une offre de tooonly. Les abonnements d’un client déterminent les plans/services accessibles.

Les abonnements aident les fournisseurs à organiser et à accéder aux services et aux ressources cloud.

Pour l’administrateur de hello, un abonnement de fournisseur par défaut est créé au cours du déploiement. Cet abonnement peut toomanage utilisé Azure pile, déployez davantage de fournisseurs de ressources et créer des plans et des offres pour les clients. Ne doit pas être utilisé toorun les charges de travail client et les applications. 

## <a name="azure-resource-manager"></a>Azure Resource Manager
Azure Resource Manager vous permet de travailler avec vos ressources d’infrastructure selon un modèle déclaratif et basé sur des modèles.   Il fournit une interface unique que vous pouvez utiliser toodeploy et gérer des composants de votre solution. Pour plus d’informations et des instructions, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md).

### <a name="resource-groups"></a>Groupes de ressources
Les groupes de ressources sont des ensembles de ressources, de services et d’applications, et chaque ressource a son type, tel que les machines virtuelles, les réseaux virtuels, les IP publiques, les comptes de stockage et les sites web. Chaque ressource doit être dans un groupe de ressources. Ceux-ci aident à organiser les ressources de manière logique, par exemple par charge de travail ou par emplacement.  Dans Microsoft Azure Stack, les ressources, telles que les plans et les offres, sont également gérées dans des groupes de ressources.
 
### <a name="azure-resource-manager-templates"></a>Modèles Microsoft Azure Resource Manager
Avec z Resource Manager, vous pouvez créer un modèle (au format JSON) qui définit le déploiement et la configuration de votre application. Ce modèle est appelé un modèle Azure Resource Manager et fournit un déploiement toodefine de façon déclarative. En utilisant un modèle, vous pouvez à plusieurs reprises déployer votre application tout au long du cycle de vie application hello et avez confiance que vos ressources sont déployées dans un état cohérent.

## <a name="resource-providers-rps"></a>Fournisseurs de ressources
Fournisseurs de ressources sont des services web que foundation hello de formulaire pour tous les services IaaS et PaaS Azure. Le Gestionnaire de ressources Azure s’appuie sur différents RPs tooprovide accès tooservices.

Il existe quatre fournisseurs de ressources fondamentaux : réseau, stockage, calcul et KeyVault. Chacun de ces fournisseurs vous permet de configurer et contrôler ses ressources respectives. Les administrateurs de services peuvent également ajouter de nouveaux fournisseurs de ressources personnalisés.

### <a name="compute-rp"></a>Fournisseur de ressources de calcul
Hello du fournisseur de ressources de calcul (CRP) permet à Azure pile locataires toocreate leurs propres ordinateurs virtuels. Hello CRP inclut hello capacité toocreate virtuels, ainsi que des extensions de Machine virtuelle. Hello service d’extension de Machine virtuelle permet de fournir des fonctions IaaS pour les machines virtuelles Windows et Linux.  Par exemple, vous pouvez utiliser des hello CRP tooprovision une machine virtuelle Linux et exécuter des scripts Bash pendant hello tooconfigure de déploiement machine virtuelle.

### <a name="network-rp"></a>Fournisseur de ressources réseau
Hello fournisseur de ressources réseau (NRP) offre une série de fonctionnalités logicielles défini par la mise en réseau (SDN) et la virtualisation de fonction réseau (NFV) pour le cloud privé de hello.  Vous pouvez utiliser les ressources de toocreate hello NRP telles que les groupes de sécurité logiciels charge équilibrages, des adresses IP publiques, réseau, les réseaux virtuels.

### <a name="storage-rp"></a>Fournisseur de ressources de stockage
Hello RP de stockage propose quatre services de stockage Azure-cohérente : blob, table, file d’attente et la gestion des comptes. Il offre également une stockage cloud administration service toofacilitate service administration du fournisseur de services de stockage Azure-cohérent. Le stockage Azure fournit hello flexibilité toostore et extraire de grandes quantités de données non structurées, telles que des documents et des fichiers multimédias avec des objets BLOB Azure, et NoSQL structurée en fonction des données avec les Tables Azure. Pour plus d’informations sur le stockage Azure, consultez [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).

#### <a name="blob-storage"></a>Stockage d'objets blob
Le stockage d’objets blob stocke tous les jeux de données. Un objet blob peut correspondre à n'importe quel type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d'installation d'application. Le stockage de tables stocke les jeux de données structurés. Stockage de table est un magasin de données d’attribut de clé NoSQL, qui permet un développement rapide et quantités de toolarge un accès rapide des données. Le stockage de files d’attente fournit une messagerie fiable pour le traitement du workflow et pour la communication entre les composants des services cloud.

Chaque objet blob est organisé sous un conteneur. Les conteneurs fournissent également un toogroups de stratégies de sécurité de tooassign moyen utile d’objets. Un compte de stockage peut contenir n’importe quel nombre de conteneurs, et un conteneur peut contenir n’importe quel nombre d’objets BLOB, de la limite de capacité de 500 To toohello hello du compte de stockage. Le stockage d’objets blob propose trois types d’objets : les objets blob de bloc, les objets blob d’ajout et les objets blob de page (disques). Les objets blob de bloc sont optimisés pour la diffusion en continu et le stockage d’objets cloud. Ils constituent une solution de choix pour stocker des documents, des fichiers multimédias, des sauvegardes, etc. Ajouter des objets BLOB sont des objets BLOB de tooblock similaire, mais sont optimisés pour les opérations d’ajout. Un objet blob d’ajout peut être mis à jour qu’en ajoutant une nouvelle fin toohello de bloc. Ajouter les objets BLOB sont un bon choix pour les scénarios tels que la journalisation, où les nouvelles données doivent toobe écrit uniquement toohello fin de l’objet blob de hello. Objets BLOB de pages est optimisés pour représenter les disques IaaS et écrit aléatoire de prise en charge et peut être jusqu'à too1 to. Un disque IaaS rattaché à un réseau de machines virtuelles Azure est un disque dur virtuel stocké en tant qu'objet blob de page.

#### <a name="table-storage"></a>Stockage de tables
Le stockage de tables est le magasin de clés/attributs NoSQL de Microsoft ; il a une conception sans schéma, ce en quoi il diffère des bases de données relationnelles classiques. Étant donné que les schémas d’un manque de banques de données, il est facile tooadapt vos données en tant que hello a besoin d’evolve de votre application. Stockage de table étant toouse simple, les développeurs peuvent créer rapidement des applications. Le stockage de tables est un magasin de clés/attributs : cela signifie que chaque valeur dans une table est stockée avec un nom de propriété typé. nom de la propriété Hello peut être utilisé pour le filtrage et la spécification des critères de sélection. Une collection de propriétés et leurs valeurs constituent une entité. Depuis les schémas de manque de stockage de Table, les deux entités dans hello même table peut contenir différents ensembles de propriétés, et ces propriétés peuvent être de types différents. Vous pouvez utiliser la Table stockage toostore flexible jeux de données, telles que les données utilisateur pour les applications web, carnets d’adresses, les informations de périphérique et tout autre type de métadonnées nécessaires à votre service. Vous pouvez stocker n’importe quel nombre d’entités dans une table, et un compte de stockage peut contenir n’importe quel nombre de tables, des limites de capacité toohello hello du compte de stockage.

#### <a name="queue-storage"></a>Stockage de files d’attente
Le Stockage File d’attente Azure fournit une messagerie cloud entre les composants d’application. Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment. Stockage de file d’attente fournit une messagerie asynchrone pour la communication entre les composants d’application, qu’elles s’exécutent dans le cloud hello, sur le bureau de hello, sur un serveur local ou sur un appareil mobile. Le stockage de files d’attente prend également en charge la gestion des tâches asynchrones et la création des flux de travail de processus.

### <a name="keyvault"></a>KeyVault
Hello KeyVault RP fournit la gestion et l’audit des secrets, comme les mots de passe et des certificats. Par exemple, un client peut utiliser hello des mots de passe administrateur KeyVault RP tooprovide ou des clés lors du déploiement de machine virtuelle.

## <a name="role-based-access-control-rbac"></a>Contrôle d’accès en fonction du rôle (RBAC)
Vous pouvez utiliser RBAC toogrant système accès tooauthorized, les utilisateurs, groupes et services en leur attribuant des rôles au niveau de la ressource, groupe de ressources ou abonnement. Chaque rôle définit le niveau d’accès hello qu'un utilisateur, un groupe ou un service a des ressources de la pile de Microsoft Azure.

RBAC Azure a trois rôles de base qui s’appliquent à des types de ressources tooall : propriétaire, collaborateur et lecteur. Propriétaire dispose des ressources de tooall d’un accès complet, y compris hello toodelegate droit accès tooothers. Collaboration peut créer et gérer tous les types de ressources Azure, mais ne peut pas accorder l’accès tooothers. Le Lecteur peut uniquement afficher les ressources Azure existantes. autres rôles RBAC hello dans Azure Hello autoriser la gestion de ressources Azure spécifiques. Par exemple, hello collaborateur de Machine virtuelle rôle autorise la création et gestion des ordinateurs virtuels, mais ne permet pas de gestion de réseau virtuel de hello ou un sous-réseau de hello que hello l’ordinateur virtuel se connecte à.

## <a name="usage-data"></a>Données d'utilisation
Microsoft Azure pile collecte et agrège les données d’utilisation de tous les fournisseurs de ressources, puis les transmet tooAzure pour le traitement par commerce Azure. les données d’utilisation de Hello collectées sur Azure pile sont consultables via une API REST. Est un cohérent de Azure API client, ainsi que les fournisseur et API de fournisseur déléguée tooget les données d’utilisation pour tous les abonnements du locataire. Ces données peuvent être utilisé toointegrate avec un outil externe ou un service de facturation ou de rétrofacturation. Une fois que l’utilisation a été traitée par commerce Azure, elle peut être affichée dans hello portail de facturation Azure.

## <a name="in-development-build-of-azure-stack-development-kit"></a>Builds de développement du Kit de développement Azure Stack
Les builds de développement permettent d’évaluer la version la plus récente de hello Kit de développement de pile Azure hello-premiers. Générations incrémentielles selon la version majeure la plus récente de hello, ils contiennent. Tandis que les versions principales continueront à être toobe publiées chaque mois, les builds de développement de hello quelques sera mise en production par intermittence entre hello principales mises à jour.

Les builds de développement fournira hello avantages suivants :
- Résolution des bogues
- Nouvelles fonctionnalités
- Autres améliorations

## <a name="next-steps"></a>Étapes suivantes
[Déployer le Kit de développement Azure Stack](azure-stack-deploy.md)

