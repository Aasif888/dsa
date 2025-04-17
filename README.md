

<html>
<head>
  <title>DSA Experiments</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #121212;
      color: #e0e0e0;
    }
    button {
      display: inline-block;
      margin: 10px 5px 5px 0;
      padding: 10px;
      font-size: 16px;
      cursor: pointer;
      background-color: #1f1f1f;
      color: #e0e0e0;
      border: 1px solid #444;
      border-radius: 5px;
    }
    button:hover {
      background-color: #2a2a2a;
    }
    pre {
      background-color: #121212 ! important;
      color: #e0e0e0 ! important;
      padding: 15px;
      border: 1px solid #444;
      overflow-x: auto;
      display: none;
      white-space: pre-wrap;
      border-radius: 5px;
    }
    .experiment {
      margin-bottom: 20px;
    }
  </style>
  <script>
    function toggleCode(id) {
      const block = document.getElementById(id);
      block.style.display = (block.style.display === 'block') ? 'none' : 'block';
    }

    function copyCode(id) {
      const text = document.getElementById(id).innerText;
      navigator.clipboard.writeText(text).catch(err => {
        console.error("Failed to copy: ", err);
      });
    }
  </script>
</head>
<body>
</body>
</html>

<h2> </h2>

<div class="experiment">
  <button onclick="toggleCode('exp1')">Experiment 1</button>
  <button onclick="copyCode('exp1')">Copy</button>
  <pre id="exp1">#include &lt;iostream&gt;
using namespace std;

// Function to print the array
void printArray(int arr[], int n) {
    for (int i = 0; i &lt; n; ++i) {
        cout &lt;&lt; arr[i] &lt;&lt; " ";
    }
    cout &lt;&lt; endl;
}

// Function to perform linear search
int linearSearch(int arr[], int n, int x) {
    for (int i = 0; i &lt; n; ++i) {
        if (arr[i] == x) {
            return i; // Return the index if found
        }
    }
    return -1; // Return -1 if not found
}

// Function to insert an element at a given position
void insertElement(int arr[], int&amp; n, int pos, int value) {
    if (pos &lt; 0 || pos &gt; n) {
        cout &lt;&lt; "Invalid position for insertion." &lt;&lt; endl;
        return;
    }

    // Shift elements to the right to create space for the new element
    for (int i = n - 1; i &gt;= pos; --i) {
        arr[i + 1] = arr[i];
    }

    arr[pos] = value;
    n++;
}

// Function to delete an element at a given position
int deleteElement(int arr[], int&amp; n, int value) {
    int pos = linearSearch(arr, n, value);
    if (pos == -1) {
        return 0; // Element not found
    }

    // Shift elements to the left to fill the gap
    for (int i = pos; i &lt; n - 1; ++i) {
        arr[i] = arr[i + 1];
    }
    n--;
    return 1; // Element deleted successfully
}

int main() {
    cout &lt;&lt; "Name = Aasif Mohd \nRoll no. = 24/A15/006" &lt;&lt; endl;
    cout &lt;&lt; "Enter the number of elements in array: ";
    int n;
    cin &gt;&gt; n;

    // Dynamically allocate memory for the array
    int* arr = new int[n + 1];

    cout &lt;&lt; "ENTER THE ARRAY ELEMENTS" &lt;&lt; endl;
    for (int i = 0; i &lt; n; ++i) {
        cout &lt;&lt; "Element at index " &lt;&lt; i &lt;&lt; ": ";
        cin &gt;&gt; arr[i];
    }

    cout &lt;&lt; "Original array: ";
    printArray(arr, n);
    cout &lt;&lt; endl;

    int x;
    cout &lt;&lt; "Enter element to search: ";
    cin &gt;&gt; x;
    int p = linearSearch(arr, n, x);
    if (p != -1) {
        cout &lt;&lt; "Element present at index: " &lt;&lt; p &lt;&lt; endl;
    } else {
        cout &lt;&lt; "Element is not present in array" &lt;&lt; endl;
    }
    cout &lt;&lt; endl;

    // Insert an element
    int pos, value;
    cout &lt;&lt; "For insertion of an element" &lt;&lt; endl;
    cout &lt;&lt; "Enter index: ";
    cin &gt;&gt; pos;
    cout &lt;&lt; "Enter Value: ";
    cin &gt;&gt; value;
    insertElement(arr, n, pos, value);
    cout &lt;&lt; "Array after insertion: ";
    printArray(arr, n);
    cout &lt;&lt; endl;

    // Delete an element
    cout &lt;&lt; "Enter Element for deletion: ";
    cin &gt;&gt; value;
    int m = deleteElement(arr, n, value);
    if (m == 1) {
        cout &lt;&lt; "Deletion is successful" &lt;&lt; endl;
    } else {
        cout &lt;&lt; "Deletion is unsuccessful" &lt;&lt; endl;
    }
    cout &lt;&lt; "Array after deletion: ";
    printArray(arr, n);

    // Deallocate memory
    delete[] arr;

    return 0;
}
</pre>
</div>

