---
title: aaaEnable Microsoft Windows Hello for Business dans votre organisation | Documents Microsoft
description: "Tooenable d’instructions de déploiement Microsoft Passport de votre organisation."
services: active-directory
documentationcenter: 
keywords: "configurer le déploiement Microsoft Passport, Microsoft Windows Hello Entreprise"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a>Activer Microsoft Windows Hello Entreprise dans votre organisation
Après avoir [connecter les appareils Windows 10 joints à un domaine avec Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), hello suivant tooenable Microsoft Windows Hello for Business dans votre organisation :

1. Déployer System Center Configuration Manager  
2. Configuration des paramètres de stratégie
3. Configurer le profil de certificat hello  

## <a name="deploy-system-center-configuration-manager"></a>Déployer System Center Configuration Manager
certificats d’utilisateur toodeploy basés sur Windows Hello pour les clés de l’entreprise, hello éléments suivants sont nécessaires :

* **Branche actuelle de System Center Configuration Manager** -vous devez tooinstall version 1606 ou supérieures. Pour plus d’informations, consultez hello [Documentation pour System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) et [Blog de l’équipe System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).
* **Infrastructure à clé publique (PKI)** -tooenable Microsoft Windows Hello for Business à l’aide de certificats utilisateur, vous devez disposer d’une infrastructure à clé publique en place. Si vous n’en avez pas, ou si vous ne souhaitez pas toouse il pour les certificats utilisateur, vous pouvez déployer un nouveau contrôleur de domaine qui a Windows Server 2016 générer 10551 (ou plus) est installé. Suivez les étapes de hello trop[installer un contrôleur de domaine réplica dans un domaine existant](https://technet.microsoft.com/library/jj574134.aspx) ou trop[installer une nouvelle forêt Active Directory, si vous créez un nouvel environnement](https://technet.microsoft.com/library/jj574166). (hello ISOs sont disponibles pour téléchargement sur [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)

## <a name="configure-policy-settings"></a>Configuration des paramètres de stratégie
tooconfigure hello Microsoft Windows Hello pour les paramètres de stratégie d’entreprise, vous avez deux options :

* Stratégie de groupe dans Active Directory 
* Hello System Center Configuration Manager 

La stratégie de groupe dans Active Directory est hello recommandé méthode tooconfigure Microsoft Windows Hello pour les paramètres de stratégie d’entreprise. 

À l’aide de System Center Configuration Manager d’est la méthode hello préféré lorsque vous l’utilisez également les certificats toodeploy. Ce scénario :

* Garantit la compatibilité avec les scénarios de déploiement plus récente hello
* Requiert côté hello client Windows 10 Version 1607 ou plus.

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a>Configurer Microsoft Windows Hello Entreprise via la stratégie de groupe dans Active Directory
**Étapes** :

1. Ouvrez le Gestionnaire de serveur, puis accédez trop**outils** > **gestion des stratégies de groupe**.
2. À partir de la gestion des stratégies de groupe, accédez à nœud de domaine toohello correspondant domaine toohello dans lequel vous souhaitez tooenable Azure AD Join.
3. Cliquez avec le bouton droit sur **Objets de stratégie de groupe** et sélectionnez **Nouveau**. Donnez un nom à votre objet de stratégie de groupe, par exemple Activer Windows Hello Entreprise. Cliquez sur **OK**.
4. Cliquez avec le bouton droit sur votre nouvel objet de stratégie de groupe, puis sélectionnez **Modifier**.
5. Accédez trop**Configuration ordinateur** > **stratégies** > **modèles d’administration** > **Windows Composants** > **Windows Hello for Business**.
6. Avec le bouton droit, cliquez sur **Activer Windows Hello Entreprise**, puis sélectionnez **Modifier**.
7. Sélectionnez hello **activé** case d’option, puis cliquez sur **appliquer**. Cliquez sur **OK**.
8. Vous pouvez maintenant lier emplacement de tooa hello objet stratégie de groupe de votre choix. tooenable cette stratégie pour tous les appareils Windows 10 de hello appartenant au domaine dans votre organisation, domaine toohello de lien hello stratégie de groupe. Par exemple :
   * Une unité d’organisation spécifique dans Active Directory où les ordinateurs Windows 10 joints au domaine seront situés
   * Un groupe de sécurité spécifique contenant des ordinateurs Windows 10 joints au domaine qui sera inscrit automatiquement auprès d’Azure AD

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a>Configurer Windows Hello Entreprise à l’aide de System Center Configuration Manager
**Étapes** :

1. Ouvrez hello **System Center Configuration Manager**, puis accédez trop**biens et conformité > Paramètres de compatibilité > accès aux ressources d’entreprise > Windows Hello pour les profils d’entreprise**.
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. Dans la barre d’outils de hello en haut de hello, cliquez sur **créer Windows Hello entreprise profil**.
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. Sur hello **général** boîte de dialogue, effectuer hello comme suit :
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    a. Bonjour **nom** zone de texte, tapez un nom pour votre profil, par exemple, **mon profil WHfB**.
   
    b. Cliquez sur **Suivant**.
4. Sur hello **prise en charge de plates-formes** boîte de dialogue, les plateformes hello select qui seront préparées avec ce Windows Hello pour le profil d’entreprise, puis cliquez sur **suivant**.
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. Sur hello **paramètres** boîte de dialogue, effectuer hello comme suit :
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    a. Pour **Configurer Windows Hello Entreprise**, sélectionnez **Activé**.
   
    b. Pour **Utiliser un module de plateforme sécurisée (TPM)**, sélectionnez **Obligatoire**. 
   
    c. En tant que **Méthode d’authentification**, sélectionnez **Basée sur un certificat**.
   
    d. Cliquez sur **Suivant**.
6. Sur hello **Résumé** boîte de dialogue, cliquez sur **suivant**.
7. Sur hello **achèvement** boîte de dialogue, cliquez sur **fermer**.
8. Dans la barre d’outils de hello en haut de hello, cliquez sur **déployer**.
   
    ![Configurer Windows Hello Entreprise](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a>Configurer le profil de certificat hello
Si vous utilisez l’authentification par certificat pour l’authentification locale, vous devez tooconfigure et déployez un profil de certificat. Cette tâche nécessite tooset un serveur NDES et le rôle de site de Point d’enregistrement de certificat dans hello System Center Configuration Manager. Pour plus d’informations, consultez hello [conditions préalables pour les profils de certificat dans Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).

1. Ouvrez hello **System Center Configuration Manager**, puis accédez trop**biens et conformité > Paramètres de compatibilité > accès aux ressources d’entreprise > profils de certificat**.
2. Sélectionnez un modèle qui dispose d’une ouverture de session avec carte à puce EKU.

Sur hello **inscription SCEP** page hello profil de certificat, vous devez toochoose **installer tooPassport pour travail sinon mettre en échec** comme hello **Key Storage Provider**.

## <a name="next-steps"></a>Étapes suivantes
* [Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Authentification des identités sans mot de passe avec Microsoft Passport](active-directory-azureadjoin-passport.md)
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)

