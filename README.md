# HG Chat Monitor (v2.3.0)

**Author:** iongeneral, HeLLsGamers, HGDC  
**Compatibility:** SourceMod 1.12.x, SourceBans++ 1.7.0  
**Game Support:** Counter-Strike: Source (and compatible Source Engine titles)

---

## Overview
**HG Chat Monitor** is a comprehensive chat moderation system built for HeLLsGamers community servers.  
It automatically monitors player chat using a configurable regex word filter and enforces chat bans through SourceMod and SourceBans++ integration.

The system provides **automated**, **configurable**, and **database-synced** enforcement for toxic or inappropriate language, while maintaining full control and transparency for staff members.

---

## Core Features

### 1. Configurable Word Filtering
- Uses a **regex-based word filter** stored in **addons/sourcemod/configs/hgcm-filter.txt**.  
- Automatically detects and triggers bans when any listed word or expression is used in chat.  
- Filter can be updated live without requiring plugin reload.

### 2. Automated Chat Bans
- Offending players are automatically **gagged (sm_gag)** for a configurable duration (default 15 minutes).  
- A **public, aqua-colored message** is broadcast:  
  > **{playername} You are banned from chatting for 15 minutes for inappropriate language.**  
- After the timer expires, the player is **automatically ungagged (sm_ungag)**.  
- Upon expiration, another public message is displayed:  
  > **{playername} Your chat ban has expired. Read the Server Rules (type motd in chat) to avoid further chat bans.**

### 3. SourceBans++ Integration
- Full synchronization with **SourceBans++ v1.7.0**, logging all bans to the **sb_comms** table.  
- Chat bans appear in **SourceBans "Latest Added Comms Block"** section.  
- Compatible with both **temporary** and **permanent** chat bans.

### 4. Manual Admin Controls
Admins can issue chat bans manually using standard or permanent commands:
- sm_cban <target> 15-minute chat ban (configurable duration).  
- sm_pcban <target> permanent chat ban.  
- sm_unpcban <target> remove permanent chat ban.

Each command triggers the same styled public message using the configured prefix and color codes.

### 5. Configurable Settings (CVARs)
Auto-generated config:  
**addons/sourcemod/configs/hgcm-config.cfg**

| CVAR | Default | Description |
|------|----------|-------------|
| **hgcm_enable** | **1** | Enables or disables the plugin. |
| **hgcm_tag_prefix** | **[HGCM]** | Prefix tag used in plugin messages. |
| **hgcm_cban_duration** | **15** | Default chat ban duration in minutes. |
| **hgcm_cban_msg** | **"{playername} You are banned from chatting for 15 minutes for inappropriate language."** | Public message on ban. |
| **hgcm_cban_expire** | **"{playername} Your chat ban has expired. Read the Server Rules (type motd in chat) to avoid further chat bans."** | Message when ban expires. |
| **hgcm_cban_active_msg** | **"The server demigods have stolen your voice."** | Message shown when a banned player tries to chat. |
| **hgcm_use_sourcecomms** | **1** | Toggles use of SourceComms if present. |

### 6. Admin Menu Integration
- Adds **HG Chat Monitor** section to the **Admin Player Commands** menu.  
- Displays a list of active chat bans, with options to **view**, **extend**, or **remove**.  
- Simplifies staff moderation directly in-game.

### 7. Chat Ban History Command
- Command: **!cbh <playername>** or **sm_cban_history <playername>**  
- Prints console log of that players recent chat bans, including:
  - Player name  
  - Violating message  
  - Date/time  
  - SteamID  
  - Ban duration

---

## File Structure

| File | Purpose |
|------|----------|
| **hg_chat_monitor.sp** | Plugin source code |
| **hgcm-filter.txt** | Regex word filter list |
| **hgcm-config.cfg** | Auto-generated plugin configuration |
| **sb_comms** | SourceBans++ database table storing communication bans |

---

## Key Advantages
- **Regex filtering:** extremely flexible, supports complex pattern detection.  
- **Full SourceBans++ logging:** every ban is database-verified.  
- **Customizable messaging:** all public and player messages configurable via CVARs.  
- **Automatic un-gag system:** zero manual admin intervention for temporary bans.  
- **Compatible with SourceComms:** integrates seamlessly if already running.  
- **Built for HeLLsGamers standards:** production-ready, scalable, and transparent.
