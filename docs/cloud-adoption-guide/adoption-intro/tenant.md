---
title: 'Indicazioni: Struttura di un tenant di Azure AD'
description: Indicazioni per la progettazione di un tenant di Azure nell'ambito di una strategia di adozione del cloud di base
author: telmosampaio
ms.openlocfilehash: 5bf710f74bde04e041f2896b4a638c3513e4aa44
ms.sourcegitcommit: 2e8b06e9c07875d65b91d5431bfd4bc465a7a242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="guidance-azure-ad-tenant-design"></a><span data-ttu-id="4e953-103">Indicazioni: Struttura di un tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e953-103">Guidance: Azure AD tenant design</span></span>

<span data-ttu-id="4e953-104">Un tenant di Azure AD fornisce servizi di gestione delle identità digitali e spazi dei nomi usati per una o più [sottoscrizioni di Azure](subscription-explainer.md).</span><span class="sxs-lookup"><span data-stu-id="4e953-104">An Azure AD tenant provides digital identity services and namespaces used for one or more [Azure subscriptions](subscription-explainer.md).</span></span> <span data-ttu-id="4e953-105">Se si seguono i passaggi della strategia di adozione di base, si è già appreso [come ottenere un tenant di Azure AD][how-to-get-aad-tenant].</span><span class="sxs-lookup"><span data-stu-id="4e953-105">If you are following the foundational adoption outline, you have already learned [how to get an Azure AD tenant][how-to-get-aad-tenant].</span></span> 

## <a name="design-considerations"></a><span data-ttu-id="4e953-106">Considerazioni sulla progettazione</span><span class="sxs-lookup"><span data-stu-id="4e953-106">Design considerations</span></span>

- <span data-ttu-id="4e953-107">Durante la fase di adozione di base è possibile iniziare con un singolo tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e953-107">At the foundational adoption stage, you can begin with a single Azure AD tenant.</span></span> <span data-ttu-id="4e953-108">Se la propria organizzazione ha già una sottoscrizione di Office 365 o di Azure, si avrà già a disposizione un tenant di Azure AD da usare.</span><span class="sxs-lookup"><span data-stu-id="4e953-108">If your organization has an existing Office 365 subscription or an Azure subscription, you already have an Azure AD tenant that you can use.</span></span> <span data-ttu-id="4e953-109">Se invece nessuna di queste due sottoscrizioni è disponibile, è possibile leggere altre informazioni su [come ottenere un tenant di Azure AD][how-to-get-aad-tenant].</span><span class="sxs-lookup"><span data-stu-id="4e953-109">If you do not have either or of these, you can learn more about [how to get an Azure AD tenant][how-to-get-aad-tenant].</span></span> 
- <span data-ttu-id="4e953-110">Nelle fasi di adozione intermedia e avanzata si apprenderà come eseguire la sincronizzazione o la federazione delle directory locali con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e953-110">In the intermediate and advanced adoption stages, you will learn how to synchronize or federate on-premises directories with Azure AD.</span></span> <span data-ttu-id="4e953-111">In questo modo sarà possibile usare l'identità digitale locale in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e953-111">This will allow you to use on-premises digital identity in Azure AD.</span></span> <span data-ttu-id="4e953-112">Durante la fase di base, tuttavia, si aggiungeranno nuovi utenti che hanno solo identità relative al singolo tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e953-112">However, at the foundational stage, you will be adding new users that only have identity your single Azure AD tenant.</span></span> <span data-ttu-id="4e953-113">e si dovranno gestire tali identità.</span><span class="sxs-lookup"><span data-stu-id="4e953-113">You are be responsible for managing those identities.</span></span> <span data-ttu-id="4e953-114">Sarà ad esempio necessario caricare nuovi utenti di Azure AD, scaricare gli utenti di Azure AD che non vogliono più accedere alle risorse di Azure e apportare altre modifiche alle autorizzazioni degli utenti.</span><span class="sxs-lookup"><span data-stu-id="4e953-114">For example, you will have to on-board new Azure AD users, off-board Azure AD users that you no longer wish to have access to Azure resources, and other changes to user permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e953-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4e953-115">Next Steps</span></span>

* <span data-ttu-id="4e953-116">Ora che è disponibile un tenant di Azure AD, si apprenderà [come aggiungere un utente][azure-ad-add-user].</span><span class="sxs-lookup"><span data-stu-id="4e953-116">Now that you have an Azure AD tenant, learn [how to add a user][azure-ad-add-user].</span></span> <span data-ttu-id="4e953-117">Dopo l'aggiunta di uno o più nuovi utenti al tenant di Azure AD, il passaggio successivo sarà quello di apprendere i concetti relativi alle [sottoscrizioni di Azure](subscription-explainer.md).</span><span class="sxs-lookup"><span data-stu-id="4e953-117">After you have added one or more new users to your Azure AD tenant, your next step is learning about [Azure subscriptions](subscription-explainer.md).</span></span>

<!-- Links -->

[azure-ad-add-user]: /azure/active-directory/add-users-azure-active-directory?toc=/azure/architecture/cloud-adoption-guide/toc.json
[docs-manage-azure-ad]: /azure/active-directory/active-directory-administer?toc=/azure/architecture/cloud-adoption-guide/toc.json
[docs-tenant]: /azure/active-directory/develop/active-directory-howto-tenant?toc=/azure/architecture/cloud-adoption-guide/toc.json
[docs-associate-subscription]: /azure/active-directory/active-directory-how-subscriptions-associated-directory?toc=/azure/architecture/cloud-adoption-guide/toc.json
[how-to-get-aad-tenant]: /azure/active-directory/develop/active-directory-howto-tenant?toc=/azure/architecture/cloud-adoption-guide/toc.json