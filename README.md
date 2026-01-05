# Todos for Anuj

# React Fundamentals - Assignment Sheet

**Duration:** 4-5 Hours  
**Prerequisites:** Basic understanding of React, Hooks (useState, useEffect, useRef), Props, JSX  
**Setup:** Vite + React

---

## Table of Contents

1. [Setup Instructions](#setup-instructions)
2. [Part 1: Practical Coding Challenges](#part-1-practical-coding-challenges) (10 Challenges)
3. [Part 2: Todo List Application](#part-2-todo-list-application-crud)
4. [Part 3: News Website Application](#part-3-news-website-application-api-calls)
5. [Bonus Challenges](#bonus-challenges)

---

## Setup Instructions

### Creating a New React Project with Vite

```bash
# Create a new Vite project
npm create vite@latest project-name -- --template react

# Navigate to the project
cd project-name

# Install dependencies
npm install

# Start the development server
npm run dev
```

---

## Part 1: Practical Coding Challenges

Complete each challenge in a separate component file.

---

### Challenge 1: User Profile Card (Props)

**Task:** Create a `ProfileCard` component that accepts props and renders a user profile card.

**Requirements:**
- Accept props: `name`, `email`, `avatar` (image URL), `role`, `isOnline` (boolean)
- Display all information in a styled card
- Show a green dot if user is online, red if offline
- If `avatar` is not provided, show a placeholder with user's initials (User Icons)

**Test your component with this data:**
```jsx
<ProfileCard 
  name="John Doe"
  email="john@example.com"
  avatar="https://i.pravatar.cc/150?img=1"
  role="Frontend Developer"
  isOnline={true}
/>

<ProfileCard 
  name="Jane Smith"
  email="jane@example.com"
  role="Designer"
  isOnline={false}
/>
```

**Expected Output:** Two styled profile cards displaying user information.

---

### Challenge 2: Like Button with Count (useState)

**Task:** Build a `LikeButton` component similar to social media like buttons.

**Requirements:**
- Display a heart icon (can use emoji ❤️ or 🤍)
- Show the like count next to it
- Clicking toggles between liked (red heart) and unliked (white heart)
- Count increases when liked, decreases when unliked
- Accept initial `likes` count as prop

**Test your component:**
```jsx
<LikeButton initialLikes={42} />
<LikeButton initialLikes={0} />
```

**Expected Behavior:**
```
🤍 42  → click → ❤️ 43 → click → 🤍 42
```

---

### Challenge 3: Render Product Cards from Array (Lists & Keys)

**Task:** Render a list of product cards from an array of data.

**Given Data:**
```jsx
const products = [
  { id: 1, name: "Laptop", price: 999, inStock: true, image: "https://picsum.photos/200?random=1" },
  { id: 2, name: "Headphones", price: 199, inStock: true, image: "https://picsum.photos/200?random=2" },
  { id: 3, name: "Mouse", price: 49, inStock: false, image: "https://picsum.photos/200?random=3" },
  { id: 4, name: "Keyboard", price: 129, inStock: true, image: "https://picsum.photos/200?random=4" },
  { id: 5, name: "Monitor", price: 399, inStock: false, image: "https://picsum.photos/200?random=5" },
];
```

**Requirements:**
- Create a `ProductCard` component for individual products
- Display: image, name, price (formatted as ₹XXX), stock status
- Show "In Stock" (green) or "Out of Stock" (red) badge
- Add "Add to Cart" button (disabled if out of stock)
- Render all products in a grid layout

---

### Challenge 4: Digital Clock (useEffect)

**Task:** Build a `DigitalClock` component that shows current time updating every second.

**Requirements:**
- Display current time in format: `HH:MM:SS`
- Time updates every second automatically
- Show AM/PM indicator
- Display current date below the time
- Clean up the interval when component unmounts

**Expected Output:**
```
02:45:30 PM
Monday, January 15, 2024
```

**Hint:** Use `setInterval` inside `useEffect` and don't forget cleanup!

**Cleanup Functions:** A cleanup function in React is a function returned from useEffect that runs when:

- The component unmounts (removed from DOM)
- Before the effect runs again (when dependencies change)

**Example 1**: Without Cleanup (❌ Problem)
```js
import { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    // This interval keeps running even after component unmounts!
    setInterval(() => {
      setSeconds(prev => prev + 1);
      console.log("Still running..."); // You'll see this even after component is gone
    }, 1000);
  }, []);

  return <h1>{seconds} seconds</h1>;
}
```
Problem: If this component unmounts, the interval keeps running in the background, causing memory leaks and errors.

**Example 2:** With Cleanup (✅ Correct)
```js
import { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    // Start the interval
    const intervalId = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);

    // 👇 CLEANUP FUNCTION - runs when component unmounts
    return () => {
      clearInterval(intervalId);
      console.log("Interval cleared!");
    };
  }, []);

  return <h1>{seconds} seconds</h1>;
}
```
---

### Challenge 5: Auto-Focus Form (useRef)

**Task:** Build a login form with auto-focus and form handling.

**Requirements:**
- Create a form with: Email input, Password input, Submit button
- Email input should be auto-focused when component mounts
- After successful submit, clear the form and focus back to email
- Show "Login Successful!" message for 3 seconds after submit
- Add a "Clear Form" button that clears inputs and focuses email

**Component Structure:**
```jsx
function LoginForm() {
  // Use useRef for input references
  // Use useState for form values and success message
  
  return (
    <form>
      {/* Your implementation */}
    </form>
  );
}
```

---

### Challenge 6: Character Counter Textarea (Controlled Component)

**Task:** Build a `TweetBox` component like Twitter's tweet composer.

**Requirements:**
- Textarea input for message
- Maximum 280 characters allowed
- Show remaining characters count (e.g., "250 characters remaining")
- Count turns yellow when < 50 characters remaining
- Count turns red when < 20 characters remaining
- Disable "Post" button when empty or over limit
- Show warning message when over limit

**Expected Behavior:**
```
[                              ]
[  Type your message here...   ]
[                              ]

280 characters remaining          [Post]

// As user types "Hello World" (11 chars):
269 characters remaining          [Post]

// When over limit:
-5 characters remaining (red)     [Post] (disabled)
"Your tweet is too long!"
```

---

### Challenge 7: Stopwatch (useState + useEffect + useRef)

**Task:** Build a fully functional stopwatch.

**Requirements:**
- Display time in format: `MM:SS:ms` (minutes, seconds, milliseconds)
- Three buttons: Start, Stop, Reset
- Start button changes to "Pause" when running
- Lap button to record lap times (show list of laps)
- Reset clears everything including laps

**Expected Output:**
```
00:05:42

[Pause] [Lap] [Reset]

Laps:
1. 00:02:15
2. 00:03:89
3. 00:05:42
```

**Hint:** Use `useRef` to store the interval ID for proper cleanup.

---

### Challenge 8: Accordion Component (Props + State)

**Task:** Build a reusable `Accordion` component.

**Given Data:**
```jsx
const faqs = [
  {
    id: 1,
    question: "What is React?",
    answer: "React is a JavaScript library for building user interfaces."
  },
  {
    id: 2,
    question: "What are hooks?",
    answer: "Hooks are functions that let you use state and other React features in functional components."
  },
  {
    id: 3,
    question: "What is JSX?",
    answer: "JSX is a syntax extension for JavaScript that allows you to write HTML-like code in your JavaScript files."
  }
];
```

**Requirements:**
- Only one accordion item should be open at a time
- Clicking an open item closes it
- Show expand/collapse icon (+ / -)
- Smooth transition animation (bonus)
- Create reusable `AccordionItem` component

---

### Challenge 9: Tabs Component (Component Composition)

**Task:** Build a reusable `Tabs` component.

**Requirements:**
- Create `Tabs` and `Tab` components
- Only active tab's content is visible
- Active tab should be highlighted
- Support keyboard navigation (bonus)

**Usage Example:**
```jsx
<Tabs defaultTab={0}>
  <Tab label="Profile">
    <h2>Profile Content</h2>
    <p>This is the profile section...</p>
  </Tab>
  <Tab label="Settings">
    <h2>Settings Content</h2>
    <p>This is the settings section...</p>
  </Tab>
  <Tab label="Notifications">
    <h2>Notifications Content</h2>
    <p>You have 3 new notifications...</p>
  </Tab>
</Tabs>
```

---

### Challenge 10: Shopping Cart (Lifting State Up)

**Task:** Build a mini shopping cart with product list and cart summary.

**Requirements:**
- `ProductList` component: Shows products with "Add to Cart" button
- `Cart` component: Shows added items with quantity and total
- `App` component: Manages the shared state
- Can increase/decrease quantity in cart
- Can remove items from cart
- Shows total price

**Component Structure:**
```jsx
function App() {
  const [cart, setCart] = useState([]);
  
  return (
    <div className="app">
      <ProductList onAddToCart={/* ? */} />
      <Cart items={cart} onUpdateCart={/* ? */} />
    </div>
  );
}
```

**Given Products:**
```jsx
const products = [
  { id: 1, name: "T-Shirt", price: 29.99 },
  { id: 2, name: "Jeans", price: 59.99 },
  { id: 3, name: "Sneakers", price: 89.99 },
  { id: 4, name: "Hat", price: 19.99 },
];
```
---

## Part 2: Todo List Application (CRUD)

**Time Estimate:** 1.5 - 2 hours

### Project Overview

Build a fully functional Todo List application that demonstrates Create, Read, Update, and Delete operations.

### Requirements

#### Core Features:

1. **Add Todo (Create)**
   - Input field to enter new todo
   - Button to add the todo
   - Todo should have: id, text, completed status, created date

2. **Display Todos (Read)**
   - Show all todos in a list
   - Display todo text and completion status
   - Show total count of todos
   - Show count of completed vs pending todos

3. **Edit Todo (Update)**
   - Double-click on todo text to edit it
   - Toggle completion status with a checkbox
   - Save edited text with Enter key or blur

4. **Delete Todo (Delete)**
   - Delete button for each todo
   - "Clear Completed" button to remove all completed todos
   - "Clear All" button to remove everything

#### Additional Features: (Optional)

5. **Filter Todos**
   - Filter buttons: All, Active, Completed
   - Highlight the active filter

6. **Local Storage (Bonus)**
   - Persist todos in localStorage
   - Load todos from localStorage on app start

### Suggested Component Structure

```
src/
├── App.jsx
├── components/
│   ├── TodoForm.jsx      # Input form to add todos
│   ├── TodoList.jsx      # Container for all todo items
│   ├── TodoItem.jsx      # Individual todo item
│   ├── TodoFilter.jsx    # Filter buttons
│   └── TodoStats.jsx     # Statistics display
```

### Data Structure

```javascript
const todo = {
  id: 1,                          // unique identifier
  text: "Learn React",            // todo content
  completed: false,               // completion status
  createdAt: new Date().toISOString()  // creation timestamp
};
```

### Starter Template

```jsx
// App.jsx
import { useState } from 'react';

function App() {
  const [todos, setTodos] = useState([]);
  const [filter, setFilter] = useState('all'); // 'all', 'active', 'completed'

  // TODO: Implement these functions
  const addTodo = (text) => {
    // Create new todo and add to state
  };

  const deleteTodo = (id) => {
    // Remove todo by id
  };

  const toggleTodo = (id) => {
    // Toggle completed status
  };

  const editTodo = (id, newText) => {
    // Update todo text
  };

  const clearCompleted = () => {
    // Remove all completed todos
  };

  const getFilteredTodos = () => {
    // Return todos based on current filter
  };

  return (
    <div className="app">
      <h1>Todo List</h1>
      {/* Build your UI here */}
    </div>
  );
}

export default App;
```

### Acceptance Criteria

- [ ] Can add new todos
- [ ] Can view all todos
- [ ] Can mark todos as complete/incomplete
- [ ] Can edit todo text
- [ ] Can delete individual todos
- [ ] Can clear all completed todos (Optional)
- [ ] Can filter todos by status (Optional)
- [ ] Shows todo statistics (Optional)
- [ ] Empty state message when no todos (Optional)
- [ ] Input validation (no empty todos) (Optional)

### Styling (Optional)

Basic CSS to make it look nice:

```css
/* App.css */
.app {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.todo-item {
  display: flex;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
}

.todo-item.completed {
  text-decoration: line-through;
  opacity: 0.6;
}

.filters {
  display: flex;
  gap: 10px;
  margin: 20px 0;
}

.filter-btn {
  padding: 5px 15px;
  cursor: pointer;
}

.filter-btn.active {
  background-color: #007bff;
  color: white;
}
```

---

## Part 3: News Website Application (API Calls)

**Time Estimate:** 1.5 - 2 hours

### Project Overview

Build a News Website that fetches articles from a public API and displays them. This project focuses on handling asynchronous operations, API calls, and managing loading/error states.

### API Option

**Free News API:** [NewsAPI.org](https://newsapi.org/) (requires free registration)

**Alternative (No API Key):** Use JSONPlaceholder for practice:
```
https://jsonplaceholder.typicode.com/posts
```

For this assignment, we'll use a mock news API structure that simulates real news data.

### Requirements

#### Core Features:

1. **Fetch and Display News**
   - Fetch news articles on component mount
   - Display articles in a card layout
   - Show: title, description, image, source, published date

2. **Loading State**
   - Show loading spinner/message while fetching
   - Skeleton loaders for better UX (bonus)

3. **Error Handling**
   - Display error message if fetch fails
   - Retry button to attempt fetch again

4. **Category Filter**
   - Filter news by category (Technology, Sports, Business, etc.)
   - Fetch new data when category changes

5. **Search Functionality**
   - Search input to filter articles
   - Debounce search input (bonus)

6. **Pagination or Load More**
   - Show limited articles initially
   - "Load More" button or pagination

### Suggested Component Structure

```
src/
├── App.jsx
├── components/
│   ├── Header.jsx           # App header with search
│   ├── CategoryFilter.jsx   # Category selection
│   ├── NewsList.jsx         # Container for articles
│   ├── NewsCard.jsx         # Individual article card
│   ├── LoadingSpinner.jsx   # Loading indicator
│   └── ErrorMessage.jsx     # Error display
├── hooks/
│   └── useFetch.js          # Custom hook for data fetching
```

### Custom Hook: useFetch

Create a reusable custom hook for fetching data:

```jsx
// hooks/useFetch.js
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // TODO: Implement fetch logic
    // 1. Set loading to true
    // 2. Fetch data from url
    // 3. Handle success: set data, loading false
    // 4. Handle error: set error, loading false
    // 5. Consider cleanup for unmounted components
  }, [url]);

  return { data, loading, error };
}

export default useFetch;
```

### Mock API Setup

Since free news APIs have limitations, create a mock API file:

```jsx
// data/mockNews.js
export const mockArticles = [
  {
    id: 1,
    title: "React 19 Released with Exciting New Features",
    description: "The React team has announced the release of React 19, bringing significant improvements to server components and performance.",
    image: "https://picsum.photos/400/200?random=1",
    source: "Tech Daily",
    category: "technology",
    publishedAt: "2024-01-15T10:30:00Z",
    url: "#"
  },
  {
    id: 2,
    title: "Global Markets See Record Highs",
    description: "Stock markets around the world reached new peaks as investor confidence grows amid positive economic indicators.",
    image: "https://picsum.photos/400/200?random=2",
    source: "Finance Weekly",
    category: "business",
    publishedAt: "2024-01-14T08:15:00Z",
    url: "#"
  },
  // Add more mock articles...
];

// Simulate API delay
export const fetchNews = (category = 'all') => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      // Simulate random error (10% chance)
      if (Math.random() < 0.1) {
        reject(new Error('Failed to fetch news'));
        return;
      }
      
      let filtered = mockArticles;
      if (category !== 'all') {
        filtered = mockArticles.filter(a => a.category === category);
      }
      resolve(filtered);
    }, 1000); // 1 second delay
  });
};
```

### Starter Template

```jsx
// App.jsx
import { useState, useEffect } from 'react';

function App() {
  const [articles, setArticles] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const [category, setCategory] = useState('all');
  const [searchTerm, setSearchTerm] = useState('');

  const categories = ['all', 'technology', 'business', 'sports', 'entertainment'];

  // TODO: Fetch articles when component mounts or category changes
  useEffect(() => {
    const fetchArticles = async () => {
      // Implement fetch logic here
    };
    
    fetchArticles();
  }, [category]);

  // TODO: Filter articles based on search term
  const filteredArticles = articles.filter(article => {
    // Implement search filter
  });

  if (loading) return <LoadingSpinner />;
  if (error) return <ErrorMessage message={error} onRetry={/* retry function */} />;

  return (
    <div className="app">
      <Header searchTerm={searchTerm} onSearch={setSearchTerm} />
      <CategoryFilter 
        categories={categories} 
        active={category} 
        onChange={setCategory} 
      />
      <NewsList articles={filteredArticles} />
    </div>
  );
}
```

### NewsCard Component

```jsx
// components/NewsCard.jsx
function NewsCard({ article }) {
  const { title, description, image, source, publishedAt } = article;
  
  // TODO: Format the date nicely
  const formatDate = (dateString) => {
    // Implement date formatting
  };

  return (
    <div className="news-card">
      {/* Implement the card UI */}
    </div>
  );
}
```

### Acceptance Criteria

- [ ] Articles load on initial page load
- [ ] Loading state shown while fetching
- [ ] Error state shown if fetch fails
- [ ] Can retry after error
- [ ] Can filter by category
- [ ] Category change triggers new fetch
- [ ] Can search articles by title
- [ ] Articles display title, description, image, source, date
- [ ] Responsive card layout
- [ ] Clean, readable code structure

### Styling (Optional)

```css
/* App.css */
.app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.news-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.news-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  transition: transform 0.2s;
}

.news-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}

.news-card img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.news-card-content {
  padding: 15px;
}

.loading-spinner {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 200px;
}

.error-message {
  text-align: center;
  padding: 40px;
  color: #dc3545;
}
```

---

## Bonus Challenges

If you complete the main assignments early, try these additional challenges:

### Challenge 1: Debounced Search (News App)
Implement a debounce function so the search doesn't trigger on every keystroke.

```jsx
// Hint: Create a custom useDebounce hook
function useDebounce(value, delay) {
  // Your implementation
}
```

### Challenge 2: Optimistic Updates (Todo App)
Update the UI immediately before the "API call" completes, then revert if it fails.

### Challenge 3: Drag and Drop (Todo App)
Allow users to reorder todos by dragging them.

### Challenge 4: Dark Mode Toggle
Add a dark/light mode toggle that persists in localStorage.

### Challenge 5: Infinite Scroll (News App)
Replace "Load More" with automatic loading when user scrolls to bottom.

---

## Submission Checklist

Before submitting your work, ensure:

- [ ] All conceptual questions are answered
- [ ] All mini exercises are completed
- [ ] Todo app has all CRUD operations working
- [ ] News app fetches and displays data correctly
- [ ] Code is clean and well-commented
- [ ] Components are properly separated
- [ ] No console errors or warnings

---

## Evaluation Criteria

| Criteria | Weight |
|----------|--------|
| Code Quality & Organization | 20% |
| Correct use of useState | 20% |
| Correct use of useEffect | 20% |
| Correct use of Props | 15% |
| Correct use of useRef | 10% |
| UI/UX & Styling | 15% |

---

## Resources

- [React Documentation](https://react.dev/)
- [Vite Documentation](https://vitejs.dev/)
- [MDN Web Docs - Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [CSS Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)

---

**Good luck! Happy coding! 🚀**
