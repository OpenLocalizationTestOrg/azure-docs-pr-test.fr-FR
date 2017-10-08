---
title: "attribution d’applications en libre-service aaaHow tooconfigure | Documents Microsoft"
description: "Activer les applications en libre-service accès tooallow utilisateurs toofind leurs propres applications."
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
ms.openlocfilehash: d25a0146c4c8cebf9c2ae8c516f094a8eccb4570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-self-service-application-assignment"></a>Comment l’attribution tooconfigure applications en libre-service

Avant que vos utilisateurs découvrir automatiquement des applications à partir de leur volet d’accès, vous devez tooenable **accès à l’application automatique** tooany les applications que vous souhaitez tooallow utilisateurs tooself-découvrir et de demander l’accès à.

Cette fonctionnalité est un excellent moyen de vous toosave temps et l’argent en tant qu’un groupe informatique et il est vivement recommandée dans le cadre d’un déploiement d’applications modernes avec Azure Active Directory.

À l’aide de cette fonctionnalité, vous pouvez :

-   Permettre aux utilisateurs de découvrir automatiquement les applications à partir de hello [volet d’accès Application](https://myapps.microsoft.com/) sans déranger hello informatique de groupe.

-   Ajoutez ces groupe préconfiguré tooa des utilisateurs afin de pouvoir voir qui a demandé l’accès, de supprimer l’accès et gérer des rôles hello toothem.

-   Si vous le souhaitez autorisant un approbateur d’entreprise tooapprove les demandes d’accès application hello groupe informatique n’a pas besoin.

-   Configurez éventuellement des personnes too10 peuvent autoriser l’accès toothis application.

-   Si vous le souhaitez autoriser un approbateur d’entreprise des mots de passe tooset hello ces utilisateurs peuvent utiliser toosign dans l’application toohello, directement à partir de l’approbateur d’entreprise hello [volet d’accès Application](https://myapps.microsoft.com/).

-   Éventuellement automatiquement attribuer le rôle d’application tooan libre-service des utilisateurs attribués directement.

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a>Activer les applications en libre-service accès tooallow utilisateurs toofind leurs propres applications.

Accès à l’application automatique est un tooself aux utilisateurs de tooallow excellent moyen-découvrir les applications, vous pouvez également autoriser hello entreprise groupe tooapprove toothose applications. Vous pouvez autoriser les informations d’identification de groupe toomanage hello hello entreprise affecté les utilisateurs de toothose de droite de l’authentification unique de mot de passe sur les Applications à partir de leurs panneaux d’accès.

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
   >Les groupes ne sont pas pris en charge.
   >
   >

13. **Facultatif :** **pour les applications qui présentent les rôles**, si vous voulez que le rôle de tooa tooassign libre-service des utilisateurs approuvés, cliquez sur toohello suivant du sélecteur hello **toowhich rôle doivent être assigné aux utilisateurs dans ce application ?**  tooselect hello rôle toowhich ces utilisateurs doivent être affectés.

14. Cliquez sur hello **enregistrer** bouton haut hello hello panneau toofinish.

Après avoir terminé la configuration de l’application en libre service, les utilisateurs peuvent naviguer tootheir [volet d’accès Application](https://myapps.microsoft.com/) et cliquez sur hello **+ ajouter** bouton toofind hello applications toowhich que vous avez activé Accès en libre-service. Les approbateurs d’entreprise reçoivent également une notification dans leur [volet d’accès aux applications](https://myapps.microsoft.com/). Vous pouvez activer un courrier électronique pour les informer lorsqu’un utilisateur a demandé l’application accès tooan nécessitant leur approbation. 

Ces approbations prend en charge les flux de travail approbation unique uniquement, ce qui signifie que si vous spécifiez plusieurs approbateurs, un approbateur unique peut application de toohello accès approbateur.

## <a name="next-steps"></a>Étapes suivantes
[Configuration d’Azure Active Directory pour la gestion de groupe en libre-service](active-directory-accessmanagement-self-service-group-management.md)
