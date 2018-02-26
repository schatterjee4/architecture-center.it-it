---
title: Esplorazione interattiva dei dati
description: 
author: zoinerTejada
ms:date: 02/12/2018
ms.openlocfilehash: a9e72f4cf88c9082fe79f854dd79e98bfaa918f5
ms.sourcegitcommit: 90cf2de795e50571d597cfcb9b302e48933e7f18
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="interactive-data-exploration"></a><span data-ttu-id="fdbe4-102">Esplorazione interattiva dei dati</span><span class="sxs-lookup"><span data-stu-id="fdbe4-102">Interactive data exploration</span></span>

<span data-ttu-id="fdbe4-103">In molte soluzioni aziendali di business intelligence, i report e i modelli semantici vengono creati da specialisti di business intelligence e gestiti centralmente.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-103">In many corporate business intelligence (BI) solutions, reports and semantic models are created by BI specialists and managed centrally.</span></span> <span data-ttu-id="fdbe4-104">Sempre più organizzazioni, tuttavia, vogliono consentire anche agli utenti di prendere decisioni basate sui dati.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-104">Increasingly, however, organizations want to enable users to make data-driven decisions.</span></span> <span data-ttu-id="fdbe4-105">Un numero crescente di organizzazioni, inoltre, sta assumendo *data scientist* o *analisti dati*, il cui compito consiste nell'esplorare i dati in modo interattivo e applicare modelli statistici e tecniche analitiche per individuare tendenze e modelli ricorrenti nei dati.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-105">Additionally, a growing number of organizations are hiring *data scientists* or *data analysts*, whose job is to explore data interactively and apply statistical models and analytical techniques to find trends and patterns in the data.</span></span> <span data-ttu-id="fdbe4-106">L'esplorazione interattiva dei dati richiede strumenti e piattaforme che offrono funzioni di elaborazione a bassa latenza per query ad hoc e visualizzazioni di dati.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-106">Interactive data exploration requires tools and platforms that provide low-latency processing for ad-hoc queries and data visualizations.</span></span>

![](./images/data-exploration.png)

## <a name="self-service-bi"></a><span data-ttu-id="fdbe4-107">Business intelligence self-service</span><span class="sxs-lookup"><span data-stu-id="fdbe4-107">Self-service BI</span></span>

<span data-ttu-id="fdbe4-108">Il business intelligence self-service è un nome assegnato a un approccio moderno al processo decisionale in cui gli utenti hanno la possibilità di trovare, esplorare e condividere informazioni significative ottenute dai dati disponibili a livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-108">Self-service BI is a name given to a modern approach to business decision making in which users are empowered to find, explore, and share insights from data across the enterprise.</span></span> <span data-ttu-id="fdbe4-109">La soluzione dati deve quindi supportare vari requisiti:</span><span class="sxs-lookup"><span data-stu-id="fdbe4-109">To accomplish this, the data solution must support several requirements:</span></span>

* <span data-ttu-id="fdbe4-110">Individuazione delle origini dati aziendali tramite un catalogo dati.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-110">Discovery of business data sources through a data catalog.</span></span>
* <span data-ttu-id="fdbe4-111">Gestione dei dati master per garantire coerenza dei valori e delle definizioni delle entità di dati.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-111">Master data management to ensure consistency of data entity definitions and values.</span></span>
* <span data-ttu-id="fdbe4-112">Strumenti per la visualizzazione e la modellazione interattiva dei dati per utenti aziendali.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-112">Interactive data modeling and visualization tools for business users.</span></span>

<span data-ttu-id="fdbe4-113">In una soluzione di business intelligence self-service, gli utenti aziendali in genere trovano e usano origini dati inerenti alla propria area di business e usano strumenti intuitivi e applicazioni per la produttività per definire report e modelli di dati personali che possono condividere con i colleghi.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-113">In a self-service BI solution, business users typically find and consume data sources that are relevant to their particular area of the business, and use intuitive tools and productivity applications to define personal data models and reports that they can share with their colleagues.</span></span>

