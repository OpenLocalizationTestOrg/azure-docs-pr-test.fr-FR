---
title: Attribution de licences pour Azure MFA| Microsoft Docs
description: "Découvrez comment attribuer des licences pour Microsoft Azure Multi-Factor Authentication"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: 45522bf526c4aeab1d6ccc8891a55a0436ff9320
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a>Attribution d’une licence Azure MFA, Azure AD Premium ou Enterprise Mobility aux utilisateurs
Si vous avez acheté des licences Azure MFA, Azure AD Premium ou Enterprise Mobility Suite, il est inutile de créer un fournisseur Multi-Factor Auth. Une fois que vous avez attribué des licences à vos utilisateurs, vous pouvez commencer à les activer pour l’authentification multifacteur.

## <a name="to-assign-a-license"></a>Pour attribuer une licence
1. Connectez-vous en tant qu’administrateur au [portail Azure Classic](https://manage.windowsazure.com).
2. Sélectionnez **Active Directory**à gauche.
3. Sur la page Active Directory, double-cliquez sur le répertoire qui contient les utilisateurs que vous souhaitez activer.
4. En haut de la page du répertoire, sélectionnez **Licences**.
   ![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)
5. Sur la page Licences, sélectionnez **Azure Multi-Factor Authentication**, **Active Directory Premium** ou **Enterprise Mobility Suite**.  Si vous ne disposez que d’une licence, celle-ci doit normalement être sélectionnée automatiquement.
6. En bas de cette page, cliquez sur **Attribuer**.
   ![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)
7. Dans la zone qui s’affiche, cliquez en regard des utilisateurs ou groupes auxquels vous souhaitez attribuer des licences.  Une coche verte doit apparaître.
8. Cliquez sur la coche pour enregistrer les modifications.
   ![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)
9. Vous devriez voir un message indiquant le nombre de licences qui ont été attribuées et le nombre d’échecs, le cas échéant.  Cliquez sur **OK**.
   ![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)

## <a name="next-steps"></a>Étapes suivantes

- Pour plus d’informations, consultez [Qu’est-ce que la licence Microsoft Azure Active Directory ?](../active-directory/active-directory-licensing-what-is.md)
