---
title: "rôles aaaTroubleshoot qui échouent toostart | Documents Microsoft"
description: "Voici quelques-unes des raisons pour lesquelles un rôle de Service Cloud peut échouer toostart. Problèmes de toothese solutions sont également fournies."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="d16d7-104">Résoudre les problèmes de rôle Service de cloud computing toostart</span><span class="sxs-lookup"><span data-stu-id="d16d7-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="d16d7-105">Voici certains problèmes courants et solutions connexes tooAzure Services de cloud computing rôles qui échouent toostart.</span><span class="sxs-lookup"><span data-stu-id="d16d7-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="d16d7-106">DLL ou dépendances manquantes</span><span class="sxs-lookup"><span data-stu-id="d16d7-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="d16d7-107">Les rôles qui ne répondent pas ou qui basculent sans cesse entre les états **Initialisation**, **Occupé** et **Arrêt** peuvent être affectés par l’absence de bibliothèques DLL ou d’assemblys.</span><span class="sxs-lookup"><span data-stu-id="d16d7-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="d16d7-108">Symptômes liés à l’absence de bibliothèques DLL ou d’assemblys :</span><span class="sxs-lookup"><span data-stu-id="d16d7-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="d16d7-109">Votre instance de rôle alterne entre les états **Initialisation**, **Occupé** et **Arrêt**.</span><span class="sxs-lookup"><span data-stu-id="d16d7-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="d16d7-110">Votre instance de rôle a été déplacé trop**prêt** , mais si vous naviguez d’application web de tooyour, hello ne s’affiche pas.</span><span class="sxs-lookup"><span data-stu-id="d16d7-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="d16d7-111">Plusieurs méthodes sont recommandées pour rechercher une solution à ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="d16d7-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="d16d7-112">Diagnostiquer les problèmes de DLL manquante dans un rôle web</span><span class="sxs-lookup"><span data-stu-id="d16d7-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="d16d7-113">Lorsque vous accédez tooa site Web déployé dans un rôle web et navigateur de hello affiche un serveur erreur similaires toohello suite, il peut indiquer qu’une DLL est manquante.</span><span class="sxs-lookup"><span data-stu-id="d16d7-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

