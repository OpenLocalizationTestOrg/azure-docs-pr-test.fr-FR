---
title: "Résoudre les problèmes de démarrage des rôles | Microsoft Docs"
description: "Vous trouverez ici quelques raisons courantes des problèmes de démarrage d’un rôle de service cloud. Nous vous présentons également des solutions à ces problèmes."
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
ms.openlocfilehash: 7d956192e8b9c3688b8b6f0108bd9296f66fbd62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-to-start"></a><span data-ttu-id="64df4-104">Résoudre les problèmes de démarrage des rôles de service cloud</span><span class="sxs-lookup"><span data-stu-id="64df4-104">Troubleshoot Cloud Service roles that fail to start</span></span>
<span data-ttu-id="64df4-105">Voici des solutions à quelques problèmes courants liés à l’échec du démarrage des rôles Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="64df4-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="64df4-106">DLL ou dépendances manquantes</span><span class="sxs-lookup"><span data-stu-id="64df4-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="64df4-107">Les rôles qui ne répondent pas ou qui basculent sans cesse entre les états **Initialisation**, **Occupé** et **Arrêt** peuvent être affectés par l’absence de bibliothèques DLL ou d’assemblys.</span><span class="sxs-lookup"><span data-stu-id="64df4-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="64df4-108">Symptômes liés à l’absence de bibliothèques DLL ou d’assemblys :</span><span class="sxs-lookup"><span data-stu-id="64df4-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="64df4-109">Votre instance de rôle alterne entre les états **Initialisation**, **Occupé** et **Arrêt**.</span><span class="sxs-lookup"><span data-stu-id="64df4-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="64df4-110">Votre instance de rôle est passée à l’état **Prêt** , mais la page ne s’affiche pas lorsque vous accédez à votre application web.</span><span class="sxs-lookup"><span data-stu-id="64df4-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span></span>

<span data-ttu-id="64df4-111">Plusieurs méthodes sont recommandées pour rechercher une solution à ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="64df4-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="64df4-112">Diagnostiquer les problèmes de DLL manquante dans un rôle web</span><span class="sxs-lookup"><span data-stu-id="64df4-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="64df4-113">Lorsque vous accédez à un site web déployé dans un rôle web et que le navigateur affiche une erreur de serveur semblable à ce qui suit, cela peut indiquer qu’une bibliothèque DLL est manquante.</span><span class="sxs-lookup"><span data-stu-id="64df4-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span></span>

