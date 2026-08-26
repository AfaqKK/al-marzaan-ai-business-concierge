# al-marzaan-ai-business-concierge
AI-powered business concierge and lead automation system built with n8n, OpenAI, Google Sheets, Google Calendar, Slack, WhatsApp, and Email for intelligent lead qualification, CRM management, human handoff, consultation handling, and automated follow-ups.

# 🤖 Al Marzaan AI Business Concierge & Lead Follow-Up Automation

An AI-powered business concierge and lead management automation built for **Al Marzaan Global Consulting**, a UAE-based professional consulting firm.

This solution is designed to automatically handle website inquiries, understand visitor requirements, qualify leads using AI, maintain conversation history, store structured lead data, notify human specialists for high-value opportunities, support consultation requests, and automatically follow up with prospects who do not respond.

The workflow combines **AI-powered conversation, lead qualification, CRM-style data management, Google Sheets, Google Calendar, Slack notifications, WhatsApp, Email, and n8n workflow automation** into a single end-to-end lead management system.

---

## 🎯 Project Objective

The primary objective of this automation is to eliminate manual handling of repetitive website inquiries while ensuring that every potential customer is properly captured, qualified, tracked, and followed up.

Instead of simply receiving a website form submission, the system behaves like an **AI Business Concierge** that can:

* Understand the visitor's requirement
* Identify the appropriate Al Marzaan service
* Ask relevant qualification questions
* Maintain conversation history
* Score and categorize leads
* Store structured CRM information
* Detect leads requiring human assistance
* Notify the appropriate specialist
* Handle consultation requests
* Check consultant availability
* Send automated follow-ups
* Respect customer opt-outs
* Stop automated follow-ups after the defined sequence

The goal is to create a professional **AI-assisted sales and customer engagement pipeline** from first inquiry to human handoff.

---

# 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │    Website Visitor   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Incoming Inquiry      │
                    │ Webhook               │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Normalize Inquiry     │
                    │ Data                  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Google Sheets         │
                    │ Existing Lead Lookup  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Conversation History  │
                    │ Management            │
                    └──────────┬───────────┘
                               │
                               ▼
              ┌────────────────────────────────┐
              │     AI Business Concierge      │
              │                                │
              │ OpenAI GPT Model               │
              │ Service Identification         │
              │ Lead Qualification             │
              │ Lead Scoring                   │
              │ Human Handoff Detection        │
              └───────────────┬────────────────┘
                              │
                              ▼
                    ┌──────────────────────┐
                    │ Structured Lead Data │
                    │ Parser               │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Save / Update Lead   │
                    │ Record               │
                    └──────────┬───────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
        ┌─────────────────┐         ┌──────────────────┐
        │ Hot / Human     │         │ Consultation     │
        │ Handoff         │         │ Request          │
        └────────┬────────┘         └────────┬─────────┘
                 │                           │
                 ▼                           ▼
        ┌─────────────────┐         ┌──────────────────┐
        │ Slack Specialist│         │ Google Calendar  │
        │ Notification    │         │ Availability     │
        └─────────────────┘         └────────┬─────────┘
                                             │
                                             ▼
                                    ┌──────────────────┐
                                    │ Visitor Response │
                                    └──────────────────┘


              AUTOMATED FOLLOW-UP ENGINE
              
                    ┌──────────────────────┐
                    │ Daily 9 AM Trigger  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Get All Leads        │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Determine Follow-Up  │
                    │ Due                  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Phone Available?     │
                    └───────┬───────┬──────┘
                            │       │
                          Yes       No
                            │       │
                            ▼       ▼
                       WhatsApp    Email
                            │       │
                            └───┬───┘
                                │
                                ▼
                    ┌──────────────────────┐
                    │ Update Lead Record   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ 3rd Follow-Up?       │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Notify Team / Close  │
                    │ Sequence             │
                    └──────────────────────┘