![Erreur de serveur dans l’application « / ».](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="d16d7-115">Diagnostiquer les problèmes en désactivant les erreurs personnalisées</span><span class="sxs-lookup"><span data-stu-id="d16d7-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="d16d7-116">Informations plus complètes sur l’erreur sont consultables en configurant web.config hello pour tooOff mode erreurs personnalisées de la tooset rôle hello web hello et de redéployer hello service.</span><span class="sxs-lookup"><span data-stu-id="d16d7-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="d16d7-117">tooview plus complètes que les erreurs sans l’aide du Bureau à distance :</span><span class="sxs-lookup"><span data-stu-id="d16d7-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="d16d7-118">Ouvrez la solution de hello dans Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d16d7-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="d16d7-119">Bonjour **l’Explorateur de solutions**, recherchez le fichier web.config de hello et ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="d16d7-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="d16d7-120">Dans le fichier web.config hello, localisez la section system.web de hello et ajouter hello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="d16d7-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="d16d7-121">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-121">Save hello file.</span></span>
5. <span data-ttu-id="d16d7-122">Réempaquetez et redéployez hello service.</span><span class="sxs-lookup"><span data-stu-id="d16d7-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="d16d7-123">Une fois que le service de hello est redéployé, vous verrez un message d’erreur de nom hello Hello manquant assembly ou une DLL.</span><span class="sxs-lookup"><span data-stu-id="d16d7-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="d16d7-124">Diagnostiquer les problèmes en affichant les erreurs hello à distance</span><span class="sxs-lookup"><span data-stu-id="d16d7-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="d16d7-125">Vous pouvez utiliser le rôle de bureau à distance tooaccess hello et afficher des informations plus complètes sur l’erreur à distance.</span><span class="sxs-lookup"><span data-stu-id="d16d7-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="d16d7-126">Utilisez hello suivant des erreurs de hello tooview étapes à l’aide du Bureau à distance :</span><span class="sxs-lookup"><span data-stu-id="d16d7-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="d16d7-127">Assurez-vous que le Kit de développement logiciel (SDK) Azure 1.3 ou ultérieur est installé.</span><span class="sxs-lookup"><span data-stu-id="d16d7-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="d16d7-128">Au cours du déploiement hello de solution hello à l’aide de Visual Studio, choisissez trop « Configurer les connexions Bureau à distance... ».</span><span class="sxs-lookup"><span data-stu-id="d16d7-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="d16d7-129">Pour plus d’informations sur la configuration de connexion Bureau à distance de hello, consultez [à l’aide de bureau à distance avec des rôles Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d16d7-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="d16d7-130">Dans hello classique du portail Microsoft Azure, une fois que l’instance de hello présente l’état de **prêt**, cliquez sur une des instances de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="d16d7-131">Cliquez sur hello **Connect** icône Bonjour **l’accès à distance** zone du ruban de hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="d16d7-132">Connectez-vous toohello virtuels à l’aide des informations d’identification hello qui ont été spécifiées lors de la configuration du Bureau à distance hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="d16d7-133">Ouvrez une fenêtre de commandes.</span><span class="sxs-lookup"><span data-stu-id="d16d7-133">Open a command window.</span></span>
7. <span data-ttu-id="d16d7-134">Saisissez `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="d16d7-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="d16d7-135">Notez la valeur d’adresse IPV4 hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="d16d7-136">Ouvrez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d16d7-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="d16d7-137">Tapez les adresses hello hello nom et application web de hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="d16d7-138">Par exemple, `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="d16d7-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="d16d7-139">Navigation toohello site Web sera retournent désormais des messages d’erreur plus explicites :</span><span class="sxs-lookup"><span data-stu-id="d16d7-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="d16d7-140">Erreur de serveur dans l’application « / ».</span><span class="sxs-lookup"><span data-stu-id="d16d7-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="d16d7-141">Description : Une exception non gérée s’est produite lors de l’exécution de hello de requête web actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="d16d7-142">Vérifiez la trace de la pile pour plus d’informations sur l’erreur de hello hello et son origine dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="d16d7-143">Détails de l’exception : System.IO.FIleNotFoundException : impossible de charger le fichier ou l’assembly « Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35 » ou l’une de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="d16d7-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="d16d7-144">Hello introuvable fichier hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="d16d7-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="d16d7-145">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d16d7-145">For example:</span></span>

![Erreur de serveur explicite dans l’application « / »](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="d16d7-147">Diagnostiquer les problèmes à l’aide d’émulateur de calcul hello</span><span class="sxs-lookup"><span data-stu-id="d16d7-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="d16d7-148">Vous pouvez utiliser hello Microsoft Azure compute emulator toodiagnose et résoudre les problèmes de dépendances manquantes et les erreurs de web.config.</span><span class="sxs-lookup"><span data-stu-id="d16d7-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="d16d7-149">Pour obtenir de meilleurs résultats à l’aide de cette méthode de diagnostic, vous devez utiliser un ordinateur ou une machine virtuelle disposant d’une nouvelle installation de Windows.</span><span class="sxs-lookup"><span data-stu-id="d16d7-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="d16d7-150">toobest simuler hello environnement Azure, utilisez Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="d16d7-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="d16d7-151">Installer la version autonome de hello Hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d16d7-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d16d7-152">Sur l’ordinateur de développement hello, générez le projet de service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="d16d7-153">Dans l’Explorateur Windows, accédez à toohello le dossier bin\debug du projet de service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="d16d7-154">Copier le dossier .csx hello et .cscfg ordinateur toohello que vous utilisez des problèmes de hello toodebug de fichiers.</span><span class="sxs-lookup"><span data-stu-id="d16d7-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="d16d7-155">Sur hello propre ordinateur, ouvrez une fenêtre d’invite de commandes du Kit de développement logiciel Azure et tapez `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="d16d7-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="d16d7-156">À l’invite de commandes hello, tapez `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="d16d7-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="d16d7-157">Démarrage de rôle de hello, vous verrez des informations d’erreur détaillées dans Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d16d7-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="d16d7-158">Vous pouvez également utiliser les outils de dépannage standard de Windows toofurther diagnostiquer le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="d16d7-159">Diagnostiquer les problèmes à l’aide d’IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="d16d7-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="d16d7-160">Pour les rôles de travail et les rôles web qui utilisent .NET Framework 4, vous pouvez utiliser l’utilitaire [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), qui est disponible dans Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d16d7-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="d16d7-161">Avec IntelliTrace est activé, suivez ces services de hello toodeploy comme suit :</span><span class="sxs-lookup"><span data-stu-id="d16d7-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="d16d7-162">Vérifiez que le Kit de développement logiciel (SDK) Azure 1.3 ou ultérieur est installé.</span><span class="sxs-lookup"><span data-stu-id="d16d7-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="d16d7-163">Déployer la solution de hello à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d16d7-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="d16d7-164">Pendant le déploiement, vérifiez hello **activer IntelliTrace pour les rôles .NET 4** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="d16d7-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="d16d7-165">Une fois que le démarrage de l’instance de hello, ouvrez hello **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="d16d7-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="d16d7-166">Développez hello **Azure\\Services de cloud computing** nœud et recherchez hello déploiement.</span><span class="sxs-lookup"><span data-stu-id="d16d7-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="d16d7-167">Étendre les déploiements de hello jusqu'à ce que les instances de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="d16d7-168">Avec le bouton droit sur une des instances de hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="d16d7-169">Sélectionnez **Afficher les fichiers journaux IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="d16d7-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="d16d7-170">Hello **résumé IntelliTrace** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d16d7-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="d16d7-171">Localiser la section exceptions hello hello résumé.</span><span class="sxs-lookup"><span data-stu-id="d16d7-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="d16d7-172">S’il existe des exceptions, la section de hello est étiquetée **données d’Exception**.</span><span class="sxs-lookup"><span data-stu-id="d16d7-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="d16d7-173">Développez hello **données d’Exception** et recherchez **System.IO.FileNotFoundException** suivant de toohello erreurs similaires :</span><span class="sxs-lookup"><span data-stu-id="d16d7-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![Données d’exception, fichier ou assembly manquant](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="d16d7-175">Résoudre les problèmes de DLL et d’assemblys manquants</span><span class="sxs-lookup"><span data-stu-id="d16d7-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="d16d7-176">tooaddress manquant des erreurs de DLL et d’assembly, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d16d7-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="d16d7-177">Ouvrez la solution de hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d16d7-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="d16d7-178">Dans **l’Explorateur de solutions**, ouvrez hello **références** dossier.</span><span class="sxs-lookup"><span data-stu-id="d16d7-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="d16d7-179">Cliquez sur assembly hello identifié dans l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="d16d7-180">Bonjour **propriétés** volet, recherchez **propriété copie locale** et la valeur hello trop**True**.</span><span class="sxs-lookup"><span data-stu-id="d16d7-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="d16d7-181">Redéployez le service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="d16d7-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="d16d7-182">Une fois que vous avez vérifié que toutes les erreurs ont été corrigées, vous pouvez déployer le service de hello sans vérification hello **activer IntelliTrace pour les rôles .NET 4** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="d16d7-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d16d7-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d16d7-183">Next steps</span></span>
<span data-ttu-id="d16d7-184">Affichez plus d’ [articles de résolution des problèmes](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) liés aux services cloud.</span><span class="sxs-lookup"><span data-stu-id="d16d7-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="d16d7-185">toolearn comment le rôle du service cloud tootroubleshoot problèmes à l’aide de données de diagnostic d’ordinateur PaaS Azure, consultez [série du blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="d16d7-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
