---
title: "aaaUsing Bureau à distance avec des rôles Azure | Documents Microsoft"
description: "Utilisation du Bureau à distance avec des rôles Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a>Utilisation du Bureau à distance avec des rôles Azure
À l’aide de hello Azure SDK et des Services Bureau à distance, vous pouvez accéder à des rôles Azure et les machines virtuelles qui sont hébergées par Azure. Dans Visual Studio, vous pouvez configurer les Services Bureau à distance à partir d’un projet de service cloud Azure. tooenable des Services Bureau à distance, vous devez créer un projet de travail qui contient un ou plusieurs rôles et publiez-le tooAzure.

> [!IMPORTANT]
> L’accès aux rôles Azure est réservé au dépannage et au développement. Hello d’objet de chaque machine virtuelle est toorun un rôle spécifique dans votre application Windows Azure, toorun pas les autres applications clientes. Si vous souhaitez toouse Azure toohost une machine virtuelle que vous pouvez utiliser d’autres fins, reportez-vous à l’accès à des Machines virtuelles Azure à partir de l’Explorateur de serveurs.
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a>tooenable et utilisez Bureau à distance pour un rôle Azure
1. Dans l’Explorateur de solutions, ouvrez le menu contextuel de hello pour votre projet de service cloud, puis choisissez **publier**.
   
    Hello **publier l’Application Azure** Assistant s’affiche.
   
    ![Commande Publier pour un projet de service cloud](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. Bas hello **paramètres de publication Microsoft Azure** page d’Assistant hello, sélectionnez hello **activer le Bureau à distance** pour tous les rôles case à cocher. 
   
    Hello **Configuration Bureau à distance** boîte de dialogue s’affiche.
3. En bas de hello Hello **Configuration Bureau à distance** boîte de dialogue, choisissez hello **plus d’Options** bouton. 
   
    Cela affiche une liste déroulante qui vous permet de créer ou de sélectionner un certificat afin de chiffrer les informations d'identification lors de la connexion Bureau à distance.
4. Dans la liste déroulante de hello, choisissez  **&lt;créer >**, ou choisissez un certificat existant à partir de la liste de hello. 
   
    Si vous choisissez un certificat existant, ignorez hello comme suit.
   
   > [!NOTE]
   > les certificats de Hello dont vous avez besoin pour une connexion Bureau à distance sont différents de certificats hello que vous utilisez pour d’autres opérations Windows Azure. certificat d’accès à distance Hello doit avoir une clé privée.
   > 
   > 
   
    Hello **Create Certificate** boîte de dialogue s’affiche.
   
   1. Fournissez un nom convivial pour le nouveau certificat de hello, puis choisissez hello **OK** bouton. Hello nouveau certificat apparaît dans la zone de liste déroulante hello.
   2. Bonjour **Configuration Bureau à distance** boîte de dialogue zone, fournissez un nom d’utilisateur et un mot de passe.
      
       Vous ne pouvez pas utiliser un compte existant. Ne spécifiez pas administrateur comme nom d’utilisateur de hello pour hello nouveau compte.
      
      > [!NOTE]
      > Si le mot de passe hello ne répond pas aux exigences de complexité hello, une icône rouge apparaît la zone de texte de mot de passe toohello suivante. mot de passe Hello doit inclure des lettres majuscules, lettres minuscules et nombres ou des symboles.
      > 
      > 
   3. Choisissez une date sur le compte hello expirera et après les connexions Bureau à distance seront bloquées.
   4. Une fois que vous avez fourni toutes les hello les informations requises, choisissez hello **OK** bouton.
      
       Plusieurs paramètres qui activent les Services d’accès distant sont ajoutés les fichiers .cscfg et .csdef toohello.
5. Bonjour **paramètres de publication Microsoft Azure** Assistant, choisissez hello **OK** bouton quand vous êtes prêt à toopublish votre service cloud.
   
    Si vous n’êtes pas prêt toopublish, choisissez hello **Annuler** bouton. paramètres de configuration Hello sont enregistrés, et vous pouvez publier votre service cloud ultérieurement.

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a>Se connecter tooan rôle Azure à l’aide du Bureau à distance
Après avoir publié votre service cloud sur Azure, vous pouvez utiliser l’Explorateur de serveurs toolog dans les machines virtuelles hello hébergée par Azure. 

1. Dans l’Explorateur de serveurs, développez hello **Azure** nœud, puis développez le nœud hello pour un service cloud et un de ses rôles de toodisplay une liste d’instances.
2. Ouvrez le menu contextuel de hello pour un nœud d’instance, puis choisissez **connexion de bureau à distance à l’aide de**.
   
    ![Connexion Bureau à distance](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. Entrez le nom d’utilisateur hello et un mot de passe que vous avez créé précédemment. Vous êtes maintenant connecté à votre session à distance.