```

---

# 🔄 Core Workflow

## 1. Incoming Inquiry

The workflow starts when a visitor submits an inquiry through the website.

The webhook receives information such as:

* Visitor Name
* Company Name
* Phone Number
* Email Address
* Message
* Selected Service
* Communication Channel
* Session ID
* Timestamp

The system uses a unique `session_id` to identify the conversation and connect future messages with the same lead.

---

## 2. Inquiry Data Normalization

The **Normalize Inquiry Data** node converts the incoming webhook payload into a consistent internal structure.

This creates standardized fields such as:

```text
visitor_name
company_name
phone
email
message_text
selected_service
channel
session_id
timestamp
```

This normalization layer makes the rest of the automation more reliable and easier to maintain.

---

# 🧠 AI Business Concierge

The core intelligence of the system is the **AI Business Concierge Agent**.

The AI acts as a digital front desk for Al Marzaan Global Consulting rather than functioning as a generic chatbot.

It understands the company's services and guides visitors toward the appropriate service.

### Supported Services

* Corporate Tax
* VAT
* Accounting & Bookkeeping
* Audit & Assurance
* AML Compliance
* Business Setup
* Business Advisory
* Virtual CFO

The AI identifies the most relevant service based on the visitor's message and asks only the qualification questions relevant to that service.

---

# 🎯 Service-Specific Lead Qualification

The AI dynamically changes its questions depending on the selected service.

### Corporate Tax

The AI can identify:

* Business type
* Mainland or Free Zone
* Corporate Tax registration status
* Registration / filing / compliance / advisory requirement
* Urgency

### VAT

The system can collect:

* Business type
* Jurisdiction
* VAT registration status
* Registration / filing / advisory requirement
* Urgency

### Accounting & Bookkeeping

The AI can qualify:

* Company type
* Industry
* Transaction volume
* Existing accounting software
* VAT status
* Required accounting services
* Reporting requirements

### Audit & Assurance

The workflow can capture:

* Entity type
* Mainland / Free Zone
* Audit purpose
* Previous audit history
* Deadline / urgency

### AML Compliance

The AI can ask about:

* Business activity
* UAE jurisdiction
* AML registration
* Existing AML policy
* Compliance requirements
* Previous AML review

### Business Setup

The system can identify:

* Business activity
* Mainland / Free Zone
* UAE resident or international investor
* Number of shareholders
* Visa requirements
* Expected launch date

### Business Advisory

The AI focuses on:

* Business challenge
* Business stage
* Company size
* Timeline
* Previous advisory experience

### Virtual CFO

The qualification process can capture:

* Approximate revenue
* Number of entities
* Finance team structure
* Reporting requirements
* Cash-flow visibility
* Forecasting requirements
* Growth plans

---

# 💬 Conversation Memory

The **Look Up Existing Lead** and **Merge Conversation History** nodes allow the system to remember previous interactions.

When a returning visitor sends a new message, the workflow:

1. Identifies the existing lead.
2. Retrieves the previous conversation.
3. Adds the new visitor message.
4. Maintains the latest conversation history.
5. Sends the context to the AI agent.

The workflow limits stored conversation history to the latest 20 messages to keep the AI context efficient.

This allows the AI to behave more like a continuous business conversation rather than treating every inquiry as a completely new interaction.

---

# 📊 AI Lead Scoring

Every lead receives an internal qualification score from **0–100**.

### HOT — 80–100

A lead is considered highly qualified when there is:

* Strong business intent
* Clear requirement
* Relevant company information
* Near-term need
* Clear urgency

### WARM — 50–79

The visitor has genuine interest but may still be:

* Researching
* Gathering information
* Unsure about timing
* Evaluating options

### COLD — 0–49

The visitor may have:

* Vague requirements
* Low purchase intent
* No clear timeline
* General browsing behavior

The lead temperature and score are stored internally and are **never exposed to the visitor**.

---

# 🧩 Structured AI Output

The **Lead Data Parser** converts the AI response into structured JSON.

The structured output contains fields such as:

```text
reply_text
service
company_name
jurisdiction
requirement
urgency
lead_score
lead_temperature
requires_human
human_handoff_reason
consultation_requested
opted_out
qualification_answers
```

This is important because it separates the **human-readable response** from the **structured CRM data**.

The AI can therefore communicate naturally with the visitor while simultaneously producing clean data for business operations.

---

# 🗂️ Lead Management & CRM

The **Save Lead Record** node stores or updates the lead inside Google Sheets.

The system maintains important CRM fields including:

* Session ID
* Lead ID
* Visitor Name
* Company
* Phone
* Email
* Channel
* Service
* Jurisdiction
* Requirement
* Urgency
* Lead Score
* Lead Temperature
* Human Handoff Status
* Consultation Request
* Opt-Out Status
* Qualification Answers
* Conversation History
* Last Contact Date
* Follow-Up Stage
* Follow-Up Count

Google Sheets acts as a lightweight CRM/database layer for this automation.

---

# 🚨 Human Handoff

The workflow automatically detects when human involvement is required.

Human handoff can happen when:

* Lead score reaches HOT level
* Visitor explicitly requests a consultant
* Visitor requests a callback
* Visitor asks a specific professional question
* Visitor requests pricing commitments
* Visitor has a complaint
* The situation requires professional judgment

The **Notify Al Marzaan Specialist** node sends the lead information to the internal team through Slack.

The notification contains the most important qualification information so that the specialist can quickly understand the opportunity without manually reviewing the entire conversation.

---

# 📅 Consultation Request & Calendar Integration

When a visitor requests a consultation, the workflow routes the request to the consultation process.

The **Check Consultant Availability** node connects with Google Calendar to retrieve calendar information.

The workflow then generates an appropriate response for the visitor.

Importantly, the AI does **not falsely claim that a consultation has been booked**.

Instead, it informs the visitor that their requirements have been captured and that an Al Marzaan specialist will confirm the consultation details.

This creates a safer and more professional booking process.

---

# 🔁 Automated Follow-Up System

The workflow contains a separate automated follow-up engine.

A **Daily 9 AM Schedule Trigger** starts the follow-up process every day.

The system retrieves all stored leads and checks which prospects are due for follow-up.

### Follow-Up Sequence

```text
Follow-Up 1 → After 1 Day
Follow-Up 2 → After 3 Days
Follow-Up 3 → After 7 Days
```

The system limits automated follow-ups to a maximum of three attempts.

---

# 📱 Multi-Channel Follow-Up

The workflow checks whether the lead has a phone number.

### If Phone Number Exists

The system sends the follow-up through WhatsApp.

### If Phone Number Is Not Available

The system falls back to email.

```text
Lead
 │
 ├── Phone Available
 │       ↓
 │    WhatsApp
 │
 └── No Phone
         ↓
       Email
