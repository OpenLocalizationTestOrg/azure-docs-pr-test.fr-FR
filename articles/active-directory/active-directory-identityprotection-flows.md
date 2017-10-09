---
title: "aaaSign dans les expériences avec Azure AD Identity Protection | Documents Microsoft"
description: "Fournit une vue d’ensemble de l’expérience utilisateur hello lors de la Protection de l’identité a atténué ou mis à jour un utilisateur ou lorsque l’authentification multifacteur est requise par une stratégie."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>Expériences de connexion avec Azure AD Identity Protection
Avec Azure Active Directory Identity Protection, vous pouvez :

* exiger des utilisateurs tooregister pour l’authentification multifacteur
* gérer les connexions risquées et les utilisateurs compromis

réponse Hello des problèmes de toothese hello système a un impact sur l’expérience de connexion d’un utilisateur, car il est simplement directement de signature d’en fournissant un nom d’utilisateur et un mot de passe ne sera pas possible plus. Des étapes supplémentaires sont requis tooget un utilisateur sauvegarder en toute sécurité dans l’entreprise.

Cette rubrique donne une vue d’ensemble de l’expérience de connexion d’un utilisateur pour tous les cas qui peuvent se produire.

**Authentification multifacteur**

* Inscription à l’authentification multifacteur

**Connexion risquée**

* Récupération de connexion à risque
* Connexion à risque bloquée
* Inscription à l’authentification multifacteur au cours d’une connexion à risque

**Utilisateur à risque**

* Récupération de compte compromis
* Compte compromis bloqué

## <a name="multi-factor-authentication-registration"></a>Inscription à l’authentification multifacteur
Hello meilleure expérience utilisateur pour les deux, hello du flux de récupération de compte compromis et hello de flux de connexion présente des risques, est lorsque hello utilisateur peut les récupérer. Si les utilisateurs sont inscrits pour l’authentification multifacteur, qu’il a déjà un numéro de téléphone associé à leur compte qui peut être des défis de sécurité toopass utilisé. Sans intervention du support technique ou l’administrateur aide est toorecover nécessaire à partir de la compromission d’un compte. Par conséquent, il est vivement recommandé tooget vos utilisateurs inscrits pour l’authentification multifacteur. 

Les administrateurs peuvent :

* définir une stratégie qui impose tooset utilisateurs leurs comptes pour la vérification de sécurité supplémentaire. 
* Autoriser l’enregistrement de l’authentification multifacteur pour des jours de too30, ignoré au cas où ils souhaitent toogive utilisateurs avant d’inscrire une période de grâce.

**l’inscription de l’authentification multifacteur Hello comporte trois étapes :**

1. Dans la première étape de hello, utilisateur de hello reçoit une notification à propos hello exigence tooset hello du compte pour l’authentification multifacteur. 
   
    ![Correction](./media/active-directory-identityprotection-flows/140.png "Correction")
2. l’authentification multifacteur tooset haut, il vous faut toolet hello système savoir comment vous souhaitez toobe contacté.
   
    ![Correction](./media/active-directory-identityprotection-flows/141.png "Correction")
3. système de Hello soumet une demande d’accès tooyou et que vous devez toorespond.
   
    ![Correction](./media/active-directory-identityprotection-flows/142.png "Correction")

## <a name="risky-sign-in-recovery"></a>Récupération de connexion à risque
Lorsqu’un administrateur a configuré une stratégie de risques pour la connexion, les utilisateurs de hello affecté sont avertis quand ils essaient de toosign. 

**flux de connexion présente des risques Hello comprend deux étapes :** 

1. l’utilisateur Hello est informé que quelque chose d’inhabituel a été détecté sur leurs connectez-vous, telles que la connexion à partir d’un nouvel emplacement, appareil ou application. 
   
    ![Correction](./media/active-directory-identityprotection-flows/120.png "Correction")
2. utilisateur de Hello est requis tooprove leur identité en résolvant une vérification de sécurité. Si l’utilisateur de hello est inscrit pour l’authentification multifacteur dont ils ont besoin d’un numéro de téléphone de sécurité code tootheir de tooround-voyage. Comme il s’agit seulement un risque de connexion et non un compte compromis, utilisateur de hello ne devra pas un mot de passe toochange hello dans ce flux. 
   
    ![Correction](./media/active-directory-identityprotection-flows/121.png "Correction")

## <a name="risky-sign-in-blocked"></a>Connexion à risque bloquée
Les administrateurs peuvent également choisir des tooset une ouverture de session risque stratégie tooblock des utilisateurs lors de l’authentification en fonction du niveau de risque hello. tooget débloqué, les utilisateurs finaux doivent contacter un administrateur ou le support technique, ou ils peuvent essayez de vous connecter à partir d’un emplacement de votre choix ou un périphérique. Il n’a pas la possibilité de récupérer lui-même son compte en résolvant l’authentification multifacteur dans ce cas précis.

![Correction](./media/active-directory-identityprotection-flows/200.png "Correction")

## <a name="compromised-account-recovery"></a>Récupération de compte compromis
Lorsqu’une stratégie de sécurité risque utilisateur a été configurée, les utilisateurs qui répondent aux utilisateurs de hello risque au niveau spécifié dans la stratégie de hello (et sont donc supposés compromis) doivent passer par le flux de restauration hello utilisateur compromis avant qu’ils peuvent se connecter au. 

**flux de restauration Hello utilisateur compromis comporte trois étapes :**

1. Hello l’utilisateur est informé que leur sécurité du compte est menacée en raison d’une activité suspecte ou une fuite des informations d’identification.
   
    ![Correction](./media/active-directory-identityprotection-flows/101.png "Correction")
2. utilisateur de Hello est requis tooprove leur identité en résolvant une vérification de sécurité. Si l’utilisateur de hello est inscrit pour l’authentification multifacteur ils peuvent récupérer automatiquement à partir de la compromission. Ils devront tooround-trip un numéro de téléphone de sécurité code tootheir. 
   
   ![Correction](./media/active-directory-identityprotection-flows/110.png "Correction")
3. Enfin, hello utilisateur est forcé toochange leur mot de passe, car une autre personne peut avoir eu accès tootheir compte. 
   Vous trouverez ci-dessous des captures d’écran de cette expérience.
   
   ![Correction](./media/active-directory-identityprotection-flows/111.png "Correction")

## <a name="compromised-account-blocked"></a>Compte compromis bloqué
tooget un utilisateur qui a été bloqué par une stratégie de sécurité utilisateur risque débloquée, utilisateur de hello doit contacter un administrateur ou le support technique. Il n’a pas la possibilité de récupérer lui-même son compte en résolvant l’authentification multifacteur dans ce cas précis.

![Correction](./media/active-directory-identityprotection-flows/104.png "Correction")

## <a name="reset-password"></a>Réinitialiser le mot de passe
Si des utilisateurs compromis voient leur connexion bloquée, un administrateur peut générer un mot de passe temporaire pour eux. les utilisateurs de Hello ont toochange leur mot de passe pendant une prochaine connexion de.

![Correction](./media/active-directory-identityprotection-flows/160.png "Correction")

## <a name="see-also"></a>Voir aussi
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md) 

