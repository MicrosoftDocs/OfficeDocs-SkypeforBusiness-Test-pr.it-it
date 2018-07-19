---
title: 'Lync Server 2013: Protezione di IIS'
TOCTitle: Protezione di IIS in Lync Server 2013
ms:assetid: a67171a6-6703-4e09-abb3-35d335bb674e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn518332(v=OCS.15)
ms:contentKeyID: 60490917
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Protezione di IIS in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-12-05_

In Microsoft Office Communications Server 2007 e Microsoft Office Communications Server 2007 R2, Internet Information Services (IIS) viene eseguito con un account utente standard. Ciò può causare problemi: se la password scade è possibile che si perdano i servizi Web, un problema spesso difficile da diagnosticare. Per evitare il problema della scadenza delle password, Microsoft Lync Server 2013 consente di creare un account computer (per un computer che in effetti non esiste) da usare come entità di sicurezza dell'autenticazione per tutti i computer in un sito che eseguono IIS. Dato che questi account usano il protocollo di autenticazione Kerberos, vengono denominati account Kerberos e il nuovo processo di autenticazione è noto come autenticazione Web Kerberos. In questo modo è possibile gestire tutti i server IIS con un singolo account.

Per eseguire i server con questa entità di sicurezza dell'autenticazione, è prima di tutto necessario creare un account computer con il cmdlet New-CsKerberosAccount. Questo account viene quindi assegnato a uno o più siti. Dopo l'assegnazione, l'associazione tra l'account e il sito di Lync Server 2013 viene abilitata con l'esecuzione del cmdlet Enable-CsTopology. Tra l'altro, questo cmdlet crea il nome dell'entità servizio (SPN, Service Principal Name) obbligatorio in Servizi di dominio Active Directory. I nomi SPN offrono alle applicazioni client un mezzo per individuare un particolare servizio. Per informazioni dettagliate, vedere [New-CsKerberosAccount](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsKerberosAccount) nella documentazione relativa alle operazioni.

## Procedure consigliate

Per potenziare la sicurezza di IIS, consigliamo di implementare un account Kerberos per IIS. Se non si implementa un account Kerberos, IIS viene eseguito con un account utente standard.