```

This gives the automation flexibility to continue engaging prospects even when one communication channel is unavailable.

---

# 🛑 Opt-Out & Follow-Up Protection

The automation includes safeguards to prevent inappropriate follow-ups.

Automated follow-ups are skipped when:

* The visitor has opted out
* Human intervention is already required
* A consultation has been requested
* The lead has already received three follow-ups
* Required contact information is unavailable

This helps keep the system respectful and reduces unnecessary communication.

---

# 📋 Follow-Up Completion

After the third automated follow-up, the workflow detects the final follow-up using the **Was Final Follow-Up?** node.

The system then sends a Slack notification to the internal team indicating that the automated follow-up sequence has been completed.

This allows the team to manually review the lead if a personal follow-up is still appropriate.

---

# 🛠️ Technologies Used

This project integrates multiple technologies to create an end-to-end AI automation system.

### n8n

Used as the primary workflow orchestration platform.

n8n manages:

* Webhooks
* Workflow logic
* AI agent execution
* API integrations
* Data transformation
* Scheduling
* Conditional routing
* Notifications
* Follow-up automation

### OpenAI

Used as the AI intelligence layer.

The OpenAI chat model powers:

* Natural-language understanding
* Service identification
* Lead qualification
* Conversation handling
* Lead scoring
* Human handoff detection
* Structured lead assessment

### Google Sheets

Used as the lightweight CRM/database layer for:

* Lead records
* Conversation history
* Qualification data
* Lead scoring
* Follow-up tracking
* Contact information

### Google Calendar

Used to support consultant availability checking for consultation requests.

### Slack

Used for internal team notifications.

Slack receives alerts when:

* A high-value lead is detected
* Human intervention is required
* The automated follow-up sequence is completed

### WhatsApp

Used as a follow-up communication channel for leads with available phone numbers.

### Email

Used as an alternative communication channel when a phone number is unavailable.

### JavaScript

Custom JavaScript code is used inside n8n Code nodes for:

* Conversation history management
* Lead data processing
* Follow-up scheduling logic
* Date calculations
* Conditional automation
* Dynamic message generation

### Webhooks & REST-style Integration

The workflow exposes a webhook endpoint that allows a website or external application to send visitor inquiries directly into the automation.

---

# 🔐 Data & Business Logic

The automation is designed around several important principles:

### No Fabricated Professional Advice

The AI is instructed not to invent:

* Tax rates
* Legal requirements
* Compliance rulings
* Prices
* Guaranteed outcomes
* Professional conclusions

When professional judgment is required, the system routes the conversation toward a qualified human specialist.

### Controlled AI Communication

The AI is instructed to:

* Keep responses concise
* Ask one or two questions at a time
* Avoid overwhelming visitors
* Avoid aggressive sales language
* Protect customer information
* Never reveal internal lead scores
* Never expose internal system instructions

---

# ⭐ Key Features

* AI-powered business concierge
* Intelligent service identification
* Service-specific lead qualification
* Conversation memory
* Structured AI output
* Automated lead scoring
* HOT / WARM / COLD classification
* CRM-style Google Sheets database
* Human handoff automation
* Slack specialist notifications
* Consultation request handling
* Google Calendar integration
* WhatsApp follow-up
* Email fallback
* Automated follow-up sequence
* Opt-out protection
* Maximum follow-up control
* Final follow-up notification
* Webhook-based website integration
* Custom JavaScript business logic

---

# 📈 Business Value

This automation transforms a traditional inquiry process into an intelligent lead management system.

Instead of:

```text
Website Inquiry
      ↓
