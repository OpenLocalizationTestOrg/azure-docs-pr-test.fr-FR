---
title: "aaaSettings et FAQ sur l’itinérance des données | Documents Microsoft"
description: "Fournit des réponses aux questions de toosome les administrateurs informatiques peuvent avoir sur les paramètres et la synchronisation de données d’application."
services: active-directory
keywords: "paramètres enterprise state roaming, cloud windows, forum aux questions sur enterprise state roaming"
documentationcenter: 
author: tanning
manager: swadhwa
editor: curtand
ms.assetid: c0824f5c-129b-4240-969f-921f6a64eae7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4d6d6619b3a5fbd1d274603808d89b73ed942cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="settings-and-data-roaming-faq"></a>FAQ sur l’itinérance des paramètres et des données
Cette rubrique répond à certaines questions que les administrateurs informatiques peuvent se poser sur les paramètres et la synchronisation des données d’application.

## <a name="what-data-roams"></a>Quelles données sont itinérantes ?
**Paramètres Windows**: hello paramètres du PC qui sont intégrées dans le système d’exploitation de Windows hello. En règle générale, il s’agit des paramètres que vous personnalisez votre PC et inclure des hello suivant grandes catégories :

* Le *Thème* comprenant des fonctionnalités telles que les paramètres de thème du bureau et de la barre des tâches.
* Les *paramètres Internet Explorer* comprenant les onglets récemment ouverts et les favoris.
* Les *Paramètres du navigateur Edge*, tel que les favoris et la liste de lecture.
* Les *Mots de passe* comprenant les mots de passe Internet, les profils Wi-Fi, etc.
* Les *Préférences linguistiques* comprenant la disposition du clavier, la langue du système, la date et l’heure, etc.
* Les *Options d’ergonomie* comprenant les thèmes à contraste élevé, le Narrateur et la Loupe.
* Les *Autres paramètres Windows* comprenant les paramètres d’invite de commandes et la liste des applications.

**Données d’application**: les applications Windows universelles peuvent écrire tooa de données de paramètres du dossier itinérants, et toutes les données écrites toothis dossier sont automatiquement synchronisées. C’est toohello différentes applications développeur toodesign un avantage de tootake d’application de cette fonctionnalité. Pour plus d’informations sur comment toodevelop une application Windows universelle qui utilise des fonctions d’itinérance, consultez hello [API de stockage appdata](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx) et hello [appdata Windows 8 itinérance blog des développeurs](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx).

## <a name="what-account-is-used-for-settings-sync"></a>Quel compte est utilisé pour la synchronisation des paramètres ?
Dans Windows 8 et Windows 8.1, la synchronisation des paramètres a toujours utilisé les comptes Microsoft consommateur. Utilisateurs de l’entreprise avaient hello capacité tooconnect un tootheir de compte Microsoft Active Directory domaine compte toogain accès toosettings sync. Dans Windows 10, cette fonctionnalité « compte Microsoft connecté » est remplacée par une structure de compte principal et secondaire.

le compte principal Hello est défini comme compte de hello utilisé toosign dans tooWindows. Il peut s’agir d’un compte Microsoft, d’un compte Azure Active Directory (Azure AD), d’un compte Active Directory local ou d’un compte local. Compte de principal toohello addition, aux utilisateurs de Windows 10 d’ajouter un ou plusieurs périphériques de tootheir de comptes cloud secondaire. Un compte secondaire est généralement un compte Microsoft, Active Directory, ou un autre compte tel que Gmail ou Facebook. Ces comptes secondaire fournissant un accès tooadditional des services tels que l’authentification unique et hello du Windows Store, mais ils ne sont pas capables d’alimenter la synchronisation des paramètres.

Dans Windows 10, uniquement hello compte principal pour les appareils hello peut être utilisé pour la synchronisation des paramètres (voir [comment passer de la synchronisation de paramètres de compte Microsoft dans synchronisation des paramètres Windows 8 tooAzure AD dans Windows 10 ?](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10)).

Données ne sont jamais mélangées entre hello différents comptes d’utilisateurs sur l’appareil de hello. Il existe deux règles de synchronisation des paramètres :

* Paramètres Windows itinérant toujours avec le compte principal hello.
* Les données d’application seront marquées avec l’application de hello tooacquire hello compte utilisé. Seules les applications marquées avec le compte principal hello seront synchronisés. Le balisage de la propriété application est déterminé lorsqu’une application est chargée côté via hello Windows Store ou de gestion des appareils mobiles (MDM).

