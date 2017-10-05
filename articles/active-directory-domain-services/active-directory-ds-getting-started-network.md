---
title: "Bien démarrer avec Azure Active Directory Domain Services | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide du portail Azure (préversion)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a>Activer Azure Active Directory Domain Services à l’aide du portail Azure (préversion)


## <a name="before-you-begin"></a>Avant de commencer
Reportez-vous à [Considérations relatives à la mise en réseau pour Azure Active Directory Domain Services](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Tâche 2 : Configurer les paramètres réseau
La tâche de configuration suivante consiste à créer un réseau virtuel Azure et un sous-réseau dédié à l’intérieur de celui-ci. Vous activez Azure Active Directory Domain Services dans ce sous-réseau de votre réseau virtuel. Vous pouvez également sélectionner un réseau virtuel actuel et créez le sous-réseau dédié à l’intérieur de celui-ci.

1. Cliquez sur **Réseau virtuel** pour choisir un réseau virtuel.
2. Dans le panneau **Choisir un réseau virtuel**, vous voyez tous les réseaux virtuels actuels. Vous voyez uniquement les réseaux virtuels qui appartiennent au groupe de ressources et à l’emplacement Azure que vous avez sélectionnés dans la page **Fonctions de base** de l’Assistant.

3. Choisissez le réseau virtuel dans lequel Azure AD Domain Services doit être activé. Si vous préférez créer un réseau virtuel, cliquez sur **Créer**. Nous vous recommandons vivement d’utiliser un sous-réseau dédié pour Azure AD Domain Services. Si vous sélectionnez un réseau virtuel existant, [créez un sous-réseau dédié à l’aide de l’extension de réseaux virtuels](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), puis choisissez ce sous-réseau. 

    ![Sélectionner un réseau virtuel](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Cliquez sur **Sous-réseau** pour sélectionner le sous-réseau dédié dans ce réseau virtuel, dans lequel activer votre nouveau domaine managé. Dans le panneau **Créer un sous-réseau**, spécifiez un nom pour le sous-réseau, puis cliquez sur **OK** lorsque vous avez terminé. Par exemple, créez un sous-réseau nommé « DomainServices », de façon à aider les autres administrateurs à comprendre ce qui est déployé au sein du sous-réseau.

    ![Sélectionner un sous-réseau au sein du réseau virtuel](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Indications pour la sélection d’un sous-réseau**
  > 1. Utilisez un sous-réseau dédié pour Azure AD Domain Services. Ne déployez pas d’autres machines virtuelles sur ce sous-réseau. Cette configuration vous permet de configurer des groupes de sécurité réseau (NSG) pour vos charges de travail ou machines virtuelles sans perturber votre domaine managé. Pour plus de détails, consultez [Considérations relatives à la mise en réseau pour Azure Active Directory Domain Services](active-directory-ds-networking.md).
  2. Ne sélectionnez pas le sous-réseau de passerelle pour déployer Azure AD Domain Services, car cette configuration n’est pas prise en charge.
  3. Vérifiez que le sous-réseau que vous avez sélectionné dispose d’un espace suffisant, comprenant entre 3 et 5 adresses IP disponibles.
  >

5. Lorsque vous avez terminé, cliquez sur **OK** pour accéder à la page **Groupe des administrateurs** de l’Assistant.


## <a name="next-step"></a>Étape suivante
[Tâche 3 : Configurer le groupe d’administration et activer Azure AD Domain Services](active-directory-ds-getting-started-admingroup.md)
