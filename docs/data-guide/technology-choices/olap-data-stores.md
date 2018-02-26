---
title: Scelta di un archivio dati OLAP
description: 
author: zoinerTejada
ms:date: 02/12/2018
ms.openlocfilehash: f3041b95696c9408a2c9ab747fe1ec3041db0743
ms.sourcegitcommit: 90cf2de795e50571d597cfcb9b302e48933e7f18
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="choosing-an-olap-data-store-in-azure"></a><span data-ttu-id="7eac5-102">Scelta di un archivio dati OLAP in Azure</span><span class="sxs-lookup"><span data-stu-id="7eac5-102">Choosing an OLAP data store in Azure</span></span>

<span data-ttu-id="7eac5-103">OLAP (Online Analytical Processing) è una tecnologia che consente di organizzare i database aziendali di grandi dimensioni e supporta l'esecuzione di analisi complesse.</span><span class="sxs-lookup"><span data-stu-id="7eac5-103">Online analytical processing (OLAP) is a technology that organizes large business databases and supports complex analysis.</span></span> <span data-ttu-id="7eac5-104">Questo argomento mette a confronto le opzioni disponibili in Azure per le soluzioni OLAP.</span><span class="sxs-lookup"><span data-stu-id="7eac5-104">This topic compares the options for OLAP solutions in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="7eac5-105">Per altre informazioni sull'uso di un archivio dati OLAP, vedere [OLAP (Online Analytical Processing)](../scenarios/online-analytical-processing.md).</span><span class="sxs-lookup"><span data-stu-id="7eac5-105">For more information about when to use an OLAP data store, see [Online analytical processing](../scenarios/online-analytical-processing.md).</span></span>

## <a name="what-are-your-options-when-choosing-an-olap-data-store"></a><span data-ttu-id="7eac5-106">Opzioni disponibili per la scelta di un archivio dati OLAP</span><span class="sxs-lookup"><span data-stu-id="7eac5-106">What are your options when choosing an OLAP data store?</span></span>

<span data-ttu-id="7eac5-107">In Azure tutti gli archivi dati elencati di seguito soddisfano i requisiti di base per OLAP:</span><span class="sxs-lookup"><span data-stu-id="7eac5-107">In Azure, all of the following data stores will meet the core requirements for OLAP:</span></span>

