# 🌐 Sports Leagues (Vue 3 + Vite)
A modern web app built with **Vue 3 (Composition API)** and **Vite**, designed to display sports leagues using the open [TheSportsDB API](https://www.thesportsdb.com).  
Users can search for leagues, filter them by sport type, and view each league’s official badge in a modal window — with caching via `localStorage` for faster loading.

---

## 🚀 Features
- 🔍 **Search leagues by name**
- 🏆 **Filter by sport type (Soccer, Motorsport, Basketball, etc.)**
- 🖼️ **View league badge in a modal window**
- 💾 **Cache league badges in `localStorage` to reduce API calls**
- ⚡ **Reactive filtering and instant updates**
- 🧱 **Component-based Vue 3 architecture**

---

## 🧩 Tech Stack
- **Vue 3 (Composition API + `<script setup>`)**
- **Vite**
- **Axios** — for API requests  
- **TheSportsDB API** — for league data  
- **LocalStorage** — for badge caching  
- **CSS3** — for animations and responsive design  

---

## 📁 Project Structure
src/
 ├── components/
 │   ├── GetData/               # Core logic: fetching, filtering, and caching data
 │   │   └── GetData.vue
 │   ├── LeagueList/            # Displays all leagues as clickable cards
 │   │   └── LeagueList.vue
 │   ├── LeagueBadges/          # Modal popup for showing league badge
 │   │   └── LeagueBadges.vue
 │   ├── SearchBox/             # Search input field for league names
 │   │   └── SearchBox.vue
 │   └── SelectLeague/          # Dropdown to filter by sport type
 │       └── SelectLeague.vue
 │
 ├── App.vue                    # Root component combining everything
 ├── main.js                    # Vue app initialization
 ├── index.html
 ├── package.json
 └── vite.config.js

---

## ⚙️ Installation & Setup
1️⃣ **Clone the repository**  
git clone https://github.com/yourusername/sports-leagues.git  
cd sports-leagues-viewer  

2️⃣ **Install dependencies**  
npm install  

3️⃣ **Start the development server**  
npm run dev  

App will be available at:  
👉 **http://localhost:5173**

---

## 🌐 API Endpoints
All data is provided by **TheSportsDB API**  
- All leagues → https://www.thesportsdb.com/api/v1/json/3/all_leagues.php  
- League badge → https://www.thesportsdb.com/api/v1/json/3/lookupleague.php?id={idLeague}

---

## 🧠 Application Logic
🟢 **GetData.vue**
- Fetches leagues from API using axios on mount  
- Handles `getBadges(idLeague)`  
- Checks `localStorage` cache before API call  
- Passes data to `LeagueList`, `SearchBox`, `SelectLeague`, and `LeagueBadges`  

🔵 **LeagueList.vue**
- Displays leagues in cards  
- Emits `select-league` event when clicked  

🟣 **LeagueBadges.vue**
- Displays league badge inside a modal  
- Supports fade + slide animation  
- Closes on outside click, ESC, or close button  
- Disables page scroll while open  

🟡 **SearchBox.vue** and **SelectLeague.vue**
- Controlled input components for filtering  
- Update search and sport filters reactively  

---

## 🖼️ Example User Flow
1. App loads all leagues  
2. User searches by keyword  
3. List filters in real-time  
4. Click a league card → modal opens with badge  
5. Badge cached for faster reload  

---

## 🧩 Future Improvements
- Add loading spinner  
- Display league descriptions  
- Add favorites with persistence  
- Dark/light theme toggle  

---

## 👨‍💻 Author
**Andranik Kocharyan**  
📍 Yerevan, Armenia  
💼 Frontend 
 

---

## 📜 License
This project is licensed under the **MIT License** — free to use, modify, and distribute.

---

⭐ If you like this project — give it a **Star** on GitHub!
