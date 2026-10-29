# AI-Powered Academic Article Review Automation

**Make.com · Tally · HTTP · Google Gemini AI · JSON · Gmail**

An academic article intake and AI-assisted preliminary review workflow developed for Artrexia Akademi. This portfolio repository documents the **full module-level architecture**, including conditional branches and error handling, without exposing operational secrets.

## Workflow

```text
Tally (Watch New Response)
  → HTTP (GET uploaded document)
  → Gemini AI (Upload a File)
  → Gemini AI (Create a Completion)
       ↳ Error handler: Resume
  → JSON (Parse JSON)
  → Router
       ├── automatic_approval = true  → Gmail (Approval email)
       └── automatic_approval = false → Gmail (Feedback email)
```

## All configured modules

| # | Module | Role |
|---|---|---|
| 1 | Tally: Watch New Response | Collect author name, email, selected category, and uploaded article. |
| 2 | HTTP: Make a Request | Retrieve the uploaded document via GET. |
| 3 | Gemini AI: Upload a File | Upload the document for analysis. |
| 4 | Gemini AI: Create a Completion | Generate publication-type-aware academic feedback in JSON format. |
| 5 | Built-in: Resume | Error-handler branch attached to the Gemini completion module. |
| 6 | JSON: Parse JSON | Extract structured evaluation results. |
| 7 | Router: Basic Router | Branch based on the automatic approval Boolean. |
| 8 | Gmail: Send an Email | Send approval notification and report when approval is true. |
| 9 | Gmail: Send an Email | Send revision/feedback notification and report when approval is false. |

## Evaluation logic

The AI instructions distinguish research articles, reviews, essays, popular-science pieces, and other publication types. Evaluation covers academic structure, scientific quality, references, language, ethics, originality, readability, and contribution. The JSON response includes a decision, an approval flag, an overall score, a score breakdown, detected article type and category, keywords, strengths, improvements, an HTML report, and a summary for the author.

The configured threshold is **85/100**. A score at or above 85 sets the approval flag to true; lower scores trigger the feedback branch. **This threshold is a workflow configuration, not a validated academic quality metric.** AI feedback should support human editors, not replace editorial judgment.

## Repository contents

- `README.md`: full workflow description.
- `workflow-overview.json`: sanitized representation of all modules, including error handling and routing. **It is not a Make.com-importable blueprint.**

## Security and privacy

The public files intentionally exclude API credentials, connection and webhook identifiers, form IDs, recipient addresses, submitted articles, document URLs, operational account details, and private prompt wording. The original production blueprint is not published.

## Project context

Built using **Make.com** and integrations with **Tally**, **Google Gemini AI**, and **Gmail** for Artrexia Akademi.

Website: https://www.artrexiaakademi.com

This documentation reflects the provided configuration; it does not claim verified production uptime, accuracy, or completed end-to-end testing.
