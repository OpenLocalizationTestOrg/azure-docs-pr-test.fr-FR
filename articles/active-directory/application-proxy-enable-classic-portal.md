---
title: "aaaEnable Proxy d’Application Azure AD dans le portail classique de hello | Documents Microsoft"
description: "Activer le Proxy d’Application Bonjour portail Azure classic et installer des connecteurs de proxy inverse de hello hello."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a><span data-ttu-id="c5685-103">Activer le Proxy d’Application dans le portail classique de hello et télécharger des connecteurs</span><span class="sxs-lookup"><span data-stu-id="c5685-103">Enable Application Proxy in hello classic portal and download connectors</span></span>
<span data-ttu-id="c5685-104">Cet article vous assiste hello étapes tooenable Proxy d’Application Microsoft Azure AD pour votre annuaire cloud dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5685-104">This article walks you through hello steps tooenable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span></span>

<span data-ttu-id="c5685-105">Si vous n’êtes pas familiarisé avec ce que le Proxy d’Application peuvent vous aider à effectuer, en savoir plus sur [comment tooprovide sécuriser l’accès à distance, applications locales tooon](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c5685-105">If you're unfamiliar with what Application Proxy can help you do, learn more about [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>

## <a name="application-proxy-prerequisites"></a><span data-ttu-id="c5685-106">Conditions préalables pour le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="c5685-106">Application Proxy prerequisites</span></span>
<span data-ttu-id="c5685-107">Avant que vous pouvez activer et utiliser les services de Proxy d’Application, vous devez toohave :</span><span class="sxs-lookup"><span data-stu-id="c5685-107">Before you can enable and use Application Proxy services, you need toohave:</span></span>

* <span data-ttu-id="c5685-108">Un [abonnement Microsoft Azure AD de base ou Premium](active-directory-editions.md) et un annuaire Azure AD sur lequel vous êtes administrateur général.</span><span class="sxs-lookup"><span data-stu-id="c5685-108">A [Microsoft Azure AD basic or premium subscription](active-directory-editions.md) and an Azure AD directory for which you are a global administrator.</span></span>
* <span data-ttu-id="c5685-109">Un serveur exécutant Windows Server 2012 R2 ou 2016, sur lequel vous pouvez installer hello connecteur Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="c5685-109">A server running Windows Server 2012 R2 or 2016, on which you can install hello Application Proxy Connector.</span></span> <span data-ttu-id="c5685-110">serveur de Hello envoie des demandes toohello les services de Proxy d’Application dans le cloud de hello, et il doit une applications toohello connexion HTTP ou HTTPS que vous publiez.</span><span class="sxs-lookup"><span data-stu-id="c5685-110">hello server sends requests toohello Application Proxy services in hello cloud, and it needs an HTTP or HTTPS connection toohello applications that you are publishing.</span></span>
  * <span data-ttu-id="c5685-111">Tooyour de l’authentification unique pour les applications publiées cet ordinateur doit être joint au domaine dans le domaine de hello même AD en tant qu’applications hello que vous publiez.</span><span class="sxs-lookup"><span data-stu-id="c5685-111">For single sign-on tooyour published applications, this machine should be domain-joined in hello same AD domain as hello applications that you are publishing.</span></span> <span data-ttu-id="c5685-112">Pour plus d’informations, consultez [Authentification unique avec le proxy d’application](active-directory-application-proxy-sso-using-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="c5685-112">For information, see [Single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md)</span></span>
* <span data-ttu-id="c5685-113">Si votre organisation utilise le proxy internet, de serveurs tooconnect toohello lecture [travail avec existant local serveurs proxy](application-proxy-working-with-proxy-servers.md) pour plus d’informations sur la façon de tooconfigure les.</span><span class="sxs-lookup"><span data-stu-id="c5685-113">If your organization uses proxy servers tooconnect toohello internet, read [Work with existing on-premises proxy servers](application-proxy-working-with-proxy-servers.md) for details on how tooconfigure them.</span></span>

## <a name="open-your-ports"></a><span data-ttu-id="c5685-114">Ouvrir vos ports</span><span class="sxs-lookup"><span data-stu-id="c5685-114">Open your ports</span></span>

<span data-ttu-id="c5685-115">tooprepare votre environnement pour le Proxy d’Application Azure AD, vous devez d’abord tooenable communication tooAzure des centres de données.</span><span class="sxs-lookup"><span data-stu-id="c5685-115">tooprepare your environment for Azure AD Application Proxy, you first need tooenable communication tooAzure data centers.</span></span> <span data-ttu-id="c5685-116">S’il existe un pare-feu dans le chemin d’accès de hello, assurez-vous qu’il est ouvert afin que hello que connecteur peut rendre HTTPS (TCP) demande toohello le Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="c5685-116">If there is a firewall in hello path, make sure that it's open so that hello Connector can make HTTPS (TCP) requests toohello Application Proxy.</span></span>

1. <span data-ttu-id="c5685-117">Ports de suivants de hello ouverte trop**sortant** le trafic :</span><span class="sxs-lookup"><span data-stu-id="c5685-117">Open hello following ports too**outbound** traffic:</span></span>

   | <span data-ttu-id="c5685-118">Numéro de port</span><span class="sxs-lookup"><span data-stu-id="c5685-118">Port number</span></span> | <span data-ttu-id="c5685-119">Utilisation</span><span class="sxs-lookup"><span data-stu-id="c5685-119">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="c5685-120">80</span><span class="sxs-lookup"><span data-stu-id="c5685-120">80</span></span> | <span data-ttu-id="c5685-121">Téléchargement de la révocation de certificats de listes (CRL) lors de la validation du certificat SSL de hello</span><span class="sxs-lookup"><span data-stu-id="c5685-121">Downloading certificate revocation lists (CRLs) while validating hello SSL certificate</span></span> |
   | <span data-ttu-id="c5685-122">443</span><span class="sxs-lookup"><span data-stu-id="c5685-122">443</span></span> | <span data-ttu-id="c5685-123">Toutes les communications sortantes par hello service Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="c5685-123">All outbound communication with hello Application Proxy service</span></span> |

   <span data-ttu-id="c5685-124">Si votre pare-feu gère le trafic en fonction des utilisateurs de toooriginating, ouvrir ces ports pour le trafic en provenance des services Windows exécutés comme Service réseau.</span><span class="sxs-lookup"><span data-stu-id="c5685-124">If your firewall enforces traffic according toooriginating users, open these ports for traffic coming from Windows services running as a Network Service.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c5685-125">table de Hello reflète les exigences du port hello pour les versions de connecteur 1.5.132.0 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="c5685-125">hello table reflects hello port requirements for connector versions 1.5.132.0 and newer.</span></span> <span data-ttu-id="c5685-126">Si vous disposez toujours d’une ancienne version de connecteur, vous devez également hello tooenable suivant des ports : 5671, 8080, 9090, 9091, 9350, 9352 et 10100 – 10120.</span><span class="sxs-lookup"><span data-stu-id="c5685-126">If you still have an older connector version, you also need tooenable hello following ports: 5671, 8080, 9090, 9091, 9350, 9352, and 10100–10120.</span></span>
   >
   ><span data-ttu-id="c5685-127">Pour plus d’informations sur la mise à jour de votre version la plus récente toohello connecteurs, consultez [connecteurs de Proxy d’Application Azure de comprendre AD](application-proxy-understand-connectors.md#automatic-updates).</span><span class="sxs-lookup"><span data-stu-id="c5685-127">For information about updating your connectors toohello newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md#automatic-updates).</span></span>

2. <span data-ttu-id="c5685-128">Si votre pare-feu ou un proxy autorise liste approuvées DNS, vous pouvez servicebus.windows.net et toomsappproxy.net de connexions de liste blanche.</span><span class="sxs-lookup"><span data-stu-id="c5685-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections toomsappproxy.net and servicebus.windows.net.</span></span> <span data-ttu-id="c5685-129">Si non, vous devez tooallow accès toohello [plages d’adresses IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653), qui sont mis à jour chaque semaine.</span><span class="sxs-lookup"><span data-stu-id="c5685-129">If not, you need tooallow access toohello [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span></span>

3. <span data-ttu-id="c5685-130">Hello d’utilisation [Azure AD Application Proxy Connector Ports Test outil](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que votre connecteur pouvez contacter le service de Proxy d’Application hello.</span><span class="sxs-lookup"><span data-stu-id="c5685-130">Use hello [Azure AD Application Proxy Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify that your connector can reach hello Application Proxy service.</span></span> <span data-ttu-id="c5685-131">Au minimum, assurez-vous que toutes les coches vertes la région du centre des États-Unis hello et tooyou le plus proche de la région de hello.</span><span class="sxs-lookup"><span data-stu-id="c5685-131">At a minimum, make sure that hello Central US region and hello region closest tooyou have all green checkmarks.</span></span> <span data-ttu-id="c5685-132">En outre, un nombre plus élevé de coches vertes signifie une résilience accrue.</span><span class="sxs-lookup"><span data-stu-id="c5685-132">Beyond that, more green checkmarks means greater resiliency.</span></span>

## <a name="enable-application-proxy-in-azure-ad"></a><span data-ttu-id="c5685-133">Activer le proxy d’application dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5685-133">Enable Application Proxy in Azure AD</span></span>
1. <span data-ttu-id="c5685-134">Connectez-vous en tant qu’administrateur Bonjour [portail Azure classic](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="c5685-134">Sign in as an administrator in hello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="c5685-135">TooActive active, sélectionnez le répertoire hello dans lequel vous souhaitez tooenable Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="c5685-135">Go tooActive Directory and select hello directory in which you want tooenable Application Proxy.</span></span>

    ![Active Directory - icône](./media/active-directory-application-proxy-enable/ad_icon.png)
3. <span data-ttu-id="c5685-137">Sélectionnez **configurer** la page annuaire hello et faites défiler trop**le Proxy d’Application**.</span><span class="sxs-lookup"><span data-stu-id="c5685-137">Select **Configure** from hello directory page, and scroll down too**Application Proxy**.</span></span>
4. <span data-ttu-id="c5685-138">Activer/désactiver **activer les Services de Proxy d’Application pour ce répertoire** trop**activé**.</span><span class="sxs-lookup"><span data-stu-id="c5685-138">Toggle **Enable Application Proxy Services for this Directory** too**Enabled**.</span></span>

    ![Activer le proxy d’application](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. <span data-ttu-id="c5685-140">Sélectionnez **Télécharger maintenant**.</span><span class="sxs-lookup"><span data-stu-id="c5685-140">Select **Download now**.</span></span> <span data-ttu-id="c5685-141">Hello **Azure AD Application Proxy Connector Télécharger** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c5685-141">hello **Azure AD Application Proxy Connector Download** opens.</span></span> <span data-ttu-id="c5685-142">Lisez et acceptez les termes du contrat de licence hello et cliquez sur **télécharger** toosave hello fichier Windows Installer (.exe) de connecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="c5685-142">Read and accept hello license terms and click **Download** toosave hello Windows Installer file (.exe) for hello connector.</span></span>

## <a name="install-and-register-hello-connector"></a><span data-ttu-id="c5685-143">Installer et inscrire hello connecteur</span><span class="sxs-lookup"><span data-stu-id="c5685-143">Install and register hello Connector</span></span>
1. <span data-ttu-id="c5685-144">Exécutez **AADApplicationProxyConnectorInstaller.exe** sur le serveur de hello vous préparé conséquente toohello prerequisites.</span><span class="sxs-lookup"><span data-stu-id="c5685-144">Run **AADApplicationProxyConnectorInstaller.exe** on hello server you prepared according toohello prerequisites.</span></span>
2. <span data-ttu-id="c5685-145">Suivez les instructions de hello de hello Assistant tooinstall.</span><span class="sxs-lookup"><span data-stu-id="c5685-145">Follow hello instructions in hello wizard tooinstall.</span></span>
3. <span data-ttu-id="c5685-146">Pendant l’installation, vous êtes tooregister demandées hello connecteur hello Proxy d’Application de votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5685-146">During installation, you are prompted tooregister hello connector with hello Application Proxy of your Azure AD tenant.</span></span>

   * <span data-ttu-id="c5685-147">Fournissez vos informations d’identification d’administrateur général d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5685-147">Provide your Azure AD global administrator credentials.</span></span> <span data-ttu-id="c5685-148">Votre client d’administrateur global peut être différent de vos informations d’identification Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c5685-148">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
   * <span data-ttu-id="c5685-149">Assurez-vous que l’administrateur de hello hello connecteur se trouve dans des registres hello même répertoire où vous avez activé hello service Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="c5685-149">Make sure hello admin who registers hello connector is in hello same directory where you enabled hello Application Proxy service.</span></span> <span data-ttu-id="c5685-150">Par exemple, si le domaine du locataire hello est contoso.com, hello admin doit être admin@contoso.com ou tout autre alias sur ce domaine.</span><span class="sxs-lookup"><span data-stu-id="c5685-150">For example, if hello tenant domain is contoso.com, hello admin should be admin@contoso.com or any other alias on that domain.</span></span>
   * <span data-ttu-id="c5685-151">Si **la Configuration de sécurité renforcée d’Internet Explorer** est défini trop**sur** sur le serveur de hello, l’écran d’enregistrement hello risque d’être bloqué.</span><span class="sxs-lookup"><span data-stu-id="c5685-151">If **IE Enhanced Security Configuration** is set too**On** on hello server, hello registration screen might be blocked.</span></span> <span data-ttu-id="c5685-152">accès tooallow, suivez les instructions dans le message d’erreur hello hello.</span><span class="sxs-lookup"><span data-stu-id="c5685-152">tooallow access, follow hello instructions in hello error message.</span></span> <span data-ttu-id="c5685-153">Vérifiez que la configuration de sécurité renforcée d’Internet Explore est désactivée.</span><span class="sxs-lookup"><span data-stu-id="c5685-153">Make sure that Internet Explorer Enhanced Security is off.</span></span>
   * <span data-ttu-id="c5685-154">Si l’inscription du connecteur n’aboutit pas, voir [Résoudre les problèmes du proxy d’application](active-directory-application-proxy-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="c5685-154">If connector registration does not succeed, see [Troubleshoot Application Proxy](active-directory-application-proxy-troubleshoot.md).</span></span>  
4. <span data-ttu-id="c5685-155">Lors de l’installation de hello terminée, deux nouveaux services sont ajoutés tooyour server :</span><span class="sxs-lookup"><span data-stu-id="c5685-155">When hello installation completes, two new services are added tooyour server:</span></span>

   * <span data-ttu-id="c5685-156">**connecteur de proxy d’application Microsoft AAD** active la connectivité.</span><span class="sxs-lookup"><span data-stu-id="c5685-156">**Microsoft AAD Application Proxy Connector** enables connectivity</span></span>

     * <span data-ttu-id="c5685-157">**Le programme de mise à jour du connecteur de proxy d’application Microsoft AAD** est un service de mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="c5685-157">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span></span> <span data-ttu-id="c5685-158">Il vérifie les nouvelles versions de connecteur de hello périodiquement et met à jour de connecteur de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="c5685-158">It periodically checks for new versions of hello connector and updates hello connector as needed.</span></span>

     ![Services de connecteur de proxy d’application - capture d’écran](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. <span data-ttu-id="c5685-160">Cliquez sur **Terminer** dans la fenêtre d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="c5685-160">Click **Finish** in hello installation window.</span></span>

<span data-ttu-id="c5685-161">Pour plus d’informations sur les connecteurs, consultez [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="c5685-161">For information about connectors, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

<span data-ttu-id="c5685-162">Pour bénéficier d’une haute disponibilité, vous devez déployer au moins deux connecteurs.</span><span class="sxs-lookup"><span data-stu-id="c5685-162">For high availability purposes, you should deploy at least two connectors.</span></span> <span data-ttu-id="c5685-163">toodeploy plusieurs connecteurs, répétez les étapes 2 et 3.</span><span class="sxs-lookup"><span data-stu-id="c5685-163">toodeploy more connectors, repeat steps 2 and 3.</span></span> <span data-ttu-id="c5685-164">Chaque connecteur doit être inscrit séparément.</span><span class="sxs-lookup"><span data-stu-id="c5685-164">Each connector must be registered separately.</span></span>

<span data-ttu-id="c5685-165">Si vous souhaitez toouninstall hello connecteur, désinstallez les services de connecteur hello et hello mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c5685-165">If you want toouninstall hello Connector, uninstall both hello Connector service and hello Updater service.</span></span> <span data-ttu-id="c5685-166">Redémarrez votre ordinateur toofully supprimer hello service.</span><span class="sxs-lookup"><span data-stu-id="c5685-166">Restart your computer toofully remove hello service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5685-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c5685-167">Next steps</span></span>
<span data-ttu-id="c5685-168">Vous êtes maintenant prêt trop[publier des applications avec Proxy d’Application](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="c5685-168">You are now ready too[Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

<span data-ttu-id="c5685-169">Si vous avez des applications qui se trouvent sur des réseaux distincts ou des emplacements différents, vous pouvez utiliser plusieurs connecteurs connecteur groupes tooorganize hello dans des unités logiques.</span><span class="sxs-lookup"><span data-stu-id="c5685-169">If you have applications that are on separate networks or different locations, you can use connector groups tooorganize hello different connectors into logical units.</span></span> <span data-ttu-id="c5685-170">Apprenez-en davantage sur [l’utilisation de connecteurs de proxy d’application](active-directory-application-proxy-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="c5685-170">Learn more about [Working with Application Proxy connectors](active-directory-application-proxy-connectors.md).</span></span>