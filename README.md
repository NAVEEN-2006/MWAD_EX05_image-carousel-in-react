## MWAD_EX05_image-carousel-in-react
## Date: 27-10-2025

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

## PROGRAM
~~~ jsx
import React, { useState } from "react";
import "./Carousel.css";

const images = [
  "https://cdn.thecollector.com/wp-content/uploads/2021/12/colosseum-world-wonder-national-geographic.jpg?width=1200&quality=100&dpr=2",
  "https://cdn.thecollector.com/wp-content/uploads/2020/08/great-wall-of-china-photo-smithsonian.jpg?width=1200&quality=100&dpr=2",
  "https://cdn.thecollector.com/wp-content/uploads/2021/12/the-taj-mahal-architectural-digest.jpg?width=1200&quality=100&dpr=2",
  "https://cdn.thecollector.com/wp-content/uploads/2021/12/christ-the-redeemer-statue-rio-1-scaled.jpg?width=1200&quality=100&dpr=2",
  "https://cdn.thecollector.com/wp-content/uploads/2021/12/machu-picchu-world-wonder.jpg?width=1095&quality=100&dpr=2",
  "https://cdn.thecollector.com/wp-content/uploads/2021/12/chichen-itza-image-1-1.jpg?width=1280&quality=100&dpr=2",
  "https://cdn.thecollector.com/wp-content/uploads/2022/12/petra-jordan-treasury-al-khazneh.jpg?width=1200&quality=100&dpr=2"
];

const Carousel = () => {
  const [currentIndex, setCurrentIndex] = useState(0);

  const nextSlide = () => {
    setCurrentIndex((prev) =>
      prev === images.length - 1 ? 0 : prev + 1
    );
  };

  const prevSlide = () => {
    setCurrentIndex((prev) =>
      prev === 0 ? images.length - 1 : prev - 1
    );
  };

  return (
    <div className="carousel-container">
      <div
        className="carousel-slider"
        style={{ transform: `translateX(-${currentIndex * 100}%)` }}
      >
        {images.map((img, index) => (
          <div className="carousel-slide" key={index}>
            <img src={img} alt={`Slide ${index}`} />
          </div>
        ))}
      </div>

      <button className="prev-btn" onClick={prevSlide}>
        ❮
      </button>
      <button className="next-btn" onClick={nextSlide}>
        ❯
      </button>

      <div className="carousel-dots">
        {images.map((_, index) => (
          <span
            key={index}
            className={index === currentIndex ? "dot active" : "dot"}
            onClick={() => setCurrentIndex(index)}
          ></span>
        ))}
      </div>
    </div>
  );
};

export default Carousel;
~~~
~~~css
.carousel-container {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.carousel-slider {
  display: flex;
  height: 100%;
  transition: transform 0.7s ease-in-out;
}

.carousel-slide {
  min-width: 100%;
  height: 100%;
}

.carousel-slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(0.9);
  transition: filter 0.5s ease-in-out, transform 0.5s ease-in-out;
}

.carousel-slide img:hover {
  filter: brightness(1);
  transform: scale(1.03);
}
.prev-btn,
.next-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.15);
  border: none;
  color: #fff;
  font-size: 2rem;
  padding: 12px 16px;
  cursor: pointer;
  border-radius: 50%;
  backdrop-filter: blur(8px);
  transition: background 0.3s ease, transform 0.2s ease;
  z-index: 10;
}

.prev-btn:hover,
.next-btn:hover {
  background: rgba(255, 255, 255, 0.35);
  transform: translateY(-50%) scale(1.1);
}

.prev-btn {
  left: 30px;
}

.next-btn {
  right: 30px;
}

/* Dots */
.carousel-dots {
  position: absolute;
  bottom: 25px;
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 8px;
}

.dot {
  height: 12px;
  width: 12px;
  background: rgba(255, 255, 255, 0.4);
  border-radius: 50%;
  transition: all 0.3s ease;
  cursor: pointer;
}

.dot.active {
  background: #fff;
  transform: scale(1.3);
  box-shadow: 0 0 8px #fff;
}

/* Responsive */
@media (max-width: 768px) {
  .prev-btn,
  .next-btn {
    font-size: 1.5rem;
    padding: 8px 12px;
  }

  .dot {
    height: 10px;
    width: 10px;
  }
}
~~~

## OUTPUT
<img width="1920" height="1141" alt="511814639-33fb73a4-1306-4b1d-98c8-c92faf561a35" src="https://github.com/user-attachments/assets/a7c6ab6d-b029-4e92-bc80-453573194b98" />

<img width="1919" height="1136" alt="image" src="https://github.com/user-attachments/assets/2b53aaa4-d845-4bb0-b3e7-317433e67b05" />
<img width="1919" height="1144" alt="image" src="https://github.com/user-attachments/assets/d22add9f-46ca-46f4-8d78-8619acc14dfd" />
<img width="1919" height="1142" alt="image" src="https://github.com/user-attachments/assets/53fa369a-6cec-48c1-9a85-bf084219408a" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
