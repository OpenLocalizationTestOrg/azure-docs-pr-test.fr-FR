---
title: "aaaWhat repose sur groupe de licences dans Azure Active Directory ? | Microsoft Docs"
description: "Description des licences basées sur les groupes Azure Active Directory, de leur fonctionnement et des bonnes pratiques"
services: active-directory
keywords: Gestion des licences Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a>Principes de base des licences basées sur les groupes dans Azure Active Directory

L’utilisation de services cloud Microsoft payants, comme Office 365, Enterprise Mobility + Security, Dynamics CRM et d’autres produits similaires, nécessite des licences. Ces licences sont affectées utilisateur tooeach ayant besoin de services d’accès toothese. toomanage des licences, les administrateurs utilisent un des portails de gestion hello (Office ou Azure) et les applets de commande PowerShell. Azure Active Directory (Azure AD) est l’infrastructure sous-jacente hello qui prend en charge la gestion des identités pour tous les services de cloud de Microsoft. Azure AD stocke des informations sur les états d’affectation de licence pour les utilisateurs.

Jusqu'à présent, les licences ne peut être attribués qu’au niveau utilisateur individuel de hello, qui peut compliquer la gestion à grande échelle. Par exemple, tooadd ou supprimez licences utilisateur basés sur les modifications organisationnelles, telles que les utilisateurs de rejoindre ou quitter hello société ou un service, un administrateur souvent doit écrire un script PowerShell complex. Ce script effectue les appels toohello le service cloud.

tooaddress ces défis, Azure AD inclut basée sur le groupe de licences. Vous pouvez affecter une ou plusieurs licences tooa catégorie. Azure AD garantit que les licences hello assignés tooall les membres du groupe de hello. Tous les nouveaux membres qui rejoignent le groupe de hello sont affectées des licences appropriées de hello. Lorsqu’ils quittent le groupe de hello, les licences sont supprimés. Cela élimine la nécessité de hello pour automatiser la gestion des licences via les modifications de tooreflect PowerShell dans l’organisation de hello et la structure des départements sur une base par utilisateur.

## <a name="features"></a>Caractéristiques

Voici hello principales fonctionnalités de groupe de licences :

- Licences peuvent être attribuées de groupe de sécurité tooany dans Azure AD. Les groupes de sécurité peuvent être synchronisés en local à l’aide d’Azure AD Connect. Vous pouvez également créer des groupes de sécurité directement dans Azure AD (également appelés groupes uniquement dans le cloud), ou automatiquement via la fonctionnalité de groupe dynamique hello Azure AD.

- Lorsque le groupe de tooa est affectée à une licence de produit, administrateur de hello peut désactiver un ou plusieurs plans de service dans le produit de hello. En règle générale, cela lors de l’organisation de hello n’est pas encore prêt toostart à l’aide d’un service inclus dans un produit. Par exemple, administrateur de hello peut affecter le service de tooa d’Office 365, mais désactiver temporairement le service de Yammer hello.

- Tous les services de cloud computing Microsoft nécessitant des licences au niveau des utilisateurs sont pris en charge. Cela comprend tous les produits Office 365, Enterprise Mobility + Security et Dynamics CRM.

- Basé sur le groupe de licences est actuellement disponible uniquement via [hello Azure portal](https://portal.azure.com). Si vous utilisez principalement des autres portails de gestion pour l’utilisateur et de gestion de groupe, tels que le portail de hello Office 365, vous pouvez continuer toodo donc. Mais vous devez utiliser les licences toomanage portail Azure hello au niveau du groupe.

- Azure AD gère automatiquement les modifications de licences qui résultent de modifications de l’appartenance aux groupes. En règle générale, les modifications de licence sont effectives quelques minutes après une modification d’appartenance.

- Un utilisateur peut être membre de plusieurs groupes dans lesquels des stratégies de licences sont spécifiées. Un utilisateur peut également disposer de licences affectées directement, en dehors de groupes. Hello résultant de l’état utilisateur est une combinaison de tous les produits et les licences de service.

- Dans certains cas, les licences ne peut pas être assignés tooa utilisateur. Par exemple, il peut ne pas être suffisamment de licences disponibles locataire de hello ou services conflictuels peuvent avoir été affectés à hello même temps. Les administrateurs ont tooinformation d’accès sur les utilisateurs pour lequel Azure AD ne peut pas effectuer un traitement complet des licences de groupe. Ils peuvent prendre des mesures correctives en fonction de ces informations.

- Version préliminaire publique, un abonnement d’évaluation ou payant pour les éditions d’Azure AD Basic ou Premium est requise dans hello client toouse basée sur le groupe de gestion des licences.

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les autres scénarios de gestion des licences via le groupe de licences, consultez :

* [Bien démarrer avec les licences dans Azure Active Directory](active-directory-licensing-get-started-azure-portal.md)
* [Affectation d’un groupe de tooa de licences dans Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Identification et résolution des problèmes de licence pour un groupe dans Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Comment toomigrate individuels titulaires d’une licence dans Azure Active Directory en fonction des toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios (Autres scénarios de licence basée sur le groupe Azure Active Directory)](active-directory-licensing-group-advanced.md)
