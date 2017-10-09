---
title: aaaAzure multi-Factor Authentication - son fonctionnement
description: "L’authentification multifacteur Azure permet de toodata d’accès de sauvegarde et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Il fournit une sécurité supplémentaire en exigeant un deuxième formulaire d'authentification et fournit une authentification renforcée via un éventail d'options de vérification simples."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a>Azure Multi-Factor Authentication : fonctionnement
sécurité de Hello de vérification en deux étapes réside dans son approche en couches. Compromettre plusieurs facteurs d'authentification présente un défi de taille pour les attaquants. Même si une personne malveillante parvient toolearn hello mot de passe utilisateur, il est inutile sans également en sa possession de l’appareil de confiance hello. 

![Vérification](./media/multi-factor-authentication-how-it-works/howitworks.png)

L’authentification multifacteur Azure permet de toodata d’accès de sauvegarde et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple.  Il fournit une sécurité supplémentaire en exigeant un deuxième formulaire d'authentification et fournit une authentification renforcée via un éventail d'options de vérification simples.


## <a name="methods-available-for-two-step-verification"></a>Méthodes disponibles pour la vérification en deux étapes
Lorsqu’un utilisateur se connecte, une vérification supplémentaire est envoyée toohello utilisateur.  Hello Voici une liste des méthodes qui peut être utilisé pour cette vérification du second.

| Méthode de vérification | Description |
| --- | --- |
| appel téléphonique |Un appel est passé de téléphone enregistré de l’utilisateur tooa. utilisateur de Hello entre un code PIN si nécessaire, puis appuie sur la touche # de hello. |
| SMS |Un message texte est envoyé de téléphone mobile de l’utilisateur tooa avec un code à six chiffres. utilisateur de Hello entre ce code sur la page de connexion hello. |
| Notification sur l’application mobile |Une demande de vérification est envoyée Smartphone tooa de l’utilisateur. Hello utilisateur entre un code PIN si nécessaire, puis sélectionne **Vérifiez** sur l’application mobile hello. |
| Code de vérification de l’application mobile |application mobile Hello, qui s’exécute sur un Smartphone d’un utilisateur, affiche un code de vérification que les modifications apportées à toutes les 30 secondes. utilisateur de Hello recherche le code le plus récent hello et l’insère dans la page de connexion hello. |
| Jetons OATH tiers | Serveur Azure multi-Factor peuvent être des méthodes de vérification de l’application tierce de tooaccept configuré. |

Azure Multi-Factor Authentication fournit des méthodes de vérification sélectionnables pour cloud et pour serveur. Vous pouvez choisir les méthodes mises à la disposition de vos utilisateurs : appel téléphonique, SMS, notification sur l’application ou codes d’application. Pour plus d’informations, consultez [Méthodes de vérification sélectionnables](multi-factor-authentication-whats-next.md#selectable-verification-methods).

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur hello différents [versions et les méthodes de consommation pour l’authentification multifacteur Azure](multi-factor-authentication-versions-plans.md)

- Choisissez si toodeploy Azure MFA [dans hello ou local](multi-factor-authentication-get-started.md)

- Obtenez des réponses aux [questions fréquemment posées](multi-factor-authentication-faq.md).