---
title: "Problème rencontré lors de l’utilisation de l’accès aux applications en libre-service | Microsoft Docs"
description: "Résoudre les problèmes liés à l’accès aux applications en libre-service"
services: active-directory
documentationcenter: 
author: ajamess
manager: mtillman
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: dcd3ea1269ff40e4777cc9b0ca46f0b64560f923
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2017
---
# <a name="problem-using-self-service-application-access"></a>Problème lié à l’accès aux applications en libre-service

L’accès aux applications en libre-service est un excellent moyen pour permettre aux utilisateurs de découvrir eux-mêmes des applications, et éventuellement de permettre au groupe d’entreprise d’approuver l’accès à ces applications. Vous pouvez autoriser le groupe d’entreprise à gérer les informations d’identification affectées à ces utilisateurs dans le cadre d’une authentification unique par mot de passe, directement depuis leurs volets d’accès.

Pour permettre à vos utilisateurs de découvrir eux-mêmes des applications depuis leur panneau d’accès, vous devez activer l’option **Accès en libre-service à l’application** pour toutes les applications pour lesquelles vous souhaitez autoriser les utilisateurs à les découvrir eux-mêmes et en demander l’accès.

## <a name="general-issues-to-check-first"></a>Problèmes d’ordre général à vérifier en premier

-   Vérifiez que l’accès à l’application en libre-service est configuré correctement. Consultez Configuration de l’accès aux applications en libre-service.

-   Vérifiez que l’utilisateur ou le groupe a été activé pour demander l’accès aux applications en libre-service.

-   Vérifiez que l’utilisateur visite l’emplacement adéquat pour demander l’accès aux applications en libre-service. Les utilisateurs peuvent accéder à leur [volet d’accès aux applications](https://myapps.microsoft.com/) et cliquer sur le bouton **+Ajouter** pour choisir les applications pour lesquelles vous avez activé l’accès en libre-service.

-   Si l’accès aux applications en libre-service a été récemment configuré, essayez de vous reconnecter au volet d’accès de l’utilisateur au bout de quelques minutes pour voir si les modifications de l’accès en libre-service sont apparues.

## <a name="how-to-configure-self-service-application-access"></a>Configuration de l’accès aux applications en libre-service

Pour activer l’accès en libre-service à une application, procédez comme suit :

1.  Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.

2.  Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.

3.  Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.

4.  Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.

5.  Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.

  * Si l’application que vous recherchez n’apparaît pas, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications**.

6.  Sélectionnez l’application pour laquelle vous souhaitez activer l’accès en libre-service à partir de la liste.

7.  Une fois l’application chargée, cliquez sur **Libre-service** dans le menu de navigation gauche de l’application.

8.  Pour activer l’accès en libre-service à cette application, définissez l’option **Autoriser les utilisateurs à demander l’accès à cette application ?** sur **Oui.**

9.  Ensuite, pour sélectionner le groupe auquel les utilisateurs qui demandent l’accès à cette application doivent être ajoutés, cliquez sur le sélecteur en regard de l’étiquette **À quel groupe les utilisateurs attribués doivent-ils être ajoutés ?** et sélectionnez un groupe.

10. **Facultatif :** si vous souhaitez exiger une approbation d’entreprise avant d’accorder l’accès aux utilisateurs, définissez l’option **Demander une approbation avant d’accorder l’accès à cette application ?** sur **Oui**.

11. **Facultatif : pour les applications qui nécessitent une authentification unique par mot de passe uniquement,** si vous souhaitez autoriser ces approbateurs d’entreprise à spécifier les mots de passe envoyés à cette application pour les utilisateurs approuvés, définissez l’option **Autoriser les approbateurs à définir les mots de passe de l’utilisateur pour cette application ?** sur **Oui**.

12. **Facultatif :** pour spécifier les approbateurs d’entreprise autorisés à approuver l’accès à cette application, cliquez sur le sélecteur en regard de l’étiquette **Qui est autorisé à approuver l’accès à cette application ?** pour sélectionner jusqu’à 10 approbateurs d’entreprise.

 >[!NOTE]
 > Les groupes ne sont pas pris en charge.
 >
 >

13. **Facultatif :****pour les applications qui exposent des rôles**, si vous souhaitez attribuer un rôle à des utilisateurs approuvés en libre-service, cliquez sur le sélecteur en regard de l’option  **À quel rôle attribuer des utilisateurs dans cette application ?** pour sélectionner le rôle à affecter à ces utilisateurs.

14. Cliquez sur le bouton **Enregistrer** en haut du volet pour terminer.

Lorsque vous avez terminé la configuration d’applications en libre-service, les utilisateurs peuvent accéder à leur [volet d’accès aux applications](https://myapps.microsoft.com/) et cliquer sur le bouton **+Ajouter** pour choisir les applications pour lesquelles vous avez activé l’accès en libre-service. Les approbateurs d’entreprise reçoivent également une notification dans leur [volet d’accès aux applications](https://myapps.microsoft.com/). Vous pouvez leur envoyer une notification par e-mail les avertissant qu’un utilisateur a demandé l’accès à une application nécessitant leur approbation. 

Ces approbations prennent en charge les flux de travail avec approbation unique uniquement, ce qui signifie que si vous spécifiez plusieurs approbateurs, chaque approbateur peut approuver l’accès à l’application.

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a>Si ces étapes de dépannage ne résolvent pas le problème 

Ouvrez un ticket de support en fournissant les informations suivantes, dans la mesure du possible :

-   ID d’erreur de corrélation

-   UPN (adresse e-mail de l’utilisateur)

-   ID de locataire

-   Type de navigateur

-   Fuseau horaire et heure/période à laquelle l’erreur se produit

-   Traces Fiddler

## <a name="next-steps"></a>Étapes suivantes
[Configuration d’Azure Active Directory pour la gestion de groupe en libre-service](active-directory-accessmanagement-self-service-group-management.md)
