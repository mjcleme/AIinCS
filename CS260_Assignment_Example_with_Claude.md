# CS 260 Assignment Example: Restaurant Review App with Claude Integration

> [!NOTE]
>
> `LEE` This seems great. We should try it ourselves first. It will be a significant mental shift for our students to move to this model. They love detailed rubrics. Possible reactions will likely be:
>
> - The AI grader isn't working right
> - I don't know what the AI grader wants
> - What am I suppose to do?
>
> Also, what about UI testing? It looks like everything is API testing. It is a web app and so you really need to test the frontend. Google's Antigravity has really slick testing via the browser.

**Course:** CS 260 - Web Programming
**Assignment:** Build a Full-Stack Restaurant Review Application
**Duration:** 3 weeks
**Claude Usage:** Allowed and encouraged for design discussion and implementation assistance

## Assignment Specification

### Overview

Build a full-stack web application that allows users to browse restaurants, submit reviews, and view ratings.

### Required Features

1. **Restaurant Listing:** Display all restaurants with name, cuisine type, average rating
2. **Restaurant Detail:** Show individual restaurant with all reviews
3. **Add Review:** Form to submit review (rating 1-5 stars, text review, reviewer name)
4. **Filter/Search:** Filter restaurants by cuisine type or search by name
5. **Responsive Design:** Works on mobile and desktop

### Technical Requirements

