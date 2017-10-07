---
title: application de Java aaaCompute intensif sur une machine virtuelle | Documents Microsoft
description: "Découvrez comment toocreate une machine virtuelle Azure qui exécute une application Java de calcul intensif qui peut être surveillée par une autre application Java."
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
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="fc19e-103">Comment toorun nécessitant une tâche dans Java sur un ordinateur virtuel</span><span class="sxs-lookup"><span data-stu-id="fc19e-103">How toorun a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="fc19e-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fc19e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fc19e-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fc19e-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="fc19e-107">Avec Azure, vous pouvez utiliser une tâche de calcul intensif toohandle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fc19e-107">With Azure, you can use a virtual machine toohandle compute-intensive tasks.</span></span> <span data-ttu-id="fc19e-108">Par exemple, un ordinateur virtuel peut gérer des tâches et de remettre machines tooclient de résultats ou des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="fc19e-108">For example, a virtual machine can handle tasks and deliver results tooclient machines or mobile applications.</span></span> <span data-ttu-id="fc19e-109">Après avoir lu cet article, vous devez comprendre comment toocreate une machine virtuelle qui exécute une application Java de calcul intensif qui peut être surveillée par une autre application Java.</span><span class="sxs-lookup"><span data-stu-id="fc19e-109">After reading this article, you will have an understanding of how toocreate a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="fc19e-110">Ce didacticiel suppose que vous savez comment les applications console toocreate Java, peut importer l’application de bibliothèques tooyour Java et peut générer une archive Java (JAR).</span><span class="sxs-lookup"><span data-stu-id="fc19e-110">This tutorial assumes you know how toocreate Java console applications, can import libraries tooyour Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="fc19e-111">Aucune connaissance de Microsoft Azure n'est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fc19e-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="fc19e-112">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fc19e-112">You will learn:</span></span>

* <span data-ttu-id="fc19e-113">Comment toocreate un ordinateur virtuel avec un Kit de développement Java (JDK) déjà installé.</span><span class="sxs-lookup"><span data-stu-id="fc19e-113">How toocreate a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="fc19e-114">Comment tooremotely du journal dans la machine virtuelle de tooyour.</span><span class="sxs-lookup"><span data-stu-id="fc19e-114">How tooremotely log in tooyour virtual machine.</span></span>
* <span data-ttu-id="fc19e-115">Comment toocreate un service bus espace de noms.</span><span class="sxs-lookup"><span data-stu-id="fc19e-115">How toocreate a service bus namespace.</span></span>
* <span data-ttu-id="fc19e-116">Comment toocreate une application Java qui effectue une tâche de calcul intensif.</span><span class="sxs-lookup"><span data-stu-id="fc19e-116">How toocreate a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="fc19e-117">Comment toocreate une application Java qui surveille hello progression de la tâche de calcul intensif hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-117">How toocreate a Java application that monitors hello progress of hello compute-intensive task.</span></span>
* <span data-ttu-id="fc19e-118">Comment toorun hello des applications Java.</span><span class="sxs-lookup"><span data-stu-id="fc19e-118">How toorun hello Java applications.</span></span>
* <span data-ttu-id="fc19e-119">Comment toostop hello des applications Java.</span><span class="sxs-lookup"><span data-stu-id="fc19e-119">How toostop hello Java applications.</span></span>

<span data-ttu-id="fc19e-120">Ce didacticiel utilise hello problème commercial pour la tâche de calcul intensif hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-120">This tutorial will use hello Traveling Salesman Problem for hello compute-intensive task.</span></span> <span data-ttu-id="fc19e-121">Hello Voici un exemple de tâche de calcul intensif hello en cours d’exécution hello Java application.</span><span class="sxs-lookup"><span data-stu-id="fc19e-121">hello following is an example of hello Java application running hello compute-intensive task.</span></span>

![Résolution du problème du voyageur de commerce][solver_output]

<span data-ttu-id="fc19e-123">Hello Voici un exemple de tâche de calcul intensif Java application analyse hello de hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-123">hello following is an example of hello Java application monitoring hello compute-intensive task.</span></span>

