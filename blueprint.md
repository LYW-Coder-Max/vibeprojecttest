
# Blueprint: Teaching Assistant

## Overview

The Teaching Assistant is a web-based application designed to enhance classroom presentations and remote learning. It allows an instructor to display a Google Slides presentation alongside a real-time discussion feed. Students or participants can add timestamped notes, questions, and images tied to specific slides, creating a collaborative and contextual learning environment. This tool aims to bridge the gap between presentation content and audience engagement.

## Design and Features

### 1. Visual Design & Layout

*   **Layout:** A two-panel layout with a main slide display area and a side panel for the discussion feed. The layout is responsive and adapts to different screen sizes.
*   **Header:** A prominent header with a professional and inspiring background image, clearly stating the application's title.
*   **Color Palette:** A clean and modern color scheme with a primary color (dark blue-gray), an accent color (Google Blue), and a light background for readability.
*   **Typography:** Uses the 'Segoe UI' font family for a clean, modern look. Font sizes are used to create a clear visual hierarchy.
*   **Interactivity:** Buttons and input fields are styled for a modern look with clear hover states.

### 2. Core Features

*   **Google Slides Integration:**
    *   Users can load any Google Slides presentation by pasting its `<iframe>` embed code.
    *   The application automatically parses the embed code to control the presentation.
*   **Slide Navigation:**
    *   Dedicated "Previous" and "Next" buttons allow the presenter to navigate the slides.
    *   The slide navigation is synchronized with the note feed, showing relevant notes for the current slide.
    *   A slide indicator displays the current and total number of slides (e.g., "Slide 5 / 20").
*   **Discussion Stream (Feed Panel):**
    *   Displays notes and questions related to the currently viewed slide.
    *   When the feed is empty for a particular slide, a clear message is shown.
*   **Note & Question Submission:**
    *   A simple input area allows users to add notes or questions.
    *   Users can target a specific slide number for their note.
    *   Users can optionally upload an image to accompany their text post.
    *   Posts are displayed as "cards" with a timestamp.

### 3. Technical Implementation

*   **Frontend:** Built with standard HTML, CSS, and JavaScript, without any external frameworks.
*   **Styling:** Modern CSS practices, including CSS Variables for easy theming.
*   **JavaScript:** Vanilla JavaScript is used for all functionality. ES6 features and best practices are followed for clean and maintainable code.
*   **State Management:** Global JavaScript variables are used to maintain the application's state, including the current slide number, total slides, and all slide-related data (notes and images).

## Current Task: Bug Fix - Feed Synchronization

### 1. The Problem

After fixing the slide navigation, a new bug was introduced: the discussion feed was no longer synchronizing with the slide changes. The feed would not update to show the notes for the newly displayed slide. This was due to a timing issue in the `changeSlide` function, where the UI was being re-rendered *before* the `<iframe>`'s source URL was updated.

### 2. The Solution

The bug was resolved by reordering the function calls within the `changeSlide` function.

*   **`changeSlide()` Function Update:**
    1.  The `updateIframeSource()` function is now called *before* the `updateUI()` function.
    2.  This ensures that the Google Slides `<iframe>` is instructed to change to the new slide first.
    3.  Once the new slide is loading, the `updateUI()` function is called, which in turn calls `renderFeed()`. This correctly fetches and displays the notes for the current slide, resolving the synchronization issue.

*   **`updateIframeSource()` Function Enhancement:**
    1.  A small improvement was made to the URL construction. The slide number is now appended in the format `slide=id.p<slide_number>`, which is a more robust way to link to specific slides in Google Slides.
