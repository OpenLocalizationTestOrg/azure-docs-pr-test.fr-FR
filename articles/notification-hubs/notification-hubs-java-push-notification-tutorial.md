---
title: aaaHow toouse concentrateurs de Notification avec Java
description: "Découvrez comment toouse Azure Notification Hubs à partir d’un Java back-end."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="66fd7-103">Comment toouse concentrateurs de Notification à partir de Java</span><span class="sxs-lookup"><span data-stu-id="66fd7-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="66fd7-104">Cette rubrique décrit les principales fonctionnalités de hello d’officielle de hello nouvelle entièrement pris en charge Azure Notification Hub Java SDK.</span><span class="sxs-lookup"><span data-stu-id="66fd7-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="66fd7-105">Il s’agit d’un projet open source et vous pouvez afficher hello ensemble SDK du code à [Kit de développement logiciel Java].</span><span class="sxs-lookup"><span data-stu-id="66fd7-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="66fd7-106">En règle générale, vous pouvez accéder à toutes les fonctionnalités de concentrateurs de Notification à partir d’un Java/PHP/Python/Ruby back-end à l’aide d’interface REST de concentrateur de Notification de hello comme décrit dans la rubrique MSDN hello [API REST de concentrateurs de Notification](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="66fd7-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="66fd7-107">Ce kit de développement logiciel Java fournit un wrapper fin par rapport aux interfaces REST dans Java.</span><span class="sxs-lookup"><span data-stu-id="66fd7-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="66fd7-108">Hello SDK prend en charge actuellement :</span><span class="sxs-lookup"><span data-stu-id="66fd7-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="66fd7-109">CRUD sur Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="66fd7-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="66fd7-110">CRUD sur les inscriptions</span><span class="sxs-lookup"><span data-stu-id="66fd7-110">CRUD on Registrations</span></span>
* <span data-ttu-id="66fd7-111">Gestion de l’installation</span><span class="sxs-lookup"><span data-stu-id="66fd7-111">Installation Management</span></span>
* <span data-ttu-id="66fd7-112">Importation/exportation des inscriptions</span><span class="sxs-lookup"><span data-stu-id="66fd7-112">Import/Export Registrations</span></span>
* <span data-ttu-id="66fd7-113">Envois réguliers</span><span class="sxs-lookup"><span data-stu-id="66fd7-113">Regular Sends</span></span>
* <span data-ttu-id="66fd7-114">Envois planifiés</span><span class="sxs-lookup"><span data-stu-id="66fd7-114">Scheduled Sends</span></span>
* <span data-ttu-id="66fd7-115">Opérations asynchrones via Java NIO</span><span class="sxs-lookup"><span data-stu-id="66fd7-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="66fd7-116">Plates-formes prises en charge : APNs (iOS), GCM (Android), WNS (applications Windows Store), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android sans services Google)</span><span class="sxs-lookup"><span data-stu-id="66fd7-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="66fd7-117">Utilisation du kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="66fd7-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="66fd7-118">Compilation et génération</span><span class="sxs-lookup"><span data-stu-id="66fd7-118">Compile and build</span></span>
<span data-ttu-id="66fd7-119">Utilisation de [Maven]</span><span class="sxs-lookup"><span data-stu-id="66fd7-119">Use [Maven]</span></span>

<span data-ttu-id="66fd7-120">toobuild :</span><span class="sxs-lookup"><span data-stu-id="66fd7-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="66fd7-121">Code</span><span class="sxs-lookup"><span data-stu-id="66fd7-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="66fd7-122">CRUD de Notification Hub</span><span class="sxs-lookup"><span data-stu-id="66fd7-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="66fd7-123">**Création d’un NamespaceManager :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="66fd7-124">**Création d’un concentrateur de notification :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="66fd7-125">OU</span><span class="sxs-lookup"><span data-stu-id="66fd7-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="66fd7-126">**Obtention d’un hub de notification :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="66fd7-127">**Mise à jour d’un concentrateur de notification :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="66fd7-128">**Suppression d’un hub de notification :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="66fd7-129">CRUID d’inscription</span><span class="sxs-lookup"><span data-stu-id="66fd7-129">Registration CRUDs</span></span>
<span data-ttu-id="66fd7-130">**Création d’un client de hub de notification :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="66fd7-131">**Création d’une inscription Windows :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="66fd7-132">**Création d’une inscription iOS :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="66fd7-133">De même, vous pouvez créer des inscriptions pour Android (GCM), Windows Phone (MPNS) et Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="66fd7-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="66fd7-134">**Création de modèles d’inscription :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="66fd7-135">**Création d’inscriptions à l’aide du moèle registrationid + upsert**</span><span class="sxs-lookup"><span data-stu-id="66fd7-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="66fd7-136">Supprime les doublons en raison de réponses de tooany perdu si vous stockez les ID d’inscription sur l’appareil de hello :</span><span class="sxs-lookup"><span data-stu-id="66fd7-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="66fd7-137">**Mise à jour d’inscriptions :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="66fd7-138">**Suppression d’inscriptions :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="66fd7-139">**Interrogation d’inscriptions :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-139">**Query registrations:**</span></span>

