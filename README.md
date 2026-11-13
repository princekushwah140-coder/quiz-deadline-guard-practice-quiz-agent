# Quiz Deadline Guard & Practice Quiz Agent

An AI-powered academic productivity automation project built with **n8n,
Google Gemini, Gmail, and Google Calendar**.

This project combines two practical automations:

1.  **Quiz Deadline Guard** --- checks email for quiz-related
    announcements, extracts key information with Gemini AI, sends a
    structured email alert, and checks Google Calendar for quiz events
    coming up within 48 hours.
2.  **Practice Quiz Agent** --- accepts a subject or topic through an
    n8n chat interface, generates a practice quiz with AI, and can email
    the quiz when requested.

> **Project 02 / 05 · Personal Automation Projects**

------------------------------------------------------------------------

## Table of Contents

-   [Overview](#overview)
-   [The Problem](#the-problem)
-   [The Solution](#the-solution)
-   [Features](#features)
-   [Workflow Architecture](#workflow-architecture)
-   [Technologies Used](#technologies-used)
-   [Repository Structure](#repository-structure)
-   [Screenshots](#screenshots)
-   [Getting Started](#getting-started)
-   [Configuration](#configuration)
-   [Example Practice Quiz Request](#example-practice-quiz-request)
-   [Security and Privacy](#security-and-privacy)
-   [Limitations and Notes](#limitations-and-notes)
-   [What I Learned](#what-i-learned)
-   [Future Improvements](#future-improvements)
-   [Author](#author)

------------------------------------------------------------------------

## Overview

Academic quiz announcements and deadlines can be spread across emails
and calendar events. This project uses workflow automation and
AI-assisted information extraction to make quiz tracking and practice
preparation more organized.

The system has two independent parts:

-   **Quiz Deadline Guard:** scheduled email processing and calendar
    reminders.
-   **Practice Quiz Agent:** conversational, topic-based practice
    question generation with optional email delivery.

The workflows are designed in n8n and connect external services through
their integrations and APIs.

## The Problem

Students may need to check their inbox regularly to find quiz
announcements, identify important dates, and remember upcoming
assessments. Preparing practice questions for a topic can also take
additional time.

## The Solution

I built a two-part n8n automation system:

-   It processes quiz-related email content and uses Gemini AI to
    extract relevant details.
-   It sends a structured notification when quiz information is
    identified.
-   It checks Google Calendar for quiz events within the next 48 hours
    and sends reminder notifications.
-   It provides a chat-based AI agent that generates practice MCQs on a
    requested topic.
-   It can send the generated practice quiz through Gmail when
    requested.

## Features

### 1. Quiz Deadline Guard

-   Runs automatically every morning at **8:00 AM** using a Schedule
    Trigger.
-   Searches Gmail for quiz-related emails.
-   Prepares email content for AI processing.
-   Uses Gemini AI to extract available quiz details, such as topic and
    dates/deadlines.
-   Applies conditional logic to determine whether quiz information was
    found.
-   Sends a structured Gmail notification when relevant information is
    identified.
-   Checks Google Calendar for quiz events within the next **48 hours**.
-   Sends a separate calendar reminder notification.

### 2. Practice Quiz Agent

-   Accepts a subject or topic through an n8n chat interface.
-   Uses an AI Agent with Google Gemini.
-   Generates **10 multiple-choice questions** by default.
-   Includes four options per question.
-   Provides an answer key and a short explanation for each answer.
-   Uses Chat Memory to maintain conversational context.
-   Can use a Gmail tool to email the generated quiz when requested.

## Workflow Architecture

### Part 1 --- Quiz Deadline Guard

``` text
Schedule Trigger (Daily, 8 AM)
            |
            v
     Find Quiz Emails (Gmail)
            |
            v
   Build Email Digest Text
            |
            v
   Extract Quiz Details (Gemini)
            |
            v
      Any Quizzes Found?
            |
            v
    Email Quiz Alert (Gmail)


Google Calendar Events (Next 48 Hours)
            |
            v
    Format Calendar List
            |
            v
      Extract Details (Gemini)
            |
            v
  Email Calendar Reminder (Gmail)
```

### Part 2 --- Practice Quiz Agent

``` text
       Practice Chat
             |
             v
      Quiz Practice Agent
          /    |     \
         v     v      v
      Gemini Memory Gmail Tool
                       |
                       v
                Send Quiz Email
```

The diagrams show the logical flow. The exact node names and connections
may vary slightly in the exported n8n workflow files.

## Technologies Used

  -----------------------------------------------------------------------
  Technology                          Purpose
  ----------------------------------- -----------------------------------
  n8n                                 Workflow orchestration and
                                      automation

  Google Gemini API                   AI-based information extraction and
                                      quiz generation

  Gmail integration/API               Finding quiz emails and sending
                                      notifications

  Google Calendar integration/API     Checking upcoming quiz events

  JavaScript                          Data preparation and formatting
                                      where required

  AI Agent                            Processing conversational quiz
                                      requests

  Chat Memory                         Maintaining conversation context

  REST APIs                           Connecting external services
  -----------------------------------------------------------------------

## Repository Structure

``` text
quiz-deadline-guard-practice-quiz-agent/
│
├── README.md
│
├── workflows/
│   ├── quiz-deadline-guard.json
│   └── practice-quiz-agent.json
│
├── screenshots/
│   ├── 01-workflow-overview.png
│   ├── 02-gmail-quiz-detection.png
│   ├── 03-gemini-quiz-extraction.png
│   ├── 04-calendar-reminder.png
│   ├── 05-practice-agent-architecture.png
│   ├── 06-generated-practice-quiz.png
│   └── 07-gmail-quiz-delivery.png
│
├── docs/
│   └── workflow-explanation.md
│
└── .gitignore
```

Keep this structure aligned with the files actually uploaded to the
repository. If a file has a different name, update the relevant links
and paths in this README.

## Screenshots

The screenshots below document the workflow structure and example
executions. Add the corresponding image files to the `screenshots/`
directory.

## 📸 Project Screenshots

### Quiz Deadline Guard

**1. Complete workflow overview**

![Quiz Deadline Guard workflow overview](./Screenshot%20%2823%29.png)

**2. Gmail quiz email detection**

![Gmail quiz email detection](./Screenshot%20%2825%29.png)

**3. Gemini quiz detail extraction**

![Gemini quiz detail extraction](./Screenshot%20%2826%29.png)

**4. Google Calendar reminder**

![Google Calendar reminder](./Screenshot%20%2827%29.png)

---

### Practice Quiz Agent

**5. Practice Quiz Agent architecture**

![Practice Quiz Agent architecture](./Screenshot%20%2828%29.png)

**6. Generated practice quiz**

![Generated practice quiz](./Screenshot%20%2830%29.png)

**7. Gmail quiz delivery**

![Gmail quiz delivery](./Screenshot%20%2832%29.png)

---

## Getting Started
### Prerequisites

Before importing the workflows, you need:

-   An n8n instance (cloud or self-hosted).
-   A Google account for Gmail and Google Calendar integrations.
-   A Google Gemini API key or an appropriately configured Gemini
    credential in n8n.
-   Permission to connect the required Google services through n8n
    OAuth.

### 1. Clone the repository

``` bash
git clone https://github.com/princekushwah140-coder/quiz-deadline-guard-practice-quiz-agent.git
cd quiz-deadline-guard-practice-quiz-agent
```

### 2. Import the workflows into n8n

1.  Open your n8n instance.
2.  Open the workflow menu.
3.  Choose the option to import a workflow from a file.
4.  Import `workflows/quiz-deadline-guard.json`.
5.  Repeat for `workflows/practice-quiz-agent.json`.
6.  Review the imported nodes and reconnect your own credentials.

### 3. Configure credentials

Set up your own credentials for:

-   Gmail
-   Google Calendar
-   Google Gemini

The exported workflows should not contain working credentials. Configure
your own connections inside n8n.

### 4. Review workflow settings

Before activating the workflows:

-   Confirm the Schedule Trigger time and timezone.
-   Confirm the Gmail search/filter settings.
-   Review the Gemini prompts and output format.
-   Confirm the Google Calendar query and 48-hour time window.
-   Confirm the recipient address used by notification nodes.
-   Test each workflow manually with sample data.

### 5. Activate and test

Activate the scheduled Quiz Deadline Guard after testing it. Start the
Practice Quiz Agent through its chat interface and test both quiz
generation and optional Gmail delivery.

## Configuration

Some values depend on your own n8n setup and Google account. Review
these after importing:

  -----------------------------------------------------------------------
  Setting                             What to configure
  ----------------------------------- -----------------------------------
  Gmail credential                    Connect your own Gmail account

  Google Calendar credential          Connect your own calendar

  Gemini credential                   Configure your own Gemini API
                                      access

  Notification recipient              Set the email address that should
                                      receive alerts

  Schedule Trigger                    Confirm the daily run time and
                                      timezone

  Calendar time window                Confirm the upcoming-event window
                                      is 48 hours

  AI prompts                          Review or adapt the extraction and
                                      quiz-generation instructions
  -----------------------------------------------------------------------

Do not paste API keys, OAuth tokens, passwords, or private account
details into this README.

## Example Practice Quiz Request

Try a request like this in the Practice Chat:

``` text
Generate a 10-question practice quiz on DBMS covering SQL,
keys, normalization, and transactions.

Include four options for each question, followed by an
answer key and a one-line explanation for every answer.
Email the complete quiz to my configured email address.
```

The agent should generate the practice material and use its Gmail tool
when email delivery is requested and correctly configured.

## Security and Privacy

**Never commit secrets or personal data to GitHub.**

Before uploading workflow JSON files:

-   Remove or replace API keys and access tokens.
-   Do not upload OAuth client secrets or credential exports.
-   Remove private email addresses where they are not needed.
-   Remove personal calendar event details and other private data.
-   Review node parameters and execution data for sensitive information.
-   Use your own credentials after importing the workflows.

If a secret is accidentally committed, revoke or rotate it immediately.
Deleting it from the latest version of a file may not remove it from Git
history.

## Limitations and Notes

-   AI extraction depends on the quality and clarity of the source
    email.
-   Extracted dates and topics should be checked against the original
    announcement.
-   Calendar reminders depend on the events and permissions available in
    the connected Google Calendar account.
-   Gmail and Google Calendar access requires valid authorization.
-   The exact behavior may depend on your n8n version and node
    configuration.
-   This project is an academic productivity aid; users should verify
    important deadlines independently.

## What I Learned

Through this project, I practised:

-   Building multi-step workflows in n8n.
-   Integrating AI models into practical automation systems.
-   Extracting structured information from unstructured email content.
-   Connecting Gmail and Google Calendar.
-   Building conversational AI agents with memory.
-   Passing data between workflow nodes.
-   Using conditional logic for automated decisions.
-   Integrating external services through APIs.
-   Testing and documenting automation workflows.

## Future Improvements

-   Add support for more academic announcement formats.
-   Improve date validation and handling of incomplete information.
-   Add configurable reminder intervals.
-   Support more quiz formats and difficulty levels.
-   Add a simple dashboard for tracking detected quizzes and deadlines.
-   Improve error handling and workflow execution logging.

## Author

**Prince Kushwaha**\
Aspiring Software & Backend Developer \| AI Automation & Integration
Engineering

-   GitHub:
    [princekushwah140-coder](https://github.com/princekushwah140-coder)
-   LinkedIn:
    [prince-kushwaha-02ab1a392](https://www.linkedin.com/in/prince-kushwaha-02ab1a392/)

------------------------------------------------------------------------

If you find this project useful, feel free to explore the workflows and
screenshots.

**Built with n8n, Gemini AI, Gmail, and Google Calendar.**
