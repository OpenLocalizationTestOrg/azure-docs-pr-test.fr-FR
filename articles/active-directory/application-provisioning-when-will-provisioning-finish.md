---
title: "aaaUser approvisionnement d’une application de la galerie tooan Azure AD est prise en heures ou plus | Documents Microsoft"
description: "Comment toofind out pourquoi configuration tooyour application peut prendre plus de temps que prévu"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a>Configuration d’application de la galerie tooan Azure AD de l’utilisateur est tenu heures ou plus

Lorsque vous activez tout d’abord la configuration automatique pour une application, la synchronisation initiale hello peut prendre entre 20 minutes tooseveral heures, selon la taille de hello de Windows Azure AD pour hello et hello des utilisateurs dans la portée pour la configuration. 

Les synchronisations suivantes après la synchronisation initiale hello être plus rapide, hello configuration service stocke les filigranes qui représentent l’état hello des deux systèmes après la synchronisation initiale hello, améliorer les performances des synchronisations suivantes.

## <a name="how-tooimprove-provisioning-performance"></a>Comment tooimprove mise en service des performances

Si la synchronisation initiale hello prend plusieurs heures, il est une chose à faire tooimprove performances :

-   **Filtres d’étendue utilisateur**. Filtres d’étendue permettent de données hello régler toofine hello configuration extraits de service à partir d’Azure AD en filtrant les utilisateurs basés sur des valeurs d’attribut spécifiques. Pour plus d’informations sur les filtres d’étendue, consultez [Approvisionnement d’applications basé sur les attributs avec filtres d’étendue](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

## <a name="next-steps"></a>Étapes suivantes
[Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications avec Azure Active Directory](active-directory-saas-app-provisioning.md)

