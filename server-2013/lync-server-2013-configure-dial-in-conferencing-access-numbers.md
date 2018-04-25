---
title: 'Lync Server 2013: Configurare i numeri di accesso per le conferenze telefoniche con accesso esterno'
TOCTitle: Configurare i numeri di accesso per le conferenze telefoniche con accesso esterno
ms:assetid: d8a18030-f318-43dd-834d-70e5014b5e8a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398952(v=OCS.15)
ms:contentKeyID: 49302156
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i numeri di accesso per le conferenze telefoniche con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2011-07-17_

Quando si distribuisce la funzionalità di conferenza telefonica con accesso esterno, è necessario configurare i numeri di telefono che gli utenti possono comporre dalla rete PSTN (Public Switched Telephone Network) per partecipare alla parte audio delle conferenze. Questi numeri di accesso esterno vengono visualizzati negli inviti alle riunioni e nella pagina Web Impostazioni conferenza telefonica con accesso esterno.

Prima di creare numeri di accesso esterno, è necessario pianificare le aree geografiche e quindi configurare i relativi dial plan. Per informazioni dettagliate sulle aree, vedere [Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-dial-in-conferencing-requirements.md) nella documentazione relativa alla pianificazione. Per informazioni dettagliate sulla configurazione di dial plan per le conferenze telefoniche con accesso esterno, vedere [Configurare dial plan per le conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-configure-dial-plans-for-dial-in-conferencing.md).


> [!NOTE]
> Non è possibile utilizzare un nuovo numero di accesso esterno fino a quando non viene completata la replica dei servizi di dominio Active Directory (AD DS) per tale numero. Il completamento della replica può richiedere diverse ore.




> [!NOTE]
> Dopo aver creato i numeri di accesso esterno, è possibile modificare il nome visualizzato per gli oggetti contatto di Active Directory, in modo che gli utenti possano identificare più facilmente il numero corretto. Utilizzare il cmdlet <STRONG>Set-CsDialInConferencingAccessNumber</STRONG> per modificare il nome visualizzato. Si sconsiglia di modificare manualmente gli oggetti Active Directory. Per informazioni dettagliate sulla modifica dei numeri di accesso, vedere la documentazione di Lync Server Management Shell relativa al cmdlet <STRONG>Set-CsDialInConferencingAccessNumber</STRONG>.



## Argomenti della sezione

[Creare o modificare un numero di accesso per una conferenza telefonica con accesso esterno in Lync Server 2013](lync-server-2013-create-or-modify-a-dial-in-conferencing-access-number.md)

## Vedere anche

#### Concetti

[Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-dial-in-conferencing-requirements.md)  

#### Ulteriori risorse

[Configurare dial plan per le conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-configure-dial-plans-for-dial-in-conferencing.md)

