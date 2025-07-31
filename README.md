2)# 🏅 Badge System for Profile Page
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

3)📚 React Course Browser
A responsive React component that lets users browse and filter a list of courses using a search bar and tag-based filtering. Built with Tailwind CSS for rapid styling and a modern UI.

✨ Features
🔍 Live search by title or description
🏷️ Clickable tags for filtering by category (e.g., Programming, Design)
⚡ Responsive layout using CSS Grid and Flexbox
🎨 Styled with Tailwind CSS
💡 Clean, beginner-friendly logic using React hooks (useState)

🖥️ Preview
Users can:
Type keywords to filter courses.
Click on tags to refine results.
Combine both filters seamlessly.

📁 File Structure
css
Copy
Edit
src/
└── components/
    └── CourseBrowser.jsx

🚀 Getting Started
1. Install Tailwind CSS (if not already installed)
Use the Tailwind CSS installation guide if you’re using Create React App or Vite.

2. Import the Component
jsx
Copy
Edit
import CourseBrowser from './components/CourseBrowser';

function App() {
  return (
    <div>
      <CourseBrowser />
    </div>
  );
}
3. Run Your Project
bash
Copy
Edit
npm install
npm run dev   # or npm start (for CRA)

🧠 How It Works
searchTerm: Filters courses by title or description.

activeTags: Stores the selected tags.

The filteredCourses array combines both filters to show only matching results.

🔧 Customization
Add more courses
Modify the courses array with your own course data.

Add more tags
Update the tags array and ensure each course includes relevant tags.

📦 Dependencies
React
Tailwind CSS
No additional libraries are required.

🙌 Acknowledgements
Thanks to the React and Tailwind CSS communities for their fantastic tooling.

4)🎓 Course Completion Celebration Page
A simple, elegant web page that lets users celebrate course completion with a motivational message and colorful confetti animation. Built with HTML, CSS, and the Canvas Confetti JavaScript library.

✨ Features
✅ Clean and responsive design
🎉 Confetti burst animation using canvas-confetti
💬 Motivational message on completion
🎯 Zero dependencies other than CDN (no build tools needed)

📸 Preview
Click the “Complete Course” button to:
Show a motivational message
Trigger a celebratory confetti animation for 4 seconds

🚀 Live Demo
You can try the page by opening index.html in your browser.

📁 File Structure
pgsql
Copy
Edit
project-root/
├── index.html
└── README.md

🔧 How It Works
When the user clicks Complete Course, the function celebrateCompletion() is triggered.
It:
Reveals a hidden congratulatory message using a smooth fade-in effect.
Launches confetti bursts from both sides using the Canvas Confetti library.
The confetti continues for 4 seconds using requestAnimationFrame.

📦 Dependencies
Only one library via CDN:
html
Copy
Edit
<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
No setup or installation required.

🛠️ Customization
🔧 Message text: Edit the content inside <div id="completionMessage">...</div>
🎨 Colors and fonts: Update the CSS in the <style> tag
⏱️ Duration: Modify const duration = 4000; in the JS block
💥 Particle count or spread: Adjust values inside confetti({...})

🙌 Acknowledgements
canvas-confetti by @catdad
A lightweight, zero-dependency confetti library for the web.

5)📦 Offline Course Downloader (React + IndexedDB + Workbox)
A React-based solution that allows users to download course content (text + images) for offline access using IndexedDB and Workbox-powered service workers.

✨ Features
🔄 Download full course content and media via downloadCourseContent(courseId)
💾 Store HTML/text and images in IndexedDB (via idb)
✅ Detect whether a course is available offline
🧠 View cached content even when offline
📡 Service worker integration using Workbox
NetworkFirst strategy for API
CacheFirst strategy for images

📁 File Structure
bash
Copy
Edit
src/
├── components/
│   └── CourseCard.jsx
├── utils/
│   └── offlineManager.js
└── sw.js               # Service Worker with Workbox

🚀 How It Works
🧠 1. Downloading Course Data
js
Copy
Edit
await downloadCourseContent(courseId);
Fetches course data from /api/course/:id
Downloads associated images as Blobs
Saves the entire content to IndexedDB under the 'OfflineCourses' database

🏷️ 2. CourseCard UI
jsx
Copy
Edit
<CourseCard course={course} />
Dynamically shows a ✅ “Available offline” badge if content exists in IndexedDB
Uses useEffect() to check offline status on render

🔐 3. IndexedDB Schema (via idb)
js
Copy
Edit
{
  id: courseId,
  title: string,
  content: string, // text/HTML
  images: [{ url, blob }],
  downloadedAt: Date
}

🛡️ Service Worker (Workbox)
js
Copy
Edit
// Cache API data
workbox.routing.registerRoute(
  ({url}) => url.pathname.startsWith('/api/course'),
  new workbox.strategies.NetworkFirst({
    cacheName: 'api-cache',
  })
);

// Cache images
workbox.routing.registerRoute(
  ({request}) => request.destination === 'image',
  new workbox.strategies.CacheFirst({
    cacheName: 'image-cache',
  })
);

🧩 Dependencies
idb – Promisified IndexedDB
Workbox – Google’s service worker toolkit
React (for UI integration)

📦 Installation & Setup
1. Install idb and Workbox
bash
Copy
Edit
npm install idb workbox-core workbox-routing workbox-strategies
2. Register Your Service Worker
In your index.js:
js
Copy
Edit
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/sw.js');
  });
}
3. Add Workbox to sw.js
You can bundle with workbox-cli or serve the raw script via CDN for quick prototyping.

🧪 Test Offline Mode
Visit a course while online and click Download.
Turn off your internet connection.
Reload the page or navigate to the course.
Offline content should still load, and badge should appear ✅.

🙌 Acknowledgements
idb by Jake Archibald
workbox









