# 🏆 EventEngine

**EventEngine** is an event and minigame core designed for high-traffic Minecraft server networks. Built on top of a robust **Finite State Machine (FSM)** architecture, it allows network staff, event hosts, and media creators to seamlessly browse, create, and manage live events and minigames through interactive GUI interfaces.

---

## ✨ Key Features

* **⚙️ Finite State Machine (FSM) Lifecycle**: Strict state separation (`LOBBY` ➔ `STARTING` ➔ `INGAME` ➔ `ENDING`) ensuring thread safety and clear logic progression.
* **📱 Interactive GUI Management System**:
  * `/events`: Displays active/running events with live player counts and status badges.
  * **Host & Creator Button**: Integrated emerald block trigger allowing authorized staff and media roles to initiate new event lobbies.
* **🛡️ Smart Protection Listeners**: Automatic protection against block placement/destruction, fall damage, and non-gameplay interactions outside active match states.
* **🔑 Role & Permission Integration**: Tailored command workflow specifically designed for Media, Content Creators, and Network Staff (`coreminigame.events` and `coreminigame.host`).
* **⚡ Paper API Optimized**: Designed using Modern Java 17+ and Kyori Adventure components for high-TPS performance under heavy load.

---

## 🏗️ Architecture & Finite State Machine

The core lifecycle of every event managed by `EventEngine` is controlled through an isolated state pattern:

```text
       ┌──────────┐
       │  LOBBY   │  ◄── Event created via GUI / Staff Host
       └────┬─────┘
            │  /starts command or timer finish
            ▼
       ┌──────────┐
       │ STARTING │  ◄── Countdown phase & spawn preparation
       └────┬─────┘
            │  Timer finishes
            ▼
       ┌──────────┐
       │  INGAME  │  ◄── Game mechanics, build/PvP enabled
       └────┬─────┘
            │  Match end condition met
            ▼
       ┌──────────┐
       │  ENDING  │  ◄── Winner declaration & cleanup
       └──────────┘
