## <a name="clean-up-deployment"></a><span data-ttu-id="0b0da-101">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="0b0da-101">Clean up deployment</span></span> 

<span data-ttu-id="0b0da-102">Après exécution de l’exemple de script hello, commande de suivi hello peut être groupe de ressources utilisé tooremove hello, instance de Cache Redis Azure et toutes les ressources associées dans un groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="0b0da-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```