<!-- Experiment 2 -->
<div class="experiment">
  <button onclick="toggleCode('exp2')">Experiment 2</button>
  <button onclick="copyCode('exp2')">Copy</button>
  <pre id="exp2">#include &lt;iostream&gt;
using namespace std;
#include &lt;stdlib.h&gt;

struct node {
    int data;
    node* next;
};

// Function to traverse and print the linked list
void linkedListTraversal(struct node* ptr) {
    int i = 0;
    while (ptr != NULL) {
        cout &lt;&lt; "Element at index " &lt;&lt; i &lt;&lt; ": " &lt;&lt; ptr-&gt;data &lt;&lt; "\n";
        i++;
        ptr = ptr-&gt;next;
    }
}

// Function to insert a new node at a given position
void insertAtIndex(node*& head, int index, int value) {
    node* newNode = new node;
    newNode-&gt;data = value;
    newNode-&gt;next = NULL;

    if (index == 0) {
        newNode-&gt;next = head;
        head = newNode;
        return;
    }

    node* current = head;
    for (int i = 0; i &lt; index - 1 &amp;&amp; current != NULL; ++i) {
        current = current-&gt;next;
    }

    if (current == NULL) {
        cout &lt;&lt; "Invalid index! Insertion failed." &lt;&lt; endl;
        delete newNode;
        return;
    }

    newNode-&gt;next = current-&gt;next;
    current-&gt;next = newNode;
}

// Function to delete a node by value
void deleteNode(node*& head, int value) {
    if (head == NULL) {
        cout &lt;&lt; "List is empty! Deletion failed.";
        return;
    }

    if (head-&gt;data == value) {
        node* temp = head;
        head = head-&gt;next;
        free(temp);
        return;
    }

    node* temp = head;
    while (temp-&gt;next != NULL &amp;&amp; temp-&gt;next-&gt;data != value) {
        temp = temp-&gt;next;
    }

    if (temp-&gt;next == NULL) {
        cout &lt;&lt; "Value not found in the list\n";
        return;
    }

    node* nodeToDelete = temp-&gt;next;
    temp-&gt;next = temp-&gt;next-&gt;next;
    free(nodeToDelete);
}

// Function to search for an element in the list
bool searchNode(node* head, int value) {
    int i = 0;
    node* temp = head;
    while (temp != NULL) {
        if (temp-&gt;data == value) {
            cout &lt;&lt; "Value is found at index " &lt;&lt; i &lt;&lt; endl;
            return true;
        }
        i++;
        temp = temp-&gt;next;
    }
    cout &lt;&lt; "Value is not found" &lt;&lt; endl;
    return false;
}

int main() {
    cout &lt;&lt; "Name: Aasif Mohd\nRoll No.: 24/A15/006" &lt;&lt; endl;

    struct node* first = new node;
    struct node* second = new node;
    struct node* third = new node;
    struct node* fourth = new node;

    first-&gt;data = 3;
    first-&gt;next = second;

    second-&gt;data = 6;
    second-&gt;next = third;

    third-&gt;data = 8;
    third-&gt;next = fourth;

    fourth-&gt;data = 6;
    fourth-&gt;next = NULL;

    cout &lt;&lt; "Original List:\n";
    linkedListTraversal(first);
    cout &lt;&lt; "\n";

    cout &lt;&lt; "Inserting 10 at index 2:\n";
    insertAtIndex(first, 2, 10);
    cout &lt;&lt; "Updated List:\n";
    linkedListTraversal(first);
    cout &lt;&lt; "\n";

    int Value = 8;
    cout &lt;&lt; "Search node with value = " &lt;&lt; Value &lt;&lt; endl;
    searchNode(first, Value);

    cout &lt;&lt; "\nDeleting node with value = 8\n";
    deleteNode(first, 8);
    cout &lt;&lt; "Updated List:\n";
    linkedListTraversal(first);
    cout &lt;&lt; "\n";

    return 0;
}
</pre>
</div>

<!-- Experiment 3a (Stack operations) -->
<div class="experiment">
  <button onclick="toggleCode('exp3a')">Experiment 3(a)</button>
  <button onclick="copyCode('exp3a')">Copy</button>
  <pre id="exp3a">#include &lt;iostream&gt;
#include &lt;stdlib.h&gt;
using namespace std;

struct stack {
    int size;
    int top;
    int* arr;
};

// Function to check if stack is full
bool isFull(stack *sp) {
    return sp-&gt;top == sp-&gt;size - 1;
}

