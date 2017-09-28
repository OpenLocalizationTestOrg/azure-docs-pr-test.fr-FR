---
title: Fichier de test Sipi | Documents Microsoft
description: "Fichier de test pour vérifier les dépendances ReadyForTest"
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a>Fichier de test Sipi

Ce démarrage rapide vous aide à inscrire une application dans un client B2C Microsoft Azure Active Directory (Azure AD) en quelques minutes. Lorsque vous avez terminé, votre application est inscrite comme utilisable dans le client Azure B2C.

## <a name="prerequisites"></a>Composants requis

Pour générer une application acceptant l’inscription et la connexion des consommateurs, vous devez commencer par inscrire cette application auprès d’un client Azure Active Directory B2C. Obtenez votre propre client en suivant la procédure décrite dans [Création d’un client Azure AD B2C](active-directory-b2c-get-started.md).

Les applications créées dans le panneau Azure AD B2C dans le portail Azure doivent être gérées à partir du même emplacement. Si vous modifiez des applications B2C à l’aide de PowerShell ou d’un autre portail, ces dernières ne sont plus prises en charge et ne fonctionnent pas avec Azure AD B2C. Consultez les détails dans la section [Applications ayant généré une erreur](#faulted-apps). 

## <a name="navigate-to-b2c-settings"></a>Accéder aux paramètres B2C

Connectez-vous au [portail Azure](https://portal.azure.com/) en tant qu’administrateur général du client B2C. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

Choisissez les étapes suivantes en fonction du type d’application que vous inscrivez :