* <span data-ttu-id="66fd7-140">**Obtention d’une inscription unique :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="66fd7-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="66fd7-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="66fd7-142">**Obtention de toutes les inscriptions du hub :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="66fd7-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="66fd7-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="66fd7-144">**Obtention des inscriptions avec balise :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="66fd7-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="66fd7-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="66fd7-146">**Obtention des inscriptions par canal :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="66fd7-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="66fd7-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="66fd7-148">Toutes les requêtes de collection prennent en charge les jetons $top et de continuation.</span><span class="sxs-lookup"><span data-stu-id="66fd7-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="66fd7-149">Utilisation de l’API d’installation</span><span class="sxs-lookup"><span data-stu-id="66fd7-149">Installation API usage</span></span>
<span data-ttu-id="66fd7-150">L’API d’installation est un autre mécanisme de gestion des inscriptions.</span><span class="sxs-lookup"><span data-stu-id="66fd7-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="66fd7-151">Au lieu de la gestion de plusieurs enregistrements qui ne sont pas insignifiants et peut être facilement effectuée par inadvertance ou mal, il est désormais possible toouse un objet d’Installation unique.</span><span class="sxs-lookup"><span data-stu-id="66fd7-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="66fd7-152">L’installation contient tout ce dont vous avez besoin : un canal Push (jeton d’appareil), des balises, des modèles, des vignettes secondaires (pour WNS et APN).</span><span class="sxs-lookup"><span data-stu-id="66fd7-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="66fd7-153">Vous n’avez plus besoin toocall hello service tooget Id - générer des GUID ou tout autre identificateur, conservez-le sur l’appareil et envoient simplement principal tooyour ainsi que le canal de push (jeton d’appareil).</span><span class="sxs-lookup"><span data-stu-id="66fd7-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="66fd7-154">Sur hello principal, vous devez uniquement effectuer un appel unique : CreateOrUpdateInstallation, il est entièrement idempotent, nous avons tooretry libre si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="66fd7-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="66fd7-155">L’exemple pour Amazon Kindle Fire ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="66fd7-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="66fd7-156">Si vous souhaitez tooupdate il :</span><span class="sxs-lookup"><span data-stu-id="66fd7-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="66fd7-157">Pour les scénarios avancés, nous avons une fonctionnalité de mise à jour partielle qui permet de toomodify uniquement des propriétés particulières d’objet d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="66fd7-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="66fd7-158">La mise à jour partielle est un sous-ensemble d’opérations de correction JSON que vous pouvez exécuter sur l’objet de l’Installation.</span><span class="sxs-lookup"><span data-stu-id="66fd7-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="66fd7-159">Supprimer l’Installation :</span><span class="sxs-lookup"><span data-stu-id="66fd7-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="66fd7-160">CreateOrUpdate, Patch et Delete sont cohérents avec Get.</span><span class="sxs-lookup"><span data-stu-id="66fd7-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="66fd7-161">L’opération demandée simplement tombe en file d’attente système toohello au cours de l’appel de hello et sera exécutée en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="66fd7-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="66fd7-162">Notez que Get n’est pas conçu pour le scénario d’exécution principale, mais uniquement pour le débogage et à des fins de dépannage, il est étroitement limitée par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="66fd7-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="66fd7-163">Flux d’envoi pour les Installations est hello identique pour les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="66fd7-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="66fd7-164">Nous venons de créer un toohello de notification tootarget option Installation particulière - suffit d’utiliser balise « ID d’installation : {souhaité-id} ».</span><span class="sxs-lookup"><span data-stu-id="66fd7-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="66fd7-165">Pour l’exemple ci-dessus, elle ressemblerait à ceci :</span><span class="sxs-lookup"><span data-stu-id="66fd7-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="66fd7-166">Pour l’un des modèles :</span><span class="sxs-lookup"><span data-stu-id="66fd7-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="66fd7-167">planification des notifications (disponible pour le niveau STANDARD)</span><span class="sxs-lookup"><span data-stu-id="66fd7-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="66fd7-168">Bonjour même régulière d’envoi, mais avec un paramètre supplémentaire - scheduledTime qui indique que lorsque la notification doit être remise.</span><span class="sxs-lookup"><span data-stu-id="66fd7-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="66fd7-169">Le service accepte n’importe quel point dans le temps entre maintenant + 5 minutes et maintenant + 7 jours.</span><span class="sxs-lookup"><span data-stu-id="66fd7-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="66fd7-170">**Planification d’une notification native Windows :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="66fd7-171">Importation/exportation (disponible pour le niveau STANDARD)</span><span class="sxs-lookup"><span data-stu-id="66fd7-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="66fd7-172">Il est parfois requis tooperform en bloc par rapport à des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="66fd7-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="66fd7-173">Il est généralement pour l’intégration avec un autre système ou un correctif massive toosay mise à jour hello balises.</span><span class="sxs-lookup"><span data-stu-id="66fd7-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="66fd7-174">Il est fortement déconseillé toouse flux de Get/mise à jour si nous évoquons des milliers d’inscriptions.</span><span class="sxs-lookup"><span data-stu-id="66fd7-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="66fd7-175">Fonction d’importation/exportation est un scénario de hello toocover conçue.</span><span class="sxs-lookup"><span data-stu-id="66fd7-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="66fd7-176">Fondamentalement, vous fournissez un conteneur d’objets blob accès toosome sous votre compte de stockage en tant que source de données entrantes et l’emplacement de sortie.</span><span class="sxs-lookup"><span data-stu-id="66fd7-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="66fd7-177">**Envoi de la tâche d’exportation :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="66fd7-178">**Envoi de la tâche d’importation :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="66fd7-179">**Attendez que la tâche soit terminée :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="66fd7-180">**Obtenez toutes les tâches :**</span><span class="sxs-lookup"><span data-stu-id="66fd7-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="66fd7-181">**URI avec la signature SAS :** il s’agit d’URL hello de certains fichier blob ou un conteneur d’objets blob plus de jeu de paramètres tels que les autorisations et l’heure d’expiration, ainsi que la signature de toutes ces tâches effectuées à l’aide de la clé SAS du compte.</span><span class="sxs-lookup"><span data-stu-id="66fd7-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="66fd7-182">Le Kit de développement logiciel (SDK) Azure Storage Java dispose de nombreuses fonctionnalités, notamment la création de ce type d’URI.</span><span class="sxs-lookup"><span data-stu-id="66fd7-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="66fd7-183">En guise d’alternative simple vous pouvez examiner ImportExportE2E classe de test (à partir de l’emplacement de github hello) a une implémentation très compacte et de base de l’algorithme de signature.</span><span class="sxs-lookup"><span data-stu-id="66fd7-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="66fd7-184">Envoi de notifications</span><span class="sxs-lookup"><span data-stu-id="66fd7-184">Send Notifications</span></span>
<span data-ttu-id="66fd7-185">objet de Notification Hello est simplement un corps avec des en-têtes, des méthodes utilitaires aident dans la création d’objets de hello et des modèles de notifications.</span><span class="sxs-lookup"><span data-stu-id="66fd7-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="66fd7-186">**Windows Store et Windows Phone 8.1 (non-Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="66fd7-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="66fd7-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="66fd7-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="66fd7-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="66fd7-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="66fd7-189">**Windows Phone 8.0 et 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="66fd7-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="66fd7-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="66fd7-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="66fd7-191">**Envoyer tooTags**</span><span class="sxs-lookup"><span data-stu-id="66fd7-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="66fd7-192">**Envoyer tootag expression**</span><span class="sxs-lookup"><span data-stu-id="66fd7-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="66fd7-193">**Envoyer une notification modèle**</span><span class="sxs-lookup"><span data-stu-id="66fd7-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="66fd7-194">L’exécution de votre code Java produit normalement une notification qui apparaît sur votre appareil cible.</span><span class="sxs-lookup"><span data-stu-id="66fd7-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="66fd7-195"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66fd7-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="66fd7-196">Dans cette rubrique, nous vous avons montré comment toocreate REST simple Java client pour les concentrateurs de Notification.</span><span class="sxs-lookup"><span data-stu-id="66fd7-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="66fd7-197">À ce stade, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="66fd7-197">From here you can:</span></span>

