## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="ffada-101">Vue d’ensemble des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ffada-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="ffada-102">Les modèles Azure Resource Manager permettent toodeclaratively spécifier infrastructure IaaS Azure de hello en langage de Json en définissant des dépendances hello entre les ressources.</span><span class="sxs-lookup"><span data-stu-id="ffada-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="ffada-103">Pour obtenir une présentation détaillée des modèles de gestionnaire de ressources Azure, consultez l’article toohello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ffada-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="ffada-104">Présentation du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="ffada-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="ffada-105">Extrait de l’exemple de modèle pour les extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ffada-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="ffada-106">Déploiement d’extensions de machine virtuelle dans le cadre d’un modèle Azure Resource Manager nécessite que vous toodeclaratively spécifier la configuration de l’extension hello dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="ffada-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="ffada-107">Voici le format hello pour spécifier la configuration de l’extension hello.</span><span class="sxs-lookup"><span data-stu-id="ffada-107">Here is hello format for specifying hello extension configuration.</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

<span data-ttu-id="ffada-108">Comme vous pouvez voir à partir de hello ci-dessus, le modèle d’extension hello contient deux parties principales :</span><span class="sxs-lookup"><span data-stu-id="ffada-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="ffada-109">Nom de l’extension, éditeur et version.</span><span class="sxs-lookup"><span data-stu-id="ffada-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="ffada-110">Configuration de l’extension.</span><span class="sxs-lookup"><span data-stu-id="ffada-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="ffada-111">Serveur de publication hello identification, le type et typeHandlerVersion pour toute extension</span><span class="sxs-lookup"><span data-stu-id="ffada-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="ffada-112">Les extensions de machine virtuelle Azure sont publiées par Microsoft et approuvées éditeurs 3e et chaque extension est identifiée par son typeHandlerVersion de serveur de publication, le type et hello.</span><span class="sxs-lookup"><span data-stu-id="ffada-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="ffada-113">Ils peuvent être déterminés comme suit :</span><span class="sxs-lookup"><span data-stu-id="ffada-113">These can be determined as following:</span></span>  

