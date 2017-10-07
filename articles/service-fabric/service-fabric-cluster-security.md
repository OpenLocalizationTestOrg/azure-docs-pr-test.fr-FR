---
title: aaaSecure un cluster Service Fabric | Documents Microsoft
description: "Décrit les scénarios de sécurité hello pour un tooimplement de différentes technologies utilisées hello et de cluster Service Fabric ces scénarios."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Scénarios de sécurité d’un cluster Service Fabric
Un cluster Service Fabric est une ressource que vous possédez. Clusters doivent être tooprevent sécurisé non autorisé les utilisateurs de se connecter tooyour cluster, surtout quand les charges de production en cours d’exécution sur ce dernier. Bien qu’il soit possible de toocreate un cluster non sécurisé, cela permet aux utilisateurs anonymes tooconnect tooit, s’il expose toohello de points de terminaison de gestion Internet public. 

Cet article fournit une vue d’ensemble de hello des scénarios de sécurité pour les clusters en cours d’exécution sur Azure ou autonome et hello différentes technologies utilisées tooimplement ces scénarios. scénarios de sécurité du cluster Hello sont :

* Sécurité nœud à nœud
* Sécurité client à nœud
* Contrôle d’accès en fonction du rôle

## <a name="node-to-node-security"></a>Sécurité nœud à nœud
Sécurise les communications entre les machines virtuelles de hello ou des ordinateurs dans un cluster de hello. Cela garantit que seuls les ordinateurs qui sont autorisés toojoin hello clusters peuvent participer hébergeant des applications et services de cluster de hello.

![Diagramme de communication nœud à nœud][Node-to-Node]

