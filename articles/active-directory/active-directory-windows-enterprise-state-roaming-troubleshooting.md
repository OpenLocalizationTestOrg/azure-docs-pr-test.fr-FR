---
title: "Résolution des problèmes de paramètres Enterprise State Roaming dans Azure Active Directory | Microsoft Docs"
description: "Fournit des réponses aux questions de toosome les administrateurs informatiques peuvent avoir sur les paramètres et la synchronisation de données d’application."
services: active-directory
keywords: "paramètres enterprise state roaming, cloud windows, forum aux questions sur enterprise state roaming"
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>Résolution des problèmes de paramètres Enterprise State Roaming dans Azure Active Directory

Cette rubrique fournit des informations sur la façon de tootroubleshoot et de diagnostiquer les problèmes avec Enterprise State Roaming et fournit une liste des problèmes connus.

## <a name="preliminary-steps-for-troubleshooting"></a>Étapes préliminaires pour la résolution des problèmes 
Avant de commencer la résolution des problèmes, vérifiez que des périphériques et des utilisateurs de hello ont été configurés correctement et que toutes les exigences de hello de Enterprise State Roaming sont remplies par l’appareil de hello et utilisateur de hello. 

1. Windows 10, hello dernières mises à jour et un minimum Version 1511 (version du système d’exploitation 10586 ou ultérieure) est installé sur l’appareil de hello. 
2. l’appareil Hello est Azure AD joint, ou à un domaine et inscrit auprès d’Azure AD.
3. Dans le portail Azure Active Directory hello, **Enterprise State Roaming** est activée pour le répertoire hello sous **configurer** > **périphériques**  >  **Les utilisateurs peuvent synchroniser les paramètres et données d’application Enterprise**. Tous les utilisateurs sont sélectionnés ou hello utilisateur est activé pour la synchronisation via l’option de hello sélectionné et inclus dans le groupe de sécurité hello.
4. utilisateur de Hello a un abonnement Azure Active Directory Premium toothem.  
5. Hello périphérique a été redémarré et hello utilisateur s’est connecté après que Enterprise State Roaming a été activée.

## <a name="information-tooinclude-when-you-need-help"></a>Informations tooinclude lorsque vous avez besoin d’aide
Si vous ne pouvez pas résoudre votre problème avec instructions hello ci-dessous, vous pouvez contacter nos ingénieurs du support technique. Lorsque vous les contactez, il est recommandé de hello tooinclude informations suivantes :

- **Description générale de l’erreur de hello** : messages d’erreur vus par hello utilisateur ? Si aucun message d’erreur s’est produite, décrire hello remarqué, en détail un comportement inattendu. Quelles fonctionnalités sont activées pour la synchronisation et ce qu’il est utilisateur hello attendu toosync ? Sont plusieurs fonctionnalités ne synchronise pas ou est informatique isolé tooone ?
- **Utilisateurs affectés** : la synchronisation fonctionne/échoue-t-elle pour un ou plusieurs utilisateurs ? Combien d’appareils sont concernés par utilisateur ? Tous les appareils ne synchronisent-ils pas ou certains d’entre eux synchronisent-ils et d’autres non ?
- **Informations sur l’utilisateur de hello** – quel identité est utilisateur hello à l’aide de toolog dans toohello appareil ? Comment les utilisateurs hello se connecte toohello appareil ? Ils sont dans le cadre d’un groupe de sécurité sélectionné autorisé toosync ? 
- **Plus d’informations sur les appareils hello** : cet appareil joints à Azure AD ou à un domaine ? Génération est appareil de hello ? Quelles sont les dernières mises à jour de hello ?
- **Date / heure / fuseau horaire** : quel était hello date et heure précises, vous avez vu les erreur hello (inclure le fuseau horaire de hello) ?
- Ces informations nous aident à résoudre votre problème aussi rapidement que possible.

## <a name="troubleshooting-and-diagnosing-issues"></a>Résolution et diagnostic des problèmes
Cette section offre des suggestions sur la façon de tootroubleshoot et diagnostiquer les problèmes connexes tooEnterprise est itinérant de l’état.

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a>Vérifier la synchronisation et hello « Synchroniser vos paramètres » la page de paramètres 

