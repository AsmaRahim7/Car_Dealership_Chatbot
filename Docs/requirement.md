
Requirement Analysis 
Chatbot:
Chatbots are the automated online helpers who can guide you for the system, products and take some complaints and suggestion from user for the system. 
Our chatbot will be based on car dealership website (https://oxfordwheels.co.uk/) and respond to user requests for the system by interacting with them. 
Key features of chatbot
NLP, context aware, intent aware, and closed domain (only focused on cars business)
Goal of chat bot is chat/conversation based, e.g asking car model, car price, 
This chatbot will work on retrieval based model means that it will see the user request and retrieve from website to response

Here’s a refined **Requirement Analysis** section for your car dealership AI chatbot project, incorporating closed-domain, retrieval-based functionality and modern software engineering practices:

---
Requirement Analysis for Car Dealership Chatbot

Purpose
To develop a **closed-domain, retrieval-based AI chatbot** for a car dealership website that assists users with inquiries about car models, pricing, features, dealership information, bookings, and feedback. The chatbot will leverage NLP to understand user intent, maintain context-aware conversations, and retrieve accurate responses from the dealership’s website/database.  

---

Stakeholders
1. **Car Dealership Business**: To automate customer support and improve user engagement.  
2. **End Users (Customers)**: To quickly find car details, pricing, and dealership services.  
3. **Developers/Admin**: To maintain, monitor, and improve the chatbot.  
4. **Support Team**: To handle escalated queries or complaints. 

Functional Requirements 
1. Core Chatbot Features  
   - Closed-Domain Focus:  
     - Handle queries only related to cars, dealership services, and promotions.  
     - Topics: Car models, prices, features (mileage, engine specs), test drives, dealership locations, and operating hours.  
   - Retrieval-Based Responses:  
     - Fetch answers from a structured knowledge base (e.g., dealership website content, product database, FAQs).  
   - Intent Recognition:  
     - Classify user intents (e.g., `inquire_price`, `book_test_drive`, `ask_features`).  
   - Context Awareness:  
     - Maintain conversation context (e.g., "What’s the price of Model X?" → "Is it available in red?").  

2. User Interaction  
   - Multi-Turn Dialogues: Allow follow-up questions without restating context.  
   - Feedback Collection: Capture user ratings/complaints for continuous improvement.  
   - Fallback Mechanism: Escalate unresolved queries to human agents.  

3. Integration Requirements 
   - Embed the chatbot into the dealership’s website using a JavaScript widget or API.  
   - Sync with the dealership’s inventory database for real-time updates (e.g., car availability).  

---

Non-Functional Requirements 
1. Performance:  
   - Response time < 2 seconds for 95% of queries.  
   - Handle 100+ concurrent users during peak traffic.  
2. Security:  
   - Encrypt user data (e.g., contact details for test drive bookings).  
   - Comply with GDPR/CCPA for data privacy.  
3. Scalability:  
   - Deploy on cloud infrastructure (AWS/Azure) with auto-scaling.  
4. Usability:  
   - Simple, intuitive interface matching the dealership’s website design.  
   - Support text and button-based interactions.  
5. Reliability:  
   - 99.9% uptime with monitoring/alerts (e.g., Prometheus + Grafana).  

---


Use Cases 

| **User Action**               | **Chatbot Response**|--------------------------------|-------------------------------------------------------------------------------------|  
| Ask about car prices           | Retrieve price from the database and display discounts/financing options.            |  
| Inquire about car features     | List specifications (engine, mileage, safety) from the product catalog.            |  
| Book a test drive              | Collect user details (name, contact) and confirm via email/SMS.                     |  
| Request dealership location       | Provide address, map link, and operating hours.                                    |  
| Submit feedback                  | Store feedback in a CRM (e.g., Salesforce) and thank the user.                     |  

---
Data Sources
1. Structured Data:  
   - Car inventory database (models, prices, features).  
   - Dealership info (locations, staff contacts).  
2. Unstructured Data:  
   - FAQ documents, brochures, and website content.  
   - Historical chat logs for improving intent classification.  

---

Technical Requirements
1. NLP Pipeline:  
   - Use Rasa or Dialogflow for intent recognition and entity extraction.  
   - Preprocess text with SpaCy (tokenization, lemmatization).  
2. Backend:  
   - Python/Node.js API to handle requests and query the database.  
   - Database: PostgreSQL for structured data, Elasticsearch for fast retrieval.  
3. Frontend:  
   - Lightweight JavaScript widget for website integration.  
   - Admin dashboard (React) to view chat logs and analytics.  
4. Deployment:  
   - Containerize with Docker and orchestrate with Kubernetes  
   - CI/CD pipeline using GitHub Actions(automate testing and deployment).  

---

Tools & Practices 
1. Version Control:  
   - Host code on GitHub with branches: `main`, `develop`, `feature/retrieval-engine`.  
   - Enforce pull requests and code reviews.  
2. Documentation:  
   - Wiki for setup instructions, API docs (Swagger), and user guides.  
3. Testing:  
   - Unit tests (Pytest), integration tests (Postman), and load testing (Locust).  
4. Monitoring:  
   - Log errors with ELK Stack (Elasticsearch, Logstash, Kibana).  
   - Track performance metrics (latency, error rates) in Grafana.  

—
Key Challenges
1. Ensuring accurate intent classification for car-specific jargon (e.g., "MPG," "torque").  
2. Synchronizing real-time inventory data with the chatbot’s responses.  
3. Balancing retrieval-based responses with conversational fluency.  

--- 
This requirement analysis sets the foundation for your project, aligning with modern practices like Agile, DevOps, and MLOps. Next steps: System design, sprint planning, and prototyping!
