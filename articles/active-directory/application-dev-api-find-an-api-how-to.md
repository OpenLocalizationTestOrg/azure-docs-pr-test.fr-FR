---
title: "aaaHow toofind une API spécifique est nécessaire pour une application personnalisée | Documents Microsoft"
description: "Comment tooconfigure hello autorisations tooaccess une API particulière dans votre développement application Azure AD"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>Comment toofind une API spécifique est nécessaire pour une application personnalisée

Accès tooAPIs nécessite la configuration des étendues d’accès et des rôles. Si vous souhaitez tooexpose vos ressources d’applications web API tooclient applications, vous devez tooconfigure accès étendues et des rôles pour hello API. Si vous souhaitez un tooaccess d’application client une API web, vous devez tooconfigure autorisations tooaccess hello API dans l’inscription d’une application hello.

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configuration d’un site web tooexpose d’application de ressource API

Lorsque vous exposez votre API web, hello API affichera Bonjour **sélectionner une API** liste lors de l’ajout d’inscription d’une application tooan autorisations. étendues d’accès tooadd, suivez les instructions de hello dans [Ajout d’accès étendues application de ressource tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configuration d’un ordinateur client application tooaccess web API

Lorsque vous ajoutez d’inscription d’une application tooyour autorisations, vous pouvez **ajouter l’accès aux API** tooexposed web API. tooaccess API web, suivez les étapes de hello décrites dans [ajoutez tooaccess des informations d’identification ou des autorisations web API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).

## <a name="next-steps"></a>Étapes suivantes

-   [Intégration d’applications dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [Présentation de manifeste de l’application hello Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