- [<span data-ttu-id="7eac5-108">SQL Server con indici columnstore</span><span class="sxs-lookup"><span data-stu-id="7eac5-108">SQL Server with Columnstore indexes</span></span>](/sql/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics)
- [<span data-ttu-id="7eac5-109">Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7eac5-109">Azure Analysis Services</span></span>](/azure/analysis-services/analysis-services-overview)
- [<span data-ttu-id="7eac5-110">SQL Server Analysis Services (SSAS)</span><span class="sxs-lookup"><span data-stu-id="7eac5-110">SQL Server Analysis Services (SSAS)</span></span>](/sql/analysis-services/analysis-services)

<span data-ttu-id="7eac5-111">SQL Server Analysis Services (SSAS) offre funzionalità OLAP e di data mining per applicazioni di business intelligence.</span><span class="sxs-lookup"><span data-stu-id="7eac5-111">SQL Server Analysis Services (SSAS) offers OLAP and data mining functionality for business intelligence applications.</span></span> <span data-ttu-id="7eac5-112">È possibile installare SSAS nei server locali oppure ospitarlo all'interno di una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="7eac5-112">You can either install SSAS on local servers, or host within a virtual machine in Azure.</span></span> <span data-ttu-id="7eac5-113">Azure Analysis Services è un servizio completamente gestito che fornisce le stesse funzionalità principali di SSAS.</span><span class="sxs-lookup"><span data-stu-id="7eac5-113">Azure Analysis Services is a fully managed service that provides the same major features as SSAS.</span></span> <span data-ttu-id="7eac5-114">Azure Analysis Services supporta la connessione a [varie origini dati](/azure/analysis-services/analysis-services-datasource) sul cloud e locali nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7eac5-114">Azure Analysis Services supports connecting to [various data sources](/azure/analysis-services/analysis-services-datasource) in the cloud and on-premises in your organization.</span></span>

<span data-ttu-id="7eac5-115">Gli indici columnstore cluster sono disponibili in SQL Server 2014 e versioni successive, oltre che nel database SQL di Azure, e sono ideali per i carichi di lavoro OLAP.</span><span class="sxs-lookup"><span data-stu-id="7eac5-115">Clustered Columnstore indexes are available in SQL Server 2014 and above, as well as Azure SQL Database, and are ideal for OLAP workloads.</span></span> <span data-ttu-id="7eac5-116">Tuttavia, a partire da SQL Server 2016 (incluso il database SQL di Azure), è possibile sfruttare la tecnologia di elaborazione HTAP (Hybrid Transactional/Analytics Processing) usando indici columnstore non cluster aggiornabili.</span><span class="sxs-lookup"><span data-stu-id="7eac5-116">However, beginning with SQL Server 2016 (including Azure SQL Database), you can take advantage of hybrid transactional/analytics processing (HTAP) through the use of updateable nonclustered columnstore indexes.</span></span> <span data-ttu-id="7eac5-117">HTAP consente di eseguire l'elaborazione OLTP e OLAP sulla stessa piattaforma, eliminando così la necessità di archiviare più copie dei dati e di usare sistemi OLTP e OLAP distinti.</span><span class="sxs-lookup"><span data-stu-id="7eac5-117">HTAP enables you to perform OLTP and OLAP processing on the same platform, which removes the need to store multiple copies of your data, and eliminates the need for distinct OLTP and OLAP systems.</span></span> <span data-ttu-id="7eac5-118">Per altre informazioni, vedere [Introduzione a columnstore per l'analisi operativa in tempo reale](/sql/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics).</span><span class="sxs-lookup"><span data-stu-id="7eac5-118">For more information, see [Get started with Columnstore for real-time operational analytics](/sql/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics).</span></span>

## <a name="key-selection-criteria"></a><span data-ttu-id="7eac5-119">Criteri di scelta principali</span><span class="sxs-lookup"><span data-stu-id="7eac5-119">Key selection criteria</span></span>

<span data-ttu-id="7eac5-120">Per limitare le possibilità di scelta, rispondere prima di tutto a queste domande:</span><span class="sxs-lookup"><span data-stu-id="7eac5-120">To narrow the choices, start by answering these questions:</span></span>

- <span data-ttu-id="7eac5-121">Si vuole usare un servizio gestito anziché gestire direttamente i propri server?</span><span class="sxs-lookup"><span data-stu-id="7eac5-121">Do you want a managed service rather than managing your own servers?</span></span>

- <span data-ttu-id="7eac5-122">Si richiede l'autenticazione sicura con Azure Active Directory (Azure AD)?</span><span class="sxs-lookup"><span data-stu-id="7eac5-122">Do you require secure authentication using Azure Active Directory (Azure AD)?</span></span>

- <span data-ttu-id="7eac5-123">Si vogliono eseguire analisi in tempo reale?</span><span class="sxs-lookup"><span data-stu-id="7eac5-123">Do you want to conduct real-time analytics?</span></span> <span data-ttu-id="7eac5-124">In caso affermativo, limitare la scelta alle opzioni che supportano l'analisi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="7eac5-124">If so, narrow your options to those that support real-time analytics.</span></span> 

    <span data-ttu-id="7eac5-125">In questo contesto l'*analisi in tempo reale* si applica a una singola origine dati, ad esempio un'applicazione ERP (Enterprise Resource Planning), che gestisce contemporaneamente un carico di lavoro operativo e un carico di lavoro di analisi.</span><span class="sxs-lookup"><span data-stu-id="7eac5-125">*Real-time analytics* in this context applies to a single data source, such as an enterprise resource planning (ERP) application, that will run both an operational and an analytics workload.</span></span> <span data-ttu-id="7eac5-126">Se si ha la necessità di integrare dati provenienti da più origini o di ottenere prestazioni di analisi estremamente elevate con l'uso di dati preaggregati, ad esempio i cubi, è possibile richiedere un data warehouse separato.</span><span class="sxs-lookup"><span data-stu-id="7eac5-126">If you need to integrate data from multiple sources, or require extreme analytics performance by using pre-aggregated data such as cubes, you might still require a separate data warehouse.</span></span>