1. Après avoir joint tooa de votre PC Windows 10 de domaine qui est configuré tooallow Enterprise State Roaming, ouverture de session avec votre compte professionnel. Accédez trop**paramètres** > **comptes** > **vos paramètres de synchronisation** et vérifiez que hello et la synchronisation des paramètres individuels et ce haut hello de page des paramètres Hello indique que vous synchronisez votre compte professionnel. Confirmer hello même compte est également utilisé en tant que votre compte de connexion dans **paramètres** > **comptes** > **votre Info**. 
2. Vérifiez que la synchronisation fonctionne sur plusieurs ordinateurs en apportant des modifications sur l’ordinateur d’origine hello, tels que le déplacement hello barre des tâches toohello côté droit ou supérieur de l’écran hello. Surveiller les modifications de hello propager toohello deuxième ordinateur dans les cinq minutes. 
 - Verrouillage et déverrouillage écran hello (Win + L) permettent de déclencher une synchronisation.
 - Vous devez utiliser hello même compte d’ouverture de session sur les deux ordinateurs pour la synchronisation toowork – Enterprise State Roaming est liée toohello compte d’utilisateur et de compte d’ordinateur hello pas.

**Problème potentiel**: page de paramètres hello a bascules hello grisées, et au lieu de voir un compte, vous constatez texte hello « certaines fonctionnalités de Windows sont disponibles uniquement si vous utilisez un compte Microsoft ou un compte professionnel ». Ce problème peut se produire pour les appareils qui ont été définies toobe appartenant au domaine et inscrit tooAzure AD, mais le périphérique de hello n’a pas été authentifié tooAzure AD. Il est possible que hello appareil stratégie doit être appliquée, mais que cette application se produit de façon asynchrone et peut être retardée de quelques heures. tooverify ce problème, suivez les étapes hello dans vérifier hello toocheck de statut d’inscription de périphérique hello cas.

### <a name="verify-hello-device-registration-status"></a>Vérifiez l’état de l’inscription de périphérique hello
Enterprise State Roaming nécessite hello appareil toobe est inscrit auprès d’Azure AD. Bien que non spécifique tooEnterprise State Roaming, suivant les instructions de hello ci-dessous peut aider à confirmer que hello Client de Windows 10 est inscrit et confirmer l’empreinte numérique, URL de paramètres d’Azure AD, NGC état et d’autres informations.

1.  Invite de commandes ouverte hello baisse des privilèges. toodo dans Windows, ouvrez hello Lanceur d’exécution (Win + R) et tapez « cmd » tooopen.
2.  Une fois que l’invite de commandes hello est ouvert, tapez «*dsregcmd.exe /status*».
3.  Pour la sortie attendue, hello **AzureAdJoined** valeur de champ doit être « YES », **WamDefaultSet** valeur de champ doit être « Oui » et hello **WamDefaultGUID** valeur de champ doit être un GUID avec « (organisation) » à la fin de hello.

**Problème potentiel**: **WamDefaultSet** et **AzureAdJoined** à la fois ont « Non » dans la valeur du champ hello, appareil de hello a été joint au domaine et inscrit auprès d’Azure AD et les appareils hello ne synchronisent pas. Si elle est affichée à cela, les appareil hello peuvent devez toowait pour toobe stratégie appliquée ou hello d’authentification pour appareil hello a échoué lors de la connexion tooAzure AD. utilisateur de Hello peut-être toowait quelques heures hello toobe de stratégie appliqués. Autres étapes de dépannage peuvent inclure une nouvelle tentative d’enregistrement automatique par tâche de hello et revenir dans, ou de signature lors du lancement du Planificateur de tâches. Dans certains cas, l’exécution de «*dsregcmd.exe /leave*» dans une fenêtre d’invite de commandes avec élévation de privilèges, un redémarrage et une nouvelle tentative d’inscription peuvent résoudre ce problème.


