---
title: Scelta di una tecnologia di elaborazione del linguaggio naturale
description: 
author: zoinerTejada
ms:date: 02/12/2018
ms.openlocfilehash: dacf7bf9cf3e9efed212f34da93c1470954965cf
ms.sourcegitcommit: 90cf2de795e50571d597cfcb9b302e48933e7f18
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="choosing-a-natural-language-processing-technology-in-azure"></a><span data-ttu-id="d21e8-102">Scelta di una tecnologia di elaborazione del linguaggio naturale in Azure</span><span class="sxs-lookup"><span data-stu-id="d21e8-102">Choosing a natural language processing technology in Azure</span></span>

<span data-ttu-id="d21e8-103">L'elaborazione di testo in formato libero viene eseguita su documenti che contengono paragrafi di testo, in genere allo scopo di supportare la ricerca, ma viene usata anche per eseguire altre attività di elaborazione del linguaggio naturale, ad esempio analisi del sentiment, rilevamento di argomenti, rilevamento della lingua, estrazione di frasi chiave e categorizzazione di documenti.</span><span class="sxs-lookup"><span data-stu-id="d21e8-103">Free-form text processing is performed against documents containing paragraphs of text, typically for the purpose of supporting search, but is also used to perform other natural language processing (NLP) tasks such as sentiment analysis, topic detection, language detection, key phrase extraction, and document categorization.</span></span> <span data-ttu-id="d21e8-104">Questo articolo illustra le opzioni di tecnologia disponibili a supporto delle attività di elaborazione del linguaggio naturale.</span><span class="sxs-lookup"><span data-stu-id="d21e8-104">This article focuses on the technology choices that act in support of the NLP tasks.</span></span>

## <a name="what-are-your-options-when-choosing-an-nlp-service"></a><span data-ttu-id="d21e8-105">Opzioni disponibili per la scelta di un servizio di elaborazione del linguaggio naturale</span><span class="sxs-lookup"><span data-stu-id="d21e8-105">What are your options when choosing an NLP service?</span></span>

<span data-ttu-id="d21e8-106">In Azure, i servizi seguenti forniscono funzionalità di elaborazione del linguaggio naturale:</span><span class="sxs-lookup"><span data-stu-id="d21e8-106">In Azure, the following services provide natural language processing (NLP) capabilities:</span></span>