// Function to check if stack is empty
bool isEmpty(stack *sp) {
    return sp-&gt;top == -1;
}

// Function to push an element onto the stack
void push(stack *sp, int value) {
    if (isFull(sp)) {
        cout &lt;&lt; "Stack overflow! Cannot push " &lt;&lt; value &lt;&lt; endl;
    } else {
        sp-&gt;top++;
        sp-&gt;arr[sp-&gt;top] = value;
        cout &lt;&lt; "Pushed " &lt;&lt; value &lt;&lt; " onto stack." &lt;&lt; endl;
    }
}

// Function to pop an element from the stack
int pop(stack *sp) {
    if (isEmpty(sp)) {
        cout &lt;&lt; "Stack underflow! No elements to pop." &lt;&lt; endl;
        return -1;
    } else {
        int poppedValue = sp-&gt;arr[sp-&gt;top];
        sp-&gt;top--;
        cout &lt;&lt; "Popped " &lt;&lt; poppedValue &lt;&lt; " from stack." &lt;&lt; endl;
        return poppedValue;
    }
}

int display(stack* sp) {
    cout &lt;&lt; "stack element: ";
    if (isEmpty(sp)) cout &lt;&lt; "Empty stack";
    for (int i = 0; i &lt;= sp-&gt;top; i++) {
        cout &lt;&lt; sp-&gt;arr[i] &lt;&lt; " ";
    }
    cout &lt;&lt; endl &lt;&lt; endl;
    return 0;
}

int main() {
    stack* sp = new stack;
    sp-&gt;size = 5;
    sp-&gt;top = -1;
    sp-&gt;arr = new int[sp-&gt;size];

    cout &lt;&lt; "Stack created successfully" &lt;&lt; endl;

    // Push elements
    push(sp, 10);
    push(sp, 20);
    push(sp, 30);
    push(sp, 40);
    push(sp, 50);
    push(sp, 60); // Should show stack overflow
    cout &lt;&lt; endl &lt;&lt; "Stack element after all elements pushed" &lt;&lt; endl;
    display(sp);

    // Pop elements
    pop(sp);
    pop(sp);
    pop(sp);
    pop(sp);
    pop(sp);
    pop(sp); // Should show stack underflow
    cout &lt;&lt; endl &lt;&lt; "Stack element after all elements popped" &lt;&lt; endl;
    display(sp);

    // Free allocated memory
    delete[] sp-&gt;arr;
    delete sp;

    return 0;
}
</pre>
</div>

<!-- Experiment 3b (Stack using linked list) -->
<div class="experiment">
  <button onclick="toggleCode('exp3b')">Experiment 3(b)</button>
  <button onclick="copyCode('exp3b')">Copy</button>
  <pre id="exp3b">#include &lt;iostream&gt;
using namespace std;

struct Node {
    int data;
    Node* next;
};

int isempty(Node* top) {
    return top == NULL;
}

void push(Node*& top, int x) {
    Node* n = new Node;
    n-&gt;data = x;
    n-&gt;next = top;
    top = n;
    cout &lt;&lt; "Pushed Element = " &lt;&lt; x &lt;&lt; endl;
}

void pop(Node*& top) {
    if (isempty(top)) {
        cout &lt;&lt; "Popped Element = Stack Underflow\n";
    } else {
        Node* n = top;
        int x = n-&gt;data;
        top = top-&gt;next;
        delete n;
        cout &lt;&lt; "Popped Element = " &lt;&lt; x &lt;&lt; endl;
    }
}

void display(Node* top) {
    cout &lt;&lt; "Stack elements: ";
    if (isempty(top)) {
        cout &lt;&lt; "Stack is empty" &lt;&lt; endl &lt;&lt; endl;
    } else {
        Node* temp = top;
        while (temp != NULL) {
            cout &lt;&lt; temp-&gt;data &lt;&lt; " ";
            temp = temp-&gt;next;
        }
        cout &lt;&lt; endl &lt;&lt; endl;
    }
}

int main() {
    cout &lt;&lt; "Name: Aasif Mohd\nRoll no.: 24/A15/006" &lt;&lt; endl;
    Node* top = NULL;

    cout &lt;&lt; "\nPushing values onto the stack" &lt;&lt; endl;
    push(top, 10);
    push(top, 20);
    push(top, 30);
    push(top, 40);
    cout &lt;&lt; endl;
    display(top);

    cout &lt;&lt; "Popping values from the stack" &lt;&lt; endl;
    pop(top);
    pop(top);
    pop(top);
    pop(top);
    pop(top);

    cout &lt;&lt; endl;
    display(top);

    return 0;
}
</pre>
</div>

