# Exactspace Technologies – React Assignments

This repository includes the finished **Photo Gallery Assignment** developed as part of the React assignment for Exactspace Technologies.

---

## Photo Gallery – Project Overview

The Photo Gallery is a responsive React-based web application that loads and displays photographs from the Picsum API in an automatically updating feed. Users can browse images, view the corresponding author's name, and interact with a thumbs-up button to track likes for individual photographs.

The application is designed as a single-page interface with infinite scrolling, optimized image loading, and a layout that adapts to different screen sizes. Considerable attention has been given to matching the reference screenshots supplied with the assignment.

### Features and Implementation

**1. Integration with Picsum API**

- Retrieves photo information from the Picsum public API, beginning with `https://picsum.photos/v2/list?page=1`.
- Loads additional records by incrementing the page number (`page=2`, `page=3`, and so on).
- Uses asynchronous requests to retrieve data without blocking the interface.
- Includes request-handling mechanisms to avoid multiple simultaneous fetch operations.

**2. Automatic Infinite Scrolling**

- Implements the browser's `IntersectionObserver` API to monitor a designated element at the bottom of the gallery.
- Starts loading the next set of photographs when the user scrolls close to the end of the currently displayed content.
- Uses a prefetch margin to initiate requests before the user reaches the actual bottom.
- Prevents unnecessary API requests after the available photo data has been exhausted by maintaining a `hasMore` state.

**3. Image Rendering and Author Details**

- Fetches and renders photographs using the `download_url` received from the API.
- Applies native lazy loading to images through `loading="lazy"` to improve page performance.
- Displays shimmer-style skeleton placeholders while images are being loaded.
- Shows the photographer's name below each image using the format `Author: <author name>`.

**4. Like Functionality and Font Awesome Integration**

- Integrates Font Awesome through `@fortawesome/react-fontawesome` and `@fortawesome/free-solid-svg-icons`.
- Provides a thumbs-up button for every photograph.
- Initializes the like counter of each photo to `0`.
- Updates the corresponding counter by one whenever its button is clicked.
- Maintains separate like counts so that interacting with one photograph does not affect another.
- Adds a small bounce animation to improve the interaction experience.
- Supports keyboard interaction and accessible button descriptions through `aria-label`.

**5. Responsive UI and Reference Matching**

- Recreates the overall appearance of the supplied `photo-gallery.png` and `photo-gallery.jpg` reference images.
- On desktop screens, photographs are arranged in a single-column layout, with the heading "Photo gallery" positioned towards the right side of the header.
- On smaller screens, the layout adjusts automatically to maintain proper image sizing and spacing.
- Includes responsive styling for desktop, tablet, and mobile devices.
- Maintains comfortable spacing and touch-friendly controls on mobile screens.

**6. Error Management and Duplicate Prevention**

- Uses photo IDs to identify and filter out duplicate entries before adding new data to the gallery.
- Displays loading feedback during both the initial API request and subsequent pagination requests.
- Handles API failures and network connectivity issues without breaking the application.
- Shows a readable error message whenever a request fails.
- Provides a **"Retry loading"** option that allows users to attempt the failed request again.

---

## Project Directory Structure

```text
react-assignments-main/
├── README.md                           # Repository documentation
├── package.json                        # Root-level scripts and configuration
├── .gitignore                          # Files excluded from Git
├── chat-app/                           # Chat application assignment resources
│   ├── assets/
│   ├── reactjs_chat_assignment.md
│   └── team-chat-intro.gif
└── photo-gallery/                      # Implemented photo gallery application
    ├── README.md                       # Photo gallery documentation
    ├── package.json                    # Project dependencies and scripts
    ├── vite.config.js                  # Vite and Vitest configuration
    ├── index.html                      # Application HTML template
    ├── photo-gallery.jpg               # Reference screenshot (JPEG)
    ├── photo-gallery.png               # Reference screenshot (PNG)
    ├── reactjs_photo_gallery_assignment.md
    └── src/
        ├── main.jsx                    # React application entry point
        ├── App.jsx                     # Main application layout
        ├── index.css                   # Global styling and responsive rules
        ├── components/
        │   ├── PhotoGallery.jsx        # API integration and scrolling logic
        │   └── PhotoCard.jsx           # Photo component with like functionality
        └── test/
            ├── setup.js                # Test environment configuration
            ├── PhotoCard.test.jsx      # Tests for individual photo cards
            ├── PhotoGallery.test.jsx   # Gallery integration and behavior tests
            └── serverProbe.js          # Development server verification
```

---

## Installation and Execution Guide

### Requirements

Before running the application, ensure the following software is available:

- **Node.js:** Version 18.0.0 or above (tested with Node v22.17.1).
- **npm:** Version 9.0.0 or above (tested with npm 10.9.2).

### Method 1: Start the application from its project folder

This is the preferred approach.

```bash
# Step 1: Open the photo-gallery directory
cd photo-gallery

# Step 2: Download and install the required packages
npm install

# Step 3: Launch the Vite development server
npm run dev

# Alternatively
npm start
```

After the server starts, open the URL displayed in the terminal. The default configured address is:

`http://localhost:3000`

### Method 2: Run commands from the repository root

You can also install dependencies and launch the project without manually entering the subdirectory.

```bash
# Install dependencies for the photo gallery
npm --prefix photo-gallery install

# Start the development server
npm run dev

# Alternatively
npm start
```

---

## Testing and Production Build

### 1. Execute Automated Tests

The application uses Vitest along with React Testing Library to validate component behavior and application functionality.

Run the following commands:

```bash
cd photo-gallery
npm test
```

The test suite covers:

- Initial photo retrieval from the API.
- Loading additional photographs through infinite scrolling.
- Filtering duplicate photo entries.
- Individual like counter functionality.
- Handling failed requests and retry operations.
- Component-level rendering and interactions.

### 2. Generate a Production Build

To create an optimized version of the application for deployment, execute:

```bash
cd photo-gallery
npm run build
```

The generated production files will be available inside:

`photo-gallery/dist`

### 3. Run the Production Preview

To locally inspect the generated production build, use:

```bash
cd photo-gallery
npm run preview
```

This launches a local preview server so that the production output can be checked before deployment.

---

## Technologies Used and Implementation Choices

| Technology | Purpose |
|---|---|
| React 18 | Building reusable UI components and managing application state using hooks. |
| Vite 5 | Development server, project bundling, and production build generation. |
| Font Awesome | Providing the thumbs-up icon and its associated interactions. |
| Picsum API | Supplying photograph details and image URLs. |
| IntersectionObserver | Detecting scroll position and triggering additional data requests. |
| Vitest | Running automated unit and integration tests. |
| React Testing Library | Testing React components and user interactions. |
| jsdom | Providing a simulated browser environment for automated tests. |
