# MWAD_EX05_image-carousel-in-react
## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM:
# App.jsx:
```
import React, { useState, useEffect } from "react";
import "./App.css";

// 🌅 Morning, ☀️ Afternoon, 🌇 Evening, 🌙 Night
const images = [
  {
    url: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e", // Morning
    label: "Morning View 🌅",
  },
  {
    url: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=1000&q=70", // Afternoon
    label: "Afternoon View ☀️",
  },
  {
    url: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=1000&q=60&blend=000000&sat=-100", // Evening
    label: "Evening View 🌇",
  },
  {
    url: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=1000&q=50&blend=0b0b3b&sat=-90", // Night
    label: "Night View 🌙",
  },
];

function App() {
  const [current, setCurrent] = useState(0);

  // Auto-slide every 3 seconds
  useEffect(() => {
    const timer = setInterval(() => {
      setCurrent((prev) => (prev === images.length - 1 ? 0 : prev + 1));
    }, 3000);
    return () => clearInterval(timer);
  }, []);

  const prevSlide = () => {
    setCurrent((prev) => (prev === 0 ? images.length - 1 : prev - 1));
  };

  const nextSlide = () => {
    setCurrent((prev) => (prev === images.length - 1 ? 0 : prev + 1));
  };

  return (
    <div className="app">
      <h2>🏖️ Beach Views — Morning to Night</h2>

      <div className="carousel">
        {images.map((img, index) => (
          <div
            key={index}
            className={index === current ? "slide active" : "slide"}
          >
            <img src={img.url} alt={img.label} />
            <div className="caption">{img.label}</div>
          </div>
        ))}

        <button className="nav left" onClick={prevSlide}>
          ❮
        </button>
        <button className="nav right" onClick={nextSlide}>
          ❯
        </button>
      </div>

      <footer>
        <p>
          © {new Date().getFullYear()} T.DANUSH REEDY (212223040029) — All rights
          reserved.
        </p>
      </footer>
    </div>
  );
}

export default App;
```
# App.css:
```
.app {
  text-align: center;
  font-family: Arial, sans-serif;
  background: linear-gradient(to bottom, #b3ecff, #ffffff);
  min-height: 100vh;
  padding-bottom: 30px;
}

h2 {
  margin-top: 30px;
  color: #0077b6;
}

/* Carousel container */
.carousel {
  position: relative;
  width: 700px;
  height: 400px;
  margin: 40px auto;
  overflow: hidden;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
}

/* Each slide */
.slide {
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 1s ease-in-out;
  display: flex;
  align-items: flex-end;
  justify-content: center;
}

.slide img {
  width: 100%;
  height: 100%;
  object-fit: contain; /* shows full image */
  background-color: #000;
  border-radius: 15px;
}

.slide.active {
  opacity: 1;
  z-index: 1;
}

/* Caption */
.caption {
  position: absolute;
  bottom: 15px;
  background: rgba(0, 0, 0, 0.5);
  color: #fff;
  padding: 8px 15px;
  border-radius: 8px;
  font-size: 18px;
}

/* Navigation buttons */
.nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  padding: 10px 15px;
  cursor: pointer;
  font-size: 24px;
  border-radius: 50%;
}

.nav.left {
  left: 10px;
}

.nav.right {
  right: 10px;
}

/* Footer */
footer {
  margin-top: 30px;
  color: #555;
  font-size: 14px;
}
```
## OUTPUT:
<img width="908" height="1015" alt="image" src="https://github.com/user-attachments/assets/06eb719a-b040-4d98-b57c-306540a0b258" />
<img width="895" height="1012" alt="image" src="https://github.com/user-attachments/assets/e4e3a48f-3ad2-4b6d-8140-5a3055464b61" />
<img width="895" height="1018" alt="image" src="https://github.com/user-attachments/assets/42783664-dbcb-4e47-bc9b-c091e836a39f" />
<img width="925" height="1020" alt="Screenshot 2025-10-16 110614" src="https://github.com/user-attachments/assets/12d91fc9-4b95-4459-8a3c-023e41f760ea" />





## RESULT
The program for creating Image Carousel using React is executed successfully.