<!-- Experiment 4a (Queue Implementation) -->
<div class="experiment">
  <button onclick="toggleCode('exp4a')">Experiment 4a</button>
  <button onclick="copyCode('exp4a')">Copy</button>
  <pre id="exp4a">#include &lt;iostream&gt;
#include &lt;stdlib.h&gt;
using namespace std;

struct queue {
    int size;
    int f, r;
    int *array;
};

// Check if the queue is full
int isfull(queue *&p) {
    if (p-&gt;r == p-&gt;size - 1) {
        return 1;
    }
    return 0;
}

// Check if the queue is empty
int isempty(queue *&p) {
    if (p-&gt;f == -1 || p-&gt;f &gt; p-&gt;r) { // Empty if f &gt; r or f is -1
        return 1;
    }
    return 0;
}

// Enqueue function to add an item to the queue
void enqueue(queue *&p, int value) {
    if (isfull(p)) {
        cout &lt;&lt; "Queue is full" &lt;&lt; endl;
    } else {
        if (p-&gt;f == -1) { // First element being added
            p-&gt;f = 0;
        }
        p-&gt;r++;
        p-&gt;array[p-&gt;r] = value;
        cout &lt;&lt; "Enqueued item: " &lt;&lt; value &lt;&lt; endl;
    }
}

// Remove an element from the queue (dequeue)
void dequeue(queue *&p) {
    if (isempty(p)) {
        cout &lt;&lt; "Dequeuing: Queue is empty" &lt;&lt; endl;
    } else {
        int a = p-&gt;array[p-&gt;f];
        p-&gt;f++;
        cout &lt;&lt; "Dequeued item: " &lt;&lt; a &lt;&lt; endl;

        // Reset the queue if it's empty
        if (p-&gt;f &gt; p-&gt;r) {
            p-&gt;f = p-&gt;r = -1;
        }
    }
}

// Display all elements in the queue
void display(queue *&p) {
    cout &lt;&lt; "Queue elements: ";
    if (isempty(p)) {
        cout &lt;&lt; "Queue is empty" &lt;&lt; endl;
    } else {
        for (int i = p-&gt;f; i &lt;= p-&gt;r; i++) {
            cout &lt;&lt; p-&gt;array[i] &lt;&lt; " ";
        }
        cout &lt;&lt; endl;
    }
}

int main() {
    cout &lt;&lt; " Name = Aasif Mohd\nRoll No = 24/A15/006" &lt;&lt; endl;
    // Create a queue
    struct queue* p;
    p = new queue;
    p-&gt;size = 10;
    p-&gt;f = -1;
    p-&gt;r = -1;
    p-&gt;array = new int[p-&gt;size];

    // Test the queue operations
    cout&lt;&lt;"Is the queue empty: "&lt;&lt;(isempty(p)?"Yes" :"No")&lt;&lt;endl;
    enqueue(p, 4);
    enqueue(p, 8);
    enqueue(p, 49);
    enqueue(p, 47);

    // Display current queue
    display(p);

    dequeue(p);
    dequeue(p);
    dequeue(p);
    dequeue(p);

    // This should show "Queue is empty"
    display(p);

    // Cleanup
    delete[] p-&gt;array;
    delete p;

    return 0;
}
</pre>
</div>

<!-- Experiment 4b (Queue using Linked List) -->
<div class="experiment">
  <button onclick="toggleCode('exp4b')">Experiment 4(b)</button>
  <button onclick="copyCode('exp4b')">Copy</button>
  <pre id="exp4b">#include &lt;iostream&gt;
using namespace std;

struct node {
    int data;
    struct node *next;
};

node *f = NULL; // Front of the queue
node *r = NULL; // Rear of the queue

// Check if the queue is empty
bool isempty() {
    return (f == NULL && r == NULL); // Queue is empty if both front and rear are NULL
}

// Add an element to the queue (enqueue)
void enqueue(int value) {
    node* newNode = new node;
    newNode->data = value;
    newNode->next = NULL;
    if(f == NULL) { // If the queue is empty
        f = r = newNode;
    } else {
        r->next = newNode;
        r = newNode;
    }

    cout << "Enqueued element: " << value << endl;
}

// Remove an element from the queue (dequeue)
void dequeue() {
    if (isempty()) {
        cout << "Dequeuing: Queue is empty" << endl;
    } else {
        node *ptr = f;
        int d = ptr->data;
        f = f->next;
        // If the queue becomes empty after dequeue
        if (f == NULL) {
            r = NULL;
        }
        delete ptr; // Use delete instead of free
        cout << "Dequeued element: " << d << endl;
    }
}

// Display all elements in the queue
void display() {
    cout << "Queue elements: ";
    if (isempty()) {
        cout << "Queue is empty" << endl;
    } else {
        node *ptr = f;
        while (ptr != NULL) {
            cout << ptr->data << " ";
            ptr = ptr->next;
        }
        cout << endl;
    }
}