- <span data-ttu-id="7eac5-127">È necessario usare dati preaggregati, ad esempio per fornire modelli semantici che consentano un'analisi più intuitiva a livello aziendale?</span><span class="sxs-lookup"><span data-stu-id="7eac5-127">Do you need to use pre-aggregated data, for example to provide semantic models that make analytics more business user friendly?</span></span> <span data-ttu-id="7eac5-128">In caso affermativo, scegliere un'opzione con il supporto per cubi multidimensionali o modelli semantici tabulari.</span><span class="sxs-lookup"><span data-stu-id="7eac5-128">If yes, choose an option that supports multidimensional cubes or tabular semantic models.</span></span> 

    <span data-ttu-id="7eac5-129">La disponibilità di dati preaggregati può aiutare gli utenti a calcolare le aggregazioni di dati in modo coerente.</span><span class="sxs-lookup"><span data-stu-id="7eac5-129">Providing aggregates can help users consistently calculate data aggregates.</span></span> <span data-ttu-id="7eac5-130">I dati preaggregati consentono inoltre di migliorare notevolmente le prestazioni quando si gestiscono più colonne per un numero elevato righe.</span><span class="sxs-lookup"><span data-stu-id="7eac5-130">Pre-aggregated data can also provide a large performance boost when dealing with several columns across many rows.</span></span> <span data-ttu-id="7eac5-131">I dati possono essere preaggregati in cubi multidimensionali o in modelli semantici tabulari.</span><span class="sxs-lookup"><span data-stu-id="7eac5-131">Data can be pre-aggregated in multidimensional cubes or tabular semantic models.</span></span>

- <span data-ttu-id="7eac5-132">È necessario integrare dati provenienti da più origini, oltre all'archivio dati OLTP?</span><span class="sxs-lookup"><span data-stu-id="7eac5-132">Do you need to integrate data from several sources, beyond your OLTP data store?</span></span> <span data-ttu-id="7eac5-133">In caso affermativo, prendere in considerazione le opzioni che facilitano l'integrazione di più origini dati.</span><span class="sxs-lookup"><span data-stu-id="7eac5-133">If so, consider options that easily integrate multiple data sources.</span></span>

## <a name="capability-matrix"></a><span data-ttu-id="7eac5-134">Matrice delle funzionalità</span><span class="sxs-lookup"><span data-stu-id="7eac5-134">Capability matrix</span></span>

<span data-ttu-id="7eac5-135">Le tabelle seguenti contengono un riepilogo delle differenze principali in termini di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7eac5-135">The following tables summarize the key differences in capabilities.</span></span>

### <a name="general-capabilities"></a><span data-ttu-id="7eac5-136">Funzionalità generali</span><span class="sxs-lookup"><span data-stu-id="7eac5-136">General capabilities</span></span>

