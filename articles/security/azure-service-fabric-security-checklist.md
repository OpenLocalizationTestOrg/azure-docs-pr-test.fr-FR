---
title: "liste de vérification de la sécurité de l’ensemble fibre optique d’aaaAzure service | Documents Microsoft"
description: "Cet article fournit un ensemble de listes de contrôle pour la sécurité Azure Service Fabric."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Liste de contrôle pour la sécurité Azure Service Fabric
Cet article fournit une liste de contrôle facile à utiliser qui vous aide à sécuriser votre environnement Azure Service Fabric.

## <a name="introduction"></a>Introduction
Azure Service Fabric est une plateforme de systèmes distribués qui rend facile toopackage, déployer et gérer des microservices fiables et évolutives. Service Fabric résout également des défis de hello dans le développement et la gestion des applications de cloud. Les développeurs et administrateurs sont en mesure d’éviter les problèmes d’infrastructure complexes et peuvent se concentrer sur l’implémentation de charges de travail stratégiques et exigeantes, évolutives, fiables et faciles à gérer.

## <a name="checklist"></a>Liste de contrôle
Utilisez hello suivant toohelp de liste de vérification pour vous assurer que vous n’avez pas négligé tous les problèmes importants dans la gestion et la configuration d’une solution Azure Service Fabric sécurisé.


|Catégorie de la liste de contrôle| Description |
| ------------ | -------- |
|[Contrôle d’accès en fonction du rôle (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>Contrôle d’accès permet de cluster administrateur toolimit toocertain cluster opérations d’accès pour différents groupes d’utilisateurs, la sécurisation de cluster de hello hello.</li><li>Les administrateurs disposent de fonctionnalités de toomanagement d’un accès complet (y compris les fonctionnalités en lecture/écriture). </li><li>   Les utilisateurs, par défaut, ont uniquement un accès en lecture toomanagement fonctionnalités (par exemple, les fonctions de requête), hello capacité tooresolve applications et services.</li></ul>|
|[Certificats X.509 et Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>Les [certificats](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates) utilisés dans les clusters qui exécutent des charges de travail de production doivent être créés en utilisant un service de certificats Windows Server correctement configuré ou obtenus auprès d’une [autorité de certification (AC)](https://en.wikipedia.org/wiki/Certificate_authority) approuvée.</li><li>En production, n’utilisez jamais de [certificats temporaires ou de test](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development) créés avec des outils comme [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx). </li><li>Vous pouvez utiliser un [certificat auto-signé](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security), mais seulement pour les clusters de test et non en production.</li></ul>|
|[Sécurité des clusters](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>scénarios de sécurité du cluster Hello incluent la sécurité de nœud à l’autre, la sécurité au nœud Client, [contrôle d’accès basé sur un rôle (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles).</li></ul>|
|[Authentification du cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Authentifie la [communication nœud à nœud](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md) pour la fédération du cluster. </li></ul>|
|[Authentification du serveur](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Authentifie hello [points de terminaison de gestion de cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal) client de gestion tooa.</li></ul>|
|[Sécurité des applications](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>Le chiffrement et déchiffrement de valeurs de configuration d’application.</li><li> Le chiffrement des données sur les nœuds lors de la réplication.</li></ul>|
|[Certificat de cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>Ce certificat est la communication de hello toosecure requis entre les nœuds de hello sur un cluster.</li><li>  Définir l’empreinte numérique hello du certificat principal de hello Bonjour section de l’empreinte numérique et que de hello secondaire dans les variables ThumbprintSecondary hello.</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>Ce certificat est présenté toohello client quand il tente de tooconnect toothis cluster. Vous pouvez utiliser deux certificats de serveur différents : un certificat principal et un certificat secondaire pour la mise à niveau.</li></ul>|
|ClientCertificateThumbprints| <ul><li>Il s’agit d’un jeu de certificats que vous souhaitez tooinstall sur les clients de hello authentifié. </li></ul>|
|ClientCertificateCommonNames| <ul><li>Hello de nom commun du certificat de client premier hello pour hello CertificateCommonName du jeu. Hello CertificateIssuerThumbprint est l’empreinte numérique hello pour émetteur hello de ce certificat. </li></ul>|
|ReverseProxyCertificate| <ul><li>Il s’agit d’un certificat facultatif qui peut être spécifié si vous souhaitez toosecure votre [Proxy inverse](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy). </li></ul>|
|Key Vault| <ul><li>Utilisé toomanage certificats pour les clusters Service Fabric dans Azure.  </li></ul>|


## <a name="next-steps"></a>Étapes suivantes
- [Processus de mise à niveau du cluster Service Fabric et attentes à votre égard](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [Gestion de vos applications Service Fabric dans Visual Studio](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio).
- [Présentation du modèle d’intégrité de Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction).
