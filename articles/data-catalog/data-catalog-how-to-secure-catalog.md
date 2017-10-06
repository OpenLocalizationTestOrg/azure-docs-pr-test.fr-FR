---
title: "aaaHow toosecure accès tooAzure Data Catalog | Documents Microsoft"
description: "Cet article explique comment toosecure data catalog et ses ressources de données."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Comment toosecure accéder aux ressources de catalogue et les données toodata
> [!IMPORTANT]
> Cette fonctionnalité est disponible uniquement dans l’édition standard de hello d’Azure Data Catalog.

Azure Data Catalog vous permet de toospecify qui peut accéder au catalogue de données hello et les opérations (inscrire, annoter, prendre possession) qu’ils peuvent effectuer sur les métadonnées de catalogue de hello. 

## <a name="catalog-users-and-permissions"></a>Utilisateurs du catalogue et autorisations
toogive un utilisateur ou un Bonjour groupe accéder au catalogue de données tooa et définir des autorisations :

1. Sur hello [page d’accueil de votre catalogue de données](http://www.azuredatacatalog.com), cliquez sur **paramètres** sur la barre d’outils hello.

    ![catalogue de données - paramètres](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. Dans la page Paramètres de hello, développez hello **utilisateurs catalogue** section.
    ![Utilisateurs du catalogue - Ajouter](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. Cliquez sur **Add**.
4. Entrez hello complet **nom d’utilisateur** ou le nom de hello **groupe de sécurité** Bonjour Azure Active Directory (AAD) associés au catalogue de hello. Utilisez une virgule (« , ») comme séparateur si vous ajoutez plusieurs utilisateurs ou groupes.
    ![Utilisateurs du catalogue - utilisateurs ou groupes](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. Appuyez sur **entrée** ou **onglet** en dehors de la zone de texte hello. 
6.  Vérifiez que toutes les autorisations (**annoter**, **inscrire**, et **Take Ownership**) sont affectés toothese utilisateurs ou des groupes par défaut. Autrement dit, hello utilisateur ou un groupe peut [inscrire les ressources de données]( data-catalog-how-to-register.md), [annoter les ressources de données]( data-catalog-how-to-annotate.md), et [s’approprier les ressources de données]( data-catalog-how-to-manage.md). 
    ![Utilisateurs du catalogue - autorisations par défaut](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  toogive un utilisateur ou groupe uniquement hello lire accès toohello catalogue, désactivez hello **annoter** option pour cet utilisateur ou groupe. Lorsque vous procédez ainsi, hello utilisateur ou un groupe ne peut pas annoter les ressources de données dans le catalogue de hello, mais ils peuvent les afficher. 
8.  toodeny un utilisateur ou un groupe de l’inscription de vos données, désactivez hello **inscrire** option pour cet utilisateur ou groupe.
9.  toodeny un utilisateur de prendre possession d’une ressource de données, désactivez hello **prendre possession** option pour cet utilisateur ou groupe. 
10. toodelete un utilisateur/groupe d’utilisateurs du catalogue, cliquez sur **x** pour un utilisateur/groupe hello bas hello de liste de hello. 
    ![Utilisateurs du catalogue - supprimer un utilisateur](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > Nous vous recommandons de vous ajoutez directement des utilisateurs de toocatalog de groupes de sécurité plutôt que d’ajouter des utilisateurs et affectez des autorisations. Ensuite, ajoutez les utilisateurs toohello des groupes de sécurité qui correspondent à leurs rôles et leur catalogue toohello d’accès requis.

## <a name="special-considerations"></a>Considérations spéciales

- toosecurity groupes affectés aux autorisations de Hello sont additives. Imaginez par exemple qu’un utilisateur appartient à deux groupes. L’un des groupes a des autorisations d’annotation, tandis que l’autre n’en a pas. Dans ce cas de figure, l’utilisateur a des autorisations d’annotation. 
- Hello autorisations affectées explicitement hello de remplacement tooa utilisateur les autorisations affectées toogroups toowhich hello utilisateur appartient. Dans l’exemple précédent de hello, par exemple, vous avez ajouté explicitement les utilisateurs de toocatalog hello et n’affectez pas d’annoter les autorisations. utilisateur de Hello ne peut pas annoter les ressources de données même si l’utilisateur de hello est un membre d’un groupe qui possède annoter les autorisations.

## <a name="next-steps"></a>Étapes suivantes
- [Prise en main d’Azure Data Catalog](data-catalog-get-started.md)

