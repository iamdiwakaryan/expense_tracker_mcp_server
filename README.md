# FastMCP Expense Tracker

A simple Python expense tracking tool using FastMCP. It stores and manages expenses in an SQLite database and provides useful tools for listing, adding, and summarizing expense data.

## Setup

1. **Clone the repository and navigate to your project directory.**

2. **Install dependencies:**
   ```bash
   pip install fastmcp
   ```

3. **Prepare category data and budget:**
   - Place a `categories.json` and `budget.json` file in the project directory for expense categories.

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


---

### 3. List Expenses
List expense entries within an inclusive date range.

**Parameters:**
- `start_date` (string, required): `"YYYY-MM-DD"`
- `end_date` (string, required): `"YYYY-MM-DD"`

---

### 4. Summarize Expenses
Summarize expenses by category or overall within a date range.

**Parameters:**
- `start_date` (string, required)
- `end_date` (string, required)
- `category` (optional): Filter to a single category

---

### 5. Delete Expense
Delete an expense entry by ID.

**Parameters:**
- `expense_id` (integer, required)

---

### 6. Update Expense
Update one or more fields of an expense entry.

**Parameters:**
- `expense_id` (integer, required)
- `date` (string, optional)
- `amount` (float, optional)
- `category` (string, optional)
- `subcategory` (string, optional)
- `note` (string, optional)

---

### 7. Get Categories
Fetch available categories.

- `GET /resource/expensecategories`
- Returns the contents of `categories.json`.

---

### 8. Total Budget
Get the total monthly budget (sum of all categories from `budget.json`).

**Return:**  
{
"total_budget": 850
}

---
### 9. Category Budget Usage
Check budget usage for a specific category in a given date range.

**Parameters:**
- `category` (string, required)
- `start_date` (string, required)
- `end_date` (string, required)

**Return Example:**
{
"category": "Food",
"budget_limit": 500,
"spent": 120.0,
"remaining": 380.0
}


---

## Data Storage

- Expenses are stored in `expenses.db` (SQLite).
- Categories are loaded from `categories.json`.
- Budgets are loaded from `budget.json`.

---

## Notes

- All commands are exposed as FastMCP tools.
- You can inspect and call them with the **MCP Inspector** or any API client.
- Database changes (insert/update/delete) take effect instantly.
- Category and budget JSON files are re-read on each access so you can edit them without restarting the server.

