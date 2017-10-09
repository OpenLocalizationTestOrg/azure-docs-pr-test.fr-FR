---
title: Application Extensions - Azure AD B2C | Microsoft Docs
description: Restauration des extensions b2c-application hello
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C : application Extensions

Lors de la création d’un annuaire Azure AD B2C, une application appelée `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` est automatiquement créé à l’intérieur de hello nouveau répertoire. Cette application, le tooas référencé hello **b2c-extensions-app**, est visible dans *inscriptions d’application*. Il est utilisé par hello Azure AD B2C service toostore informations utilisateurs et les attributs personnalisés. Si l’application hello est supprimée, Azure AD B2C ne fonctionnera pas correctement et votre environnement de production est affectée.

> [!IMPORTANT]
> Ne supprimez pas les extensions b2c-application hello, sauf si vous envisagez de supprimer des tooimmediately votre client. Si l’application hello reste supprimée depuis plus de 30 jours, les informations utilisateur seront définitivement perdues.

## <a name="verifying-that-hello-extensions-app-is-present"></a>Vérification de cette application d’extensions hello est présente

tooverify qui hello b2c-extensions-app est présente :

1. À l’intérieur de votre locataire Azure AD B2C, cliquez sur **davantage de services** dans le menu de navigation gauche hello.
1. Recherchez et ouvrez **Inscriptions des applications**.
1. Recherchez une application dont le nom commence par **b2c-extensions-app**

## <a name="recover-hello-extensions-app"></a>Récupérer l’application des extensions hello

Si vous avez supprimé accidentellement hello b2c-extensions-app, vous avez 30 jours toorecover il. Vous pouvez restaurer l’application hello hello API Graph à l’aide de :

1. Parcourir trop[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).
1. Connectez-vous toohello site comme un administrateur global pour le répertoire d’Azure AD B2C hello souhaité toorestore d’application hello supprimé pour.
1. Émettre un verbe HTTP GET pour l’URL de hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` avec api-version = 1,6. Assurez-vous que tooreplace `{tenantName}` avec votre nom de client. Cette opération répertorie toutes les applications hello qui ont été supprimées dans hello 30 derniers jours.
1. Application hello de trouver dans la liste hello où le nom de hello commence avec 'b2c-extension-app' et copie son `objectid` valeur de propriété.
1. Émettre une requête HTTP POST par rapport à l’URL de hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`. Remplacez hello `{OBJECTID}` partie de l’URL de hello avec hello `objectid` à partir de l’étape précédente de hello. 

Vous devez maintenant être en mesure de trop[consultez application hello restauré](#verifying-that-the-extensions-app-is-present) Bonjour portail Azure.

> [!NOTE]
> Une application ne peut être restaurée que si elle a été supprimée dans hello 30 derniers jours. Après ce délai, les données sont définitivement perdues. Pour obtenir de l’aide, soumettez un ticket de support.
