# 🏅 Badge System for Profile Page
This project implements a simple client-side badge system for a profile page. Users can earn and display achievement badges for completing courses. The badges are stored in the browser using `localStorage`.

## ✨ Features
- Displays a grid of available course badges
- Earned badges appear in color
- Locked badges appear in grayscale
- Badges persist between sessions via `localStorage`
- Easy to integrate into existing web profiles

## 📂 File Structure
index.html # HTML structure for the badge section
styles.css # CSS styles for the badge grid
script.js # JavaScript logic to render and award badges
images/
├─ html.png
├─ css.png
└─ js.png # Badge icons

## 🚀 How It Works
1. The `availableBadges` array lists all badge options.
2. When a course is completed, `awardBadge(courseId)` is called to unlock the corresponding badge.
3. Badges are saved in `localStorage` and displayed dynamically with `renderBadges()`.

## 🛠 Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/badge-system.git
Open index.html in your browser.
Complete a course by calling the function in the browser console:
completeCourse("html101");

🧪 Demo
You can simulate course completion by calling:
js
Copy
Edit
completeCourse("css101");
This will unlock the "CSS Stylist" badge.

🎨 Customization
Add new badges to the availableBadges array in the script.
Include new icons in the images/ folder.
Adjust styles in .badge-grid and .badge to change layout or effects.

   💡 Example Badge Object
js
Copy
Edit
{
  id: "js101",
  name: "JS Explorer",
  image: "js.png"
}

📌 Requirements
No external dependencies
Modern browser with localStorage support

🤝 Contributing
Feel free to fork the project, open issues, or submit pull requests!

