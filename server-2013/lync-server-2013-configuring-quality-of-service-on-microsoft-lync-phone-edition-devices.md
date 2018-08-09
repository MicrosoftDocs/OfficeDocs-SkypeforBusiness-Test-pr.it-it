---
title: "Lync Server 2013: Configura QoS in dispositivi Microsoft Lync Phone Edition"
TOCTitle: "Lync Server 2013: Configura QoS in dispositivi Microsoft Lync Phone Edition"
ms:assetid: a6eb2620-a512-4ab6-bdfd-eb76be43bbfe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205137(v=OCS.15)
ms:contentKeyID: 49301582
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Qualità del servizio (QoS) nei dispositivi Microsoft Lync Phone Edition

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Benché la qualità del servizio (QoS) non sia abilitata per impostazione predefinita per dispositivi come iPhone, è abilitata per impostazione predefinita per i dispositivi che eseguono Lync Phone Edition. Tali dispositivi vengono comunemente indicati come telefoni UC o per comunicazioni unificate. Per verificare questa condizione, eseguire il comando di Windows PowerShell seguente da Lync Server Management Shell:

    Get-CsUCPhoneConfiguration

Se non sono state apportate modifiche alle impostazioni di configurazione dei telefoni UC, verranno restituite informazioni simili alle seguenti:

    Identity             : Global
    CalendarPollInterval : 00:03:00
    EnforcePhoneLock     : True
    PhoneLockTimeout     : 00:10:00
    MinPhonePinLength    : 6
    SIPSecurityMode      : High
    VoiceDiffServTag     : 40
    Voice8021p           : 0
    LoggingLevel         : Off

Ai fini della qualità del servizio, è interessante solo una di queste proprietà, ovvero VoiceDiffServTag, che rappresenta il valore DSCP assegnato al traffico vocale proveniente da un dispositivo Lync Phone Edition.


> [!NOTE]
> Il parametro Voice8021p non è più supportato in Lync Server 2013. Tale parametro è ancora valido per compatibilità con Microsoft Lync Server 2010, tuttavia non ha alcun effetto sui dispositivi utilizzati con Lync Server 2013.



Nella maggior parte delle reti il fatto di contrassegnare i pacchetti di Lync Phone Edition con una proprietà VoiceDiffServTag pari a 40 non dovrebbe causare problemi. 40 non è tuttavia il valore utilizzato comunemente per il traffico audio, che invece è quasi sempre contrassegnato con il codice DSCP 46. Per mantenere la coerenza all'interno della rete, è possibile modificare la proprietà VoiceDiffServTag dei telefoni UC impostandola su 46.

A tale scopo, è possibile utilizzare Windows PowerShell o il Pannello di controllo di Lync Server. Per modificare il valore di VoiceDiffServTag mediante Windows PowerShell, eseguire il comando seguente da Lync Server Management Shell:

    Set-CsUCPhoneConfiguration -VoiceDiffServTag 46

Il comando precedente modifica la raccolta globale delle impostazioni di configurazione dei telefoni UC. Tali impostazioni possono tuttavia essere assegnate anche all'ambito del sito. Per modificare le impostazioni di configurazione dei telefoni UC nell'ambito del sito, è necessario specificare l'identità (Identity) del sito. Ad esempio:

    Set-CsUCPhoneConfiguration -Identity "site:Redmond" -VoiceDiffServTag 46

È inoltre possibile utilizzare il comando seguente per modificare contemporaneamente tutte le impostazioni di configurazione dei telefoni UC:

    Get-CsUCPhoneConfiguration | Set-CsUCPhoneConfiguration -VoiceDiffServTag 46

Se si preferisce apportare tale modifica utilizzando il Pannello di controllo di Lync Server, avviare il Pannello di controllo e quindi eseguire la procedura seguente:

1.  Fare clic su **Client** e quindi su **Configurazione dispositivo**.

2.  Nella scheda **Configurazione dispositivo** fare doppio clic sulla raccolta di impostazioni che si desidera modificare, ad esempio **Globale**.

3.  Nella finestra di dialogo **Modifica configurazione dispositivo** impostare il valore della casella **Qualità vocale servizio (QoS)** su **46** e quindi fare clic su **Commit**.

Se si dispone di più raccolte, sarà necessario ripetere questo processo per ogni raccolta di impostazioni per i telefoni UC. Il Pannello di controllo di Lync Server non consentirà di modificare più raccolte di impostazioni contemporaneamente.

Se si dispone di dispositivi non basati sul sistema operativo Windows, come nel caso di iPhone, nell'organizzazione la modifica dell'impostazione VoiceDiffServTag non inciderà su questi dispositivi. Se si desidera modificare i valori DSCP su tali dispositivi, sarà necessario fare riferimento al manuale dell'amministratore per ogni tipo di dispositivo.

