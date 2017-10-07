---
title: "aaaProblem à l’aide d’accès des applications en libre-service | Documents Microsoft"
description: "Résoudre les problèmes connexes tooself service application l’accès"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a>Problème lié à l’accès aux applications en libre-service

Accès à l’application automatique est un tooself aux utilisateurs de tooallow excellent moyen-découvrir les applications, vous pouvez également autoriser hello entreprise groupe tooapprove toothose applications. Vous pouvez autoriser les informations d’identification de groupe toomanage hello hello entreprise affecté les utilisateurs de toothose de droite de l’authentification unique de mot de passe sur les Applications à partir de leurs panneaux d’accès.

Avant que vos utilisateurs découvrir automatiquement des applications à partir de leur volet d’accès, vous devez tooenable **accès à l’application automatique** tooany les applications que vous souhaitez tooallow utilisateurs tooself-découvrir et de demander l’accès à.

## <a name="general-issues-toocheck-first"></a>Général émet toocheck tout d’abord

-   Vérifiez que l’accès à l’application en libre-service est configuré correctement. Voir « Comment accéder à application en libre service tooconfigure ».

-   Vérifiez que hello utilisateur ou le groupe a été activé l’accès des applications en libre-service toorequest.

-   Vérifiez que hello utilisateur visite sur place de correct hello pour l’accès des applications en libre-service. les utilisateurs peuvent naviguer tootheir [volet d’accès Application](https://myapps.microsoft.com/) et cliquez sur hello **+ ajouter** bouton toofind hello applications toowhich que vous avez activé les accès en libre-service.

-   Si l’accès à l’application automatique a été récemment configuré, réessayez toosign et l’extraction dans le volet d’accès de l’utilisateur hello après quelques minutes toosee si les modifications d’accès en libre-service hello apparaissent.

## <a name="how-tooconfigure-self-service-application-access"></a>Comment accéder aux applications en libre-service tooconfigure

tooenable libre-service accès tooan une application, suivez les étapes hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello liste de hello toofrom tooenable accès en libre-service.

7.  Une fois le charge de l’application hello, cliquez sur **libre-service** à partir du menu de navigation de gauche de l’application hello.

8.  tooenable accès des applications en libre-service pour cette application, activez hello **autoriser l’application de toothis accès toorequest ?** basculer trop**Oui.**

9.  Ensuite, tooselect hello groupe toowhich les utilisateurs qui demandent l’accès toothis application doit être ajoutée, cliquez sur le libellé de toohello suivant hello sélecteur **toowhich groupe doivent être assignées utilisateurs ajoutés ?** et sélectionnez un groupe.

10. **Facultatif :** si vous souhaitez toorequire une approbation de l’entreprise avant que les utilisateurs sont autorisés à accéder, affectez à hello **exiger l’approbation avant d’accorder l’accès toothis application ?** basculer trop**Oui**.

11. **Facultatif : pour les applications à l’aide d’un mot de passe d’authentification unique sur uniquement,** si vous le souhaitez tooallow ces business approbateurs toospecify hello des mots de passe sont envoyés application toothis pour les utilisateurs approuvés, définissez hello **autoriser approbateurs tooset mots de passe de l’utilisateur pour cette application ?**  basculer trop**Oui**.

12. **Facultatif :** toospecify hello entreprise approbateurs sont autorisés à application de toothis tooapprove access, cliquez sur le libellé de toohello suivant hello sélecteur **qui est autorisé d’application de toothis accès tooapprove ?** tooselect des approbateurs d’entreprise too10.

 >[!NOTE]
 > Les groupes ne sont pas pris en charge.
 >
 >

13. **Facultatif :** **pour les applications qui présentent les rôles**, si vous voulez que le rôle de tooa tooassign libre-service des utilisateurs approuvés, cliquez sur toohello suivant du sélecteur hello **toowhich rôle doivent être assigné aux utilisateurs dans ce application ?**  tooselect hello rôle toowhich ces utilisateurs doivent être affectés.

14. Cliquez sur hello **enregistrer** bouton haut hello hello panneau toofinish.

Après avoir terminé la configuration de l’application en libre service, les utilisateurs peuvent naviguer tootheir [volet d’accès Application](https://myapps.microsoft.com/) et cliquez sur hello **+ ajouter** bouton toofind hello applications toowhich que vous avez activé Accès en libre-service. Les approbateurs d’entreprise reçoivent également une notification dans leur [volet d’accès aux applications](https://myapps.microsoft.com/). Vous pouvez activer un courrier électronique pour les informer lorsqu’un utilisateur a demandé l’application accès tooan nécessitant leur approbation. 

Ces approbations prend en charge les workflows approbation unique uniquement, ce qui signifie que si vous spécifiez plusieurs approbateurs, tout seul approbateur peut approuver accès toohello application.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Si ces étapes de dépannage ne résolvent pas le problème de hello 

Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :

-   ID d’erreur de corrélation

-   UPN (adresse e-mail de l’utilisateur)

-   ID de locataire

-   Type de navigateur

-   Fuseau horaire et heure/période à laquelle l’erreur se produit

-   Traces Fiddler

## <a name="next-steps"></a>Étapes suivantes
[Configuration d’Azure Active Directory pour la gestion de groupe en libre-service](active-directory-accessmanagement-self-service-group-management.md)
