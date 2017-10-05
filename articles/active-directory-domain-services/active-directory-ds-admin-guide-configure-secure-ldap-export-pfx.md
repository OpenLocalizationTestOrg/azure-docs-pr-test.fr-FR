---
title: "Configurer le protocole LDAPS (LDAP sécurisé) dans les services de domaine Azure AD | Microsoft Docs"
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
ms.openlocfilehash: 5d46f376d46b8bbf3f93de57a7d4e31abdbcdb2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="07a97-103">Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="07a97-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="07a97-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="07a97-104">Before you begin</span></span>
<span data-ttu-id="07a97-105">Vérifiez que vous avez accompli la [Tâche 1 : Obtenir un certificat pour le protocole LDAP sécurisé](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="07a97-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="07a97-106">Tâche 2 : Exporter le certificat du protocole LDAP sécurisé vers un fichier .PFX</span><span class="sxs-lookup"><span data-stu-id="07a97-106">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="07a97-107">Avant de commencer cette tâche, assurez-vous que vous avez obtenu le certificat LDAP sécurisé auprès d’une autorité de certification publique ou créé un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="07a97-107">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="07a97-108">Procédez comme suit pour exporter le certificat LDAP sécurisé vers un fichier .PFX.</span><span class="sxs-lookup"><span data-stu-id="07a97-108">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="07a97-109">Appuyez sur le bouton **Démarrer** et tapez **R**. Dans la boîte de dialogue **Exécuter**, tapez **mmc** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="07a97-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Démarrer la console MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="07a97-111">Sur l’invite **Contrôle de compte d’utilisateur**, cliquez sur **OUI** pour démarrer la console MMC (Microsoft Management Console) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="07a97-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="07a97-112">Dans le menu **Fichier**, cliquez sur **Ajouter/Supprimer un composant logiciel enfichable**.</span><span class="sxs-lookup"><span data-stu-id="07a97-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Ajouter le composant logiciel enfichable à la console MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="07a97-114">Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, sélectionnez le composant logiciel enfichable **Certificats** et cliquez sur le bouton **Ajouter >**.</span><span class="sxs-lookup"><span data-stu-id="07a97-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![Ajouter le composant logiciel enfichable Certificats à la console MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="07a97-116">Dans l’Assistant **Composant logiciel enfichable Certificats**, sélectionnez **Compte d’ordinateur** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="07a97-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Ajouter le composant logiciel enfichable Certificats pour le compte d’ordinateur](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="07a97-118">Sur la page **Sélection de l’ordinateur**, sélectionnez **L’ordinateur local (l’ordinateur sur lequel cette console s’exécute)** et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="07a97-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![Ajouter le composant logiciel enfichable Certificats - Sélection de l’ordinateur](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="07a97-120">Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, cliquez sur **OK** et ajoutez le composant logiciel enfichable Certificats dans la console MMC.</span><span class="sxs-lookup"><span data-stu-id="07a97-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![Ajouter le composant logiciel enfichable Certificats à la console MMC - Terminé](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="07a97-122">Dans la fenêtre MMC, cliquez pour développer la **racine de la console**.</span><span class="sxs-lookup"><span data-stu-id="07a97-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="07a97-123">Vous devriez voir le composant logiciel enfichable Certificats se charger.</span><span class="sxs-lookup"><span data-stu-id="07a97-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="07a97-124">Cliquez sur le champ **Certificats (ordinateur local)** pour le développer.</span><span class="sxs-lookup"><span data-stu-id="07a97-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="07a97-125">Cliquez pour développer le nœud **Personnel**, suivi par le nœud **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="07a97-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![Banque de certificats personnels ouverte](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="07a97-127">Vous devez voir s’afficher le certificat auto-signé que nous avons créé.</span><span class="sxs-lookup"><span data-stu-id="07a97-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="07a97-128">Vous pouvez examiner les propriétés du certificat pour vous assurer que le Thumbprint correspond à celui qu’affichaient les fenêtres PowerShell lorsque vous avez créé le certificat.</span><span class="sxs-lookup"><span data-stu-id="07a97-128">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="07a97-129">Sélectionnez le certificat auto-signé et **cliquez avec le bouton droit sur ce dernier**.</span><span class="sxs-lookup"><span data-stu-id="07a97-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="07a97-130">Dans le menu contextuel, sélectionnez **Toutes les tâches** et sélectionnez **Exporter...**.</span><span class="sxs-lookup"><span data-stu-id="07a97-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Exportation du certificat](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="07a97-132">Dans **l’Assistant Exportation de certificat**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="07a97-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![Assistant Exportation de certificat](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="07a97-134">Sur la page **Exportation de la clé privée**, cliquez sur **Oui, exporter la clé privée** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="07a97-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![Exportation du certificat - Clé privée](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="07a97-136">Vous DEVEZ exporter la clé privée avec le certificat.</span><span class="sxs-lookup"><span data-stu-id="07a97-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="07a97-137">L’activation du protocole LDAP sécurisé pour votre domaine géré échoue si vous fournissez un fichier PFX qui ne contient pas la clé privée associée au certificat.</span><span class="sxs-lookup"><span data-stu-id="07a97-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="07a97-138">Sur la page **Format de fichier d’exportation**, sélectionnez le format de fichier **Échange d’informations personnelles - PKCS #12 (.PFX)** pour le certificat exporté.</span><span class="sxs-lookup"><span data-stu-id="07a97-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![Exportation du certificat - Format de fichier](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="07a97-140">Seul le format de fichier .PFX est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="07a97-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="07a97-141">N’exportez pas le certificat au format de fichier .CER.</span><span class="sxs-lookup"><span data-stu-id="07a97-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="07a97-142">Sur la page **Sécurité**, sélectionnez l’option **Mot de passe** et saisissez le mot de passe de protection du fichier .PFX.</span><span class="sxs-lookup"><span data-stu-id="07a97-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="07a97-143">N’oubliez pas ce mot de passe, car il est nécessaire pour la tâche suivante.</span><span class="sxs-lookup"><span data-stu-id="07a97-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="07a97-144">Cliquez sur **Suivant** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="07a97-144">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="07a97-145">Exportation du certificat - Mot de passe</span><span class="sxs-lookup"><span data-stu-id="07a97-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="07a97-146">Notez ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="07a97-146">Make a note of this password.</span></span> <span data-ttu-id="07a97-147">Vous en aurez besoin pour activer le protocole LDAP sécurisé pour ce domaine managé dans le cadre de la [Tâche 3 : Activer le protocole LDAP sécurisé pour le domaine managé](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md).</span><span class="sxs-lookup"><span data-stu-id="07a97-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="07a97-148">Sur la page **Fichier à exporter** , spécifiez le nom du fichier et l’emplacement d’exportation prévus pour le certificat.</span><span class="sxs-lookup"><span data-stu-id="07a97-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![Exportation du certificat - Chemin d’accès](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="07a97-150">Sur la page suivante, cliquez sur **Terminer** pour exporter le certificat en tant que fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="07a97-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="07a97-151">Vous devez voir apparaître une boîte de dialogue de confirmation lorsque le certificat est exporté.</span><span class="sxs-lookup"><span data-stu-id="07a97-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![Exportation du certificat - Terminé](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="07a97-153">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="07a97-153">Next step</span></span>
[<span data-ttu-id="07a97-154">Tâche 3 : Activer le protocole LDAP sécurisé pour le domaine managé</span><span class="sxs-lookup"><span data-stu-id="07a97-154">Task 3 - enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
