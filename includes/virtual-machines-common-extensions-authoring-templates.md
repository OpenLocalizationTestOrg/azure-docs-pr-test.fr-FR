## <a name="overview-of-azure-resource-manager-templates"></a>Vue d’ensemble des modèles Azure Resource Manager
Les modèles Azure Resource Manager permettent toodeclaratively spécifier infrastructure IaaS Azure de hello en langage de Json en définissant des dépendances hello entre les ressources. Pour obtenir une présentation détaillée des modèles de gestionnaire de ressources Azure, consultez l’article toohello ci-dessous :

[Présentation du groupe de ressources](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Extrait de l’exemple de modèle pour les extensions de machine virtuelle.
Déploiement d’extensions de machine virtuelle dans le cadre d’un modèle Azure Resource Manager nécessite que vous toodeclaratively spécifier la configuration de l’extension hello dans le modèle de hello.
Voici le format hello pour spécifier la configuration de l’extension hello.

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

Comme vous pouvez voir à partir de hello ci-dessus, le modèle d’extension hello contient deux parties principales :

1. Nom de l’extension, éditeur et version.
2. Configuration de l’extension.

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Serveur de publication hello identification, le type et typeHandlerVersion pour toute extension
Les extensions de machine virtuelle Azure sont publiées par Microsoft et approuvées éditeurs 3e et chaque extension est identifiée par son typeHandlerVersion de serveur de publication, le type et hello. Ils peuvent être déterminés comme suit :  