![Client du problème du voyageur de commerce][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="fc19e-125">toocreate une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fc19e-125">toocreate a virtual machine</span></span>
1. <span data-ttu-id="fc19e-126">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fc19e-126">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fc19e-127">Cliquez sur **New**, sur **Compute**, sur **Virtual machine**, puis sur **From Gallery**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="fc19e-128">Bonjour **sélection d’image de machine virtuelle** boîte de dialogue, sélectionnez **JDK 7 Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-128">In hello **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="fc19e-129">Notez que **JDK 6 Windows Server 2012** au cas où vous avez des applications héritées qui ne sont pas encore prêt toorun JDK 7.</span><span class="sxs-lookup"><span data-stu-id="fc19e-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready toorun in JDK 7.</span></span>
4. <span data-ttu-id="fc19e-130">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-130">Click **Next**.</span></span>
5. <span data-ttu-id="fc19e-131">Bonjour **configuration d’ordinateur virtuel** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="fc19e-131">In hello **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="fc19e-132">Spécifiez un nom pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-132">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="fc19e-133">Spécifiez toouse de taille hello pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-133">Specify hello size toouse for hello virtual machine.</span></span>
   3. <span data-ttu-id="fc19e-134">Entrez un nom pour l’administrateur de hello dans hello **nom d’utilisateur** champ.</span><span class="sxs-lookup"><span data-stu-id="fc19e-134">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="fc19e-135">N’oubliez pas ce nom et hello mot de passe que vous devrez entrer ensuite, vous allez les utiliser lorsque vous vous connectez à distance dans la machine virtuelle de toohello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-135">Remember this name and hello password you will enter next, you will use them when you remotely log in toohello virtual machine.</span></span>
   4. <span data-ttu-id="fc19e-136">Entrez un mot de passe Bonjour **nouveau mot de passe** champ et entrez-la dans hello **confirmer** champ.</span><span class="sxs-lookup"><span data-stu-id="fc19e-136">Enter a password in hello **New password** field, and re-enter it in hello **Confirm** field.</span></span> <span data-ttu-id="fc19e-137">Il s’agit de mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-137">This is hello Administrator account password.</span></span>
   5. <span data-ttu-id="fc19e-138">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-138">Click **Next**.</span></span>
6. <span data-ttu-id="fc19e-139">Bonjour suivant **configuration d’ordinateur virtuel** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="fc19e-139">In hello next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="fc19e-140">Pour **service de cloud computing**, utiliser la valeur par défaut hello **créer un service cloud**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-140">For **Cloud service**, use hello default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="fc19e-141">Hello valeur pour **nom DNS du service Cloud** doit être unique sur cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="fc19e-141">hello value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="fc19e-142">Si nécessaire, modifiez cette valeur afin qu'Azure indique qu'elle est unique.</span><span class="sxs-lookup"><span data-stu-id="fc19e-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="fc19e-143">Indiquez une région, un groupe d'affinités ou un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="fc19e-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="fc19e-144">Dans le cadre de ce didacticiel, indiquez une région comme **Bretagne**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="fc19e-145">Pour **Storage Account**, sélectionnez **Use an automatically generated storage account**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="fc19e-146">Pour **Availability Set**, sélectionnez **(None)**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="fc19e-147">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-147">Click **Next**.</span></span>
7. <span data-ttu-id="fc19e-148">Bonjour final **configuration d’ordinateur virtuel** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="fc19e-148">In hello final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="fc19e-149">Accepter les entrées de point de terminaison par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-149">Accept hello default endpoint entries.</span></span>
   2. <span data-ttu-id="fc19e-150">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-150">Click **Complete**.</span></span>

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a><span data-ttu-id="fc19e-151">journal de tooremotely dans la machine virtuelle de tooyour</span><span class="sxs-lookup"><span data-stu-id="fc19e-151">tooremotely log in tooyour virtual machine</span></span>
1. <span data-ttu-id="fc19e-152">Ouvrez une session sur toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fc19e-152">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fc19e-153">Cliquez sur **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="fc19e-154">Cliquez sur nom hello hello virtuels que vous souhaitez toolog dans.</span><span class="sxs-lookup"><span data-stu-id="fc19e-154">Click hello name of hello virtual machine that you want toolog in to.</span></span>
4. <span data-ttu-id="fc19e-155">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-155">Click **Connect**.</span></span>
5. <span data-ttu-id="fc19e-156">Répondre toohello invites en tant que machine virtuelle de toohello tooconnect nécessaires.</span><span class="sxs-lookup"><span data-stu-id="fc19e-156">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="fc19e-157">À l’invite de mot de passe et le nom de l’administrateur hello, utilisez les valeurs de hello que vous avez fourni lors de la création de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-157">When prompted for hello administrator name and password, use hello values that you provided when you created hello virtual machine.</span></span>

<span data-ttu-id="fc19e-158">Notez que les fonctionnalités Azure Service Bus hello requiert hello Baltimore CyberTrust Root certificat toobe est installé dans le cadre de votre JRE **cacerts** stocker.</span><span class="sxs-lookup"><span data-stu-id="fc19e-158">Note that hello Azure Service Bus functionality requires hello Baltimore CyberTrust Root certificate toobe installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="fc19e-159">Ce certificat est automatiquement inclus dans hello Java Runtime Environment (JRE) utilisé par ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="fc19e-159">This certificate is automatically included in hello Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="fc19e-160">Si vous n’avez pas de ce certificat dans votre JRE **cacerts** stockage, consultez [Ajout d’un toohello certificat magasin de certificats d’autorité de certification Java] [ add_ca_cert] pour plus d’informations sur l’ajout d’il (ainsi que informations sur l’affichage des certificats de hello dans votre magasin cacerts).</span><span class="sxs-lookup"><span data-stu-id="fc19e-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing hello certificates in your cacerts store).</span></span>

## <a name="how-toocreate-a-service-bus-namespace"></a><span data-ttu-id="fc19e-161">Comment toocreate un service bus espace de noms</span><span class="sxs-lookup"><span data-stu-id="fc19e-161">How toocreate a service bus namespace</span></span>
<span data-ttu-id="fc19e-162">les files d’attente de toobegin à l’aide du Service Bus dans Azure, vous devez d’abord créer un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="fc19e-162">toobegin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="fc19e-163">Ce dernier fournit un conteneur d’étendue pour l’adressage des ressources Service Bus au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="fc19e-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="fc19e-164">toocreate un espace de noms de service :</span><span class="sxs-lookup"><span data-stu-id="fc19e-164">toocreate a service namespace:</span></span>

1. <span data-ttu-id="fc19e-165">Ouvrez une session sur toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fc19e-165">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fc19e-166">Dans le volet de navigation inférieure gauche hello Hello portail Azure classic, cliquez sur **Service Bus, contrôle d’accès et la mise en cache**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-166">In hello lower-left navigation pane of hello Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="fc19e-167">Dans le volet supérieur gauche de hello Hello portail Azure classic, cliquez sur hello **Service Bus** nœud, puis cliquez sur hello **nouveau** bouton.</span><span class="sxs-lookup"><span data-stu-id="fc19e-167">In hello upper-left pane of hello Azure classic portal, click hello **Service Bus** node, and then click hello **New** button.</span></span>  
   <span data-ttu-id="fc19e-168">![Capture d'écran du nœud Service Bus][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="fc19e-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="fc19e-169">Bonjour **créer un nouveau Namespace de Service** boîte de dialogue, entrez un **Namespace**, puis toomake assurer qu’il est unique, cliquez sur le **vérifier la disponibilité** bouton.</span><span class="sxs-lookup"><span data-stu-id="fc19e-169">In hello **Create a new Service Namespace** dialog box, enter a **Namespace**, and then toomake sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="fc19e-170">![Capture d'écran Créer un espace de noms][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="fc19e-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="fc19e-171">Après avoir vérifié que le nom d’espace de noms hello est disponible, cliquez sur le pays ou la région dans laquelle votre espace de noms doit être hébergé, puis cliquez sur hello **créer de Namespace** bouton.</span><span class="sxs-lookup"><span data-stu-id="fc19e-171">After making sure hello namespace name is available, choose the country or region in which your namespace should be hosted, and then click hello **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="fc19e-172">espace de noms de Hello que vous avez créé apparaît dans hello portail Azure classic et prend un tooactivate moment.</span><span class="sxs-lookup"><span data-stu-id="fc19e-172">hello namespace you created will then appear in hello Azure classic portal and takes a moment tooactivate.</span></span> <span data-ttu-id="fc19e-173">Attendez que l’état hello est **Active** avant de passer à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-173">Wait until hello status is **Active** before continuing with hello next step.</span></span>

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a><span data-ttu-id="fc19e-174">Obtenir hello par défaut gestion des informations d’identification pour l’espace de noms hello</span><span class="sxs-lookup"><span data-stu-id="fc19e-174">Obtain hello Default Management Credentials for hello namespace</span></span>
<span data-ttu-id="fc19e-175">Dans les opérations de gestion de tooperform commande, telles que la création d’une file d’attente, sur hello le nouvel espace de noms, vous avez besoin d’informations d’identification de gestion tooobtain hello pour l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="fc19e-175">In order tooperform management operations, such as creating a queue, on hello new namespace, you need tooobtain hello management credentials for the namespace.</span></span>

1. <span data-ttu-id="fc19e-176">Dans le volet de navigation gauche hello, cliquez sur hello **Service Bus** nœud pour afficher la liste de hello des espaces de noms disponibles.</span><span class="sxs-lookup"><span data-stu-id="fc19e-176">In hello left navigation pane, click hello **Service Bus** node to display hello list of available namespaces.</span></span>
   <span data-ttu-id="fc19e-177">![Capture d'écran Available Namespaces][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="fc19e-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="fc19e-178">Sélectionnez l’espace de noms hello que vous venez de créer à partir de la liste hello indiqué.</span><span class="sxs-lookup"><span data-stu-id="fc19e-178">Select hello namespace you just created from hello list shown.</span></span>
   <span data-ttu-id="fc19e-179">![Capture d’écran Liste d’espaces de noms][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="fc19e-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="fc19e-180">Hello droite **propriétés** volet répertorie les propriétés hello pour le nouvel espace de noms.</span><span class="sxs-lookup"><span data-stu-id="fc19e-180">hello right-hand **Properties** pane lists hello properties for the new namespace.</span></span>
   <span data-ttu-id="fc19e-181">![Capture d'écran du volet Propriétés][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="fc19e-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="fc19e-182">Hello **clé par défaut** est masqué.</span><span class="sxs-lookup"><span data-stu-id="fc19e-182">hello **Default Key** is hidden.</span></span> <span data-ttu-id="fc19e-183">Cliquez sur hello **vue** bouton informations d’identification de sécurité toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-183">Click hello **View** button toodisplay hello security credentials.</span></span>
   <span data-ttu-id="fc19e-184">![Capture d'écran Clé par défaut][default_key]</span><span class="sxs-lookup"><span data-stu-id="fc19e-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="fc19e-185">Prenez note de hello **émetteur par défaut** et hello **clé par défaut** car vous utiliserez ces informations ci-dessous tooperform opérations avec l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="fc19e-185">Make a note of hello **Default Issuer** and hello **Default Key** as you will use this information below tooperform operations with the namespace.</span></span>

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="fc19e-186">Comment toocreate une application Java qui effectue une tâche de calcul intensif</span><span class="sxs-lookup"><span data-stu-id="fc19e-186">How toocreate a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="fc19e-187">Sur votre ordinateur de développement (qui n’a pas de machine virtuelle de hello toobe que vous avez créés), téléchargement hello [SDK Azure pour Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="fc19e-187">On your development machine (which does not have toobe hello virtual machine that you created), download hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="fc19e-188">Créez une application de console Java à l’aide du code d’exemple hello à fin hello de cette section.</span><span class="sxs-lookup"><span data-stu-id="fc19e-188">Create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="fc19e-189">Dans ce didacticiel, nous allons utiliser **TSPSolver.java** comme nom de fichier hello Java.</span><span class="sxs-lookup"><span data-stu-id="fc19e-189">In this tutorial, we'll use **TSPSolver.java** as hello Java file name.</span></span> <span data-ttu-id="fc19e-190">Modifier hello **votre\_service\_bus\_espace de noms**, **votre\_service\_bus\_propriétaire**et **votre\_service\_bus\_clé** des espaces réservés toouse service bus **espace de noms**, **émetteur par défaut** et  **Clé par défaut** valeurs, respectivement.</span><span class="sxs-lookup"><span data-stu-id="fc19e-190">Modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="fc19e-191">Après le codage, exportation hello application tooa exécutable archive Java (JAR) et hello de package requis bibliothèques dans hello généré JAR.</span><span class="sxs-lookup"><span data-stu-id="fc19e-191">After coding, export hello application tooa runnable Java archive (JAR), and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="fc19e-192">Dans ce didacticiel, nous allons utiliser **TSPSolver.jar** comme nom de fichier JAR hello généré.</span><span class="sxs-lookup"><span data-stu-id="fc19e-192">In this tutorial, we'll use **TSPSolver.jar** as hello generated JAR name.</span></span>

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

        //  Value specifying how often tooprovide an update toohello console.
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

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
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



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a><span data-ttu-id="fc19e-193">Comment toocreate une application Java qui surveille hello la progression de la tâche de calcul intensif hello</span><span class="sxs-lookup"><span data-stu-id="fc19e-193">How toocreate a Java application that monitors hello progress of hello compute-intensive task</span></span>
1. <span data-ttu-id="fc19e-194">Sur votre ordinateur de développement, créez une application de console Java à l’aide du code d’exemple hello à fin hello de cette section.</span><span class="sxs-lookup"><span data-stu-id="fc19e-194">On your development machine, create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="fc19e-195">Dans ce didacticiel, nous allons utiliser **TSPClient.java** comme nom de fichier hello Java.</span><span class="sxs-lookup"><span data-stu-id="fc19e-195">In this tutorial, we'll use **TSPClient.java** as hello Java file name.</span></span> <span data-ttu-id="fc19e-196">Comme indiqué précédemment, modifiez hello **votre\_service\_bus\_espace de noms**, **votre\_service\_bus\_propriétaire**, et **votre\_service\_bus\_clé** des espaces réservés toouse service bus **espace de noms**, **émetteur par défaut**et **clé par défaut** valeurs, respectivement.</span><span class="sxs-lookup"><span data-stu-id="fc19e-196">As shown earlier, modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="fc19e-197">Exporter hello application tooa JAR exécutable hello de package requis bibliothèques dans hello généré JAR.</span><span class="sxs-lookup"><span data-stu-id="fc19e-197">Export hello application tooa runnable JAR, and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="fc19e-198">Dans ce didacticiel, nous allons utiliser **TSPClient.jar** comme nom de fichier JAR hello généré.</span><span class="sxs-lookup"><span data-stu-id="fc19e-198">In this tutorial, we'll use **TSPClient.jar** as hello generated JAR name.</span></span>

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

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
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

                            // Display hello queue message.
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
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
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

## <a name="how-toorun-hello-java-applications"></a><span data-ttu-id="fc19e-199">Comment toorun hello des applications Java</span><span class="sxs-lookup"><span data-stu-id="fc19e-199">How toorun hello Java applications</span></span>
<span data-ttu-id="fc19e-200">Exécuter des applications de calcul intensif hello, première file d’attente de hello toocreate, puis toosolve hello problème Saleseman en déplacement, qui ajoute hello meilleur itinéraire toohello service bus file d’attente actuelle.</span><span class="sxs-lookup"><span data-stu-id="fc19e-200">Run hello compute-intensive application, first toocreate hello queue, then toosolve hello Traveling Saleseman Problem, which will add hello current best route toohello service bus queue.</span></span> <span data-ttu-id="fc19e-201">Hello lors de l’application de calcul intensif est en cours d’exécution (ou par la suite), résultats de toodisplay exécution hello client à partir de la file d’attente de bus de service hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-201">While hello compute-intensive application is running (or afterwards), run hello client toodisplay results from hello service bus queue.</span></span>

### <a name="toorun-hello-compute-intensive-application"></a><span data-ttu-id="fc19e-202">application de calcul intensif hello toorun</span><span class="sxs-lookup"><span data-stu-id="fc19e-202">toorun hello compute-intensive application</span></span>
1. <span data-ttu-id="fc19e-203">Ouvrez une session sur l’ordinateur virtuel de tooyour.</span><span class="sxs-lookup"><span data-stu-id="fc19e-203">Log on tooyour virtual machine.</span></span>
2. <span data-ttu-id="fc19e-204">Créez un dossier où vous exécuterez votre application.</span><span class="sxs-lookup"><span data-stu-id="fc19e-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="fc19e-205">Par exemple, **C:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="fc19e-206">Copie **TSPSolver.jar** trop**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="fc19e-206">Copy **TSPSolver.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="fc19e-207">Créez un fichier nommé **c:\TSP\cities.txt** avec hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="fc19e-207">Create a file named **c:\TSP\cities.txt** with hello following contents.</span></span>
   
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
5. <span data-ttu-id="fc19e-208">À une invite de commandes, modifiez les répertoires tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="fc19e-208">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="fc19e-209">Assurez-vous dossier de JRE hello bin se trouve dans la variable d’environnement PATH hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-209">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
7. <span data-ttu-id="fc19e-210">Vous aurez besoin de file d’attente du bus toocreate hello service avant d’exécuter des permutations de solveur PVC hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-210">You'll need toocreate hello service bus queue before you run hello TSP solver permutations.</span></span> <span data-ttu-id="fc19e-211">Exécutez hello suivant la file d’attente de commande toocreate hello service bus.</span><span class="sxs-lookup"><span data-stu-id="fc19e-211">Run hello following command toocreate hello service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="fc19e-212">Maintenant que hello file d’attente est créée, vous pouvez exécuter des permutations de solveur PVC hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-212">Now that hello queue is created, you can run hello TSP solver permutations.</span></span> <span data-ttu-id="fc19e-213">Par exemple, exécutez hello suivant solveur de hello toorun commande 8 villes.</span><span class="sxs-lookup"><span data-stu-id="fc19e-213">For example, run hello following command toorun hello solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="fc19e-214">Si vous n'entrez aucun nombre, l'exécution portera sur 10 villes.</span><span class="sxs-lookup"><span data-stu-id="fc19e-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="fc19e-215">Comme le solveur de hello recherche les itinéraires les plus courts en cours, il ajoute les file d’attente toohello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-215">As hello solver finds current shortest routes, it will add them toohello queue.</span></span>

> [!NOTE]
> <span data-ttu-id="fc19e-216">Hello plus grande hello nombre que vous spécifiez, solveur de hello plu hello s’exécutera.</span><span class="sxs-lookup"><span data-stu-id="fc19e-216">hello larger hello number that you specify, hello longer hello solver will run.</span></span> <span data-ttu-id="fc19e-217">Par exemple, une exécution portant sur 14 villes peut prendre quelques minutes, et une exécution portant sur 15 villes peut prendre des heures.</span><span class="sxs-lookup"><span data-stu-id="fc19e-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="fc19e-218">Augmentez too16 ou davantage de villes, vous risquez de jours du runtime (finalement semaines, mois et année).</span><span class="sxs-lookup"><span data-stu-id="fc19e-218">Increasing too16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="fc19e-219">Il s’agit en raison de l’augmentation rapide toohello nombre hello de permutations évaluées par le solveur de hello en tant que nombre hello de villes.</span><span class="sxs-lookup"><span data-stu-id="fc19e-219">This is due toohello rapid increase in hello number of permutations evaluated by hello solver as hello number of cities increases.</span></span>
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a><span data-ttu-id="fc19e-220">Comment toorun hello analyse de l’application client</span><span class="sxs-lookup"><span data-stu-id="fc19e-220">How toorun hello monitoring client application</span></span>
1. <span data-ttu-id="fc19e-221">Ouvrez une session sur l’ordinateur tooyour où vous allez exécuter l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-221">Log on tooyour machine where you will run hello client application.</span></span> <span data-ttu-id="fc19e-222">Cela n’a pas besoin toobe hello même ordinateur en cours d’exécution hello **TSPSolver** application, bien qu’il peut l’être.</span><span class="sxs-lookup"><span data-stu-id="fc19e-222">This does not need toobe hello same machine running hello **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="fc19e-223">Créez un dossier où vous exécuterez votre application.</span><span class="sxs-lookup"><span data-stu-id="fc19e-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="fc19e-224">Par exemple, **C:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="fc19e-225">Copie **TSPClient.jar** trop**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="fc19e-225">Copy **TSPClient.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="fc19e-226">Assurez-vous dossier de JRE hello bin se trouve dans la variable d’environnement PATH hello.</span><span class="sxs-lookup"><span data-stu-id="fc19e-226">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
5. <span data-ttu-id="fc19e-227">À une invite de commandes, modifiez les répertoires tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="fc19e-227">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="fc19e-228">Exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="fc19e-228">Run hello following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="fc19e-229">Si vous le souhaitez, spécifiez hello nombre de toosleep minutes entre la vérification de la file d’attente de hello, en passant un argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="fc19e-229">Optionally, specify hello number of minutes toosleep in between checking hello queue, by passing in a command-line argument.</span></span> <span data-ttu-id="fc19e-230">Hello période par défaut en mode veille pour la vérification de la file d’attente hello est 3 minutes, qui est utilisé si aucun argument de ligne de commande est passé trop**TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="fc19e-230">hello default sleep period for checking hello queue is 3 minutes, which is used if no command-line argument is passed too**TSPClient**.</span></span> <span data-ttu-id="fc19e-231">Si vous souhaitez toouse une autre valeur pour l’intervalle de veille hello, par exemple, une minute, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="fc19e-231">If you want toouse a different value for hello sleep interval, for example, one minute, run hello following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="fc19e-232">Hello client exécute jusqu'à ce qu’elle voit un message de la file d’attente de « Terminé ».</span><span class="sxs-lookup"><span data-stu-id="fc19e-232">hello client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="fc19e-233">Notez que si vous exécutez plusieurs occurrences de solveur de hello sans exécutant hello client, vous devrez peut-être le client de hello toorun file d’attente de plusieurs fois toocompletely hello vide.</span><span class="sxs-lookup"><span data-stu-id="fc19e-233">Note that if you run multiple occurrences of hello solver without running hello client, you may need toorun hello client multiple times toocompletely empty hello queue.</span></span> <span data-ttu-id="fc19e-234">Vous pouvez également supprimer la file d’attente hello et puis recréez-le.</span><span class="sxs-lookup"><span data-stu-id="fc19e-234">Alternatively, you can delete hello queue and then create it again.</span></span> <span data-ttu-id="fc19e-235">file d’attente de toodelete hello, exécutez hello **TSPSolver** (pas **TSPClient**) commande.</span><span class="sxs-lookup"><span data-stu-id="fc19e-235">toodelete hello queue, run hello following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="fc19e-236">Solveur de Hello s’exécute jusqu'à ce qu’il a terminé d’examiner des tous les itinéraires.</span><span class="sxs-lookup"><span data-stu-id="fc19e-236">hello solver will run until it finishes examining all routes.</span></span>

## <a name="how-toostop-hello-java-applications"></a><span data-ttu-id="fc19e-237">Comment toostop hello des applications Java</span><span class="sxs-lookup"><span data-stu-id="fc19e-237">How toostop hello Java applications</span></span>
<span data-ttu-id="fc19e-238">Pour les applications clientes et les solveur de hello, vous pouvez appuyer sur **Ctrl + C** tooexit si vous souhaitez tooend toonormal préalable achèvement.</span><span class="sxs-lookup"><span data-stu-id="fc19e-238">For both hello solver and client applications, you can press **Ctrl+C** tooexit if you want tooend prior toonormal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
