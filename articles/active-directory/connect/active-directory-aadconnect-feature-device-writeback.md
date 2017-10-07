---
title: "Azure AD Connect : Activation de l’écriture différée des appareils | Microsoft Docs"
description: "Ce document comment les détails de l’écriture différée de l’appareil tooenable à l’aide d’Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect : Activation de l’écriture différée des appareils
> [!NOTE]
> Un tooAzure abonnement Premium d’Active Directory est requis pour l’écriture différée de l’appareil.
> 
> 

Hello suivant documentation fournit des informations sur la façon dont l’écriture différée des appareils tooenable hello fonctionnalité dans Azure AD Connect. L’écriture différée de l’appareil est utilisée dans hello les scénarios suivants :

* Activer l’accès conditionnel basé sur les appareils tooADFS (2012 R2 ou version ultérieure) protégé par des applications (de confiance).

Cela offre une sécurité supplémentaire et assurance que tooapplications d’accès est accordé uniquement les appareils de tootrusted. Pour plus d’informations sur l’accès conditionnel, consultez [Gestion des risques avec accès conditionnel](../active-directory-conditional-access.md) et [Configuration d’un accès conditionnel en local à l’aide du service d’inscription d’appareils Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).

> [!IMPORTANT]
> <li>Les appareils doivent se trouver dans hello de la même forêt en tant qu’utilisateurs de hello. Étant donné que les appareils doivent être réécrites tooa une seule forêt, cette fonctionnalité ne prend pas en charge un déploiement à plusieurs forêts de l’utilisateur.</li>
> <li>Objet de configuration qu’un périphérique d’enregistrement peut être ajouté forêt d’Active Directory toohello local. Cette fonctionnalité n’est pas compatible avec une topologie où hello locale Active Directory est synchronisé toomultiple Azure AD répertoires.</li>> 

## <a name="part-1-install-azure-ad-connect"></a>1re partie : Installer Azure AD Connect
1. Installez Azure AD Connect à l’aide de paramètres personnalisés ou Express. Microsoft vous recommande de toostart avec tous les utilisateurs et groupes ont bien été synchronisées avant d’activer l’écriture différée de l’appareil.

## <a name="part-2-prepare-active-directory"></a>Partie 2 : Préparer Active Directory
Utilisez hello suivant tooprepare étapes pour l’utilisation de l’écriture différée de l’appareil.

