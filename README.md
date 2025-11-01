# 1) Voll-medienbruchfreies E-Collecting: direkte  Demokratie im digitalen Zeitalter

*Over the course of two days, you will develop your solution for collecting electronic signatures for popular initiatives and referendums from A to Z, addressing the 10 topics outlined in the [guidelines](https://www.bk.admin.ch/bk/de/home/politische-rechte/e-collecting/aktuelles.html). Your prototype can be conceptual, clickable, and/or technical. Either way, you should clearly present the interactions and data flows between actors, software, and infrastructure components over time, as well as the user experience of these actors.*

## Approach


**Sales pitch**
<img width="1915" height="938" alt="Seite _1" src="https://github.com/user-attachments/assets/8181363a-f595-4dce-940a-88d944f83a9c" />
<img width="1916" height="940" alt="Seite_2" src="https://github.com/user-attachments/assets/8d033a25-8970-44f8-93dc-004deae6fc28" />
<img width="1912" height="940" alt="Seite_3" src="https://github.com/user-attachments/assets/1b94e0b8-5258-4799-8e59-ab7269b10a64" />
<img width="1912" height="938" alt="Seite_4" src="https://github.com/user-attachments/assets/ba702319-890c-4712-a428-8bcf3d5e4dc8" />
<img width="1916" height="940" alt="Seite_5" src="https://github.com/user-attachments/assets/f4624fe8-1d2a-40cc-9d6f-63554ee46a99" />

**Sales pitch version in PDF**
[Voll-medienbruchfreies-eCollecting_sales pitch.pdf](https://github.com/user-attachments/files/23126915/Voll-medienbruchfreies-eCollecting_sales.pitch.pdf)



## *Three bullet points that summarize it technically*

- Nodes oder API's
- Blockchain (Permissioned DLT)
- Dasboards & Audit-UI
  

## *User Journey*

**1. Digitale Teilnahme**

Bürger*in meldet sich über die eCollecting-Plattform an und authentifiziert sich mit einer staatlich geprüften eID.
Nach erfolgreichem Login wird ein Unterschriftsvorgang gestartet.

**2. Stimmrechtsprüfung**

Die Gemeinde-API fragt das kantonale Stimmregister ab und prüft, ob die Person stimmberechtigt ist.
Ergebnis: OK/NICHT-OK – wird nur für die Prüfung genutzt, nicht gespeichert.

**3. Digitale Signatur & Speicherung**

Wenn gültig:

- Gemeinde erstellt ein signiertes Unterschrifts-Artefakt (z. B. PDF + Metadaten).
- Artefakt wird verschlüsselt im föderalistischen IPFS-Cluster gespeichert.
- Aus dem Inhalt entsteht ein CID (Content Identifier) – der eindeutige Hash des Objekts.

Ein CID-Registry speichert Metadaten wie Zeitstempel, Gemeinde-ID und Status.

**4. IPFS-Einträge & Validierung**

- Gemeinde übermittelt: CID, Zeitstempel, Gemeinde-ID, Status („gültig“, „zurückgezogen“).
- Mehrere IPFS-Nodes (Gemeinden, Kantone, Bund) pinnen und replizieren das Objekt.
- Die Bundes- oder Staatskanzlei kann über die Registry alle gültigen Einträge zählen – ohne Zugriff auf personenbezogene Daten.

**5. Papierbezogene Unterschriften**

Für physische Unterschriften:

1. Gemeinde prüft Stimmberechtigung.
2. Scan + Metadaten werden erstellt und verschlüsselt gespeichert.
3. Ein CID wird generiert und in der Registry eingetragen.
→ Papier und Digital sind vollständig gleichwertig abgebildet.

**6. Komitee-Dashboard & Monitoring**

Ein Dashboard zeigt in Echtzeit:

- Anzahl gültiger Unterstützungen (digital & Papier)
- Verteilung nach Gemeinden/Kantonen
- Auditierbarkeit via CIDs

Keine personenbezogenen Daten – nur verifizierbare Hashes & Metadaten.

**7. Bürger*innen-Selbstprüfung**

Bürger*innen können prüfen, ob ihre Unterschrift registriert wurde:
→ über einen CID-Lookup oder eine anonyme Prüfreferenz.
Nur der Hash wird angezeigt – keine Identitätsdaten.

## *Main challenges*
  
Blockchain:
- **Off-Chain Storage (verschlüsselt)**: Persönliche Daten und komplette Signatur-Artefakte bleiben bei der Gemeinde oder in einem verschlüsselten föderalistischen Datenspeicher
- **Blockchain (Permissioned DLT)**: Speichert Prüfergebnisse, Transaktions-Metadaten, Hashes von Unterschriftsartefakten, Zeitstempel, Statusflags (z. B. gültig, zurückgezogen)
- **Blockchain-Integration** papierbasierter Unterschriften
- **Smart Contracts / Chaincode**: Regeln Validierung, Aufnahme, Grundregeln für Revocation und Übermittlung an die zentrale Stelle
- **Zentrale Zählkomponente (Bund-/Staatskanzlei)**: Liest die Blockchain, zählt Referenzen (verifiziert mit Smart Contract Logik)

Gemeinde-API:
- Kommuniziert mit eID, verifiziert Stimmberechtigung über kantonale Stimmregister
  

## *Sub-challenges*

- **eID-System**: Identifizierung & digitale Signatur der Stimmberechtigten (Login + Signatur)
- **eCollecting Plattform**: Wo Bürger unterschreiben
- **Dashboards & Audit-UI**: Für Komitees/Kantone/öffentliche Transparenz (mit Rollen & Zugriffskontrolle)

## *Required skills*   
- UX/UI Designer						(Prototyp: Bürger-Flow & Behörden-Dashboard)
- Frontend Developer                   	(React/Next.js – Login, Signatur & Bestätigung)
- Backend Developer                 	(API-Simulation eID-Gemeinde–Bund)
- Security Engineer                 	(Proof-of-Concept für eID-Verifikation & Datenintegrität)
- DevOps                             	(Setup & GitHub-Dokumentation, CI/CD)
- Legal/Policy Researcher            	(Rechtliche Rahmenbedingungen & Datenschutz)


## Documentation and Diagrams


Klar — hier ist dein Text **neu formuliert für IPFS** (statt Blockchain), im **gleichen GitHub-kompatiblen Format** inklusive Markdown-Struktur, Emojis und Tabellen.
Ich habe alle blockchain-spezifischen Teile auf **IPFS (InterPlanetary File System)** übertragen und gleichzeitig den föderalistischen, datenschutzkonformen Charakter des Projekts beibehalten.

---

# eCollecting – **IPFS – Technische Architektur**

## 🧭 Übersicht

Dieses Projekt beschreibt die **technische Architektur** und den **Ablauf** eines föderalistischen, datenschutzkonformen eCollecting-Systems, das sowohl **digitale** als auch **papierbasierte Unterschriften** sicher und nachvollziehbar verarbeitet.
Ziel: **Integrität, Transparenz und Nachvollziehbarkeit**, ohne dass personenbezogene Daten auf zentralen Servern gespeichert werden.

---

## 📑 Inhaltsverzeichnis

1. [Was macht IPFS hier?](#1-was-macht-ipfs-hier)
2. [Wichtige Design-Entscheidung](#2-wichtige-design-entscheidung)
3. [Systemkomponenten](#3-systemkomponenten)
4. [Ablauf (User Journey)](#4-ablauf-user-journey)
5. [IPFS-Datenobjekte](#5-ipfs-datenobjekte)
6. [Revocation / Rückzug](#6-revocation--rückzug)
7. [Datenschutz-Techniken](#7-datenschutz-techniken)
8. [Authentisierung & Schlüsselmanagement](#8-authentisierung--schlüsselmanagement)
9. [Metadaten & Integritätsnachweis](#9-metadaten--integritätsnachweis)
10. [Papierbasierte Unterschriften – Integration](#10-papierbasierte-unterschriften--integration)
11. [Beispielhafte Datenstrukturen & Upload-Logik](#11-beispielhafte-datenstrukturen--upload-logik)
12. [Sicherheit & Rechtliches](#12-sicherheit--rechtliches)
13. [Empfehlungen für Betrieb & Audit](#13-empfehlungen-für-betrieb--audit)
14. [Governance & Betrieb](#14-governance--betrieb)
15. [Vor und Nachteile](#15-vor-und-nachteile)
16. [Technische Optionen](#16-technische-optionen)
17. [Bedrohungsmodell & Gegenmaßnahmen](#17-bedrohungsmodell--gegenmaßnahmen)
18. [Roadmap / Umsetzung](#18-roadmap--umsetzung)

---

## 1. Was macht IPFS hier?

Stell dir IPFS als ein **verteiltes Archivsystem** vor, das von **Gemeinden, Kantonen und dem Bund** gemeinsam betrieben wird.
Jede gültige Unterschrift wird als **verschlüsseltes Objekt** gespeichert und über ihren **Inhalts-Hash (CID)** eindeutig identifiziert.

**Funktionen:**

* Nachvollziehbar: Wer wann wie viele Unterschriften abgelegt hat.
* Manipulationssicher: Inhalte können nachträglich nicht verändert werden.
* Dezentral: Behörden können unabhängig prüfen und zählen.

📘 **Wichtig:** Keine Personendaten im Klartext!
Gespeichert werden nur verschlüsselte Artefakte & Metadaten-Hashes.

---

## 2. Wichtige Design-Entscheidung

> **Federiertes IPFS-Netzwerk (Private IPFS Cluster)** – Nur staatliche Akteure (Gemeinden, Kantone, Bund) betreiben Nodes.
> Dadurch sind **Governance, Datenschutz und rechtliche Verantwortung** klar geregelt.

---

## 3. Systemkomponenten

| Komponente                                      | Beschreibung                                           |
| ----------------------------------------------- | ------------------------------------------------------ |
| **eID-System**                                  | Authentifizierung & Signatur der Stimmberechtigten     |
| **Gemeinde-API / eCollecting-Plattform**        | Webplattform für Bürger, prüft Stimmberechtigung       |
| **Verschlüsselter Object-Store (IPFS Cluster)** | Speicherung persönlicher Artefakte, Signaturen, Scans  |
| **CID-Registry (Index-Dienst)**                 | Erfasst Hashes, Status & Metadaten                     |
| **Integrity Proof Service**                     | Verifiziert Integrität & Zeitstempel                   |
| **Zentrale Zählkomponente (Bund)**              | Aggregiert & prüft Metadaten                           |
| **Dashboards / Audit-UI**                       | Transparenz & Monitoring für Behörden & Öffentlichkeit |

---

## 4. Ablauf (User Journey)

1. Bürger loggt sich via eID ein und unterschreibt.
2. Gemeinde prüft Stimmberechtigung.
3. Verschlüsselung & Upload der Unterschrift:

   * Signatur-Artefakt wird verschlüsselt.
   * Artefakt + Metadaten werden auf IPFS hochgeladen.
   * CID wird im föderalen Index-System registriert.
4. Bund zählt registrierte CIDs und prüft Integrität über Hashes.

---

```mermaid
flowchart TB
    A["Bürger möchte Initiative/Referendum unterschreiben"] --> B["Papier oder elektronisch?"]
    B --> C["Papierbogen unterschreiben"] & D["elektronisch via eCollecting Interface"]
    n1["Bürgerin-Sicht"] --> A & n4["Initiative im eCollecting-Interface einreichen"] & n8["Unterschriften erhalten"] & n11["Metadaten aus IPFS abrufen"]
    D --> n2["Zugriff auf eID-Daten bestätigen"]
    n2 --> n3["CID generieren und Objekt verschlüsselt hochladen"]
    C --> n3
    n4 --> n5["Unterschriften via Plattform & Papierbogen erhalten"]
    n5 --> n7["Signierte Unterschriftsbögen einreichen"]
    n7 --> n9["Scannen, Metadaten erstellen, CID registrieren"]
    n9 --> n10["Integritätsnachweis & Speicherung im IPFS-Cluster"]
    n10 --> n11
    n11 --> n12["Zählung und Prüfung durch Bund"]
    n21["Farben: Bürger (gelb), Initiant (violett), Gemeinde (blau), Bund (grün)"]
```

---

## 5. IPFS-Datenobjekte

**Gespeichert wird nur das Minimum:**

* Verschlüsseltes Unterschriftsartefakt
* CID (Content Identifier, z. B. `Qm...xyz`)
* Zeitstempel & Prüfsumme
* Gemeinde/Kanton-ID
* Statusflag (gültig, zurückgezogen etc.)
* Optionale Referenz zu Papierdokument (Merkle-Root oder UUID)

**Datenschutz:** DSG/GDPR-konform – keine sensiblen Personendaten unverschlüsselt gespeichert.

---

## 6. Revocation / Rückzug

* IPFS ist *content-addressed* – Änderungen erzeugen neue CIDs.
* Rückzug erfolgt durch **neue Version des Metadatenobjekts** mit `status: revoked`.
* Historie bleibt nachvollziehbar über die Versionskette (`IPNS` oder Registry-Verlauf).

→ **Transparent, unveränderlich, revisionssicher.**

---

## 7. Datenschutz-Techniken

* **Ende-zu-Ende-Verschlüsselung** aller Artefakte
* **CID-basierte Pseudonymisierung**
* **Private IPFS Cluster + Access Tokens**
* **Zero-Knowledge Proofs (ZKP)** optional zur Validierung
* **Keine Metadatenlecks** durch dedizierte Gateway-Architektur

---

## 8. Authentisierung & Schlüsselmanagement

* Bürger signiert mit **eID** (juristische Signatur)
* Gemeinden & Behörden nutzen **HSMs oder KMS** für Schlüssel
* **Signierte IPFS-Pins** (Authentizität gesichert)
* **TLS + gegenseitige Authentifizierung** zwischen Nodes

---

## 9. Metadaten & Integritätsnachweis

Eine separate föderierte **CID-Registry** speichert:

* CID
* Signatur der hochladenden Behörde
* Zeitstempel
* Status (valid / revoked / counted)
* Prüfsumme (Hash über Dateiinhalt)

Optional kann regelmäßig ein **Merkle-Root über alle Tages-CIDs** gebildet und als Audit-Beleg (z. B. in öffentlichem Journal oder Blockchain-Anker) abgelegt werden.

---

## 10. Papierbasierte Unterschriften – Integration

Auch **Papierunterschriften** können über IPFS nachgewiesen werden.
Gemeinden digitalisieren geprüfte Papierbögen, erzeugen daraus **Hashes & CIDs**, und laden die verschlüsselten Artefakte in den Cluster.

### Zwei Modi

| Modus                   | Beschreibung                                                             |
| ----------------------- | ------------------------------------------------------------------------ |
| **Einzeln (Itemized)**  | Jede Unterschrift einzeln gehasht und auf IPFS gespeichert               |
| **Batch (Merkle-Root)** | Mehrere Scans → Hashbaum → Merkle-Root-Objekt gespeichert (performanter) |

---

## 11. Beispielhafte Datenstrukturen & Upload-Logik

### Beispiel-Payload (Batch-Upload)

```json
{
  "type": "paper_signature_batch",
  "authority_id": "gemeinde-zh-123",
  "batch_id": "BATCH-2025-10-27-001",
  "merkle_root": "0x9f2...ab3",
  "count": 138,
  "timestamp": "2025-10-27T09:42:00Z",
  "ipfs_cid": "QmXyz123...",
  "attestation_signature": "MEUCIQDb...",
  "metadata": {
    "storage_ref": "ipfs://QmXyz123...",
    "scan_format": "PDF/A-2",
    "hash_algorithm": "SHA-256"
  }
}
```

### Beispielhafte Upload-Logik (Pseudocode)

```javascript
async function submitBatch(batchData, privateKey) {
  const cid = await ipfs.add(encrypt(batchData));
  const attestation = sign(privateKey, cid + batchData.timestamp);
  registry.add({
    cid,
    authority: batchData.authority_id,
    merkle_root: batchData.merkle_root,
    count: batchData.count,
    status: "accepted",
    attestation
  });
  emit("BatchSubmitted", cid, batchData.authority_id, batchData.count);
}
```

---

## 12. Sicherheit & Rechtliches

* Keine Klartextdaten in IPFS
* Off-Chain-Archivierung gesetzeskonform (PDF/A)
* Autorisierte Behörden signieren Uploads
* Rückzüge dokumentiert über neue Versionen
* Auditlog & Zeitstempelung verpflichtend

---

## 13. Empfehlungen für Betrieb & Audit

1. Standardisierte **CID-Registry** mit Audit-Trail
2. Einheitliche **Scan-Richtlinien** (DPI, Format, Hash-Algorithmen)
3. **HSM-Signaturen** für Uploads
4. **Multi-Sig-Genehmigungen** bei Batch-Uploads
5. **Datenschutz- & Sicherheits-Audits** jährlich
6. **Juristische Klärung** zu Aufbewahrung & Rückzugspflichten

---

## 14. Governance & Betrieb

* **Cluster-Betreiber:** Gemeinden, Kantone, Bund
* **Betriebsvereinbarungen:** SLAs, Datenschutz, Replikationsrichtlinien
* **Audits & PenTests:** Regelmäßig extern
* **Governance via Multi-Sig & föderierte Kontrolle**

---

## 15. Vor– und Nachteile

| Vorteile                                | Herausforderungen                         |
| --------------------------------------- | ----------------------------------------- |
| Dezentral, kein Single Point of Failure | Koordination vieler Behörden              |
| DSG-konform durch Verschlüsselung       | Aufwändiges Schlüsselmanagement           |
| Transparente Integritätsnachweise       | Versionierung & Zugriffskontrolle komplex |
| Geringe Abhängigkeit von Blockchain     | Rechtliche Anerkennung neu zu definieren  |

---

## 16. Technische Optionen

* **IPFS-Cluster (Private Network Mode)**
* **libp2p Access Control Lists (ACL)**
* **Merkle-DAG für Batch-Strukturen**
* **IPNS für Revocation und Updates**
* **W3C Verifiable Credentials / DIDs** für eID-Integration

---

## 17. Bedrohungsmodell & Gegenmaßnahmen

| Bedrohung            | Gegenmaßnahme                             |
| -------------------- | ----------------------------------------- |
| Manipulierte Uploads | Digitale Signaturen, CID-Validierung      |
| Key-Diebstahl        | HSM, MFA, Key Recovery                    |
| Datenlecks           | Verschlüsselung, private Cluster          |
| Unautorisierte Pins  | Node-ACL, Access Tokens                   |
| Privacy Leaks        | Pseudonymisierung, ZKP, Gateway-Isolation |

---

## 18. Roadmap / Umsetzung

1. **Design-Workshop & Governance Agreement**
2. **PoC (5 IPFS-Nodes + eID + CID-Registry)**
3. **Pilotphase (ein Kanton, mehrere Gemeinden)**
4. **Evaluation & Skalierung**
5. **Rollout & föderaler Dauerbetrieb**

**Nächste Schritte**

* Technisches Konzept (2–4 Seiten) ausarbeiten
* Stakeholder-Workshop (Bund, Kantone, Gemeinden, Datenschutz, Juristen)
* PoC-Prototyp (3–6 Monate): Private IPFS-Cluster + eID + Audit-Dashboard

---

Möchtest du, dass ich daraus direkt ein **README.md** für GitHub mit Titel, Lizenzabschnitt und visueller Projektstruktur (Ordnerbaum + Beispielkonfiguration) mache?



1. **[Mermaid](https://mermaid.js.org/) diagram(s) showing interactions and data flows between actors, software and infrastructure components of your solution over time.**
2. **Wireframes or mockups with user flow showing the user experience of different actors** (using e.g. Figma)
3. Explain how you addressed the topics presented in the [guidelines](https://www.bk.admin.ch/bk/de/home/politische-rechte/e-collecting/aktuelles.html), filling in the template below.
4. List the key strengths and weaknesses of your solution.
5. Explanation of features used (if applicable)
6. A requirements file with all packages and versions used (if applicable)
7. Environment code to be run (if applicable)

*For your reference, you will find below an example of two diagrams showing interactions and data flows between actors, software and infrastructure components of ordering a pizza via a third-party delivery website over time. Please replace them with diagrams for your solution.*


## User Experience

*Add or reference wireframes or mockups with user flow showing the user experience of different actors.*

## Topics addressed

*Explain how you addressed the topics presented in the [guidelines](https://www.bk.admin.ch/bk/de/home/politische-rechte/e-collecting/aktuelles.html), filling in the template below.*

| Topic | (How) is it addressed? |
| -| ------- |
| 1 | Verschiedene User-Journey, eindeutige Komitee-ID, Menschen mit Beeinträchtigungen können Ihre politischen Rechte selbstbestimmt wahrnehmen|
| 2 | Mit Hilfe eines Dashboard werden die Daten für das Komitee in Echtzeit aufbereitet  |
| 3 | Die Blockchain-Technologie ermöglicht die gesammelten Unterstützungsbekundungen den Sammelorganisationen eindeutig zuzuschreiben |
| 5 | Starke Authentifizierung durch eID mit zusätzlicher Blockchain-Technologie verhindert Fälschungen |
| 6 | Mit Blockchain-Technologie und Dashboardvisualisierung der gezählten gültigen Stimmen in Echtzeit sind unterschlagene Unterstützungsbekundungen nicht mehr möglich |
| 7 | Stufe 3 |
| 8 | Anbindung Papierprozess - manuelle Überprüfung/Ergänzung direkt auf der Blockchain |

## Key Strenghts and Weaknesses

*List the key strengths and weaknesses of your solution.*

### Strengths:

- Integrität & Nachvollziehbarkeit (Manipulation praktisch ausgeschlossen)
- Verteilte Verantwortung (kein Single Point of Failure)
- Echtzeit-Transparenz für Komitees und behördliche Kontrolle (Counts / Monitoring)

### Weaknesses / Challenges:

- Komplexe Koordination zwischen Gemeinden/Kantonen/Bund
- Datenschutz erfordert strenge Architektur (keine Klartextdaten on-chain)
- Schlüsselmanagement-Risiko (gestohlene Schlüssel können Schaden anrichten)

## Getting Started

*These instructions will get you a copy of the technical prototype (if applicable) up and running on your local machine for development and testing purposes. **If you are not developing a technical prototype, please present or reference your conceptual and/or clickable prototype.***

### Prerequisites

*What things you need to install the software and how to install them.*

### Installation

*A step by step series of examples that tell you how to get a development env running.*

## Contributing

Please read [CONTRIBUTING.md](/CONTRIBUTING.md) for details on our code of conduct.

## Team Members

- [Marco Loppacher](https://github.com/LoppiNW1) (
  Team leader) 
- [Julia Wegmann](https://github.com/juliaNina) (Konzeptionlle Rolle)
- [Thomas Gemperle](https://github.com/thomasgemperle) (Backend Developer)
- [Hanna Franz](https://github.com/hannafranz) (Frontend Developer, UX-Designer)
- [Nicolas Meylan](https://github.com/Nicolas2030) (Beobachter)

## License

This software is licensed under a AGPL 3.0 License - see the [LICENSE](LICENSE) file for details. Please feel free to [choose any other](https://choosealicense.com/) [Open Source Initiative approved license](https://opensource.org/licenses) (e.g. a permissive license such as [MIT](https://opensource.org/license/mit)). Other content (e.g. text, images, etc.) is licensed under a [Creative Commons CC BY-SA 4.0 license](https://creativecommons.org/licenses/by-sa/4.0/deed.de). Exceptions are possible in consultation with the organizers.
