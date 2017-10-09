---
title: "aaaNo utilisateurs sont en cours d’application de la galerie tooan mis en service Azure AD | Documents Microsoft"
description: "Comment tootroubleshoot les problèmes courants rencontrés lorsque vous ne voyez pas les utilisateurs figurant dans une une annonce Azure Application de la galerie que vous avez configuré pour l’approvisionnement des utilisateurs auprès d’Azure AD"
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
ms.date: 05/04/2017
ms.author: asteen
ms.openlocfilehash: 4d9693a202ed657e1de5571b50e5d499bef1bb3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="no-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Aucun utilisateur n’est en cours d’application de la galerie tooan mis en service Azure AD

Mise en service une fois automatique a été configuré pour une application (notamment pour vérifier que les informations d’identification d’application hello fourni tooAzure AD tooconnect toohello application sont valides). Les utilisateurs ou des groupes sont approvisionnés toohello application et est déterminée par hello suivant choses :

-   Utilisateurs et groupes ayant été **affecté** toohello application. Pour plus d’informations sur l’attribution, consultez [affecter une application d’entreprise tooan utilisateur ou un groupe dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

-   Ou non **mappages d’attributs** toosync activé et configuré les attributs valide à partir de l’application de toohello Azure AD. Pour plus de détails sur les mappages d’attributs, consultez [Personnalisation des mappages d’attributs d’approvisionnement d’utilisateurs pour les applications SaaS dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

-   Un **filtre d’étendue** permet-il de filtrer les utilisateurs en fonction de valeurs d’attribut spécifiques. Pour plus d’informations sur les filtres d’étendue, consultez [Approvisionnement d’applications basé sur les attributs avec filtres d’étendue](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

Lorsque vous observez que les utilisateurs ne sont pas configurés, consultez les journaux d’Audit de hello dans Azure AD et recherchez les entrées de journal pour un utilisateur spécifique.

Hello, journaux d’audit de configuration sont accessibles dans hello portail Azure, Bonjour **Azure Active Directory &gt; applications d’entreprise &gt; \[nom de l’Application\] &gt; lesjournauxd’Audit**onglet. Hello du filtre de session hello **l’approvisionnement de comptes** catégorie tooonly voir hello événements pour cette application de configuration. Vous pouvez rechercher des utilisateurs en fonction de hello « correspondance ID » qui a été configuré pour eux dans les mappages d’attributs hello. Par exemple, si vous avez configuré hello « nom d’utilisateur principal » ou « adresse de messagerie » comme hello attribut côté hello Azure AD correspondant, et ne pas en cours de configuration de l’utilisateur hello a la valeur «audrey@contoso.com». Puis recherchez les journaux d’audit de hello pour «audrey@contoso.com» et révision puis entrées retournées.

Hello d’audit de configuration journaux enregistrent que toutes hello opérations effectuées par le service d’approvisionnement hello, y compris l’interrogation d’Azure AD pour les utilisateurs assignés sont dans la portée de l’approvisionnement, interrogation application cible de hello existence hello de ces utilisateurs, comparaison hello objets utilisateur entre le système de hello. Puis ajouter, mettre à jour ou désactiver le compte d’utilisateur hello dans le système cible de hello en fonction de comparaison de hello.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Zones à problème général avec l’allocation tooconsider

Voici une liste de hello zones à problème général que vous pouvez Explorer si vous avez une idée de l’endroit où toostart.

* [Service de configuration n’apparaît pas toostart](#provisioning-service-does-not-appear-to-start)
* [Les journaux d’audit indiquent que les utilisateurs sont ignorés et non approvisionnés, bien qu’ils soient affectés](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Service de configuration n’apparaît pas toostart

Si vous définissez hello **état d’approvisionnement** toobe **sur** Bonjour **Azure Active Directory &gt; applications d’entreprise &gt; \[nomdel’Application\] &gt;Provisioning** section Hello portail Azure. Toutefois aucun autre état détails sont affichés sur cette page après recharge suivantes, il est probable que le service de hello est en cours d’exécution mais encore synchronisation initiale n’est pas terminée. Vérifiez hello **journaux d’Audit** décrite ci-dessus toodetermine quel service de hello opérations s’effectue, et s’il existe des erreurs.

>[!NOTE]
>Une synchronisation initiale peut prendre entre 20 minutes tooseveral heures, selon la taille de hello de Windows Azure AD pour hello et hello des utilisateurs dans la portée pour la configuration. Les synchronisations suivantes après la synchronisation initiale hello sont plus rapides, en tant que hello configuration service stocke les filigranes qui représentent l’état hello des deux systèmes après la synchronisation initiale hello. Cela améliore les performances des synchronisations suivantes.
>
>

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Les journaux d’audit indiquent que les utilisateurs sont ignorés et non approvisionnés, bien qu’ils soient affectés

Lorsqu’un utilisateur s’affiche comme « ignorée » dans les journaux d’audit de hello, il est hello tooread très important détails en raison de hello hello journal message toodetermine étendus. Voici les raisons les plus courantes et les solutions correspondantes :

-   **Un filtre d’étendue a été configuré** **qui est filtrant utilisateur de hello basé sur une valeur d’attribut**. Pour plus d’informations sur les filtres d’étendue, consultez <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **utilisateur de Hello » n’est effectivement en droit ».** Si vous voyez ce message d’erreur spécifique, il est, car il existe un problème avec l’enregistrement d’affectation hello utilisateur stocké dans Azure AD. toofix ce problème, supprimer l’affectation hello utilisateur (ou groupe) à partir de l’application hello et réaffectez à nouveau. Pour plus d’informations sur l’affectation, consultez <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Un attribut requis manque ou n’est pas indiqué pour un utilisateur.** Un tooconsider plus important lors de la configuration de l’approvisionnement d’être tooreview et configurer les mappages d’attributs hello et flux de travail qui définissent le flux de propriétés utilisateur (ou groupe) à partir de l’application de toohello Azure AD. Cela inclut le paramètre hello « correspondance property » être toouniquely utilisé identifier et correspondent aux utilisateurs/groupes entre les systèmes de hello deux. Pour plus de détails sur ce processus important, consultez [Personnalisation des mappages d’attributs d’approvisionnement d’utilisateurs pour les applications SaaS dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

  * **Mappages pour les groupes d’attributs :** Provisioning Hello détails nom et de groupe, dans les membres de toohello Ajout du groupe si pris en charge pour certaines applications. Vous pouvez activer ou désactiver cette fonctionnalité en activant ou désactivant hello **mappage** pour les objets de groupe affichés dans hello **Provisioning** onglet. Si la configuration des groupes est activée, veillez à tooreview hello attribut mappages tooensure un champ approprié est utilisé pour hello « correspondant ID ». Il peut s’agir hello affichage nom alias de messagerie électronique), comme groupe de hello et ses membres ne pas être configurés si hello correspondance de propriété est vide ou non remplie pour un groupe dans Azure AD.

## <a name="next-steps"></a>Étapes suivantes
[Azure AD Connect Sync : présentation de l’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning.md)