1. À partir de l’ordinateur hello sur lequel est installé Azure AD Connect, lancez PowerShell avec élévation de privilèges.
2. Si le module d’Active Directory PowerShell hello n’est pas installé, installer à l’aide de hello de commande suivante :
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. Si le module d’Azure Active Directory PowerShell hello n’est pas installé, puis télécharger et l’installer à partir de [Azure Module Active Directory pour Windows PowerShell (version 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297). Ce composant a une dépendance sur hello-assistant de connexion, qui est installé avec Azure AD Connect.
4. Avec l’identification d’administrateur d’entreprise, exécutez hello suivant de commandes, puis quittez PowerShell.
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

Identification d’administrateur d’entreprise est nécessaires, car l’espace de noms de modifications toohello configuration sont nécessaires. Un administrateur de domaine ne dispose pas des autorisations suffisantes.

![Powershell pour l’activation de l’écriture différée des appareils](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

Description :

* Si elles n’existent pas, des conteneurs et des objets sont créés et configurés sous CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].
* Si elles existent, des conteneurs et des objets sont créés et configurés sous CN=RegisteredDevices,[domain-dn]. Les objets d’appareil seront créés dans ce conteneur.
* Définit les autorisations nécessaires sur hello compte du connecteur Azure AD, appareils toomanage sur votre annuaire Active Directory.
* Ne doit toorun sur une forêt, même si Azure AD Connect est installé sur plusieurs forêts.

Paramètres :

* DomainName : domaine Active Directory où les objets d’appareil seront créés. Remarque : tous les appareils pour une forêt Active Directory donnée seront créés dans un domaine unique.
* AdConnectorAccount : Compte Active Directory qui sera utilisé par les objets Azure AD Connect toomanage dans le répertoire de hello. Il s’agit de compte hello utilisé par Azure AD Connect synchronisation tooconnect tooAD. Si vous avez installé à l’aide de la configuration rapide, il est compte hello précédé MSOL_.

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>3ème partie : Activer l’écriture différée des appareils dans Azure AD Connect
Utilisez hello suivant la procédure tooenable périphérique l’écriture différée dans Azure AD Connect.

1. Réexécutez l’Assistant installation de hello. Sélectionnez **personnaliser les options de synchronisation** hello des tâches supplémentaires de page, puis cliquez sur **suivant**.
   ![Installation personnalisée - Personnaliser les options de synchronisation](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. Dans la page de fonctionnalités facultatives de hello, l’écriture différée de l’appareil sera n’est plus grisée. Veuillez noter que les étapes de préparation Azure AD Connect ne sont pas terminées si hello l’écriture différée de l’appareil sera grisée dans la page des fonctionnalités facultatives hello. Cochez la case hello pour l’écriture différée de l’appareil, cliquez sur **suivant**. Si la case à cocher hello est toujours désactivé, consultez hello [section Dépannage](#the-writeback-checkbox-is-still-disabled).
   ![Installation personnalisée - Fonctionnalités facultatives de l’écriture différée des appareils](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. Sur la page de l’écriture différée de hello, vous verrez le domaine de hello fourni forêt de l’écriture différée appareil hello par défaut.
   ![Installation personnalisée - Forêt cible de l’écriture différée des appareils](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. Terminer l’installation de hello Hello Assistant sans aucune modification de configuration supplémentaire. Si nécessaire, consultez trop[installation personnalisée d’Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>Activer l’accès conditionnel
Tooenable obtenir des instructions détaillées ce scénario sont disponibles dans [configuration d’accès conditionnel en local à l’aide d’Azure Active Directory Device Registration](../active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>Vérifiez que les appareils sont synchronisé tooActive Active
L’écriture différée des appareils doit désormais fonctionner correctement. N’oubliez pas qu’il peut prendre jusqu'à heures too3 pour appareil objets toobe réécriture tooAD.  tooverify que vos appareils sont en cours de synchronisation correctement, procédez comme hello suivant après que les règles de synchronisation hello terminé :

1. Lancez le Centre d’administration Active Directory.
2. Développez RegisteredDevices, au sein de hello domaine fédéré en cours.
   ![Active Directory - Appareils inscrits au Centre d’administration](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. Les appareils enregistrés actuels sont répertoriés à cet emplacement.
   ![Active Directory - Liste des appareils inscrits au Centre d’administration](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>Résolution des problèmes
### <a name="hello-writeback-checkbox-is-still-disabled"></a>case à cocher de l’écriture différée Hello est toujours désactivé.
Si la case à cocher hello pour l’écriture différée de l’appareil n’est pas activée même si vous avez suivi les étapes de hello ci-dessus, hello suit vous guide via l’installation hello Assistant consiste à vérifier avant de hello est activée.

Commençons par le début :

* Assurez-vous qu'au moins une forêt a Windows Server 2012R2. type d’objet périphérique Hello doit être présent.
* Si l’Assistant installation hello est déjà en cours d’exécution, toutes les modifications ne seront pas détectées. Dans ce cas, terminez l’Assistant installation hello et exécutez-le à nouveau.
* Assurez-vous que le compte hello que vous fournissez dans le script d’initialisation hello est réellement hello correct utilisateur utilisé par hello connecteur Active Directory. tooverify, procédez comme suit :
  * À partir du menu Démarrer de hello, ouvrez **Service de synchronisation**.
  * Ouvrez hello **connecteurs** onglet.
  * Recherche hello connecteur avec type de Services de domaine Active Directory et sélectionnez-le.
  * Sous **Actions**, sélectionnez **Propriétés**.
  * Accédez trop**connecter tooActive Directory forêt**. Vérifiez que hello domaine et nom d’utilisateur spécifié sur ce script de toohello écran correspondance hello compte fourni.
    ![Compte de connecteur dans Sync Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

Vérifiez la configuration dans Active Directory :

* Vérifiez que hello Device Registration Service se trouve dans un emplacement hello ci-dessous (CN = DeviceRegistrationService, CN = Services d’inscription de périphérique, CN = Device Registration Configuration, CN = Services, CN = Configuration) sous le contexte d’appellation de configuration.

![Résoudre les problèmes, DeviceRegistrationService dans l’espace de noms de configuration](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* Vérifiez qu’un seul objet de configuration en recherchant l’espace de noms de configuration hello. S’il en existe plusieurs, supprimez hello.

![Résoudre les problèmes, recherchez les objets dupliqués hello](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* Sur l’objet de Service d’inscription de périphérique hello, assurez-vous que hello attribut msDS-DeviceLocation est présent et a une valeur. Recherche de cet emplacement et l’Assurez-vous qu’il est présent avec hello objectType msDS-DeviceContainer.

![Résoudre les problèmes, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Résoudre les problèmes, classe d’objet RegisteredDevices](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* Vérifier le compte de hello utilisé par hello que connecteur Active Directory a les autorisations requises sur conteneur de périphériques inscrits hello trouvé par l’étape précédente de hello. Il s’agit d’autorisations hello attendu sur ce conteneur :

![Résoudre les problèmes, vérifier les autorisations du conteneur](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* Vérifiez hello compte Active Directory dispose des autorisations sur hello CN = Device Registration Configuration, CN = Services, CN = l’objet de Configuration.

![Résoudre les problèmes, vérifier les autorisations de la configuration de l’inscription des appareils](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>Informations supplémentaires
* [Gestion des risques avec accès conditionnel](../active-directory-conditional-access.md)
* [Configuration d’un accès conditionnel en local à l’aide du service d’inscription d’appareils Azure Active Directory](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

