---
title: "aaaHow toochange hello durée de vie par défaut pour une application personnalisée | Documents Microsoft"
description: "Comment les stratégies de durée de vie de jeton tooupdate pour votre application que vous développez sur Azure AD"
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
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a>La durée de vie toochange hello par défaut pour une application personnalisée

Azure AD Premium permet aux développeurs d’application et client administrateurs tooconfigure hello durée de vie des jetons émis pour les clients non confidentielle. Stratégies de durée de vie de jeton sont définies sur un client à l’échelle ou ressources hello en cours d’accès.

 * tooset une stratégie de durée de vie de jeton, vous devez les hello toodownload [Module PowerShell Azure AD](https://www.powershellgallery.com/packages/AzureADPreview).

 * Exécutez hello **organisation de se connecter-confirmer** commande.

 * Voici un exemple de stratégie qui définit le jeton d’actualisation hello âge max facteur unique. Créez la stratégie de hello :```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Hello d’extraction [durée de vie de jeton configuration](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) document toolearn comment toocreate autres personnalisé.

## <a name="next-steps"></a>Étapes suivantes
[Durées de vie des jetons configurables dans Azure Active Directory (version préliminaire publique)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Référence sur les jetons Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

