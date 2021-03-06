---
title: Problembehandlung für SQL Server-Datenbanksicherungen
description: Informationen zur Problembehandlung beim Sichern von SQL Server-Datenbanken auf virtuellen Azure-Computern mit Azure Backup
ms.topic: troubleshooting
ms.date: 06/18/2019
ms.openlocfilehash: 7ebe76fde344b1dabca9a3aee2d0cc9e1edb8df4
ms.sourcegitcommit: 509b39e73b5cbf670c8d231b4af1e6cfafa82e5a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78392806"
---
# <a name="troubleshoot-sql-server-database-backup-by-using-azure-backup"></a>Problembehandlung für die SQL Server-Datenbanksicherung mit Azure Backup

Dieser Artikel enthält Informationen zur Problembehandlung bei SQL Server-Datenbank-Instanzen, die auf Azure-VMs ausgeführt werden.

Weitere Informationen zu Sicherungsprozess und Einschränkungen finden Sie unter [Funktionsaspekte und Einschränkungen](backup-azure-sql-database.md#feature-consideration-and-limitations).

## <a name="sql-server-permissions"></a>SQL Server-Berechtigungen

Zum Konfigurieren des Schutzes für eine SQL Server-Datenbank auf einem virtuellen Computer, müssen Sie auf diesem virtuellen Computer die Erweiterung **AzureBackupWindowsWorkload** installieren. Wenn Sie die Fehlermeldung **UserErrorSQLNoSysadminMembership** erhalten, bedeutet das, dass Ihre SQL Server-Instanz nicht über die erforderlichen Berechtigungen für die Sicherung verfügt. Um diesen Fehler zu beheben, führen Sie die Schritte in [Einrichten von Berechtigungen für virtuelle Computer](backup-azure-sql-database.md#set-vm-permissions) aus.

## <a name="troubleshoot-discover-and-configure-issues"></a>Behandlung von Problemen beim Ermitteln und Konfigurieren

Der Prozess des Ermittelns von Datenbanken und Konfigurierens einer Sicherung besteht nach dem Erstellen und Konfigurieren des Recovery Services-Tresors aus zwei Schritten.<br>

![sql](./media/backup-azure-sql-database/sql.png)

Wenn die SQL-VM und ihre Instanzen während der Sicherungskonfiguration unter **DBs in VMs ermitteln** und **Sicherung konfigurieren** (siehe Bild oben) nicht sichtbar sind, stellen Sie Folgendes sicher:

### <a name="step-1-discovery-dbs-in-vms"></a>Schritt 1: Ermitteln der DBs in VMs

- Folgen Sie den Schritten unter [Ermitteln der Sicherung des SQL-Servers](https://docs.microsoft.com/azure/backup/backup-sql-server-database-azure-vms#discover-sql-server-databases), wenn die VM nicht in der Liste der ermittelten VMs aufgeführt und auch nicht für die SQL-Sicherung in einem anderen Tresor registriert ist.

### <a name="step-2-configure-backup"></a>Schritt 2: Konfiguration der Sicherung

- Folgen Sie den Schritten unter [Konfiguration der Sicherung](https://docs.microsoft.com/azure/backup/backup-sql-server-database-azure-vms#configure-backup), wenn der Tresor, in dem die SQL-VM registriert ist, dem Tresor entspricht, in dem Datenbanken geschützt werden.

Die SQL-VM muss zunächst aus dem alten Tresor abgemeldet werden, bevor sie im neuen Tresor registriert werden kann.  Für die Abmeldung der SQL-VM aus dem Tresor müssen Sie den Schutz aller Datenquellen beenden. Erst danach können Sie die gesicherten Daten löschen. Das Löschen der gesicherten Daten kann nicht rückgängig gemacht werden.  Registrieren Sie die VM in einem neuen Tresor, und versuchen Sie die Sicherung noch einmal, nachdem Sie alles überprüft und alle Vorsichtsmaßnahmen zum Abmelden der SQL-VM getroffen haben.

## <a name="troubleshoot-backup-and-recovery-issues"></a>Beheben von Problemen bei der Sicherung und Wiederherstellung  

Gelegentlich können bei Sicherungs- und Wiederherstellungsvorgängen zufällige Ausfälle auftreten, da diese Vorgänge möglicherweise hängen bleiben. Der Grund hierfür kann ein Antivirenprogramm auf Ihrer VM sein. Als bewährte Vorgehensweise werden die folgenden Schritte empfohlen:

1. Schließen Sie die folgenden Ordner von der Antivirenüberprüfung aus:

    `C:\Program Files\Azure Workload Backup` `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.RecoveryServices.WorkloadBackup.Edp.AzureBackupWindowsWorkload`

    Ersetzen Sie `C:\` durch den Buchstaben Ihres *Systemlaufwerks*.

1. Schließen Sie die folgenden drei Prozesse, die innerhalb einer VM ausgeführt werden, von der Antivirenüberprüfung aus:

    - IaasWLPluginSvc.exe
    - IaasWorkloadCoordinaorService.exe
    - TriggerExtensionJob.exe

1. SQL bietet ebenfalls einige Richtlinien für die Arbeit mit Antivirussoftware. Nähere Einzelheiten finden Sie in [diesem Artikel](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server).

## <a name="error-messages"></a>Fehlermeldungen

### <a name="backup-type-unsupported"></a>Nicht unterstützter Sicherungstyp

| severity | BESCHREIBUNG | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|---|
| Warnung | Die aktuellen Einstellungen für diese Datenbank unterstützen bestimmte Sicherungstypen nicht, die in der zugehörigen Richtlinie enthalten sind. | <li>Für die Masterdatenbank kann nur eine vollständige Datenbanksicherung ausgeführt werden. Weder die differenzielle Sicherung noch die Sicherung des Transaktionsprotokolls ist möglich. </li> <li>Datenbanken im einfachen Wiederherstellungsmodell erlauben die Sicherung von Transaktionsprotokollen nicht.</li> | Ändern Sie die Datenbankeinstellungen so, dass alle Sicherungstypen in der Richtlinie unterstützt werden. Sie können die aktuelle Richtlinie auch so ändern, dass nur die unterstützten Sicherungstypen berücksichtigt werden. Andernfalls werden die nicht unterstützten Sicherungstypen bei der geplanten Sicherung übersprungen oder der Sicherungsauftrag schlägt bei einer bedarfsgesteuerten Sicherung fehl.

### <a name="usererrorsqlpodoesnotsupportbackuptype"></a>UserErrorSQLPODoesNotSupportBackupType

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Diese SQL-Datenbank unterstützt nicht den angeforderten Sicherungstyp. | Tritt auf, wenn das Wiederherstellungsmodell der Datenbank den angeforderten Sicherungstyp nicht zulässt. Der Fehler kann in den folgenden Situationen auftreten: <br/><ul><li>Eine Datenbank, die ein einfaches Wiederherstellungsmodell verwendet, lässt keine Protokollsicherung zu.</li><li>Differenzielle und Protokollsicherungen sind für eine Masterdatenbank nicht zulässig.</li></ul>Weitere Einzelheiten finden Sie in der Dokumentation [Wiederherstellungsmodelle (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server). | Wenn bei der Protokollsicherung für die Datenbank im einfachen Wiederherstellungsmodell ein Fehler auftritt, probieren Sie eine der folgenden Optionen aus:<ul><li>Wenn sich die Datenbank im einfachen Wiederherstellungsmodus befindet, deaktivieren Sie die Protokollsicherungen.</li><li>Verwenden Sie [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server), um das Wiederherstellungsmodell für die Datenbank in „Vollständig“ oder „Massenprotokolliert“ zu ändern. </li><li> Wenn Sie das Wiederherstellungsmodell nicht ändern möchten und bei der Sicherung mehrerer Datenbanken mit einer Standardrichtlinie arbeiten, die nicht geändert werden kann, ignorieren Sie den Fehler. Die vollständigen und differenziellen Sicherungen werden gemäß Zeitplan ausgeführt. Die Protokollsicherungen werden übersprungen, was in diesem Fall erwartet wird.</li></ul>Wenn es sich jedoch um eine Masterdatenbank handelt, und Sie differenzielle Sicherungen oder Protokollsicherungen konfiguriert haben, verwenden Sie einen der folgenden Schritte:<ul><li>Verwenden Sie das Portal, um den Sicherungsrichtlinienzeitplan für die Masterdatenbank in „Vollständig“ zu ändern.</li><li>Wenn Sie bei der Sicherung mehrerer Datenbanken mit einer Standardrichtlinie arbeiten, die nicht geändert werden kann, ignorieren Sie den Fehler. Die vollständige Sicherung wird gemäß Zeitplan ausgeführt. Differenzielle Sicherungen oder Protokollsicherungen werden nicht ausgeführt, was in diesem Fall erwartet wird.</li></ul> |
| Der Vorgang wurde abgebrochen, da auf der gleichen Datenbank bereits ein widersprüchlicher Vorgang ausgeführt wurde. | Weitere Informationen finden Sie im [Blogeintrag zum Sichern und Wiederherstellen von Einschränkungen](https://deep.data.blog/2008/12/30/concurrency-of-full-differential-and-log-backups-on-the-same-database/), die gleichzeitig ausgeführt werden.| [Verwenden Sie SQL Server Management Studio (SSMS) zum Überwachen von Sicherungsaufträgen](manage-monitor-sql-database-backup.md). Nachdem bei dem widersprüchlichen Vorgang ein Fehler aufgetreten ist, wiederholen Sie den Vorgang.|

### <a name="usererrorsqlpodoesnotexist"></a>UserErrorSQLPODoesNotExist

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Die SQL-Datenbank ist nicht vorhanden. | Die Datenbank wurde entweder gelöscht oder umbenannt. | Überprüfen Sie, ob die Datenbank versehentlich gelöscht oder umbenannt wurde.<br/><br/> Wenn die Datenbank versehentlich gelöscht wurde, stellen Sie sie am ursprünglichen Speicherort wieder her, um weiter Sicherungen anzulegen.<br/><br/> Wenn Sie die Datenbank gelöscht haben und zukünftig keine weiteren Sicherungen benötigen, wählen Sie im Recovery Services-Tresor **Sicherung beenden** mit **Sicherungsdaten beibehalten** oder **Sicherungsdaten löschen** aus. Weitere Informationen finden Sie unter [Verwalten und Überwachen gesicherter SQL Server-Datenbanken](manage-monitor-sql-database-backup.md).

### <a name="usererrorsqllsnvalidationfailure"></a>UserErrorSQLLSNValidationFailure

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Protokollkette ist unterbrochen. | Die Datenbank oder der virtuelle Computer wird mit einer anderen Sicherungslösung gesichert, die die Protokollkette abschneidet.|<ul><li>Überprüfen Sie, ob eine andere Sicherungslösung oder ein anderes Skript verwendet wird. Wenn dies der Fall ist, beenden Sie die anderen Sicherungslösung. </li><li>Wenn die Sicherung eine bedarfsgesteuerte Protokollsicherung war, sollten Sie eine vollständige Sicherung auslösen, um eine neue Protokollkette zu starten. Für geplante Protokollsicherungen ist keine Aktion erforderlich, da der Azure Backup-Dienst zur Behebung des Problems automatisch eine vollständige Sicherung auslöst.</li>|

### <a name="usererroropeningsqlconnection"></a>UserErrorOpeningSQLConnection

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Azure Backup kann keine Verbindung mit der SQL-Instanz herstellen. | Azure Backup kann keine Verbindung mit der SQL Server-Instanz herstellen. | Verwenden Sie im Azure-Portal im Fehlermenü die Option „Zusätzliche Details“, um die Grundursache einzugrenzen. Lesen Sie [Problembehandlung bei SQL-Sicherung](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine), um den Fehler zu beheben.<br/><ul><li>Wenn die SQL-Standardeinstellungen Remoteverbindungen nicht zulassen, ändern Sie die Einstellungen. Informationen zum Ändern der Einstellungen finden Sie in den folgenden Artikeln:<ul><li>[MSSQLSERVER_-1](https://docs.microsoft.com/sql/relational-databases/errors-events/mssqlserver-1-database-engine-error?view=sql-server-ver15)</li><li>[MSSQLSERVER_2](/sql/relational-databases/errors-events/mssqlserver-2-database-engine-error)</li><li>[MSSQLSERVER_53](/sql/relational-databases/errors-events/mssqlserver-53-database-engine-error)</li></ul></li></ul><ul><li>Wenn bei der Anmeldung Probleme auftreten, verwenden Sie diese Links zur Problembehebung:<ul><li>[MSSQLSERVER_18456](/sql/relational-databases/errors-events/mssqlserver-18456-database-engine-error)</li><li>[MSSQLSERVER_18452](/sql/relational-databases/errors-events/mssqlserver-18452-database-engine-error)</li></ul></li></ul> |

### <a name="usererrorparentfullbackupmissing"></a>UserErrorParentFullBackupMissing

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Die erste vollständige Sicherung für diese Datenquelle ist nicht vorhanden. | Vollständige Sicherung für die Datenbank ist nicht vorhanden. Protokollsicherungen und differenzielle Sicherungen sind einer vollständigen Sicherung übergeordnet. Daher müssen erst vollständige Sicherungen erstellt werden, bevor differenzielle Sicherungen oder Protokollsicherungen ausgelöst werden. | Auslösen einer bedarfsgesteuerten vollständigen Sicherung.   |

### <a name="usererrorbackupfailedastransactionlogisfull"></a>UserErrorBackupFailedAsTransactionLogIsFull

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Sicherung nicht möglich, da das Transaktionsprotokoll für die Datenquelle voll ist. | Das Transaktionsprotokoll der Datenbank ist voll. | Um dieses Problem zu beheben, lesen Sie die [SQL Server-Dokumentation](https://docs.microsoft.com/sql/relational-databases/errors-events/mssqlserver-9002-database-engine-error). |

### <a name="usererrorcannotrestoreexistingdbwithoutforceoverwrite"></a>UserErrorCannotRestoreExistingDBWithoutForceOverwrite

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Eine Datenbank mit demselben Namen ist am Zielspeicherort bereits vorhanden. | Im Ziel für die Wiederherstellung ist bereits eine Datenbank mit demselben Namen vorhanden.  | <ul><li>Ändern Sie den Zieldatenbanknamen.</li><li>Verwenden Sie alternativ die Option „Überschreiben erzwingen“ auf der Seite „Wiederherstellung“.</li> |

### <a name="usererrorrestorefaileddatabasecannotbeofflined"></a>UserErrorRestoreFailedDatabaseCannotBeOfflined

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Fehler bei der Wiederherstellung, wie die Datenbank konnte nicht offline geschaltet werden konnte. | Während einer Wiederherstellung muss die Zieldatenbank offline geschaltet werden. Azure Backup kann diese Daten nicht offline schalten. | Verwenden Sie im Azure-Portal im Fehlermenü die Option „Zusätzliche Details“, um die Grundursache einzugrenzen. Weitere Informationen finden Sie in der [SQL Server-Dokumentation](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). |

### <a name="usererrorcannotfindservercertificatewiththumbprint"></a>UserErrorCannotFindServerCertificateWithThumbprint

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Serverzertifikat mit dem Fingerabdruck kann im Ziel nicht gefunden werden. | Die Masterdatenbank auf der Zielinstanz verfügt nicht über einen gültigen Verschlüsselungsfingerabdruck. | Importieren Sie den in der Quellinstanz verwendeten gültigen Zertifikatfingerabdruck in die Zielinstanz. |

### <a name="usererrorrestorenotpossiblebecauselogbackupcontainsbulkloggedchanges"></a>UserErrorRestoreNotPossibleBecauseLogBackupContainsBulkLoggedChanges

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Die für die Wiederherstellung verwendete Protokollsicherung enthält massenprotokollierte Änderungen. Sie kann gemäß SQL-Richtlinien nicht verwendet werden, um an einem beliebigen Punkt anzuhalten. | Wenn sich eine Datenbank im massenprotokollierten Wiederherstellungsmodus befindet, können die Daten zwischen einer massenprotokollierten Transaktion und der nächsten protokollierten Transaktion nicht wiederhergestellt werden. | Wählen Sie einen anderen Zeitpunkt für die Wiederherstellung aus. [Weitere Informationen](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server?view=sql-server-ver15)

### <a name="fabricsvcbackuppreferencecheckfailedusererror"></a>FabricSvcBackupPreferenceCheckFailedUserError

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Sicherungsvoreinstellungen für die SQL Always On-Verfügbarkeitsgruppe kann nicht erfüllt werden, da einige Knoten der Verfügbarkeitsgruppe nicht registriert sind. | Knoten, die zum Durchführen der Sicherungen erforderlich sind, sind nicht registriert oder nicht erreichbar. | <ul><li>Stellen Sie sicher, dass alle Knoten, die zum Durchführen der Sicherungen dieser Datenbank erforderlich sind, registriert und fehlerfrei sind, und wiederholen Sie dann den Vorgang.</li><li>Ändern Sie die Sicherungseinstellung für die SQL Server Always On-Verfügbarkeitsgruppe.</li></ul> |

### <a name="vmnotinrunningstateusererror"></a>VMNotInRunningStateUserError

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Der virtuelle SQL Server-Computer ist herunterfahren und für Azure Backup-Dienst nicht verfügbar. | Der virtuelle Computer wird heruntergefahren. | Stellen Sie sicher, dass die SQL Server-Instanz ausgeführt wird. |

### <a name="guestagentstatusunavailableusererror"></a>GuestAgentStatusUnavailableUserError

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Der Azure Backup-Dienst verwendet den Azure VM-Gast-Agent für die Sicherung, der Gast-Agent ist auf dem Zielserver jedoch nicht verfügbar. | Der Gast-Agent ist nicht aktiviert oder fehlerhaft. | [Installieren Sie den VM-Gast-Agent](../virtual-machines/extensions/agent-windows.md) manuell. |

### <a name="autoprotectioncancelledornotvalid"></a>AutoProtectionCancelledOrNotValid

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
| Der beabsichtigte automatische Schutz wurde entweder entfernt oder ist nicht mehr gültig. | Wenn Sie den automatischen Schutz für eine SQL Server-Instanz aktivieren, werden Aufträge des Typs **Sicherung konfigurieren** für alle Datenbanken in dieser Instanz ausgeführt. Wenn Sie den automatischen Schutz während der Ausführung der Aufträge deaktivieren, werden die Aufträge des Typs **In Bearbeitung** mit diesem Fehlercode abgebrochen. | Aktivieren Sie den automatischen Schutz erneut, um alle restlichen Datenbanken zu schützen. |

### <a name="clouddosabsolutelimitreached"></a>CloudDosAbsoluteLimitReached

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
Der Vorgang ist blockiert, da Sie den Höchstwert für die Anzahl der innerhalb von 24 Stunden durchführbaren Vorgänge erreicht haben. | Dieser Fehler tritt auf, wenn Sie den maximal zulässigen Grenzwert für einen Vorgang im Zeitraum von 24 Stunden erreicht haben. <br> Beispiel: Wenn Sie den Grenzwert für die Anzahl der Aufträge zum Konfigurieren der Sicherung, die pro Tag ausgelöst werden können, erreicht haben und versuchen, die Sicherung für ein neues Element zu konfigurieren, wird diese Fehlermeldung angezeigt. | In der Regel wird dieses Problem durch Wiederholen des Vorgangs nach 24 Stunden behoben. Wenn das Problem jedoch weiterhin besteht, können Sie sich an den Microsoft-Support wenden, um Unterstützung zu erhalten.

### <a name="clouddosabsolutelimitreachedwithretry"></a>CloudDosAbsoluteLimitReachedWithRetry

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
Der Vorgang wird blockiert, da der Tresor die in einem Zeitraum von 24 Stunden maximal zulässige Anzahl von Vorgängen erreicht hat. | Dieser Fehler tritt auf, wenn Sie den maximal zulässigen Grenzwert für einen Vorgang im Zeitraum von 24 Stunden erreicht haben. Dieser Fehler tritt in der Regel bei skalierten Vorgängen auf, z. B. beim Ändern von Richtlinien oder beim automatischen Schutz. Anders als bei CloudDosAbsoluteLimitReached lässt sich dieses Problem nicht beheben. Der Azure Backup-Dienst wiederholt die Vorgänge für alle betroffenen Elemente intern.<br> Beispiel: Wenn eine große Anzahl von Datenquellen durch eine Richtlinie geschützt wird und Sie versuchen, diese Richtlinie zu ändern, werden Aufträge zum Konfigurieren des Schutzes für alle geschützten Elemente ausgelöst, sodass manchmal der pro Tag maximal zulässige Grenzwert für diese Vorgänge erreicht wird.| Der Azure Backup-Dienst wiederholt diesen Vorgang automatisch nach 24 Stunden.

### <a name="usererrorvminternetconnectivityissue"></a>UserErrorVMInternetConnectivityIssue

| Fehlermeldung | Mögliche Ursachen | Empfohlene Maßnahme |
|---|---|---|
Die VM kann den Azure Backup-Dienst aufgrund von Problemen mit der Internetverbindung nicht erreichen. | Die VM benötigt eine ausgehende Verbindung zu den Diensten von Azure Backup, Azure Storage oder Azure Active Directory.| – Wenn Sie die Konnektivität mit NSG einschränken, sollten Sie den ausgehenden Zugriff auf Azure Backup in den Diensten Azure Backup, Azure Storage oder Azure Active Directory mit dem Diensttag AzureBackup zulassen. Mithilfe folgender [Schritte](https://docs.microsoft.com/azure/backup/backup-sql-server-database-azure-vms#allow-access-using-nsg-tags) können Sie den Zugriff erteilen.<br>– Stellen Sie sicher, dass DNS Azure-Endpunkte löst.<br>– Überprüfen Sie, ob sich die VM hinter einem Lastenausgleich befindet, der den Zugriff auf das Internet blockiert. Durch das Zuweisen einer öffentlichen IP-Adresse funktioniert die Ermittlung.<br>– Überprüfen Sie, ob eine Firewall/ein Antivirenprogramm/ein Proxy die Aufrufe der drei oben genannten Dienste blockiert.

## <a name="re-registration-failures"></a>Fehler bei der erneuten Registrierung

Überprüfen Sie vor dem Auslösen der erneuten Registrierung, ob ein oder mehrere der folgenden Symptome vorhanden sind:

* Für alle Vorgänge (z.B. Sicherung, Wiederherstellung und Sicherungskonfiguration) tritt auf der VM ein Fehler mit einem der folgenden Fehlercodes auf: **WorkloadExtensionNotReachable**, **UserErrorWorkloadExtensionNotInstalled**, **WorkloadExtensionNotPresent**, **WorkloadExtensionDidntDequeueMsg**.
* Wenn im Bereich **Sicherungsstatus** für das Sicherungselement der Status **Nicht erreichbar** angezeigt wird, schließen Sie alle anderen Gründe aus, die zum gleichen Status führen könnten:

  * Fehlende Berechtigung zur Durchführung von sicherungsbezogenen Vorgängen auf der VM
  * Herunterfahren des virtuellen Computers, sodass die Sicherungen nicht durchgeführt werden können
  * Netzwerkfehler

   ![Wiederkehrende Registrierung der VM](./media/backup-azure-sql-database/re-register-vm.png)



* Bei einer Always On-Verfügbarkeitsgruppe: Für die Sicherungen ist ein Fehler aufgetreten, nachdem Sie die Sicherungseinstellung geändert haben, oder nach einem Failover.

Zu diesen Symptomen kann es aufgrund von einer oder mehreren der folgenden Ursachen kommen:

* Eine Erweiterung wurde gelöscht oder im Portal deinstalliert.
* Eine Erweiterung wurde in der **Systemsteuerung** der VM unter **Programm deinstallieren oder ändern** deinstalliert.
* Die VM wurde über eine direkte Datenträgerwiederherstellung rechtzeitig wiederhergestellt.
* Die VM wurde für längere Zeit heruntergefahren, sodass die Erweiterungskonfiguration dafür abgelaufen ist.
* Die VM wurde gelöscht, und eine andere VM wurde mit dem gleichen Namen und in derselben Ressourcengruppe wie die gelöschte VM erstellt.
* Einer der Verfügbarkeitsgruppenknoten hat nicht die vollständige Sicherungskonfiguration erhalten. Dies kann passieren, wenn die Verfügbarkeitsgruppe im Tresor registriert ist, oder wenn ein neuer Knoten hinzugefügt wird.

In den vorhergehenden Szenarien sollten Sie einen Neuregistrierungsvorgang auf der VM auszulösen. Anweisungen zum Durchführen dieser Aufgabe in PowerShell finden Sie [hier](https://docs.microsoft.com/azure/backup/backup-azure-sql-automation#enable-backup).

## <a name="size-limit-for-files"></a>Maximale Größe für Dateien

Die gesamte Zeichenfolgengröße von Dateien hängt nicht nur von der Anzahl der Dateien, sondern auch von deren Namen und Pfaden ab. Rufen Sie für jede der Datenbankdateien den logischen Dateinamen und den physischen Pfad ab. Sie können diese SQL-Abfrage verwenden:

```sql
SELECT mf.name AS LogicalName, Physical_Name AS Location FROM sys.master_files mf
               INNER JOIN sys.databases db ON db.database_id = mf.database_id
               WHERE db.name = N'<Database Name>'"
```

Ordnen Sie sie jetzt im folgenden Format an:

```json
[{"path":"<Location>","logicalName":"<LogicalName>","isDir":false},{"path":"<Location>","logicalName":"<LogicalName>","isDir":false}]}
```

Hier sehen Sie ein Beispiel:

```json
[{"path":"F:\\Data\\TestDB12.mdf","logicalName":"TestDB12","isDir":false},{"path":"F:\\Log\\TestDB12_log.ldf","logicalName":"TestDB12_log","isDir":false}]}
```

Wenn die Zeichenfolgegröße des Inhalts 20.000 Bytes überschreitet, werden die Datenbankdateien anders gespeichert. Während der Wiederherstellung können Sie den Pfad der Zieldatei für die Wiederherstellung nicht festlegen. Die Dateien werden in dem von SQL Server bereitgestellten Standard-SQL-Pfad wiederhergestellt.

### <a name="override-the-default-target-restore-file-path"></a>Außerkraftsetzen des Standard-Zieldateipfads für die Wiederherstellung

Sie können den Zieldateipfad für die Wiederherstellung während des Wiederherstellungsvorgangs außer Kraft setzen, indem Sie eine JSON-Datei mit der Zuordnung der Datenbankdatei zum Wiederherstellungszielpfad platzieren. Erstellen Sie eine Datei `database_name.json`, und speichern Sie sie am Speicherort *C:\Programme\Azure Workload Backup\bin\plugins\SQL*.

Der Inhalt der Datei sollte dieses Format haben:

```json
[
  {
    "Path": "<Restore_Path>",
    "LogicalName": "<LogicalName>",
    "IsDir": "false"
  },
  {
    "Path": "<Restore_Path>",
    "LogicalName": "LogicalName",
    "IsDir": "false"
  },  
]
```

Hier sehen Sie ein Beispiel:

```json
[
  {
   "Path": "F:\\Data\\testdb2_1546408741449456.mdf",
   "LogicalName": "testdb7",
   "IsDir": "false"
  },
  {
    "Path": "F:\\Log\\testdb2_log_1546408741449456.ldf",
    "LogicalName": "testdb7_log",
    "IsDir": "false"
  },  
]
```

Im oben stehenden Inhalt können Sie den logischen Namen der Datenbankdatei mit der folgenden SQL-Abfrage abrufen:

```sql
SELECT mf.name AS LogicalName FROM sys.master_files mf
                INNER JOIN sys.databases db ON db.database_id = mf.database_id
                WHERE db.name = N'<Database Name>'"
  ```

Diese Datei muss abgelegt werden, bevor Sie den Wiederherstellungsvorgang auslösen.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Azure Backup für SQL Server-VMs (Public Preview) finden Sie unter [Azure Backup für SQL-VMs](../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md#azbackup).
