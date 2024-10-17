# ASSIGNMENT - Data Structures

## developed by :Gokulramanan k
## reg no: 212222230040

```

#Q1.a)Infix to Postfix conversion

```
#include <stdio.h>
#include <ctype.h>
#include <string.h>

#define MAX 100

char stack[MAX];
int top = -1;

void push(char x) {
    stack[++top] = x;
}

char pop() {
    if (top == -1)
        return -1;
    else
        return stack[top--];
}

int precedence(char x) {
    if (x == '(')
        return 0;
    if (x == '+' || x == '-')
        return 1;
    if (x == '*' || x == '/')
        return 2;
    if (x == '^')
        return 3;
    return 0;
}

void infixToPostfix(char *infix) {
    char *exp, x;
    exp = infix;

    while (*exp != '\0') {
        if (isalnum(*exp)) {
            printf("%c", *exp);
        } else if (*exp == '(') {
            push(*exp);
        } else if (*exp == ')') {
            while ((x = pop()) != '(')
                printf("%c", x);
        } else {
            while (precedence(stack[top]) >= precedence(*exp))
                printf("%c", pop());
            push(*exp);
        }
        exp++;
    }

    while (top != -1) {
        printf("%c", pop());
    }
    printf("\n");
}

int main() {
    char infix[MAX];
    printf("Enter an infix expression: ");
    gets(infix);
    printf("Postfix expression: ");
    infixToPostfix(infix);
    return 0;
}


```
# OUTPUT:
```
Postfix expression: ABC*+



```

#Q2Using scatter plot compare data   cylinder vs Co2Emission and Enginesize Vs Co2Emission using different colors:
```
#include <stdio.h>
#include <ctype.h>

#define MAX 100

int stack[MAX];
int top = -1;

void push(int x) {
    stack[++top] = x;
}

int pop() {
    return stack[top--];
}

int evaluatePostfix(char *postfix) {
    char *exp;
    int num1, num2, result;

    exp = postfix;
    while (*exp != '\0') {
        if (isdigit(*exp)) {
            push(*exp - '0');
        } else {
            num2 = pop();
            num1 = pop();

            switch (*exp) {
                case '+':
                    result = num1 + num2;
                    break;
                case '-':
                    result = num1 - num2;
                    break;
                case '*':
                    result = num1 * num2;
                    break;
                case '/':
                    result = num1 / num2;
                    break;
            }
            push(result);
        }
        exp++;
    }
    return pop();
}

int main() {
    char postfix[MAX];
    printf("Enter a postfix expression: ");
    gets(postfix);
    printf("Result of evaluation: %d\n", evaluatePostfix(postfix));
    return 0;
}


```
# ouput:
```
Result of evaluation: 48

```


#Q3

```
#include <stdio.h>
#include <stdlib.h>

#define MAX 3
#define MIN 2

struct BTreeNode {
    int val[MAX + 1], count;
    struct BTreeNode *link[MAX + 1];
};

struct BTreeNode *root;

struct BTreeNode *createNode(int val, struct BTreeNode *child) {
    struct BTreeNode *newNode;
    newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
    newNode->val[1] = val;
    newNode->count = 1;
    newNode->link[0] = root;
    newNode->link[1] = child;
    return newNode;
}

void addValToNode(int val, int pos, struct BTreeNode *node, struct BTreeNode *child) {
    int j = node->count;
    while (j > pos) {
        node->val[j + 1] = node->val[j];
        node->link[j + 1] = node->link[j];
        j--;
    }
    node->val[j + 1] = val;
    node->link[j + 1] = child;
    node->count++;
}

void splitNode(int val, int *pval, int pos, struct BTreeNode *node, struct BTreeNode *child, struct BTreeNode **newNode) {
    int median, j;

    if (pos > MIN)
        median = MIN + 1;
    else
        median = MIN;

    *newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
    j = median + 1;
    while (j <= MAX) {
        (*newNode)->val[j - median] = node->val[j];
        (*newNode)->link[j - median] = node->link[j];
        j++;
    }
    node->count = median;
    (*newNode)->count = MAX - median;

    if (pos <= MIN) {
        addValToNode(val, pos, node, child);
    } else {
        addValToNode(val, pos - median, *newNode, child);
    }

    *pval = node->val[node->count];
    (*newNode)->link[0] = node->link[node->count];
    node->count--;
}

int setValInNode(int val, int *pval, struct BTreeNode *node, struct BTreeNode **child) {
    int pos;
    if (!node) {
        *pval = val;
        *child = NULL;
        return 1;
    }

    if (val < node->val[1]) {
        pos = 0;
    } else {
        for (pos = node->count; (val < node->val[pos] && pos > 1); pos--);
        if (val == node->val[pos]) {
            printf("Duplicates are not allowed\n");
            return 0;
        }
    }
    if (setValInNode(val, pval, node->link[pos], child)) {
        if (node->count < MAX) {
            addValToNode(*pval, pos, node, *child);
        } else {
            splitNode(*pval, pval, pos, node, *child, child);
            return 1;
        }
    }
    return 0;
}

void insert(int val) {
    int flag, i;
    struct BTreeNode *child;

    flag = setValInNode(val, &i, root, &child);
    if (flag)
        root = createNode(i, child);
}

void inorderTraversal(struct BTreeNode *myNode) {
    int i;
    if (myNode) {
        for (i = 0; i < myNode->count; i++) {
            inorderTraversal(myNode->link[i]);
            printf("%d ", myNode->val[i + 1]);
        }
        inorderTraversal(myNode->link[i]);
    }
}

int main() {
    int val, ch;
    while (1) {
        printf("\n1. Insert\n2. Display\n3. Exit\nEnter your choice: ");
        scanf("%d", &ch);
        switch (ch) {
            case 1:
                printf("Enter the value to insert: ");
                scanf("%d", &val);
                insert(val);
                break;
            case 2:
                printf("B-tree elements: ");
                inorderTraversal(root);
                printf("\n");
                break;
            case 3:
                exit(0);
            default:
                printf("Invalid choice\n");
        }
    }
    return 0;
}


```
# ouput:
```
B-tree elements: 5 6 7 10 12 17 20 30

```