int main() {
    cout << "Name = Aasif Mohd\nRoll No = 24/A15/006" << endl;
    // Test the queue operations
    cout << "Is the queue empty: " << (isempty() ? "Yes" : "No") << endl;
    enqueue(4);
    enqueue(8);
    enqueue(49);
    enqueue(54);
    // Display the queue after enqueues
    display();
    dequeue();
    dequeue();
    dequeue();
    dequeue();
    // Display the queue after dequeues
    display();
    return 0;
}
</pre>
</div>

<!-- Experiment 5 (Infix to Postfix using Stack) -->
<div class="experiment">
  <button onclick="toggleCode('exp5')">Experiment 5</button>
  <button onclick="copyCode('exp5')">Copy</button>
  <pre id="exp5">#include &lt;iostream&gt;
#include &lt;stdlib.h&gt;

using namespace std;

struct stack {
    int size;
    int top;
    char *arr;
};

int stackTop(struct stack* sp) {
    if (sp->top == -1) {
        return -1; // Return -1 if the stack is empty
    }
    return sp->arr[sp->top];
}

int isEmpty(struct stack *ptr) {
    return (ptr->top == -1);
}

int isFull(struct stack *ptr) {
    return (ptr->top == ptr->size - 1);
}

void push(struct stack* ptr, char val) {
    if (isFull(ptr)) {
        cout << "Stack Overflow! Cannot push " << val << " to the stack" << endl;
    } else {
        ptr->top++;
        ptr->arr[ptr->top] = val;
    }
}

char pop(struct stack* ptr) {
    if (isEmpty(ptr)) {
        cout << "Stack Underflow! Cannot pop from the stack" << endl;
        return -1;
    } else {
        char val = ptr->arr[ptr->top];
        ptr->top--;
        return val;
    }
}

int precedence(char ch) {
    if (ch == '*' || ch == '/') {
        return 3;
    } else if (ch == '+' || ch == '-') {
        return 2;
    } else {
        return 0;
    }
}

int isOperator(char ch) {
    return (ch == '+' || ch == '-' || ch == '*' || ch == '/');
}

char* infixToPostfix(const char* infix) {
    struct stack * sp = new stack;
    sp->size = 10;
    sp->top = -1;
    sp->arr = new char[sp->size];

    char* postfix = new char[sp->size];
    int i = 0; // Track infix traversal
    int j = 0; // Track postfix addition
    while (infix[i] != '\0') {
        if (!isOperator(infix[i])) {
            postfix[j] = infix[i];
            j++;
            i++;
        } else {
            if (precedence(infix[i]) > precedence(stackTop(sp))) {
                push(sp, infix[i]);
                i++;
            } else {
                postfix[j] = pop(sp);
                j++;
            }
        }
    }
    while (!isEmpty(sp)) {
        postfix[j] = pop(sp);
        j++;
    }
    postfix[j] = '\0';
    return postfix;
}

int main() {
    cout << " Name = Aasif Mohd\nRoll No = 24/A15/006" << endl;
    const char* infix = "x-y/z-k*d"; // Example infix expression
    cout << "Infix Expression: " << infix << endl;
    char* postfix = infixToPostfix(infix);
    cout << "Postfix Expression: " << postfix << endl;

    delete[] postfix; // Free memory for the postfix expression
    return 0;
}
</pre>
</div>

<!-- Experiment 6 (Binary Tree Traversal) -->
<div class="experiment">
  <button onclick="toggleCode('exp6')">Experiment 6</button>
  <button onclick="copyCode('exp6')">Copy</button>
  <pre id="exp6">#include &lt;iostream&gt;
#include &lt;stdlib.h&gt;
using namespace std;

struct node{
    int data;
    struct node* left;
    struct node* right;
};

struct node* createnode(int data){
    struct node* n = new node;
    n->data = data;
    n->left = NULL;
    n->right = NULL;
    return n;
}

void preorder(struct node* n){
    if(n){
        cout << n->data << " ";
        preorder(n->left);
        preorder(n->right);
    }
}

void inorder(struct node* n){
    if(n){
        inorder(n->left);
        cout << n->data << " ";
        inorder(n->right);
    }
}

void postorder(struct node* n){
    if(n){
        postorder(n->left);
        postorder(n->right);
        cout << n->data << " ";
    }
}

