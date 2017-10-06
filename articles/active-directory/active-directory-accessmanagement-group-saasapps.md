---
title: "aaaUsing un tooSaaS d’accès groupe toomanage Applications | Documents Microsoft"
description: "Comment les groupes dans Azure Active Directory Premium ou Basic tooassign toouse d’accéder aux applications tooSaaS sont intégrées à Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>À l’aide d’une application de groupe toomanage accès tooSaaS
À l’aide d’Azure Active Directory (Azure AD) avec une licence Azure AD Premium ou Azure AD Basic, vous pouvez utiliser des groupes tooassign accès tooa application SaaS intégrée à Azure AD. Par exemple, si vous souhaitez accéder tooassign pour hello marketing service toouse cinq applications SaaS différentes, vous pouvez créer un groupe qui contient des utilisateurs hello hello département de marketing et puis affectez ce groupe toothese cinq applications SaaS qui sont requis par le service marketing de hello. Cette façon vous pouvez gagner du temps en gérant l’appartenance de hello Hello marketing service dans un seul emplacement. Les utilisateurs sont ensuite affectées toohello application lorsqu’ils sont ajoutés en tant que membres du groupe marketing de hello et leur affectation est supprimée à partir de l’application hello lorsqu’ils sont supprimés hello groupe marketing.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. 

Cette fonctionnalité peut être utilisée avec des centaines d’applications que vous pouvez ajouter à partir de hello Galerie d’applications Azure AD.

**accès tooassign pour un groupe de tooa application SaaS**

1. Bonjour [portail Azure classic](https://manage.windowsazure.com), sélectionnez **Active Directory** sur la barre de navigation hello sur le côté gauche de hello.
2. Sélectionnez hello **répertoire** onglet et répertoire puis ouvrez hello dans lequel vous souhaitez tooassign l’accès pour un groupe de tooa application SaaS.
3. Sélectionnez hello **Applications** onglet. Sélectionnez une application que vous avez ajouté à partir de hello Galerie d’applications, puis cliquez sur hello **utilisateurs et groupes** onglet.
4. Sur hello **utilisateurs et groupes** onglet hello **commençant par** , entrez le nom de hello de hello groupe toowhich vous choix tooassign accès, puis sélectionnez hello case à cocher dans le coin supérieur droit de hello. Vous ne devez tootype hello première partie du nom d’un groupe.
5. Sélectionnez le groupe de hello, puis sélectionnez hello **attribuer un accès** bouton. Sélectionnez **Oui** lorsque vous voyez le message de confirmation hello. Appartenances aux groupes imbriqués ne sont pas pris en charge pour l’affectation basée sur le groupe tooapplications à ce stade.
6. Vous pouvez également voir quels utilisateurs sont affectés toohello application, directement ou par l’appartenance à un groupe. toodo, hello modification **afficher la liste déroulante à partir de « Groupes »** trop**« Tous les utilisateurs »**. liste de Hello montre aux utilisateurs dans le répertoire de hello et s’il faut ou non chaque utilisateur se voit affecter toohello application. liste de Hello indique également si les utilisateurs de hello affecté assignés toohello application directement (type d’affectation « Direct »), ou en vertu de l’appartenance au groupe (type d’affectation comme « Hérité »)

> [!NOTE]
> Vous pouvez voir hello utilisateurs et onglet groupes uniquement après avoir activé Azure AD Premium ou Azure AD Basic.
>
>

### <a name="next-steps"></a>Étapes suivantes
Ces articles fournissent des informations supplémentaires sur Azure Active Directory.

* [La gestion des accès tooresources avec les groupes Azure Active Directory](active-directory-manage-groups.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Configuration des paramètres de groupe avec les applets de commande Azure Active Directory](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md)
* [Intégration des identités locales dans Azure Active Directory](active-directory-aadconnect.md)
