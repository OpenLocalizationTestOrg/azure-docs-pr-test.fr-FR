---
title: aaaAzure AD + Active Directory requise pour Azure RemoteApp | Documents Microsoft
description: "Découvrez comment tooset des toowork d’Active Directory avec Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Configuration requise d’Azure AD et d’Active Directory pour Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Pour votre collection de hybride Azure RemoteApp ou pour une collection de cloud que vous souhaitez toofederate à l’aide d’AD Connect, toodo, hello éléments suivants sont nécessaires.

### <a name="connect-azure-ad-and-active-directory"></a>Connexion à Azure AD et Active Directory
Si vous souhaitez tooconnect votre locataire Azure AD et les environnements Active Directory local, utilisez Active Directory. Il vous faudra uniquement [4 clics](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello deux répertoires.

Remarque : la synchronisation d’annuaires est requise pour les collections hybride.

### <a name="make-sure-your-domaincom-match"></a>Vérifiez que votre @domain.com correspond
Avant de commencer, assurez-vous que hello UPN votre forêt locale correspondances le suffixe hello de votre domaine Azure AD. 

Après avoir configuré hello domaine suffixe dans Azure AD, tous les utilisateurs qui se connectent à Azure RemoteApp seront connectez-vous en tant que « utilisateur @<hello suffix you set up>. » Assurez-vous que les utilisateurs peuvent également se connecter avec hello même user@suffix dans le domaine local de hello. Dans certains cas vous pouvez configurer un nom de domaine dans Azure AD lors de la spécification d’un suffixe de domaine différent pour hello utilisateur localement. Dans ce cas, vos utilisateurs ne sont pas être en mesure de tooconnect tooany appartenant au domaine ordinateurs ou des ressources via Azure RemoteApp.

Par exemple, si vous configurez votre suffixe UPN dans AAD contoso.com, mais certains utilisateurs sur site et d’Active Directory sont toolog configuré avec @contoso.uk, ces utilisateurs ne seront pas connectez-vous toocorrectly en mesure de hello collection de ARA. Les utilisateurs de le QU'UPN dans AAD et Active Directory doit être même hello pour possible de toobe connexion hello »

### <a name="create-objects-for-azure-remoteapp"></a>Création d’objets pour Azure RemoteApp
Vous devez également hello toocreate objets d’Active Directory locaux suivants :

* Un compte tooprovide accès toodomain ressources du service pour les programmes RemoteApp en joignant le domaine de postes de travail points de terminaison toohello local.
* Une unité d’organisation (UO) toocontain RemoteApp ordinateur les objets. Utilisation de l’unité d’organisation de hello est recommandé (mais n’est pas obligatoire) tooisolate hello comptes et les stratégies que vous utiliserez avec RemoteApp.

Vous avez besoin de ces deux objets lorsque vous créez votre collection RemoteApp, soyez sûr toodo ces étapes tout d’abord.

