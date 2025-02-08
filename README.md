Here's the infix to postfix algorithm in c: 

Traversing the Expression: Scan the given infix expression from left to right and go character by character.
If the Scanned Character is an Operand: Directly output the operand (e.g., A, B, 3, etc.) to the postfix expression.
If the Scanned Character is an Operator :
If the operator’s precedence is greater than the operator on top of the stack, or the stack is empty, or the top of the stack is a (, push the scanned operator onto the stack.
Operator Precedence: Operators like * and / have higher precedence over + and -. This step ensures that operators with higher precedence are handled first.
If the Scanned Operator has Lower or Equal Precedence:
While the operator at the top of the stack has greater than or equal precedence than the current operator, pop the stack and append each popped operator to the postfix expression.
After popping the operators with higher or equal precedence, push the current operator onto the stack.
Parentheses Handling: If you encounter a (, during popping, stop popping and push the scanned operator onto the stack.
If the Scanned Character is a Left Parenthesis (:
Push the ( onto the stack. This helps to keep track of the boundaries of sub-expressions. It ensures that operators are processed correctly within those bounds.
If the Scanned Character is a Right Parenthesis ):
Pop the stack and output each operator until a ( is encountered.
Eliminate both the ( and ) after processing.
This ensures that any operators inside parentheses are properly evaluated and placed in the correct order.
Repeat Steps 2 to 6: Continue scanning the entire expression, applying the above steps for each character.
End of Expression:
After the entire expression has been scanned, pop and print any remaining operators from the stack.
This step ensures that all operators are output in the correct postfix order