int main() {
    cout << " Name = Aasif Mohd\nRoll No = 24/A15/006" << endl
    <<endl;
    cout << "Binary Tree Implementation" << endl;
    struct node* n = createnode(10);
    struct node* n1 = createnode(20);
    struct node* n2 = createnode(30);
    struct node* n11 = createnode(40);
    struct node* n12 = createnode(50);
    struct node* n21 = createnode(60);
    struct node* n22 = createnode(70);

    n->left = n1;
    n->right = n2;
    n1->left = n11;
    n1->right = n12;
    n2->left = n21;
    n2->right = n22;

    /* Binary Tree Structure
        10
       /  \
      20   30
     /  \  /  \
    40  50 60  70 */

    cout << "Preorder Traversal: ";
    preorder(n);

    cout << endl;

    cout << "Inorder Traversal: ";
    inorder(n);
    cout << endl;

    cout << "Postorder Traversal: ";
    postorder(n);
    cout << endl;

    return 0;
}
</pre>
</div>

<!-- Experiment 7 (Binary Search Tree) -->
<div class="experiment">
  <button onclick="toggleCode('exp7')">Experiment 7</button>
  <button onclick="copyCode('exp7')">Copy</button>
  <pre id="exp7">#include &lt;iostream&gt;
using namespace std;

struct node {
    int data;
    struct node* left;
    struct node* right;
};

// Function to create a new node
struct node* createnode(int data) {
    struct node* n = new node;
    n->data = data;
    n->left = NULL;
    n->right = NULL;
    return n;
}

// In-order Traversal
void inorder(struct node* n) {
    if (n) {
        inorder(n->left);
        cout << n->data << " ";
        inorder(n->right);
    }
}

// Search Function with Integrated Output
struct node* searchIter(struct node* root, int key) {
    while (root != NULL) {
        if (key == root->data) {
            cout << "Found node with value " << key << endl;
            return root;
        } else if (key < root->data) {
            root = root->left;
        } else {
            root = root->right;
        }
    }
    cout << "Node with value " << key << " not found." << endl;
    return NULL;
}

// Insert Function with Confirmation Message
void insert(struct node*& root, int key) {
    if (root == NULL) {
        root = createnode(key);
        cout << "Inserted " << key << " into the BST." << endl;
        return;
    }

    struct node* current = root;
    struct node* prev = NULL;

    while (current != NULL) {
        prev = current;
        if (key == current->data) {
            cout << "Cannot insert " << key << ", already in BST" << endl;
            return;
        } else if (key < current->data) {
            current = current->left;
        } else {
            current = current->right;
        }
    }

    struct node* newNode = createnode(key);

    if (key < prev->data) {
        prev->left = newNode;
    } else {
        prev->right = newNode;
    }
    cout << "Inserted " << key << " into the BST." << endl;
}

// Delete Node Function (Direct Root Handling)
void deleteNode(struct node*& root, int value) {
    if (root == NULL) return;

    // If the node to be deleted is found
    if (value == root->data) {
        // Node with one child or no child
        if (root->left == NULL) {
            struct node* temp = root->right;
            delete root;
            root = temp;
            return;
        } else if (root->right == NULL) {
            struct node* temp = root->left;
            delete root;
            root = temp;
            return;
        }

        // Node with two children: Get in-order predecessor
        struct node* iPre = root->left;
        while (iPre->right) {
            iPre = iPre->right;
        }

        // Replace data with predecessor's data
        root->data = iPre->data;

        // Delete the predecessor
        deleteNode(root->left, iPre->data);
    }
    // If the node to be deleted is not found, continue searching
    else if (value < root->data) {
        deleteNode(root->left, value);
    } else {
        deleteNode(root->right, value);
    }
}

int main() {
    cout<<" Name = Aasif Mohd\nRoll No = 24/A15/006"<<endl<<endl;
    struct node* root = NULL;

    // Insert Nodes
    insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 40);
    insert(root, 60);
    insert(root, 80);

    // In-order Traversal
    cout << "# In-order Traversal: ";
    inorder(root);
    cout << endl;

    // Search with Integrated Output
    cout << "# Searching Node with value 30:"<<endl;
    searchIter(root, 30); // Found
    cout << "# Searching Node with value 100:"<<endl;
    searchIter(root, 100); // Not Found

    // Delete a Node (Direct Call)
    cout << "# Deleting node with value 50..." << endl;
    deleteNode(root, 50); // Direct call without reassigning root

    // In-order Traversal After Deletion
    cout << "# In-order Traversal After Deletion: ";
    inorder(root);
    cout << endl;

    return 0;
}
</pre>
</div>

<!-- Experiment 8a (Breadth-First Search) -->
<div class="experiment">
  <button onclick="toggleCode('exp8a')">Experiment 8a</button>
  <button onclick="copyCode('exp8a')">Copy</button>
  <pre id="exp8a">#include &lt;iostream&gt;
using namespace std;

struct queue {
    int size;
    int f;
    int r;
    int* arr;
};