Les clusters qui s’exécutent sur Azure ou les clusters autonomes sur Windows peuvent utiliser la [Sécurité par certificat](https://msdn.microsoft.com/library/ff649801.aspx) ou la [Sécurité Windows](https://msdn.microsoft.com/library/ff649396.aspx) pour les ordinateurs Windows Server.

### <a name="node-to-node-certificate-security"></a>Sécurité de certificat de nœud à nœud
L’infrastructure de service utilise les certificats de serveur X.509 que vous spécifiez dans le cadre des configurations de nœud de type hello lorsque vous créez un cluster. Une vue d’ensemble rapide de ces certificats et comment vous pouvez acquérir ou créez-les est fourni à fin hello de cet article.

Sécurité de certificat est configurée lors de la création de cluster de hello via hello portail Azure, des modèles Azure Resource Manager ou un modèle JSON autonome. Vous pouvez spécifier un certificat primaire et un certificat secondaire facultatif utilisé pour les renouvellements de certificats. Hello certificats principaux et secondaires, vous spécifiez doivent être différents de celui de client d’administration hello et les certificats de client en lecture seule vous spécifiez pour [sécurité du Client au nœud](#client-to-node-security).

Pour lire les Azure [configurer un cluster à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) toolearn comment tooconfigure certificat de sécurité dans un cluster.

Pour Windows Server autonome, consultez [Sécuriser un cluster autonome sur Windows à l’aide de certificats X.509 ](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>Sécurité Windows de nœud à nœud
Pour Windows Server autonome, consultez [Sécuriser un cluster autonome sur Windows à l’aide de la sécurité Windows](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>Sécurité client à nœud
Authentifie les clients et sécurise les communications entre un client et les différents nœuds d’un cluster de hello. Ce type de sécurité authentifie et sécurise les communications client, ce qui garantit que seuls les utilisateurs autorisés peuvent accéder à cluster de hello et applications hello sur hello cluster. Les clients sont identifiés de manière grâce à leurs informations d’identification de sécurité Windows ou à leurs informations d’identification de sécurité de certificat.

![Diagramme de communication client à nœud][Client-to-Node]

Les clusters qui s’exécutent sur Azure ou les clusters autonomes qui s’exécutent sur Windows peuvent utiliser la [Sécurité par certificat](https://msdn.microsoft.com/library/ff649801.aspx) ou la [Sécurité Windows](https://msdn.microsoft.com/library/ff649396.aspx).

### <a name="client-to-node-certificate-security"></a>Sécurité par certificat de client à nœud
 Sécurité du certificat du client à ce nœud est configurée lors de la création de cluster de hello via hello portail Azure, modèles du Gestionnaire de ressources ou un modèle JSON autonome en spécifiant un certificat de client d’administration et/ou d’un certificat client utilisateur.  Hello administrateur client et l’utilisateur les certificats clients vous spécifiez doivent être différents de celui hello principal et secondaire certificats que vous spécifiez pour [sécurité du nœud à l’autre](#node-to-node-security) comme une meilleure pratique. Par défaut, les certificats de cluster hello pour la sécurité du nœud à l’autre sont ajoutés toohello autorisé client de liste de certificats Admin.

Les clients se connectant cluster toohello à l’aide du certificat d’administration hello ont des fonctionnalités de toomanagement d’un accès complet.  Les clients se connectant cluster toohello à l’aide du certificat de client utilisateur en lecture seule hello ont uniquement des fonctionnalités de toomanagement de l’accès en lecture. En d’autres termes, ces certificats sont utilisés pour hello bases de contrôle d’accès rôle (RBAC) décrit plus loin dans cet article.

Pour lire les Azure [configurer un cluster à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) toolearn comment tooconfigure certificat de sécurité dans un cluster.

Pour Windows Server autonome, consultez [Sécuriser un cluster autonome sur Windows à l’aide de certificats X.509 ](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Sécurité Azure Active Directory (AAD) de client-à-nœud sur Azure
Les clusters en cours d’exécution sur Azure peuvent également sécuriser l’accès aux points de terminaison de gestion toohello à l’aide d’Azure Active Directory (AAD). Consultez [configurer un cluster à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) pour plus d’informations sur la façon dont toocreate hello artefacts AAD nécessaires, comment toopopulate au cours de cluster la création, et comment tooconnect toothose clusters par la suite.

## <a name="security-recommendations"></a>Recommandations en matière de sécurité
Pour les clusters Azure, il est recommandé d’utiliser AAD sécurité tooauthenticate clients et les certificats pour la sécurité du nœud à l’autre.

Pour les clusters Windows Server, nous vous recommandons d’utiliser la sécurité Windows avec des comptes gérés par des groupes (GMA) si vous avez Windows Server 2012 R2 et Active Directory. Sinon, continuez à utiliser la sécurité Windows avec les comptes Windows.

## <a name="role-based-access-control-rbac"></a>Contrôle d’accès en fonction du rôle (RBAC)
Contrôle d’accès permet de cluster administrateur toolimit toocertain cluster opérations d’accès pour différents groupes d’utilisateurs, la sécurisation de cluster de hello hello. Deux types de contrôle d’accès différents sont pris en charge pour les clients se connectant tooa cluster : rôle d’administrateur et le rôle d’utilisateur.

Les administrateurs disposent de fonctionnalités de toomanagement d’un accès complet (y compris les fonctionnalités en lecture/écriture). Les utilisateurs, par défaut, ont uniquement un accès en lecture toomanagement fonctionnalités (par exemple, les fonctions de requête), hello capacité tooresolve applications et services.

Vous spécifiez hello administrateur client rôles d’utilisateur et lors de la création du cluster hello en fournissant des identités séparées (certificats, etc. AAD) pour chacun. Pour plus d’informations sur les paramètres de contrôle de l’accès par défaut hello et comment toochange hello les paramètres par défaut, consultez [le contrôle d’accès basée sur les rôles pour les clients du Service Fabric](service-fabric-cluster-security-roles.md).

## <a name="x509-certificates-and-service-fabric"></a>Certificats X.509 et Service Fabric
Les certificats numériques X.509 sont couramment utilisés tooauthenticate clients et les serveurs et tooencrypt et signer numériquement les messages. Pour plus d’informations sur ces certificats, consultez trop[utilisation des certificats](http://msdn.microsoft.com/library/ms731899.aspx).

Tooconsider de certains points importants :

* Les certificats utilisés dans les clusters qui exécutent des charges de travail de production doivent être créés en utilisant un service de certificats Windows Server correctement configuré ou obtenus auprès d’une [autorité de certification (AC)](https://en.wikipedia.org/wiki/Certificate_authority)approuvée.
* En production, n’utilisez jamais de certificats temporaires ou de test créés avec des outils comme MakeCert.exe.
* Vous pouvez utiliser un certificat auto-signé, mais seulement pour les clusters de test et non en production.

### <a name="server-x509-certificates"></a>Certificats X.509 de serveur
Certificats de serveur ont hello principale tâche des authentifier un tooclients serveur (nœud), ou l’authentification d’un serveur de tooa (nœud) serveur (nœud). Un des contrôles d’initiale hello lorsqu’un nœud ou un client s’authentifie à un nœud de valeur toocheck hello de nom commun de hello dans le champ de l’objet hello. Ce nom commun ou un des autres noms d’objet des certificats hello doit être présent dans la liste hello des noms communs autorisés.

Hello suivant décrit comment les certificats avec d’autres noms d’objet (SAN) toogenerate : [comment tooadd un tooa autre nom de sujet sécuriser le certificat LDAP](http://support.microsoft.com/kb/931351).

champ d’objet Hello peut contenir plusieurs valeurs, chacune préfixée par un type de valeur d’initialisation tooindicate hello. En règle générale, l’initialisation de hello est « CN » pour le nom commun ; par exemple, « CN = www.contoso.com ». Il est également possible pour hello sujet champ toobe vide. Si hello facultatif nom alternatif du sujet est renseigné, il doit contenir hello le nom commun du certificat de hello et une entrée par nom alternatif du sujet. Ils sont entrés sous forme de valeurs de nom DNS.

valeur Hello du champ de prévus hello du certificat de hello doit inclure une valeur appropriée, comme « Authentification serveur » ou « Authentification cliente ».

### <a name="client-x509-certificates"></a>Certificats X.509 de client
Les certificats clients ne sont généralement pas émis par une autorité de certification tierce. Au lieu de cela, hello magasin personnel de l’emplacement de l’utilisateur actuel hello contient généralement les certificats de client par une autorité racine, avec l’objectif de le « Authentification cliente ». client de la Hello peut utiliser ce certificat lors de l’authentification mutuelle est requise.

> [!NOTE]
> Toutes les opérations de gestion sur un cluster Service Fabric requièrent des certificats de serveur. Les certificats clients ne peuvent pas être utilisés pour la gestion.
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a>Étapes suivantes
Cet article fournit des informations conceptuelles sur la sécurité des clusters. Ensuite,


1.  [créez un cluster dans Azure à l’aide d’un modèle Resource Manager](service-fabric-cluster-creation-via-arm.md) 
2.  [Portail Azure](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
