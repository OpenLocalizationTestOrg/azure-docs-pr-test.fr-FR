---
title: "aaaConfigure sécurisé LDAP (LDAPS) dans les Services de domaine Active Directory de Azure | Documents Microsoft"
description: "Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine géré par les services de domaine Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services

## <a name="before-you-begin"></a>Avant de commencer
Vérifiez que vous avez accompli la [Tâche 1 : Obtenir un certificat pour le protocole LDAP sécurisé](active-directory-ds-admin-guide-configure-secure-ldap.md).


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>Tâche 2 : exporter hello tooa du certificat LDAP sécurisé. Fichier PFX
Avant de commencer cette tâche, assurez-vous que vous avez obtenu le certificat LDAP sécurisé de hello à partir d’une autorité de certification publique ou que vous avez créé un certificat auto-signé.

Effectuer hello comme suit, tooexport hello LDAPS certificat tooa. Fichier PFX.

1. Hello de presse **Démarrer** et tapez **R**. Bonjour **exécuter** boîte de dialogue, tapez **mmc** et cliquez sur **OK**.

    ![Lancer la console MMC de hello](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. Sur hello **contrôle de compte d’utilisateur** invite, cliquez sur **Oui** toolaunch MMC (Microsoft Management Console) en tant qu’administrateur.
3. À partir de hello **fichier** menu, cliquez sur **ajouter/supprimer un composant logiciel enfichable...** .

    ![Ajout de la console de composant logiciel enfichable tooMMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. Bonjour **ajouter ou supprimer des composants logiciel enfichables** boîte de dialogue, sélectionnez hello **certificats** -composant logiciel enfichable, cliquez sur hello **Ajouter >** bouton.

    ![Ajout de la console de tooMMC du composant logiciel enfichable Certificats](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. Bonjour **enfichable Certificats** Assistant, sélectionnez **compte d’ordinateur** et cliquez sur **suivant**.

    ![Ajouter le composant logiciel enfichable Certificats pour le compte d’ordinateur](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. Sur hello **sélectionner un ordinateur** , sélectionnez **ordinateur Local : (hello ordinateur cette console s’exécute)** et cliquez sur **Terminer**.

    ![Ajouter le composant logiciel enfichable Certificats - Sélection de l’ordinateur](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. Bonjour **ajouter ou supprimer des composants logiciel enfichables** boîte de dialogue, cliquez sur **OK** tooadd hello certificats enfichable tooMMC.

    ![Ajouter des certificats enfichable tooMMC - terminé](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. Dans la fenêtre de console MMC hello, cliquez sur tooexpand **racine de la Console**. Vous devez voir hello le composant logiciel enfichable Certificats chargé. Cliquez sur **certificats (ordinateur Local)** tooexpand. Cliquez sur tooexpand hello **personnel** nœud, suivie de hello **certificats** nœud.

    ![Banque de certificats personnels ouverte](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. Vous devez voir hello un certificat auto-signé, nous avons créé. Vous pouvez examiner les propriétés de hello de hello certificat tooensure hello empreinte correspond à celui indiqué sur windows PowerShell de hello lorsque vous avez créé le certificat de hello.
10. Sélectionnez hello certificat auto-signé et **bouton droit sur**. Dans le menu contextuel hello, sélectionnez **toutes les tâches** et sélectionnez **exporter...** .

    ![Exportation du certificat](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. Bonjour **Assistant Exportation de certificat**, cliquez sur **suivant**.

    ![Assistant Exportation de certificat](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. Sur hello **exporter la clé privée** page, sélectionnez **Oui, exporter la clé privée de hello**, puis cliquez sur **suivant**.

    ![Exportation du certificat - Clé privée](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > Vous devez exporter la clé privée de hello en même temps que le certificat de hello. Si vous fournissez un PFX qui ne contient pas de clé privée de hello pour le certificat de hello, l’activation de LDAP sécurisé pour votre domaine géré échoue.
    >
    >
13. Sur hello **Format de fichier d’exportation** page, sélectionnez **échange d’informations personnelles - PKCS #12 (. PFX)** en tant que format de fichier hello pour hello exportées de certificat.

    ![Exportation du certificat - Format de fichier](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Uniquement hello. Format de fichier PFX est pris en charge. Ne pas exporter hello certificat toohello. Format du fichier CER.
    >
    >
14. Sur hello **sécurité** page, sélectionnez hello **mot de passe** option et tapez un Bonjour tooprotect de mot de passe. Fichier PFX. N’oubliez pas ce mot de passe, car il est nécessaire dans la tâche suivante hello. Cliquez sur **suivant** tooproceed.

    ![Exportation du certificat - Mot de passe ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > Notez ce mot de passe. Vous en avez besoin lors de l’activation de LDAP sécurisé pour ce domaine géré dans [tâche 3 : activer LDAP sécurisé pour le domaine géré de hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. Sur hello **fichier tooExport** , spécifiez le nom de fichier hello et l’emplacement où vous souhaitez que le certificat de hello tooexport.

    ![Exportation du certificat - Chemin d’accès](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. Dans hello suivant page, cliquez sur **Terminer** le fichier PFX tooa tooexport hello certificat. Vous devez voir la boîte de dialogue de confirmation lorsque hello certificat a été exporté.

    ![Exportation du certificat - Terminé](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>Étape suivante
[Tâche 3 : activer LDAP sécurisé pour le domaine géré de hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
