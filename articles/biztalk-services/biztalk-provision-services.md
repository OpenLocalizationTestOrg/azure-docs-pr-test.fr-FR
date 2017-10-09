---
title: aaaCreate Azure BizTalk Services Bonjour portail Azure | Documents Microsoft
description: "Découvrez comment tooprovision ou créer des Services BizTalk Azure Bonjour portail Azure ; MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="72735-103">Créer des Services BizTalk à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="72735-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="72735-104">toosign dans toohello portail Azure, vous devez un compte Azure et un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="72735-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="72735-105">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="72735-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="72735-106">Consultez [Version d'évaluation gratuite d'Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="72735-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="72735-107"><a name="CreateService"></a>Créer un service BizTalk</span><span class="sxs-lookup"><span data-stu-id="72735-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="72735-108">Selon l’édition que vous choisissez de hello, pas tous les paramètres de BizTalk Service peuvent être disponibles.</span><span class="sxs-lookup"><span data-stu-id="72735-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="72735-109">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="72735-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="72735-110">Dans le volet de navigation inférieur hello, sélectionnez **nouveau**:</span><span class="sxs-lookup"><span data-stu-id="72735-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="72735-111">![Sélectionnez le bouton de nouveau hello][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="72735-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="72735-112">Sélectionnez **APP SERVICES** > **SERVICE BIZTALK** > **CRÉATION PERSONNALISÉE** :</span><span class="sxs-lookup"><span data-stu-id="72735-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="72735-113">![Sélectionner BizTalk Services, puis Custom Create][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="72735-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="72735-114">Entrez les paramètres de Service BizTalk hello :</span><span class="sxs-lookup"><span data-stu-id="72735-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="72735-115"><strong>Nom du service BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="72735-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="72735-116">Vous pouvez entrer n'importe quel nom, mais soyez spécifique.</span><span class="sxs-lookup"><span data-stu-id="72735-116">You can enter any name but be specific.</span></span> <span data-ttu-id="72735-117">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="72735-117">Some examples include:</span></span><br/><br/><span data-ttu-id="72735-118">
    <em>masociété</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="72735-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="72735-119">
    <em>masociétémonapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="72735-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="72735-120">
    <em>monapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="72735-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="72735-121">«. biztalk.windows.net » est automatiquement ajouté toohello nom que vous entrez.</span><span class="sxs-lookup"><span data-stu-id="72735-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="72735-122">Cette opération crée une URL qui est utilisé tooaccess votre BizTalk Service, tel que <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="72735-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="72735-123"><strong>Édition</strong></span><span class="sxs-lookup"><span data-stu-id="72735-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="72735-124">Si vous êtes dans la phase de test/développement hello, choisissez <strong>développeur</strong>.</span><span class="sxs-lookup"><span data-stu-id="72735-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="72735-125">Si vous êtes dans la phase de production hello, utilisez hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">Services BizTalk : tableau comparatif des éditions</a> toodetermine si <strong>Premium</strong>, <strong>Standard</strong>, ou <strong>Basic</strong>est hello bon choix pour votre scénario d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="72735-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="72735-126"><strong>Région</strong></span><span class="sxs-lookup"><span data-stu-id="72735-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="72735-127">Sélectionnez hello région géographique toohost votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="72735-128"><strong>URL du domaine</strong></span><span class="sxs-lookup"><span data-stu-id="72735-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="72735-129"><strong>Facultatif</strong>.</span><span class="sxs-lookup"><span data-stu-id="72735-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="72735-130">Par défaut, les URL de domaine hello est <em>Nom_de_votre_service_biztalk</em>. biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="72735-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="72735-131">Un domaine personnalisé peut également être entré.</span><span class="sxs-lookup"><span data-stu-id="72735-131">A custom domain can also be entered.</span></span> <span data-ttu-id="72735-132">Par exemple, si votre domaine est <em>contoso</em>, vous pouvez entrer :</span><span class="sxs-lookup"><span data-stu-id="72735-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="72735-133">
    <em>MaSociété</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="72735-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="72735-134">
    <em>MaSociétéMonApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="72735-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="72735-135">
    <em>MonApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="72735-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="72735-136">
    <em>NomServiceBizTalk</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="72735-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="72735-137">Sélectionnez la flèche suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="72735-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="72735-138">5.</span><span class="sxs-lookup"><span data-stu-id="72735-138">5.</span></span> <span data-ttu-id="72735-139">Entrez hello stockage et les paramètres de la base de données :</span><span class="sxs-lookup"><span data-stu-id="72735-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="72735-140"><strong>Compte de stockage de surveillance/archivage</strong></span><span class="sxs-lookup"><span data-stu-id="72735-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="72735-141">Sélectionnez un compte de stockage existant ou créez un nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="72735-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="72735-142">Si vous créez un compte de stockage, entrez hello <strong>nom de compte de stockage</strong>.</span><span class="sxs-lookup"><span data-stu-id="72735-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="72735-143"><strong>Base de données de suivi</strong></span><span class="sxs-lookup"><span data-stu-id="72735-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="72735-144">Si vous utilisez une base de données SQL Azure existante, celle-ci ne peut pas être utilisée par un autre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="72735-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="72735-145">Vous devez le nom de connexion hello et le mot de passe entré lors de la création de ce serveur de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="72735-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="72735-146"><strong>Conseil</strong> base de données de suivi créer hello et compte de stockage surveillance/archivage hello même région que hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="72735-147">Sélectionnez la flèche suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="72735-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="72735-148">6.</span><span class="sxs-lookup"><span data-stu-id="72735-148">6.</span></span> <span data-ttu-id="72735-149">Entrez les paramètres de base de données hello :</span><span class="sxs-lookup"><span data-stu-id="72735-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="72735-150"><strong>Name</strong></span><span class="sxs-lookup"><span data-stu-id="72735-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="72735-151">Disponible lorsque <strong>créer une nouvelle instance de la base de données SQL</strong> est sélectionné dans l’écran précédent hello.</span><span class="sxs-lookup"><span data-stu-id="72735-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="72735-152">Entrez un toobe de nom de base de données SQL utilisée par votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="72735-153"><strong>Serveur</strong></span><span class="sxs-lookup"><span data-stu-id="72735-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="72735-154">Disponible lorsque <strong>créer une nouvelle instance de la base de données SQL</strong> est sélectionné dans l’écran précédent hello.</span><span class="sxs-lookup"><span data-stu-id="72735-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="72735-155">Sélectionnez un serveur SQL Database existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="72735-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="72735-156"><strong>Nom de connexion du serveur</strong></span><span class="sxs-lookup"><span data-stu-id="72735-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="72735-157">Entrez le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="72735-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="72735-158"><strong>Mot de passe de connexion du serveur</strong></span><span class="sxs-lookup"><span data-stu-id="72735-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="72735-159">Entrez le mot de passe de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="72735-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="72735-160"><strong>Région</strong></span><span class="sxs-lookup"><span data-stu-id="72735-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="72735-161">Disponible lorsque l’option <strong>Créer une instance de base de données SQL</strong> est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="72735-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="72735-162">Sélectionnez hello région géographique toohost votre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="72735-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="72735-163">Sélectionnez hello coche toocomplete hello Assistant.</span><span class="sxs-lookup"><span data-stu-id="72735-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="72735-164">icône de progression Hello s’affiche :</span><span class="sxs-lookup"><span data-stu-id="72735-164">hello progress icon appears:</span></span>  
![Icône d'avancement affichée à la fin de l'opération][ProgressComplete]

<span data-ttu-id="72735-166">Lorsque vous avez terminé, hello Azure BizTalk Service est créé et prêt pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="72735-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="72735-167">paramètres par défaut de Hello sont suffisants.</span><span class="sxs-lookup"><span data-stu-id="72735-167">hello default settings are sufficient.</span></span> <span data-ttu-id="72735-168">Si vous souhaitez que les paramètres par défaut de hello toochange, sélectionnez **BIZTALK SERVICES** dans hello du volet de navigation gauche, puis sélectionnez votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="72735-169">Paramètres supplémentaires sont affichés dans hello [onglets tableau de bord, analyse et mise à l’échelle](biztalk-dashboard-monitor-scale-tabs.md) haut hello.</span><span class="sxs-lookup"><span data-stu-id="72735-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="72735-170">En fonction de l’état de hello Hello BizTalk Service, il existe certaines opérations qui ne peut pas être terminées.</span><span class="sxs-lookup"><span data-stu-id="72735-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="72735-171">Pour obtenir la liste de ces opérations, consultez trop[BizTalk Services état graphique](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="72735-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="72735-172">Étapes postérieures à l’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="72735-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="72735-173">Installer le certificat de hello sur un ordinateur local</span><span class="sxs-lookup"><span data-stu-id="72735-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="72735-174">Ajouter un certificat prêt pour la production</span><span class="sxs-lookup"><span data-stu-id="72735-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="72735-175">Obtenir l’espace de noms de contrôle d’accès hello</span><span class="sxs-lookup"><span data-stu-id="72735-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="72735-176"><a name="InstallCert"></a>Installer le certificat de hello sur un ordinateur local</span><span class="sxs-lookup"><span data-stu-id="72735-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="72735-177">Dans le cadre de l'approvisionnement du service BizTalk, un certificat auto-signé est créé et associé à votre abonnement au service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="72735-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="72735-178">Vous devez télécharger ce certificat et l’installer sur des ordinateurs de l’emplacement où vous déployez des applications de BizTalk Service ou envoyez des messages tooa point de terminaison de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="72735-179">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="72735-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="72735-180">Sélectionnez **BIZTALK SERVICES** dans hello du volet de navigation gauche, puis sélectionnez votre abonnement au Service de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="72735-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="72735-181">Sélectionnez hello **tableau de bord** onglet.</span><span class="sxs-lookup"><span data-stu-id="72735-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="72735-182">Sélectionnez **Télécharger le certificat SSL** :</span><span class="sxs-lookup"><span data-stu-id="72735-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="72735-183">![Modifier le certificat SSL][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="72735-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="72735-184">Double-cliquez sur le certificat de hello et exécuter via un certificat de hello Assistant tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="72735-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="72735-185">Assurez-vous que vous installez le certificat hello sous hello **autorités de certification racine de confiance** stocker.</span><span class="sxs-lookup"><span data-stu-id="72735-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="72735-186"><a name="AddCert"></a>Ajouter un certificat prêt pour la production</span><span class="sxs-lookup"><span data-stu-id="72735-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="72735-187">Hello un certificat auto-signé créé automatiquement lors de la création de Services de BizTalk est prévu pour une utilisation dans les environnements de développement uniquement.</span><span class="sxs-lookup"><span data-stu-id="72735-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="72735-188">Dans les scénarios de production, remplacez-le par un certificat prêt pour la production.</span><span class="sxs-lookup"><span data-stu-id="72735-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="72735-189">Sur hello **tableau de bord** onglet, sélectionnez **certificat SSL de mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="72735-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="72735-190">Parcourir les certificats SSL privé tooyour (*CertificateName*.pfx) qui inclut le nom de votre BizTalk Service, hello mot de passe, puis cliquez sur la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="72735-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="72735-191"><a name="ACS"></a>Obtenir l’espace de noms de contrôle d’accès hello</span><span class="sxs-lookup"><span data-stu-id="72735-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="72735-192">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="72735-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="72735-193">Sélectionnez **BIZTALK SERVICES** dans hello du volet de navigation gauche, puis sélectionnez votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="72735-194">Dans la barre des tâches hello, sélectionnez **les informations de connexion**:</span><span class="sxs-lookup"><span data-stu-id="72735-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="72735-195">![Sélectionner les informations de connexion][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="72735-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="72735-196">Copiez les valeurs de contrôle d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="72735-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="72735-197">Lorsque vous déployez un projet BizTalk Services à partir de Visual Studio, vous entrez cet espace de noms de contrôle d'accès.</span><span class="sxs-lookup"><span data-stu-id="72735-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="72735-198">espace de noms de contrôle d’accès Hello est automatiquement créé pour votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="72735-199">valeurs de contrôle d’accès de Hello peuvent être utilisées avec n’importe quelle application.</span><span class="sxs-lookup"><span data-stu-id="72735-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="72735-200">En cas d’Azure BizTalk Services est créé, cet espace de noms de contrôle d’accès contrôle authentification hello avec votre déploiement de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="72735-201">Si vous souhaitez toochange hello abonnement ou gérez l’espace de noms hello, sélectionnez **ACTIVE DIRECTORY** dans hello du volet de navigation gauche et sélectionnez votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="72735-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="72735-202">barre des tâches Hello répertorie les options disponibles.</span><span class="sxs-lookup"><span data-stu-id="72735-202">hello task bar lists your options.</span></span>

<span data-ttu-id="72735-203">En cliquant sur **gérer** ouvre hello portail de gestion Access Control.</span><span class="sxs-lookup"><span data-stu-id="72735-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="72735-204">Dans le portail de gestion Access Control de hello, hello BizTalk Service utilise **identités de Service**:</span><span class="sxs-lookup"><span data-stu-id="72735-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="72735-205">![Identités de Service ACS Bonjour portail de gestion Access Control][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="72735-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="72735-206">Hello identité de service de contrôle d’accès est un ensemble d’informations d’identification qui permettent aux applications ou tooauthenticate clients directement avec le contrôle d’accès et de recevoir un jeton.</span><span class="sxs-lookup"><span data-stu-id="72735-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72735-207">Hello BizTalk Service utilise **propriétaire** pour l’identité de service par défaut hello et hello **mot de passe** valeur.</span><span class="sxs-lookup"><span data-stu-id="72735-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="72735-208">Si vous utilisez la valeur de clé symétrique hello au lieu de la valeur de mot de passe de hello, hello erreur suivante peut se produire.</span><span class="sxs-lookup"><span data-stu-id="72735-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="72735-209">*Pas pu se connecter compte de Service de gestion Access Control toohello hello spécifié avec les informations d’identification*</span><span class="sxs-lookup"><span data-stu-id="72735-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="72735-210">[Gestion de votre espace de noms ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) répertorie quelques instructions et recommandations.</span><span class="sxs-lookup"><span data-stu-id="72735-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="72735-211">Explication des exigences</span><span class="sxs-lookup"><span data-stu-id="72735-211">Requirements explained</span></span>
<span data-ttu-id="72735-212">Ces exigences ne s’appliquent pas toohello édition gratuite.</span><span class="sxs-lookup"><span data-stu-id="72735-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="72735-213"><strong>Ce dont vous avez besoin</strong></span><span class="sxs-lookup"><span data-stu-id="72735-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="72735-214"><strong>Raison</strong></span><span class="sxs-lookup"><span data-stu-id="72735-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="72735-215">Abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="72735-215">Azure subscription</span></span></td>
<td><span data-ttu-id="72735-216">abonnement de Hello détermine qui peut se connecter toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="72735-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="72735-217">détenteur du compte de Hello crée l’abonnement hello sur <a HREF="https://account.windowsazure.com/Subscriptions"> abonnements Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="72735-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="72735-218">Bonjour compte Azure peut avoir plusieurs abonnements et peut être géré par toute personne qui est autorisée.</span><span class="sxs-lookup"><span data-stu-id="72735-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="72735-219">Par exemple, le détenteur du compte Azure crée un abonnement nommé <em>BizTalkServiceSubscription</em> et donne hello administrateurs BizTalk au sein de votre société (par exemple, ContosoBTSAdmins@live.com) à toothis abonnement.</span><span class="sxs-lookup"><span data-stu-id="72735-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="72735-220">Dans ce scénario, les administrateurs de BizTalk hello connectez-vous toohello portail Azure et ont des services de hello hébergé tooall de droits administrateur complets dans l’abonnement hello, y compris les Services BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="72735-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="72735-221">les administrateurs de BizTalk Hello ne sont pas des détenteurs de compte Azure hello et par conséquent, n’avez pas accès aux informations de facturation tooany.</span><span class="sxs-lookup"><span data-stu-id="72735-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="72735-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gérer les abonnements et les comptes de stockage Bonjour Azure portal</a> fournit plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="72735-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="72735-223">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="72735-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="72735-224">Stocke les tables de hello, vues et procédures stockées utilisées par hello BizTalk Service, y compris les données de suivi hello.</span><span class="sxs-lookup"><span data-stu-id="72735-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="72735-225">Lorsque vous créez un service BizTalk, vous pouvez utiliser un serveur SQL Azure existant, une base de données SQL Azure existante ou créer automatiquement un serveur ou une base de données.</span><span class="sxs-lookup"><span data-stu-id="72735-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="72735-226">Hello montée en puissance de la base de données SQL est configuré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="72735-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="72735-227">En règle générale, la mise à l’échelle par défaut de hello est suffisant pour un BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="72735-228">Modifier l’échelle de hello a un impact sur la tarification.</span><span class="sxs-lookup"><span data-stu-id="72735-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="72735-229">Voir <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Comptes et facturation dans la base de données SQL Azure</a>
</span><span class="sxs-lookup"><span data-stu-id="72735-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="72735-230">
<strong>Remarques</strong>
</span><span class="sxs-lookup"><span data-stu-id="72735-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="72735-231">Lorsque vous créez un serveur et une base de données SQL Azure, les services Azure sont automatiquement activés.</span><span class="sxs-lookup"><span data-stu-id="72735-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="72735-232">Hello BizTalk Service nécessite des Services Azure est activée.</span><span class="sxs-lookup"><span data-stu-id="72735-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="72735-233">Si vous créez une nouvelle base de données SQL Azure sur un serveur SQL Azure, hello des règles de pare-feu de hello serveur ne sont pas modifiés.</span><span class="sxs-lookup"><span data-stu-id="72735-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="72735-234">Par conséquent, il est possible d’autres Services Azure ne sont pas autorisés de bases de données du serveur d’accès toohello.</span><span class="sxs-lookup"><span data-stu-id="72735-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="72735-235">Espace de noms de contrôle d'accès Azure</span><span class="sxs-lookup"><span data-stu-id="72735-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="72735-236">Permet de s'authentifier auprès d'Azure BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="72735-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="72735-237">Lorsque vous déployez un projet BizTalk Services à partir de Visual Studio, vous entrez cet espace de noms de contrôle d'accès.</span><span class="sxs-lookup"><span data-stu-id="72735-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="72735-238">Lorsque vous créez un BizTalk Service, espace de noms de contrôle d’accès hello est automatiquement créé.</span><span class="sxs-lookup"><span data-stu-id="72735-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="72735-239">Compte de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="72735-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="72735-240">Offrent un accès tootables, objets BLOB et files d’attente utilisées par votre suivant de hello toosave BizTalk Service :</span><span class="sxs-lookup"><span data-stu-id="72735-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="72735-241">Les fichiers journaux qui hello moniteur BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="72735-242">Hello analyse la sortie s’affiche également dans hello **analyse** onglet Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="72735-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="72735-243">Lorsque vous créez un X12 ou accord AS2 entre partenaires, vous pouvez activer les propriétés de message hello d’archivage fonctionnalité toostore.</span><span class="sxs-lookup"><span data-stu-id="72735-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="72735-244">Ces données sont enregistrées dans le compte de stockage de hello.</span><span class="sxs-lookup"><span data-stu-id="72735-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="72735-245">Lorsque vous créez un service BizTalk, vous pouvez utiliser un compte de stockage existant ou en créer un automatiquement.</span><span class="sxs-lookup"><span data-stu-id="72735-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="72735-246">paramètres de stockage Hello par défaut sont suffisantes pour un BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="72735-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="72735-247">Lorsque vous créez un compte de stockage, une clé primaire et une clé secondaire sont automatiquement créées.</span><span class="sxs-lookup"><span data-stu-id="72735-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="72735-248">Ces clés contrôlent l’accès tooyour compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="72735-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="72735-249">Hello BizTalk Service utilise automatiquement hello clé primaire.</span><span class="sxs-lookup"><span data-stu-id="72735-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="72735-250">Pour plus d’informations, consultez <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Stockage</a>.</span><span class="sxs-lookup"><span data-stu-id="72735-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="72735-251">Certificat privé SSL</span><span class="sxs-lookup"><span data-stu-id="72735-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="72735-252">Quand un service Azure BizTalk est créé, une URL HTTPS qui inclut le nom de votre service BizTalk est également créée.</span><span class="sxs-lookup"><span data-stu-id="72735-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="72735-253">Cette URL est automatiquement configuré toouse un certificat auto-signé de développement uniquement.</span><span class="sxs-lookup"><span data-stu-id="72735-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="72735-254">Pour la production, vous avez besoin d'un certificat SSL privé.</span><span class="sxs-lookup"><span data-stu-id="72735-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="72735-255">
<strong>Informations importantes sur le certificat SSL</strong>

</span><span class="sxs-lookup"><span data-stu-id="72735-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="72735-256">date d’expiration de certificat Hello doit être inférieure à 5 ans.</span><span class="sxs-lookup"><span data-stu-id="72735-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="72735-257">Tous les certificats privés exigent un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="72735-257">All private certificates require a password.</span></span> <span data-ttu-id="72735-258">Retenez ce mot de passe. Il est également recommandé de communiquer ce mot de passe à vos administrateurs.</span><span class="sxs-lookup"><span data-stu-id="72735-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="72735-259">Les certificats auto-signés sont utilisés dans des environnements de test/développement.</span><span class="sxs-lookup"><span data-stu-id="72735-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="72735-260">Lors de l’utilisation des certificats auto-signés, importez le magasin de certificats personnel hello certificat tooyour et hello du magasin de certificats Autorités de Certification racines de confiance.</span><span class="sxs-lookup"><span data-stu-id="72735-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="72735-261">Lors de l’envoi d’autorité de certification du certificat demande tooyour hello production, donnez à hello certificat propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="72735-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="72735-262"><strong>Utilisation avancée de la clé</strong> : au minimum, Azure BizTalk Services exige l’authentification du serveur.</span><span class="sxs-lookup"><span data-stu-id="72735-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="72735-263"><strong>Nom commun</strong>: entrez le nom de domaine complet (FQDN) hello de votre URL de Service Azure BizTalk.</span><span class="sxs-lookup"><span data-stu-id="72735-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="72735-264">Voir <a HREF="#CreateService">Création d’un service BizTalk</a> dans cet article.</span><span class="sxs-lookup"><span data-stu-id="72735-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="72735-265">Un certificat nouveau ou différent peut être ajouté après que hello BizTalk Service est créé.</span><span class="sxs-lookup"><span data-stu-id="72735-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="72735-266">les connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="72735-266">Hybrid Connections</span></span>
<span data-ttu-id="72735-267">Lorsque vous créez un BizTalk Service de Azure, hello **connexions hybrides** onglet est disponible :</span><span class="sxs-lookup"><span data-stu-id="72735-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![Onglet Connexions hybrides][HybridConnectionTab]

<span data-ttu-id="72735-269">Connexions hybrides sont utilisé tooconnect Azure site Web ou service mobile Azure tooany localement les ressources qui utilise un port TCP statique, telles que SQL Server, MySQL, HTTP Web API, les Services mobiles et la plupart des Services Web personnalisés.</span><span class="sxs-lookup"><span data-stu-id="72735-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="72735-270">Connexions hybrides et hello Service d’adaptateur BizTalk sont différents.</span><span class="sxs-lookup"><span data-stu-id="72735-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="72735-271">Hello Service d’adaptateur BizTalk est le système métier (LOB) local utilisé tooconnect Azure BizTalk Services tooan.</span><span class="sxs-lookup"><span data-stu-id="72735-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="72735-272">Consultez [connexions hybrides](integration-hybrid-connection-overview.md) toolearn plus, notamment la création et la gestion des connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="72735-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72735-273">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72735-273">Next steps</span></span>
<span data-ttu-id="72735-274">Maintenant que la création d’un BizTalk Service, familiarisez-vous avec hello différents [BizTalk Services : onglets tableau de bord, analyse et mise à l’échelle](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="72735-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="72735-275">Votre service BizTalk est prêt pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="72735-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="72735-276">toostart création d’applications, accédez trop[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="72735-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="72735-277">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="72735-277">See also</span></span>
* [<span data-ttu-id="72735-278">Tableau comparatif des éditions de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="72735-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="72735-279">Tableau comparatif des états du service BizTalk</span><span class="sxs-lookup"><span data-stu-id="72735-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="72735-280">Sauvegarde et restauration de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="72735-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="72735-281">Limitation dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="72735-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="72735-282">Nom et clé de l'émetteur dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="72735-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="72735-283">Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="72735-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="72735-284">Connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="72735-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
