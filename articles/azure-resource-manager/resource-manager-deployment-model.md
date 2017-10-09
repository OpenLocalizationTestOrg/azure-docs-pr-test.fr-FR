---
title: "aaaResource Manager et le déploiement classique | Documents Microsoft"
description: "Décrit le modèle de déploiement hello différences entre le modèle de déploiement du Gestionnaire de ressources hello et hello classique (ou la gestion de Service)."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7ae0ffa3-c8da-4151-bdcc-8f4f69290fb4
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: tomfitz
ms.openlocfilehash: fbf1959991b100547a459bf88a29c0afbc8592e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-hello-state-of-your-resources"></a>Le Gestionnaire de ressources Azure et déploiement classique : comprendre les modèles de déploiement et hello l’état de vos ressources
Dans cette rubrique, vous découvrez Azure Resource Manager et les modèles de déploiement classique, état hello de vos ressources, et pourquoi vos ressources ont été déployés avec une ou hello autres. Hello Gestionnaire de ressources et les modèles de déploiement classique représentent deux façons différentes de déploiement et la gestion de vos solutions Azure. Vous travaillez avec eux via deux différents ensembles d’API, et les ressources hello déployé peuvent contenir des différences importantes. Hello deux modèles ne sont pas entièrement compatibles entre eux. Cette rubrique décrit ces différences.

déploiement de hello toosimplify et la gestion des ressources, Microsoft recommande d’utiliser le Gestionnaire de ressources pour toutes les nouvelles ressources. Microsoft recommande, si possible, un nouveau déploiement des ressources existantes via Resource Manager.

Si vous êtes tooResource nouveau gestionnaire, vous souhaiterez toofirst revue la terminologie hello définie dans hello [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).

## <a name="history-of-hello-deployment-models"></a>Historique des modèles de déploiement hello
Initialement, Azure fourni uniquement le modèle de déploiement classique hello. Dans ce modèle, chaque ressource existe indépendamment ; Il n’existait aucun moyen toogroup les ressources associées ensemble. Au lieu de cela, vous aviez toomanually suivre les ressources qui composés votre solution ou votre application et n’oubliez pas de toomanage dans une approche coordonnée. toodeploy une solution, vous aviez tooeither créer chaque ressource individuellement via le portail classique de hello ou créer un script qui déployé toutes les ressources hello dans l’ordre correct de hello. toodelete une solution, vous aviez toodelete chaque ressource individuellement. Il était difficile d’appliquer et de mettre à jour des stratégies de contrôle d’accès pour des ressources liées. Enfin, vous ne pouvez pas appliquer balises tooresources toolabel les termes du contrat qui vous aident à surveiller vos ressources et que vous gérez la facturation.

En 2014, Azure introduit le Gestionnaire de ressources qui a ajouté le concept de hello d’un groupe de ressources. Un groupe de ressources est un conteneur de ressources qui partagent un cycle de vie commun. modèle de déploiement du Gestionnaire de ressources Hello offre plusieurs avantages :

* Vous pouvez déployer, gérer et surveiller tous les services hello pour votre solution en tant qu’un groupe, au lieu de gérer ces services individuellement.
* Vous pouvez déployer votre solution à plusieurs reprises tout au long de son cycle de vie et avoir ainsi l’assurance que vos ressources présentent un état cohérent lors de leur déploiement.
* Vous pouvez appliquer tooall contrôler les accès aux ressources dans votre groupe de ressources, et ces stratégies sont appliquées automatiquement lorsque de nouvelles ressources sont ajoutés à groupe de ressources toohello.
* Vous pouvez appliquer des balises tooresources toologically organiser toutes les ressources hello dans votre abonnement.
* Vous pouvez utiliser l’infrastructure de hello toodefine JavaScript Objet Notation (JSON) pour votre solution. fichier JSON de Hello est connu en tant que gestionnaire de ressources du modèle.
* Vous pouvez définir des dépendances de hello entre les ressources de sorte qu’ils sont déployés dans l’ordre correct de hello.

Lorsque le Gestionnaire de ressources a été ajouté, toutes les ressources ont été ajoutés rétroactivement toodefault les groupes de ressources. Si vous créez une ressource via maintenant le déploiement classique, les ressources hello sont créé automatiquement dans un groupe de ressources par défaut pour ce service, même si vous ne spécifiez pas de groupe de ressources au moment du déploiement. Toutefois, simplement existantes dans un groupe de ressources ne signifie pas que les ressources hello a été converti toohello Gestionnaire de ressources du modèle. Nous allons examiner comment chaque service gère les deux modèles de déploiement hello dans la section suivante de hello. 

