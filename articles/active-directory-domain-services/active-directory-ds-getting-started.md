---
title: "Bien démarrer avec Azure Active Directory Domain Services | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)"
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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)
Cet article explique comment tooenable Active Directory domaine Services Azure (Azure AD DS) à l’aide de hello portail Azure.


toolaunch hello **activer un domaine Azure AD Services** hello Assistant, complète comme suit :

1. Accédez toohello [portail Azure](https://portal.azure.com).
2. Dans le volet gauche de hello, cliquez sur **nouveau**.
3. Bonjour **nouveau** panneau, tapez **Services de domaine** dans la barre de recherche hello.

    ![Rechercher Domain Services](./media/getting-started/search-domain-services.png)

4. Cliquez sur tooselect **les Services de domaine Active Directory de Azure** à partir de la liste de hello des suggestions de recherche. Sur hello **les Services de domaine Active Directory de Azure** panneau, cliquez sur hello **créer** bouton.

    ![Panneau Domain Services](./media/getting-started/domain-services-blade.png)

5. Hello **activer un domaine Azure AD Services** Assistant est lancé.


## <a name="task-1-configure-basic-settings"></a>Tâche 1 : Configurer les paramètres de base
Bonjour **notions de base** page de l’Assistant de hello, vous pouvez spécifier le nom de domaine DNS hello pour le domaine géré de hello. Vous pouvez également choisir le groupe de ressources hello et emplacement Azure toowhich hello managé domaine doit être déployé.

![Configurer les fonctions de base](./media/getting-started/domain-services-blade-basics.png)

1. Choisissez hello **nom de domaine DNS** pour votre domaine géré.

   * nom de domaine par défaut Hello du répertoire de hello (avec un **. onmicrosoft.com** suffixe) est spécifié par défaut.

   * Vous pouvez également entrer un nom de domaine personnalisé. Dans cet exemple, le nom de domaine personnalisé hello est *contoso100.com*.

     > [!WARNING]
     > préfixe Hello de votre nom de domaine spécifié (par exemple, *contoso100* Bonjour *contoso100.com* nom de domaine) doit contenir au maximum 15 caractères. Vous ne pouvez pas créer de domaine managé avec un préfixe de plus de 15 caractères.
     >
     >

2. Vérifiez que nom de domaine DNS hello choisie pour hello géré domaine n’existe pas déjà dans le réseau virtuel de hello. Plus spécifiquement, vérifiez les poins suivants :

   * Vous disposez déjà d’un domaine avec hello même nom de domaine DNS sur le réseau virtuel de hello.

   * réseau virtuel de Hello où vous prévoyez de domaine géré de hello tooenable a une connexion VPN avec votre réseau local. Dans ce scénario, assurez-vous de vous n’avez pas un domaine avec hello même nom de domaine DNS de votre réseau local.

   * Vous avez un service cloud existant portant le même nom sur le réseau virtuel de hello.

3. Choisissez hello **type de réseau virtuel**. Par défaut, hello **le Gestionnaire de ressources** type de réseau virtuel est sélectionné. Nous vous recommandons d’utiliser ce type de réseau virtuel pour tous les nouveaux domaines managés.

4. Sélectionnez hello Azure **abonnement** dans lequel vous souhaitez que le domaine géré de toocreate hello.

5. Sélectionnez hello **groupe de ressources** domaine géré de hello toowhich doit appartenir. Vous pouvez choisir soit hello **nouvel** ou **utiliser l’existante** groupe de ressources options tooselect hello.

6. Choisissez hello Azure **emplacement** dans quels hello domaine géré doit être créé. Sur hello **réseau** page de l’Assistant de hello, vous voyez des réseaux virtuels uniquement appartenant emplacement toohello que vous avez sélectionné.

7. Lorsque vous avez terminé, cliquez sur **OK** toomove sur toohello **réseau** page d’Assistant de hello.


## <a name="next-step"></a>Étape suivante
[Tâche 2 : Configurer les paramètres réseau](active-directory-ds-getting-started-network.md)