| | <span data-ttu-id="7eac5-137">Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7eac5-137">Azure Analysis Services</span></span> | <span data-ttu-id="7eac5-138">SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7eac5-138">SQL Server Analysis Services</span></span> | <span data-ttu-id="7eac5-139">SQL Server con indici columnstore</span><span class="sxs-lookup"><span data-stu-id="7eac5-139">SQL Server with Columnstore Indexes</span></span> | <span data-ttu-id="7eac5-140">Database SQL di Azure con indici columnstore</span><span class="sxs-lookup"><span data-stu-id="7eac5-140">Azure SQL Database with Columnstore Indexes</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="7eac5-141">Servizio gestito</span><span class="sxs-lookup"><span data-stu-id="7eac5-141">Is managed service</span></span> | <span data-ttu-id="7eac5-142">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-142">Yes</span></span> | <span data-ttu-id="7eac5-143">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-143">No</span></span> | <span data-ttu-id="7eac5-144">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-144">No</span></span> | <span data-ttu-id="7eac5-145">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-145">Yes</span></span> |
| <span data-ttu-id="7eac5-146">Supporto per i cubi multidimensionali</span><span class="sxs-lookup"><span data-stu-id="7eac5-146">Supports multidimensional cubes</span></span> | <span data-ttu-id="7eac5-147">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-147">No</span></span> | <span data-ttu-id="7eac5-148">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-148">Yes</span></span> | <span data-ttu-id="7eac5-149">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-149">No</span></span> | <span data-ttu-id="7eac5-150">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-150">No</span></span> |
| <span data-ttu-id="7eac5-151">Supporto per i modelli semantici tabulari</span><span class="sxs-lookup"><span data-stu-id="7eac5-151">Supports tabular semantic models</span></span> | <span data-ttu-id="7eac5-152">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-152">Yes</span></span> | <span data-ttu-id="7eac5-153">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-153">Yes</span></span> | <span data-ttu-id="7eac5-154">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-154">No</span></span> | <span data-ttu-id="7eac5-155">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-155">No</span></span> |
| <span data-ttu-id="7eac5-156">Facilità di integrazione di più origini dati</span><span class="sxs-lookup"><span data-stu-id="7eac5-156">Easily integrate multiple data sources</span></span> | <span data-ttu-id="7eac5-157">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-157">Yes</span></span> | <span data-ttu-id="7eac5-158">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-158">Yes</span></span> | <span data-ttu-id="7eac5-159">No <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="7eac5-159">No <sup>1</sup></span></span> | <span data-ttu-id="7eac5-160">No <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="7eac5-160">No <sup>1</sup></span></span> |
| <span data-ttu-id="7eac5-161">Supporto per l'analisi in tempo reale</span><span class="sxs-lookup"><span data-stu-id="7eac5-161">Supports real-time analytics</span></span> | <span data-ttu-id="7eac5-162">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-162">No</span></span> | <span data-ttu-id="7eac5-163">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-163">No</span></span> | <span data-ttu-id="7eac5-164">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-164">Yes</span></span> | <span data-ttu-id="7eac5-165">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-165">Yes</span></span> |
| <span data-ttu-id="7eac5-166">Necessità di un processo per copiare i dati da una o più origini</span><span class="sxs-lookup"><span data-stu-id="7eac5-166">Requires process to copy data from source(s)</span></span> | <span data-ttu-id="7eac5-167">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-167">Yes</span></span> | <span data-ttu-id="7eac5-168">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-168">Yes</span></span> | <span data-ttu-id="7eac5-169">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-169">No</span></span> | <span data-ttu-id="7eac5-170">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-170">No</span></span> |
| <span data-ttu-id="7eac5-171">Integrazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7eac5-171">Azure AD integration</span></span> | <span data-ttu-id="7eac5-172">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-172">Yes</span></span> | <span data-ttu-id="7eac5-173">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-173">No</span></span> | <span data-ttu-id="7eac5-174">No <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="7eac5-174">No <sup>2</sup></span></span> | <span data-ttu-id="7eac5-175">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-175">Yes</span></span> |