<span data-ttu-id="fdbe4-114">Servizi di Azure pertinenti:</span><span class="sxs-lookup"><span data-stu-id="fdbe4-114">Relevant Azure services:</span></span>

- [<span data-ttu-id="fdbe4-115">Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="fdbe4-115">Azure Data Catalog</span></span>](/azure/data-catalog/data-catalog-what-is-data-catalog)
- [<span data-ttu-id="fdbe4-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="fdbe4-116">Microsoft Power BI</span></span>](https://powerbi.microsoft.com/)

## <a name="data-science-experimentation"></a><span data-ttu-id="fdbe4-117">Esperimenti di data science</span><span class="sxs-lookup"><span data-stu-id="fdbe4-117">Data science experimentation</span></span>
<span data-ttu-id="fdbe4-118">Se un'organizzazione deve eseguire operazioni di analisi avanzata e modellazione predittiva, le attività preliminari vengono in genere effettuate da data scientist esperti.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-118">When an organization requires advanced analytics and predictive modeling, the initial preparation work is usually undertaken by specialist data scientists.</span></span> <span data-ttu-id="fdbe4-119">Un data scientist esamina i dati e applica tecniche di analisi statistica per trovare eventuali relazioni tra le *caratteristiche* dei dati e le *etichette* stimate desiderate.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-119">A data scientist explores the data and applies statistical analytical techniques to find relationships between data *features* and the desired predicted *labels*.</span></span> <span data-ttu-id="fdbe4-120">L'esplorazione dei dati viene eseguita in genere usando linguaggi di programmazione come Python o R, che supportano in modo nativo la visualizzazione e la modellazione statistica.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-120">Data exploration is typically done using programming languages such as Python or R that natively support statistical modeling and visualization.</span></span> <span data-ttu-id="fdbe4-121">Gli script usati per esplorare i dati vengono generalmente ospitati in ambienti specializzati, quali notebook di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-121">The scripts used to explore the data are typically hosted in specialized environments such as Jupyter Notebooks.</span></span> <span data-ttu-id="fdbe4-122">Questi strumenti consentono ai data scientist di esplorare i dati a livello di programmazione, nonché di documentare e condividere le informazioni approfondite che trovano.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-122">These tools enable data scientists to explore the data programmatically while documenting and sharing the insights they find.</span></span>

<span data-ttu-id="fdbe4-123">Servizi di Azure pertinenti:</span><span class="sxs-lookup"><span data-stu-id="fdbe4-123">Relevant Azure services:</span></span>

- [<span data-ttu-id="fdbe4-124">Azure Notebooks</span><span class="sxs-lookup"><span data-stu-id="fdbe4-124">Azure Notebooks</span></span>](https://notebooks.azure.com/)
- [<span data-ttu-id="fdbe4-125">Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="fdbe4-125">Azure Machine Learning Studio</span></span>](/azure/machine-learning/studio/what-is-ml-studio)
- [<span data-ttu-id="fdbe4-126">Servizi Sperimentazione di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fdbe4-126">Azure Machine Learning Experimentation Services</span></span>](/azure/machine-learning/preview/experimentation-service-configuration)
- [<span data-ttu-id="fdbe4-127">Macchina virtuale di data science</span><span class="sxs-lookup"><span data-stu-id="fdbe4-127">The Data Science Virtual Machine</span></span>](/azure/machine-learning/data-science-virtual-machine/overview)

## <a name="challenges"></a><span data-ttu-id="fdbe4-128">Problematiche</span><span class="sxs-lookup"><span data-stu-id="fdbe4-128">Challenges</span></span>

- <span data-ttu-id="fdbe4-129">**Conformità sulla privacy dei dati.**</span><span class="sxs-lookup"><span data-stu-id="fdbe4-129">**Data privacy compliance.**</span></span> <span data-ttu-id="fdbe4-130">È necessario prestare attenzione quando si mettono a disposizione degli utenti dati personali per attività di analisi e report self-service.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-130">You need to be careful about making personal data available to users for self-service analysis and reporting.</span></span> <span data-ttu-id="fdbe4-131">È probabile che sia necessario attenersi a considerazioni sulla conformità, dettate da criteri organizzativi e problemi normativi.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-131">There are likely to be compliance considerations, due to organizational policies and also regulatory issues.</span></span> 

- <span data-ttu-id="fdbe4-132">**Volume dei dati.**</span><span class="sxs-lookup"><span data-stu-id="fdbe4-132">**Data volume.**</span></span> <span data-ttu-id="fdbe4-133">Se da un lato può essere utile offrire agli utenti l'accesso all'origine dati completa, dall'altro questa scelta può determinare operazioni di Excel o Power BI molto lunghe o query Spark SQL che richiedono numerose risorse cluster.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-133">While it may be useful to give users access to the full data source, it can result in very long-running Excel or Power BI operations, or Spark SQL queries that use a lot of cluster resources.</span></span>

- <span data-ttu-id="fdbe4-134">**Conoscenza degli utenti.**</span><span class="sxs-lookup"><span data-stu-id="fdbe4-134">**User knowledge.**</span></span> <span data-ttu-id="fdbe4-135">Gli utenti creano query e aggregazioni personali per acquisire informazioni sulle decisioni aziendali.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-135">Users create their own queries and aggregations in order to inform business decisions.</span></span> <span data-ttu-id="fdbe4-136">Si è certi che gli utenti dispongano delle capacità di analisi e creazione di query necessarie per ottenere risultati accurati?</span><span class="sxs-lookup"><span data-stu-id="fdbe4-136">Are you confident that users have the necessary analytical and querying skills to get accurate results?</span></span>

- <span data-ttu-id="fdbe4-137">**Condivisione dei risultati.**</span><span class="sxs-lookup"><span data-stu-id="fdbe4-137">**Sharing results.**</span></span> <span data-ttu-id="fdbe4-138">Se gli utenti possono creare e condividere report o visualizzazioni di dati, è possibile che sia necessario tenere conto di considerazioni sulla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-138">There may be security considerations if users can create and share reports or data visualizations.</span></span>

## <a name="architecture"></a><span data-ttu-id="fdbe4-139">Architettura</span><span class="sxs-lookup"><span data-stu-id="fdbe4-139">Architecture</span></span>

<span data-ttu-id="fdbe4-140">Anche se l'obiettivo di questo scenario è supportare l'analisi interattiva dei dati e le attività di pulizia, campionamento e strutturazione dei dati inerenti al data science, sono spesso necessari processi a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-140">Although the goal of this scenario is to support interactive data analysis, the data cleansing, sampling, and structuring tasks involved in data science often include long-running processes.</span></span> <span data-ttu-id="fdbe4-141">Ecco perché, in questo caso, è necessaria un'architettura di [elaborazione in batch](./batch-processing.md).</span><span class="sxs-lookup"><span data-stu-id="fdbe4-141">That makes a [batch processing](./batch-processing.md) architecture appropriate.</span></span>

## <a name="technology-choices"></a><span data-ttu-id="fdbe4-142">Scelte di tecnologia</span><span class="sxs-lookup"><span data-stu-id="fdbe4-142">Technology choices</span></span>

<span data-ttu-id="fdbe4-143">Per l'esplorazione interattiva dei dati sono consigliate le tecnologie seguenti.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-143">The following technologies are recommended choices for interactive data exploration in Azure.</span></span>

### <a name="data-storage"></a><span data-ttu-id="fdbe4-144">Archiviazione dei dati</span><span class="sxs-lookup"><span data-stu-id="fdbe4-144">Data storage</span></span>

- <span data-ttu-id="fdbe4-145">**Contenitori BLOB dell'Archiviazione di Azure** o **Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-145">**Azure Storage Blob Containers** or **Azure Data Lake Store**.</span></span> <span data-ttu-id="fdbe4-146">I data scientist usano in genere dati di origine non elaborati per poter accedere a tutti i possibili outlier, caratteristiche ed errori nei dati.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-146">Data scientists generally work with raw source data, to ensure they have access to all possible features, outliers, and errors in the data.</span></span> <span data-ttu-id="fdbe4-147">In uno scenario di Big Data, questi dati sono disponibili in genere come file in un archivio dati.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-147">In a big data scenario, this data usually takes the form of files in a data store.</span></span>

<span data-ttu-id="fdbe4-148">Per altre informazioni, vedere [Archiviazione dei dati](../technology-choices/data-storage.md).</span><span class="sxs-lookup"><span data-stu-id="fdbe4-148">For more information, see [Data storage](../technology-choices/data-storage.md).</span></span>

### <a name="batch-processing"></a><span data-ttu-id="fdbe4-149">Elaborazione batch</span><span class="sxs-lookup"><span data-stu-id="fdbe4-149">Batch processing</span></span>

- <span data-ttu-id="fdbe4-150">**R Server** o **Spark**.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-150">**R Server** or **Spark**.</span></span> <span data-ttu-id="fdbe4-151">La maggior parte dei data scientist usa linguaggi di programmazione con un solido supporto per pacchetti matematici e statistici, ad esempio R o Python.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-151">Most data scientists use programming languages with strong support for mathematical and statistical packages, such as R or Python.</span></span> <span data-ttu-id="fdbe4-152">Quando si usano grandi volumi di dati, è possibile ridurre la latenza usufruendo di piattaforme che abilitano questi linguaggi per l'utilizzo dell'elaborazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-152">When working with large volumes of data, you can reduce latency by using platforms that enable these languages to use distributed processing.</span></span> <span data-ttu-id="fdbe4-153">R Server può essere usato in modo autonomo o in combinazione con Spark per ampliare le funzioni di elaborazione di R e Spark supporta in modo nativo Python per applicare simili funzionalità di ampliamento nel rispettivo linguaggio.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-153">R Server can be used on its own or in conjunction with Spark to scale out R processing functions, and Spark natively supports Python for similar scale-out capabilities in that language.</span></span>
- <span data-ttu-id="fdbe4-154">**Hive**.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-154">**Hive**.</span></span> <span data-ttu-id="fdbe4-155">Hive è un'ottima soluzione per la trasformazione di dati tramite semantica di tipo SQL.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-155">Hive is a good choice for transforming data using SQL-like semantics.</span></span> <span data-ttu-id="fdbe4-156">Gli utenti possono creare e caricare tabelle usando istruzioni HiveQL, semanticamente simili a SQL.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-156">Users can create and load tables using HiveQL statements, which are semantically similar to SQL.</span></span>

<span data-ttu-id="fdbe4-157">Per altre informazioni, vedere [Elaborazione batch](../technology-choices/batch-processing.md).</span><span class="sxs-lookup"><span data-stu-id="fdbe4-157">For more information, see [Batch processing](../technology-choices/batch-processing.md).</span></span>

### <a name="analytical-data-store"></a><span data-ttu-id="fdbe4-158">Archivio dati analitici</span><span class="sxs-lookup"><span data-stu-id="fdbe4-158">Analytical Data Store</span></span>

- <span data-ttu-id="fdbe4-159">**Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-159">**Spark SQL**.</span></span> <span data-ttu-id="fdbe4-160">Spark SQL è un'API basata su Spark che supporta la creazione di dataframe e tabelle su cui è possibile eseguire query usando la sintassi SQL.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-160">Spark SQL is an API built on Spark that supports the creation of dataframes and tables that can be queried using SQL syntax.</span></span> <span data-ttu-id="fdbe4-161">Indipendentemente dal fatto che i file di dati da analizzare siano file di origine non elaborati o nuovi file puliti e preparati tramite un processo batch, gli utenti possono definire su di essi tabelle Spark SQL per l'esecuzione di attività di analisi aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-161">Regardless of whether the data files to be analyzed are raw source files or new files that have been cleaned and prepared by a batch process, users can define Spark SQL tables on them for further querying an analysis.</span></span> 
- <span data-ttu-id="fdbe4-162">**Hive**.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-162">**Hive**.</span></span> <span data-ttu-id="fdbe4-163">Oltre a eseguire l'elaborazione in batch di dati non elaborati tramite Hive, è possibile creare un database Hive contenente visualizzazioni e tabelle Hive basate sulle cartelle in cui sono archiviati i dati, abilitando query interattive per attività di analisi e di creazione di report.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-163">In addition to batch processing raw data by using Hive, you can create a Hive database that contains Hive tables and views based on the folders where the data is stored, enabling interactive queries for analysis and reporting.</span></span> <span data-ttu-id="fdbe4-164">HDInsight include un tipo di cluster Interactive Hive che usa la memorizzazione nella cache per ridurre i tempi di risposta di query Hive.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-164">HDInsight includes an Interactive Hive cluster type that uses in-memory caching to reduce Hive query response times.</span></span> <span data-ttu-id="fdbe4-165">Gli utenti che hanno familiarità con la sintassi di tipo SQL possono quindi usare Interactive Hive per esplorare i dati.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-165">Users who are comfortable with SQL-like syntax can use Interactive Hive to explore data.</span></span>

<span data-ttu-id="fdbe4-166">Per altre informazioni, vedere [Analytical data stores](../technology-choices/analytical-data-stores.md) (Archivi dati analitici).</span><span class="sxs-lookup"><span data-stu-id="fdbe4-166">For more information, see [Analytical data stores](../technology-choices/analytical-data-stores.md).</span></span>

### <a name="analytics-and-reporting"></a><span data-ttu-id="fdbe4-167">Analisi e report</span><span class="sxs-lookup"><span data-stu-id="fdbe4-167">Analytics and reporting</span></span>

- <span data-ttu-id="fdbe4-168">**Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-168">**Jupyter**.</span></span> <span data-ttu-id="fdbe4-169">I notebook di Jupyter offrono un'interfaccia basata su browser per l'esecuzione di codice nei linguaggi R, Python e Scala.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-169">Jupyter Notebooks provides a browser-based interface for running code in languages such as R, Python, or Scala.</span></span> <span data-ttu-id="fdbe4-170">Se si usa R Server o Spark per l'elaborazione in batch dei dati o se si usa SQL Spark per definire uno schema delle tabelle per l'esecuzione di query, Jupyter può essere una scelta ottimale per l'esecuzione di query nei dati.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-170">When using R Server or Spark to batch process data, or when using Spark SQL to define a schema of tables for querying, Jupyter can be a good choice for querying the data.</span></span> <span data-ttu-id="fdbe4-171">Se invece si usa Spark, è possibile usare l'API del dataframe Spark standard, l'API di Spark SQL o istruzioni SQL incorporate per eseguire query sui dati e generare visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-171">When using Spark, you can use the standard Spark dataframe API or the Spark SQL API as well as embedded SQL statements to query the data and produce visualizations.</span></span>
- <span data-ttu-id="fdbe4-172">**Client Interactive Hive**.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-172">**Interactive Hive Clients**.</span></span> <span data-ttu-id="fdbe4-173">Se si usa un cluster Interactive Hive per eseguire query sui dati, è possibile usare la visualizzazione Hive nel dashboard del cluster Ambari, lo strumento da riga di comando Beeline o qualsiasi strumento basato su ODBC (tramite Hive ODBC Driver), ad esempio Microsoft Excel o Power BI.</span><span class="sxs-lookup"><span data-stu-id="fdbe4-173">If you use an Interactive Hive cluster to query the data, you can use the Hive view in the Ambari cluster dashboard, the Beeline command line tool, or any ODBC-based tool (using the Hive ODBC driver), such as Microsoft Excel or Power BI.</span></span>

<span data-ttu-id="fdbe4-174">Per altre informazioni, vedere [Data analytics and reporting technology](../technology-choices/analysis-visualizations-reporting.md) (Tecnologia per l'analisi dei dati e la creazione di report).</span><span class="sxs-lookup"><span data-stu-id="fdbe4-174">For more information, see [Data analytics and reporting technology](../technology-choices/analysis-visualizations-reporting.md).</span></span>