// Check if the queue is empty
int isEmpty(struct queue* q) {
    return (q->r == q->f);
}

// Check if the queue is full
int isFull(struct queue* q) {
    return (q->r == q->size - 1);
}

// Enqueue operation
void enqueue(struct queue* q, int val) {
    if (isFull(q)) {
        cout << "This Queue is full" << endl;
    } else {
        q->r++;
        q->arr[q->r] = val;
    }
}

// Dequeue operation
int dequeue(struct queue* q) {
    int a = -1;
    if (isEmpty(q)) {
        cout << "This Queue is empty" << endl;
    } else {
        q->f++;
        a = q->arr[q->f];
    }
    return a;
}

int main() {
    cout << " Name = Aasif Mohd\nRoll No = 24/A15/006" << endl << endl;
    struct queue* q = new queue;
    q->size = 400;
    q->f = q->r = -1;
    q->arr = new int[q->size];

    // BFS Implementation
    int node;
    int i = 1; // Starting from node 1
    int visited[7] = {0, 0, 0, 0, 0, 0, 0};
    int a[7][7] = {
        {0, 1, 1, 1, 0, 0, 0},
        {1, 0, 1, 0, 0, 0, 0},
        {1, 1, 0, 1, 1, 0, 0},
        {1, 0, 1, 0, 1, 0, 0},
        {0, 0, 1, 1, 0, 1, 1},
        {0, 0, 0, 0, 1, 0, 0},
        {0, 0, 0, 0, 1, 0, 0}
    };

    cout << "Breadth-First Search Traversal Starting from node 1: " << endl;
    // BFS starting node
    cout << i << " ";
    visited[i] = 1;
    enqueue(q, i); // Enqueue i for exploration
    // BFS Traversal
    while (!isEmpty(q)) {
        int node = dequeue(q);
        for (int j = 0; j < 7; j++) {
            if (a[node][j] == 1 && visited[j] == 0) {
                cout << j << " ";
                visited[j] = 1;
                enqueue(q, j);
            }
        }
    }

    // Cleanup
    delete[] q->arr;
    delete q;
    return 0;
}
</pre>
</div>

<!-- Experiment 8b (Depth-First Search) -->
<div class="experiment">
  <button onclick="toggleCode('exp8b')">Experiment 8b</button>
  <button onclick="copyCode('exp8b')">Copy</button>
  <pre id="exp8b">#include &lt;iostream&gt;
using namespace std;

int visited[7] = {0,0,0,0,0,0,0};
int A [7][7] = {
    {0,1,1,1,0,0,0},
    {1,0,1,0,0,0,0},
    {1,1,0,1,1,0,0},
    {1,0,1,0,1,0,0},
    {0,0,1,1,0,1,1},
    {0,0,0,0,1,0,0},
    {0,0,0,0,1,0,0}
};

void DFS(int i){
    cout << i << " ";
    visited[i] = 1;
    for (int j = 0; j < 7; j++) {
        if(A[i][j] == 1 && !visited[j]){
            DFS(j);
        }
    }
}

int main(){
    cout << " Name = Aasif Mohd\nRoll No = 24/A15/006" << endl << endl;
    // DFS Implementation when the root node is 0
    cout << "Depth-First Search Traversal Starting from Node 0: " << endl;
    DFS(0);
    return 0;
}
</pre>
</div>

<!-- Experiment 9 (Linear and Binary Search) -->
<div class="experiment">
  <button onclick="toggleCode('exp9')">Experiment 9</button>
  <button onclick="copyCode('exp9')">Copy</button>
  <pre id="exp9">#include &lt;iostream&gt;
using namespace std;

// Function to print the array
void printArray(int arr[], int size) {
    cout &lt;&lt; "Array: ";
    for (int i = 0; i &lt; size; i++) {
        cout &lt;&lt; arr[i] &lt;&lt; " ";
    }
    cout &lt;&lt; endl;
}

// Linear Search Function
int linearSearch(int arr[], int size, int key) { // Added 'size' parameter
    for (int i = 0; i &lt; size; i++) {
        if (arr[i] == key) {
            return i; // Return index if key is found
        }
    }
    return -1; // Return -1 if not found
}

// Binary Search Function (Requires Sorted Array)
int binarySearch(int arr[], int size, int key) { // Added 'size' parameter
    int left = 0, right = size - 1;

    while (left &lt;= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == key) {
            return mid; // Return index if key is found
        }
        else if (arr[mid] &lt; key) {
            left = mid + 1; // Search in the right half
        }
        else {
            right = mid - 1; // Search in the left half
        }
    }
    return -1; // Return -1 if not found
}

