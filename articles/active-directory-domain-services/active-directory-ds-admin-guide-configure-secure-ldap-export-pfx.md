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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="e81fb-103">Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="e81fb-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e81fb-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e81fb-104">Before you begin</span></span>
<span data-ttu-id="e81fb-105">Vérifiez que vous avez accompli la [Tâche 1 : Obtenir un certificat pour le protocole LDAP sécurisé](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="e81fb-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="e81fb-106">Tâche 2 : exporter hello tooa du certificat LDAP sécurisé. Fichier PFX</span><span class="sxs-lookup"><span data-stu-id="e81fb-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="e81fb-107">Avant de commencer cette tâche, assurez-vous que vous avez obtenu le certificat LDAP sécurisé de hello à partir d’une autorité de certification publique ou que vous avez créé un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="e81fb-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="e81fb-108">Effectuer hello comme suit, tooexport hello LDAPS certificat tooa. Fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="e81fb-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="e81fb-109">Hello de presse **Démarrer** et tapez **R**. Bonjour **exécuter** boîte de dialogue, tapez **mmc** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e81fb-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Lancer la console MMC de hello](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="e81fb-111">Sur hello **contrôle de compte d’utilisateur** invite, cliquez sur **Oui** toolaunch MMC (Microsoft Management Console) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e81fb-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="e81fb-112">À partir de hello **fichier** menu, cliquez sur **ajouter/supprimer un composant logiciel enfichable...** .</span><span class="sxs-lookup"><span data-stu-id="e81fb-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Ajout de la console de composant logiciel enfichable tooMMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="e81fb-114">Bonjour **ajouter ou supprimer des composants logiciel enfichables** boîte de dialogue, sélectionnez hello **certificats** -composant logiciel enfichable, cliquez sur hello **Ajouter >** bouton.</span><span class="sxs-lookup"><span data-stu-id="e81fb-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![Ajout de la console de tooMMC du composant logiciel enfichable Certificats](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="e81fb-116">Bonjour **enfichable Certificats** Assistant, sélectionnez **compte d’ordinateur** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e81fb-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Ajouter le composant logiciel enfichable Certificats pour le compte d’ordinateur](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="e81fb-118">Sur hello **sélectionner un ordinateur** , sélectionnez **ordinateur Local : (hello ordinateur cette console s’exécute)** et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e81fb-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![Ajouter le composant logiciel enfichable Certificats - Sélection de l’ordinateur](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="e81fb-120">Bonjour **ajouter ou supprimer des composants logiciel enfichables** boîte de dialogue, cliquez sur **OK** tooadd hello certificats enfichable tooMMC.</span><span class="sxs-lookup"><span data-stu-id="e81fb-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![Ajouter des certificats enfichable tooMMC - terminé](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="e81fb-122">Dans la fenêtre de console MMC hello, cliquez sur tooexpand **racine de la Console**.</span><span class="sxs-lookup"><span data-stu-id="e81fb-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="e81fb-123">Vous devez voir hello le composant logiciel enfichable Certificats chargé.</span><span class="sxs-lookup"><span data-stu-id="e81fb-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="e81fb-124">Cliquez sur **certificats (ordinateur Local)** tooexpand.</span><span class="sxs-lookup"><span data-stu-id="e81fb-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="e81fb-125">Cliquez sur tooexpand hello **personnel** nœud, suivie de hello **certificats** nœud.</span><span class="sxs-lookup"><span data-stu-id="e81fb-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![Banque de certificats personnels ouverte](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="e81fb-127">Vous devez voir hello un certificat auto-signé, nous avons créé.</span><span class="sxs-lookup"><span data-stu-id="e81fb-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="e81fb-128">Vous pouvez examiner les propriétés de hello de hello certificat tooensure hello empreinte correspond à celui indiqué sur windows PowerShell de hello lorsque vous avez créé le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="e81fb-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="e81fb-129">Sélectionnez hello certificat auto-signé et **bouton droit sur**.</span><span class="sxs-lookup"><span data-stu-id="e81fb-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="e81fb-130">Dans le menu contextuel hello, sélectionnez **toutes les tâches** et sélectionnez **exporter...** .</span><span class="sxs-lookup"><span data-stu-id="e81fb-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Exportation du certificat](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="e81fb-132">Bonjour **Assistant Exportation de certificat**, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e81fb-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![Assistant Exportation de certificat](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="e81fb-134">Sur hello **exporter la clé privée** page, sélectionnez **Oui, exporter la clé privée de hello**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e81fb-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![Exportation du certificat - Clé privée](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="e81fb-136">Vous devez exporter la clé privée de hello en même temps que le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="e81fb-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="e81fb-137">Si vous fournissez un PFX qui ne contient pas de clé privée de hello pour le certificat de hello, l’activation de LDAP sécurisé pour votre domaine géré échoue.</span><span class="sxs-lookup"><span data-stu-id="e81fb-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="e81fb-138">Sur hello **Format de fichier d’exportation** page, sélectionnez **échange d’informations personnelles - PKCS #12 (. PFX)** en tant que format de fichier hello pour hello exportées de certificat.</span><span class="sxs-lookup"><span data-stu-id="e81fb-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![Exportation du certificat - Format de fichier](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="e81fb-140">Uniquement hello. Format de fichier PFX est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e81fb-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="e81fb-141">Ne pas exporter hello certificat toohello. Format du fichier CER.</span><span class="sxs-lookup"><span data-stu-id="e81fb-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="e81fb-142">Sur hello **sécurité** page, sélectionnez hello **mot de passe** option et tapez un Bonjour tooprotect de mot de passe. Fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="e81fb-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="e81fb-143">N’oubliez pas ce mot de passe, car il est nécessaire dans la tâche suivante hello.</span><span class="sxs-lookup"><span data-stu-id="e81fb-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="e81fb-144">Cliquez sur **suivant** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="e81fb-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="e81fb-145">Exportation du certificat - Mot de passe</span><span class="sxs-lookup"><span data-stu-id="e81fb-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="e81fb-146">Notez ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e81fb-146">Make a note of this password.</span></span> <span data-ttu-id="e81fb-147">Vous en avez besoin lors de l’activation de LDAP sécurisé pour ce domaine géré dans [tâche 3 : activer LDAP sécurisé pour le domaine géré de hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="e81fb-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="e81fb-148">Sur hello **fichier tooExport** , spécifiez le nom de fichier hello et l’emplacement où vous souhaitez que le certificat de hello tooexport.</span><span class="sxs-lookup"><span data-stu-id="e81fb-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![Exportation du certificat - Chemin d’accès](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="e81fb-150">Dans hello suivant page, cliquez sur **Terminer** le fichier PFX tooa tooexport hello certificat.</span><span class="sxs-lookup"><span data-stu-id="e81fb-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="e81fb-151">Vous devez voir la boîte de dialogue de confirmation lorsque hello certificat a été exporté.</span><span class="sxs-lookup"><span data-stu-id="e81fb-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![Exportation du certificat - Terminé](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="e81fb-153">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="e81fb-153">Next step</span></span>
[<span data-ttu-id="e81fb-154">Tâche 3 : activer LDAP sécurisé pour le domaine géré de hello</span><span class="sxs-lookup"><span data-stu-id="e81fb-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
