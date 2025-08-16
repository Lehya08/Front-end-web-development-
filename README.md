1)🎓 Certificate Generator
A simple web-based Certificate Generator that allows users to enter their name and download a certificate as an image.

🚀 Features
Enter your name in a text field.
See your name rendered on a certificate canvas.
Download the generated certificate as an image.

📂 Project Structure
index.html        → Main HTML file  
style.css         → Stylesheet (optional)  
script.js         → JavaScript for canvas and download  

🛠️ How It Works
User enters their name in the input field.
JavaScript writes the name onto the <canvas>.
A download button allows the user to save the certificate as an image (.png).

📦 Installation & Usage
Clone the repository and open the index.html in your browser.
git clone https://github.com/your-username/certificate-generator.git
cd certificate-generator
Then open index.html in any browser.

📜 Example Code
<canvas id="canvas" height="350px" width="500px"></canvas>
<a href="#" id="download-btn">Download</a>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");
document.getElementById("download-btn").addEventListener("click", () => {
  const link = document.createElement("a");
  link.download = "certificate.png";
  link.href = canvas.toDataURL();
  link.click();
});
🖌️ Customization
Update the certificate background by loading an image on the canvas.
Change fonts, colors, or position of the text.
Add more input fields (date, course name, etc.).

🤝 Contributing
Feel free to fork this repo and submit pull requests with improvements!



2)🏅 Profile Page Badge System
A simple Badge Display System for profile pages that allows users to earn and display badges when completing courses.

🚀 Features
🎨 Grid-based responsive badge layout
🔒 Locked badges shown in grayscale until earned
📦 LocalStorage support to save earned badges
🏆 Earn badges by completing courses

📂 Project Structure
index.html   → Profile page with badge section  
style.css    → Badge grid and styling  
script.js    → Logic for awarding & rendering badges  

🛠️ How It Works
Available badges are defined in JavaScript.
When a user completes a course, awardBadge(courseId) saves it to localStorage.
renderBadges() updates the UI to show earned badges in color and locked ones in grayscale.

📜 Example Code
HTML
<div id="badge-section">
  <h2>My Achievements</h2>
  <div id="badge-container" class="badge-grid"></div>
</div>

CSS
.badge-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));
  gap: 16px;
  padding: 10px;
}
.badge {
  text-align: center;
  border-radius: 10px;
  transition: transform 0.3s;
}
.badge.locked img {
  filter: grayscale(100%);
  opacity: 0.5;
}
.badge img {
  width: 60px;
  height: 60px;
}

JavaScript
const availableBadges = [
  { id: "html101", name: "HTML Beginner", image: "html.png" },
  { id: "css101", name: "CSS Stylist", image: "css.png" },
  { id: "js101", name: "JS Explorer", image: "js.png" },
];
function renderBadges() {
  const badges = JSON.parse(localStorage.getItem("userBadges")) || {};
  const container = document.getElementById("badge-container");
  container.innerHTML = '';
  availableBadges.forEach(badge => {
    const isEarned = badges[badge.id];
    const badgeDiv = document.createElement("div");
    badgeDiv.className = `badge ${isEarned ? '' : 'locked'}`;
    badgeDiv.innerHTML = `
      <img src="${badge.image}" alt="${badge.name}" />
      <div>${badge.name}</div>
    `;
    container.appendChild(badgeDiv);
  });
}
function awardBadge(courseId) {
  const badges = JSON.parse(localStorage.getItem("userBadges")) || {};
  badges[courseId] = true;
  localStorage.setItem("userBadges", JSON.stringify(badges));
  renderBadges();
  }
// Example: Award a badge when a course is completed
function completeCourse(courseId) {
  awardBadge(courseId);
}
// Call on page load
renderBadges();

📦 Usage
Clone the repo:
git clone https://github.com/your-username/profile-badge-system.git
cd profile-badge-system
Open index.html in your browser.
Call completeCourse("html101") in console (or from your course logic) to unlock badges.

🖌️ Customization
Add more badges by editing the availableBadges array.
Replace html.png, css.png, etc. with your own images.
Customize styles for hover effects or animations.

🤝 Contributing
Pull requests are welcome! If you’d like to add features (like animations, sharing badges, etc.), feel free to contribute.



3)📚 Course Browser
A React-based Course Browser that lets users search and filter courses by keywords and tags. Built with React + TailwindCSS for a clean, responsive UI.

🚀 Features
🔍 Search courses by title or description
🏷️ Filter by tags (Programming, Design, Marketing, etc.)
⚡ Responsive grid layout for course cards
🎨 Clean UI with TailwindCSS styling

📂 Project Structure
src/
 ├── CourseBrowser.jsx   # Main component
 ├── index.js            # Entry point
 └── App.js              # App wrapper