**Problème potentiel**: champ hello pour **AzureAdSettingsUrl** est vide et hello périphérique ne pas synchroniser. hello utilisateur peut avoir dernier connecté toohello périphérique avant l’activation de Enterprise State Roaming Bonjour Azure Active Portail de l’annuaire. Redémarrez l’appareil de hello et ont hello connexion d’utilisateur. Si vous le souhaitez, dans le portail hello, essayez d’avoir hello administrateur informatique, désactiver et réactiver les utilisateurs peuvent des paramètres de synchronisation et données d’application Enterprise. Une fois réactivé, redémarrage hello appareil et la connexion utilisateur hello. Si cela ne résout pas le problème de hello, **AzureAdSettingsUrl** peut être vide dans le cas de hello d’un certificat de périphérique incorrect. Dans ce cas, l’exécution de «*dsregcmd.exe /leave*» dans une fenêtre d’invite de commandes avec élévation de privilèges, un redémarrage et une nouvelle tentative d’inscription peuvent résoudre ce problème.

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>Enterprise State Roaming et authentification multifacteur 
Sous certaines conditions, la Enterprise State Roaming peut échouer toosync données si l’authentification multifacteur Azure est configurée. Pour plus d’informations sur ces problèmes, consultez le document de prise en charge hello [KB3193683](https://support.microsoft.com/kb/3193683). 

**Problème potentiel**: Si votre appareil est configuré toorequire multi-Factor Authentication sur le portail Azure Active Directory hello, toosync paramètres peuvent échouer lors de la signature de l’appareil tooa Windows 10 à l’aide d’un mot de passe. Ce type de configuration de l’authentification multifacteur est prévue tooprotect un compte d’administrateur Azure. Les utilisateurs administrateurs peuvent toujours être en mesure de toosync en vous connectant avec leurs Microsoft Passport, les appareils tootheir Windows 10 pour le code confidentiel de travail ou en effectuant l’authentification multifacteur lors de l’accès à d’autres services Azure tels qu’Office 365.

**Problème potentiel**: synchronisation peut échouer si hello administrateur configure la stratégie d’accès conditionnel hello Active Directory Federation Services l’authentification multifacteur et l’expiration du jeton d’accès hello sur l’appareil de hello. Assurez-vous de vous connecter et se déconnecter à l’aide de hello Microsoft Passport pour le code confidentiel de travail ou d’effectuer l’authentification multifacteur lors de l’accès à d’autres services Azure tels qu’Office 365.

###<a name="event-viewer"></a>Observateur d’événements
Pour procéder au dépannage, l’Observateur d’événements peut être utilisé toofind des erreurs spécifiques. Ceux-ci sont décrits dans le tableau hello ci-dessous. événements de Hello se trouve dans l’Observateur d’événements > journaux des Applications et Services > **Microsoft** > **Windows** > **SettingSync** et pour les problèmes liés à identité avec la synchronisation **Microsoft** > **Windows** > **AD Azure**.


## <a name="known-issues"></a>Problèmes connus

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>La synchronisation ne fonctionne pas sur les appareils contenant des applications chargées à l’aide de logiciels de gestion des appareils mobiles

A une incidence sur les appareils exécutant hello mise à jour de la date anniversaire Windows 10 (Version 1607). Dans l’Observateur d’événements sous journaux des SettingSync-Azure hello, hello 6013 d’ID d’événement avec l’erreur 80070259 est fréquent.

**Action recommandée**  
Assurez-vous que client de v1607 hello Windows 10 a hello 23 août 2016 mise à jour Cumulative ([KB3176934](https://support.microsoft.com/kb/3176934) 14393.82 de Build du système d’exploitation). 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>Les favoris Internet Explorer ne sont pas synchronisés

A une incidence sur les appareils exécutant hello mise à jour de novembre Windows 10 (Version 1511).

**Action recommandée**  
Assurez-vous que le client de v1511 hello Windows 10 a hello juillet 2016 mise à jour Cumulative ([KB3172985](https://support.microsoft.com/kb/3172985) 10586.494 de Build du système d’exploitation).

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>Le thème n’est pas synchronisé, ainsi que les données protégées avec Windows Information Protection 

tooprevent toute fuite de données, des données protégées avec [Protection des informations Windows](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) ne seront pas synchronisées via Enterprise State Roaming pour les appareils à l’aide de hello le mise à jour anniversaire Windows 10.



**Action recommandée**  
Aucune. TooWindows de futures mises à jour peut résoudre ce problème.

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>Les paramètres de date, d’heure et région ne sont pas synchronisés sur un appareil joint au domaine 
  
Les appareils qui sont joints au domaine ne subissent pas de synchronisation pour hello paramètre Date, Time et région : temps automatique. À l’aide de temps automatique peut override hello d’autres paramètres de Date et d’heure région et ces paramètres toosync pas. 

**Action recommandée**  
Aucune. 

---

### <a name="uac-prompts-when-syncing-passwords"></a>Invites UAC lors de la synchronisation des mots de passe

Affecte les appareils exécutant hello Windows 10 novembre mise à jour (Version 1511) avec une carte réseau sans fil est configuré toosync les mots de passe.

**Action recommandée**  
Assurez-vous que le client de v1511 hello Windows 10 a hello mise à jour Cumulative ([KB3140743](https://support.microsoft.com/kb/3140743) 10586.494 de Build du système d’exploitation).

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>La synchronisation ne fonctionne pas sur les appareils qui utilisent des cartes à puce pour la connexion
Si vous essayez de toosign dans tooyour périphérique de Windows à l’aide d’une carte à puce ou une carte à puce virtuelle, synchronisation des paramètres cessera de fonctionner.     

**Action recommandée**  
Aucune. TooWindows de futures mises à jour peut résoudre ce problème.

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>Un appareil joint au domaine n’est pas synchronisé après avoir quitté le réseau d’entreprise     
Les périphériques joints au domaine inscrit tooAzure QU'AD entraîner l’échec de la synchronisation si l’appareil de hello est hors site pendant de longues périodes de temps, et l’authentification de domaine ne peut pas terminer.

**Action recommandée**  
Connexion réseau d’entreprise de hello périphérique tooa afin que la synchronisation puisse reprendre.

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a>Azure pour appareils joints à AD n’est pas la synchronisation et l’utilisateur de hello a un nom d’utilisateur Principal de casse mixte.
 Si l’utilisateur de hello a une casse mixte UPN (par exemple, nom d’utilisateur au lieu du nom d’utilisateur) et utilisateur de hello est sur un appareil joints à Azure AD qui a mis à niveau à partir de Windows 10 Build 10586 too14393, appareil de l’utilisateur hello peut échouer toosync. 

**Action recommandée**  
utilisateur de Hello devez toounjoin et rejoindre hello appareil toohello cloud. toodo, connectez-vous en tant qu’utilisateur d’administrateur Local hello et disjoindre l’appareil de hello en accédant trop**paramètres** > **système** > **sur** et sélectionnez » Gérer ou vous déconnecter de l’entreprise ou école ». Nettoyer les fichiers hello ci-dessous, puis sur Azure AD Join hello appareil à nouveau dans **paramètres** > **système** > **sur** et en sélectionnant « se connecter tooWork ou scolaire ». Continuer toojoin hello appareil tooAzure Active Directory et les flux hello terminée.

À l’étape de nettoyage hello, hello nettoyage fichiers suivants :
- Settings.dat dans `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`
- Tous les fichiers hello sous le dossier de hello`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>ID d’événement 6065:80070533 Cet utilisateur ne peut pas se connecter car ce compte est actuellement désactivé  
Dans l’Observateur d’événements sous journaux des hello SettingSync/Debug, cette erreur peut apparaître lorsque les informations d’identification de l’utilisateur hello ont expiré. En outre, il peut se produire lorsque le client de hello n’avait pas automatiquement AzureRMS configuré. 

**Action recommandée**  
Dans le premier cas de hello, hello utilisateur être mise à jour leurs informations d’identification et l’appareil de toohello de connexion avec les nouvelles informations d’identification de hello. toosolve hello AzureRMS problème, effectuez les étapes hello répertoriés dans [KB3193791](https://support.microsoft.com/kb/3193791). 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>ID d’événement 1098 : Erreur : Échec de l’opération de service Broker de jeton 0xCAA5001C  
Dans l’Observateur d’événements sous journaux d’AAD/Operational hello, cette erreur peut se produire avec les événements 1104 : appel de plug-in AAD Cloud PA obtenir un jeton a retourné l’erreur : 0xC000005F. Ce problème se produit si des autorisations ou des attributs de propriété sont manquants.    

**Action recommandée**  
Effectuez les étapes hello répertoriés [KB3196528](https://support.microsoft.com/kb/3196528).  



## <a name="next-steps"></a>Étapes suivantes

- Hello d’utilisation [forum vocal des utilisateurs](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) tooprovide des commentaires et apporter des suggestions sur comment tooimprove Enterprise état itinérant.

- Pour plus d’informations, consultez hello [présentation d’Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md). 

## <a name="related-topics"></a>Rubriques connexes
* [Présentation d’Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Activer Enterprise State Roaming dans Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [FAQ sur l’itinérance des paramètres et des données](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Paramètres de stratégie de groupe et de MDM pour la synchronisation des paramètres](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Référence des paramètres d’itinérance Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
