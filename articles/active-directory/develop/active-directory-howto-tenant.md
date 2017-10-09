---
title: aaaHow tooget un locataire Azure AD | Documents Microsoft
description: "Comment tooget Azure Active Directory du client pour l’inscription et la création d’applications."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Comment tooget Azure Active Directory de client
Dans Azure Active Directory (Azure AD), un [client](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) est représentatif d'une organisation.  Il s’agit d’une instance dédiée de hello service Azure AD qui une entreprise reçoit et possède quand elle s’inscrit à un service de cloud Microsoft comme Office 365, Microsoft Intune ou Azure.  Chaque client Azure AD est distinct et indépendant des autres clients Azure AD.  

Un locataire héberge utilisateurs hello dans une entreprise et hello informations - leurs mots de passe, les données de profil utilisateur, autorisations et ainsi de suite.  Il contient également des groupes, des applications et des autres informations se rapportant tooan organisation et sa sécurité.

tooallow le toosign les utilisateurs Azure AD dans tooyour application, vous devez inscrire votre application dans un client de votre choix.  La publication d'une application dans un client Azure AD est **absolument gratuite**.  En fait, la plupart des développeurs créent plusieurs clients et applications pour expérimenter, développer, organiser et tester.  Les organisations qui s’inscrire et utilisent votre application peuvent éventuellement choisir toopurchase licences s’ils le souhaitent parti tootake de fonctionnalités avancées active.

Mais comment faire pour obtenir un client Azure AD ?  Hello processus peut être un peu les différents cas vous :

* [Vous avez un abonnement Office 365 en cours](#use-an-existing-office-365-subscription)
* [Vous avez un abonnement Azure en cours associé à un compte Microsoft](#use-an-msa-azure-subscription)
* [Vous avez un abonnement Azure en cours associé à un compte professionnel](#use-an-organizational-azure-subscription)
* [N’ont aucune de hello ci-dessus et souhaitez toostart à partir de zéro](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Utilisation d’un abonnement Office 365 en cours
Si vous avez un abonnement à Office 365 existant, vous disposez déjà d’un client Azure AD ! Vous pouvez vous connecter toohello [portail Azure](https://portal.azure.com) avec votre O365 et démarrer à l’aide d’Azure AD.

## <a name="use-an-msa-azure-subscription"></a>Utilisation d’un abonnement Microsoft Azure
Si vous vous êtes déjà inscrit à un abonnement Azure avec votre compte individuel Microsoft, vous avez déjà un client !  Lorsque vous ouvrez une session dans toohello [Azure Portal](https://portal.azure.com), vous serez automatiquement connecté dans le locataire de tooyour par défaut. Vous êtes libre toouse ce client que vous consultez tenir - mais vous pouvez toocreate un compte d’administrateur d’organisation.

toodo par conséquent, ces étapes.  Ou bien, vous pouvez souhaitez toocreate un nouveau client et créer un administrateur de ce client suivant un processus similaire.

1. Ouvrez une session sur hello [portail Azure](https://portal.azure.com) avec votre compte individuel
2. Parcourir la section « Azure Active Directory » de toohello du portail de hello (trouvé dans la barre de navigation gauche de hello, sous **plus Services**)
3. Vous devez automatiquement être connecté toohello « Annuaire par défaut », sinon vous pouvez changer de répertoire en cliquant sur le nom de votre compte dans le coin supérieur droit de hello.
4. À partir de hello **tâches rapides** , choisissez **ajouter un utilisateur**.
5. Dans l’hello le formulaire Ajouter des utilisateurs, fournissez hello les détails suivants :

   * Nom : (choisissez une valeur appropriée)
   * Nom d'utilisateur : (choisissez un nom d'utilisateur pour cet administrateur)
   * Profil : (renseignez hello approprié pour le prénom, nom, fonction et service)
   * Rôle : administrateur général
6. Lorsque vous avez terminé hello le formulaire Ajouter des utilisateurs et recevoir hello un mot de passe temporaire pour un utilisateur administratif hello, être toorecord que ce mot de passe car vous en aurez besoin toologin avec ce nouvel utilisateur dans le mot de passe ordre toochange hello. Vous pouvez également envoyer un mot de passe hello directement toohello utilisateur, à l’aide d’un autre e-mail.
7. Cliquez sur **créer** utilisateur toocreate hello.
8. toochange hello mot de passe temporaire, ouvrez une session sur [https://login.microsoftonline.com](https://login.microsoftonline.com) avec ce nouvel utilisateur de compte et modifier le mot de passe hello lorsqu’il est demandé.

## <a name="use-an-organizational-azure-subscription"></a>Utilisation d’un abonnement Azure professionnel
Si vous vous êtes déjà inscrit à un abonnement Azure avec votre compte professionnel, vous avez déjà un client !  Bonjour [Azure Portal](https://portal.azure.com), vous devez rechercher un client lorsque vous accédez trop « Plus Services » et « Azure Active Directory. »  Vous êtes libre toouse ce client que vous consultez ajuster.

## <a name="start-from-scratch"></a>Commencer à partir de zéro
Si tout hello ci-dessus est incompréhensible tooyou, ne vous inquiétez pas.  Visitez simplement [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) toosign pour Azure avec une organisation.  Une fois que vous avez terminé le processus de hello, vous aurez votre propre locataire Azure AD avec nom de domaine hello choisi lors de l’authentification des.  Bonjour [Azure Portal](https://portal.azure.com), vous pouvez trouver votre locataire en accédant trop « Azure Active Directory » dans hello, gauche NAV.

Dans le cadre du processus de hello de s’inscrire à Azure, vous serez détails de la carte de crédit tooprovide requis.  Vous pouvez procéder en toute confiance. Vous ne serez pas facturé pour la publication d'applications dans Azure AD ou la création de nouveaux clients.
