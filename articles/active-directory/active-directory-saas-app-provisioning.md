---
title: "approvisionnement d’utilisateur application aaaAutomated SaaS dans Azure AD | Documents Microsoft"
description: "Un toohow de présentation que vous pouvez utiliser Azure AD tooautomatically provision, annuler le déploiement et mise à jour des comptes d’utilisateur dans plusieurs applications SaaS de tiers."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>Automatiser la configuration et de mise hors service des applications tooSaaS avec Azure Active Directory
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>Qu’est-ce que l’attribution automatique des utilisateurs dans les applications SaaS ?
Azure Active Directory (Azure AD) vous permet de la création de hello tooautomate, la maintenance et la suppression des identités des utilisateurs dans le cloud ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) des applications telles que l’échange, Salesforce, ServiceNow et bien plus encore.

**Voici quelques exemples de ce que cette fonctionnalité vous permet de toodo :**

* Automatiquement créer de nouveaux comptes Bonjour les applications SaaS à droite pour les nouveaux développeurs lorsqu’ils connectent à votre équipe.
* Désactiver automatiquement des comptes à partir d’applications SaaS lorsque les utilisateurs quittent inévitablement équipe de hello.
* Vous assurer que les identités hello dans vos applications SaaS des toodate en fonction des modifications dans le répertoire de hello.
* Configurer des objets non utilisateur, tels que les groupes, les applications tooSaaS qui les prennent en charge.

**Approvisionnement automatique des utilisateurs comprend également hello suivant de fonctionnalités :**

* Hello identités existantes de capacité toomatch entre Azure AD et les applications SaaS.
* Options de personnalisation toohelp Azure AD ajuste les configurations actuelles de hello d’applications SaaS hello que votre organisation utilise actuellement.
* Alertes par courrier électronique pour les erreurs d’approvisionnement
* Création de rapports et l’activité des journaux toohelp avec l’analyse et le dépannage.

## <a name="why-use-automated-provisioning"></a>Pourquoi utiliser l’approvisionnement automatique ?
Voici les principales raisons pour utiliser cette fonctionnalité :

* les coûts de tooavoid hello, manque d’efficacité et d’erreur humaine associé au processus d’approvisionnement manuelle.
* toosecure votre organisation en supprimant instantanément les identités des utilisateurs à partir de la clé applications SaaS lorsqu’ils quittent l’organisation de hello.
* tooeasily importer un nombre en bloc d’utilisateurs dans une application SaaS.
* tooenjoy hello possibilité pour votre solution d’approvisionnement fonctionnent sur hello mêmes stratégies d’accès application que vous avez définie pour Azure AD Single Sign-On.

## <a name="frequently-asked-questions"></a>Forum Aux Questions (FAQ)
**La fréquence à laquelle les Azure AD n’écrit pas les application SaaS de répertoire modifications toohello ?**

Azure AD vérifie les modifications à toutes les cinq minutes tooten. Si l’application SaaS de hello retourne plusieurs erreurs (par exemple, comme dans les cas de hello d’informations d’identification d’administration non valide), Azure AD peuvent ralentir progressivement ses tooonce tooup de fréquence par jour jusqu'à ce que les erreurs de hello sont résolues.

**Combien de temps faut-il tooprovision mes utilisateurs ?**

Les modifications incrémentielles se produisent presque instantanément, mais si vous essayez de tooprovision la plupart de votre annuaire, puis il varie selon le nombre hello des utilisateurs et des groupes que vous avez. L’opération ne prend que cinq à dix minutes pour les petits annuaires, une trentaine de minutes pour les annuaires de taille moyenne et plusieurs heures pour les annuaires volumineux.

**Comment puis-je suivre la progression de hello de tâche d’approvisionnement actuel hello ?**

Vous pouvez examiner hello rapport Configuration du compte sous la section de rapports hello de votre annuaire. Une autre option est onglet tableau de bord hello application SaaS que vous configurez des toovisit hello et regardez sous la section « Intégration Status » bas hello de page de hello de hello.

**Comment savoir si les utilisateurs ne parviennent pas tooget configuré correctement ?**

Un Assistant de configuration configuration fin hello Hello est une option toosubscribe tooemail les notifications pour l’approvisionnement des échecs. Vous pouvez également vérifier toosee du rapport d’erreurs de configuration hello quels utilisateurs échec toobe configuré et pourquoi.

**Azure AD permettre écrire des modifications du répertoire de toohello arrière application hello SaaS ?**

