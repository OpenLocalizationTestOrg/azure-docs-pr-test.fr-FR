---
title: "aaaProblem configuration de configuration d’application de la galerie tooan Azure AD de l’utilisateur | Documents Microsoft"
description: "Comment tootroubleshoot les problèmes courants rencontrés lors de la configuration de configuration d’application tooan déjà énumérée dans la galerie d’applications hello Azure AD de l’utilisateur"
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
ms.openlocfilehash: 19b12be019b05faecef74c6f92a9de03b52a5ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-user-provisioning-tooan-azure-ad-gallery-application"></a>Problème de configuration de configuration d’application de la galerie tooan Azure AD de l’utilisateur

Configuration [configuration automatique d’utilisateurs](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning) pour une application (si pris en charge), requiert que les instructions spécifiques soient application hello de suivi tooprepare pour la configuration automatique. Ensuite, vous pouvez utiliser Bonjour Azure tooconfigure portail Bonjour approvisionnement d’une application de service toosynchronize utilisateur comptes toohello.

Vous devez toujours commencer par recherche hello le programme d’installation de didacticiel toosetting spécifique de la configuration de votre application. Puis suivez les étapes tooconfigure les deux application hello et Azure AD toocreate hello connexion mise en service. Vous trouverez une liste des didacticiels de l’application à [liste de didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

## <a name="how-toosee-if-provisioning-is-working"></a>Fonctionne de toosee en cas de configuration 

Une fois que le service de hello est configuré, la plupart des informations dans l’opération hello du service de hello peuvent être dessinées à partir de deux emplacements :

-   **Journaux d’audit** : hello toutes les opérations de hello effectuées hello mise en service du service d’enregistrement des journaux d’audit de la configuration, y compris l’interrogation d’Azure AD pour attribué aux utilisateurs qui se trouvent dans la portée pour la configuration. Requête hello cible application existence hello de ces utilisateurs, comparer des objets utilisateur hello entre le système de hello. Puis ajouter, mettre à jour ou désactiver le compte d’utilisateur hello dans le système cible de hello en fonction de comparaison de hello. Hello, journaux d’audit de configuration sont accessibles dans hello portail Azure, Bonjour **Azure Active Directory &gt; applications d’entreprise &gt; \[nom de l’Application\] &gt; lesjournauxd’Audit**onglet. Hello du filtre de session hello **l’approvisionnement de comptes** catégorie tooonly voir hello événements pour cette application de configuration.

-   **Configuration d’état –** un résumé de l’approvisionnement dernière hello série pour une application donnée peut être observée dans hello **Azure Active Directory &gt; applications d’entreprise &gt; \[nom de l’Application\] &gt; Approvisionnement** section, bas hello écran hello sous les paramètres de service hello. Cette section résume combien les utilisateurs (ou des groupes) sont en cours de synchronisation entre hello deux systèmes, et s’il existe des erreurs. Détails de l’erreur se trouver dans les journaux d’audit de hello. Notez que hello l’état de configuration ne pas peuplées jusqu'à ce qu’une synchronisation initiale complète a été effectuée entre Azure AD et l’application hello.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Zones à problème général avec l’allocation tooconsider

Voici une liste de hello zones à problème général que vous pouvez Explorer si vous avez une idée de l’endroit où toostart.

* [Service de configuration n’apparaît pas toostart](#provisioning-service-does-not-appear-to-start)
* [Impossible d’enregistrer la configuration en raison d’informations d’identification tooapp ne fonctionne ne pas](#can’t-save-configuration-due-to-app-credentials-not-working)
* [Les journaux d’audit indiquent que les utilisateurs sont ignorés et non approvisionnés, alors qu’ils sont affectés](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Service de configuration n’apparaît pas toostart

Si vous définissez hello **état d’approvisionnement** toobe **sur** Bonjour **Azure Active Directory &gt; applications d’entreprise &gt; \[nomdel’Application\] &gt;Provisioning** section Hello portail Azure. Cependant aucune autre information d’état n’apparaît sur cette page après de nouveaux chargements. Il est probable que le service de hello est en cours d’exécution mais encore synchronisation initiale n’est pas terminée. Vérifiez hello **journaux d’Audit** décrite ci-dessus toodetermine quel service de hello opérations s’effectue, et s’il existe des erreurs.

>[!NOTE]
>Une synchronisation initiale peut prendre entre 20 minutes tooseveral heures, selon la taille de hello de Windows Azure AD pour hello et hello des utilisateurs dans la portée pour la configuration. Les synchronisations suivantes après la synchronisation initiale hello être plus rapide, hello configuration service stocke les filigranes qui représentent l’état hello des deux systèmes après la synchronisation initiale hello, améliorer les performances des synchronisations suivantes.
>
>

## <a name="cant-save-configuration-due-tooapp-credentials-not-working"></a>Impossible d’enregistrer la configuration en raison d’informations d’identification tooapp ne fonctionne ne pas

Dans l’ordre d’approvisionnement toowork, Azure AD nécessite des informations d’identification valides qui permettent de gestion des utilisateurs tooa tooconnect API fournie par cette application. Si ces informations d’identification ne fonctionnent pas ou si vous ne connaissez pas wat qu’ils sont, passez en revue le didacticiel hello pour configurer cette application, décrite précédemment.

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Les journaux d’audit indiquent que les utilisateurs sont ignorés et non approvisionnés, bien qu’ils soient affectés

Lorsqu’un utilisateur s’affiche comme « ignorée » dans les journaux d’audit de hello, il est hello tooread très important détails en raison de hello hello journal message toodetermine étendus. Voici les raisons les plus courantes et les solutions correspondantes :

-   **Un filtre d’étendue a été configuré** **qui est filtrant utilisateur de hello basé sur une valeur d’attribut**. Pour plus d’informations sur les filtres d’étendue, consultez <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **utilisateur de Hello » n’est effectivement en droit ».** Si vous voyez ce message d’erreur spécifique, il est, car il existe un problème avec l’enregistrement d’affectation hello utilisateur stocké dans Azure AD. toofix ce problème, supprimer l’affectation hello utilisateur (ou groupe) à partir de l’application hello et réaffectez à nouveau. Pour plus d’informations sur l’affectation, consultez <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Un attribut requis manque ou n’est pas indiqué pour un utilisateur.** Un tooconsider plus important lors de la configuration de l’approvisionnement d’être tooreview et configurer les mappages d’attributs hello et flux de travail qui définissent le flux de propriétés utilisateur (ou groupe) à partir de l’application de toohello Azure AD. Cela inclut le paramètre hello « correspondance property » être toouniquely utilisé identifier et correspondent aux utilisateurs/groupes entre les systèmes de hello deux. Pour plus d’informations sur ce processus important, consultez la page <https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings>.

   * **Mappages pour les groupes d’attributs :** Provisioning Hello détails nom et de groupe, dans les membres de toohello Ajout du groupe si pris en charge pour certaines applications. Vous pouvez activer ou désactiver cette fonctionnalité en activant ou désactivant hello **mappage** pour les objets de groupe affichés dans hello **Provisioning** onglet. Si la configuration des groupes est activée, veillez à tooreview hello attribut mappages tooensure un champ approprié est utilisé pour hello « correspondant ID ». Il peut s’agir hello affichage nom alias de messagerie électronique), comme groupe de hello et ses membres ne pas être configurés si hello correspondance de propriété est vide ou non remplie pour un groupe dans Azure AD.

#<a name="next-steps"></a>Étapes suivantes
[Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications avec Azure Active Directory](active-directory-saas-app-provisioning.md)
