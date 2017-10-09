---
title: "aaaSign connexions après plusieurs échecs"
description: "Un rapport indiquant les utilisateurs qui sont parvenus à se connecter, mais après plusieurs tentatives de connexion infructueuses."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a>Connexions après plusieurs échecs
Ce rapport indique les utilisateurs qui sont parvenus à se connecter, mais après plusieurs tentatives de connexion infructueuses. Les causes possibles sont :

* L’utilisateur a oublié son mot de passe</li><li>L’utilisateur est victime hello de mot de passe réussie estimation attaque en force brute

Les résultats de ce rapport affiche hello de nombre de consécutives ayant échoué tentatives de connexion effectuées toohello préalable réussie connectez-vous et un horodatage associé hello première réussie connectez-vous.

**Paramètres de rapport**: vous pouvez configurer le nombre minimal de hello d’échecs de connexion consécutifs tentatives qui doit se produire avant d’être affichée dans le rapport de hello. Lorsque vous apportez des modifications toothis définition est toonote important que ces modifications ne seront pas appliqué tooany existant ayant échoué connexions qui s’affichent actuellement dans votre rapport existant. Toutefois, ils seront appliqués tooall futures connexions. Rapport sur toothis les modifications ne sont accessibles que par les administrateurs sous licence.

![Connexions après plusieurs échecs](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