## <a name="understand-support-for-hello-models"></a>Comprendre la prise en charge pour les modèles de hello
Lorsque vous décidez quels toouse de modèle de déploiement pour vos ressources, il existe trois toobe scénarios prenant en charge de :

1. service de Hello prend en charge le Gestionnaire de ressources et fournit seulement un type unique.
2. Hello service prend en charge le Gestionnaire de ressources, mais fournit deux types suivants : une pour le Gestionnaire de ressources et une pour classique. Ce scénario s’applique uniquement les ordinateurs de toovirtual, les comptes de stockage et les réseaux virtuels.
3. service de Hello ne prend pas en charge le Gestionnaire de ressources.

toodiscover si un service prend en charge le Gestionnaire de ressources, consultez [les types et les fournisseurs de ressources](resource-manager-supported-services.md).

Si le service hello vous souhaitez toouse ne prend pas en charge le Gestionnaire de ressources, vous devez continuer à l’aide de déploiement classique.

Si le service de hello prend en charge le Gestionnaire de ressources et **n’est pas** un ordinateur virtuel, le compte de stockage ou le réseau virtuel, vous pouvez utiliser le Gestionnaire de ressources sans difficulté.

Pour les ordinateurs virtuels, les comptes de stockage et les réseaux virtuels, si les ressources hello a été créé via le déploiement classique, vous devez continuer toooperate sur ce dernier via des opérations classiques. Si l’ordinateur virtuel de hello, compte de stockage ou réseau virtuel a été créé par le Gestionnaire de ressources du déploiement, vous devez continuer à l’aide des opérations de gestionnaire de ressources. Cette distinction peut être déroutante lorsque votre abonnement contient un mélange de ressources créées via un déploiement Resource Manager et un déploiement classique. Cette combinaison de ressources peut créer des résultats inattendus, car les ressources hello ne gèrent pas hello les mêmes opérations.

Dans certains cas, une commande du Gestionnaire de ressources peut récupérer des informations sur la ressource créée par le déploiement classique, ou peut exécuter une tâche d’administration tels que le déplacement d’un groupe de ressources tooanother classique. Toutefois, ces cas ne doivent pas fournir impression hello que type de hello prend en charge les opérations du Gestionnaire de ressources. Par exemple, supposons que vous disposiez d’un groupe de ressources qui contient une machine virtuelle, créée via un déploiement classique. Si vous exécutez hello suivant de commande PowerShell de gestionnaire de ressources :

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

Il renvoie la machine virtuelle de hello :

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

Toutefois, hello applet de commande Gestionnaire de ressources **Get-AzureRmVM** retourne uniquement les ordinateurs virtuels déployés par le biais du Gestionnaire de ressources. Hello commande suivante ne retourne pas virtuels hello créés via le déploiement classique.

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

Seules les ressources créées via Resource Manager prennent en charge les balises. Vous ne pouvez pas appliquer les balises tooclassic ressources.

## <a name="resource-manager-characteristics"></a>Caractéristiques de Resource Manager
toohelp vous comprenez hello deux modèles, passons en revue les caractéristiques de hello de types de gestionnaire de ressources :