<span data-ttu-id="7eac5-176">[1] Anche se SQL Server e il database SQL di Azure non possono essere usati per eseguire query da più origini dati esterne e integrare tali origini, è possibile creare una pipeline che esegua automaticamente questa operazione usando [SSIS](/sql/integration-services/sql-server-integration-services) o [Azure Data Factory](/azure/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="7eac5-176">[1] Although SQL Server and Azure SQL Database cannot be used to query from and integrate multiple external data sources, you can still build a pipeline that does this for you using [SSIS](/sql/integration-services/sql-server-integration-services) or [Azure Data Factory](/azure/data-factory/).</span></span> <span data-ttu-id="7eac5-177">Con SQL Server ospitato in una macchina virtuale di Azure, è possibile sfruttare opzioni aggiuntive, ad esempio i server collegati e [PolyBase](/sql/relational-databases/polybase/polybase-guide).</span><span class="sxs-lookup"><span data-stu-id="7eac5-177">SQL Server hosted in an Azure VM has additional options, such as linked servers and [PolyBase](/sql/relational-databases/polybase/polybase-guide).</span></span> <span data-ttu-id="7eac5-178">Per altre informazioni, vedere [Scelta di una tecnologia di orchestrazione di una pipeline di dati in Azure](../technology-choices/pipeline-orchestration-data-movement.md).</span><span class="sxs-lookup"><span data-stu-id="7eac5-178">For more information, see [Pipeline orchestration, control flow, and data movement](../technology-choices/pipeline-orchestration-data-movement.md).</span></span>

<span data-ttu-id="7eac5-179">[2] La connessione a SQL Server in esecuzione in una macchina virtuale di Azure non è supportata con un account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7eac5-179">[2] Connecting to SQL Server running on an Azure Virtual Machine is not supported using an Azure AD account.</span></span> <span data-ttu-id="7eac5-180">Usare un account Active Directory di dominio.</span><span class="sxs-lookup"><span data-stu-id="7eac5-180">Use a domain Active Directory account instead.</span></span>

### <a name="scalability-capabilities"></a><span data-ttu-id="7eac5-181">Funzionalità di scalabilità</span><span class="sxs-lookup"><span data-stu-id="7eac5-181">Scalability Capabilities</span></span>

| | <span data-ttu-id="7eac5-182">Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7eac5-182">Azure Analysis Services</span></span> | <span data-ttu-id="7eac5-183">SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7eac5-183">SQL Server Analysis Services</span></span> | <span data-ttu-id="7eac5-184">SQL Server con indici columnstore</span><span class="sxs-lookup"><span data-stu-id="7eac5-184">SQL Server with Columnstore Indexes</span></span> | <span data-ttu-id="7eac5-185">Database SQL di Azure con indici columnstore</span><span class="sxs-lookup"><span data-stu-id="7eac5-185">Azure SQL Database with Columnstore Indexes</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="7eac5-186">Server regionali ridondanti per disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="7eac5-186">Redundant regional servers for high availability</span></span>  | <span data-ttu-id="7eac5-187">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-187">Yes</span></span> | <span data-ttu-id="7eac5-188">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-188">No</span></span> | <span data-ttu-id="7eac5-189">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-189">Yes</span></span> | <span data-ttu-id="7eac5-190">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-190">Yes</span></span> |
| <span data-ttu-id="7eac5-191">Supporto per la scalabilità orizzontale delle query</span><span class="sxs-lookup"><span data-stu-id="7eac5-191">Supports query scale out</span></span>  | <span data-ttu-id="7eac5-192">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-192">Yes</span></span> | <span data-ttu-id="7eac5-193">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-193">No</span></span> | <span data-ttu-id="7eac5-194">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-194">Yes</span></span> | <span data-ttu-id="7eac5-195">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-195">No</span></span> |
| <span data-ttu-id="7eac5-196">Scalabilità dinamica (aumento delle prestazioni)</span><span class="sxs-lookup"><span data-stu-id="7eac5-196">Dynamic scalability (scale up)</span></span>  | <span data-ttu-id="7eac5-197">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-197">Yes</span></span> | <span data-ttu-id="7eac5-198">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-198">No</span></span> | <span data-ttu-id="7eac5-199">Sì</span><span class="sxs-lookup"><span data-stu-id="7eac5-199">Yes</span></span> | <span data-ttu-id="7eac5-200">No </span><span class="sxs-lookup"><span data-stu-id="7eac5-200">No</span></span> |
