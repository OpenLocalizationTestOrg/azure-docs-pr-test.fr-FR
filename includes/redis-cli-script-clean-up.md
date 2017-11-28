## <a name="clean-up-deployment"></a><span data-ttu-id="015ce-101">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="015ce-101">Clean up deployment</span></span> 

<span data-ttu-id="015ce-102">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’instance Cache Redis Azure et toutes les ressources associées dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="015ce-102">After the script sample has been run, the follow command can be used to remove the resource group, Azure Redis Cache instance, and any related resources in the resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```