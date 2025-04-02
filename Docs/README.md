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
