# Quiz-App
**Alternative Prüfungsleistung – Architekturprozess & -dokumentation**
**16.01.2025**
**Marvin Hofmann, Markus Siegert**

---

## Teammitglieder
- Marvin Hofmann
- Markus Siegert

---

## Architektur Ist/Soll

### Gegeben:
- **Ist-Zustand:**
  - Funktionalität der Software ist gegeben.
  - Keine Ist-Zustand Architektur vorhanden.

### Ziel:
- **Ist-Architektur:**
  - Erstellung einer Ist-Architektur, die die komplette Funktionalität des Status-Quo der Quiz-App abdeckt.
- **Soll-Architektur:**
  - Ergänzt um eine Ansicht zum Erstellen von Quizzen.
  - Berücksichtigung des Skalierbarkeitsfaktors.

### Skalierbarkeit:
- Modularität der Instanzen gewährleisten:
  - **Unabhängige Skalierung** der Module:
    - „Quiz spielen“
    - „Quiz erstellen“
    - Authentifizierungs-Logik
    - Zugehörige Backend-Logik

### Modularität:
- Keine Abhängigkeiten zwischen den Instanzen.
- Backend-Logik, auf die mehrere Frontend-Instanzen zugreifen, wird in eine eigene Backend-Instanz ausgelagert.

### Zielgruppe:
- Entwickler zwischen **20 und 25 Jahren** auf **Junior-Niveau**.

---

## Softwareprodukt/-projekt

### Produkt:
- **Quiz-App** (ähnlich zu *Mentimeter* mit nutzererstellten Quizzen).
- App soll Nutzern die Möglichkeit bieten, **Quizze als Präsentation zu erstellen und mit anderen zu bespielen**.
- **Komplexität:** ca. **5000 Lines of Code**.
- Funktionale App, aber **keine Softwarearchitektur-Dokumentation**.

### Software Ist-Zustand:
- **Quiz-App**, ausgelegt auf das Spielen von vordefinierten Quizzen.
- Quizze beinhalten nur eine **Standard-Ansicht** ohne individuellen Präsentationsstil.

#### **Ist-Zustand Tech-Stack:**
- **Next.js**:
  - Einzige Instanz, die sowohl Frontend- als auch Backend-Logik vereint (inkl. Nutzer-Authentifizierung).
- **PostgreSQL-Datenbank**:
  - Einzige Instanz zur Speicherung von Daten (nicht in Normalform).
- **WebSockets in Next.js**:
  - Direkt integriert für bidirektionale Kommunikation.
  - Skalierung limitiert durch den Next.js-Server.

### Software Soll-Zustand:
- Quiz-App im Ist-Zustand **+ zusätzliche Funktion**:
  - **Quizze mit individuellem Präsentationsstil können bespielt werden**.

#### **Soll-Zustand Tech-Stack:**
- **Next.js**:
  - Mehrere Instanzen für unterschiedliche Teile der Geschäftslogik.
- **Backend-Logik + WebSockets**:
  - In **Microservices** ausgegliedert.
  - Unterschiedliche Next.js-Instanzen greifen auf eine **gemeinsame Backend-Logik** zu.

---

## Besonderer Fokus (Technische Konzepte, ...)

- **Implementation einer neuen Ansicht** zum Erstellen von Quizzen (inkl. Nutzer-Authentifizierung).
- **Modularität der Komponenten**:
  - Unterschiedliche Frontend-Instanzen müssen auf dieselbe Backend-Logik zugreifen können.
- **Multiuser-Fähigkeit**:
  - Synchronität der Spieler gewährleisten.
  - Benötigt Skalierungsmöglichkeit & Modularität der Instanzen.
- **Unabhängige Skalierbarkeit** der Logik für das **Spielen und Erstellen von Quizzen** (in separaten Instanzen).