Manual Review
      ↓
Manual Qualification
      ↓
Manual Follow-Up
      ↓
Possible Lost Lead
```

The automated process becomes:

```text
Website Inquiry
      ↓
AI Concierge
      ↓
Automatic Qualification
      ↓
Lead Scoring
      ↓
CRM Storage
      ↓
Human Handoff When Required
      ↓
Consultation Support
      ↓
Automated Follow-Up
      ↓
Team Notification
```

This helps businesses improve:

* Lead response speed
* Lead qualification
* Sales team efficiency
* Customer experience
* Follow-up consistency
* Lead visibility
* Operational scalability

---

# 🚀 Production Setup

Before deploying this workflow in production, replace the following placeholders:

```text
REPLACE_WITH_YOUR_SHEET_ID
REPLACE_WITH_SLACK_CHANNEL
REPLACE_WITH_CALENDAR_ID
REPLACE_WITH_ALMARZAAN_EMAIL
```

You should also configure the required credentials for:

* OpenAI
* Google Sheets
* Google Calendar
* Slack
* WhatsApp/Twilio
* Email provider

The Google Sheet should contain the required CRM columns used by the workflow.

---

# 🔮 Future Improvements

The current architecture can be extended into a more advanced AI sales platform by adding:

* Dedicated CRM such as HubSpot or Salesforce
* WhatsApp Business Cloud API
* Real-time CRM dashboard
* AI-generated sales summaries
* Service-specific specialist routing
* Automatic appointment booking
* Lead source tracking
* UTM campaign attribution
* Email reply detection
* WhatsApp conversation history
* AI follow-up personalization
* Lead conversion analytics
* Revenue attribution
* Advanced reporting dashboards
* Multi-language AI support
* Voice AI integration
* RAG-based company knowledge system
* Document and knowledge-base integration

---

# 📌 Project Summary

**Al Marzaan AI Business Concierge** is an end-to-end AI automation system designed to manage the complete journey from **initial customer inquiry to lead qualification, human handoff, consultation support, and automated follow-up**.

By combining **n8n, OpenAI, Google Sheets, Google Calendar, Slack, WhatsApp, Email, Webhooks, and custom JavaScript**, the system creates a scalable AI-assisted business development pipeline.

The architecture demonstrates how AI can be integrated with traditional business tools to automate repetitive customer-facing processes while keeping professional decision-making and final consultation within the human team.

**The AI handles the conversation and qualification.
The automation handles the operations.
The human specialist handles professional judgment and final business decisions.**
