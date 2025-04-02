#Table of Content
1. [requirement Analysis](requirement.md)
2. [system Analysis]

    2.1 [System Architecture](system-analysis/Architecture.mmd)

     2.2 [use cases](system-analysis/usecase.mmd)
     ### Book Test Drive  
- **Actor**: User  
- **Steps**:  
  1. User requests test drive.  
  2. System checks availability.  
  3. User selects slot → Database updates.  
- **Exception**: No slots → Suggest alternatives.  
2.3 [ER Diagram](system-analysis/er.mmd)

NLP extracts intent and parameters → Saved in QUERY.

Chatbot joins QUERY with CAR/DEALERSHIP to generate a response.

User Books a Test Drive:

Inserts into TEST_DRIVE → Updates CAR.availability_status.

Admin Updates Inventory:

Modifies CAR table → Chatbot reflects changes in real-time.
2.4 [ER Diagram Detailed](system-analysis/erddetailed.mmd)
Key Chatbot-Specific Entities
CHATBOT_SESSION

Tracks active user conversations (session_id, timestamps).

Links to QUERY for audit logging.

QUERY

Stores NLP-processed intents (e.g., ask_price) and parameters (e.g., {"make": "Audi"}).

Maps to CAR or DEALERSHIP for responses.

USER

Minimal info (phone number for bookings). No passwords needed (chatbot uses messaging platforms).

2.4 DFDs
2.4.1 [0-level DFD](system-analysis/dfd0level.mmd)

/n
2.4.2 [1-level DFD](system-analysis/dfdlevel1.mmd)
Key Components Explained
1. External Entities
User: Submits queries via chat (text input).

Admin: Updates inventory/dealership data.

Inventory System: Database of cars (prices, specs).

Booking Calendar: Manages test drive slots.

2. Chatbot Processes
Process	Description	Example
1. Process Query	Receives raw user input (text).	"Price of Audi A3?"
2. Classify Intent	Uses NLP (Rasa/DialogFlow) to detect intent (ask_price, book_test_drive).	Intent: ask_price
3. Retrieve Data	Fetches from DB/APIs based on intent.	SQL: SELECT price FROM cars...
4. Generate Response	Formats data into user-friendly text.	"Audi A3: £25,000"
5. Log Interaction	Stores queries/responses for analytics.	Log: {query: 'price', time:...}
3. Data Stores
Inventory System: Structured DB (PostgreSQL) with car details.

Logs: MongoDB/JSON files for conversation history.


2.4.3 [level-2 DFD](system-analysis/level2dfd.mmd)
Rules & Constraints
Closed-Domain Flow:

If intent ≠ (ask_price|book_test_drive|ask_location), respond: "I can only help with car-related queries."

Data Validation:

Before booking: Check Inventory.availability_status = TRUE.

Error Handling:

DB unreachable → "Sorry, I can’t access data right now. Try later."
P1["1. Process Query"]

Receives raw user input (e.g., "What's the price of an Audi A3?").

Passes the text to preprocessing.

P2A["2.1 Preprocess Text"]

Removes stopwords: Filters out words like "what's," "the," "of."

Tokenizes: Splits the sentence into tokens: ["price", "Audi", "A3"].

Output: Cleaned text → "price Audi A3".

P2B["2.2 Predict Intent"]

NLP model (e.g., Rasa/Dialogflow) classifies the intent as ask_price.

P2C["2.3 Extract Entities"]

Extracts key parameters (entities) from the text:

car_model = "A3"

car_make = "Audi" (if your model detects it).

Output: Structured JSON → { "intent": "ask_price", "entities": { "model": "A3", "make": "Audi" } }.

P3["3. Retrieve Data"]

Uses the extracted parameters to query the database:

sql
Copy
SELECT price FROM cars WHERE make = 'Audi' AND model = 'A3';



2.5 [sequence Diagram](system-analysis/sequence.mmd)

[sequence Diagram Error Handling ](system-analysis/sequenceError.mmd)

2.6 [Class Diagram](system-analysis/class.mmd) 
Key Classes Explained
1. User
Attributes:

sessionId: Unique ID for each chat session.

phoneNumber: User identifier (if using SMS/WhatsApp).

queryHistory: Logs past interactions.

Methods:

startChatSession(): Initiates a new conversation.

2. Chatbot (Orchestrator)
Attributes:

currentState: Tracks conversation state (e.g., "awaiting_test_drive_date").

Methods:

processQuery(): Delegates to NLPEngine and InventoryDB.

generateResponse(): Formats replies based on intent/entities.

3. NLPEngine
Methods:

classifyIntent(): Returns ask_price, book_test_drive, etc.

extractEntities(): Parses { "make": "Audi", "model": "A3" }.

4. Car
Attributes:

Standard car details + availability flag.

Methods:

getPrice(), checkAvailability(): Called by InventoryDB.

5. TestDriveBooking
Methods:

bookSlot(): Validates availability and creates booking.

cancelBooking(): Updates status.

6. InventoryDB
Methods:

searchCars(): Retrieves cars by make/model (used for price queries).

updateCar(): Modifies availability after bookings.

Relationships
Relationship	Description
User → Chatbot	A user can have multiple chat sessions.
Chatbot → NLPEngine	Delegates NLP tasks.
Chatbot → InventoryDB	Fetches car data.
TestDriveBooking → Car	Links bookings to specific cars.
How This Aligns with Your System
Closed-Domain Focus:

Only car-related classes (Car, TestDriveBooking) are included.

No generic "Conversation" class (since your chatbot is task-specific).

Retrieval-Based Design:

InventoryDB.searchCars() handles price/availability queries.

No generative AI methods (e.g., generateCarDescription()).

Scalability:

NLPEngine can be swapped (e.g., Rasa → Dialogflow) without changing other classes.


