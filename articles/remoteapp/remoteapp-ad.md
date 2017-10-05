---
title: "Configuration requise d’Azure AD et d’Active Directory pour Azure RemoteApp | Microsoft Docs"
description: "Découvrez comment configurer Active Directory pour l'utiliser avec Azure RemoteApp."
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
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Configuration requise d’Azure AD et d’Active Directory pour Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Si vous souhaitez fédérer une collection hybride RemoteApp Azure ou une collection cloud à l’aide d’AD Connect, vous devez procéder ainsi.

### <a name="connect-azure-ad-and-active-directory"></a>Connexion à Azure AD et Active Directory
Si vous souhaitez connecter votre locataire Azure AD et vos environnements Active Directory locaux, utilisez AD Connect. Il vous faudra simplement [cliquer 4 fois](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) pour connecter les deux annuaires.

Remarque : la synchronisation d’annuaires est requise pour les collections hybride.

### <a name="make-sure-your-domaincom-match"></a>Vérifiez que votre @domain.com correspond
Avant de commencer, assurez-vous que l’UPN de votre forêt locale correspond au suffixe de votre domaine Azure AD. 

Une fois que vous avez configuré le suffixe du domaine UPN dans Azure AD, tous les utilisateurs se connectant dans Azure RemoteApp sont connectés en tant que « utilisateur@<the suffix you set up> ». Assurez-vous que les utilisateurs peuvent également ouvrir une session avec le même user@suffix dans le domaine local. Dans certains cas vous pouvez configurer un nom de domaine dans Azure AD lors de la spécification d’un suffixe de domaine différent pour l’utilisateur local. Dans ce cas, vos utilisateurs ne peuvent plus se connecter à des ordinateurs ou des ressources appartenant à un domaine via Azure RemoteApp.

Par exemple, si vous configurez votre suffixe de domaine UPN dans AAD en tant que contoso.com, mais que certains utilisateurs locaux/AD sont configurés pour se connecter avec @contoso.uk, ces utilisateurs ne pourront pas se connecter correctement à la collection ARA. L’UPN des utilisateurs doit être le même pour AAD et AD pour permettre la connexion.

### <a name="create-objects-for-azure-remoteapp"></a>Création d’objets pour Azure RemoteApp
Vous devez également créer les objets Active Directory locaux suivants :

* Un compte de service afin de fournir l'accès aux ressources du domaine pour les programmes RemoteApp, en rattachant des points de terminaison RDSH au domaine local.
* Une unité d'organisation pour contenir les objets ordinateur RemoteApp. L'utilisation de l'unité d'organisation est recommandée (mais pas obligatoire) pour isoler les comptes et les stratégies que vous utiliserez avec RemoteApp.

Vous avez besoin de ces deux objets lorsque vous créez votre collection RemoteApp ; veuillez donc vous assurer d’avoir déjà effectué ces étapes.

