---
title: "aaaMigrate un tooAzure d’application enterprise web du Service d’applications"
description: "Montre comment tooquickly de l’Assistant Migration de Web Apps toouse migrer tooAzure de sites Web IIS existant App Service Web Apps"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a><span data-ttu-id="36f99-103">Migrer un ordinateur enterprise web application tooAzure du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="36f99-103">Migrate an enterprise web app tooAzure App Service</span></span>
<span data-ttu-id="36f99-104">Vous pouvez facilement migrer vos sites Web existante qui s’exécutent sur Internet Information Services (IIS) 6 ou version ultérieure trop[App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="36f99-104">You can easily migrate your existing websites that run on Internet Information Service (IIS) 6 or later too[App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="36f99-105">La fin du support de Windows Server 2003 est intervenue le 14 juillet 2015.</span><span class="sxs-lookup"><span data-stu-id="36f99-105">Windows Server 2003 reached end of support on July 14th 2015.</span></span> <span data-ttu-id="36f99-106">Si vous hébergez vos sites Web sur un serveur IIS qui est Windows Server 2003, les applications Web est un moyen de faible risque, économique et problèmes tookeep vos sites Web en ligne et l’Assistant Migration de Web Apps peuvent aider à automatiser les processus de migration de hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="36f99-106">If you are currently hosting your websites on an IIS server that is Windows Server 2003, Web Apps is a low-risk, low-cost, and low-friction way tookeep your websites online, and Web Apps Migration Assistant can help automate hello migration process for you.</span></span> 
> 
> 

<span data-ttu-id="36f99-107">[Web Assistant de Migration applications](https://www.movemetothecloud.net/) peut analyser votre installation de serveur IIS, identifier les sites qui peuvent être migré tooApp Service, mettez en surbrillance tous les éléments qui ne peuvent pas être migrés ou sont non pris en charge sur la plateforme de hello et puis migrez vos sites Web et tooAzure de bases de données associées.</span><span class="sxs-lookup"><span data-stu-id="36f99-107">[Web Apps Migration Assistant](https://www.movemetothecloud.net/) can analyze your IIS server installation, identify which sites can be migrated tooApp Service, highlight any elements that cannot be migrated or are unsupported on hello platform, and then migrate your websites and associated databases tooAzure.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a><span data-ttu-id="36f99-108">Éléments vérifiés au cours de l’analyse de compatibilité</span><span class="sxs-lookup"><span data-stu-id="36f99-108">Elements Verified During Compatibility Analysis</span></span>
<span data-ttu-id="36f99-109">Hello, l’Assistant Migration crée un tooidentify de rapport de disponibilité entraîne de tout risque de poser problème ou des problèmes de blocage qui empêchent la réussite d’une migration à partir de local IIS tooAzure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="36f99-109">hello Migration Assistant creates a readiness report tooidentify any potential causes for concern or blocking issues which may prevent a successful migration from on-premises IIS tooAzure App Service Web Apps.</span></span> <span data-ttu-id="36f99-110">Certaines des toobe des éléments clés hello prenant en charge de sont :</span><span class="sxs-lookup"><span data-stu-id="36f99-110">Some of hello key items toobe aware of are:</span></span>

* <span data-ttu-id="36f99-111">Liaisons de port : Web Apps prend uniquement en charge le port 80 pour le trafic HTTP et le port 443 pour le trafic HTTPS.</span><span class="sxs-lookup"><span data-stu-id="36f99-111">Port Bindings – Web Apps only supports Port 80 for HTTP and Port 443 for HTTPS traffic.</span></span> <span data-ttu-id="36f99-112">Configurations de port différent seront ignorées et le trafic sera routé too80 ou 443.</span><span class="sxs-lookup"><span data-stu-id="36f99-112">Different port configurations will be ignored and traffic will be routed too80 or 443.</span></span> 
* <span data-ttu-id="36f99-113">Authentification : Web Apps prend en charge l’authentification anonyme par défaut et l’authentification par formulaire lorsqu’une application le spécifie.</span><span class="sxs-lookup"><span data-stu-id="36f99-113">Authentication – Web Apps supports Anonymous Authentication by default and Forms Authentication where specified by an application.</span></span> <span data-ttu-id="36f99-114">L'authentification Windows peut être utilisée uniquement en cas d'intégration à Azure Active Directory et ADFS.</span><span class="sxs-lookup"><span data-stu-id="36f99-114">Windows Authentication can be used by integrating with Azure Active Directory and ADFS only.</span></span> <span data-ttu-id="36f99-115">Aucune des autres formes d’authentification, telles que l’authentification de base, n’est prise en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="36f99-115">All other forms of authentication - for example, Basic Authentication - are not currently supported.</span></span> 
* <span data-ttu-id="36f99-116">Global Assembly Cache (GAC) : hello GAC n’est pas pris en charge dans les applications Web.</span><span class="sxs-lookup"><span data-stu-id="36f99-116">Global Assembly Cache (GAC) – hello GAC is not supported in Web Apps.</span></span> <span data-ttu-id="36f99-117">Si votre application fait référence à des assemblys dont vous déployez généralement toohello GAC, vous devez toodeploy toohello bin dossier d’application dans les applications Web.</span><span class="sxs-lookup"><span data-stu-id="36f99-117">If your application references assemblies which you usually deploy toohello GAC, you will need toodeploy toohello application bin folder in Web Apps.</span></span> 
* <span data-ttu-id="36f99-118">Mode de compatibilité IIS5 : non pris en charge dans Web Apps.</span><span class="sxs-lookup"><span data-stu-id="36f99-118">IIS5 Compatibility Mode – This is not supported in Web Apps.</span></span> 
* <span data-ttu-id="36f99-119">Pools d’applications – dans les applications Web, de chaque site et de ses applications enfants s’exécutent dans hello même pool d’applications.</span><span class="sxs-lookup"><span data-stu-id="36f99-119">Application Pools – In Web Apps, each site and its child applications run in hello same application pool.</span></span> <span data-ttu-id="36f99-120">Si votre site comporte plusieurs applications enfant utilisant plusieurs pools d’applications, les consolider le pool d’applications unique tooa avec des paramètres communs ou migrer chaque application web distinct de tooa application.</span><span class="sxs-lookup"><span data-stu-id="36f99-120">If your site has multiple child applications utilizing multiple application pools, consolidate them tooa single application pool with common settings or migrate each application tooa separate web app.</span></span>
* <span data-ttu-id="36f99-121">Des composants COM : Web Apps n’autorise pas l’inscription de hello de composants COM sur la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="36f99-121">COM Components – Web Apps does not allow hello registration of COM Components on hello platform.</span></span> <span data-ttu-id="36f99-122">Si vos applications ou sites Web disposer de tous les composants COM, vous devez les réécrire dans le code managé et les déployer avec le site Web de hello ou application.</span><span class="sxs-lookup"><span data-stu-id="36f99-122">If your websites or applications make use of any COM Components, you must rewrite them in managed code and deploy them with hello website or application.</span></span>
* <span data-ttu-id="36f99-123">Extensions ISAPI – Web Apps peut prend en charge hello Extensions ISAPI.</span><span class="sxs-lookup"><span data-stu-id="36f99-123">ISAPI Extensions – Web Apps can support hello use of ISAPI Extensions.</span></span> <span data-ttu-id="36f99-124">Toodo, hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="36f99-124">You need toodo hello following:</span></span>
  
  * <span data-ttu-id="36f99-125">déployer la DLL hello avec votre application web</span><span class="sxs-lookup"><span data-stu-id="36f99-125">deploy hello DLLs with your web app</span></span> 
  * <span data-ttu-id="36f99-126">inscrire la DLL hello à l’aide de [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span><span class="sxs-lookup"><span data-stu-id="36f99-126">register hello DLLs using [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span></span>
  * <span data-ttu-id="36f99-127">Placez un fichier applicationHost.xdt dans la racine du site hello avec contenu hello décrit dans « Chargée autorisant arbitrart ISAPI extensions toobe » [section de cet article](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span><span class="sxs-lookup"><span data-stu-id="36f99-127">place an applicationHost.xdt file in hello site root with hello content outlined in "Allowing arbitrart ISAPI extensions toobe loaded" [section of this article](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span></span> 
    
  
    
    <span data-ttu-id="36f99-128">Pour plus d’informations toouse des Transformations de documents XML avec votre site Web, consultez [transformer votre Site Web de Microsoft Azure](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).</span><span class="sxs-lookup"><span data-stu-id="36f99-128">For more examples of how toouse XML Document Transformations with your website, see [Transform your Microsoft Azure Web Site](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).</span></span>
* <span data-ttu-id="36f99-129">La migration ne concerne pas les autres composants comme SharePoint, les extensions serveur FrontPage (FPSE), les serveurs FTP et les certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="36f99-129">Other components like SharePoint, front page server extensions (FPSE), FTP, SSL certificates will not be migrated.</span></span>

## <a name="how-toouse-hello-web-apps-migration-assistant"></a><span data-ttu-id="36f99-130">Comment toouse hello l’Assistant Migration de Web Apps</span><span class="sxs-lookup"><span data-stu-id="36f99-130">How toouse hello Web Apps Migration Assistant</span></span>
<span data-ttu-id="36f99-131">Cette section parcourt un tootoomigrate exemple plusieurs sites Web qui utilisent une base de données SQL Server et en cours d’exécution sur un ordinateur local, Windows Server 2003 R2 (IIS 6.0) :</span><span class="sxs-lookup"><span data-stu-id="36f99-131">This section steps through an example tootoomigrate a few websites that use a SQL Server database and running on an on-premises Windows Server 2003 R2 (IIS 6.0) machine:</span></span>

1. <span data-ttu-id="36f99-132">Sur hello IIS server ou votre ordinateur client Accédez trop[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span><span class="sxs-lookup"><span data-stu-id="36f99-132">On hello IIS server or your client machine navigate too[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. <span data-ttu-id="36f99-133">Installez l’Assistant Migration d’applications Web en cliquant sur hello **dédié le serveur IIS** bouton.</span><span class="sxs-lookup"><span data-stu-id="36f99-133">Install Web Apps Migration Assistant by clicking on hello **Dedicated IIS Server** button.</span></span> <span data-ttu-id="36f99-134">Plus d’options sera options Bonjour futur proche.</span><span class="sxs-lookup"><span data-stu-id="36f99-134">More options will be options in hello near future.</span></span> 
3. <span data-ttu-id="36f99-135">Cliquez sur hello **Install Tool** bouton tooinstall Assistant de Migration les applications Web sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="36f99-135">Click hello **Install Tool** button tooinstall Web Apps Migration Assistant on your machine.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > <span data-ttu-id="36f99-136">Vous pouvez également cliquer sur **télécharger pour installation hors connexion** toodownload un fichier ZIP de fichiers de l’installation sur des serveurs non connectée toohello internet.</span><span class="sxs-lookup"><span data-stu-id="36f99-136">You can also click **Download for offline install** toodownload a ZIP file for installing on servers not connected toohello internet.</span></span> <span data-ttu-id="36f99-137">Vous pouvez également cliquer sur **télécharger un rapport de préparation de migration existant**, qui est un toowork option avancée avec un migration préparation rapport existant que vous avez créé précédemment (expliqué plus loin).</span><span class="sxs-lookup"><span data-stu-id="36f99-137">Or, you can click **Upload an existing migration readiness report**, which is an advanced option toowork with an existing migration readiness report that you previously generated (explained later).</span></span>
   > 
   > 
4. <span data-ttu-id="36f99-138">Bonjour **Application installer** , cliquez sur **installer** tooinstall sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="36f99-138">In hello **Application Install** screen, click **Install** tooinstall on your machine.</span></span> <span data-ttu-id="36f99-139">Cette opération installe également les dépendances associées telles que Web Deploy, DacFX et IIS, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="36f99-139">It will also install corresponding dependencies like Web Deploy, DacFX, and IIS, if needed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   <span data-ttu-id="36f99-140">Une fois installé, l’Assistant Migration Web Apps démarre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="36f99-140">Once installed, Web Apps Migration Assistant automatically starts.</span></span>
5. <span data-ttu-id="36f99-141">Choisissez **migrer des sites et des bases de données à partir d’un serveur distant de tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="36f99-141">Choose **Migrate sites and databases from a remote server tooAzure**.</span></span> <span data-ttu-id="36f99-142">Entrez les informations d’identification administratives hello pour le serveur distant de hello et cliquez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="36f99-142">Enter hello administrative credentials for hello remote server and click **Continue**.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   <span data-ttu-id="36f99-143">Vous pouvez bien sûr choisir toomigrate à partir du serveur local de hello.</span><span class="sxs-lookup"><span data-stu-id="36f99-143">You can of course choose toomigrate from hello local server.</span></span> <span data-ttu-id="36f99-144">option de Hello à distance est utile lorsque vous souhaitez que les sites Web de toomigrate à partir d’un serveur IIS de production.</span><span class="sxs-lookup"><span data-stu-id="36f99-144">hello remote option is useful when you want toomigrate websites from a production IIS server.</span></span>
   
   <span data-ttu-id="36f99-145">À ce stade inspecte l’outil de migration hello hello la configuration de votre serveur IIS, telles que des Sites, des Applications, des Pools d’applications et des dépendances tooidentify candidat sites Web pour la migration.</span><span class="sxs-lookup"><span data-stu-id="36f99-145">At this point hello migration tool will inspect hello your IIS server's configuration, such as Sites, Applications, Application Pools, and dependencies tooidentify candidate websites for migration.</span></span> 
6. <span data-ttu-id="36f99-146">capture d’écran Hello ci-dessous montre trois des sites Web – **Site Web par défaut**, **TimeTracker**, et **CommerceNet4**.</span><span class="sxs-lookup"><span data-stu-id="36f99-146">hello screenshot below shows three websites – **Default Web Site**, **TimeTracker**, and **CommerceNet4**.</span></span> <span data-ttu-id="36f99-147">Une base de données associée que nous souhaitons toomigrate disposent de.</span><span class="sxs-lookup"><span data-stu-id="36f99-147">All of them have an associated database that we want toomigrate.</span></span> <span data-ttu-id="36f99-148">Sélectionnez tous les sites hello vous comme tooassess et puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="36f99-148">Select all of hello sites you would like tooassess and then click **Next**.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. <span data-ttu-id="36f99-149">Cliquez sur **télécharger** rapport de disponibilité du tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="36f99-149">Click **Upload** tooupload hello readiness report.</span></span> <span data-ttu-id="36f99-150">Si vous cliquez sur **enregistrer le fichier localement**, vous pouvez exécuter l’outil de migration hello plus tard et téléchargement hello enregistré le rapport Disponibilité du comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="36f99-150">If you click **save file locally**, you can run hello migration tool again later and upload hello saved readiness report as noted earlier.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   <span data-ttu-id="36f99-151">Une fois que vous téléchargez des rapports de disponibilité hello, Azure effectue analyse de disponibilité du et les affiche hello de résultats.</span><span class="sxs-lookup"><span data-stu-id="36f99-151">Once you upload hello readiness report, Azure performs readiness analysis and shows you hello results.</span></span> <span data-ttu-id="36f99-152">Lire les détails d’évaluation hello pour chaque site Web et assurez-vous que vous comprenez ou avez traité tous les problèmes avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="36f99-152">Read hello assessment details for each website and make sure that you understand or have addressed all issues before you proceed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. <span data-ttu-id="36f99-153">Cliquez sur **commencer la Migration** toostart la migration hello. Vous serez maintenant redirigé tooAzure toolog à votre compte.</span><span class="sxs-lookup"><span data-stu-id="36f99-153">Click **Begin Migration** toostart hello migration.You will now be redirected tooAzure toolog into your account.</span></span> <span data-ttu-id="36f99-154">Il est important que vous vous connectiez à un compte dont l’abonnement Azure est actif.</span><span class="sxs-lookup"><span data-stu-id="36f99-154">It is important that you log in with an account that has an active Azure Subscription.</span></span> <span data-ttu-id="36f99-155">Si vous n’avez pas de compte Azure, vous pouvez vous inscrire [ici](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_) pour bénéficier d’un essai gratuit.</span><span class="sxs-lookup"><span data-stu-id="36f99-155">If you do not have an Azure account then you can sign up for a free trial [here](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_).</span></span> 
9. <span data-ttu-id="36f99-156">Sélectionnez le compte client hello, abonnement Azure et toouse de région pour vos applications web Azure migrés et les bases de données, puis cliquez sur **commencer la Migration**.</span><span class="sxs-lookup"><span data-stu-id="36f99-156">Select hello tenant account, Azure subscription and region toouse for your migrated Azure web apps and databases, and then click **Start Migration**.</span></span> <span data-ttu-id="36f99-157">Vous pouvez sélectionner toomigrate de sites Web hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="36f99-157">You can select hello websites toomigrate later.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. <span data-ttu-id="36f99-158">Sur l’écran suivant de hello vous pouvez modifier les paramètres de migration par défaut toohello, telles que :</span><span class="sxs-lookup"><span data-stu-id="36f99-158">On hello next screen you can make changes toohello default migration settings, such as:</span></span>
    
    * <span data-ttu-id="36f99-159">utiliser une base de données SQL Azure existante ou créer une base de données SQL Azure et configurer ses informations d'identification ;</span><span class="sxs-lookup"><span data-stu-id="36f99-159">use an existing Azure SQL Database or create a new Azure SQL Database, and configure its credentials</span></span>
    * <span data-ttu-id="36f99-160">Sélectionnez toomigrate de sites Web hello</span><span class="sxs-lookup"><span data-stu-id="36f99-160">select hello websites toomigrate</span></span>
    * <span data-ttu-id="36f99-161">définir des noms pour les applications web Azure hello et leurs bases de données SQL liés</span><span class="sxs-lookup"><span data-stu-id="36f99-161">define names for hello Azure web apps and their linked SQL databases</span></span>
    * <span data-ttu-id="36f99-162">personnaliser les paramètres globaux hello et les paramètres au niveau du site</span><span class="sxs-lookup"><span data-stu-id="36f99-162">customize hello global settings and site-level settings</span></span>
    
    <span data-ttu-id="36f99-163">capture d’écran Hello ci-dessous montre tous les sites Web de hello sélectionnés pour la migration avec les paramètres par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="36f99-163">hello screenshot below shows all hello websites selected for migration with hello default settings.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > <span data-ttu-id="36f99-164">Hello **activer Azure Active Directory** case à cocher dans les paramètres personnalisés s’intègre l’application web Azure hello [Azure Active Directory](../active-directory/active-directory-whatis.md) (hello **répertoire par défaut**).</span><span class="sxs-lookup"><span data-stu-id="36f99-164">hello **Enable Azure Active Directory** checkbox in custom settings integrates hello Azure web app with [Azure Active Directory](../active-directory/active-directory-whatis.md) (hello **Default Directory**).</span></span> <span data-ttu-id="36f99-165">Pour plus d’informations sur la synchronisation d’Azure Active Directory avec votre annuaire Azure Directory local, consultez la page [Intégration d’annuaire](http://msdn.microsoft.com/library/jj573653).</span><span class="sxs-lookup"><span data-stu-id="36f99-165">For more information on syncing Azure Active Directory with your on-premises Active Directory, see [Directory integration](http://msdn.microsoft.com/library/jj573653).</span></span>
    > 
    > 
11. <span data-ttu-id="36f99-166">Une fois que vous apportez toutes les modifications de hello souhaité, cliquez sur **créer** processus de migration toostart hello.</span><span class="sxs-lookup"><span data-stu-id="36f99-166">Once you make all hello desired changes, click **Create** toostart hello migration process.</span></span> <span data-ttu-id="36f99-167">outil de migration Hello créer une application de web de base de données SQL Azure et Azure hello et publier des bases de données et le contenu du site Web de hello.</span><span class="sxs-lookup"><span data-stu-id="36f99-167">hello migration tool will create hello Azure SQL Database and Azure web app, and then publish hello website content and databases.</span></span> <span data-ttu-id="36f99-168">progression de la migration Hello est clairement indiquée dans l’outil de migration hello, et vous verrez un écran récapitulatif fin hello, les sites de hello détails migrés, si elles ont échoué, les liens toohello nouvellement créé Azure web apps.</span><span class="sxs-lookup"><span data-stu-id="36f99-168">hello migration progress is clearly shown in hello migration tool, and you will see a summary screen at hello end, which details hello sites migrated, whether they were successful, links toohello newly-created Azure web apps.</span></span> 
    
    <span data-ttu-id="36f99-169">Si une erreur se produit pendant la migration, hello outil de migration va clairement indiquer des changements de hello échec et l’annulation de hello.</span><span class="sxs-lookup"><span data-stu-id="36f99-169">If any error occurs during migration, hello migration tool will clearly indicate hello failure and rollback hello changes.</span></span> <span data-ttu-id="36f99-170">Vous serez également le rapport d’erreurs en mesure de toosend hello directement l’équipe d’ingénierie toohello de l’équipe en cliquant sur hello **envoyer le rapport d’erreur** bouton, avec la pile des appels capturée échec hello et créer le corps du message.</span><span class="sxs-lookup"><span data-stu-id="36f99-170">You will also be able toosend hello error report directly toohello engineering team by clicking hello **Send Error Report** button, with hello captured failure call stack and build message body.</span></span> 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    <span data-ttu-id="36f99-171">Si migrer aboutit sans erreur, vous pouvez également cliquer sur hello **commenter** bouton, tooprovide de vos commentaires directement.</span><span class="sxs-lookup"><span data-stu-id="36f99-171">If migrate succeeds without errors, you can also click hello **Give Feedback** button tooprovide any feedback directly.</span></span> 
12. <span data-ttu-id="36f99-172">Cliquez sur hello liens toohello Azure web apps et vérifiez que la migration de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="36f99-172">Click hello links toohello Azure web apps and verify that hello migration has succeeded.</span></span>
13. <span data-ttu-id="36f99-173">Vous pouvez désormais gérer hello migrer des applications web dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="36f99-173">You can now manage hello migrated web apps in Azure App Service.</span></span> <span data-ttu-id="36f99-174">toodo, connectez-vous à hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36f99-174">toodo this, log into hello [Azure Portal](https://portal.azure.com).</span></span>
14. <span data-ttu-id="36f99-175">Bonjour portail Azure, ouvrez hello Web Apps panneau toosee vos sites migrés (représenté par les applications web), puis cliquez sur l’un d’eux toostart gestion hello web application, telles que la configuration de publication, création de sauvegardes, échelle et surveillance de l’utilisation continue ou performances.</span><span class="sxs-lookup"><span data-stu-id="36f99-175">In hello Azure Portal, open hello Web Apps blade toosee your migrated websites (shown as web apps), then click on any one of them toostart managing hello web app, such as configuring continuous publishing, creating backups, autoscaling, and monitoring usage or performance.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> <span data-ttu-id="36f99-176">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="36f99-176">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="36f99-177">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="36f99-177">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="36f99-178">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="36f99-178">What's changed</span></span>
* <span data-ttu-id="36f99-179">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="36f99-179">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
