---
title: "aaaOverview de Azure des applications gérées | Documents Microsoft"
description: "Décrit les concepts de hello pour Azure applications managées"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 2fd1844a442515f4492c890c9798073475a66f88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-overview"></a>Vue d’ensemble des applications gérées Azure

Les fournisseurs qui utilisent Azure peuvent offrir toocustomers solutions monde hello. La Place de marché Azure est une galerie composée de centaines de modèles à plusieurs ressources complexes issus de fournisseurs tiers et internes. En quelques minutes, les clients peuvent déployer et commencer à utiliser des applications PaaS (plateforme en tant que service) et SaaS (logiciel en tant que service). 

Bien que hello Marketplace constitue un excellent moyen pour les clients tooquickly déployer une offre, client de hello est responsable de la maintenance et la mise à jour de la solution de hello. Au-delà de la facturation d’image de machine virtuelle hello, les fournisseurs ne peut pas facturer des clients pour utiliser une application hello. En outre, les fournisseurs ne peuvent pas empêcher les clients de modifier des ressources d’application critiques. Fournisseurs ne peut pas également bloquer les propriété toointellectual d’accès qui composent une application. Les applications gérées Azure constituent une solution à ces problèmes. 

Une application managée est similaire modèle de solution tooa Bonjour Marketplace, avec une différence majeure. Dans une application managée, les ressources hello sont un groupe de ressources tooa configuré qui est géré par le fournisseur de hello. groupe de ressources Hello est présent dans l’abonnement du client hello, mais une identité dans les locataire du fournisseur hello a le groupe de ressources toohello accès.

## <a name="advantages-of-managed-applications"></a>Avantages des applications gérées

Fournisseurs de services (MSP), des éditeurs de logiciels indépendants, managés et les équipes informatiques centrales d’entreprise peuvent utiliser des solutions de toodeliver les applications managées via hello Marketplace ou hello du catalogue de services. Bien que les clients déployer ces applications gérées dans leurs abonnements, ils n’ont pas toomaintain, mettre à jour ou les traiter. Étant donné que les fournisseurs, gérer et prendre en charge les applications hello, les clients n’ont pas toodevelop domaine spécifique à l’application de base de connaissances toomanage ces applications. Les clients peuvent acquérir automatiquement mises à jour de l’application sans tooworry besoin de hello sur le dépannage et de diagnostic des problèmes avec les applications hello.

Pour les fournisseurs et les fournisseurs, les applications managées créent une infrastructure de canal toosell et les logiciels via hello Marketplace. Les applications gérées fournissent également un moyen tooattach services et les clients tooAzure de prise en charge opérationnelle. Fournisseurs de facturer les clients à l’aide de hello système de facturation Azure. Ils peuvent utiliser des modèles toomanage hello du cycle de vie des applications déployées. Ces solutions étant autonome et sealed toohello client, les fournisseurs peuvent fournir des services de haute qualité. Cette approche est bénéfique pour les fournisseurs de services PaaS et SaaS. Cela permet également aux équipes de plate-forme centrale d’entreprise et les intégrateurs système (SIs) qui souhaitez toopackage et revendre leurs solutions.

## <a name="managed-application-types"></a>Types d’applications gérées
Les applications gérées Azure se présentent sous deux types : un catalogue de services et la Place de marché.
 
### <a name="service-catalog"></a>Catalogue de services  

Avec hello catalogue de services, aux clients de créer un catalogue des solutions approuvées pour Azure toobe utilisés par des personnes dans leur organisation. Il est utile pour les équipes informatiques centrales des entreprises de maintenir un tel catalogue à jour. Ils peuvent utiliser hello catalogue tooensure respect de certaines normes d’organisation pendant qu’ils fournissent des solutions pour leurs organisations. Elles peuvent contrôler, mettre à jour et gérer ces applications. Les employés peuvent utiliser hello catalogue tooeasily détecter le jeu complet de hello d’applications qui sont recommandé et approuvées par leurs services informatiques. Les clients voient les applications de catalogue de services gérés hello qu’ils ont créés. Ils peuvent également voir hello que d’autres personnes dans leur part de l’organisation avec les applications managées.
 
Pour plus d’informations sur la publication d’une application gérée de catalogue de services, consultez l’article [Créer et publier une application gérée de catalogue de services](managed-application-publishing.md).
 
Pour plus d’informations sur l’utilisation d’une application gérée de catalogue de services, consultez l’article [Utiliser une application gérée du catalogue de services](managed-application-consumption.md).
 
### <a name="marketplace"></a>Marketplace

