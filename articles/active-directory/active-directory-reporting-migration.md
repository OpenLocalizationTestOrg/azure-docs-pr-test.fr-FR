---
title: "rapports d’activité d’aaaFind Bonjour portail Azure | Documents Microsoft"
description: "Découvrez comment les rapports toofind activité d’Azure Active Directory Bonjour portail Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>Rechercher les rapports d’activité Bonjour portail Azure

Si vous déplacez de hello toohello de portail classique Azure portail Azure, vous obtenez un nouveau look journaux d’activité Azure Active Directory (Azure AD). Dans un récent [billet de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), nous expliquons comment vous pouvez voir des journaux d’activité dans le contexte hello de ressource hello vous travaillez dans hello portail Azure. Dans cet article, nous décrivons comment toofind les rapports que vous avez utilisé dans hello portail classique Azure Bonjour portail Azure.

## <a name="whats-new"></a>Nouveautés

Rapports Bonjour portail Azure classic sont divisées en catégories :

1.  Rapports de sécurité
2.  Rapports d’activité
3.  Rapports d’application intégrée

### <a name="activity-and-integrated-app-reports"></a>Rapports d’activité et d’application intégrée

Pour un rapport basé sur le contexte Bonjour portail Azure, les rapports existants sont fusionnés dans une vue unique. Une seule API sous-jacente présente hello données toohello.

toosee cette vue, sur hello **Azure Active Directory** panneau, sous **activité**, sélectionnez **journaux d’Audit**.

![Journaux d’audit](./media/active-directory-reporting-migration/482.png "Journaux d’Audit")

Hello suivant des rapports est consolidée dans cette vue :

-   Rapport d’audit
-   Activité de réinitialisation de mot de passe
-   Activité de l’enregistrement de la réinitialisation de mot de passe
-   Activité de groupes en libre-service
-   Changements de nom de groupe d’Office 365
-   Activité d’approvisionnement de compte
-   État de substitution de mot de passe
-   Erreurs de configuration de compte


Hello rapport d’utilisation de l’Application a été améliorée et est incluse dans hello **connexions** vue. toosee cette vue, sur hello **Azure Active Directory** panneau, sous **activité**, sélectionnez **connexions**.

![Vue Connexions](./media/active-directory-reporting-migration/483.png "Vue Connexions")

Hello **connexions** vue inclut toutes les connexions utilisateur. Vous pouvez utiliser les informations d’utilisation de cette application informations tooget. Vous pouvez également afficher des informations sur l’utilisation de l’application Bonjour **des applications d’entreprise** vue d’ensemble, Bonjour **gérer** section.

![Applications d’entreprise](./media/active-directory-reporting-migration/484.png "Applications d’entreprise")

## <a name="access-a-specific-report"></a>Accéder à un rapport spécifique

Bien que hello portail Azure offre une vue unique, vous pouvez également rechercher à des rapports spécifiques.

### <a name="audit-logs"></a>Journaux d’audit

Vos commentaires toocustomer de réponse, Bonjour portail Azure, vous pouvez utiliser avancées données hello tooaccess filtrage que vous souhaitez. Un filtre, vous pouvez utiliser un *catégorie de l’activité*, qui répertorie hello différents types d’activité consigne dans Azure AD. toowhat de résultats toonarrow vous recherchez, vous pouvez sélectionner une catégorie.

Par exemple, si vous êtes uniquement intéressé par les réinitialisations de mot de passe associé tooself-service activités, vous pouvez choisir hello **gestion de mot de passe libre-service** catégorie. catégories de Hello que vous consultez sont basées sur les ressources hello dans que vous travaillez.  

![Options de catégorie sur la page de journaux d’Audit de filtre hello](./media/active-directory-reporting-migration/06.png "des options de catégorie sur la page de journaux d’Audit de filtre hello")

Les catégories d’activités sont les suivantes :

- Annuaire principal
- Gestion des mots de passe en libre-service
- Gestion des groupes en libre-service
- Approvisionnement des comptes

### <a name="application-usage"></a>Utilisation des applications

tooview des détails sur l’utilisation des applications pour toutes les applications ou d’une seule application, sous **activité**, sélectionnez **connexions**. résultats de hello toonarrow, vous pouvez filtrer sur le nom d’utilisateur ou le nom de l’application.

![Page Filtrer les événements de connexion](./media/active-directory-reporting-migration/07.png "Page Filtrer les événements de connexion")

### <a name="security-reports"></a>Rapports de sécurité

#### <a name="azure-ad-anomalous-activity-reports"></a>Rapports d’activités anormales Azure AD

