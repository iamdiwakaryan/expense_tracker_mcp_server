# FastMCP Expense Tracker

A simple Python expense tracking tool using FastMCP. It stores and manages expenses in an SQLite database and provides useful tools for listing, adding, and summarizing expense data.

## Setup

1. **Clone the repository and navigate to your project directory.**

2. **Install dependencies:**
   ```bash
   pip install fastmcp
   ```

3. **Prepare category data (optional):**
   - Place a `categories.json` file in the project directory for expense categories.

## Usage

### Add Server into Claude Desktop

Start the server with:
```bash
uv run fastmcp install claude-desktop main.py
```
This will run FastMCP and expose the defined tools and resources into claude desktop

---

## Commands / Tools

### 1. Initialize Database
Creates the SQLite database and table if they do not already exist.
- This runs automatically on startup.

### 2. Add Expense

Add a new expense entry.

**Parameters:**
- `date` (string, required): Date of the expense (e.g., `"2025-09-30"`)
- `amount` (float, required): Amount spent
- `category` (string, required): Category name
- `subcategory` (string, optional): Subcategory
- `note` (string, optional): Description or note

**Example:**
```json
{
  "date": "2025-09-30",
  "amount": 50.0,
  "category": "Food",
  "subcategory": "Groceries",
  "note": "Lunch items"
}
```

### 3. List Expenses

Lists expense entries between two dates.

**Parameters:**
- `startdate` (string, required): Start of date range (`"YYYY-MM-DD"`)
- `enddate` (string, required): End of date range (`"YYYY-MM-DD"`)

### 4. Summarize Expenses

Summarizes expenses by category within a date range.

**Parameters:**
- `startdate` (string, required): Start of range
- `enddate` (string, required): End of range
- `category` (string, optional): Filter by specific category

### 5. Get Categories

Returns the list of expense categories.

- `GET /resource/expensecategories`
- Returns the contents of `categories.json`.

---

## Data Storage

- Expenses are saved in `expenses.db` (SQLite).
- Categories are loaded from `categories.json`.

---

## Notes

- All commands are exposed as FastMCP tools and can be called via the MCP Inspector or API client.
- Make sure to always provide required fields, especially `category`, for input validation.

---