Si le propriétaire de l’application ne peut pas être identifié, déplacera avec le compte principal hello. Si un appareil est mis à niveau à partir de Windows 8 ou Windows 8.1 tooWindows 10, toutes les applications hello seront marquées comme acquis par le compte Microsoft de hello. Il s’agit, car la plupart des utilisateurs acquérir des applications via hello du Windows Store, et aucune prise en charge du Windows Store tooWindows préalable de comptes Azure AD 10. Si une application est installée via une licence hors connexion, l’application hello est marquée à l’aide du compte de principal hello sur l’appareil de hello.

> [!NOTE]
> Les appareils Windows 10 appartenant à l’entreprise et sont connecté tooAzure AD ne peuvent ne plus se connecter à leur compte de domaine tooa comptes Microsoft. Hello capacité tooconnect un compte de domaine Microsoft compte tooa et ont la synchronisation des données de tous les utilisateurs hello toohello compte Microsoft (autrement dit, hello Microsoft compte itinérance via le compte Microsoft de hello connecté et les fonctionnalités Active Directory) est supprimé Les appareils Windows 10 qui sont jointe tooa connecté à Active Directory ou Azure AD votre environnement.
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-tooazure-ad-settings-sync-in-windows-10"></a>Comment passer de la synchronisation de paramètres de compte Microsoft dans synchronisation des paramètres Windows 8 tooAzure AD dans Windows 10 ?
Si vous êtes toohello joint à un domaine d’Active Directory exécutant Windows 8 ou Windows 8.1 avec un compte connecté à Microsoft, vous synchroniser les paramètres via votre compte Microsoft. Après la mise à niveau tooWindows 10, vous continuerez toosync les paramètres utilisateur via un compte Microsoft tant que vous êtes un utilisateur appartenant au domaine et de domaine Active Directory de hello ne se connecte pas à Azure AD.

Si hello local domaine Active Directory se connecte à Azure AD, votre périphérique va tenter de paramètres toosync à l’aide du compte Azure Active Directory hello connecté. Si administrateur de hello Azure AD ne permet pas d’Enterprise State Roaming, à votre connecté compte Azure AD s’arrête à la synchronisation des paramètres. Si vous êtes un utilisateur Windows 10 et que vous vous connectez avec une identité Azure AD, vous pouvez commencer la synchronisation des paramètres Windows dès que votre administrateur active la synchronisation des paramètres via Azure AD.

Si vous avez stocké des données personnelles de votre appareil d’entreprise, sachez que système d’exploitation Windows et les données d’application commence la synchronisation tooAzure AD. Cela a hello suivant implications :

* Paramètres de votre compte Microsoft personnels seront dérive indépendamment des paramètres de hello sur votre travail ou d’établissement scolaire Azure AD. C’est parce que la synchronisation de compte Microsoft de hello et paramètres d’Azure AD sont maintenant en utilisant les comptes distincts.
* Les données personnelles (mots de passe Wi-Fi, informations d’identification web et favoris d’Internet Explorer) qui étaient auparavant synchronisées via un compte Microsoft seront maintenant synchronisées via Azure AD.

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>Comment fonctionne l’interopérabilité d’Azure AD Enterprise State Roaming et des comptes Microsoft ?
Hello novembre 2015 ou versions ultérieures de Windows 10, Enterprise State Roaming est uniquement prise en charge pour un seul compte à la fois. Si vous vous connectez dans tooWindows à l’aide d’une entreprise ou école compte Azure AD, toutes les données sont synchronisés au moyen d’Azure AD. Si vous vous connectez dans tooWindows à l’aide d’un compte Microsoft personnel, toutes les données sont synchronisés au moyen de hello compte Microsoft. Appdata universel itinérant à l’aide de la seule hello principal compte de connexion sur l’appareil de hello et déplacera uniquement si la licence de l’application hello appartient à un compte de principal hello. Appdata universel pour les applications hello appartenant à des comptes secondaires n’est pas synchronisé.

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>Les paramètres se synchronisent-ils pour les comptes Azure AD regroupant plusieurs clients ?
Lorsque plusieurs Azure AD des comptes à partir de différents clients Azure AD sont sur hello même périphérique, vous devez mettre à jour toocommunicate de Registre du périphérique hello avec Azure Rights Management (Azure RMS) pour chaque locataire Azure AD.  

