---
title: "client d’Azure Active Directory hello aaaChange dans Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment client Azure Active Directory de hello toochange associé à Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>Changer le locataire d’Azure Active Directory hello dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp utilise l’accès des utilisateurs tooallow Azure Active Directory (Azure AD). client Hello uniquement à Azure AD que vous pouvez utiliser dans Azure RemoteApp est hello associé hello abonnement Azure. Vous pouvez afficher les abonnement hello associé sur hello **paramètres** page hello portail. Examinez hello **active** colonne hello **abonnements** onglet.

> [!NOTE]
> Pour cette modification toosucceed, tout d’abord supprimer tous les utilisateurs à partir de client Azure Active Directory existant hello de toutes les collections Azure RemoteApp. toodo, accédez toohello portail Azure, accédez toohello **Azure RemoteApp** onglet et ouvrir chaque collection Azure RemoteApp. Accédez toohello **utilisateurs** onglet et supprimer des utilisateurs qui appartiennent tooyour locataire d’Azure Active Directory actuel. Répétez l’opération pour toutes les collections Azure RemoteApp. Sans cela, vous ne serez pas en mesure de toocreate ou des collections de correctif.
> 
> 

Si vous voulez toouse un autre client, utilisez ces étapes toochange hello associé à votre abonnement :

1. Dans le portail hello, supprimez tout toowhich d’utilisateurs Azure AD vous avez donné accès tooAzure RemoteApp collections. (Voir Remarque hello ci-dessus pour obtenir des instructions sur la façon de toodo cela.)
2. Définir un compte Microsoft (anciennement appelé Live ID) en tant qu’administrateur de Service hello. (Ne pas savoir si vous êtes déjà administrateur de service hello ? Vous pouvez vous en assurer en cliquant sur **Paramètres -> Administrateurs**.) À présent, voici comment effectuer les modifications
   
   1. Cliquez sur un utilisateur dans le coin supérieur droit de hello hello, puis cliquez sur **afficher ma facture**.
   2. Cliquez sur l’abonnement hello. Dans nouvelle page de hello, faites défiler la liste, puis cliquez sur **modifier les détails de l’abonnement** Bonjour droite. (Tri de hello intermédiaire en bas à droite, si cela vous aide à trouver.)
   3. Type de compte Microsoft de hello pour utilisateur hello qui doit être administrateur de service hello.
3. Maintenant, déconnectez-vous hello portail et puis reconnectez-vous avec hello compte Microsoft que vous avez spécifié à l’étape précédente de hello.
4. Cliquez sur **Nouveau -> Services d’application -> Active Directory -> Annuaire -> Création personnalisée**.
5. Sous **Annuaire**, choisissez **Utiliser un annuaire existant**. Nous allons toohave toosign vous déconnecte du portail hello maintenant, choisissez **je suis prêt toobe me déconnecter**.
6. Vous reconnecter à hello portail en tant qu’administrateur général du répertoire de hello souhaité tooadd. (Si vous n'étiez pas déjà un administrateur général, vous le serez après vous être reconnecté et déconnecté.)
7. Vous êtes invité lors de la connexion si vous souhaitez toouse votre client Active Directory existant avec votre abonnement. Cliquez sur **Continuer**, puis sur **Se déconnecter maintenant**.
8. Vous reconnecter et revenir trop**Paramètres -> abonnements**. Sélectionnez votre abonnement, puis cliquez sur **Modifier l'annuaire**. Sélectionnez le locataire hello Azure AD que vous souhaitez toouse.

Vous pouvez maintenant utiliser hello AD Azure nouveau locataire toocontrol accès toohello accès d’utilisateur abonnement et tooconfigure Azure dans Azure RemoteApp.