- [<span data-ttu-id="d21e8-107">Azure HDInsight con Spark e Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="d21e8-107">Azure HDInsight with Spark and Spark MLlib</span></span>](/azure/hdinsight/spark/apache-spark-overview)
- [<span data-ttu-id="d21e8-108">Servizi cognitivi Microsoft</span><span class="sxs-lookup"><span data-stu-id="d21e8-108">Microsoft Cognitive Services</span></span>](/azure/#pivot=products&panel=cognitive)

## <a name="key-selection-criteria"></a><span data-ttu-id="d21e8-109">Criteri di scelta principali</span><span class="sxs-lookup"><span data-stu-id="d21e8-109">Key selection criteria</span></span>

<span data-ttu-id="d21e8-110">Per limitare le possibilità di scelta, rispondere prima di tutto a queste domande:</span><span class="sxs-lookup"><span data-stu-id="d21e8-110">To narrow the choices, start by answering these questions:</span></span>

- <span data-ttu-id="d21e8-111">Si desidera usare modelli predefiniti?</span><span class="sxs-lookup"><span data-stu-id="d21e8-111">Do you want to use prebuilt models?</span></span> <span data-ttu-id="d21e8-112">In caso affermativo, può essere opportuno usare le API offerte da Servizi cognitivi Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d21e8-112">If yes, consider using the APIs offered by Microsoft Cognitive Services.</span></span>

- <span data-ttu-id="d21e8-113">È necessario eseguire il training di modelli personalizzati con una raccolta di grandi dimensioni di dati di testo?</span><span class="sxs-lookup"><span data-stu-id="d21e8-113">Do you need to train custom models against a large corpus of text data?</span></span> <span data-ttu-id="d21e8-114">In caso affermativo, può essere opportuno usare Azure HDInsight con Spark MLlib e Spark NLP.</span><span class="sxs-lookup"><span data-stu-id="d21e8-114">If yes, consider using Azure HDInsight with Spark MLlib and Spark NLP.</span></span>

- <span data-ttu-id="d21e8-115">Sono necessarie funzionalità di elaborazione del linguaggio naturale di base, quali tokenizzazione, stemming, lemmatizzazione e frequenza del termine/frequenza inversa del documento (TF/IDF)?</span><span class="sxs-lookup"><span data-stu-id="d21e8-115">Do you need low-level NLP capabilities like tokenization, stemming, lemmatization, and term frequency/inverse document frequency (TF/IDF)?</span></span> <span data-ttu-id="d21e8-116">In caso affermativo, può essere opportuno usare Azure HDInsight con Spark MLlib e Spark NLP.</span><span class="sxs-lookup"><span data-stu-id="d21e8-116">If yes, consider using Azure HDInsight with Spark MLlib and Spark NLP.</span></span>

- <span data-ttu-id="d21e8-117">Sono necessarie funzionalità di elaborazione del linguaggio naturale avanzate, quali identificazione di entità e finalità, rilevamento dell'argomento, controllo ortografico o analisi del sentiment?</span><span class="sxs-lookup"><span data-stu-id="d21e8-117">Do you need simple, high-level NLP capabilities like entity and intent identification, topic detection, spell check, or sentiment analysis?</span></span> <span data-ttu-id="d21e8-118">In caso affermativo, può essere opportuno usare le API offerte da Servizi cognitivi Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d21e8-118">If yes, consider using the APIs offered by Microsoft Cognitive Services.</span></span>

## <a name="capability-matrix"></a><span data-ttu-id="d21e8-119">Matrice delle funzionalità</span><span class="sxs-lookup"><span data-stu-id="d21e8-119">Capability matrix</span></span>

<span data-ttu-id="d21e8-120">Le tabelle seguenti contengono un riepilogo delle differenze principali in termini di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d21e8-120">The following tables summarize the key differences in capabilities.</span></span>  

### <a name="general-capabilities"></a><span data-ttu-id="d21e8-121">Funzionalità generali</span><span class="sxs-lookup"><span data-stu-id="d21e8-121">General capabilities</span></span>

| | <span data-ttu-id="d21e8-122">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d21e8-122">Azure HDInsight</span></span> | <span data-ttu-id="d21e8-123">Servizi cognitivi Microsoft</span><span class="sxs-lookup"><span data-stu-id="d21e8-123">Microsoft Cognitive Services</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d21e8-124">Fornisce modelli sottoposti a training come servizio</span><span class="sxs-lookup"><span data-stu-id="d21e8-124">Provides pretrained models as a service</span></span> | <span data-ttu-id="d21e8-125">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-125">No</span></span> | <span data-ttu-id="d21e8-126">Sì</span><span class="sxs-lookup"><span data-stu-id="d21e8-126">Yes</span></span> |
| <span data-ttu-id="d21e8-127">API REST</span><span class="sxs-lookup"><span data-stu-id="d21e8-127">REST API</span></span> | <span data-ttu-id="d21e8-128">Sì</span><span class="sxs-lookup"><span data-stu-id="d21e8-128">Yes</span></span> | <span data-ttu-id="d21e8-129">Sì</span><span class="sxs-lookup"><span data-stu-id="d21e8-129">Yes</span></span> |
| <span data-ttu-id="d21e8-130">Programmabilità</span><span class="sxs-lookup"><span data-stu-id="d21e8-130">Programmability</span></span> | <span data-ttu-id="d21e8-131">Python, Scala, Java</span><span class="sxs-lookup"><span data-stu-id="d21e8-131">Python, Scala, Java</span></span> | <span data-ttu-id="d21e8-132">C#, Java, Node.js, Python, PHP, Ruby</span><span class="sxs-lookup"><span data-stu-id="d21e8-132">C#, Java, Node.js, Python, PHP, Ruby</span></span> |
| <span data-ttu-id="d21e8-133">Supporta l'elaborazione di set di Big Data e documenti di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="d21e8-133">Support processing of big data sets and large documents</span></span> | <span data-ttu-id="d21e8-134">Sì</span><span class="sxs-lookup"><span data-stu-id="d21e8-134">Yes</span></span> | <span data-ttu-id="d21e8-135">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-135">No</span></span> |

### <a name="low-level-natural-language-processing-capabilities"></a><span data-ttu-id="d21e8-136">Funzionalità di elaborazione del linguaggio naturale di base</span><span class="sxs-lookup"><span data-stu-id="d21e8-136">Low-level natural language processing capabilities</span></span>

| | <span data-ttu-id="d21e8-137">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d21e8-137">Azure HDInsight</span></span> | <span data-ttu-id="d21e8-138">Servizi cognitivi Microsoft</span><span class="sxs-lookup"><span data-stu-id="d21e8-138">Microsoft Cognitive Services</span></span> |  
| --- | --- | --- | 
| <span data-ttu-id="d21e8-139">Tokenizer</span><span class="sxs-lookup"><span data-stu-id="d21e8-139">Tokenizer</span></span> | <span data-ttu-id="d21e8-140">Sì (Spark NLP)</span><span class="sxs-lookup"><span data-stu-id="d21e8-140">Yes (Spark NLP)</span></span> | <span data-ttu-id="d21e8-141">Sì (API Analisi linguistica)</span><span class="sxs-lookup"><span data-stu-id="d21e8-141">Yes (Linguistic Analysis API)</span></span> |
| <span data-ttu-id="d21e8-142">Stemmer</span><span class="sxs-lookup"><span data-stu-id="d21e8-142">Stemmer</span></span> | <span data-ttu-id="d21e8-143">Sì (Spark NLP)</span><span class="sxs-lookup"><span data-stu-id="d21e8-143">Yes (Spark NLP)</span></span> | <span data-ttu-id="d21e8-144">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-144">No</span></span> |
| <span data-ttu-id="d21e8-145">Lemmatizer</span><span class="sxs-lookup"><span data-stu-id="d21e8-145">Lemmatizer</span></span> | <span data-ttu-id="d21e8-146">Sì (Spark NLP)</span><span class="sxs-lookup"><span data-stu-id="d21e8-146">Yes (Spark NLP)</span></span> | <span data-ttu-id="d21e8-147">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-147">No</span></span> |
| <span data-ttu-id="d21e8-148">Tag delle parti del discorso</span><span class="sxs-lookup"><span data-stu-id="d21e8-148">Part of speech tagging</span></span> | <span data-ttu-id="d21e8-149">Sì (Spark NLP)</span><span class="sxs-lookup"><span data-stu-id="d21e8-149">Yes (Spark NLP)</span></span> | <span data-ttu-id="d21e8-150">Sì (API Analisi linguistica)</span><span class="sxs-lookup"><span data-stu-id="d21e8-150">Yes (Linguistic Analysis API)</span></span> |
| <span data-ttu-id="d21e8-151">Frequenza del termine/Frequenza inversa del documento (TF/IDF)</span><span class="sxs-lookup"><span data-stu-id="d21e8-151">Term frequency/inverse-document frequency (TF/IDF)</span></span> | <span data-ttu-id="d21e8-152">Sì (Spark MLlib)</span><span class="sxs-lookup"><span data-stu-id="d21e8-152">Yes (Spark MLlib)</span></span> | <span data-ttu-id="d21e8-153">No </span><span class="sxs-lookup"><span data-stu-id="d21e8-153">No</span></span> |
| <span data-ttu-id="d21e8-154">Somiglianza tra stringhe&mdash;calcolo della distanza di modifiche</span><span class="sxs-lookup"><span data-stu-id="d21e8-154">String similarity&mdash;edit distance calculation</span></span> | <span data-ttu-id="d21e8-155">Sì (Spark MLlib)</span><span class="sxs-lookup"><span data-stu-id="d21e8-155">Yes (Spark MLlib)</span></span> | <span data-ttu-id="d21e8-156">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-156">No</span></span> |
| <span data-ttu-id="d21e8-157">Calcolo di n-grammi</span><span class="sxs-lookup"><span data-stu-id="d21e8-157">N-gram calculation</span></span> | <span data-ttu-id="d21e8-158">Sì (Spark MLlib)</span><span class="sxs-lookup"><span data-stu-id="d21e8-158">Yes (Spark MLlib)</span></span> | <span data-ttu-id="d21e8-159">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-159">No</span></span> |
| <span data-ttu-id="d21e8-160">Eliminazione parole vuote</span><span class="sxs-lookup"><span data-stu-id="d21e8-160">Stop word removal</span></span> | <span data-ttu-id="d21e8-161">Sì (Spark MLlib)</span><span class="sxs-lookup"><span data-stu-id="d21e8-161">Yes (Spark MLlib)</span></span> | <span data-ttu-id="d21e8-162">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-162">No</span></span> |

### <a name="high-level-natural-language-processing-capabilities"></a><span data-ttu-id="d21e8-163">Funzionalità di elaborazione del linguaggio naturale avanzate</span><span class="sxs-lookup"><span data-stu-id="d21e8-163">High-level natural language processing capabilities</span></span>

| | <span data-ttu-id="d21e8-164">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d21e8-164">Azure HDInsight</span></span> | <span data-ttu-id="d21e8-165">Servizi cognitivi Microsoft</span><span class="sxs-lookup"><span data-stu-id="d21e8-165">Microsoft Cognitive Services</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="d21e8-166">Estrazione e identificazione di entità/finalità</span><span class="sxs-lookup"><span data-stu-id="d21e8-166">Entity/intent identification & extraction</span></span> | <span data-ttu-id="d21e8-167">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-167">No</span></span> | <span data-ttu-id="d21e8-168">Sì (API LUIS, Language Understanding Intelligent Service)</span><span class="sxs-lookup"><span data-stu-id="d21e8-168">Yes (Language Understanding Intelligent Service (LUIS) API)</span></span> |    
| <span data-ttu-id="d21e8-169">Rilevamento di argomenti</span><span class="sxs-lookup"><span data-stu-id="d21e8-169">Topic detection</span></span> | <span data-ttu-id="d21e8-170">Sì (Spark NLP)</span><span class="sxs-lookup"><span data-stu-id="d21e8-170">Yes (Spark NLP)</span></span> | <span data-ttu-id="d21e8-171">Sì (API Analisi del testo)</span><span class="sxs-lookup"><span data-stu-id="d21e8-171">Yes (Text Analytics API)</span></span> |
| <span data-ttu-id="d21e8-172">Controllo ortografico</span><span class="sxs-lookup"><span data-stu-id="d21e8-172">Spell checking</span></span> | <span data-ttu-id="d21e8-173">Sì (Spark NLP)</span><span class="sxs-lookup"><span data-stu-id="d21e8-173">Yes (Spark NLP)</span></span> | <span data-ttu-id="d21e8-174">Sì (API Controllo ortografico Bing)</span><span class="sxs-lookup"><span data-stu-id="d21e8-174">Yes (Bing Spell Check API)</span></span> |
| <span data-ttu-id="d21e8-175">Analisi del sentiment</span><span class="sxs-lookup"><span data-stu-id="d21e8-175">Sentiment analysis</span></span> | <span data-ttu-id="d21e8-176">Sì (Spark NLP)</span><span class="sxs-lookup"><span data-stu-id="d21e8-176">Yes (Spark NLP)</span></span> | <span data-ttu-id="d21e8-177">Sì (API Analisi del testo)</span><span class="sxs-lookup"><span data-stu-id="d21e8-177">Yes (Text Analytics API)</span></span> |
| <span data-ttu-id="d21e8-178">Rilevamento della lingua</span><span class="sxs-lookup"><span data-stu-id="d21e8-178">Language detection</span></span> | <span data-ttu-id="d21e8-179">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-179">No</span></span> | <span data-ttu-id="d21e8-180">Sì (API Analisi del testo)</span><span class="sxs-lookup"><span data-stu-id="d21e8-180">Yes (Text Analytics API)</span></span> |
| <span data-ttu-id="d21e8-181">Supporto di più lingue oltre all'inglese</span><span class="sxs-lookup"><span data-stu-id="d21e8-181">Supports multiple languages besides English</span></span> | <span data-ttu-id="d21e8-182">No</span><span class="sxs-lookup"><span data-stu-id="d21e8-182">No</span></span> | <span data-ttu-id="d21e8-183">Sì (varia in base all'API)</span><span class="sxs-lookup"><span data-stu-id="d21e8-183">Yes (varies by API)</span></span> |

## <a name="see-also"></a><span data-ttu-id="d21e8-184">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d21e8-184">See also</span></span>

[<span data-ttu-id="d21e8-185">Elaborazione del linguaggio naturale</span><span class="sxs-lookup"><span data-stu-id="d21e8-185">Natural language processing</span></span>](../scenarios/natural-language-processing.md)