int main() {
    cout &lt;&lt; " Name = Aasif Mohd\nRoll No = 24/A15/006" &lt;&lt; endl &lt;&lt; endl;
    int arr[] = {2, 4, 6, 8, 10, 12, 14, 16, 18, 20};
    int size = sizeof(arr) / sizeof(arr[0]);
    int key;
    printArray(arr, size);
    cout &lt;&lt; "Enter the number to search: ";
    cin &gt;&gt; key;

    // Linear Search
    int linearResult = linearSearch(arr, size, key); // Pass 'size' as argument
    if (linearResult != -1) {
        cout &lt;&lt; "Linear Search: Element " &lt;&lt; key &lt;&lt; " found at index " &lt;&lt; linearResult &lt;&lt; endl;
    } else {
        cout &lt;&lt; "Linear Search: Element " &lt;&lt; key &lt;&lt; " not found." &lt;&lt; endl;
    }

    // Binary Search
    int binaryResult = binarySearch(arr, size, key); // Pass 'size' as argument
    if (binaryResult != -1) {
        cout &lt;&lt; "Binary Search: Element " &lt;&lt; key &lt;&lt; " found at index " &lt;&lt; binaryResult &lt;&lt; endl;
    } else {
        cout &lt;&lt; "Binary Search: Element " &lt;&lt; key &lt;&lt; " not found." &lt;&lt; endl;
    }

    return 0;
}
</pre>
</div>

<!-- Experiment 10 (Bubble Sort, Insertion Sort, Merge Sort) -->
<div class="experiment">
  <button onclick="toggleCode('exp10')">Experiment 10</button>
  <button onclick="copyCode('exp10')">Copy</button>
  <pre id="exp10">#include &lt;iostream&gt;
using namespace std;

void printArray(int *A, int n)
{
    for (int i = 0; i &lt; n; i++)
    {
        cout &lt;&lt; A[i] &lt;&lt; " ";
    }
    cout &lt;&lt; endl;
}

void bubbleSort(int A[], int n) {
    for (int i = 0; i &lt; n - 1; i++) {
        for (int j = 0; j &lt; n - i - 1; j++) {
            if (A[j] &gt; A[j + 1]) {
                swap(A[j], A[j + 1]);
            }
        }
    }
}

void insertionSort(int A[], int m) {
    for (int i = 1; i &lt; m; i++) {
        int key = A[i];
        int j = i - 1;
        while (j &gt;= 0 && A[j] &gt; key) {
            A[j + 1] = A[j];
            j--;
        }
        A[j + 1] = key;
    }
}

void merge(int A[], int mid, int low, int high)
{
    int i, j, k, B[100];
    i = low;
    j = mid + 1;
    k = low;

    while (i &lt;= mid && j &lt;= high)
    {
        if (A[i] &lt; A[j])
        {
            B[k] = A[i];
            i++;
            k++;
        }
        else
        {
            B[k] = A[j];
            j++;
            k++;
        }
    }
    while (i &lt;= mid)
    {
        B[k] = A[i];
        k++;
        i++;
    }
    while (j &lt;= high)
    {
        B[k] = A[j];
        k++;
        j++;
    }

    for (int i = low; i &lt;= high; i++)
    {
        A[i] = B[i];
    }
}

void mergeSort(int A[], int low, int high){
    int mid;
    if(low&lt;high){
        mid = (low + high) /2;
        mergeSort(A, low, mid);
        mergeSort(A, mid+1, high);
        merge(A, mid, low, high);
    }
}

int main(){
    cout &lt;&lt; " Name = Aasif Mohd\nRoll No = 24/A15/006" &lt;&lt; endl
    &lt;&lt; endl;
    int A[] = {9, 1, 4, 14, 4, 15, 6};
    int n = 7;
    cout&lt;&lt;"----BUBBLE SORT----"&lt;&lt;endl;
    cout&lt;&lt;"Original array: ";
    printArray(A, n);
    bubbleSort(A, n);
    cout&lt;&lt;"Sorted array: ";
    printArray(A, n);
    cout&lt;&lt;endl;
    int B[] = {4, 2, 1, 4, 9, 5, 6};
    int m = 7;
    cout&lt;&lt;"----INSERTION SORT----"&lt;&lt;endl;
    cout&lt;&lt;"Original array: ";
    printArray(B, m);
    insertionSort(B, m);
    cout&lt;&lt;"Sorted array: ";
    printArray(B, m);
    cout&lt;&lt;endl;
    int C[] = {8, 2, 7, 4, 1, 5, 4};
    int o = 7;
    cout&lt;&lt;"----MERGE SORT----"&lt;&lt;endl;
    cout&lt;&lt;"Original array: ";
    printArray(C, o);
    mergeSort(C, 0, o-1);
    cout&lt;&lt;"Sorted array: ";
    printArray(C, o);
    return 0;
}
</pre>
</div>