* <span data-ttu-id="66fd7-198">Télécharger hello complète [Kit de développement logiciel Java], qui contient l’ensemble du code SDK hello.</span><span class="sxs-lookup"><span data-stu-id="66fd7-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="66fd7-199">Manipuler les exemples hello :</span><span class="sxs-lookup"><span data-stu-id="66fd7-199">Play with hello samples:</span></span>
  * <span data-ttu-id="66fd7-200">[Prise en main de Notification Hubs]</span><span class="sxs-lookup"><span data-stu-id="66fd7-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="66fd7-201">[Envoi des dernières nouvelles]</span><span class="sxs-lookup"><span data-stu-id="66fd7-201">[Send breaking news]</span></span>
  * <span data-ttu-id="66fd7-202">[Envoi de dernières nouvelles localisées]</span><span class="sxs-lookup"><span data-stu-id="66fd7-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="66fd7-203">[Envoyer des notifications aux utilisateurs de tooauthenticated]</span><span class="sxs-lookup"><span data-stu-id="66fd7-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="66fd7-204">[Envoyer des notifications d’inter-plateformes tooauthenticated utilisateurs]</span><span class="sxs-lookup"><span data-stu-id="66fd7-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[Kit de développement logiciel Java]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Prise en main de Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Envoi des dernières nouvelles]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Envoi de dernières nouvelles localisées]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Envoyer des notifications aux utilisateurs de tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Envoyer des notifications d’inter-plateformes tooauthenticated utilisateurs]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

