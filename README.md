# 🤖 Java WhatsApp Chatbot Backend

**Build secure, scalable, and smart conversational automation — right inside WhatsApp.**

---

## 🔍 Description

A modular and scalable **Java + Spring Boot** backend for a WhatsApp chatbot. It integrates the **Meta WhatsApp Cloud API** with **Firebase** (Firestore or Realtime DB) and is deployable on cloud platforms like **Render**, making it ideal for real-time chatbot applications.

<p align=" ">
  <img src="https://img.shields.io/badge/Java-17-blue.svg" alt="Java Badge"/>
  <img src="https://img.shields.io/badge/SpringBoot-Backend-green" alt="SpringBoot Badge"/>
  <img src="https://img.shields.io/badge/Firebase-RealtimeDB-orange" alt="Firebase Badge"/>
  <img src="https://img.shields.io/badge/MetaAPI-WhatsApp-blueviolet" alt="Meta API Badge"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="MIT License Badge"/>
</p>

---

## 📜 Tagline

> *"Empowering seamless human-bot communication — one WhatsApp message at a time."*

---

## ✨ Features

- 🔌 Webhook receiver for WhatsApp messages
- 📬 Meta Cloud API (v18.0) integration
- ☁️ Firebase Firestore / Realtime DB support
- 🔄 REST API structure for extensibility
- ✅ Unit-tested with JUnit
- 🚀 Cloud-deployable via Render, Railway

---

<h2>🧰 Language & Tools</h2>
  <ul>
    <li><strong>Java + Spring Boot</strong> – Backend & APIs</li>
    <li><strong>Firebase Firestore</strong> – Session persistence</li>
    <li><strong>WhatsApp Cloud API</strong> – User interaction</li>
    <li><strong>Render</strong> – Cloud hosting with CI/CD</li>
    <li><strong>JUnit + Mockito</strong> – Unit & integration testing</li>
    <li><strong>Mermaid.js + SVGs</strong> – Architecture visuals</li>
  </ul>

---

## 🧠 System Flow

```
[User sends message via WhatsApp]
          ↓
[Meta WhatsApp Cloud API Webhook]
          ↓
[Spring Boot Controller (/webhook)]
          ↓
[BotService → Firebase (optional)]
          ↓
[Meta API Response → WhatsApp]
          ↓
[User receives chatbot reply]
```

---

## 🧠 System Architecture

```
+------------------+
|      [User]      |
+--------+---------+
         |
         v
+-----------------------------+
|  Meta Cloud API (Webhook)  |
+-------------+---------------+
              |
              v
+-----------------------------+
| Spring Boot Controller      |
+-------------+---------------+
              |
              v
+-----------------------------+
|       BotService            |
+-------------+---------------+
              |
              v
+-----------------------------+
|          Firebase           |
+-------------+---------------+
              |
              v
+-----------------------------+
|  Meta API → WhatsApp Reply |
+-----------------------------+
```

---

## 🧠 System Layers

```
Input Layer:
- WhatsApp User Messages
- Meta Webhook Calls

Processing Layer:
- Spring Boot Controller
- BotService Logic
- Firebase Operations

Output Layer:
- WhatsApp API Responses
- Chatbot Replies to Users
- Firebase Data Updates
```

---

## 📂 Folder Structure

```
whatsapp-chatbot-backend/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── yourorg/
│   │   │           └── whatsappbot/
│   │   │               ├── WhatsAppBotApplication.java
│   │   │               ├── controller/
│   │   │               │   └── WebhookController.java
│   │   │               ├── service/
│   │   │               │   └── BotService.java
│   │   │               ├── config/
│   │   │               │   └── FirebaseConfig.java
│   │   │               ├── model/
│   │   │               │   └── MessagePayload.java
│   │   │               └── util/
│   │   │                   └── ApiHelper.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── firebase-config.json
│   └── test/
│       └── java/
│           └── com/yourorg/whatsappbot/
│               └── BotServiceTest.java
├── .gitignore
├── pom.xml
└── README.md
```
---

## ⚙️ Setup Instructions (Local)

