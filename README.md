# Xtream Codes VOD & Live TV Playlist

A lightweight Xtream Codes API implementation that provides access to VOD (Movies/Series) and Live TV content through a Cloudflare Worker, compatible with any Xtream Codes player.

---

## 🖼️ Screenshots

<p align="center">
  <img src="https://github.com/dtankdempsey2/xc-vod-playlist/blob/main/images/live.PNG" alt="Live" width="30%" style="margin-right: 5px;"/>
  <img src="https://github.com/dtankdempsey2/xc-vod-playlist/blob/main/images/movies.PNG" alt="Movies" width="30%" style="margin-right: 5px;"/>
  <img src="https://github.com/dtankdempsey2/xc-vod-playlist/blob/main/images/series.PNG" alt="Series" width="30%"/>
</p>

---

## 📺 Content Sources

> All credit goes to Discord users **BigData** *(VOD Content)* and **Drewski24** *(LiveTV)* for providing the content this script indexes.

### 🎬 VOD Content (Movies & Series)
The VOD catalog is indexed from [**a.111477.xyz**](https://a.111477.xyz), providing a comprehensive collection of movies and TV series.

For questions, issues, or information regarding VOD content, please join their Discord community:  
**Discord:** [https://discord.gg/qt2JC64E](https://discord.gg/qt2JC64E)

### 📡 Live TV Content
Live TV functionality is powered by [**DrewLive**](https://github.com/Drewski2423/DrewLive), offering a wide range of live television channels.

For Live TV support and discussions:  
**Discord:** [https://discord.gg/bfzxKzkc](https://discord.gg/bfzxKzkc)


---

## 🚀 Quick Deploy

Deploy your own instance in under **2 minutes** using **Cloudflare's free tier** — perfect for personal or small-scale use.

> ⚠️ **Requires a free [GitHub account](https://github.com/signup)** to clone and deploy the project.

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/dtankdempsey2/xc-vod-playlist/tree/main/cloudflare)

### ✨ Why Cloudflare Workers?

- **100% Free** – Includes 100,000 requests/day on the free tier  
- **Global CDN** – Runs on Cloudflare’s worldwide edge network  
- **No Server Needed** – No hosting, backend, or maintenance required  
- **Instant Deploy** – Click the button, sign in, and go live in seconds  

---

## 🛠️ Option 2: Manual Deployment (No GitHub Required)

### 📺 Setup Video

https://github.com/user-attachments/assets/6da1cb9b-79d6-45ba-87ba-8ddb8867fe0a

If you prefer to set it up manually, follow these steps:

1. **Sign up for Cloudflare**  
   Create a free account here: [https://dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up)

2. **Create a New Worker**  
   - Log into the Cloudflare dashboard  
   - Navigate to **Workers & Pages → Create Worker**  
   - Name your Worker (e.g., `xtream-codes-vod`)

3. **Copy the Code**  
   Open this file in the repository:  
   👉 [`/cloudflare/worker.js`](https://github.com/dtankdempsey2/xc-vod-playlist/blob/main/cloudflare/worker.js)

4. **Paste into the Cloudflare Editor**  
   Replace the default Worker code with the contents of `worker.js`

5. **Save and Deploy**  
   Click **Save and Deploy**, then test your Worker URL, e.g.: https://your-worker-name.username.workers.dev

### ✅ That’s It!
Your personal Xtream Codes worker is now live on Cloudflare’s global edge network.

---

## 📋 Setup Instructions

### Step 1: Deploy to Cloudflare
1. Click the "Deploy to Cloudflare" button above
2. Sign up for a free Cloudflare account (or sign in if you have one)
3. Authorize the deployment
4. Your worker will be deployed automatically with a URL like: `https://your-worker-name.your-subdomain.workers.dev`

### Step 2: Connect Your Xtream Codes Player

Add your new server to any Xtream Codes compatible player:

- **Server URL**: `https://your-worker-name.your-subdomain.workers.dev`
- **Username**: Any value (see File Size Options below)
- **Password**: Any value

### 📱 Compatible Players
- TiviMate
- IPTV Smarters Pro
- Perfect Player
- Xtream IPTV Player
- And many more!

---

## ⚙️ File Size Management

By default, the script automatically selects the **smallest available file** to ensure smooth playback. However, you can customize this behavior using the username field:

### 🎯 Default Behavior
- **Username**: `anything`
- **Result**: Selects the smallest file available

### 🎮 Custom File Size Preference
- **Username**: `filesize:4`
- **Result**: Prefers files ≤4GB, but will play larger files if that's all that's available

### 📊 Examples
| Username | Target Size | Behavior |
|----------|------------|----------|
| `filesize:2` | ≤2GB | Targets smaller files for mobile/limited bandwidth |
| `filesize:5.5` | ≤5.5GB | Balanced quality and performance |
| `filesize:10` | ≤10GB | Higher quality for fast connections |

> **⚠️ Note**: Higher file sizes may cause buffering or stuttering during peak traffic periods on the a.111477.xyz servers. For best performance, stick with smaller file sizes.

---

## 🧪 Test Server

Want to try it out first? Test the functionality with our demo instance:

**Test Server URL**: `https://xtream-vod.data-search.workers.dev/`

👤 **Username/Password**: Anything (enter any values)

> ⚠️ **Important**: This test server is on the free tier and will stop working once daily limits are reached.  
> For reliable service, please deploy your own instance using the button above.

---

## 🔧 API Endpoints

The worker implements the standard Xtream Codes API:

### 📡 Player API
```
/player_api.php
```
- `action=get_vod_streams` - List all movies
- `action=get_vod_info&vod_id=X` - Get movie details
- `action=get_series` - List all TV series
- `action=get_series_info&series_id=X` - Get series details
- `action=get_live_streams` - List live TV channels
- `action=get_live_categories` - List live TV categories

### 📝 Playlist
```
/get.php?type=m3u_plus
```
M3U playlist with all content

### 📅 EPG
```
/xmltv.php
```
Electronic Program Guide for live TV

### ▶️ Direct Streaming
- `/movie/{username}/{password}/{stream_id}` - Direct movie playback
- `/series/{username}/{password}/{episode_id}.{ext}` - Direct episode playback

---

## 🔄 Coming Soon

| Feature | Timeline | Description |
|---------|----------|-------------|
| **Node.js Version** | 1-2 days | Run on any VPS or local machine |
| **Docker Container** | 1-2 days | One-command deployment with Docker |

---

## 📊 Technical Details

- **VOD Metadata**: Cached from GitHub JSON files for instant loading
- **File Resolution**: On-demand file selection from a.111477.xyz
- **Live TV**: Real-time M3U8 playlist parsing
- **Caching**: Intelligent caching to minimize API calls
- **Performance**: Runs on Cloudflare's global edge network

---

## 🤝 Contributing

Feel free to open issues or submit pull requests. For content-specific issues:

| Issue Type | Support Channel |
|------------|-----------------|
| **VOD Issues** | [a.111477.xyz Discord](https://discord.gg/qt2JC64E) |
| **Live TV Issues** | [DrewLive Discord](https://discord.gg/bfzxKzkc) |
| **Script Issues** | Open an issue on this repository |

---

## 📄 License

This project provides an API interface and does not host any content. All content is provided by third-party sources.

---

> **Disclaimer**: This script is a technical implementation of the Xtream Codes API protocol. Users are responsible for ensuring they have appropriate permissions for any content they access.
