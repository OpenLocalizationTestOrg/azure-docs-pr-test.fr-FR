---
title: "aaaView vos rapports d’accès et d’utilisation | Documents Microsoft"
description: "Explique comment tooview accès et utilisation des rapports toogain approfondie d’intégrité de hello et la sécurité de répertoire de votre organisation."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a>Afficher vos rapports d'accès et d'utilisation
*Cette documentation fait partie de hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).*

Vous pouvez utiliser l’accès Azure Active Directory et l’utilisation des rapports toogain visibilité intégrité de hello et la sécurité de répertoire de votre organisation. Avec cette information, un administrateur d’annuaire peut déterminer plus précisément où peut se trouver des risques de sécurité afin qu’ils peuvent planifier en conséquence toomitigate ces risques.

Bonjour portail de gestion Azure, les rapports sont classés Bonjour suivant façons :

* Rapports d’anomalies – Contain événements de connexion que nous avons trouvé toobe anormale. Notre objectif est toomake vous prenant en charge de cette activité et vous toobe toomake en mesure de déterminer si un événement est suspect.
* Rapports d’application intégrée : fournissent des indications sur l'utilisation des applications du cloud au sein de votre société. Azure Active Directory permet d’intégrer des milliers d'applications du cloud.
* Erreur – ces rapports indiquent les erreurs qui peuvent se produire lors de la configuration des applications tooexternal de comptes.
* Rapports spécifiques à l'utilisateur : affichent les données d'activité relatives aux appareils/connexions d’un utilisateur spécifique.
* Journaux d’activité – contiennent un enregistrement de tous les événements audités dans hello dernières 24 heures, 7 derniers jours, ou 30 derniers jours, ainsi que modifications d’activité de groupe et activité d’inscription et de réinitialisation de mot de passe.

> [!NOTE]
> * Certains rapports d'utilisation de ressources et d’anomalies avancés ne sont disponibles que lorsque vous activez [Azure Active Directory Premium](active-directory-get-started-premium.md). Les rapports avancés permettent d’améliorer la sécurité d’accès, répondre à des menaces de toopotential et obtenir un accès tooanalytics sur l’utilisation du périphérique de l’accès et l’application.
> * Azure Active Directory Premium et les éditions de base sont disponibles pour les clients en Chine utilisent hello instance mondiale d’Azure Active Directory. Azure Active Directory Premium et les éditions de base ne sont pas actuellement pris en charge dans le service Microsoft Azure hello géré par 21Vianet en Chine. Pour plus d’informations, veuillez nous contacter à hello [Forum Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).
> 
> 