- **Frontend:** HTML, CSS, JavaScript (vanilla or React - student's choice)
- **Backend:** Node.js + Express
- **Database:** MongoDB or PostgreSQL
- **API:** RESTful API with proper HTTP methods (GET, POST, etc.)
- **Security:** Input validation, no SQL injection vulnerabilities
- **Testing:** At least 5 meaningful tests

### Deliverables

1. **Design Document** (Due Week 1):

   - Architecture diagram
   - API endpoint design
   - Database schema
   - Technology choices with justification

2. **Implementation** (Due Week 3):

   - Working application
   - Tests
   - README with setup instructions

3. **Reflection Document** (Due Week 3):
   - Explain design decisions
   - Describe challenges encountered and solutions
   - Reflect on how Claude helped and limitations you found

### Grading Breakdown (100 points)

- **Design Document (20 pts):** Claude API-graded for justification quality
- **Functional Correctness (30 pts):** Autograder tests all required features
- **API Design Quality (15 pts):** Autograder checks REST conventions, status codes
- **Code Quality (10 pts):** Autograder checks security, structure
- **Testing (10 pts):** Autograder evaluates test coverage and quality
- **Reflection (15 pts):** Claude API-graded for depth of understanding

## Phase 1: Design Phase with Claude

### Student-Claude Interaction: Architecture Discussion

**Student:**

> I need to design a restaurant review app for my CS 260 assignment. The requirements are: display restaurants, show reviews, let users add reviews, filter by cuisine. I need to choose between vanilla JavaScript and React for the frontend, and decide on database schema. Can you help me think through the architecture?

**Claude:**

> I'd be happy to help you think through the architecture for your restaurant review app. Let's break this down into key decisions:
>
> **Frontend Framework Decision:**
>
> **Vanilla JavaScript:**
>
> - Pros: Better understanding of DOM manipulation, lighter weight, no build tools needed
> - Cons: More boilerplate for state management, manual DOM updates can get complex
> - Best if: You want to deeply understand how frameworks work under the hood
>
> **React:**
>
> - Pros: Component reusability, easier state management, declarative UI updates
> - Cons: Build setup required, more abstraction from fundamentals
> - Best if: You want to focus more on application logic than DOM manipulation
>
> Given this is CS 260, I'd lean toward React if you're comfortable with it - it will let you build a more sophisticated app with less boilerplate. However, if you want to really understand DOM fundamentals, vanilla JS is valuable.
>
> **Database Schema Design:**
>
> For your use case, you'll need at least two collections/tables:
>
> ```
> Restaurants:
> - id (primary key)
> - name
> - cuisine_type
> - address
> - description
>
> Reviews:
> - id (primary key)
> - restaurant_id (foreign key)
> - rating (1-5)
> - review_text
> - reviewer_name
> - created_at
> ```
>
> **API Endpoints:**
>
> Following REST conventions:
>
> - GET /api/restaurants - List all restaurants
> - GET /api/restaurants/:id - Get single restaurant with reviews
> - POST /api/restaurants/:id/reviews - Add review to restaurant
> - GET /api/restaurants?cuisine=Italian - Filter by cuisine
>
> **Questions for you to consider:**
>
> - Do you want to implement user authentication, or allow anonymous reviews?
> - Should reviews be editable/deletable?
> - Do you want real-time updates when reviews are added?
> - What's your comfort level with React vs vanilla JS?

**Student:**

> I'm comfortable with React and want to focus on the application logic rather than DOM manipulation. I don't think I need authentication for this assignment - anonymous reviews are fine. Reviews don't need to be editable. No real-time updates needed.
>
> For the database, should I use MongoDB or PostgreSQL? And do I need any indexes for the filter/search functionality?

**Claude:**

> Great choices - React will let you focus on the application architecture.
>
> **MongoDB vs PostgreSQL for this project:**
>
> **MongoDB:**
>
> - Pros: Easier to get started, flexible schema, can embed reviews in restaurant documents
> - Cons: Less strict about data integrity, joins are more complex
> - Good fit: Your data model is relatively simple, no complex relationships
>
> **PostgreSQL:**
>
> - Pros: Strong data integrity with foreign keys, excellent for relational data (restaurants ↔ reviews)
> - Cons: Requires more schema design upfront, slightly more complex setup
> - Good fit: You have a clear relational model, want to ensure review consistency
>
> For this assignment, **MongoDB might be simpler** since your data model is straightforward. You could structure it two ways:
>
> **Option 1: Embedded reviews (simpler for this scale)**
>
> ```javascript
> {
>   _id: ObjectId,
>   name: "Pizza Palace",
>   cuisine: "Italian",
>   reviews: [
>     {rating: 5, text: "Amazing!", reviewer: "John", date: "2024-01-15"},
>     {rating: 4, text: "Pretty good", reviewer: "Jane", date: "2024-01-16"}
>   ]
> }
> ```
>
> **Option 2: Separate collections (more scalable)**
>
> ```javascript
> // Restaurants collection
> {_id: ObjectId, name: "Pizza Palace", cuisine: "Italian"}
>
> // Reviews collection
> {_id: ObjectId, restaurant_id: ObjectId("..."), rating: 5, text: "Amazing!"}
> ```
>
> **Recommendation:** Use **separate collections** (Option 2). Here's why:
>
> - More scalable (if a restaurant has 1000 reviews, embedded would make the document huge)
> - Easier to query "all reviews by user" later if needed
> - Better practice for learning database design
>
> **Indexes for performance:**
> Yes, you should add indexes:
>
> - `cuisine` field in Restaurants collection (for filtering)
> - `name` field in Restaurants collection (for search)
> - `restaurant_id` in Reviews collection (for lookups)
>
> **Does this make sense for your design doc? What questions do you have?**

**Student:**

> That makes sense! So I'll go with React frontend, Express backend, MongoDB with separate collections. Let me draft my API endpoints more specifically:
>
> - GET /api/restaurants - returns all restaurants with average rating calculated
> - GET /api/restaurants?cuisine=Italian - filter by cuisine
> - GET /api/restaurants?search=pizza - search by name
> - GET /api/restaurants/:id - get one restaurant
> - GET /api/restaurants/:id/reviews - get reviews for a restaurant
> - POST /api/restaurants/:id/reviews - add a review
>
> Does this API design look good? Should I calculate average rating in the backend or frontend?

**Claude:**

> Your API design is solid! A few suggestions:
>
> **API Refinements:**
>
> 1. **Consolidate GET endpoints:**
>    Instead of separate endpoints for cuisine and search, use query parameters on the main endpoint:
>
>    ```
>    GET /api/restaurants           # all restaurants
>    GET /api/restaurants?cuisine=Italian
>    GET /api/restaurants?search=pizza
>    GET /api/restaurants?cuisine=Italian&search=palace  # can combine
>    ```
>
> 2. **Consider nesting:**
>    Your current design has:
>
>    - GET /api/restaurants/:id - restaurant data
>    - GET /api/restaurants/:id/reviews - reviews for restaurant
>
>    You could simplify: make GET /api/restaurants/:id return the restaurant WITH its reviews included. This reduces API calls from the frontend.
>
>    **Alternatively**, keep them separate if you want the list view to load fast (without fetching all reviews), then fetch reviews only when user clicks into detail view.
>
> 3. **Status codes:**
>    Make sure your implementation uses proper HTTP status codes:
>    - 200 OK for successful GET
>    - 201 Created for successful POST
>    - 400 Bad Request for invalid review data
>    - 404 Not Found if restaurant doesn't exist
>    - 500 Internal Server Error for server issues
>
> **Average Rating Calculation:**
>
> **Calculate on backend** (recommended):
>
> - When a new review is added, recalculate and store average rating in restaurant document
> - Or calculate on-the-fly using MongoDB aggregation:
>   ```javascript
>   db.reviews.aggregate([{ $match: { restaurant_id: id } }, { $group: { _id: null, avgRating: { $avg: '$rating' } } }]);
>   ```
> - Pro: API returns ready-to-use data, consistent calculation
> - Con: Slightly more backend logic
>
> **Calculate on frontend:**
>
> - Fetch all reviews, calculate average in JavaScript
> - Pro: Simpler backend
> - Con: Extra data transferred, calculation logic in multiple places
>
> **Best practice:** Calculate on backend. Your API should return:
>
> ```json
> {
>   "id": "123",
>   "name": "Pizza Palace",
>   "cuisine": "Italian",
>   "averageRating": 4.5,
>   "reviewCount": 12
> }
> ```
>
> This way frontend just displays the number, doesn't need to calculate.
>
> **Ready to start implementation?** Document these decisions in your design doc!

### Student's Design Document (Submitted)

````markdown
# Restaurant Review App - Design Document

## Architecture Overview

- **Frontend:** React application with component-based UI
- **Backend:** Node.js + Express REST API
- **Database:** MongoDB with separate collections for restaurants and reviews

## Technology Justification

### Why React?

I chose React over vanilla JavaScript because:

- Component reusability will make it easier to build restaurant cards and review lists
- State management is simpler for handling filter/search interactions
- Declarative UI updates reduce DOM manipulation complexity
- Industry-relevant skill

### Why MongoDB?

- Straightforward setup for this project scale
- Flexible schema if requirements change
- Good practice with NoSQL databases
- Separate collections approach is more scalable than embedded documents

## Database Schema

### Restaurants Collection

```javascript
{
  _id: ObjectId,
  name: String,
  cuisine: String,
  address: String,
  description: String,
  averageRating: Number,  // calculated when reviews are added
  reviewCount: Number
}
```
````

**Indexes:**

- `cuisine` (for filtering)
- `name` (for search)

### Reviews Collection

```javascript
{
  _id: ObjectId,
  restaurant_id: ObjectId,  // reference to restaurant
  rating: Number,  // 1-5
  reviewText: String,
  reviewerName: String,
  createdAt: Date
}
```

**Indexes:**

- `restaurant_id` (for querying reviews by restaurant)

## API Design

| Method | Endpoint                     | Description                                                      | Status Codes  |
| ------ | ---------------------------- | ---------------------------------------------------------------- | ------------- |
| GET    | /api/restaurants             | Get all restaurants, with optional ?cuisine= or ?search= filters | 200           |
| GET    | /api/restaurants/:id         | Get single restaurant with details                               | 200, 404      |
| GET    | /api/restaurants/:id/reviews | Get all reviews for a restaurant                                 | 200, 404      |
| POST   | /api/restaurants/:id/reviews | Add a review to a restaurant                                     | 201, 400, 404 |

### Design Decision: Average Rating Calculation

I will calculate average rating on the backend when reviews are added, and store it in the restaurant document. This is better than frontend calculation because:

- API returns consistent data to all clients
- Reduces data transfer (don't need to send all reviews just to calculate average)
- Single source of truth for rating calculation

## Component Architecture (Frontend)

```
App
├── RestaurantList (displays filtered list)
│   └── RestaurantCard (individual restaurant)
├── RestaurantDetail (shows single restaurant)
│   ├── ReviewList
│   │   └── ReviewCard
│   └── AddReviewForm
└── FilterBar (search and cuisine filter)
```

## Security Considerations

- Input validation on review submissions (validate rating is 1-5, text is not empty)
- Sanitize user input to prevent XSS attacks
- Use parameterized queries to prevent NoSQL injection
- Rate limiting on review submission to prevent spam

## Testing Plan

- Test GET /api/restaurants returns all restaurants
- Test filtering by cuisine works correctly
- Test search by name works correctly
- Test POST review creates review and updates restaurant averageRating
- Test invalid review data returns 400 error

````

### Claude API Autograding of Design Document

The autograder runs this design document through Claude API:

```python
def grade_design_document(design_doc):
    prompt = f"""You are grading a CS 260 student's design document for a restaurant review app.

ASSIGNMENT REQUIREMENTS:
- Full-stack app with restaurant listing, reviews, filtering
- Must include architecture, database schema, API design, technology justification

STUDENT DESIGN DOCUMENT:
{design_doc}

RUBRIC (20 points):
1. Technology Justification (5 pts): Do they explain WHY they chose React/MongoDB/etc.?
2. Database Design (5 pts): Is schema appropriate? Are indexes mentioned?
3. API Design (5 pts): RESTful design? Proper endpoints and status codes?
4. Depth of Thinking (5 pts): Do they show understanding of tradeoffs and design decisions?

Evaluate each criterion. For each, identify:
- What is done well
- What is missing or could be improved
- Whether explanation demonstrates genuine understanding or is superficial

Return JSON:
{{
    "technology_justification": {{
        "score": <0-5>,
        "feedback": "<specific feedback>"
    }},
    "database_design": {{
        "score": <0-5>,
        "feedback": "<specific feedback>"
    }},
    "api_design": {{
        "score": <0-5>,
        "feedback": "<specific feedback>"
    }},
    "depth_of_thinking": {{
        "score": <0-5>,
        "feedback": "<specific feedback>"
    }},
    "total_score": <sum>,
    "overall_feedback": "<summary for student>"
}}
"""

    response = claude_api.messages.create(
        model="claude-3-5-sonnet-20241022",
        max_tokens=1500,
        messages=[{"role": "user", "content": prompt}]
    )

    return json.loads(response.content[0].text)
````

**Claude's Assessment:**

```json
{
  "technology_justification": {
    "score": 5,
    "feedback": "Excellent justification. Student explains React choice with specific reasons (component reusability, state management, declarative UI) rather than generic statements. MongoDB justification is solid with awareness of tradeoffs (flexible schema, separate vs embedded collections). Shows consideration of scale and future changes."
  },
  "database_design": {
    "score": 5,
    "feedback": "Strong database design. Appropriate schema with clear separation of concerns. Importantly, student includes indexes for cuisine, name, and restaurant_id - showing performance awareness. Averageing and reviewCount in restaurant document is a good denormalization decision. Clear foreign key relationship via restaurant_id."
  },
  "api_design": {
    "score": 4,
    "feedback": "Good RESTful API design with proper endpoints and HTTP methods. Correctly uses query parameters for filtering/search. Includes appropriate status codes (200, 201, 400, 404). Minor issue: could mention GET /api/restaurants/:id could optionally include reviews to reduce API calls, but current design is acceptable. Good documentation in table format."
  },
  "depth_of_thinking": {
    "score": 5,
    "feedback": "Demonstrates genuine understanding of design tradeoffs. The average rating calculation section shows excellent critical thinking - student compares backend vs frontend calculation with specific pros/cons and makes a justified choice. Security considerations section shows awareness of real-world concerns (XSS, NoSQL injection, rate limiting). Component architecture is clearly thought through. This goes beyond surface-level description."
  },
  "total_score": 19,
  "overall_feedback": "Outstanding design document. You demonstrate clear understanding of architectural decisions and can justify your choices with technical reasoning. Your database design is solid with appropriate indexes, and your API follows REST conventions. The average rating calculation discussion particularly shows strong critical thinking. One minor suggestion: consider whether GET /api/restaurants/:id should include reviews to reduce client API calls, or keep them separate for faster list view loading - document your reasoning. Great work!"
}
```

**Grade: 19/20**

---

## Phase 2: Implementation Phase with Claude

### Student-Claude Interaction: Implementation Help

**Student:**

> I'm ready to start implementing my restaurant review app. I have my design approved. Can you help me set up the Express server with the REST endpoints I designed?

**Claude:**

> Absolutely! Let's set up your Express server with the endpoints from your design. Here's a structure to get you started:
>
> ```javascript
> // server.js
> const express = require('express');
> const mongoose = require('mongoose');
> const cors = require('cors');
>
> const app = express();
>
> // Middleware
> app.use(express.json());
> app.use(cors());
>
> // MongoDB connection
> mongoose.connect('mongodb://localhost:27017/restaurant-reviews', {
>   useNewUrlParser: true,
>   useUnifiedTopology: true,
> });
>
> // Models
> const restaurantSchema = new mongoose.Schema({
>   name: String,
>   cuisine: String,
>   address: String,
>   description: String,
>   averageRating: { type: Number, default: 0 },
>   reviewCount: { type: Number, default: 0 },
> });
>
> // Add indexes as per your design
> restaurantSchema.index({ cuisine: 1 });
> restaurantSchema.index({ name: 1 });
>
> const reviewSchema = new mongoose.Schema({
>   restaurant_id: { type: mongoose.Schema.Types.ObjectId, ref: 'Restaurant' },
>   rating: { type: Number, min: 1, max: 5 },
>   reviewText: String,
>   reviewerName: String,
>   createdAt: { type: Date, default: Date.now },
> });
>
> reviewSchema.index({ restaurant_id: 1 });
>
> const Restaurant = mongoose.model('Restaurant', restaurantSchema);
> const Review = mongoose.model('Review', reviewSchema);
>
> // Routes
>
> // GET /api/restaurants - with optional filtering
> app.get('/api/restaurants', async (req, res) => {
>   try {
>     const { cuisine, search } = req.query;
>     let query = {};
>
>     if (cuisine) {
>       query.cuisine = cuisine;
>     }
>     if (search) {
>       query.name = { $regex: search, $options: 'i' }; // case-insensitive search
>     }
>
>     const restaurants = await Restaurant.find(query);
>     res.json(restaurants);
>   } catch (error) {
>     res.status(500).json({ error: 'Server error' });
>   }
> });
>
> // GET /api/restaurants/:id
> app.get('/api/restaurants/:id', async (req, res) => {
>   try {
>     const restaurant = await Restaurant.findById(req.params.id);
>     if (!restaurant) {
>       return res.status(404).json({ error: 'Restaurant not found' });
>     }
>     res.json(restaurant);
>   } catch (error) {
>     res.status(500).json({ error: 'Server error' });
>   }
> });
>
> // GET /api/restaurants/:id/reviews
> app.get('/api/restaurants/:id/reviews', async (req, res) => {
>   try {
>     const reviews = await Review.find({ restaurant_id: req.params.id }).sort({ createdAt: -1 });
>     res.json(reviews);
>   } catch (error) {
>     res.status(500).json({ error: 'Server error' });
>   }
> });
>
> // POST /api/restaurants/:id/reviews
> app.post('/api/restaurants/:id/reviews', async (req, res) => {
>   try {
>     const { rating, reviewText, reviewerName } = req.body;
>
>     // Input validation
>     if (!rating || rating < 1 || rating > 5) {
>       return res.status(400).json({ error: 'Rating must be between 1 and 5' });
>     }
>     if (!reviewText || reviewText.trim() === '') {
>       return res.status(400).json({ error: 'Review text is required' });
>     }
>     if (!reviewerName || reviewerName.trim() === '') {
>       return res.status(400).json({ error: 'Reviewer name is required' });
>     }
>
>     // Check restaurant exists
>     const restaurant = await Restaurant.findById(req.params.id);
>     if (!restaurant) {
>       return res.status(404).json({ error: 'Restaurant not found' });
>     }
>
>     // Create review
>     const review = new Review({
>       restaurant_id: req.params.id,
>       rating,
>       reviewText,
>       reviewerName,
>     });
>     await review.save();
>
>     // Update restaurant's average rating
>     const allReviews = await Review.find({ restaurant_id: req.params.id });
>     const avgRating = allReviews.reduce((sum, r) => sum + r.rating, 0) / allReviews.length;
>
>     restaurant.averageRating = avgRating;
>     restaurant.reviewCount = allReviews.length;
>     await restaurant.save();
>
>     res.status(201).json(review);
>   } catch (error) {
>     res.status(500).json({ error: 'Server error' });
>   }
> });
>
> const PORT = process.env.PORT || 3000;
> app.listen(PORT, () => {
>   console.log(`Server running on port ${PORT}`);
> });
> ```
>
> This implementation:
>
> - Sets up all your designed endpoints
> - Includes input validation (as you noted in your design doc)
> - Calculates average rating on backend (your design decision)
> - Uses appropriate status codes (200, 201, 400, 404, 500)
> - Implements the indexes you specified
> - Handles filtering and search via query parameters
>
> **Next steps:**
>
> 1. Test each endpoint with Postman or curl
> 2. Add some seed data to test filtering/search
> 3. Start building your React frontend
>
> **Questions?**

**Student:**

> This looks great! One question - in the POST /api/restaurants/:id/reviews, you're recalculating the average by fetching all reviews. Is this the most efficient approach, or could I do the math incrementally?

**Claude:**

> Excellent question! You're thinking about performance - that's great. You're right that my current implementation fetches all reviews every time, which could be inefficient if a restaurant has hundreds of reviews.
>
> **Current approach (what I showed):**
>
> ```javascript
> const allReviews = await Review.find({ restaurant_id: req.params.id });
> const avgRating = allReviews.reduce((sum, r) => sum + r.rating, 0) / allReviews.length;
> ```
>
> - Pro: Always accurate, simple logic
> - Con: O(n) database query every time a review is added
>
> **Incremental calculation (more efficient):**
>
> ```javascript
> // Use the existing averageRating and reviewCount to calculate new average
> const oldAvg = restaurant.averageRating;
> const oldCount = restaurant.reviewCount;
> const newCount = oldCount + 1;
> const newAvg = (oldAvg * oldCount + rating) / newCount;
>
> restaurant.averageRating = newAvg;
> restaurant.reviewCount = newCount;
> await restaurant.save();
> ```
>
> - Pro: O(1) calculation, no need to fetch all reviews
> - Con: Prone to rounding errors over time, harder to debug if data gets inconsistent
>
> **Recommendation:**
> For this assignment, **use the incremental approach**. Here's why:
>
> - Demonstrates understanding of algorithmic efficiency
> - Scales better (important if discussing tradeoffs in your reflection)
> - More professional implementation
>
> However, in your reflection document, you should mention:
>
> - Why you chose incremental calculation (performance)
> - The tradeoff (potential precision issues vs. efficiency)
> - That in a production system you might periodically recalculate all averages to fix any drift
>
> Does that make sense? Want to see the updated POST endpoint code?

**Student:**

> Yes, that makes sense! I'll use the incremental approach. Can you show me the updated POST endpoint?

**Claude:**

> Sure! Here's the updated POST endpoint with incremental average calculation:
>
> ```javascript
> app.post('/api/restaurants/:id/reviews', async (req, res) => {
>   try {
>     const { rating, reviewText, reviewerName } = req.body;
>
>     // Input validation
>     if (!rating || rating < 1 || rating > 5) {
>       return res.status(400).json({ error: 'Rating must be between 1 and 5' });
>     }
>     if (!reviewText || reviewText.trim() === '') {
>       return res.status(400).json({ error: 'Review text is required' });
>     }
>     if (!reviewerName || reviewerName.trim() === '') {
>       return res.status(400).json({ error: 'Reviewer name is required' });
>     }
>
>     // Check restaurant exists
>     const restaurant = await Restaurant.findById(req.params.id);
>     if (!restaurant) {
>       return res.status(404).json({ error: 'Restaurant not found' });
>     }
>
>     // Create review
>     const review = new Review({
>       restaurant_id: req.params.id,
>       rating,
>       reviewText,
>       reviewerName,
>     });
>     await review.save();
>
>     // Update restaurant's average rating incrementally
>     const oldAvg = restaurant.averageRating || 0;
>     const oldCount = restaurant.reviewCount || 0;
>     const newCount = oldCount + 1;
>     const newAvg = (oldAvg * oldCount + rating) / newCount;
>
>     restaurant.averageRating = newAvg;
>     restaurant.reviewCount = newCount;
>     await restaurant.save();
>
>     res.status(201).json(review);
>   } catch (error) {
>     res.status(500).json({ error: 'Server error' });
>   }
> });
> ```
>
> Key changes:
>
> - No longer fetching all reviews
> - Uses math formula: `new_avg = (old_avg * old_count + new_rating) / (old_count + 1)`
> - Handles case where restaurant has no reviews yet (|| 0)
>
> **Make sure to document this decision in your reflection!**

[Student continues implementation, building React frontend, testing, etc.]

---

## Phase 3: Automated Grading

### Functional Correctness Autograder (30 points)

```python
import requests
import pytest

BASE_URL = "http://localhost:3000/api"

def test_get_all_restaurants():
    """Test GET /api/restaurants returns all restaurants"""
    response = requests.get(f"{BASE_URL}/restaurants")
    assert response.status_code == 200
    data = response.json()
    assert isinstance(data, list)
    assert len(data) > 0
    assert "name" in data[0]
    assert "cuisine" in data[0]
    # 5 points

def test_filter_by_cuisine():
    """Test filtering restaurants by cuisine"""
    response = requests.get(f"{BASE_URL}/restaurants?cuisine=Italian")
    assert response.status_code == 200
    data = response.json()
    for restaurant in data:
        assert restaurant["cuisine"] == "Italian"
    # 5 points

def test_search_by_name():
    """Test searching restaurants by name"""
    response = requests.get(f"{BASE_URL}/restaurants?search=pizza")
    assert response.status_code == 200
    data = response.json()
    assert len(data) > 0
    # Verify search works (case-insensitive)
    for restaurant in data:
        assert "pizza" in restaurant["name"].lower()
    # 5 points

def test_get_single_restaurant():
    """Test GET /api/restaurants/:id"""
    # First get all restaurants to get an ID
    response = requests.get(f"{BASE_URL}/restaurants")
    restaurants = response.json()
    restaurant_id = restaurants[0]["_id"]

    # Now get single restaurant
    response = requests.get(f"{BASE_URL}/restaurants/{restaurant_id}")
    assert response.status_code == 200
    data = response.json()
    assert data["_id"] == restaurant_id
    # 3 points

def test_get_reviews_for_restaurant():
    """Test GET /api/restaurants/:id/reviews"""
    response = requests.get(f"{BASE_URL}/restaurants")
    restaurant_id = response.json()[0]["_id"]

    response = requests.get(f"{BASE_URL}/restaurants/{restaurant_id}/reviews")
    assert response.status_code == 200
    data = response.json()
    assert isinstance(data, list)
    # 3 points

def test_add_review():
    """Test POST /api/restaurants/:id/reviews creates review and updates rating"""
    response = requests.get(f"{BASE_URL}/restaurants")
    restaurant_id = response.json()[0]["_id"]

    # Get initial review count
    initial_response = requests.get(f"{BASE_URL}/restaurants/{restaurant_id}")
    initial_count = initial_response.json()["reviewCount"]
    initial_avg = initial_response.json()["averageRating"]

    # Add review
    review_data = {
        "rating": 5,
        "reviewText": "Excellent food!",
        "reviewerName": "Test User"
    }
    response = requests.post(f"{BASE_URL}/restaurants/{restaurant_id}/reviews", json=review_data)
    assert response.status_code == 201

    # Verify review was created
    review = response.json()
    assert review["rating"] == 5
    assert review["reviewText"] == "Excellent food!"

    # Verify restaurant's averageRating and reviewCount were updated
    updated_response = requests.get(f"{BASE_URL}/restaurants/{restaurant_id}")
    updated_restaurant = updated_response.json()
    assert updated_restaurant["reviewCount"] == initial_count + 1
    assert updated_restaurant["averageRating"] != initial_avg  # Should have changed
    # 9 points

def test_invalid_review_rating():
    """Test that invalid rating (< 1 or > 5) returns 400"""
    response = requests.get(f"{BASE_URL}/restaurants")
    restaurant_id = response.json()[0]["_id"]

    # Try invalid rating
    review_data = {
        "rating": 6,  # Invalid!
        "reviewText": "Test",
        "reviewerName": "Test"
    }
    response = requests.post(f"{BASE_URL}/restaurants/{restaurant_id}/reviews", json=review_data)
    assert response.status_code == 400
    # 3 points

def test_restaurant_not_found():
    """Test that invalid restaurant ID returns 404"""
    fake_id = "507f1f77bcf86cd799439011"  # Valid ObjectId format but doesn't exist
    response = requests.get(f"{BASE_URL}/restaurants/{fake_id}")
    assert response.status_code == 404
    # 2 points

# Total: 30 points for functional correctness
```

### API Design Quality Autograder (15 points)

```python
def test_rest_conventions():
    """Verify REST conventions are followed"""
    response = requests.get(f"{BASE_URL}/restaurants")

    # Check GET returns 200
    assert response.status_code == 200

    # Check POST returns 201
    restaurant_id = response.json()[0]["_id"]
    review_data = {"rating": 4, "reviewText": "Good", "reviewerName": "Tester"}
    post_response = requests.post(f"{BASE_URL}/restaurants/{restaurant_id}/reviews", json=review_data)
    assert post_response.status_code == 201
    # 5 points

def test_response_format():
    """Check that responses are properly formatted JSON"""
    response = requests.get(f"{BASE_URL}/restaurants")
    data = response.json()

    # Verify structure
    assert isinstance(data, list)
    for restaurant in data:
        assert "_id" in restaurant
        assert "name" in restaurant
        assert "averageRating" in restaurant
        assert "reviewCount" in restaurant
    # 5 points

def test_error_handling():
    """Verify proper error responses"""
    # 404 for non-existent restaurant
    response = requests.get(f"{BASE_URL}/restaurants/507f1f77bcf86cd799439011")
    assert response.status_code == 404
    assert "error" in response.json()

    # 400 for bad request
    response = requests.post(f"{BASE_URL}/restaurants/507f1f77bcf86cd799439011/reviews",
                            json={"rating": 10})
    assert response.status_code == 400
    assert "error" in response.json()
    # 5 points

# Total: 15 points for API design quality
```

### Code Quality Autograder (10 points)

```python
import ast
import subprocess

def test_no_sql_injection():
    """Check that student code doesn't have SQL injection vulnerabilities"""
    # For MongoDB, check they're using Mongoose queries, not raw string concatenation
    with open("server.js", "r") as f:
        code = f.read()
        # Bad pattern: db.collection.find("name: '" + userInput + "'")
        assert "find(\"" not in code or "+ req." not in code
        # Good pattern: using Mongoose query objects
        assert "find({" in code or "findById" in code
    # 5 points

def test_input_validation():
    """Verify input validation is present"""
    with open("server.js", "r") as f:
        code = f.read()
        # Check for validation keywords
        assert "if (!rating" in code or "if (rating <" in code
        assert "if (!reviewText" in code
    # 3 points

def test_proper_error_handling():
    """Check that endpoints have try-catch blocks"""
    with open("server.js", "r") as f:
        code = f.read()
        # Should have error handling
        assert "try {" in code
        assert "catch" in code
        assert "res.status(500)" in code or "status(400)" in code
    # 2 points

# Total: 10 points for code quality
```

### Testing Quality Autograder (10 points)

```python
def test_student_has_tests():
    """Check that student submitted tests"""
    # Run student's test file
    result = subprocess.run(["npm", "test"], capture_output=True)
    assert result.returncode == 0  # Tests should pass
    # 5 points

def test_sufficient_coverage():
    """Check test coverage"""
    result = subprocess.run(["npm", "run", "coverage"], capture_output=True)
    output = result.stdout.decode()
    # Look for coverage percentage (this is simplified)
    # Real implementation would parse coverage report
    assert "Statements" in output
    # Award points based on coverage level
    # 5 points for >= 70% coverage
```

### Reflection Document Grading (Claude API) - 15 points

```python
def grade_reflection(reflection_doc, student_code):
    """Use Claude API to grade reflection document"""

    prompt = f"""You are grading a CS 260 student's reflection on their restaurant review app project.

The student was allowed to use Claude (an AI assistant) during design and implementation.

STUDENT'S REFLECTION:
{reflection_doc}

STUDENT'S CODE (for reference):
{student_code}

RUBRIC (15 points):
1. Design Decision Explanation (5 pts): Do they clearly explain key architectural decisions?
2. Claude Usage Reflection (5 pts): Do they thoughtfully discuss how Claude helped and where it was limited?
3. Technical Understanding (5 pts): Does reflection demonstrate genuine understanding vs. surface-level description?

Evaluate:
- Do they explain WHY they made specific choices (not just WHAT they did)?
- Do they discuss challenges encountered and how they solved them?
- Do they reflect critically on AI assistance (both benefits and limitations)?
- Does the reflection match the code (are they describing what they actually built)?

Return JSON:
{{
    "design_decisions": {{
        "score": <0-5>,
        "feedback": "<specific feedback>"
    }},
    "claude_usage": {{
        "score": <0-5>,
        "feedback": "<specific feedback>"
    }},
    "technical_understanding": {{
        "score": <0-5>,
        "feedback": "<specific feedback>"
    }},
    "total_score": <sum>,
    "overall_feedback": "<summary>"
}}
"""

    response = claude_api.messages.create(
        model="claude-3-5-sonnet-20241022",
        max_tokens=1500,
        messages=[{"role": "user", "content": prompt}]
    )

    return json.loads(response.content[0].text)
```

**Example Student Reflection:**

```markdown
# Reflection: Restaurant Review App

## Design Decisions

### React vs. Vanilla JavaScript

I chose React because I wanted to focus on application architecture rather than DOM manipulation. The component-based structure made it easy to build reusable RestaurantCard and ReviewCard components. In hindsight, this was the right choice - I was able to build a more sophisticated UI with less code than vanilla JS would have required.

### Database Schema

I used separate collections for restaurants and reviews rather than embedding reviews in restaurant documents. This decision was based on scalability - if a popular restaurant has thousands of reviews, an embedded approach would make the restaurant document huge and slow to query.

One challenge I encountered: initially I was recalculating average ratings by fetching all reviews every time. Claude suggested an incremental calculation approach, which I implemented. However, I realized this could lead to rounding errors over time. In a production system, I'd add a periodic batch job to recalculate all averages to fix any drift.

### API Design

I used query parameters (?cuisine=Italian) for filtering instead of separate endpoints. This kept the API clean and allowed combining filters easily.

## How Claude Helped (and Where It Didn't)

### Where Claude Was Helpful:

- **Boilerplate code**: Claude generated the initial Express server structure, Mongoose schemas, and route handlers. This saved significant time.
- **Design discussion**: Talking through architecture decisions with Claude helped me think through tradeoffs (embedded vs. separate collections, frontend vs. backend rating calculation).
- **Debugging**: When my average rating calculation wasn't updating correctly, Claude helped me identify that I wasn't saving the restaurant model after updating it.

### Where Claude Was Limited:

- **UI Design**: Claude could generate React components, but couldn't help me decide on the visual design or UX flow. I had to make those decisions myself.
- **Testing edge cases**: Claude suggested basic tests, but I had to think through edge cases like "what happens if restaurant has zero reviews?" myself.
- **Understanding my specific data**: When debugging, Claude gave general advice, but I had to actually examine my database and console logs to understand what was wrong.

### Critical Reflection on AI Usage:

Using Claude was like having an experienced developer to discuss ideas with, but I still had to make all the decisions and understand the code. I couldn't just copy-paste - I had to understand WHY the suggested approaches worked. For example, when Claude suggested the incremental average calculation, I had to work through the math myself to understand it.

The biggest risk I noticed: it's tempting to just accept Claude's suggestions without thinking critically. I had to constantly ask myself "Why this approach?" and "What are the tradeoffs?" to avoid shallow learning.

## Challenges and Solutions

### Challenge 1: CORS Errors

Initially, my React frontend couldn't communicate with the Express backend due to CORS errors. Claude suggested adding the cors middleware, which fixed it. However, I then researched CORS to understand WHY it was needed (browser security).

### Challenge 2: Mongoose ObjectId Validation

When testing with invalid restaurant IDs, my server was crashing instead of returning 404. I had to add error handling for Mongoose CastError when an invalid ObjectId format is provided.

### Challenge 3: Real-Time Average Rating Updates

I wanted the UI to immediately show the new average after adding a review, without refreshing. I had to implement state management in React to update the restaurant detail view after the POST request completed.

## What I Learned

- **Design matters**: The time spent on design (schema, API endpoints, component architecture) made implementation much smoother.
- **Tradeoffs are everywhere**: Embedded vs. separate collections, incremental vs. full recalculation, frontend vs. backend logic - every decision has pros and cons.
- **AI is a tool, not a replacement**: Claude accelerated my work, but I still had to understand the code, make decisions, and solve problems Claude couldn't anticipate.
- **Testing reveals assumptions**: Writing tests exposed edge cases I hadn't considered (empty reviews, invalid IDs, etc.).
```

**Claude's Assessment:**

```json
{
  "design_decisions": {
    "score": 5,
    "feedback": "Excellent explanation of design decisions with clear justification. Student explains React choice with specific reasoning, discusses database schema tradeoffs (embedded vs. separate collections with scalability justification), and shows awareness of the average rating calculation tradeoff (incremental efficiency vs. potential drift). The mention of adding a batch job to fix drift shows mature engineering thinking. API design reasoning is clear and practical."
  },
  "claude_usage": {
    "score": 5,
    "feedback": "Outstanding critical reflection on AI usage. Student clearly articulates where Claude helped (boilerplate, design discussion, debugging) and where it was limited (UI/UX, edge cases, specific data understanding). Most importantly, the 'Critical Reflection' section shows genuine awareness of the risks of over-relying on AI ('tempting to just accept suggestions without thinking critically'). The student demonstrates they actively questioned AI suggestions and verified understanding. This is exactly the kind of thoughtful AI usage we want to see."
  },
  "technical_understanding": {
    "score": 5,
    "feedback": "Demonstrates deep understanding of the technical concepts. The CORS challenge shows they didn't just apply a fix but researched why it was needed. The Mongoose CastError handling shows attention to error cases. The real-time UI update challenge demonstrates understanding of state management. The discussion of rounding errors in incremental calculation and the batch job solution shows sophisticated thinking about production systems. Reflection matches the code and goes beyond surface-level description to discuss underlying concepts and tradeoffs."
  },
  "total_score": 15,
  "overall_feedback": "Exceptional reflection document. You demonstrate genuine understanding of your design decisions, critical thinking about tradeoffs, and thoughtful use of AI assistance. Your awareness of both the benefits and limitations of Claude shows mature engineering judgment. The specific examples (CORS, ObjectId validation, state management) demonstrate real problem-solving. Your point about AI being 'a tool, not a replacement' and the need to constantly ask 'Why?' is exactly right. This is a model reflection - you clearly learned from this project and can articulate your learning. Excellent work!"
}
```

**Grade: 15/15**

---

## Final Grade Summary

| Component                           | Points  | Student Score |
| ----------------------------------- | ------- | ------------- |
| Design Document (Claude-graded)     | 20      | 19            |
| Functional Correctness (Autograder) | 30      | 30            |
| API Design Quality (Autograder)     | 15      | 15            |
| Code Quality (Autograder)           | 10      | 10            |
| Testing (Autograder)                | 10      | 8             |
| Reflection (Claude-graded)          | 15      | 15            |
| **TOTAL**                           | **100** | **97**        |

## Key Takeaways from This Assignment Model

### For Students:

1. Claude is available to discuss design decisions and help with implementation
2. Students must explain and justify choices - can't just submit AI-generated code
3. Multi-dimensional assessment (design + implementation + reflection) prevents shallow learning
4. Reflection requirement encourages metacognition about AI usage

### For Faculty:

1. Autograding handles functional testing at scale (1,500 students)
2. Claude API grades subjective components (design doc, reflection)
3. Total grading time per student: < 5 minutes for spot-checks
4. Students receive detailed feedback on all components

### For the Department:

1. Scalable to large enrollment courses
2. Tests understanding, not just code generation
3. Prepares students for AI-augmented professional work
4. Maintains academic rigor in the AI era
