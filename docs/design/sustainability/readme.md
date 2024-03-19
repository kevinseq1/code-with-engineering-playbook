# Sustainable Software Engineering

The choices made throughout the engineering process regarding cloud services, software architecture design and automation can have a big impact on the carbon footprint of a solution.
Some choices are always beneficial, like turning off unused resources.
Other choices require a more nuanced understanding of the business case at hand and its potential carbon impact.

## Goal

One goal of this section is to provide tangible guidance for what sustainable actions you can apply in certain situations and the tools to be able to implement those recommendations.
Another goal is to highlight the many resources available to learn about the wider domain of sustainable software.

## Sustainable Engineering Checklist

This checklist should be used to quickly identify scenarios for which common sustainable actions exist.
Check the box if the scenario applies to your project, then go through the actions and tools you can use to build more sustainable software for those cases.
If there are important nuances to consider, they will be linked in the `Disclaimers` section.

> For readability some considerations are blank, indicating that the action applies to the first consideration above it.

| ✅ | Consideration                                                                                                     | Action                                                                                                        | Principle                                                                                                                                                              | Tools                                                                                                                                                                                                                                                                   | Disclaimers                                                                                                                                    |
|---|-------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
|   | For any running software/services                                                                                 | Shutdown unused resources.                                                                                    | [Electricity Consumption](./sustainable-engineering-principles.md#electricity-consumption)                                                                             | [Identify Unassociated Resources](https://devblogs.microsoft.com/scripting/use-powershell-to-identify-unassociated-azure-resources/)                                                                                                                                    |                                                                                                                                                |
|   |                                                                                                                   | Resize physical or virtual machines to improve utilization.                                                   | [Energy Proportionality](./sustainable-engineering-principles.md#energy-proportionality)                                                                               | [Azure Advisor Cost Recommendations](https://docs.microsoft.com/en-us/azure/advisor/advisor-cost-recommendations)                                                                                                                                                       | [Understanding Advisor Recommendations](./sustainable-action-disclaimers.md#action-resize-physical-or-virtual-machines-to-improve-utilization) |
|   | For development and testing VMs                                                                                   | Configure VMs to shutdown during off-hours                                                                    | [Electricity Consumption](./sustainable-engineering-principles.md#electricity-consumption)                                                                             | [Start/Stop VMs during off-hours](https://docs.microsoft.com/en-us/azure/automation/automation-solution-vm-management-config)                                                                                                                                           |                                                                                                                                                |
|   | For VMs with attached volumes                                                                                     | Limit the amount of attached storage capacity to what you expect to use and expand as necessary               | [Electricity Consumption](./sustainable-engineering-principles.md#electricity-consumption)                                                                             | [Expanding storage of active VMs](https://docs.microsoft.com/en-us/azure/virtual-machines/expand-unmanaged-disks)                                                                                                                                                       | [Understanding the energy cost of storage](https://www.cloudcarbonfootprint.org/docs/methodology/#storage)                                     |
|   | For systems using object storage (Azure Blob Storage, AWS S3, GCP Cloud Storage, etc)                             | Compress infrequently accessed data                                                                           | [Electricity Consumption](./sustainable-engineering-principles.md#electricity-consumption), [Embodied Carbon](./sustainable-engineering-principles.md#embodied-carbon) | [Compressing and extracting files in .NET](https://docs.microsoft.com/en-us/dotnet/standard/io/how-to-compress-and-extract-files)                                                                                                                                       | [Understanding the energy cost of storage](https://www.cloudcarbonfootprint.org/docs/methodology/#storage)                                     |
|   |                                                                                                                   | Delete data when it is no longer needed                                                                       | [Electricity Consumption](./sustainable-engineering-principles.md#electricity-consumption)                                                                             | [Configuring a lifecycle management policy](https://docs.microsoft.com/en-us/azure/storage/blobs/lifecycle-management-policy-configure)                                                                                                                                 | [Understanding the energy cost of storage](https://www.cloudcarbonfootprint.org/docs/methodology/#storage)                                     |
|   | For systems running in on-premise data centers                                                                    | Migrate to hyperscale cloud provider                                                                          | [Embodied Carbon](./sustainable-engineering-principles.md#embodied-carbon), [Electricity Consumption](./sustainable-engineering-principles.md#electricity-consumption) | [Cloud Adoption Approaches](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/adopt/)                                                                                                                                                                     | [Carbon benefits of cloud computing](./sustainable-action-disclaimers.md#action-migrate-to-a-hyperscale-cloud-provider)                        |
|   | For systems migrating to a hyperscale cloud provider                                                              | Consider physically shipping data to the provider                                                             | [Networking](./sustainable-engineering-principles.md#networking)                                                                                                       | [Azure Data Box](https://azure.microsoft.com/en-us/services/databox/)                                                                                                                                                                                                   | [Understanding data shipping tradeoffs](./sustainable-action-disclaimers.md#action-consider-physically-shipping-data-to-the-provider)          |
|   | For [time-flexible workloads](https://docs.microsoft.com/en-us/azure/architecture/best-practices/background-jobs) | Utilize "Spot VMs" for compute                                                                                | [Demand Shaping](./sustainable-engineering-principles.md#demand-shaping)                                                                                               | [How to use Spot VMs](https://docs.microsoft.com/en-us/azure/virtual-machines/spot-vms)                                                                                                                                                                                 |                                                                                                                                                |
|   | For services with varied utilization patterns                                                                     | Configure Autoscaling                                                                                         | [Energy Proportionality](./sustainable-engineering-principles.md#energy-proportionality)                                                                               | [Autoscaling Documentation](https://docs.microsoft.com/en-us/azure/architecture/best-practices/auto-scaling)                                                                                                                                                            |                                                                                                                                                |
|   |                                                                                                                   | Use serverless functions                                                                                      | [Energy Proportionality](./sustainable-engineering-principles.md#energy-proportionality)                                                                               | [Serverless Architecture Design](https://docs.microsoft.com/en-us/azure/architecture/serverless-quest/serverless-overview)                                                                                                                                              |                                                                                                                                                |
|   | For services with geographically co-located users (EG internal employee apps)                                     | Select a data center region that is physically close to them                                                  | [Networking](./sustainable-engineering-principles.md#networking)                                                                                                       | [Azure products available by region](https://azure.microsoft.com/en-us/global-infrastructure/services/)                                                                                                                                                                 |                                                                                                                                                |
|   |                                                                                                                   | Consider running edge devices to reduce excessive data transfer                                               | [Networking](./sustainable-engineering-principles.md#networking)                                                                                                       | [Azure Stack Edge](https://azure.microsoft.com/en-us/products/azure-stack/edge/)                                                                                                                                                                                        | [Understanding edge tradeoffs](./sustainable-action-disclaimers.md#action-consider-running-an-edge-device)                                     |
|   | For systems sending data over the network                                                                         | Use caching policies to keep data on the local machine                                                        | [Networking](./sustainable-engineering-principles.md#networking)                                                                                                       | [HTTP caching APIs](https://web.dev/http-cache/), [Cache Management in .NET](https://learn.microsoft.com/en-us/dotnet/framework/network-programming/cache-management-for-network-applications)                                                                          | [Understanding caching tradeoffs](./sustainable-action-disclaimers.md#action-use-caching-policies)                                             |
|   |                                                                                                                   | Consider caching data close to end users with a [CDN](https://en.wikipedia.org/wiki/Content_delivery_network) | [Networking](./sustainable-engineering-principles.md#networking)                                                                                                       | [Benefits of a CDN](https://docs.microsoft.com/en-us/azure/frontdoor/front-door-overview#key-benefits)                                                                                                                                                                  | [Understanding CDN tradeoffs](./sustainable-action-disclaimers.md#action-consider-caching-data-close-to-end-users-with-a-CDN)                  |
|   |                                                                                                                   | Send only the data that will be used                                                                          | [Networking](./sustainable-engineering-principles.md#networking)                                                                                                       |                                                                                                                                                                                                                                                                         |                                                                                                                                                |
|   |                                                                                                                   | Compress data to reduce the size                                                                              | [Networking](./sustainable-engineering-principles.md#networking)                                                                                                       | [Compressing and extracting files in .NET](https://docs.microsoft.com/en-us/dotnet/standard/io/how-to-compress-and-extract-files)                                                                                                                                       |                                                                                                                                                |
|   | When designing for the end user                                                                                   | Consider giving users visibility and control over their energy usage                                          | [Electricity Consumption](./sustainable-engineering-principles.md#electricity-consumption) [Demand Shaping](./sustainable-engineering-principles.md#demand-shaping)    | [Designing for eco-mode](https://principles.green/principles/demand-shaping/#heading-eco-modes)                                                                                                                                                                         |                                                                                                                                                |
|   |                                                                                                                   | Design and test your application to be compatible for a wide variety of devices, especially older devices     | [Embodied Carbon](./sustainable-engineering-principles.md#embodied-carbon)                                                                                             | [Extending device lifespan](https://medium.com/google-design/to-make-apps-accessible-make-them-compatible-with-different-devices-11298c6d3f06) [Compatibility Testing](https://www.techdim.com/what-is-compatibility-testing/)                                          |                                                                                                                                                |
|   | When selecting a programming language                                                                             | Consider the energy efficiency of languages                                                                   | [Electricity Consumption](./sustainable-engineering-principles.md#electricity-consumption)                                                                             | [Reasoning about the energy consumption of programming languages](https://thenewstack.io/which-programming-languages-use-the-least-electricity/), [Programming Language Energy Efficiency (PDF)](https://greenlab.di.uminho.pt/wp-content/uploads/2017/10/sleFinal.pdf) | [Making informed programming language choices](./sustainable-action-disclaimers.md#action-consider-the-energy-efficiency-of-languages)         |

## Resources

- [Principles of Green Software Engineering](https://principles.green/)
- [Green Software Foundation](https://greensoftware.foundation/)
- [Microsoft Cloud for Sustainability](https://www.microsoft.com/en-us/sustainability)
- [Learning Module: Sustainable Software
Engineering](https://learn.microsoft.com/en-us/learn/modules/sustainable-software-engineering-overview/)

## Tools

- [Carbon-Aware SDK](https://github.com/Green-Software-Foundation/carbon-aware-sdk)
- ["Awesome List" of Green Software](https://github.com/Green-Software-Foundation/awesome-green-software)
- [Emissions Impact](https://appsource.microsoft.com/en-us/product/power-bi/coi-sustainability.emissions_impact_dashboard)
- [Azure GreenAI Carbon-Intensity API](https://carbon-aware-api.azurewebsites.net/swagger/index.html)

## Projects

- [Sustainability through SpotVMs](https://github.com/hybridflux/SparkOnSpot)