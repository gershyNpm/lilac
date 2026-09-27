When writing a new Flower keep the following in mind:
1. Will it be automatically tagged (by default_tags set on the provider)? Flowers are expected to do a solid job assigning tags to all their encompassed aws resources, and are *required* to fully tag resources that can generate costs.
2. Can it result in dynamically-created (post-terraform-apply) infra that will prevent `terraform destroy` from accepting? If so need to add:
```ts
new PetalTerraform.Output(handle, {}, () => ({ cleanup: { [flowerId]: logger => logger.scope('cleanup', {}, async logger => {
  
  // ... clean up dynamically created infra ...
  
}}}));
```

Note that lilac takes a rare deviation from gershy terminology. Instead of saying that we "launch" and "cancel" gardens and flowers, we instead say that we "grow" and "rake" them. The cute factor here is considered worth the deviation!