Pour la plupart des applications SaaS, cette configuration est uniquement les connexions sortantes, ce qui signifie que les utilisateurs sont écrites à partir de l’application de toohello hello active et les modifications à partir de l’application hello ne peut pas être mises à jour toohello active. Pour [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), toutefois, cette configuration est entrée uniquement, ce qui signifie que les utilisateurs sont importés dans le répertoire hello à partir de la journée de travail et de même, les modifications dans le répertoire de hello ne pas obtenir réécrites dans Workday.

**Comment puis-je soumettre l’équipe d’ingénieurs toohello des commentaires ?**

Veuillez nous contacter via hello [forum de commentaires d’Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="how-does-automated-provisioning-work"></a>Comment fonctionne l’approvisionnement automatique ?
Azure AD configure les utilisateurs tooSaaS applications en connectant les points de terminaison tooprovisioning fournies par chaque fournisseur de l’application. Ces points de terminaison autorisent Azure AD tooprogrammatically créer, mettre à jour et supprimer des utilisateurs. Voici une brève vue d’ensemble de hello que Azure AD prend tooautomate l’approvisionnement des étapes différentes.

1. Lorsque vous activez la configuration pour une application pour hello la première fois, hello suit les actions est effectuée :
   * Azure AD va tenter de tous les utilisateurs existants dans l’application SaaS de hello avec leurs identités correspondantes dans le répertoire de hello toomatch. Lorsqu'un utilisateur est mis en correspondance, il n’est *pas* automatiquement activé pour l’authentification unique. Dans l’ordre pour une application de toohello utilisateur toohave d’accès, ils doivent être explicitement affectés toohello application dans Azure AD, soit directement, soit via l’appartenance au groupe.
   * Si vous avez déjà spécifié les utilisateurs qui doivent être assignées toohello application, et que Azure AD échoue toofind des comptes existants pour les utilisateurs, Azure AD configure les nouveaux comptes pour eux dans l’application hello.
2. Une fois la synchronisation initiale hello terminée comme décrit ci-dessus, Azure AD vérifiera toutes les 10 minutes pour hello modifications suivantes :
   * Si les nouveaux utilisateurs ont été affectés toohello application (directement ou via l’appartenance au groupe), puis ils seront mis en service un nouveau compte dans une application SaaS de hello.
   * Si accès un utilisateur l’a été supprimé, puis leur compte dans l’application SaaS de hello sera marqué comme désactivé (les utilisateurs sont jamais complètement supprimés, ce qui vous protège contre la perte de données dans les cas de hello d’une configuration incorrecte).
   * Si un utilisateur a été affecté récemment toohello application et qu’elles avaient déjà un compte Bonjour application SaaS compte sera marqué comme activé, certaines propriétés de l’utilisateur peuvent être mis à jour si elles sont obsolètes toohello comparés active.
   * Si les informations d’un utilisateur (par exemple, le numéro de téléphone, l’emplacement de bureau, etc.) a été modifiées dans le répertoire de hello, ces informations seront également à jour Bonjour application SaaS.

Pour plus d’informations sur la façon dont les attributs sont mappés entre Azure AD et votre application SaaS, consultez l’article hello sur [personnalisation des mappages d’attributs](active-directory-saas-customizing-attribute-mappings.md).

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>Liste des applications prenant en charge l’approvisionnement automatique des utilisateurs
Toutes les applications de « Par défaut » hello dans la galerie d’applications Azure AD hello prend en charge l’approvisionnement automatique des utilisateurs. [liste de Hello des applications proposées peut être affichée ici.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

Pour un application toosupport automatisée configuration de l’utilisateur, il doit tout d’abord fournir hello des points de terminaison nécessaires permettant la création de programmes externes tooautomate hello, la maintenance et la suppression des utilisateurs. Par conséquent, toutes les applications SaaS ne sont pas compatibles avec cette fonctionnalité. Pour les applications qui prennent en charge cela, l’équipe d’ingénieurs hello Azure AD est alors en mesure de toobuild un toothose de connecteur configuration applications et ce travail est hiérarchisé en fonction des besoins des clients actuels et futurs hello.

l’équipe d’ingénierie hello Azure AD toocontact toorequest prise en charge des applications supplémentaires de configuration d’équipe, veuillez envoyer un message via hello [forum de commentaires d’Azure Active Directory](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Personnalisation des mappages d’attributs pour l’approvisionnement des utilisateurs](active-directory-saas-customizing-attribute-mappings.md)
* [Écriture d’expressions pour les mappages d’attributs](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtres d’étendue pour l’approvisionnement des utilisateurs](active-directory-saas-scoping-filters.md)
* [SCIM tooenable la configuration automatique des utilisateurs et groupes à partir d’Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notifications d’approvisionnement de comptes](active-directory-saas-account-provisioning-notifications.md)
* [Liste des didacticiels sur la façon de tooIntegrate applications SaaS](active-directory-saas-tutorial-list.md)

