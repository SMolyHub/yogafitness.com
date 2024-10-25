# shreyasi.com
1. Data Structure for AST
   class Node:
    def __init__(self, node_type, left=None, right=None, value=None):
        self.type = node_type  # "operator" or "operand"
        self.left = left       # Reference to left child
        self.right = right     # Reference to right child (for operators)
        self.value = value     # Optional value for operand nodes

    def __repr__(self):
        return f"Node(type={self.type}, value={self.value}, left={self.left}, right={self.right})"
2. Data Storage
   {
    "rule_id": "rule1",
    "rule_string": "((age > 30 AND department = 'Sales') OR (age < 25 AND department = 'Marketing')) AND (salary > 50000 OR experience > 5)",
    "created_at": "2024-10-25T12:00:00Z",
    "modified_at": "2024-10-25T12:00:00Z"
}
3. API Design
   import re

def create_rule(rule_string):
    # Tokenization and parsing logic goes here.
    # For simplicity, we'll assume the rule_string is well-formed.

    def parse(tokens):
        # Recursive function to build the AST
        # Logic for handling operators and operands
        pass

    tokens = re.findall(r'\w+|[<>!=]=|AND|OR|\(|\)', rule_string)
    root = parse(tokens)
    return root
Function to Combine Rules
def combine_rules(rules):
    combined_root = None
    for rule in rules:
        new_ast = create_rule(rule)
        # Logic to combine new_ast into combined_root efficiently
        # This could use heuristics for merging similar operators.
    return combined_root
Function to Evaluate Rules
def evaluate_rule(ast, data):
    if ast.type == "operand":
        # Handle comparisons (e.g., age > 30)
        field_value = data.get(ast.value[0])  # Extract field
        operator = ast.value[1]                # Extract operator
        # Comparison logic here
    elif ast.type == "operator":
        left_eval = evaluate_rule(ast.left, data)
        right_eval = evaluate_rule(ast.right, data)
        if ast.value == "AND":
            return left_eval and right_eval
        elif ast.value == "OR":
            return left_eval or right_eval
4. Test Cases
Create Individual Rules
rule1 = create_rule("((age > 30 AND department = 'Sales') OR (age < 25 AND department = 'Marketing')) AND (salary > 50000 OR experience > 5)")
assert rule1  # Check if rule1 AST is created correctly
Combine Rules
combined_ast = combine_rules(["rule1", "rule2"])
assert combined_ast  # Check combined AST
Evaluate Rules
data = {"age": 35, "department": "Sales", "salary": 60000, "experience": 3}
result = evaluate_rule(combined_ast, data)
assert result is True  # Expected output based on the conditions
