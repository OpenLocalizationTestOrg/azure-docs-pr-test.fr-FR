---
title: "Azure Active Directory Domain Services : déployer le Proxy d’application Azure Active Directory | Microsoft Docs"
description: "Utiliser le proxy d'application sur les domaines managés par les Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>Déployer le proxy d'application sur un domaine managé par les Azure Active Directory Domain Services
Proxy d’Application Azure Active Directory (AD) vous permet de prendre en charge des travailleurs à distance en publiant toobe d’applications local accédé via hello internet. Avec les Services de domaine Active Directory de Azure, vous pouvez maintenant finesse-et-MAJ les applications héritées des Services d’Infrastructure sur site tooAzure en cours d’exécution. Vous pouvez ensuite publier ces applications à l’aide de hello Proxy d’Application Azure AD, toousers d’accès à distance sécurisé tooprovide dans votre organisation.

Si vous êtes toohello nouveau Proxy d’Application Azure AD, en savoir plus sur cette fonctionnalité avec hello l’article suivant : [comment tooprovide sécuriser l’accès à distance, applications locales tooon](../active-directory/active-directory-application-proxy-get-started.md).


## <a name="before-you-begin"></a>Avant de commencer
tâches de hello tooperform répertoriées dans cet article, vous devez :

1. Un **abonnement Azure**valide.
2. Un **répertoire Azure AD** , synchronisé avec un répertoire local ou un répertoire cloud uniquement.
3. Un **licence Azure AD Basic ou Premium** est requis toouse hello Proxy d’Application Azure AD.
4. **Les Services de domaine Active Directory Azure** doit être activée pour le répertoire de hello Azure AD. Si vous n’avez pas encore fait, suivez toutes les tâches de hello présentées dans hello [guide Mise en route](active-directory-ds-getting-started.md).

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>Tâche 1 : activer le proxy d’application Azure AD pour votre annuaire Azure AD
Effectuer hello suivant les étapes tooenable hello Proxy d’Application Azure AD de votre annuaire Azure AD.

