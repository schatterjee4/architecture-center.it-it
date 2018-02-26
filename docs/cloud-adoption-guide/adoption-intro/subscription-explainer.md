---
title: 'Spiegazione: Informazioni sulla sottoscrizione di Azure'
description: Spiega le sottoscrizioni, gli account e le offerte di Azure
author: alexbuckgit
ms.openlocfilehash: 1650d90d6f78b46b7fe4128d2dab6a80bd6cca78
ms.sourcegitcommit: 3d9ee03e2dda23753661a80c7106d1789f5223bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2018
---
# <a name="explainer-what-is-an-azure-subscription"></a><span data-ttu-id="9e5cf-103">Spiegazione: Informazioni sulla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="9e5cf-103">Explainer: What is an Azure subscription?</span></span>

<span data-ttu-id="9e5cf-104">Nell'articolo [Spiegazione: Informazioni su un tenant di Azure Active Directory](tenant-explainer.md) si è appreso che l'identità digitale dell'organizzazione viene archiviata in un tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-104">In the [what is an Azure Active Directory tenant?](tenant-explainer.md) explainer article, you learned that digital identity for your organization is stored in an Azure Active Directory tenant.</span></span> <span data-ttu-id="9e5cf-105">Si è inoltre appreso che Azure si affida ad Azure Active Directory per autenticare le richieste utente allo scopo di creare, leggere, aggiornare o eliminare una risorsa.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-105">You also learned that Azure trusts Azure Active Directory to authenticate user requests to create, read, update, or delete a resource.</span></span> 

<span data-ttu-id="9e5cf-106">Fondamentalmente, si comprende il motivo per cui è necessario limitare l'accesso a queste operazioni su una risorsa, ovvero per impedire che utenti non autenticati e non autorizzati accedano alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-106">We fundamentally understand why it's necessary to restrict access to these operations on a resource - to prevent unauthenticated and unauthorized users from accessing our resources.</span></span> <span data-ttu-id="9e5cf-107">Queste operazioni sulle risorse, tuttavia, hanno anche altre proprietà che un'organizzazione vorrebbe controllare, come il numero di risorse che un utente o un gruppo di utenti può creare, oltre al costo di esecuzione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-107">However, these resource operations have other properties that an organization would like to control, such as the number of resources a user or group of users is allowed to create, and, the cost to run those resources.</span></span> 

<span data-ttu-id="9e5cf-108">Azure implementa questo controllo, che prende il nome di **sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-108">Azure implements this control, and it is named a **subscription**.</span></span> <span data-ttu-id="9e5cf-109">In una sottoscrizione vengono raggruppati gli utenti e le risorse create dagli utenti.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-109">A subscription groups together users and the resources that have been created by those users.</span></span> <span data-ttu-id="9e5cf-110">Ognuna di queste risorse contribuisce a un [limite complessivo][subscription-service-limits] su una determinata risorsa.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-110">Each of those resources contributes to an [overall limit][subscription-service-limits] on that particular resource.</span></span>

<span data-ttu-id="9e5cf-111">Le organizzazioni possono usare le sottoscrizioni per gestire i costi e la creazione di risorse in base a utenti, team e progetti o adottando molte altre strategie.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-111">Organizations can use subscriptions to manage costs and creation of resource by users, teams, projects, or using many other strategies.</span></span> <span data-ttu-id="9e5cf-112">Queste strategie verranno descritte negli articoli relativi alle fasi di adozione intermedia e avanzata.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-112">These strategies will be discussed in the intermediate and advanced adoption stage articles.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9e5cf-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e5cf-113">Next steps</span></span>

* <span data-ttu-id="9e5cf-114">Dopo aver appreso le nozioni di base relative alle sottoscrizioni di Azure, è ora necessario acquisire informazioni sulla [creazione di una sottoscrizione](subscription.md) prima di creare le prime risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e5cf-114">Now that you have learned about Azure subscriptions, learn more about [creating a subscription](subscription.md) before you create your first Azure resources..</span></span>

<!-- Links -->
[azure-get-started]: https://azure.microsoft.com/get-started/
[azure-offers]: https://azure.microsoft.com/support/legal/offer-details/
[azure-free-trial]: https://azure.microsoft.com/offers/ms-azr-0044p/
[azure-change-subscription-offer]: /azure/billing/billing-how-to-switch-azure-offer
[microsoft-account]: https://account.microsoft.com/account
[subscription-service-limits]: /azure/azure-subscription-service-limits
[docs-organizational-account]: https://docs.microsoft.com/azure/active-directory/sign-up-organization