![Erreur de serveur dans l’application « / ».](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="64df4-115">Diagnostiquer les problèmes en désactivant les erreurs personnalisées</span><span class="sxs-lookup"><span data-stu-id="64df4-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="64df4-116">Vous pouvez afficher des informations plus complètes sur les erreurs en configurant le fichier web.config du rôle web pour qu’il désactive le mode d’erreur personnalisée et en redéployant le service.</span><span class="sxs-lookup"><span data-stu-id="64df4-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span></span>

<span data-ttu-id="64df4-117">Pour afficher des erreurs plus détaillées sans utiliser le Bureau à distance :</span><span class="sxs-lookup"><span data-stu-id="64df4-117">To view more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="64df4-118">Ouvrez la solution dans Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="64df4-118">Open the solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="64df4-119">Dans l’ **Explorateur de solutions**, recherchez et ouvrez le fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="64df4-119">In the **Solution Explorer**, locate the web.config file and open it.</span></span>
3. <span data-ttu-id="64df4-120">Dans le fichier web.config, recherchez la section system.web et ajoutez la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="64df4-120">In the web.config file, locate the system.web section and add the following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="64df4-121">Enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="64df4-121">Save the file.</span></span>
5. <span data-ttu-id="64df4-122">Recréez le package et redéployez le service.</span><span class="sxs-lookup"><span data-stu-id="64df4-122">Repackage and redeploy the service.</span></span>

<span data-ttu-id="64df4-123">Une fois le service redéployé, un message d’erreur s’affiche avec le nom de la DLL ou de l’assembly manquant.</span><span class="sxs-lookup"><span data-stu-id="64df4-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-the-error-remotely"></a><span data-ttu-id="64df4-124">Diagnostiquer les problèmes en affichant l’erreur à distance</span><span class="sxs-lookup"><span data-stu-id="64df4-124">Diagnose issues by viewing the error remotely</span></span>
<span data-ttu-id="64df4-125">Vous pouvez utiliser le Bureau à distance pour accéder au rôle et afficher des informations plus complètes sur l’erreur à distance.</span><span class="sxs-lookup"><span data-stu-id="64df4-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span></span> <span data-ttu-id="64df4-126">Pour afficher les erreurs à l’aide du Bureau à distance, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="64df4-126">Use the following steps to view the errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="64df4-127">Assurez-vous que le Kit de développement logiciel (SDK) Azure 1.3 ou ultérieur est installé.</span><span class="sxs-lookup"><span data-stu-id="64df4-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="64df4-128">Lors du déploiement de la solution à l’aide de Visual Studio, choisissez Configurer les connexions Bureau à distance...</span><span class="sxs-lookup"><span data-stu-id="64df4-128">During the deployment of the solution by using Visual Studio, choose to “Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="64df4-129">Pour plus d’informations sur la configuration de la connexion Bureau à distance, consultez l’article [Utilisation du Bureau à distance avec des rôles Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="64df4-129">For more information on configuring the Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="64df4-130">Dans le portail Microsoft Azure Classic, cliquez sur l’une des instances de rôle une fois que l’instance affiche l’état **Prêt**.</span><span class="sxs-lookup"><span data-stu-id="64df4-130">In the Microsoft Azure classic portal, once the instance shows a status of **Ready**, click one of the role instances.</span></span>
4. <span data-ttu-id="64df4-131">Cliquez sur l’icône **Connexion** dans la zone **Accès à distance** du ruban.</span><span class="sxs-lookup"><span data-stu-id="64df4-131">Click the **Connect** icon in the **Remote Access** area of the ribbon.</span></span>
5. <span data-ttu-id="64df4-132">Connectez-vous à la machine virtuelle à l’aide des informations d’identification spécifiées lors de la configuration du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="64df4-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span></span>
6. <span data-ttu-id="64df4-133">Ouvrez une fenêtre de commandes.</span><span class="sxs-lookup"><span data-stu-id="64df4-133">Open a command window.</span></span>
7. <span data-ttu-id="64df4-134">Saisissez `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="64df4-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="64df4-135">Notez la valeur de l’adresse IPV4.</span><span class="sxs-lookup"><span data-stu-id="64df4-135">Note the IPV4 Address value.</span></span>
9. <span data-ttu-id="64df4-136">Ouvrez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="64df4-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="64df4-137">Entrez l’adresse et le nom de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="64df4-137">Type the address and the name of the web application.</span></span> <span data-ttu-id="64df4-138">Par exemple, `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="64df4-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="64df4-139">L’accès au site web renvoie maintenant des messages d’erreur plus explicites :</span><span class="sxs-lookup"><span data-stu-id="64df4-139">Navigating to the website will now return more explicit error messages:</span></span>

* <span data-ttu-id="64df4-140">Erreur de serveur dans l’application « / ».</span><span class="sxs-lookup"><span data-stu-id="64df4-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="64df4-141">Description : une exception non gérée s’est produite lors de l’exécution de la requête Web en cours.</span><span class="sxs-lookup"><span data-stu-id="64df4-141">Description: An unhandled exception occurred during the execution of the current web request.</span></span> <span data-ttu-id="64df4-142">Veuillez consulter l’arborescence des appels de procédure pour plus d’informations sur l’erreur et sa source dans le code.</span><span class="sxs-lookup"><span data-stu-id="64df4-142">Please review the stack trace for more information about the error and where it originated in the code.</span></span>
* <span data-ttu-id="64df4-143">Détails de l’exception : System.IO.FIleNotFoundException : impossible de charger le fichier ou l’assembly « Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35 » ou l’une de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="64df4-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="64df4-144">Le système ne peut pas trouver le fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="64df4-144">The system cannot find the file specified.</span></span>

<span data-ttu-id="64df4-145">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="64df4-145">For example:</span></span>

![Erreur de serveur explicite dans l’application « / »](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-the-compute-emulator"></a><span data-ttu-id="64df4-147">Diagnostiquer les problèmes à l’aide de l’émulateur de calcul</span><span class="sxs-lookup"><span data-stu-id="64df4-147">Diagnose issues by using the compute emulator</span></span>
<span data-ttu-id="64df4-148">Vous pouvez utiliser l’émulateur de calcul Microsoft Azure pour diagnostiquer et résoudre les problèmes de dépendances manquantes et les erreurs du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="64df4-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="64df4-149">Pour obtenir de meilleurs résultats à l’aide de cette méthode de diagnostic, vous devez utiliser un ordinateur ou une machine virtuelle disposant d’une nouvelle installation de Windows.</span><span class="sxs-lookup"><span data-stu-id="64df4-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="64df4-150">Pour mieux simuler l’environnement Azure, utilisez Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="64df4-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="64df4-151">Installez la version autonome du [SDK Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="64df4-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="64df4-152">Sur l’ordinateur de développement, générez le projet de service cloud.</span><span class="sxs-lookup"><span data-stu-id="64df4-152">On the development machine, build the cloud service project.</span></span>
3. <span data-ttu-id="64df4-153">Dans l’Explorateur Windows, accédez au dossier bin\debug du projet de service cloud.</span><span class="sxs-lookup"><span data-stu-id="64df4-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span></span>
4. <span data-ttu-id="64df4-154">Copiez le dossier .csx et le fichier .cscfg sur l’ordinateur que vous utilisez pour déboguer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="64df4-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span></span>
5. <span data-ttu-id="64df4-155">Sur le nouvel ordinateur, ouvrez une fenêtre d’invite de commandes du Kit de développement logiciel (SDK) Azure et tapez `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="64df4-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="64df4-156">Dans l’invite de commandes, tapez `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="64df4-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="64df4-157">Au démarrage du rôle, le détail de l’erreur s’affiche dans Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="64df4-157">When the role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="64df4-158">Vous pouvez également utiliser les outils de dépannage Windows standard pour diagnostiquer le problème.</span><span class="sxs-lookup"><span data-stu-id="64df4-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="64df4-159">Diagnostiquer les problèmes à l’aide d’IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="64df4-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="64df4-160">Pour les rôles de travail et les rôles web qui utilisent .NET Framework 4, vous pouvez utiliser l’utilitaire [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), qui est disponible dans Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="64df4-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="64df4-161">Pour déployer le service avec la fonction IntelliTrace activée, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="64df4-161">Follow these steps to deploy the service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="64df4-162">Vérifiez que le Kit de développement logiciel (SDK) Azure 1.3 ou ultérieur est installé.</span><span class="sxs-lookup"><span data-stu-id="64df4-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="64df4-163">Déployez la solution à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="64df4-163">Deploy the solution by using Visual Studio.</span></span> <span data-ttu-id="64df4-164">Au cours du déploiement, cochez la case **Activer IntelliTrace pour les rôles .NET 4** .</span><span class="sxs-lookup"><span data-stu-id="64df4-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="64df4-165">Une fois l’instance démarrée, ouvrez l’ **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="64df4-165">Once the instance starts, open the **Server Explorer**.</span></span>
4. <span data-ttu-id="64df4-166">Développez le nœud **Azure\\Cloud Services** et recherchez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="64df4-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span></span>
5. <span data-ttu-id="64df4-167">Développez le déploiement jusqu’à ce que les instances de rôle s’affichent.</span><span class="sxs-lookup"><span data-stu-id="64df4-167">Expand the deployment until you see the role instances.</span></span> <span data-ttu-id="64df4-168">Cliquez avec le bouton droit sur l’une des instances.</span><span class="sxs-lookup"><span data-stu-id="64df4-168">Right-click on one of the instances.</span></span>
6. <span data-ttu-id="64df4-169">Sélectionnez **Afficher les fichiers journaux IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="64df4-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="64df4-170">Le **Résumé IntelliTrace** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="64df4-170">The **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="64df4-171">Recherchez la section du résumé relative aux exceptions.</span><span class="sxs-lookup"><span data-stu-id="64df4-171">Locate the exceptions section of the summary.</span></span> <span data-ttu-id="64df4-172">S’il existe des exceptions, la section s’intitule **Données d’exception**.</span><span class="sxs-lookup"><span data-stu-id="64df4-172">If there are exceptions, the section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="64df4-173">Développez les **Données d’exception** et recherchez les erreurs **System.IO.FileNotFoundException** semblables à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="64df4-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span></span>

![Données d’exception, fichier ou assembly manquant](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="64df4-175">Résoudre les problèmes de DLL et d’assemblys manquants</span><span class="sxs-lookup"><span data-stu-id="64df4-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="64df4-176">Pour résoudre les erreurs liées à des DLL et des assemblies manquants, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="64df4-176">To address missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="64df4-177">Ouvrez la solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="64df4-177">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="64df4-178">Dans l’**Explorateur de solutions**, ouvrez le dossier **Références**.</span><span class="sxs-lookup"><span data-stu-id="64df4-178">In **Solution Explorer**, open the **References** folder.</span></span>
3. <span data-ttu-id="64df4-179">Cliquez sur l’assembly identifié dans l’erreur.</span><span class="sxs-lookup"><span data-stu-id="64df4-179">Click the assembly identified in the error.</span></span>
4. <span data-ttu-id="64df4-180">Dans le volet **Propriétés**, recherchez la propriété **Copy Local** et définissez sa valeur sur **True**.</span><span class="sxs-lookup"><span data-stu-id="64df4-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span></span>
5. <span data-ttu-id="64df4-181">Redéployez le service cloud.</span><span class="sxs-lookup"><span data-stu-id="64df4-181">Redeploy the cloud service.</span></span>

<span data-ttu-id="64df4-182">Après avoir vérifié que toutes les erreurs ont été corrigées, vous pouvez déployer le service sans cocher la case **Activer IntelliTrace pour les rôles .NET 4** .</span><span class="sxs-lookup"><span data-stu-id="64df4-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64df4-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64df4-183">Next steps</span></span>
<span data-ttu-id="64df4-184">Affichez plus d’ [articles de résolution des problèmes](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) liés aux services cloud.</span><span class="sxs-lookup"><span data-stu-id="64df4-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="64df4-185">Pour découvrir comment résoudre les problèmes liés aux rôles de service cloud à l’aide des données de diagnostic de calcul PaaS Azure, consultez la [série de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="64df4-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
