---
title: Fichier de test Sipi | Documents Microsoft
description: "Tester les dépendances de fichier toocheck ReadyForTest"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a>Fichier de test Sipi

Ce démarrage rapide vous aide à inscrire une application dans un client B2C Microsoft Azure Active Directory (Azure AD) en quelques minutes. Lorsque vous avez terminé, votre application est enregistrée pour une utilisation dans le locataire de hello Azure B2C.

## <a name="prerequisites"></a>Composants requis

toobuild une application qui accepte le consommateur d’inscription et de connexion, vous devez tout d’abord d’application de hello tooregister avec un locataire Azure Active Directory B2C. Obtenir votre propre locataire à l’aide de hello étapes [créer un client Azure AD B2C](active-directory-b2c-get-started.md).

Les applications créées à partir du panneau hello Azure AD B2C Bonjour portail Azure doivent être gérées à partir de hello même emplacement. Si vous modifiez les applications B2C hello à l’aide de PowerShell ou un autre portail, ils deviennent non pris en charge et ne fonctionnent pas avec Azure Active Directory B2C. Consultez les détails dans hello [a généré une erreur d’applications](#faulted-apps) section. 

## <a name="navigate-toob2c-settings"></a>Accédez tooB2C paramètres

Connectez-vous à toohello [portail Azure](https://portal.azure.com/) comme hello administrateur Global du client de hello B2C. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

Choisissez les étapes suivantes, selon le type d’application hello que l’inscription :
