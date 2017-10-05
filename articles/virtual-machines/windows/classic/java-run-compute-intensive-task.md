---
title: "Application Java nécessitant beaucoup de ressources système sur une machine virtuelle | Microsoft Docs"
description: "Apprenez à créer une machine virtuelle Azure qui exécute une application de calcul intensif Java qu'une autre application Java peut surveiller."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8c51c0bb37e25ad61fe58a85dd641dabe0a1958c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-run-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="cb6de-103">Exécution d'une tâche nécessitant beaucoup de ressources en langage Java sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cb6de-103">How to run a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="cb6de-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cb6de-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cb6de-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="cb6de-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="cb6de-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb6de-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="cb6de-107">Azure permet d'utiliser une machine virtuelle pour gérer les tâches nécessitant beaucoup de ressources.</span><span class="sxs-lookup"><span data-stu-id="cb6de-107">With Azure, you can use a virtual machine to handle compute-intensive tasks.</span></span> <span data-ttu-id="cb6de-108">Par exemple, une machine virtuelle peut gérer des tâches et fournir des résultats à des ordinateurs clients ou à des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="cb6de-108">For example, a virtual machine can handle tasks and deliver results to client machines or mobile applications.</span></span> <span data-ttu-id="cb6de-109">Après avoir lu cet article, vous serez en mesure de créer une machine virtuelle exécutée sur une application Java nécessitant beaucoup de ressources et pouvant être surveillée par une autre application Java.</span><span class="sxs-lookup"><span data-stu-id="cb6de-109">After reading this article, you will have an understanding of how to create a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="cb6de-110">Ce didacticiel part du principe que vous savez créer des applications console Java, importer des bibliothèques dans votre application Java et générer une archive Java (JAR).</span><span class="sxs-lookup"><span data-stu-id="cb6de-110">This tutorial assumes you know how to create Java console applications, can import libraries to your Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="cb6de-111">Aucune connaissance de Microsoft Azure n'est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cb6de-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="cb6de-112">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb6de-112">You will learn:</span></span>

* <span data-ttu-id="cb6de-113">créer une machine virtuelle déjà dotée d'un kit de développement Java (JDK) ;</span><span class="sxs-lookup"><span data-stu-id="cb6de-113">How to create a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="cb6de-114">vous connecter à distance à votre machine virtuelle ;</span><span class="sxs-lookup"><span data-stu-id="cb6de-114">How to remotely log in to your virtual machine.</span></span>
* <span data-ttu-id="cb6de-115">création d'un espace de noms Service Bus ;</span><span class="sxs-lookup"><span data-stu-id="cb6de-115">How to create a service bus namespace.</span></span>
* <span data-ttu-id="cb6de-116">créer une application Java exécutant une tâche qui nécessite beaucoup de ressources ;</span><span class="sxs-lookup"><span data-stu-id="cb6de-116">How to create a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="cb6de-117">créer une application Java surveillant la progression de la tâche qui nécessite beaucoup de ressources ;</span><span class="sxs-lookup"><span data-stu-id="cb6de-117">How to create a Java application that monitors the progress of the compute-intensive task.</span></span>
* <span data-ttu-id="cb6de-118">exécuter les applications Java ;</span><span class="sxs-lookup"><span data-stu-id="cb6de-118">How to run the Java applications.</span></span>
* <span data-ttu-id="cb6de-119">arrêter les applications Java.</span><span class="sxs-lookup"><span data-stu-id="cb6de-119">How to stop the Java applications.</span></span>

<span data-ttu-id="cb6de-120">Dans le cadre de ce didacticiel, la tâche nécessitant beaucoup de ressources repose sur le problème du voyageur de commerce.</span><span class="sxs-lookup"><span data-stu-id="cb6de-120">This tutorial will use the Traveling Salesman Problem for the compute-intensive task.</span></span> <span data-ttu-id="cb6de-121">Vous trouverez ci-dessous un exemple d'application Java qui exécute la tâche nécessitant beaucoup de ressources.</span><span class="sxs-lookup"><span data-stu-id="cb6de-121">The following is an example of the Java application running the compute-intensive task.</span></span>

