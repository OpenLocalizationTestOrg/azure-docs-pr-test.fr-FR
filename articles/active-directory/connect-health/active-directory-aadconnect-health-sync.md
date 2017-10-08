---
title: aaaUsing Azure AD Connect Health avec synchronisation | Documents Microsoft
description: "Il s’agit de page hello Azure AD Connect Health aborderons toomonitor Azure AD Connect de la synchronisation."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Surveiller la synchronisation Azure AD Connect avec Azure AD Connect Health
Hello suivant documentation est spécifique toomonitoring Azure AD Connect (synchronisation) avec Azure AD Connect Health.  Pour plus d’informations sur la surveillance AD FS avec Azure AD Connect Health, consultez [Utilisation d’Azure AD Connect Health avec AD FS](active-directory-aadconnect-health-adfs.md). En outre, pour plus d’informations sur la surveillance des services de domaine Active Directory avec Azure AD Connect Health, consultez [Utilisation d’Azure AD Connect Health avec AD DS](active-directory-aadconnect-health-adds.md).

![Azure AD Connect Health pour la synchronisation](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Alertes d’Azure AD Connect Health pour la synchronisation
Alertes d’intégrité de Hello Azure AD Connect pour la section de synchronisation fournit que Hello de la liste des alertes actives. Chaque alerte inclut des informations pertinentes, les étapes de résolution et la documentation de toorelated de liens. En sélectionnant une alerte active ou résolue, vous verrez un nouveau panneau avec des informations supplémentaires, ainsi que les étapes à suivre tooresolve hello alerte et documentation tooadditional de liens. Vous pouvez également afficher les données d’historique des alertes qui ont été résolus dans hello passée.

En sélectionnant une alerte que vous seront fournies avec des informations supplémentaires ainsi que les étapes vous pouvez prendre des liens et alerte de hello tooresolve tooadditional documentation.

![Erreur de synchronisation d’Azure AD Connect](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Évaluation limitée des alertes
Si Azure AD Connect n’utilise pas la configuration par défaut de hello (par exemple, si le filtrage d’attributs est modifié à partir de la configuration de tooa de configuration par défaut hello personnalisée), puis l’agent de hello Azure AD Connect Health ne charge pas hello erreur événements connexes tooAzure AD Connect.

Cela limite l’évaluation hello des alertes par le service de hello. Serait s’affiche une bannière indiquant cette condition Bonjour Azure Portal sous votre service.

![Azure AD Connect Health pour la synchronisation](./media/active-directory-aadconnect-health-sync/banner.png)

Vous pouvez le modifier en cliquant sur « Paramètres » autorisant tooupload de l’agent Azure AD Connect Health tous les journaux d’erreurs.

![Azure AD Connect Health pour la synchronisation](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Aperçu de synchronisation
Administrateurs fréquemment souhaitez tooknow sur hello temps toosync modifications tooAzure AD et quantité hello des modifications se produisent. Cette fonctionnalité fournit un moyen simple de toovisualize cela à l’aide de hello sous graphiques :   

* Latence des opérations de synchronisation
* Tendance de modification d’objet

### <a name="sync-latency"></a>Latence de synchronisation
Cette fonctionnalité fournit une graphique tendance de la latence des opérations de synchronisation hello (importation, exportation, etc.) pour les connecteurs.  Cela fournit une rapide et facilement toounderstand hello non seulement la latence de vos opérations (supérieure si vous avez un grand ensemble de modifications qui se produisent), mais également une anomalies toodetect de façon latence hello qui peuvent nécessiter un examen supplémentaire.

![Latence de synchronisation](./media/active-directory-aadconnect-health-sync/synclatency02.png)

Par défaut, seulement la latence d’opération de 'Export' hello pour le connecteur Azure AD de hello hello est affichée.  toosee plusieurs opérations sur le connecteur de hello ou tooview à partir de tous les autres connecteurs, avec le bouton droit sur le graphique de hello, sélectionnez Modifier le graphique ou cliquez sur « Modifier le graphique latence » hello et choisissez une opération spécifique de hello et de connecteurs.

### <a name="sync-object-changes"></a>Synchronisation des modifications d’objet
Cette fonctionnalité fournit une graphique tendance du nombre de hello de modifications qui sont évaluées et exporté tooAzure AD.  Aujourd'hui, lors de la tentative de toogather ces informations à partir des journaux de synchronisation hello sont difficiles.  graphique de Hello vous donne, non seulement un moyen plus simple de l’analyse du nombre de hello de modifications qui se produisent dans votre environnement, mais également un affichage visuel d’échecs hello qui se produisent.

![Latence de synchronisation](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Rapport d’erreurs de synchronisation de niveau objet (version préliminaire)
Cette fonctionnalité fournit un rapport sur les erreurs de synchronisation qui peuvent se produire lorsque les données d’identité se synchronisent entre Windows Server AD et Azure AD à l’aide d’Azure AD Connect.

* rapport de Hello décrit les erreurs enregistrées par le client de synchronisation hello (Azure AD Connect version 1.1.281.0 ou une version ultérieure)
* Il inclut des erreurs hello s’est produite dans la dernière opération de synchronisation hello sur le moteur de synchronisation hello. (« Exporter » hello connecteur Azure AD.)
* Azure agent AD Connect Health pour la synchronisation doit avoir des points de terminaison de connexion sortante toohello requis pour les données les plus récentes hello rapport tooinclude hello.
* rapport de Hello est **mis à jour toutes les 30 minutes** à l’aide des données de salutation téléchargé par l’agent Azure AD Connect Health pour la synchronisation. Il fournit hello suivant les fonctionnalités clés

  * Catégorisation des erreurs
  * Liste d’objets avec erreur par catégorie
  * Toutes les données hello sur les erreurs hello à un seul endroit
  * Côté par comparaison d’objets avec l’erreur en raison de conflits de tooa
  * Télécharger le rapport d’erreurs hello sous la forme d’un CV (prochainement)

### <a name="categorization-of-errors"></a>Catégorisation des erreurs
rapport de Hello classe les erreurs de synchronisation existant hello Bonjour suivant des catégories :

| Catégorie | Description |
| --- | --- |
| Attribut en double |Erreurs quand Azure AD Connect tente de créer ou de mettre à jour des objets avec des valeurs dupliquées d’un ou plusieurs attributs dans Azure AD et qui doivent être uniques dans un client, par exemple proxyAddresses et UserPrincipalName. |
| Incohérence de données |Erreurs lors de hello soft-correspondance toomatch les objets qui génèrent des erreurs de synchronisation. |
| Échec de validation de données |Erreurs en raison de données tooinvalid, tels que des caractères non pris en charge dans les attributs critiques telles que UserPrincipalName, mettre en forme les erreurs dont la validation avant d’être écrites dans Azure AD échouent. |
| Attribut de grande taille |Erreurs lors de l’un ou plusieurs attributs sont plus grands que hello autorisée taille, de longueur ou de nombre. |
| Autres |Toutes les autres erreurs qui ne tiennent pas dans hello au-dessus des catégories. En fonction des informations reçues, cette catégorie sera divisées en plusieurs sous-catégories. |

![Rapport de résumé des erreurs de synchronisation](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Catégories de rapports d’erreurs de synchronisation](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Liste d’objets avec erreur par catégorie
L’exploration dans chaque catégorie fournira liste hello des objets d’erreur de hello dans cette catégorie.
![Liste de rapports d’erreurs de synchronisation](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Détails de l’erreur
Données suivantes sont disponibles dans hello vue pour chaque erreur détaillée

* Les identificateurs hello *objet AD* impliqués
* Les identificateurs hello *objet Active Directory de Azure* impliqués (le cas échéant)
* Description de l’erreur et comment toofix
* Articles connexes

![Détails du rapport d’erreurs de synchronisation](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Télécharger le rapport d’erreurs hello en tant que volume partagé de cluster
En sélectionnant hello bouton que vous pouvez télécharger un fichier CSV avec tous les détails de hello sur toutes les erreurs de hello « exportation ».

## <a name="related-links"></a>Liens connexes
* [Résolution des erreurs lors de la synchronisation](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [Résilience d’attribut en double](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installation de l'agent Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Opérations Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Utilisation d’Azure AD Connect Health avec AD FS](active-directory-aadconnect-health-adfs.md)
* [Utilisation d’Azure AD Connect Health avec AD DS](active-directory-aadconnect-health-adds.md)
* [Forum Aux Questions (FAQ) Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historique de publication des versions d’Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)