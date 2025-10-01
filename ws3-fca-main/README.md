# @kashif-raza/fca

Facebook Chat API protected and deployed by **KASHIF Raza**.

## Usage:

```js
const login = require("@kashif-raza/fca");

// Example usage
const fs = require("fs");

let credentials;
try {
  credentials = { appState: JSON.parse(fs.readFileSync("appstate.json", "utf8")) };
} catch (err) {
  console.error("❌ appstate.json is missing or malformed.", err);
  process.exit(1);
}

console.log("Logging in...");

login(credentials, {
  online: true,
  updatePresence: true,
  selfListen: false,
  randomUserAgent: false
}, async (err, api) => {
  if (err) return console.error("LOGIN ERROR:", err);

  console.log(`✅ Logged in as: ${api.getCurrentUserID()}`);

  api.listenMqtt(async (err, event) => {
    if (err || !event.body || event.type !== "message") return;

    const prefix = "/";
    if (!event.body.startsWith(prefix)) return;

    const args = event.body.slice(prefix.length).trim().split(/ +/);
    const commandName = args.shift().toLowerCase();

    if (commandName === "hello") {
      api.sendMessageMqtt("Hello! This is @kashif-raza/fca package!", event.threadID);
    }
  });
});
```

## Installation

```bash
npm install @kashif-raza/fca
```

## Features

* 🔐 **Precise Login Mechanism**
* 💬 **Real-time Messaging**
* 📝 **Message Editing**
* ✍️ **Typing Indicators**
* ✅ **Message Status Handling**
* 📂 **Thread Management**
* 👤 **User Info Retrieval**
* 🖼️ **Sticker API**
* 💬 **Post Interaction**
* ➕ **Follow/Unfollow Users**
* 🌐 **Proxy Support**
* 🧱 **Modular Architecture**
* 🛡️ **Robust Error Handling**

## License

**MIT** – Protected and deployed by KASHIF Raza.