1. Connectez-vous en tant qu’administrateur Bonjour [portail Azure](http://portal.azure.com).

2. Cliquez sur **Azure Active Directory** toobring de vue d’ensemble de hello active. Cliquez sur **Applications d’entreprise**.

    ![Sélectionnez un annuaire Azure AD.](./media/app-proxy/app-proxy-enable-start.png)
3. Cliquez sur **Proxy d’application**. Si vous n’avez pas un abonnement Azure AD Basic ou Azure AD Premium, vous consultez un tooenable option une version d’évaluation. Activer/désactiver **activer le Proxy d’Application ?** trop**activer** et cliquez sur **enregistrer**.

    ![Activer le Proxy d’application](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload hello connecteur, cliquez sur hello **connecteur** bouton.

    ![Télécharger le connecteur](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. Sur la page de téléchargement de hello, acceptez les termes du contrat de licence hello et accord de confidentialité, puis cliquez sur hello **télécharger** bouton.

    ![Confirmer le téléchargement](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>Tâche 2 : configurer appartenant au domaine Windows serveurs toodeploy hello Azure AD le Proxy d’Application connecteur
Vous devez appartenant au domaine de machines virtuelles Windows Server sur lequel vous pouvez installer le connecteur de Proxy d’Application Azure AD hello. Selon les applications hello en cours de publication, vous pouvez choisir tooprovision plusieurs serveurs sur lequel le connecteur de hello est installé. Cette option de déploiement vous donne une plus grande disponibilité et vous permet de traiter des charges d’authentification plus importantes.

Configurer les serveurs du connecteur hello sur hello même réseau virtuel (ou un réseau virtuel connecté/homologuer), dans lequel vous avez activé votre domaine géré des Services de domaine Active Directory de Azure. De même, les serveurs de hello hébergement d’applications hello vous publiez via le Proxy d’Application de hello doivent toobe installé sur hello même réseau virtuel Azure.

serveurs du connecteur tooprovision, suivez les tâches de hello décrites dans l’article hello intitulé [joindre un domaine géré du tooa d’ordinateur virtuel Windows](active-directory-ds-admin-guide-join-windows-vm.md).


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>Tâche 3 : installer et inscrire hello connecteur Proxy d’Application Azure AD
Auparavant, vous configuré une machine virtuelle Windows Server et il joint le domaine géré de toohello. Dans cette tâche, vous installerez le connecteur de Proxy d’Application Azure AD hello sur cet ordinateur virtuel.

1. Copie hello connecteur installation package toohello ordinateur virtuel sur lequel vous installez le connecteur de Proxy d’Application Azure AD Web hello.

2. Exécutez **AADApplicationProxyConnectorInstaller.exe** sur l’ordinateur virtuel de hello. Accepter les termes du contrat de licence de logiciel hello.

    ![Accepter les termes du contrat pour l’installation](./media/app-proxy/app-proxy-install-connector-terms.png)
3. Pendant l’installation, vous êtes tooregister demandées hello connecteur hello Proxy d’Application de votre annuaire Azure AD.
    * Fournissez vos **informations d’identification d’administrateur général d’Azure AD**. Votre client d’administrateur global peut être différent de vos informations d’identification Microsoft Azure.
    * Hello administrateur compte utilisé tooregister hello connecteur doit appartenir toohello même répertoire où vous avez activé le service de Proxy d’Application hello. Par exemple, si le domaine du locataire hello est contoso.com, hello admin doit être admin@contoso.com ou tout autre alias valide dans ce domaine.
    * Si la Configuration de sécurité renforcée d’Internet Explorer est activée pour le serveur de hello où vous installez le connecteur de hello, l’écran d’enregistrement hello peut-être être bloqué. accès tooallow, suivez les instructions dans le message d’erreur hello hello. Vérifiez que la configuration de sécurité renforcée d’Internet Explore est désactivée.
    * Si l’inscription du connecteur n’aboutit pas, voir [Résoudre les problèmes du proxy d’application](../active-directory/active-directory-application-proxy-troubleshoot.md).

    ![Connecteur installé](./media/app-proxy/app-proxy-connector-installed.png)
4. tooensure hello connecteur fonctionne correctement, exécution hello Azure AD Application Proxy Connector de résolution des problèmes. Vous devez voir un rapport réussies après la résolution des problèmes de hello en cours d’exécution.

    ![Réussite de l'utilitaire de résolution des problèmes](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. Vous devez voir connecteur hello qui vient d’être installé sur la page de proxy d’Application hello dans votre annuaire Azure AD.

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> Vous pouvez choisir les connecteurs tooinstall sur plusieurs serveurs tooguarantee haute disponibilité pour l’authentification des applications publiées via hello Proxy d’Application Azure AD. Effectuer hello mêmes étapes répertoriées ci-dessus connecteur hello tooinstall autre domaine géré tooyour jointes de serveurs.
>
>

## <a name="next-steps"></a>Étapes suivantes
Vous avez configuré hello Proxy d’Application Azure AD et intégrant à votre domaine géré des Services de domaine Active Directory de Azure.

* **Migrer vos ordinateurs virtuels de tooAzure applications :** vous pouvez de courbes d’élévation et MAJ local serveurs tooAzure virtuels tooyour joint à un domaine géré de vos applications. Cela vous permet de vous débarrasser des coûts d’infrastructure hello de l’exécution de serveurs locaux.

* **Publier des applications à l’aide du Proxy d’Application Azure AD :** publier des applications en cours d’exécution sur vos machines virtuelles Azure à l’aide de hello Proxy d’Application Azure AD. Pour plus d'informations, consultez [Publier des applications avec le proxy d'application Azure AD](../active-directory/application-proxy-publish-azure-portal.md)


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>Remarque relative au déploiement - Publier des applications IWA (authentification Windows intégrée) à l’aide du proxy d’application Azure AD
Activer les applications tooyour de l’authentification unique à l’aide de l’authentification Windows (intégrée) en accordant l’autorisation de connecteur de Proxy d’Application tooimpersonate utilisateurs et envoyer et recevoir des jetons en leur nom. Configurer la délégation contrainte kerberos (KCD) pour les ressources tooaccess hello connecteur toogrant hello requis des autorisations sur un domaine géré de hello. Utiliser le mécanisme KCD hello basée sur la ressource sur des domaines gérés pour renforcer la sécurité.


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>Activer basée sur une ressource de la délégation contrainte kerberos pour le connecteur de Proxy d’Application hello Azure AD
connecteur de Proxy d’Application Azure Hello doit être configuré pour la délégation kerberos contrainte (KCD), afin qu’il peut emprunter l’identité des utilisateurs sur le domaine géré de hello. Sur un domaine managé Azure AD Domain Services, vous n’avez pas les privilèges d’administrateur de domaine. Par conséquent, **la KCD traditionnelle au niveau des comptes ne peut pas être configurée sur un domaine managé**.

Utilisez plutôt la KCD basée sur la ressource, comme décrit dans cet [article](active-directory-ds-enable-kcd.md).

> [!NOTE]
> Vous devez toobe un membre du groupe « Administrateurs de contrôleur de domaine AAD » de hello, tooadminister hello gérés domaine à l’aide des applets de commande PowerShell d’Active Directory.
>
>

Utiliser les paramètres hello tooretrieve hello PowerShell de Get-ADComputer applet de commande pour ordinateur de hello sur le Proxy d’Application Azure AD hello connecteur est installé.
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

Par la suite, utilisez tooset d’applet de commande hello Set-ADComputer de KCD de ressources pour serveur de ressources hello.
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

Si vous avez déployé plusieurs connecteurs de Proxy d’Application sur votre domaine géré, vous devez tooconfigure basée sur la ressource KCD pour chacune de ces instances connecteur.


## <a name="related-content"></a>Contenu connexe
* [Services de domaine Azure AD : guide de prise en main](active-directory-ds-getting-started.md)
* [Configurer la délégation Kerberos contrainte sur un domaine managé](active-directory-ds-enable-kcd.md)
* [Présentation de la délégation Kerberos contrainte](https://technet.microsoft.com/library/jj553400.aspx)
