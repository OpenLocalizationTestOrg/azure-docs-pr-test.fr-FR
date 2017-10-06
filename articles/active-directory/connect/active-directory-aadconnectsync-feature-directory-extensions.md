---
title: "Azure AD Connect Sync : extensions d’annuaire | Microsoft Docs"
description: "Cette rubrique décrit la fonctionnalité d’extensions de répertoire hello dans Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Azure AD Connect Sync : extensions d’annuaire
Extensions d’annuaire vous permet de schéma de hello tooextend dans Azure AD avec vos propres attributs à partir d’Active Directory local. Cette fonctionnalité permet des applications métier toobuild consommation attributs vous continuez toomanage local. Ces attributs peuvent être utilisés via des [extensions d’annuaire Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) ou [Microsoft Graph](https://graph.microsoft.io/). Vous pouvez voir hello disponible à l’aide des attributs [explorer d’Azure AD Graph](https://graphexplorer.cloudapp.net) et [l’Explorateur Microsoft Graph](https://graphexplorer2.azurewebsites.net/) respectivement.

Actuellement, aucune charge de travail Office 365 n’utilise ces attributs.

Vous configurez les attributs supplémentaires souhaitées toosynchronize dans chemin d’accès des paramètres personnalisés hello dans l’Assistant installation hello.
![Assistant d’extension de schéma](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
installation de Hello montre hello suivant des attributs qui sont des candidats valides :

* Types d’utilisateur et d’objet de groupe
* Attributs à valeur unique : chaîne, booléen, entier, binaire
* Attributs à valeurs multiples : chaîne, binaire

liste de Hello d’attributs est lue à partir du cache de schéma hello créé pendant l’installation d’Azure AD Connect. Si vous avez étendu le schéma Active Directory de hello avec des attributs supplémentaires, puis hello [schéma doit être actualisé](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) avant que ces nouveaux attributs sont visibles.

Un objet dans Azure AD peut avoir les attributs de too100 répertoire extensions. la longueur maximale Hello est de 250 caractères. Si une valeur d’attribut est plus longue, il est tronqué par le moteur de synchronisation hello.

Lors de l’installation d’Azure AD Connect, une application dans laquelle ces attributs sont disponibles est enregistrée. Vous pouvez voir cette application Bonjour portail Azure.  
![Application d’extension de schéma](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Ces attributs sont désormais disponibles via Graph :   
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

attributs de Hello sont préfixés avec l’extension\_{AppClientId}\_. Hello AppClientId a hello même valeur pour tous les attributs dans votre locataire Azure AD.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
