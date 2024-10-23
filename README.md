
# Rule Engine with Abstract Syntax Tree (AST)

## Overview

This project implements a Rule Engine system that determines user eligibility based on attributes such as age, department, income, and spend. The engine utilizes an Abstract Syntax Tree (AST) to represent conditional rules, allowing dynamic creation, combination, and modification of these rules.

### Features

- **Rule Creation:** Create dynamic rules with conditions on various attributes.
- **Rule Combination:** Combine multiple rules into a single rule using logical operators like `AND` and `OR`.
- **Rule Evaluation:** Evaluate user data against the created or combined rules.
- **Dynamic Rule Representation:** The rules are stored and managed as ASTs.
- **Frontend Interface:** A simple UI is provided to interact with the backend API to create, combine, and evaluate rules.

---

## Folder Structure

```bash
.
├── client                  # Frontend code (HTML, CSS, and JavaScript for the UI)
│   └── index.html          # Main HTML for Rule Engine UI
├── controllers             # Logic to handle API requests for rules
│   └── ruleController.js   # Functions to create, combine, and evaluate rules
├── models                  # Mongoose models for MongoDB
│   └── Rule.js             # Schema definition for rules
├── routes                  # API routes for rule management
│   └── ruleRoutes.js       # Route definitions for rules
├── app.js                  # Main server file to start Express application
├── .env                    # Environment variables (e.g., MongoDB URI)
└── README.md               # This file
```

---

## Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/rule-engine-ast.git
   cd rule-engine-ast
   ```

2. **Install dependencies for both server and client:**
   ```bash
   npm install
   ```

3. **Set up MongoDB connection:**  
   Create a `.env` file at the root of the project and add your MongoDB URI.
   ```
   MONGO_URI=your-mongodb-uri
   ```

4. **Start the server:**
   ```bash
   npm start
   ```
   The server will run on `http://localhost:5000`.

---

## API Endpoints

### 1. Create Rule
- **POST** `/api/rules/create_rule`
- **Body:**
  ```json
  {
    "ruleName": "Rule1",
    "ruleString": "(age > 30 AND department = 'Sales') OR (salary > 50000)"
  }
  ```

- **Response:** AST representation of the created rule.

### 2. Combine Rules
- **POST** `/api/rules/combine_rules`
- **Body:**
  ```json
  {
    "rules": ["Rule1", "Rule2"],
    "op": "AND"
  }
  ```

- **Response:** Combined AST and the generated rule name.

### 3. Evaluate Rule
- **POST** `/api/rules/evaluate_rule`
- **Body:**
  ```json
  {
    "ast": "Rule1",
    "data": {
      "age": 35,
      "department": "Sales",
      "salary": 60000
    }
  }
  ```

- **Response:** `true` or `false` based on the evaluation.

---

## Frontend Usage

The frontend (client) part is a simple UI that allows you to:
1. **Create rules** by entering a rule name and string.
2. **Combine rules** by adding rules and specifying an operator.
3. **Evaluate rules** by entering a rule name and providing user data.

You can run the frontend by opening `client/index.html` in a browser after the server is running.

---

## Testing with Postman

You can use [Postman](https://www.postman.com/) to test the API endpoints.

### Example Request for Creating Rule

1. Set the method to `POST`.
2. Set the URL to `http://localhost:5000/api/rules/create_rule`.
3. Add the following JSON body:
   ```json
   {
     "ruleName": "Rule1",
     "ruleString": "(age > 30 AND department = 'Sales') OR (salary > 50000)"
   }
   ```

4. Send the request and verify the AST structure in the response.

---

## Error Handling

- Invalid rule strings or data formats are handled gracefully with appropriate error messages.
- Duplicate rule names are prevented with unique constraints on the `ruleName` field.

---

## Technologies Used

- **Node.js** and **Express** for the backend.
- **MongoDB** with **Mongoose** for database management.
- **JavaScript** for frontend logic.
- **HTML/CSS** for the UI.

---

## License

This project is licensed under the MIT License.