1. Recherche hello GUID pour chaque locataire Azure AD. Ouvrez hello portail Azure classic et sélectionner un locataire Azure AD. Hello GUID pour le client de hello est hello adresse URL dans la barre d’adresses hello de votre navigateur. Par exemple : `https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. Une fois que vous avez hello GUID, vous devrez la clé de Registre tooadd hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<GUID de l’ID de client >**.
   À partir de hello **GUID de l’ID de client** clé, créez une nouvelle valeur de chaînes multiples (REG-MULTI-SZ) nommée **AllowedRMSServerUrls**. Pour ses données, spécifiez hello licences URL de point de distribution de hello autres locataires Azure hello d’accès de périphérique.
3. Vous pouvez trouver hello licences URL de point de distribution en exécutant hello **Get-AadrmConfiguration** applet de commande. Si des valeurs hello hello **LicensingIntranetDistributionPointUrl** et **LicensingExtranetDistributionPointUrl** sont différents, spécifiez les deux valeurs. Si hello sont des valeurs hello même, spécifiez les valeur hello une seule fois.

## <a name="what-are-hello-roaming-settings-options-for-existing-windows-desktop-applications"></a>Quelles sont les options de paramètres itinérants hello pour les applications de bureau Windows existantes ?
L’itinérance ne fonctionne qu’avec les applications Windows universelles. Deux options permettent d’activer l’itinérance sur une application de bureau Windows existante :

* Hello [bureau pont](http://aka.ms/desktopbridge) vous permet de mettre votre toohello d’applications de bureau Windows existant plateforme Windows universelle. À ce stade, les modifications de code minimal requis parti tootake d’itinérance des données d’application Azure AD. Hello bureau pont fournit à vos applications avec une identité de l’application, qui est nécessaire à des données d’application tooenable itinérants pour des applications de bureau existantes.
* [User Experience Virtualization (UE-V)](https://technet.microsoft.com/library/dn458947.aspx) vous permet de créer un modèle de paramètres personnalisés pour les applications de bureau Windows existantes et d’activer le mode itinérant pour les applications Win32. Cette option ne requiert pas de code de toochange hello application développeur de l’application hello. UE-V est limitée tooon local Active Directory itinérants pour les clients qui ont acheté hello Microsoft Desktop Optimization Pack.

Les administrateurs peuvent configurer les données d’application de bureau UE-V tooroam Windows en modifiant l’itinérance des paramètres de système d’exploitation Windows et les données d’application universelle via [des stratégies de groupe UE-V](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2), y compris :

* La stratégie de groupe « Roam Windows settings » (Activer l’itinérance des paramètres Windows)
* La stratégie de groupe « Do not synchronize Windows Apps » (Ne pas synchroniser les applications Windows)
* Internet Explorer d’itinérance dans la section relative aux applications hello

Bonjour future, Microsoft peut examiner toomake façons QU'UE-V est profondément intégré à Windows et étendre les paramètres de tooroam UE-V via hello cloud d’Azure AD.

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>Puis-je stocker localement les paramètres et les données synchronisés ?
Enterprise State Roaming de stocke toutes les données synchronisées Bonjour cloud Azure. UE-V offre une solution d’itinérance locale.

## <a name="who-owns-hello-data-thats-being-roamed"></a>Qui est propriétaire des données hello qui sont en cours se déplacées ?
les entreprises Hello propres hello données déplacées via Enterprise State Roaming. Les données sont stockées dans un centre de données Azure. Toutes les données utilisateur est chiffrée à la fois en transit et au repos dans le cloud hello à l’aide d’Azure RMS. Il s’agit d’une synchronisation de paramètres basés sur le compte d’amélioration du produit par rapport tooMicrosoft, qui chiffre uniquement certaines données sensibles telles que des informations d’identification de l’utilisateur avant qu’il quitte l’appareil de hello.

Microsoft est validée toosafeguarding les données des clients. Les données de paramètres d’un utilisateur de l’entreprise sont automatiquement chiffrées par Azure RMS avant qu’elles quittent un appareil Windows 10, afin qu’elles soient illisibles pour les autres utilisateurs. Si votre organisation dispose d’un abonnement payant pour Azure RMS, vous pouvez utiliser d’autres fonctionnalités d’Azure RMS, telles que de suivre et révoquer des documents, automatiquement protéger des messages électroniques qui contiennent des informations sensibles et gérer vos propres clés (hello également solution « bring your own key », appelé BYOK). Pour plus d’informations sur ces fonctionnalités et sur le fonctionnement d’Azure RMS, consultez l’article [En quoi consiste Azure Rights Management ?](https://technet.microsoft.com/jj585026.aspx).

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>Puis-je gérer la synchronisation d’un paramètre ou d’une application spécifique ?
Dans Windows 10, il n’existe aucun toodisable paramètre stratégie de groupe ou de gestion des appareils mobiles itinérance d’une application. Les administrateurs client peuvent désactiver la synchronisation des données d’application pour toutes les applications sur un appareil géré, mais il n’existe aucun contrôle plus précis au niveau ou au sein de l’application.

## <a name="how-can-i-enable-or-disable-roaming"></a>Comment puis-je activer ou désactiver l’itinérance ?
Bonjour **paramètres** application, accédez trop**comptes** > **synchroniser vos paramètres**. À partir de cette page, vous pouvez voir le compte qui est en cours tooroam utilisé les paramètres, et vous pouvez activer ou désactiver les groupes individuels de toobe paramètres déplacés.

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>Quelle est la recommandation de Microsoft pour l’activation de l’itinérance dans Windows 10 ?
Microsoft propose quelques solutions d’itinérances de paramètres, notamment les profils utilisateur itinérant, UE-V et Enterprise State Roaming.  Microsoft s’engage toomaking un placement dans Enterprise State Roaming dans les futures versions de Windows. Si votre organisation n’est pas prêt ou à l’aise avec déplacement données toohello dans le cloud, nous recommandons que vous utilisez UE-V comme votre technologie itinérant principal. Si votre organisation nécessite des profils itinérants pour des applications de bureau Windows existantes, mais est toomove hâtif toohello cloud, nous vous recommandons d’utiliser Enterprise état itinérant et UE-V. Bien que UE-V et Enterprise State Roaming soient des technologies très similaires, elles ne sont pas mutuellement exclusives. Leur complémentarité toohelp vous assurer que votre organisation fournit hello itinérance services dont vos utilisateurs ont besoin.  

Lorsque vous utilisez à la fois Enterprise State Roaming et UE-V, hello suivant les règles s’appliquent :

* Enterprise State Roaming est hello principal itinérant l’agent sur l’appareil de hello. UE-V est en cours toosupplement utilisé hello « Intervalle de Win32 ».
* Itinérance pour les paramètres de Windows et les données d’application UWP modernes UE-V doit être désactivé lorsque des stratégies à l’aide du groupe de hello UE-V. Ceux-ci sont déjà couverts par Enterprise State Roaming.

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>Comment la solution Enterprise State Roaming prend-elle en charge Virtual Desktop Infrastructure (VDI) ?
Enterprise State Roaming est pris en charge sur les SKU client Windows 10, mais pas sur les éditions serveur. Si un ordinateur virtuel du client est hébergé sur un ordinateur de l’hyperviseur et que vous vous connectez à distance dans la machine virtuelle de toohello, vos données circuleront. Si plusieurs utilisateurs de partager le même système d’exploitation et les utilisateurs se connectent à distance dans server tooa pour une expérience complète de hello, itinérance peut ne pas fonctionnent. dernier basé sur session scénario Hello n’est pas officiellement pris en charge.

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>Que se passe-t-il si mon organisation achète Azure RMS après avoir utilisé l’itinérance ?
Si votre organisation utilise déjà itinérance dans Windows 10 avec hello abonnement gratuit limitations d’utilisation de Azure RMS, acheter un abonnement Azure RMS n’auront aucun impact sur la fonctionnalité d’itinérant de hello hello, et aucune modification de configuration est requis par votre administrateur informatique.

## <a name="known-issues"></a>Problèmes connus
Consultez la documentation de hello Bonjour [dépannage](active-directory-windows-enterprise-state-roaming-troubleshooting.md) section pour obtenir la liste des problèmes connus. 

## <a name="related-topics"></a>Rubriques connexes
* [Présentation d’Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Activer Enterprise State Roaming dans Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Paramètres de stratégie de groupe et de MDM pour la synchronisation des paramètres](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Référence des paramètres d’itinérance Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Dépannage](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
