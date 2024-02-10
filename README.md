 as tk

MAX_SIZE = 100

class Stack:
    def _init_(self):
        self.top = -1
        self.items = [0] * MAX_SIZE

    def push(self, item):
        if self.top == MAX_SIZE - 1:
            print("Stack Overflow")
            exit(1)
        self.top += 1
        self.items[self.top] = item

    def pop(self):
        if self.top == -1:
            print("Stack Underflow")
            exit(1)
        self.top -= 1
        return self.items[self.top + 1]

def is_operator(ch):
    return ch in "+-*/"

def precedence(ch):
    if ch in "+-":
        return 1
    elif ch in "*/":
        return 2
    return 0

def infix_to_postfix(infix):
    stack = Stack()
    postfix = []
    i = 0

    while i < len(infix):
        ch = infix[i]

        if ch.isalnum():
            postfix.append(ch)
            i += 1
        elif ch == '(':
            stack.push(ch)
            i += 1
        elif ch == ')':
            while stack.top != -1 and stack.items[stack.top] != '(':
                postfix.append(stack.pop())
            if stack.top != -1 and stack.items[stack.top] == '(':
                stack.pop()
            i += 1
        else:
            while stack.top != -1 and precedence(ch) <= precedence(stack.items[stack.top]):
                postfix.append(stack.pop())
            stack.push(ch)
            i += 1

    while stack.top != -1:
        postfix.append(stack.pop())

    return ''.join(postfix)

def infix_to_prefix(infix):
    reverse_infix = ""
    i = len(infix) - 1

    while i >= 0:
        if infix[i] == '(':
            reverse_infix += ')'
        elif infix[i] == ')':
            reverse_infix += '('
        else:
            reverse_infix += infix[i]
        i -= 1

    postfix = infix_to_postfix(reverse_infix)
    prefix = postfix[::-1]

    return prefix

def convert_expression():
    infix_expression = entry.get()
    prefix = infix_to_prefix(infix_expression)
    postfix = infix_to_postfix(infix_expression)
    result_label.config(text=f"Prefix: {prefix}\nPostfix: {postfix}")

app = tk.Tk()
app.title("Infix to Prefix/Postfix Converter")
app.geometry("400x200")

frame = tk.Frame(app)
frame.pack()

label = tk.Label(frame, text="Enter an infix expression:")
label.pack()

entry = tk.Entry(frame)
entry.insert(0, "Enter infix expression here")
entry.pack()

convert_button = tk.Button(frame, text="Convert", command=convert_expression)
convert_button.pack()

result_label = tk.Label(app, text="")
result_label.pack()

app.mainloop()