Sécurité de l’activité anormale AD Azure des rapports à partir du portail Azure classic de hello ont été tooprovide consolidée vous avec une vue centralisée. Cette vue affiche tous les événements liés à la sécurité qu’Azure AD peut détecter et signaler dans des rapports.

Hello tableau suivant répertorie les rapports de sécurité de l’activité anormale hello Azure AD et les types d’événements risque correspondant Bonjour portail Azure.

| Rapport d’activités anormales Azure AD |  Type d’événement à risque signalé par Identity Protection|
| :--- | :--- |
| Utilisateurs avec des informations d’identification volées | Informations d’identification divulguées |
| Activité de connexion anormale | Voyage Impossible tooatypical emplacements |
| Connexions à partir d’appareils potentiellement infectés | Connexions depuis des appareils infectés|
| Connexions à partir de sources inconnues | Connexions depuis des adresses IP anonymes |
| Connexions depuis des adresses IP avec des activités suspectes | Connexions depuis des adresses IP avec des activités suspectes |
| - | Connexions depuis des emplacements non connus |

des rapports Hello suivant la sécurité de l’activité anormale Azure AD ne sont pas inclus en tant qu’événements risque Bonjour portail Azure :

* Connexions après plusieurs échecs
* Connexions depuis plusieurs zones géographiques

Ces rapports sont toujours disponibles dans hello portail Azure classic, mais ils seront déconseillées à un moment donné dans hello futures.

Pour plus d’informations, consultez [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md).  


#### <a name="detected-risk-events"></a>Événements à risque détectés

Hello portail Azure, vous pouvez accéder à des rapports sur les événements à risque détectés sur hello **Azure Active Directory** panneau, sous **sécurité**. Événements à risque détectés sont suivies dans hello suivant des rapports :   

- les utilisateurs à risque ;
- les connexions risquées.

![Rapports de sécurité](./media/active-directory-reporting-migration/04.png "Rapports de sécurité")

Pour plus d’informations sur les rapports de sécurité, consultez :

- [Utilisateurs sur les rapports de sécurité risque dans le portail d’Azure Active Directory hello](active-directory-reporting-security-user-at-risk.md)
- [Rapport de connexions présente des risques dans le portail d’Azure Active Directory hello](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>Rapports d’activité Bonjour portail classique Azure et hello portail Azure

tableau Hello dans cette section répertorie les rapports existants dans hello portail Azure classic. Elle décrit également comment vous pouvez obtenir hello les mêmes informations dans hello portail Azure.

tooview tous l’audit des données, sur hello **Azure Active Directory** panneau, sous **activité**, accédez trop**journaux d’Audit**.

![Journaux d’audit](./media/active-directory-reporting-migration/61.png "Journaux d’Audit")

| Portail Azure Classic                 | toofind Bonjour portail Azure                                                         |
| ---                                  | ---                                                                        |
| Journaux d’audit                           | Pour **Catégorie d’activité**, sélectionnez **Annuaire principal**.                       |
| Activité de réinitialisation de mot de passe              | Pour **Catégorie d’activité**, sélectionnez **Gestion des mots de passe en libre-service**. |
| Activité de l’enregistrement de la réinitialisation de mot de passe | Pour **Catégorie d’activité**, sélectionnez **Gestion des mots de passe en libre-service**.     |
| Activité de groupes en libre-service         | Pour **Catégorie d’activité**, sélectionnez **Gestion des groupes en libre-service**.        |
| Activité d’approvisionnement de compte        | Pour **Catégorie d’activité**, sélectionnez **Approvisionnement des utilisateurs de comptes**.         |
| État de substitution de mot de passe             | Pour **Catégorie d’activité**, sélectionnez **Substitution automatique de mot de passe d’application**.      |
| Erreurs de configuration de compte          | Pour **Catégorie d’activité**, sélectionnez **Approvisionnement des utilisateurs de comptes**.        |
| Changements de nom de groupe d’Office 365         | Pour **Catégorie d’activité**, sélectionnez **Gestion des mots de passe en libre-service**. Pour **Type de ressource activité**, sélectionnez **Groupe**. Pour **Source de l’activité**, sélectionnez **Groupes O365**.|

tooview hello **l’utilisation des applications** rapport hello **Azure Active Directory** panneau, sous **gérer**, sélectionnez **des Applications d’entreprise**, puis sélectionnez **connexions**.


![Rapport sur les connexions d’applications d’entreprise](./media/active-directory-reporting-migration/199.png "Rapport sur les connexions d’applications d’entreprise")

## <a name="next-steps"></a>Étapes suivantes

Pour une vue d’ensemble de la création de rapports, consultez hello [reporting d’Azure Active Directory](active-directory-reporting-azure-portal.md).