## <a name="reports"></a>Rapports
| Rapport | Description |
| --- | --- |
| **Rapports d’activités anormales** | |
| [Connexions à partir de sources inconnues](active-directory-reporting-sign-ins-from-unknown-sources.md) |Peut indiquer qu’un toosign tentative dans sans suivi. |
| [Connexions après plusieurs échecs](active-directory-reporting-sign-ins-after-multiple-failures.md) |Peut indiquer une attaque en force brute réussie. |
| [Connexions depuis plusieurs zones géographiques](active-directory-reporting-sign-ins-from-multiple-geographies.md) |Peut indiquer que plusieurs utilisateurs sont connectent avec hello que même compte. |
| [Connexions à partir d’adresses IP affichant une activité suspecte](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |Peut indiquer une connexion réussie après une tentative d'intrusion insistante. |
| [Connexions à partir d’appareils potentiellement infectés](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |Peut indiquer un toosign tentative dans à partir d’appareils potentiellement infectés. |
| [Activité de connexion anormale](active-directory-reporting-irregular-sign-in-activity.md) |Peut indiquer les modèles de connexion des toousers événements anormaux. |
| [Utilisateurs ayant une activité de connexion anormale](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |Indique des utilisateurs dont les comptes ont été compromis. |
| Utilisateurs avec des informations d’identification volées |Utilisateurs avec des informations d’identification volées |
| **Journaux d’activité** | |
| Rapport d'audit |Événements audités dans votre répertoire |
| Activité de réinitialisation de mot de passe |Fournit une vue détaillée des réinitialisations de mot de passe qui se produisent dans votre organisation. |
| Activité de l’enregistrement de la réinitialisation de mot de passe |Fournit une vue détaillée des réinitialisations de mot de passe qui se produisent dans votre organisation. |
| Activité de groupes en libre-service |Fournit un tooall de journal d’activité activités des groupes libre-service de votre annuaire |
| **Applications intégrées** | |
| Utilisation des applications |Fournit un résumé de l'utilisation de toutes les applications SaaS intégrées à votre répertoire. |
| Activité d’approvisionnement de compte |Fournit un historique des tentatives applications de tooexternal tooprovision comptes. |
| État de substitution de mot de passe |Fournit une vue d'ensemble détaillée de l'état de substitution de mot de passe automatique des applications SaaS. |
| Erreurs de configuration de compte |Indique les applications tooexternal des toousers d’un impact sur les accès. |
| **Gestion des droits** | |
| Utilisation de RMS |Fournit un résumé de l'utilisation de Rights Management |
| Utilisateurs RMS les plus actifs |Répertorie les 1 000 premiers utilisateurs actifs ayant accédé aux fichiers protégés par RMS |
| Utilisation d’un appareil RMS |Répertorie les appareils utilisés pour l'accès aux fichiers protégés par RMS |
| Utilisation d’applications fonctionnant avec RMS |Fournit des applications activées pour l'utilisation de RMS |

## <a name="report-editions"></a>Éditions de rapport
| Rapport | Gratuit | De base | Premium |
| --- | --- | --- | --- |
| **Rapports d’activités anormales** | | | |
| Connexions à partir de sources inconnues |✓ |✓  |✓ |
| Connexions après plusieurs échecs |✓ |✓  |✓ |
| Connexions depuis plusieurs zones géographiques |✓ |✓  |✓ |
| Connexions à partir d’adresses IP affichant une activité suspecte | | |✓ |
| Connexions à partir d’appareils potentiellement infectés | | |✓ |
| Activité de connexion anormale | | |✓ |
| Utilisateurs ayant une activité de connexion anormale | | |✓ |
| Utilisateurs avec des informations d’identification volées | | |✓ |
| **Journaux d’activité** | | | |
| Rapport d'audit |✓ |✓  |✓ |
| Activité de réinitialisation de mot de passe | | |✓ |
| Activité de l’enregistrement de la réinitialisation de mot de passe | | |✓ |
| Activité de groupes en libre-service | | |✓ |
| **Applications intégrées** | | | |
| Utilisation des applications | | |✓ |
| Activité d’approvisionnement de compte |✓ |✓  |✓ |
| État de substitution de mot de passe | | |✓ |
| Erreurs de configuration de compte |✓ |✓  |✓ |
| **Gestion des droits** | | | |
| Utilisation de RMS | | |RMS uniquement |
| Utilisateurs RMS les plus actifs | | |RMS uniquement |
| Utilisation d’un appareil RMS | | |RMS uniquement |
| Utilisation d’applications fonctionnant avec RMS | | |RMS uniquement |

## <a name="anomalous-activity-reports"></a>Rapports d’activités anormales
<p>Hello anormale se connecter dans les rapports d’activité indicateur suspect de connexion tooOffice365 d’activité, portail de gestion Azure, panneau d’accès Azure AD, Sharepoint Online, Dynamics CRM Online et autres services Microsoft online services.</p>

<p>Tous ces rapports, à ceci près hello rapports « Connexions après plusieurs échecs », indicateur également suspectes <i>fédéré</i> signer ins toohello susmentionnés services, quel que soit le fournisseur de fédération hello. </p>

<p>Hello suivant des rapports est disponible : </p><ul>

<li>[Connexions à partir de sources inconnues](active-directory-reporting-sign-ins-from-unknown-sources.md).</li>

<li>[Connexions après plusieurs échecs](active-directory-reporting-sign-ins-after-multiple-failures.md).</li>

<li>[Connexions depuis plusieurs zones géographiques](active-directory-reporting-sign-ins-from-multiple-geographies.md).</li>

<li>[Connexions à partir d’adresses IP affichant une activité suspecte](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</li>

<li>[Activité de connexion anormale](active-directory-reporting-irregular-sign-in-activity.md).</li>

<li>[Connexions à partir d’appareils potentiellement infectés](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</li>

<li>[Utilisateurs ayant une activité de connexion anormale](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</li>

<li>Utilisateurs avec des informations d’identification volées</li></ul>

## <a name="activity-logs"></a>Journaux d’activité
### <a name="audit-report"></a>Rapport d'audit
| Description | Emplacement du rapport |
|:--- |:--- |
| Affiche un enregistrement de tous les événements audités dans hello des dernières 24 heures, des 7 derniers jours ou des 30 derniers jours. <br /> Pour plus d'informations, consultez la rubrique [Événements de rapport d’audit d'Azure Active Directory](active-directory-reporting-audit-events.md) |Répertoire > onglet Rapports |

![Rapport d'audit](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a>Activité de réinitialisation de mot de passe
| Description | Emplacement du rapport |
|:--- |:--- |
| Indique toutes les tentatives de réinitialisation de mot de passe réalisées dans votre société |Répertoire > onglet Rapports |

![Activité de réinitialisation de mot de passe](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a>Activité de l’enregistrement de la réinitialisation de mot de passe
| Description | Emplacement du rapport |
|:--- |:--- |
| Indique l’ensemble des enregistrements de réinitialisation de mot de passe réalisés dans votre société |Répertoire > onglet Rapports |

![Activité de l’enregistrement de la réinitialisation de mot de passe](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a>Activité de groupes en libre-service
| Description | Emplacement du rapport |
|:--- |:--- |
| Affiche toutes les activités pour hello libre-service des groupes gérés dans votre annuaire. |Répertoire > Utilisateurs > <i>Utilisateur</i> > onglet Périphériques |

![Activité de groupes en libre-service](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>Rapports d’applications intégrées
### <a name="application-usage-summary"></a>Utilisation des applications : résumé
| Description | Emplacement du rapport |
|:--- |:--- |
| Utilisez ce rapport lorsque vous souhaitez que l’utilisation de toosee pour toutes les applications SaaS de hello dans votre annuaire. Ce rapport est basé sur le nombre hello de fois où les utilisateurs cliquent sur l’application hello Bonjour panneau d’accès. |Répertoire > onglet Rapports |

Ce rapport inclut les connexions trop*tous les* applications votre annuaire comporte l’accès, notamment les applications Microsoft pré-intégrées.

Les applications Microsoft pré-intégrées incluent Office 365, Sharepoint, hello portail de gestion Azure et autres.

![Résumé de l’utilisation des applications](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>Utilisation des applications : présentation détaillée
| Description | Emplacement du rapport |
|:--- |:--- |
| Utilisez ce rapport lorsque vous souhaitez toosee combien une application SaaS spécifique est utilisée. Ce rapport est basé sur le nombre hello de fois où les utilisateurs cliquent sur l’application hello Bonjour panneau d’accès. |Répertoire > onglet Rapports |

### <a name="application-dashboard"></a>Tableau de bord de l’application
| Description | Emplacement du rapport |
|:--- |:--- |
| Ce rapport indique l’application de toohello ins cumul par les utilisateurs de votre organisation, sur un intervalle de temps sélectionné. graphique de Hello sur la page du tableau de bord hello vous aidera à identifier les tendances pour toutes les utilisations de cette application. |Répertoire > Application > onglet Tableau de bord |

## <a name="error-reports"></a>Rapports d'erreurs
### <a name="account-provisioning-errors"></a>Erreurs de configuration de compte
| Description | Emplacement du rapport |
|:--- |:--- |
| Utilisez cette toomonitor les erreurs qui se produisent pendant la synchronisation hello des comptes à partir d’applications de SaaS tooAzure Active Directory. |Répertoire > onglet Rapports |

![Erreurs de configuration de compte](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>Rapports d’erreur spécifiques à l’utilisateur
### <a name="devices"></a>Appareils
| Description | Emplacement du rapport |
|:--- |:--- |
| Utilisez ce rapport lorsque vous souhaitez l’adresse IP de hello toosee et l’emplacement géographique d’appareils qu’un utilisateur spécifique a utilisé tooaccess Azure Active Directory. |Répertoire > Utilisateurs > <i>Utilisateur</i> > onglet Périphériques |

### <a name="activity"></a>Activité
| Description | Emplacement du rapport |
|:--- |:--- |
| Affiche hello d’authentification dans l’activité d’un utilisateur. rapport de Hello inclut des informations telles que l’application hello connecté, appareil utilisé, adresse IP et emplacement. Nous ne collectons pas historique hello pour les utilisateurs qui se connectent avec un compte Microsoft. |Répertoire > Utilisateurs > <i>Utilisateur</i> > onglet Activités |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a>Connectez-vous aux événements inclus dans hello rapport activité utilisateur
Seuls certains types d’événements de connexion apparaîtront dans hello rapport activité utilisateur.

| Type d'événement | Inclus ? |
| --- | --- |
| Signer des modules toohello [panneau d’accès](http://myapps.microsoft.com/) |Oui |
| Signer des modules toohello [portail de gestion Azure](https://manage.windowsazure.com/) |Oui |
| Signer des modules toohello [portail Microsoft Azure](https://portal.azure.com/) |Oui |
| Signer des modules toohello [portail Office 365](http://portal.office.com/) |Oui |
| Signer des modules tooa application native, comme Outlook (consultez l’exception ci-dessous) |Oui |
| Signer tooa ins fédéré/configuré une application via hello volet d’accès, tel que Salesforce |Oui |
| Signer ins tooa mot de passe application via hello volet d’accès, tels que Twitter |Oui |
| Signe ins application tooa métier personnalisée qui a été ajoutée toohello Active |Non (bientôt disponible) |
| Signer ins tooan Proxy d’Application Azure AD application qui a été ajouté toohello Active |Non (bientôt disponible) |

> Remarque : connexions de quantité de hello tooreduce du bruit dans ce rapport, par hello [Assistant Microsoft Online Services Sign](http://community.office365.com/en-us/w/sso/534.aspx) ne sont pas affichés.
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a>Éléments tooconsider si vous pensez que la violation de la sécurité
Si vous pensez qu’un compte d’utilisateur peut être compromis ou n’importe quel type d’activités utilisateur suspectes pouvant entraîner tooa violation de la sécurité de vos données d’annuaire dans le cloud de hello, vous pouvez tooconsider un ou plusieurs de hello suivant des actions :

* Activité de hello hello contact utilisateur tooverify
* Réinitialiser le mot de passe de l’utilisateur hello
* [Activez l'authentification multi-facteur](../multi-factor-authentication/multi-factor-authentication-get-started.md) pour renforcer la sécurité

## <a name="view-or-download-a-report"></a>Afficher ou télécharger un rapport
1. Bonjour portail Azure classic, cliquez sur **Active Directory**, cliquez sur nom hello du répertoire de votre organisation, puis cliquez sur **rapports**.
2. Sur la page de rapports hello, cliquez sur rapport hello tooview et/ou télécharger.
   
   > [!NOTE]
   > S’il s’agit hello première fois que vous avez utilisé hello reporting fonctionnalité d’Azure Active Directory, vous verrez un tooOpt message dans. Si vous acceptez, cliquez sur toocontinue d’icône de coche hello.
   > 
   > 
3. Cliquez sur tooInterval suivant du menu déroulant hello et puis sélectionnez une des hello suivant des plages de temps qui doivent être utilisées lors de la génération de ce rapport :
   
   * 24 dernières heures
   * 7 derniers jours
   * 30 derniers jours
4. Cliquez sur le rapport hello toorun hello coche icône.
   * Des too1000 événements seront affichera dans hello portail Azure classic.
5. Le cas échéant, cliquez sur **télécharger** toodownload hello rapport tooa fichier compressé au format de valeurs séparées par des virgules (CSV) pour le consulter hors ligne ou à des fins d’archivage.
   * Les too75, 000 événements seront inclus dans le fichier de hello téléchargé.
   * Pour plus de données, consultez hello [API de création de rapports AD Azure](active-directory-reporting-api-getting-started.md).

## <a name="ignore-an-event"></a>Ignorer un événement
Si vous affichez des rapports d'anomalie, vous remarquerez peut-être que vous pouvez ignorer les différents événements qui sont mentionnés dans les rapports connexes. tooignore un événement, mettez-le en surbrillance événement hello dans les rapports de hello, puis cliquez sur **ignorer**. Hello **ignorer** bouton pour supprimer définitivement les événements mis en surbrillance hello de rapport de hello et ne peut être utilisée que par les administrateurs globaux autorisés.

## <a name="automatic-email-notifications"></a>Notifications automatiques par courrier électronique
Pour plus d’informations sur les notifications de création de rapport Azure AD, consultez [Notifications de création de rapport Azure Active Directory](active-directory-reporting-notifications.md).

## <a name="whats-next"></a>Étapes suivantes
* [Prise en main d’Azure Active Directory Premium (AD)](active-directory-get-started-premium.md)
* [Ajouter des logos tooyour pages de connexion et du volet d’accès de la société](active-directory-add-company-branding.md)

