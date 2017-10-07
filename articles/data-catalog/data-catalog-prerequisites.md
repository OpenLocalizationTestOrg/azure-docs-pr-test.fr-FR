---
title: "conditions préalables du catalogue de données aaaAzure | Documents Microsoft"
description: "En savoir plus sur la configuration requise de hello que vous devez tooget main d’Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Configuration requise pour Azure Data Catalog

Vous devez tootake administration quelques éléments avant que vous pouvez configurer Azure Data Catalog. Ce processus ne sera pas long.

## <a name="azure-subscription"></a>Abonnement Azure
tooset catalogue de données, vous devez être propriétaire de hello ou copropriétaire d’un abonnement Azure.

Abonnements Azure permettent d’organiser d’accéder aux ressources de service toocloud tels que des données de catalogue. Ils vous permettent également de contrôler le signalement, la facturation et le paiement des ressources utilisées. Chaque abonnement peut disposer d’une configuration de facturation et de paiement différente. Vous pouvez donc avoir différents abonnements et différents plans par département, projet, bureau régional, etc. Chaque service cloud appartient tooa abonnement, et vous devez toohave un abonnement avant de configurer le catalogue de données. toolearn, voir [gérer les comptes, les abonnements et les rôles d’administrateur](../active-directory/active-directory-assign-admin-roles.md).

## <a name="azure-active-directory"></a>Azure Active Directory
tooset catalogue de données, vous devez être connecté avec un compte d’utilisateur Azure Active Directory (Azure AD).

Azure AD fournit un moyen simple pour votre entreprise toomanage identités et des accès, à la fois dans le cloud de hello et sur site. Les utilisateurs peuvent utiliser un seul compte professionnel ou scolaire pour le cloud de tooany de connexion unique et une application de web local. Catalogue de données utilise l’authentification dans Azure AD tooauthenticate. toolearn, voir [quoi consiste Azure Active Directory ?](../active-directory/active-directory-whatis.md).

> [!NOTE]
> À l’aide de hello [portail Azure](http://portal.azure.com/), vous pouvez vous connecter avec un compte Microsoft personnel ou d’Azure Active Directory ou l’école de compte. tooset catalogue de données à l’aide de hello soit portail Azure ou hello [portail Data Catalog](http://www.azuredatacatalog.com), vous devez vous connecter avec un compte Azure Active Directory, pas un compte personnel.
>
>

## <a name="active-directory-policy-configuration"></a>Configuration de la stratégie Active Directory
Vous pouvez rencontrer une situation où vous pouvez vous connecter dans le portail de toohello Data Catalog, mais lorsque vous essayez de toosign dans l’outil de l’enregistrement de source de données toohello, un message d’erreur qui vous empêche de se connecter. Ce problème peut se produire uniquement lorsque vous êtes sur le réseau d’entreprise hello, ou elle peut se produire uniquement lorsque vous vous connectez à partir du réseau d’entreprise en dehors de hello.

outil de l’enregistrement de source de données Hello utilise l’authentification par formulaire toovalidate vos informations d’identification de l’utilisateur dans Active Directory. toohelp que vous vous connectez avec succès, un administrateur Active Directory doit activer l’authentification par formulaire Bonjour stratégie d’authentification globale.

Bonjour stratégie d’authentification globale, méthodes d’authentification peuvent être activées séparément pour l’intranet et extranet des connexions, comme indiqué dans hello suivant capture d’écran de. Erreurs de connexion peuvent se produire si l’authentification par formulaire n’est pas activée pour le réseau hello à partir de laquelle vous vous connectez.

 ![Stratégie d’authentification globale d’Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez [Configuration des stratégies d’authentification](https://technet.microsoft.com/library/dn486781.aspx).
