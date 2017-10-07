---
title: "Azure Active Directory B2C : Résoudre les problèmes liés à la création de locataires | Microsoft Docs"
description: "Problèmes et résolutions pour la création d’un locataire Azure Active Directory ou Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a>Résoudre les problèmes de création d’un locataire Azure Active Directory ou Azure Active Directory B2C 

## <a name="create-an-azure-ad-tenant"></a>Créer un locataire Azure AD
Si vous ne peut pas créer un locataire Azure Active Directory (Azure AD) sur la première tentative de hello, essayez à nouveau. Si hello problème persiste, contactez le Support de Azure.

## <a name="create-an-azure-ad-b2c-tenant"></a>Créer un client Azure AD B2C
Si vous rencontrez des problèmes lorsque vous [créer un B2C d’Active Directory de Azure (B2C Active Directory de Azure) client](active-directory-b2c-get-started.md), essayez hello options suivantes :

* Si le client de hello Azure AD B2C n’apparaît pas dans votre liste de clients, essayez à nouveau locataire de hello toocreate.
* Si locataire de hello Azure AD B2C s’affiche dans la liste des locataires hello message d’erreur suivant s’affiche, supprimer le client de hello et créez-en un nouveau :

    « Impossible de terminer la création de hello du client de B2C hello 'contosob2c'. Visitez ce [lien](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) pour plus d’informations. »
* Il sont problèmes connus lorsque vous supprimez un B2C d’AD Azure existant du locataire et créer de nouveau à l’aide de hello même nom de domaine. Quand vous créez un locataire Azure AD B2C, vous devez utiliser un nom de domaine différent.
* Si aucune de ces solutions ne résout votre problème, contactez le support technique Azure. Pour plus d’informations, consultez [Prise en charge des demandes d’assistance pour Azure AD B2C](active-directory-b2c-support.md).

