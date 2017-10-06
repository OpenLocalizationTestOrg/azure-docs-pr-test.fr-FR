---
title: "aaaCharacteristics d’Azure Active Directory locataire intercaction | Documents Microsoft"
description: "Gérer vos locataires Azure Active Directory en les considérant comme des ressources entièrement indépendantes"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>Comprendre l’interaction entre plusieurs locataires Azure Active Directory

Dans Azure Active Directory (Azure AD), chaque tenent est une ressource entièrement indépendante : un homologue logiquement indépendant hello autres clients que vous gérez. Il n’existe pas de relation parent-enfant entre les locataires. Cette indépendance entre les locataires vaut pour les ressources, l’administration et la synchronisation.

## <a name="resource-independence"></a>Indépendance des ressources
* Si vous créez ou supprimez une ressource dans un locataire, il n’a aucun impact sur les ressources dans une autre locataire, à l’exception de partielle de hello des utilisateurs externes. 
* Si vous utilisez l’un de vos noms de domaine avec un locataire, il ne peut être utilisé avec aucun autre locataire.

## <a name="administrative-independence"></a>Indépendance de l’administration
Si un utilisateur non administrateur du locataire « Contoso » crée le locataire de test « Test », alors :

* Par défaut, utilisateur hello qui crée un client est ajouté en tant qu’un utilisateur externe dans un nouveau client et rôle d’administrateur général hello affectées dans ce locataire.
* les administrateurs de Hello du client « Contoso » n’ont aucun tootenant des privilèges d’administrateur direct « Test », sauf si un administrateur de « Test » leur ait spécifiquement accordé ces privilèges. Toutefois, les administrateurs de « Contoso » peuvent contrôler les accès tootenant 'Test' Si contrôle de compte d’utilisateur hello créé « Test ».
* Si vous ajouter/supprimer un rôle d’administrateur d’un utilisateur dans un locataire, la fonction changement de hello ne pas les rôles d’administrateur de hello affectent ce hello utilisateur a dans un autre client.

## <a name="synchronization-independence"></a>Indépendance de la synchronisation
Vous pouvez configurer chaque Azure AD de locataire indépendamment tooget les données synchronisées à partir d’une seule instance d’un :

* outil de connexion Hello Azure AD, données toosynchronize avec une seule forêt Active Directory.
* Hello locataire Azure Active connecteur pour Forefront Identity Manager, les données toosynchronize avec l’un ou plusieurs locaux forêts et/ou des sources de données non-Azure AD.

## <a name="add-an-azure-ad-tenant"></a>Ajouter un locataire Azure AD
tooadd un locataire Azure AD Bonjour portail Azure, connectez-vous trop[hello portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global Azure AD et, sur hello gauche, sélectionnez **nouveau**.

> [!NOTE]
> Contrairement aux autres ressources Azure, vos locataires ne sont pas des ressources enfants d’un abonnement Azure. Si votre abonnement Azure est annulée ou a expiré, vous pouvez toujours accéder à vos données client à l’aide du centre d’administration hello Office 365, hello API Azure Graph ou Azure PowerShell. Vous pouvez également associer un autre abonnement hello client.
>

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir une vue d’ensemble des problèmes de licence Azure AD et découvrir les bonnes pratiques, consultez [Qu’est-ce que la gestion de licences de locataires Azure Active Directory ?](active-directory-licensing-whatis-azure-portal.md).
