---
title: Eseguire la migrazione della rubrica
TOCTitle: Eseguire la migrazione della rubrica
ms:assetid: b6e000ce-8b2e-460c-8a8b-000254b9d778
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205198(v=OCS.15)
ms:contentKeyID: 49301748
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-10-02_

**Per eseguire la migrazione delle regole di normalizzazione personalizzate della Rubrica**

1.  Individuare il file Company\_Phone\_Number\_Normalization\_Rules.txt nella radice della cartella condivisa della Rubrica e copiarlo nella radice della cartella condivisa della Rubrica nel pool pilota Lync Server 2013.
    

    > [!NOTE]
    > Le regole di normalizzazione della Rubrica di esempio sono state installate nella directory dei file dei componenti Web del Servizio Rubrica. Il percorso è <STRONG>$installedDriveLetter:\Programmi\Microsoft Lync Server 2013\Web Components\Address Book Files\Files\ Sample_Company_Phone_Number_Normalization_Rules.txt</STRONG>. Questo file può essere copiato e rinominato come&nbsp; <STRONG>Company_Phone_Number_Normalization_Rules.txt</STRONG>&nbsp;nella directory radice della cartella condivisa della Rubrica. Ad esempio, se la Rubrica è condivisa in <STRONG>$serverX</STRONG>,&nbsp;il percorso sarà simile al seguente: <STRONG>\\$serverX \LyncFileShare\2-WebServices-1\ABFiles</STRONG>.



2.  Utilizzare un editor di testo, ad esempio il Blocco Note, per aprire il file Company\_Phone\_Number\_Normalization\_Rules.txt.

3.  Alcuni tipi di voci non funzionano correttamente in Lync Server 2013. Cercare all'interno del file i tipi di voci descritti in questo passaggio, modificarli secondo necessità e salvare le modifiche nella cartella condivisa della Rubrica all'interno del pool pilota.
    
    Le stringhe che includono spazi o caratteri di punteggiatura necessari provocano un errore nelle regole di normalizzazione poiché tali caratteri vengono rimossi dalla stringa utilizzata come input nelle regole di normalizzazione. Se sono presenti stringhe che includono spazi o caratteri di punteggiatura necessari, è necessario modificare le stringhe. La stringa seguente, ad esempio, genererà un errore nelle regola di normalizzazione:
    
        \s*\(\s*\d\d\d\s*\)\s*\-\s*\d\d\d\s*\-\s*\d\d\d\d
    
    La stringa seguente non causerebbe alcun errore della regola di normalizzazione:
    
        \s*\(?\s*\d\d\d\s*\)?\s*\-?\s*\d\d\d\s*\-?\s*\d\d\d\d