🛠️ How It Works
Users can type into the search bar to filter courses by name/description.
Users can click on tags to show only courses matching those tags.
A combination of search + tags refines the results further.
If no course matches, a message "No courses found." is displayed.

📜 Example Code
Component: CourseBrowser.jsx
import React, { useState } from "react";
const courses = [
  { id: 1, title: "Introduction to Programming", description: "Learn basic coding with Python.", tags: ["Programming"] },
  { id: 2, title: "Graphic Design Basics", description: "Explore color theory and typography.", tags: ["Design"] },
  { id: 3, title: "Digital Marketing 101", description: "Understand social media and SEO.", tags: ["Marketing"] },
  { id: 4, title: "Advanced React", description: "Hooks, context, and performance tuning.", tags: ["Programming"] },
];
const tags = ["Programming", "Design", "Marketing"];
export default function CourseBrowser() {
  const [searchTerm, setSearchTerm] = useState("");
  const [activeTags, setActiveTags] = useState([]);
  const toggleTag = (tag) => {
    setActiveTags((prev) =>
      prev.includes(tag) ? prev.filter((t) => t !== tag) : [...prev, tag]
    );
  };
  const filteredCourses = courses.filter((course) => {
    const matchesSearch =
      course.title.toLowerCase().includes(searchTerm.toLowerCase()) ||
      course.description.toLowerCase().includes(searchTerm.toLowerCase());
    const matchesTags =
      activeTags.length === 0 ||
      course.tags.some((tag) => activeTags.includes(tag));
    return matchesSearch && matchesTags;
  });
  return (
    <div className="p-6 max-w-4xl mx-auto">
      <h1 className="text-2xl font-bold mb-4">Discover Courses</h1>
      <input
        type="text"
        placeholder="Search courses..."
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
        className="w-full p-2 border rounded mb-4"
      />
      <div className="flex gap-2 mb-6 flex-wrap">
        {tags.map((tag) => (
          <button
            key={tag}
            onClick={() => toggleTag(tag)}
            className={`px-3 py-1 rounded-full border ${
              activeTags.includes(tag)
                ? "bg-blue-600 text-white border-blue-600"
                : "bg-white text-gray-800 border-gray-300"
            }`}
          >
            {tag}
          </button>
        ))}
      </div>
      <div className="grid md:grid-cols-2 gap-4">
        {filteredCourses.length > 0 ? (
          filteredCourses.map((course) => (
            <div
              key={course.id}
              className="border p-4 rounded-lg shadow hover:shadow-md transition"
            >
              <h2 className="text-xl font-semibold mb-1">{course.title}</h2>
              <p className="text-gray-600 mb-2">{course.description}</p>
              <div className="flex gap-2 flex-wrap">
                {course.tags.map((tag) => (
                  <span
                    key={tag}
                    className="text-sm bg-gray-100 px-2 py-1 rounded-full"
                  >
                    {tag}
                  </span>
                ))}
              </div>
            </div>
          ))
        ) : (
          <p className="text-gray-500">No courses found.</p>
        )}
      </div>
    </div>
  );
}

📦 Installation & Usage
Clone the repo and install dependencies:
git clone https://github.com/your-username/course-browser.git
cd course-browser
npm install
npm start
This will start a development server at http://localhost:3000/.

🖌️ Customization
Add more courses inside the courses array.
Add new tags to the tags array.
Replace TailwindCSS with your own styling if desired.

🤝 Contributing
Pull requests are welcome! If you’d like to add features like:
Sorting (e.g., newest/oldest courses)
Pagination / infinite scroll
Backend integration (API)
Feel free to contribute 🚀



4)🎉 Course Completion Celebration
A fun and interactive webpage that celebrates course completion with confetti and a motivational message. Built with HTML, CSS, and JavaScript using the canvas-confetti library.

🚀 Features
✅ “Complete Course” button
🎊 Confetti animation for 4 seconds
🎉 Motivational message appears with fade-in effect
🎨 Modern, clean UI with hover effects

📂 Project Structure
index.html   → Main HTML file with inline CSS & JS

🛠️ How It Works
User clicks Complete Course button.
A celebratory message is shown:
🎉 Great Job! You've completed the course! 🎉
Confetti shoots from both sides of the screen for 4 seconds.

📜 Example Code
HTML & Button
<button class="complete-btn" onclick="celebrateCompletion()">Complete Course</button>
<div class="message" id="completionMessage">
  🎉 Great Job! You've completed the course! 🎉
