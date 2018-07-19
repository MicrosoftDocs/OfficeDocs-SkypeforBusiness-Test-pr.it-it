---
title: Eseguire la migrazione della rubrica
TOCTitle: Eseguire la migrazione della rubrica
ms:assetid: ac7f0f39-4c6d-4702-8e25-93a73e3d800f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205160(v=OCS.15)
ms:contentKeyID: 49301649
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-10-09_

La migrazione della Rubrica di Lync Server 2010 in genere viene eseguita insieme alla migrazione del resto della topologia. Potrebbe tuttavia essere necessario eseguire alcuni passaggi post-migrazione qualora all'interno dell'ambiente Lync Server 2010 siano state effettuate le personalizzazioni seguenti:

  - Impostazione della proprietà WMI **PartitionbyOU** per raggruppare le voci della Rubrica per unità organizzativa.

  - Personalizzazione delle regole di normalizzazione della Rubrica.

  - Impostazione del valore predefinito del parametro **UseNormalizationRules** su False.

**Voci della Rubrica raggruppate**

Se la proprietà WMI **PartitionbyOU** è stata impostata su True per creare una Rubrica per ogni unità organizzativa e si desidera continuare a raggruppare le voci della Rubrica, è necessario impostare l'attributo di Active Directory **msRTCSIP-GroupingId** per utenti e contatti. Per limitare l'ambito delle ricerche nella Rubrica è consigliabile raggruppare le voci della Rubrica. Per utilizzare l'attributo **msRTCSIP-GroupingId** , creare uno script per popolare l'attributo, assegnando lo stesso valore per tutti gli utenti che si desidera raggruppare. Ad esempio, assegnare un unico valore a tutti gli utenti di un'unità organizzativa.

**Regole di normalizzazione della Rubrica**

Se nell'ambiente Lync Server 2010 le regole di normalizzazione della Rubrica sono state personalizzate, è necessario eseguire la migrazione di tali regole nel pool pilota. Se non è stata personalizzata alcuna regola di normalizzazione della Rubrica, non sarà necessario effettuare alcuna migrazione per il servizio Rubrica. Le regole di normalizzazione predefinite di Lync Server 2013 sono uguali alle regole predefinite di Lync Server 2010. Eseguire la procedura descritta più avanti in questa sezione per eseguire la migrazione delle regole di normalizzazione personalizzate.


> [!NOTE]
> Se nell'organizzazione viene utilizzato il controllo delle chiamate remote e le regole di normalizzazione della Rubrica sono state personalizzate, prima di utilizzare il controllo delle chiamate remote è necessario eseguire la procedura descritta in questo argomento. L'esecuzione della procedura richiede l'appartenenza al gruppo RTCUniversalServerAdmins o diritti equivalenti.



**UseNormalizationRules impostato su False**

Se si imposta su False il valore di **UseNormalizationRules** in modo che gli utenti possano utilizzare i numeri di telefono così come sono definiti in Servizi di dominio Active Directory senza che Lync Server 2013 debba applicare regole di normalizzazione, è necessario impostare i parametri **UseNormalizationRules** e **IgnoreGenericRules** su True. Eseguire la procedura descritta più avanti in questa sezione per impostare tali parametri su True.

## Per eseguire la migrazione delle regole di normalizzazione personalizzate della Rubrica

1.  Individuare il file Company\_Phone\_Number\_Normalization\_Rules.txt nella radice della cartella condivisa della Rubrica e copiarlo nella radice della cartella condivisa della Rubrica nel pool pilota Lync Server 2013.
    

    > [!NOTE]
    > Le regole di normalizzazione della Rubrica di esempio sono state installate nella directory dei file dei componenti Web del Servizio Rubrica. Il percorso è <STRONG>$installedDriveLetter:\Programmi\Microsoft Lync Server 2013\Web Components\Address Book Files\Files\ Sample_Company_Phone_Number_Normalization_Rules.txt</STRONG>. Questo file può essere copiato e rinominato come&nbsp; <STRONG>Company_Phone_Number_Normalization_Rules.txt</STRONG>&nbsp;nella directory radice della cartella condivisa della Rubrica. Ad esempio, se la Rubrica è condivisa in <STRONG>$serverX</STRONG>,&nbsp;il percorso sarà simile al seguente: <STRONG>\\$serverX \LyncFileShare\2-WebServices-1\ABFiles</STRONG>.



2.  Utilizzare un editor di testo, ad esempio il Blocco Note, per aprire il file Company\_Phone\_Number\_Normalization\_Rules.txt.

3.  Alcuni tipi di voci non funzionano correttamente in Lync Server 2013. Cercare all'interno del file i tipi di voci descritti in questo passaggio, modificarli secondo necessità e salvare le modifiche nella cartella condivisa della Rubrica all'interno del pool pilota.
    
    Le stringhe che includono spazi o caratteri di punteggiatura necessari provocano un errore nelle regole di normalizzazione poiché tali caratteri vengono rimossi dalla stringa utilizzata come input nelle regole di normalizzazione. Se sono presenti stringhe che includono spazi o caratteri di punteggiatura necessari, è necessario modificare le stringhe. La stringa seguente, ad esempio, genererà un errore nelle regola di normalizzazione:
    
        \s*\(\s*\d\d\d\s*\)\s*\-\s*\d\d\d\s*\-\s*\d\d\d\d
    
    La stringa seguente non causerebbe alcun errore della regola di normalizzazione:
    
        \s*\(?\s*\d\d\d\s*\)?\s*\-?\s*\d\d\d\s*\-?\s*\d\d\d\d

## Per impostare UseNormalizationRules e IgnoreGenericRules su True

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire una delle operazioni seguenti:
    
      - Se nella distribuzione è incluso solo Lync Server 2013, eseguire il cmdlet seguente a livello globale per impostare i valori di **UseNormalizationRules** e **IgnoreGenericRules** su True:
        
            Set-CsAddressBookConfiguration -identity <XdsIdentity> -UseNormalizationRules=$true -IgnoreGenericRules=$true
    
      - Se la distribuzione include una combinazione di Lync Server 2013 e Lync Server 2010 o Office Communications Server 2007 R2, eseguire il cmdlet indicato di seguito e assegnarlo a ogni pool Lync Server 2013 nella topologia:
        
            new-csaddressbookconfiguration -identity <XdsIdentity> -UseNormalizationRules=$true -IgnoreGenericRules=$true

3.  Attendere che la replica dell' archivio di gestione centrale venga eseguita in tutti i pool.

4.  Modificare il file delle regole di normalizzazione dei numeri di telefono, "Company\_Phone\_Number\_Normalization\_Rules.txt", per la distribuzione per cancellare il contenuto. Il file si trova nella condivisione file di ogni pool di Lync Server 2013. Se il file non è presente, creare un file vuoto denominato "Company\_Phone\_Number\_Normalization\_Rules.txt".

5.  Attendere qualche minuto che tutti i pool Front End leggano i nuovi file.

6.  Eseguire il cmdlet seguente in ogni pool di Lync Server 2013 della distribuzione:
    
        Update-CsAddressBook