```bash
# Clone the repository
git clone https://github.com/yourusername/whatsapp-chatbot-backend.git
cd whatsapp-chatbot-backend

# Setup Firebase
# Place your service account JSON in: src/main/resources/firebase-config.json

# Configure application.properties
# Example:
firebase.config.path=classpath:firebase-config.json
meta.whatsapp.api.url=https://graph.facebook.com/v18.0/YOUR_PHONE_ID/messages
meta.whatsapp.token=YOUR_WHATSAPP_API_TOKEN

# Build the project
./mvnw clean install

# Run the backend
./mvnw spring-boot:run

# Expose the webhook (for local testing)
ngrok http 8080
```

---

<h3>☁️Deployment</h3>
<ol>
  <li>Push your project to GitHub (with private firebaseConfig.json excluded)</li>
  <li>Login to <a href="https://render.com" target="_blank">Render.com</a> and click "New Web Service"</li>
  <li>Connect your GitHub repo and choose:
    <ul>
      <li>Environment: <code>Java 17</code></li>
      <li>Build Command: <code>./mvnw clean install</code> (or <code>mvn clean install</code>)</li>
      <li>Start Command: <code>java -jar target/navmate-0.0.1-SNAPSHOT.jar</code></li>
    </ul>
  </li>
  <li>Set the following environment variables under "Environment":
    <ul>
      <li><code>WHATSAPP_TOKEN</code> – Your WhatsApp Cloud API token</li>
      <li><code>VERIFY_TOKEN</code> – Webhook verification token</li>
      <li><code>FIREBASE_CONFIG</code> – Path or JSON string of Firebase credentials</li>
    </ul>
  </li>
  <li>Click “Deploy” and wait for the build</li>
  <li>Use the deployed HTTPS endpoint as your WhatsApp webhook</li>
</ol>

<h3>📁 Firebase Setup</h3>
<ol>
  <li>Go to <a href="https://console.firebase.google.com/" target="_blank">Firebase Console</a> and create a new project</li>
  <li>Enable Firestore (in Native mode)</li>
  <li>Go to Project Settings > Service Accounts > Generate Admin SDK Key</li>
  <li>Download the JSON and save as <code>firebaseConfig.json</code> in <code>src/main/resources/</code></li>
</ol>

<h3>🧪 Running Tests</h3>
<pre><code># Run all unit and integration tests
mvn test
</code></pre>

## 📡 API Endpoint

| Method | Endpoint   | Description                                |
| ------ | ---------- | ------------------------------------------ |
| POST   | `/webhook` | Receives messages from WhatsApp (Meta API) |

---

## 🔍 Comparative Analysis

| Feature            | Traditional Chatbot   | WhatsApp Chatbot Backend |
| ------------------ | --------------------- | ------------------------ |
| UI                 | Web Interface         | WhatsApp App             |
| Communication Flow | Polling / WebSockets  | Webhooks (real-time)     |
| Backend Language   | Node / Python / Flask | Java (Spring Boot)       |
| Hosting            | Heroku / Netlify      | Render / Railway         |
| User Reach         | Browser-based         | WhatsApp-native          |

---

## 🧠 Strategic Recommendations

- 🔐 Secure `/webhook` endpoint with token validation
- 🧩 Modularize logic for easier testing and replacement (e.g., RDBMS support)
- 🚀 Automate deployments with GitHub Actions + Render
- 🧠 Integrate NLP (Dialogflow / OpenAI)
- 📈 Add user message analytics with Firebase Logs / GA
- ⚡ Use Redis for high-performance session caching

---

## 🙏 Acknowledgements

- Meta – WhatsApp Cloud API
- Firebase – Realtime DB & Firestore
- Spring Boot Community
- Crafted with ❤️ by **Dark Haven Forge** | © 2025

---

<h2>📜 License</h2>
<p>
  This project is licensed under the 
  <a href="http://www.apache.org/licenses/LICENSE-2.0" target="_blank">
    <img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg" alt="License: Apache 2.0"/>
  </a>
</p>
<blockquote>
  <em>
    Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an 
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  </em>
</blockquote>
