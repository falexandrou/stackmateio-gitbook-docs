# Provider

Currently, the only value supported is `aws` but we aim to support more providers that will be listed under the [supported services section](../general/supported-services.md). Unless specified otherwise, all services are going to use this provider as a default. This practically means that if you declare services that don't have a `provider` attribute specified, they will get auto-assigned the value for this attribute.