</div>
JavaScript (Confetti Celebration)
function celebrateCompletion() {
  // Show motivational message
  const message = document.getElementById('completionMessage');
  message.classList.add('show');
  // Fire confetti for 4 seconds
  const duration = 4000;
  const end = Date.now() + duration;
  (function frame() {
    confetti({ particleCount: 3, angle: 60, spread: 55, origin: { x: 0 } });
    confetti({ particleCount: 3, angle: 120, spread: 55, origin: { x: 1 } });
    if (Date.now() < end) {
      requestAnimationFrame(frame);
    }
  })();
}
CSS (Styling)
body {
  font-family: 'Segoe UI', sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
  background: #f0f4f8;
}
.message {
  font-size: 2rem;
  color: #2e7d32;
  margin-top: 20px;
  opacity: 0;
  transition: opacity 0.5s ease-in;
}
.message.show {
  opacity: 1;
}
.complete-btn {
  padding: 12px 24px;
  font-size: 1rem;
  background: #1976d2;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s ease;
}
.complete-btn:hover {
  background: #1565c0;
}

📦 Usage
Clone this repo:
git clone https://github.com/your-username/course-completion-celebration.git
cd course-completion-celebration
Open index.html in your browser.
Click the Complete Course button to celebrate 🎊

🖌️ Customization
Change confetti colors, speed, and spread in JS.
Update motivational message text and styling.
Integrate with an LMS (Learning Management System) to auto-trigger celebration on course completion.

🤝 Contributing
Pull requests are welcome! Feel free to add:
More confetti effects
Sounds (cheering, applause)
Dark mode UI



5)📥 Offline Course Downloader (PWA + IndexedDB)
A Progressive Web App (PWA) feature that lets users download courses (text + images) for offline access. Uses IndexedDB to store data locally and Workbox for service worker caching.

🚀 Features
📦 Download entire courses (title, content, images) to IndexedDB
🌐 NetworkFirst strategy for API data (uses cache when offline)
🖼️ CacheFirst strategy for images (loads faster offline)
✅ Shows “Available offline” badge on courses
🔌 PWA ready with Service Worker integration

📂 Project Structure
src/
 ├── CourseCard.jsx        # React component showing offline status
 ├── offline.js            # IndexedDB functions
 ├── sw.js                 # Service Worker with Workbox routes
 └── api/                  # Backend API serving course data

🛠️ How It Works
When a user clicks download, the course data is fetched and saved in IndexedDB.
Images are downloaded as blobs and stored locally.
Service Worker (sw.js) uses:
NetworkFirst → for course API data
CacheFirst → for images
The CourseCard component checks if a course is offline and displays a ✅ badge.

📜 Example Code
Save course offline
async function downloadCourseContent(courseId) {
  const courseData = await fetch(`/api/course/${courseId}`).then(res => res.json());
  // Save text + images to IndexedDB
  const db = await openDB('OfflineCourses', 1, {
    upgrade(db) {
      if (!db.objectStoreNames.contains('courses')) {
        db.createObjectStore('courses', { keyPath: 'id' });
      }
    },
  });
  const imageBlobs = await Promise.all(courseData.images.map(async (url) => {
    const res = await fetch(url);
    const blob = await res.blob();
    return { url, blob };
  }));
  await db.put('courses', {
    id: courseId,
    title: courseData.title,
    content: courseData.content,
    images: imageBlobs,
    downloadedAt: new Date(),
  });
}
Check if course is offline
async function isCourseOffline(courseId) {
  const db = await openDB('OfflineCourses', 1);
  const course = await db.get('courses', courseId);
  return !!course;
}
React Course Card
function CourseCard({ course }) {
  const [isOffline, setIsOffline] = useState(false);
  useEffect(() => {
    isCourseOffline(course.id).then(setIsOffline);
  }, [course.id]);
  return (
    <div className="course-card">
      <h3>{course.title}</h3>
      {isOffline && <span className="badge">✅ Available offline</span>}
    </div>
  );
}
Service Worker (sw.js)
workbox.routing.registerRoute(
  ({url}) => url.pathname.startsWith('/api/course'),
  new workbox.strategies.NetworkFirst({ cacheName: 'api-cache' })
);
workbox.routing.registerRoute(
  ({request}) => request.destination === 'image',
  new workbox.strategies.CacheFirst({ cacheName: 'image-cache' })
);

📦 Installation & Usage
Clone this repo:
git clone https://github.com/your-username/offline-course-pwa.git
cd offline-course-pwa
npm install
npm start
Open http://localhost:3000/ in your browser.
Enable Service Workers in dev tools to test offline mode.
Click Download Course → then disconnect internet → course still loads ✅

🖌️ Customization
Add more fields (videos, quizzes) to IndexedDB schema.
Use StaleWhileRevalidate instead of NetworkFirst for faster load.
Show progress bar while downloading large courses.

🤝 Contributing
Contributions welcome! You can help by adding:
Background sync for downloads
Notifications when course is saved offline
Offline search & filtering