Les applications managées sont disponibles via hello Marketplace Bonjour portail Azure. Une fois que le fournisseur de hello publie ces applications, elles sont disponibles pour tout le monde à l’intérieur ou à l’extérieur d’une organisation tooconsume. Avec cette approche, MSP, éditeurs de logiciels indépendants et SIs peuvent proposer leur tooall solutions Azure aux clients. Clients de hello profiter de l’utilisation de ces solutions complexes sans tooinvest besoin de hello dans la compréhension et la gestion des solutions de hello. 

Actuellement, l’auteur de la publication peut proposer son offre sous forme d’application gérée ou sous forme de modèle de solution non géré. Hello principaux composants de publication d’une application managée incluent le fichier de modèle hello et le fichier de définition de l’interface utilisateur de hello. fichier de modèle Hello décrit les ressources hello configurées. fichier de définition de l’interface utilisateur Hello décrit comment hello requis pour la configuration de ces ressources, les entrées se présentent dans le portail de hello. Hello requis les fichiers sont empaquetés dans un fichier .zip et téléchargés via le portail de publication hello.
 
Pour plus d’informations sur la publication d’une application managée de toohello Marketplace, consultez [Azure géré applications Bonjour Marketplace](managed-application-author-marketplace.md).

Pour plus d’informations sur la consommation d’une application managée à partir de hello Marketplace, consultez [Azure de consommer gérés applications Bonjour Marketplace](managed-application-consume-marketplace.md).

## <a name="key-concepts"></a>Concepts clés

### <a name="managed-resource-group"></a>Groupe de ressources géré
Bonjour groupe de ressources managé est où tous les hello Azure les ressources qui sont configurés dans le modèle de hello sont créées. Par exemple, si le dispositif de hello est toocreate utilisé un compte de stockage, ce groupe de ressources contient des ressources de compte de stockage hello. Il ne contient pas ressources d’application hello.

### <a name="appliance-package"></a>Package d’appliance
serveur de publication Hello crée un package qui contient les fichiers de modèle hello et un fichier de createUIDefinition hello. Plus précisément, elle contient hello fichiers suivants :

- **applianceMainTemplate.json**: ce fichier de modèle définit toutes les ressources hello configurés par le dispositif de hello. Ce fichier est un fichier de modèle Normal qui a utilisé toocreate de ressources.

- **MainTemplate.json**: ce fichier de modèle définit les ressources d’application hello (Microsoft.Solutions/appliances). Une propriété essentielle définie dans cette ressource est ManagedResourceGroupId. Cette propriété indique quel groupe de ressources est utilisé toohost hello réel ressources définies dans applianceMainTemplate.json.

- **applianceCreateUIDefinition.json**: ce fichier décrit le mode de rendu hello l’interface utilisateur nécessaire pour les paramètres de hello définis dans le modèle de hello.

### <a name="authorization"></a>Autorisation
serveur de publication Hello doit spécifier les autorisations de hello requises par les ressources de hello toomanage hello fournisseur pour le compte du client de hello. Cette autorisation s’applique à groupe de ressources managé toohello. Hello du jeu de valeurs suivantes :

- **PrincipalID**: hello Azure Active Directory (Azure AD) identificateur de hello utilisateur, groupe ou application qui utilise le groupe de ressources managé toohello toogrant accès. Cet identificateur appartient un client de l’éditeur toohello.

- **RoleDefinitionID**: hello identificateur Azure AD de toohello de rôle attribué hello précédant l’ID de principal. Il peut être un des rôles de contrôle d’accès basée sur les rôles intégrés hello dans le client de l’éditeur de hello. Pour plus d’informations, consultez [Rôles intégrés pour le contrôle d’accès en fonction du rôle Azure](../active-directory/role-based-access-built-in-roles.md).

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur la publication des applications managées toohello Marketplace, consultez [Azure géré applications Bonjour Marketplace](managed-application-author-marketplace.md).
* Pour plus d’informations sur la consommation d’une application managée à partir de hello Marketplace, consultez [Azure de consommer gérés applications Bonjour Marketplace](managed-application-consume-marketplace.md).
* Pour plus d’informations sur la publication d’une application gérée de catalogue de services, consultez l’article [Créer et publier une application gérée de catalogue de services](managed-application-publishing.md).
* Pour plus d’informations sur l’utilisation d’une application gérée de catalogue de services, consultez l’article [Utiliser une application gérée du catalogue de services](managed-application-consumption.md).
* toocreate un fichier de définition de l’interface utilisateur, consultez [prise en main CreateUiDefinition](managed-application-createuidefinition-overview.md).
