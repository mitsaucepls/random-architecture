# Quiz-App: Architekturprozess & -dokumentation
**Alternative Prüfungsleistung** – *Architekturprozess & -dokumentation*<br>
📅 **Datum:** 16.01.2025<br>
👨‍💻 **Team:** Marvin Hofmann, Markus Siegert

---

## 1. Zielsetzung & Kontext
Die Quiz-App soll eine interaktive Plattform bieten, die es Nutzern ermöglicht, eigene Quizze zu erstellen und als Präsentation zu bespielen.
Diese Architektur-Dokumentation beschreibt den Übergang vom aktuellen (Ist-) zum zukünftigen (Soll-) Zustand unter Berücksichtigung von Skalierbarkeit, Modularität und Multiuser-Fähigkeit.

---

## 2. Architektur: Ist vs. Soll

### 2.1 Ist-Zustand (Aktuelle Architektur)
✅ **Funktionale Software, aber keine dedizierte Architektur-Dokumentation.**<br>
✅ **Quiz-App mit Fokus auf Spielen vordefinierter Quizze.**<br>
✅ **Monolithischer Tech-Stack:**
   - **Next.js:** Vereint Frontend & Backend + Authentifizierung
   - **PostgreSQL:** Single-Instance, nicht in Normalform
   - **WebSockets in Next.js:** Direkt integriert, aber schwer skalierbar

### 2.2 Soll-Zustand (Zielarchitektur)
📌 **Neue Features & Verbesserungen:**<br>
✅ **Erweiterung um Quiz-Erstellung mit individuellem Präsentationsstil.**<br>
✅ **Microservices-Architektur für bessere Skalierbarkeit.**<br>
✅ **Modularisierung der Architektur für unabhängige Skalierung von Funktionen.**

#### 2.2.1 Skalierbarkeit & Modularität
- **Unabhängige Skalierung der Instanzen für:**
  - „Quiz spielen“
  - „Quiz erstellen“
  - Authentifizierung
  - Backend-Logik
- **Microservices für Backend-Logik & WebSockets**
- **Datenbank: PostgreSQL wird in normalisierte Form überführt oder auf NoSQL erweitert (z.B. JSONB für flexible Datenstrukturen).**

#### 2.2.2 Tech-Stack im Soll-Zustand
| **Komponente**      | **Technologie (Ist-Zustand)** | **Technologie (Soll-Zustand)** |
|---------------------|----------------------------|----------------------------|
| Frontend           | Next.js (Monolith)         | Next.js (separate Instanzen je Feature) |
| Backend            | Next.js Backend integriert | Node.js/Microservices (z. B. Express/NestJS) |
| Datenbank          | PostgreSQL (nicht normalisiert) | PostgreSQL normalisiert oder hybride Lösung (JSONB + PostgreSQL) |
| Echtzeit-Kommunikation | WebSockets in Next.js | WebSockets als Microservice mit Redis Pub/Sub |
| Skalierung         | Monolithisch (1 Instanz)   | Kubernetes für horizontale Skalierung |
| Authentifizierung  | NextAuth.js in Next.js    | Auth0 oder Keycloak für skalierbare Auth-Lösung |

---

## 3. Kommunikationsstrategie & Integration
- **Microservices-Kommunikation:**<br>
  ✅ **RESTful APIs** für synchrone Kommunikation zwischen Frontend & Backend<br>
  ✅ **WebSockets & Redis Pub/Sub** für Echtzeit-Updates & Synchronität zwischen Spielern<br>
  ✅ **API Gateway (z. B. Kong, Nginx)** als zentrale Routing-Instanz

---

## 4. Skalierbarkeit & DevOps

### 4.1 Skalierungsstrategie
✅ **Frontend & Backend als eigenständige Container** → Docker<br>
✅ **Automatische Skalierung über Kubernetes**<br>
✅ **Datenbank-Lastverteilung durch Read Replicas (PostgreSQL) oder Sharding (MongoDB)**

### 4.2 Deployment-Pipeline
📌 **CI/CD mit GitHub Actions oder GitLab CI/CD**<br>
📌 **Automatische Tests (Jest, Cypress) & Code-Review Pipelines**<br>
📌 **Containerized Deployment (Docker + Kubernetes mit Helm Charts)**

---

## 5. Nicht-funktionale Anforderungen (NFRs)
| **Kategorie**       | **Anforderung** |
|---------------------|----------------|
| **Performance**    | Antwortzeit <200ms für API-Requests |
| **Sicherheit**     | OAuth2/OpenID Connect für Authentifizierung |
| **Fehlertoleranz** | Circuit Breaker für API-Kommunikation |
| **Verfügbarkeit**  | 99,95% Uptime durch Load Balancer & Multi-Region Deployment |

---

## 6. Fazit & Nächste Schritte
🔹 **Architektur-Entwurf basiert auf Skalierbarkeit, Modularität & Echtzeit-Kommunikation.**<br>
🔹 **Microservices-Ansatz mit eigenständigen Frontend-/Backend-Instanzen.**<br>
🔹 **Technologische Upgrades für Skalierbarkeit & Performance.**<br>
🔹 **Als nächster Schritt: Erstellung eines Proof of Concept (PoC) mit einer minimalen Microservice-Architektur.**

---

### 📌 Architektur-Visualisierung (Beispiel)
*(Hier wäre ein Diagramm hilfreich, das die Architektur mit Microservices, API Gateway & Skalierung zeigt.)*

---

### 🚀 Verbesserungen im Vergleich zur ursprünglichen Version
✅ **Mehr Klarheit in der Skalierbarkeit (Microservices & Kubernetes)**<br>
✅ **Detaillierte DevOps-Strategie mit CI/CD & Testing**<br>
✅ **Klare Architektur-Kommunikation & Diagramm-Vorschlag**<br>
✅ **Nicht-funktionale Anforderungen (Performance, Sicherheit, Verfügbarkeit)**