![Résolution du problème du voyageur de commerce][solver_output]

<span data-ttu-id="cb6de-123">Vous trouverez ci-dessous un exemple d'application Java qui surveille la tâche nécessitant beaucoup de ressources :</span><span class="sxs-lookup"><span data-stu-id="cb6de-123">The following is an example of the Java application monitoring the compute-intensive task.</span></span>

![Client du problème du voyageur de commerce][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="cb6de-125">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cb6de-125">To create a virtual machine</span></span>
1. <span data-ttu-id="cb6de-126">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cb6de-126">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="cb6de-127">Cliquez sur **New**, sur **Compute**, sur **Virtual machine**, puis sur **From Gallery**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="cb6de-128">Dans la boîte de dialogue **Sélectionner une image de machine virtuelle**, sélectionnez **Windows Server 2012 JDK 7**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-128">In the **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="cb6de-129">Notez que **Windows Server 2012 JDK 6** est disponible si vous ne pouvez pas exécuter certaines de vos applications héritées dans JDK 7.</span><span class="sxs-lookup"><span data-stu-id="cb6de-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready to run in JDK 7.</span></span>
4. <span data-ttu-id="cb6de-130">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-130">Click **Next**.</span></span>
5. <span data-ttu-id="cb6de-131">Dans la boîte de dialogue **Configuration de la machine virtuelle** :</span><span class="sxs-lookup"><span data-stu-id="cb6de-131">In the **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="cb6de-132">Entrez un nom pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cb6de-132">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="cb6de-133">Entrez la taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cb6de-133">Specify the size to use for the virtual machine.</span></span>
   3. <span data-ttu-id="cb6de-134">Entrez un nom pour l'administrateur dans le champ **Nom d'utilisateur** .</span><span class="sxs-lookup"><span data-stu-id="cb6de-134">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="cb6de-135">Notez le nom et le mot de passe que vous allez entrer, car vous les utiliserez pour vous connecter à distance à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cb6de-135">Remember this name and the password you will enter next, you will use them when you remotely log in to the virtual machine.</span></span>
   4. <span data-ttu-id="cb6de-136">Entrez un mot de passe dans le champ **Nouveau mot de passe**, puis entrez-le de nouveau dans le champ **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-136">Enter a password in the **New password** field, and re-enter it in the **Confirm** field.</span></span> <span data-ttu-id="cb6de-137">Il s'agit du mot de passe du compte Administrateur.</span><span class="sxs-lookup"><span data-stu-id="cb6de-137">This is the Administrator account password.</span></span>
   5. <span data-ttu-id="cb6de-138">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-138">Click **Next**.</span></span>
6. <span data-ttu-id="cb6de-139">Dans la boîte de dialogue **Configuration de la machine virtuelle** suivante :</span><span class="sxs-lookup"><span data-stu-id="cb6de-139">In the next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="cb6de-140">Pour le **Service cloud**, utilisez le paramètre par défaut **Créer un nouveau service cloud**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-140">For **Cloud service**, use the default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="cb6de-141">La valeur du **Nom du cloud Service DNS** doit être unique sur cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="cb6de-141">The value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="cb6de-142">Si nécessaire, modifiez cette valeur afin qu'Azure indique qu'elle est unique.</span><span class="sxs-lookup"><span data-stu-id="cb6de-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="cb6de-143">Indiquez une région, un groupe d'affinités ou un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cb6de-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="cb6de-144">Dans le cadre de ce didacticiel, indiquez une région comme **Bretagne**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="cb6de-145">Pour **Storage Account**, sélectionnez **Use an automatically generated storage account**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="cb6de-146">Pour **Availability Set**, sélectionnez **(None)**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="cb6de-147">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-147">Click **Next**.</span></span>
7. <span data-ttu-id="cb6de-148">Dans la dernière boîte de dialogue **Configuration de la machine virtuelle** :</span><span class="sxs-lookup"><span data-stu-id="cb6de-148">In the final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="cb6de-149">Validez les entrées de points de terminaison par défaut.</span><span class="sxs-lookup"><span data-stu-id="cb6de-149">Accept the default endpoint entries.</span></span>
   2. <span data-ttu-id="cb6de-150">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-150">Click **Complete**.</span></span>

## <a name="to-remotely-log-in-to-your-virtual-machine"></a><span data-ttu-id="cb6de-151">Connexion distante à votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cb6de-151">To remotely log in to your virtual machine</span></span>
1. <span data-ttu-id="cb6de-152">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cb6de-152">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="cb6de-153">Cliquez sur **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="cb6de-154">Cliquez sur le nom de la machine virtuelle à laquelle vous voulez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="cb6de-154">Click the name of the virtual machine that you want to log in to.</span></span>
4. <span data-ttu-id="cb6de-155">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-155">Click **Connect**.</span></span>
5. <span data-ttu-id="cb6de-156">Répondez aux invites pour vous connecter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cb6de-156">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="cb6de-157">Lorsque vous y êtes invité, entrez le nom d’administrateur et le mot de passe fournis lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cb6de-157">When prompted for the administrator name and password, use the values that you provided when you created the virtual machine.</span></span>

<span data-ttu-id="cb6de-158">Notez que la fonctionnalité Azure Service Bus requiert l'installation du certificat racine Baltimore CyberTrust dans le magasin **cacerts** de votre environnement JRE.</span><span class="sxs-lookup"><span data-stu-id="cb6de-158">Note that the Azure Service Bus functionality requires the Baltimore CyberTrust Root certificate to be installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="cb6de-159">Ce certificat est automatiquement inclus dans l'environnement JRE (Java Runtime Environment) utilisé par ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="cb6de-159">This certificate is automatically included in the Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="cb6de-160">Si vous ne disposez pas de ce certificat dans le magasin **cacerts** de votre environnement JRE, consultez la rubrique [Ajout d’un certificat au magasin de certificats d’autorité de certification Java][add_ca_cert] pour plus d’informations sur l’ajout de celui-ci (et sur l’affichage des certificats de votre magasin cacerts).</span><span class="sxs-lookup"><span data-stu-id="cb6de-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing the certificates in your cacerts store).</span></span>

## <a name="how-to-create-a-service-bus-namespace"></a><span data-ttu-id="cb6de-161">Création d’un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="cb6de-161">How to create a service bus namespace</span></span>
<span data-ttu-id="cb6de-162">Pour commencer à utiliser les files d'attente Service Bus dans Azure, vous devez d'abord créer un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="cb6de-162">To begin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="cb6de-163">Ce dernier fournit un conteneur d’étendue pour l’adressage des ressources Service Bus au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="cb6de-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="cb6de-164">Pour créer un espace de noms de service :</span><span class="sxs-lookup"><span data-stu-id="cb6de-164">To create a service namespace:</span></span>

1. <span data-ttu-id="cb6de-165">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cb6de-165">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="cb6de-166">En bas du volet de navigation gauche du Portail Azure Classic, cliquez sur **Service Bus, Access Control et Cache**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-166">In the lower-left navigation pane of the Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="cb6de-167">Dans le volet supérieur gauche du Portail Azure Classic, cliquez sur le nœud **Service Bus**, puis sur le bouton **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-167">In the upper-left pane of the Azure classic portal, click the **Service Bus** node, and then click the **New** button.</span></span>  
   <span data-ttu-id="cb6de-168">![Capture d'écran du nœud Service Bus][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="cb6de-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="cb6de-169">Dans la boîte de dialogue **Créer un espace de noms de service**, entrez un **Espace de noms**, puis vérifiez qu’il est unique en cliquant sur le bouton **Vérifier la disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-169">In the **Create a new Service Namespace** dialog box, enter a **Namespace**, and then to make sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="cb6de-170">![Capture d'écran Créer un espace de noms][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="cb6de-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="cb6de-171">Après avoir vérifié que le nom de l'espace de noms est disponible, choisissez le pays ou la région où votre espace de noms sera hébergé, puis cliquez sur le bouton **Créer un espace de noms** .</span><span class="sxs-lookup"><span data-stu-id="cb6de-171">After making sure the namespace name is available, choose the country or region in which your namespace should be hosted, and then click the **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="cb6de-172">L’espace de noms que vous avez créé apparaît alors dans le portail Azure Classic. Son activation peut prendre un peu de temps.</span><span class="sxs-lookup"><span data-stu-id="cb6de-172">The namespace you created will then appear in the Azure classic portal and takes a moment to activate.</span></span> <span data-ttu-id="cb6de-173">Attendez que l’état **Actif** apparaisse avant de passer à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="cb6de-173">Wait until the status is **Active** before continuing with the next step.</span></span>

## <a name="obtain-the-default-management-credentials-for-the-namespace"></a><span data-ttu-id="cb6de-174">Obtention d'informations d'identification de gestion par défaut pour l'espace de noms</span><span class="sxs-lookup"><span data-stu-id="cb6de-174">Obtain the Default Management Credentials for the namespace</span></span>
<span data-ttu-id="cb6de-175">Pour pouvoir effectuer des opérations de gestion telles que la création d'une file d'attente sur le nouvel espace de noms, vous devez obtenir les informations d'identification de gestion associées.</span><span class="sxs-lookup"><span data-stu-id="cb6de-175">In order to perform management operations, such as creating a queue, on the new namespace, you need to obtain the management credentials for the namespace.</span></span>

1. <span data-ttu-id="cb6de-176">Dans le volet de navigation gauche, cliquez sur le nœud **Service Bus** pour afficher la liste des espaces de noms disponibles.</span><span class="sxs-lookup"><span data-stu-id="cb6de-176">In the left navigation pane, click the **Service Bus** node to display the list of available namespaces.</span></span>
   <span data-ttu-id="cb6de-177">![Capture d'écran Available Namespaces][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="cb6de-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="cb6de-178">Sélectionnez l’espace de noms que vous venez de créer dans la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="cb6de-178">Select the namespace you just created from the list shown.</span></span>
   <span data-ttu-id="cb6de-179">![Capture d’écran Liste d’espaces de noms][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="cb6de-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="cb6de-180">Le volet **Propriétés** de droite répertorie les propriétés du nouvel espace de noms.</span><span class="sxs-lookup"><span data-stu-id="cb6de-180">The right-hand **Properties** pane lists the properties for the new namespace.</span></span>
   <span data-ttu-id="cb6de-181">![Capture d'écran du volet Propriétés][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="cb6de-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="cb6de-182">La **Clé par défaut** est masquée.</span><span class="sxs-lookup"><span data-stu-id="cb6de-182">The **Default Key** is hidden.</span></span> <span data-ttu-id="cb6de-183">Cliquez sur le bouton **Afficher** pour afficher les informations d'identification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="cb6de-183">Click the **View** button to display the security credentials.</span></span>
   <span data-ttu-id="cb6de-184">![Capture d'écran Clé par défaut][default_key]</span><span class="sxs-lookup"><span data-stu-id="cb6de-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="cb6de-185">Notez **l’Émetteur par défaut** et la **Clé par défaut**, car vous devrez utiliser ces informations ci-dessous pour accomplir les opérations relatives à l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="cb6de-185">Make a note of the **Default Issuer** and the **Default Key** as you will use this information below to perform operations with the namespace.</span></span>

## <a name="how-to-create-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="cb6de-186">Création d'une application Java exécutant une tâche qui nécessite beaucoup de ressources</span><span class="sxs-lookup"><span data-stu-id="cb6de-186">How to create a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="cb6de-187">Sur votre ordinateur de développement (qui n'est pas forcément celui où se trouve la machine virtuelle que vous avez créée), téléchargez le [Kit de développement logiciel (SDK) Azure pour Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="cb6de-187">On your development machine (which does not have to be the virtual machine that you created), download the [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="cb6de-188">Créez une application console Java à l'aide de l'exemple de code disponible à la fin de cette section.</span><span class="sxs-lookup"><span data-stu-id="cb6de-188">Create a Java console application using the example code at the end of this section.</span></span> <span data-ttu-id="cb6de-189">Dans le cadre de ce didacticiel, nous utiliserons le nom de fichier Java **TSPSolver.java** .</span><span class="sxs-lookup"><span data-stu-id="cb6de-189">In this tutorial, we'll use **TSPSolver.java** as the Java file name.</span></span> <span data-ttu-id="cb6de-190">Modifiez les espaces réservés **your\_service\_bus\_namespace**, **your\_service\_bus\_owner** et **your\_service\_bus\_key** pour utiliser respectivement vos valeurs Service Bus **Espace de noms**, **Émetteur par défaut** et **Clé par défaut**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-190">Modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="cb6de-191">Après le codage, exportez l'application dans une archive Java exécutable (JAR) et créez un package contenant les bibliothèques requises dans le fichier JAR généré.</span><span class="sxs-lookup"><span data-stu-id="cb6de-191">After coding, export the application to a runnable Java archive (JAR), and package the required libraries into the generated JAR.</span></span> <span data-ttu-id="cb6de-192">Dans le cadre de ce didacticiel, nous utiliserons le nom **TSPSolver.jar** pour désigner le fichier JAR généré.</span><span class="sxs-lookup"><span data-stu-id="cb6de-192">In this tutorial, we'll use **TSPSolver.jar** as the generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often to provide an update to the console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as the default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing to occur other than creating the queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing to occur other than deleting the queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume the value passed in is the number of cities to solve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-to-create-a-java-application-that-monitors-the-progress-of-the-compute-intensive-task"></a><span data-ttu-id="cb6de-193">Création d'une application Java surveillant la progression de la tâche qui nécessite beaucoup de ressources</span><span class="sxs-lookup"><span data-stu-id="cb6de-193">How to create a Java application that monitors the progress of the compute-intensive task</span></span>
1. <span data-ttu-id="cb6de-194">Sur votre ordinateur de développement, créez une application console Java à l'aide de l'exemple de code disponible à la fin de cette section.</span><span class="sxs-lookup"><span data-stu-id="cb6de-194">On your development machine, create a Java console application using the example code at the end of this section.</span></span> <span data-ttu-id="cb6de-195">Dans le cadre de ce didacticiel, nous utiliserons le nom **TSPClient.java** pour désigner le fichier Java.</span><span class="sxs-lookup"><span data-stu-id="cb6de-195">In this tutorial, we'll use **TSPClient.java** as the Java file name.</span></span> <span data-ttu-id="cb6de-196">Comme indiqué plus haut, modifiez les espaces réservés **your\_service\_bus\_namespace**, **your\_service\_bus\_owner** et **your\_service\_bus\_key** pour utiliser respectivement vos valeurs Service Bus **Espace de noms**, **Émetteur par défaut** et **Clé par défaut**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-196">As shown earlier, modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="cb6de-197">Exportez l'application dans un fichier JAR exécutable et créez un package contenant les bibliothèques requises dans le fichier JAR généré.</span><span class="sxs-lookup"><span data-stu-id="cb6de-197">Export the application to a runnable JAR, and package the required libraries into the generated JAR.</span></span> <span data-ttu-id="cb6de-198">Dans le cadre de ce didacticiel, nous utiliserons le nom **TSPClient.jar** pour désigner le fichier JAR généré.</span><span class="sxs-lookup"><span data-stu-id="cb6de-198">In this tutorial, we'll use **TSPClient.jar** as the generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as the default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display the queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing to occur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // The queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-to-run-the-java-applications"></a><span data-ttu-id="cb6de-199">Exécution des applications Java</span><span class="sxs-lookup"><span data-stu-id="cb6de-199">How to run the Java applications</span></span>
<span data-ttu-id="cb6de-200">Exécutez l'application nécessitant beaucoup de ressources pour créer la file d'attente, puis pour résoudre le problème du voyageur de commerce afin d'ajouter le meilleur itinéraire actuel à la file d'attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cb6de-200">Run the compute-intensive application, first to create the queue, then to solve the Traveling Saleseman Problem, which will add the current best route to the service bus queue.</span></span> <span data-ttu-id="cb6de-201">Pendant (ou après) l'exécution de l'application nécessitant beaucoup de ressources, exécutez le client pour afficher les résultats de la file d'attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cb6de-201">While the compute-intensive application is running (or afterwards), run the client to display results from the service bus queue.</span></span>

### <a name="to-run-the-compute-intensive-application"></a><span data-ttu-id="cb6de-202">Exécution de l'application nécessitant beaucoup de ressources</span><span class="sxs-lookup"><span data-stu-id="cb6de-202">To run the compute-intensive application</span></span>
1. <span data-ttu-id="cb6de-203">Connectez-vous à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cb6de-203">Log on to your virtual machine.</span></span>
2. <span data-ttu-id="cb6de-204">Créez un dossier où vous exécuterez votre application.</span><span class="sxs-lookup"><span data-stu-id="cb6de-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="cb6de-205">Par exemple, **C:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="cb6de-206">Copiez **TSPSolver.jar** sous **C:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-206">Copy **TSPSolver.jar** to **c:\TSP**,</span></span>
4. <span data-ttu-id="cb6de-207">Créez un fichier intitulé **C:\TSP\cities.txt** avec le contenu ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cb6de-207">Create a file named **c:\TSP\cities.txt** with the following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="cb6de-208">Depuis une invite de commandes, accédez au répertoire c:\TSP.</span><span class="sxs-lookup"><span data-stu-id="cb6de-208">At a command prompt, change directories to c:\TSP.</span></span>
6. <span data-ttu-id="cb6de-209">Vérifiez que le dossier Bin de JRE se trouve dans la variable d'environnement PATH.</span><span class="sxs-lookup"><span data-stu-id="cb6de-209">Ensure the JRE's bin folder is in the PATH environment variable.</span></span>
7. <span data-ttu-id="cb6de-210">Vous devez créer la file d'attente Service Bus avant d'exécuter les permutations de solveur TSP.</span><span class="sxs-lookup"><span data-stu-id="cb6de-210">You'll need to create the service bus queue before you run the TSP solver permutations.</span></span> <span data-ttu-id="cb6de-211">Exécutez la commande ci-dessous pour créer la file d'attente de bus de services.</span><span class="sxs-lookup"><span data-stu-id="cb6de-211">Run the following command to create the service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="cb6de-212">Maintenant que la file d’attente est créée, vous pouvez exécuter les permutations de solveur TSP.</span><span class="sxs-lookup"><span data-stu-id="cb6de-212">Now that the queue is created, you can run the TSP solver permutations.</span></span> <span data-ttu-id="cb6de-213">Par exemple, exécutez la commande suivante afin d’exécuter le solveur pour 8 villes.</span><span class="sxs-lookup"><span data-stu-id="cb6de-213">For example, run the following command to run the solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="cb6de-214">Si vous n'entrez aucun nombre, l'exécution portera sur 10 villes.</span><span class="sxs-lookup"><span data-stu-id="cb6de-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="cb6de-215">Dès que le solveur trouve les itinéraires les plus courts, il les ajoute à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="cb6de-215">As the solver finds current shortest routes, it will add them to the queue.</span></span>

> [!NOTE]
> <span data-ttu-id="cb6de-216">Plus le nombre spécifié est élevé, plus l’exécution du solveur est longue.</span><span class="sxs-lookup"><span data-stu-id="cb6de-216">The larger the number that you specify, the longer the solver will run.</span></span> <span data-ttu-id="cb6de-217">Par exemple, une exécution portant sur 14 villes peut prendre quelques minutes, et une exécution portant sur 15 villes peut prendre des heures.</span><span class="sxs-lookup"><span data-stu-id="cb6de-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="cb6de-218">Au-delà de 16 villes, l'exécution peut prendre des jours (voire des semaines, des mois et des années).</span><span class="sxs-lookup"><span data-stu-id="cb6de-218">Increasing to 16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="cb6de-219">Cette lenteur est due à la hausse rapide du nombre de permutations évaluées par le solveur à mesure que le nombre de villes augmente.</span><span class="sxs-lookup"><span data-stu-id="cb6de-219">This is due to the rapid increase in the number of permutations evaluated by the solver as the number of cities increases.</span></span>
> 
> 

### <a name="how-to-run-the-monitoring-client-application"></a><span data-ttu-id="cb6de-220">Exécution de la surveillance de l'application cliente</span><span class="sxs-lookup"><span data-stu-id="cb6de-220">How to run the monitoring client application</span></span>
1. <span data-ttu-id="cb6de-221">Connectez-vous à l'ordinateur où vous exécuterez l'application cliente.</span><span class="sxs-lookup"><span data-stu-id="cb6de-221">Log on to your machine where you will run the client application.</span></span> <span data-ttu-id="cb6de-222">Il ne doit pas nécessairement s'agir de l'ordinateur qui exécute l'application **TSPSolver** .</span><span class="sxs-lookup"><span data-stu-id="cb6de-222">This does not need to be the same machine running the **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="cb6de-223">Créez un dossier où vous exécuterez votre application.</span><span class="sxs-lookup"><span data-stu-id="cb6de-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="cb6de-224">Par exemple, **C:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="cb6de-225">Copiez **TSPClient.jar** sous **C:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="cb6de-225">Copy **TSPClient.jar** to **c:\TSP**,</span></span>
4. <span data-ttu-id="cb6de-226">Vérifiez que le dossier Bin de JRE se trouve dans la variable d'environnement PATH.</span><span class="sxs-lookup"><span data-stu-id="cb6de-226">Ensure the JRE's bin folder is in the PATH environment variable.</span></span>
5. <span data-ttu-id="cb6de-227">Depuis une invite de commandes, accédez au répertoire c:\TSP.</span><span class="sxs-lookup"><span data-stu-id="cb6de-227">At a command prompt, change directories to c:\TSP.</span></span>
6. <span data-ttu-id="cb6de-228">Exécutez la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cb6de-228">Run the following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="cb6de-229">Vous pouvez éventuellement spécifier le nombre de minutes de veille entre les vérifications de la file d’attente via un argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="cb6de-229">Optionally, specify the number of minutes to sleep in between checking the queue, by passing in a command-line argument.</span></span> <span data-ttu-id="cb6de-230">La période de veille par défaut de la vérification de la file d'attente est de 3 minutes et elle est appliquée si aucun argument de ligne de commande n'est transmis à **TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="cb6de-230">The default sleep period for checking the queue is 3 minutes, which is used if no command-line argument is passed to **TSPClient**.</span></span> <span data-ttu-id="cb6de-231">Si vous souhaitez utiliser une autre valeur pour l’intervalle de veille (une minute, par exemple), exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cb6de-231">If you want to use a different value for the sleep interval, for example, one minute, run the following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="cb6de-232">Le client s'exécutera jusqu'à ce qu'il voie le message de file d'attente « Terminé ».</span><span class="sxs-lookup"><span data-stu-id="cb6de-232">The client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="cb6de-233">Notez que si vous exécutez plusieurs occurrences du solveur sans exécuter le client, vous serez peut-être amené à exécuter le client plusieurs fois pour vider entièrement la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="cb6de-233">Note that if you run multiple occurrences of the solver without running the client, you may need to run the client multiple times to completely empty the queue.</span></span> <span data-ttu-id="cb6de-234">Vous pouvez également supprimer la file d’attente puis la recréer.</span><span class="sxs-lookup"><span data-stu-id="cb6de-234">Alternatively, you can delete the queue and then create it again.</span></span> <span data-ttu-id="cb6de-235">Pour supprimer la file d’attente, exécutez la commande **TSPSolver** (et non **TSPClient**) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cb6de-235">To delete the queue, run the following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="cb6de-236">Le solveur s’exécutera jusqu’à ce qu’il ait examiné tous les itinéraires.</span><span class="sxs-lookup"><span data-stu-id="cb6de-236">The solver will run until it finishes examining all routes.</span></span>

## <a name="how-to-stop-the-java-applications"></a><span data-ttu-id="cb6de-237">Arrêt des applications Java</span><span class="sxs-lookup"><span data-stu-id="cb6de-237">How to stop the Java applications</span></span>
<span data-ttu-id="cb6de-238">Pour quitter les applications solveur et cliente avant la fin normale, vous pouvez appuyer sur **Ctrl+C** .</span><span class="sxs-lookup"><span data-stu-id="cb6de-238">For both the solver and client applications, you can press **Ctrl+C** to exit if you want to end prior to normal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