* Créé par le biais hello [portail Azure](https://portal.azure.com/).
  
     ![Portail Azure](./media/resource-manager-deployment-model/portal.png)
  
     Pour le calcul, stockage et ressources réseau, vous pouvez hello à l’aide du Gestionnaire de ressources ou classique de déploiement. Sélectionnez **Gestionnaire des ressources**.
  
     ![Déploiement Resource Manager](./media/resource-manager-deployment-model/select-resource-manager.png)
* Créé avec la version du Gestionnaire de ressources hello Hello applets de commande PowerShell de Azure. Ces commandes ont le format de hello *AzureRmNoun de verbe*.

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* Créé par le biais hello [les REST API Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) des opérations REST.
* Créé par le biais des commandes CLI d’Azure exécuter Bonjour **arm** mode.
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* type de ressource Hello n’inclut pas **(classique)** dans le nom de hello. Hello image suivante montre les type hello en tant que **compte de stockage**.
  
    ![application web](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>Caractéristiques du déploiement classique
Vous pouvez également connaître le modèle de déploiement classique hello en tant que modèle de gestion des services hello.

Ressources créées dans Bonjour Bonjour du partage de modèle de déploiement classique suivant caractéristiques :

* Créé par le biais hello [portail classique](https://manage.windowsazure.com)
  
     ![portail classique](./media/resource-manager-deployment-model/classic-portal.png)
  
     Ou, hello portail Azure et que vous spécifiez **classique** déploiement (pour le calcul, stockage et de mise en réseau).
  
     ![Déploiement classique](./media/resource-manager-deployment-model/select-classic.png)
* Créée via la version de gestion des services hello Hello applets de commande PowerShell de Azure. Ces noms de commandes ont le format de hello *AzureNoun de verbe*.

  ```powershell
  New-AzureVM
  ```

* Créé par le biais hello [API REST Service Management](https://msdn.microsoft.com/library/azure/ee460799.aspx) des opérations REST.
* Créées à l’aide de commandes de l’interface de ligne de commande Azure exécutées en mode **asm** .

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* type de ressource Hello inclut **(classique)** dans le nom de hello. Hello image suivante montre les type hello en tant que **compte de stockage (classiques)**.
  
    ![type classique](./media/resource-manager-deployment-model/classic-type.png)

Vous pouvez utiliser les ressources Azure toomanage portail hello qui ont été créés via le déploiement classique.

## <a name="changes-for-compute-network-and-storage"></a>Modifications en termes de calcul, de réseau et de stockage
Hello diagramme suivant affiche les ressources de calcul, réseau et de stockage déployés par le biais du Gestionnaire de ressources.

![Architecture Resource Manager](./media/resource-manager-deployment-model/arm_arch3.png)

Notez hello suivant des relations entre les ressources de hello :

* Toutes les ressources hello existent au sein d’un groupe de ressources.
* Hello virtual machine dépend d’un compte de stockage défini dans toostore de fournisseur de ressources de stockage hello (obligatoire) de stockage d’objets blob ses disques dans.
* machine virtuelle de Hello fait référence à une carte de réseau spécifique définie dans le fournisseur de ressources réseau hello (obligatoire) et un groupe à haute disponibilité définie dans le fournisseur de ressources de calcul hello (facultatif).
* Hello NIC références hello l’ordinateur virtuel attribué (obligatoire), de l’adresse IP sous-réseau hello du réseau virtuel de hello pour machine virtuelle de hello (obligatoire) et tooa le groupe de sécurité réseau (facultatif).
* sous-réseau Hello dans un réseau virtuel fait référence à un groupe de sécurité réseau (facultatif).
* instance de programme d’équilibrage de charge Hello fait référence à pool d’adresses IP qui incluent hello carte réseau d’un ordinateur virtuel (facultatif) principal d’hello et fait référence à une adresse équilibrage de charge publique ou privée IP (facultative).

Voici les composants hello et leurs relations pour le déploiement classique :

![architecture classique](./media/resource-manager-deployment-model/arm_arch1.png)

la solution classique Hello pour l’hébergement d’un ordinateur virtuel comprend :

* Un service cloud nécessaire qui agit en tant que conteneur pour héberger des machines virtuelles (calcul). Les machines virtuelles sont automatiquement fournies avec une carte d’interface réseau (NIC, Network Interface Card) et une adresse IP attribuée par Azure. En outre, le service de cloud computing hello contient une instance d’équilibrage de charge externe, une adresse IP publique et points de terminaison tooallow à distance à distance et bureau PowerShell du trafic par défaut pour les ordinateurs virtuels basés sur Windows et le trafic de Secure Shell (SSH) pour basés sur Linux machines virtuelles.
* Un compte de stockage requise que magasins hello des disques durs virtuels pour un ordinateur virtuel, y compris les disques de données temporaires et supplémentaires (stockage) de système d’exploitation de hello.
* Un réseau virtuel facultatif qui agit comme un conteneur supplémentaire, dans laquelle vous pouvez créer une structure de sous-réseaux et désigner le sous-réseau hello sur quel hello se trouve l’ordinateur virtuel (réseau).

Hello tableau suivant décrit les modifications de l’interaction de fournisseurs de ressources de calcul, réseau et de stockage :

| Item | Classique | Gestionnaire de ressources |
| --- | --- | --- |
| Service cloud pour machines virtuelles |Service cloud est un conteneur d’ordinateurs virtuels hello nécessitant la disponibilité à partir de la plateforme de hello et l’équilibrage de charge. |Service cloud n’est plus un objet requis pour la création d’un ordinateur virtuel à l’aide du nouveau modèle de hello. |
| Virtual Network |Un réseau virtuel est facultatif pour la machine virtuelle de hello. Si inclus, réseau virtuel de hello ne peut pas être déployé avec le Gestionnaire de ressources. |La machine virtuelle nécessite un réseau virtuel déployé avec Resource Manager. |
| Comptes de stockage |machine virtuelle de Hello requiert un compte de stockage qui stocke les disques durs virtuels hello hello système d’exploitation, des disques de données temporaire et d’autres. |machine virtuelle de Hello requiert un toostore de compte de stockage ses disques dans le stockage blob. |
| Groupes à haute disponibilité |Plateforme toohello de disponibilité a été indiqué en configurant hello même « AvailabilitySetName » sur les Machines virtuelles de hello. nombre maximal de domaines d’erreur de Hello est 2. |Le groupe à haute disponibilité est une ressource exposée par le fournisseur Microsoft.Compute. Les ordinateurs virtuels qui nécessitent une haute disponibilité doit être inclus dans hello à haute disponibilité. nombre maximal de domaines d’erreur de Hello est maintenant 3. |
| Groupe d'affinités |Les groupes d’affinités étaient nécessaires pour créer des réseaux virtuels. Toutefois, avec l’introduction de hello de réseaux virtuels régionaux, qui n’a été requise plus. |toosimplify, concept de groupes d’affinités hello n’existe pas dans hello API exposées par le biais du Gestionnaire de ressources Azure. |
| Équilibrage de la charge. |Création d’un Service Cloud fournit un équilibrage de charge implicite de hello ordinateurs virtuels déployés. |Hello équilibrage de charge est une ressource exposée par le fournisseur de Microsoft.Network hello. interface réseau principale de Hello Hello des Machines virtuelles qui a besoin d’équilibrage de charge toobe doit faire référence à équilibrage de charge hello. Ces éléments d’équilibrage de la charge peuvent être internes ou externes. Une instance d’équilibrage de charge fait référence à pool d’adresses IP qui incluent hello carte réseau d’un ordinateur virtuel (facultatif) principal d’hello et fait référence à une adresse équilibrage de charge publique ou privée IP (facultative). [En savoir plus.](../virtual-network/resource-groups-networking.md) |
| Adresse IP virtuelle |Services de cloud computing d’obtenir une adresse IP virtuelle par défaut (adresse IP virtuelle) lorsqu’une machine virtuelle est ajoutée le service cloud tooa. Hello adresse IP virtuelle est adresse hello associée à équilibrage de charge implicite de hello. |Adresse IP publique est une ressource exposée par le fournisseur de Microsoft.Network hello. L’adresse IP publique peut être statique (réservée) ou dynamique. Tooa équilibrage de charge peuvent être attribué à des adresses IP publiques dynamiques. Les adresses IP publiques peuvent être sécurisées à l’aide de groupes de sécurité. |
| Adresses IP réservées |Vous pouvez réserver une adresse IP dans Azure et à associer avec un tooensure de Service Cloud qui hello adresse IP est fixe. |Adresse IP publique peuvent être créée dans le mode « Statique » et offres hello même fonctionnalité en tant que « Adresse IP réservée ». Adresses IP publiques statiques ne peut être assignée équilibrage de charge tooa dès maintenant. |
| Adresse IP publique par machine virtuelle |Les adresses IP publiques peut également être associée tooa machine virtuelle directement. |Adresse IP publique est une ressource exposée par le fournisseur de Microsoft.Network hello. L’adresse IP publique peut être statique (réservée) ou dynamique. Toutefois, adresses IP publiques dynamiques seulement peut être tooget d’Interface réseau tooa affecté une adresse IP publique par machine virtuelle dès maintenant. |
| Points de terminaison |Toobe de points de terminaison nécessaires d’entrée configuré sur un ordinateur virtuel de toobe ouvrir la connectivité pour certains ports. Un des modes de courants de hello de la connexion des ordinateurs toovirtual faits en définissant des points de terminaison d’entrée. |Les règles NAT entrantes peuvent être configurées sur les équilibrages de charge tooachieve hello même fonctionnalité d’activation des points de terminaison sur des ports spécifiques pour la connexion des machines virtuelles de toohello. |
| Nom DNS |Les services cloud obtiennent un nom DNS global unique et implicite. Par exemple : `mycoffeeshop.cloudapp.net`. |Les noms DNS sont des paramètres facultatifs qui peuvent être spécifiés sur une ressource d’adresse IP publique. Bonjour nom de domaine complet est suivante de hello format - `<domainlabel>.<region>.cloudapp.azure.com`. |
| Interfaces réseau |L’interface réseau principale et secondaire et ses propriétés ont été définies en tant que configuration du réseau d’une machine virtuelle. |L’interface réseau est une ressource exposée par le fournisseur Microsoft.Network. cycle de vie Hello Hello Qu'interface réseau n’est pas liée tooa Machine virtuelle. Il fait référence à adresse IP attribuée l’ordinateur virtuel de hello (obligatoire), sous-réseau hello du réseau virtuel de hello pour machine virtuelle de hello (obligatoire) et tooa le groupe de sécurité réseau (facultatif). |

toolearn sur la connexion des réseaux virtuels à partir de modèles de déploiement différentes, consultez [connecter des réseaux virtuels à partir de modèles de déploiement différentes dans le portail de hello](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

## <a name="migrate-from-classic-tooresource-manager"></a>Migrer à partir de tooResource classique Manager
Si vous êtes prêt toomigrate vos ressources à partir de déploiement classique tooResource déploiement Manager, consultez :

1. [Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [Plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [Migrer les ressources de IaaS de classique tooAzure Gestionnaire de ressources à l’aide d’Azure PowerShell](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [Migrer les ressources IaaS de classique tooAzure Gestionnaire de ressources à l’aide de CLI d’Azure](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>Forum Aux Questions (FAQ)
**Puis-je créer un ordinateur virtuel à l’aide d’Azure Resource Manager toodeploy dans un réseau virtuel créé à l’aide de déploiement classique ?**

Ce n’est pas pris en charge. Vous ne pouvez pas utiliser Azure Resource Manager toodeploy un ordinateur virtuel sur un réseau virtuel qui a été créé à l’aide de déploiement classique.

**Puis-je créer un ordinateur virtuel à l’aide de hello Azure Resource Manager à partir d’une image de l’utilisateur qui a été créée à l’aide de hello API de gestion des services Azure ?**

Ce n’est pas pris en charge. Toutefois, vous pouvez copier les fichiers de disque dur virtuel hello à partir d’un compte de stockage qui a été créé à l’aide d’API de gestion de hello et ajoutez-les tooa nouveau compte créé par le biais du Gestionnaire de ressources Azure.

**Nouveautés d’impact hello sur le quota de hello pour mon abonnement ?**

quotas Hello pour les machines virtuelles de hello, les réseaux virtuels et les comptes de stockage créés via hello Azure Resource Manager sont distincts des autres quotas. Chaque abonnement obtient quotas toocreate hello ressources hello nouvelles API. Vous pouvez en savoir plus sur les quotas supplémentaires de hello [ici](../azure-subscription-service-limits.md).

**Puis-je continuer toouse de mes scripts automatisés pour la configuration des ordinateurs virtuels, les réseaux virtuels et les comptes de stockage via les API du Gestionnaire de ressources de hello ?**

Tous les scripts que vous avez créés et les automation de hello continuent toowork pour les machines virtuelles existantes hello, réseaux virtuels créés sous un mode de gestion des services Azure hello. Toutefois, les scripts de hello ont nouveau schéma de hello toobe toouse mis à jour pour la création des mêmes ressources via le mode de gestionnaire de ressources hello hello.

**Où puis-je trouver des exemples de modèles Azure Resource Manager ?**

Vous trouverez un ensemble complet de modèles de démarrage sur [Modèles de démarrage rapide Azure Resource Manager](https://azure.microsoft.com/documentation/templates/).

## <a name="next-steps"></a>Étapes suivantes
* toowalk via la création de modèle qui définit un ordinateur virtuel, compte de stockage et réseau virtuel, voir hello [procédure pas à pas de gestionnaire de ressources du modèle](resource-manager-template-walkthrough.md).
* commandes de hello toosee pour le déploiement d’un modèle, consultez [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).

