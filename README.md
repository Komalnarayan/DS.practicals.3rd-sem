# DS.practicals.3rd-sem
1. Write a shortest program to implement singly linked list as an ADT that supports the following oper-

ations:

i. Insert an element x at the beginning of the singly linked list

ii. Insert an element x at i

th position in the singly linked list

iii. Remove an element from the beginning of the doubly linked list

iv. Remove an element from ith position in the singly linked list.
v. Search for an element x in the singly linked list and return its pointer.





```
#include<iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int x) : data(x), next(NULL) {}
};

class SLL {
    Node* head;
public:
    SLL() : head(NULL) {}

    void insertBegin(int x) {
        Node* n = new Node(x);
        n->next = head;
        head = n;
    }

    void insertAt(int x, int pos) {
        if (pos == 0) { insertBegin(x); return; }
        Node* t = head;
        for (int i = 0; t && i < pos - 1; i++) t = t->next;
        if (!t) return;
        Node* n = new Node(x);
        n->next = t->next;
        t->next = n;
    }

    void removeBegin() {
        if (!head) return;
        Node* t = head;
        head = head->next;
        delete t;
    }

    void removeAt(int pos) {
        if (pos == 0) { removeBegin(); return; }
        Node* t = head;
        for (int i = 0; t && i < pos - 1; i++) t = t->next;
        if (!t || !t->next) return;
        Node* d = t->next;
        t->next = d->next;
        delete d;
    }

    Node* search(int x) {
        Node* t = head;
        while (t) {
            if (t->data == x) return t;
            t = t->next;
        }
        return NULL;
    }

    void display() {
        Node* t = head;
        while (t) {
            cout << t->data << " -> ";
            t = t->next;
        }
        cout << "NULL\n";
    }
};

int main() {
    SLL list;

    list.insertBegin(10);
    list.insertBegin(20);
    list.insertBegin(30);
    cout << "After inserting 30, 20, 10 at beginning:\n";
    list.display();

    list.insertAt(25, 2);
    cout << "After inserting 25 at position 2:\n";
    list.display();

    list.removeBegin();
    cout << "After removing from beginning:\n";
    list.display();

    list.removeAt(1);
    cout << "After removing from position 1:\n";
    list.display();

    int key = 25;
    Node* result = list.search(key);
    if (result)
        cout << key << " found at node with address: " << result << endl;
    else
        cout << key << " not found in the list.\n";

    return 0;
}
```

2. Write a program to implement doubly linked list as an ADT that supports the following op-

erations:

i. Insert an element x at the beginning of the doubly linked list

ii. Insert an element x at the end of the doubly linked list

iii. Remove an element from the beginning of the doubly linked list

iv. Remove an element from the end of the doubly linked list


```
#include<iostream>
using namespace std;

struct Node {
    int data;
    Node *prev, *next;
    Node(int x) : data(x), prev(NULL), next(NULL) {}
};

class DLL {
    Node *head = NULL, *tail = NULL;
public:
    void insertBegin(int x) {
        Node* n = new Node(x);
        n->next = head;
        if (head) head->prev = n; else tail = n;
        head = n; display();
    }

    void insertEnd(int x) {
        Node* n = new Node(x);
        n->prev = tail;
        if (tail) tail->next = n; else head = n;
        tail = n; display();
    }

    void removeBegin() {
        if (!head) return;
        Node* t = head; head = head->next;
        if (head) head->prev = NULL; else tail = NULL;
        delete t; display();
    }

    void removeEnd() {
        if (!tail) return;
        Node* t = tail; tail = tail->prev;
        if (tail) tail->next = NULL; else head = NULL;
        delete t; display();
    }

    void display() {
        for (Node* c = head; c; c = c->next) cout << c->data << " <-> ";
        cout << "NULL\n";
    }
};

int main() {
    DLL l;
    l.insertBegin(10);
    l.insertBegin(20);
    l.insertEnd(30);
    l.removeBegin();
    l.removeEnd();
}
```

3. Write a program to implement circular linked list as an ADT which supports the following 

operations:

i.Insert an element x in the list

ii.Remove an element from the list

iii.Search for an element x in the list and return its pointer

```

#include<iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int x) : data(x), next(this) {}
};

class CLL {
    Node* last = NULL;
public:
    void insert(int x) {
        Node* n = new Node(x);
        if (!last) last = n;
        else { n->next = last->next; last->next = n; last = n; }
        display();
    }

    void remove(int x) {
        if (!last) return;
        Node *curr = last->next, *prev = last;
        do {
            if (curr->data == x) {
                if (curr == last && curr->next == last) last = NULL;
                else { if (curr == last) last = prev; prev->next = curr->next; }
                delete curr; display(); return;
            }
            prev = curr; curr = curr->next;
        } while (curr != last->next);
    }

    Node* search(int x) {
        if (!last) return NULL;
        Node* curr = last->next;
        do { if (curr->data == x) return curr; curr = curr->next; } while (curr != last->next);
        return NULL;
    }

    void display() {
        if (!last) { cout << "Empty\n"; return; }
        Node* curr = last->next;
        do { cout << curr->data << " "; curr = curr->next; } while (curr != last->next);
        cout << "(loop)\n";
    }
};

int main() {
    CLL list;
    list.insert(10);
    list.insert(20);
    list.insert(30);
    list.remove(20);
    cout << (list.search(10) ? "Found" : "Not Found") << endl;
}
```


4. Write a shortest program to Implement Stack as an ADT and use it to evaluate a prefix/postfix expression.
```
#include<iostream>
#include<stack>
using namespace std;

int main() {
    stack<int> s;
    string expr = "53+82-*";
    for (char c : expr)
        if (isdigit(c)) s.push(c - '0');
        else { int b = s.top(); s.pop(); int a = s.top(); s.pop();
            s.push(c=='+'?a+b:c=='-'?a-b:c=='*'?a*b:a/b);
        }
    cout << s.top();
}
```



5. Implement Queue as an ADT.
```
#include<iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int x) : data(x), next(NULL) {}
};

class Queue {
    Node *f, *r;
public:
    Queue() : f(NULL), r(NULL) {}

    void enqueue(int x) {
        Node* n = new Node(x);
        if (!r) f = r = n;
        else r = r->next = n;
    }

    void dequeue() {
        if (!f) return;
        Node* t = f;
        f = f->next;
        if (!f) r = NULL;
        delete t;
    }

    void display() {
        for (Node* c = f; c; c = c->next)
            cout << c->data << " ";
        cout << endl;
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.display();
    q.dequeue();
    q.display();
}


```
6. Write a program to implement Binary Search Tree as an ADT which supports the following 

operations:

i.Insert an element x

ii.Delete an element x

iii.Search for an element x in the BST 

iv.Display the elements of the BST in preorder, inorder, and postorder traversal
```
#include<iostream>
using namespace std;

struct Node {
    int d; Node* l, *r;
    Node(int x) : d(x), l(0), r(0) {}
};

class BST {
    Node* r;
    Node* ins(Node* n, int x) {
        if (!n) return new Node(x);
        x < n->d ? n->l = ins(n->l, x) : n->r = ins(n->r, x);
        return n;
    }
    Node* mn(Node* n) {
        while (n->l) n = n->l;
        return n;
    }
    Node* rem(Node* n, int x) {
        if (!n) return 0;
        if (x < n->d) n->l = rem(n->l, x);
        else if (x > n->d) n->r = rem(n->r, x);
        else {
            if (!n->l) return n->r;
            if (!n->r) return n->l;
            Node* t = mn(n->r);
            n->d = t->d;
            n->r = rem(n->r, t->d);
        }
        return n;
    }
    Node* sr(Node* n, int x) {
        if (!n || n->d == x) return n;
        return x < n->d ? sr(n->l, x) : sr(n->r, x);
    }
    void pre(Node* n) { if (n) { cout << n->d << " "; pre(n->l); pre(n->r); } }
    void in(Node* n) { if (n) { in(n->l); cout << n->d << " "; in(n->r); } }
    void post(Node* n) { if (n) { post(n->l); post(n->r); cout << n->d << " "; } }
public:
    BST() : r(0) {}
    void insert(int x) { r = ins(r, x); }
    void remove(int x) { r = rem(r, x); }
    Node* search(int x) { return sr(r, x); }
    void display() {
        cout << "Pre: "; pre(r); cout << "\nIn: "; in(r); cout << "\nPost: "; post(r); cout << endl;
    }
};

int main() {
    BST t;
    t.insert(50); t.insert(30); t.insert(70); t.insert(20); t.insert(40);
    t.display();
    t.remove(30);
    cout << "After deleting 30:\n"; t.display();
    cout << (t.search(70) ? "Found" : "Not Found");
}
```
7. Write a program to implement insert and search operation in AVL trees.
```
#include<iostream>
using namespace std;

struct Node {
    int d, h; Node *l, *r;
    Node(int x) : d(x), h(1), l(0), r(0) {}
};

int h(Node* n) { return n ? n->h : 0; }
int bal(Node* n) { return n ? h(n->l) - h(n->r) : 0; }

Node* rotR(Node* y) {
    Node* x = y->l;
    y->l = x->r; x->r = y;
    y->h = 1 + max(h(y->l), h(y->r));
    x->h = 1 + max(h(x->l), h(x->r));
    return x;
}

Node* rotL(Node* x) {
    Node* y = x->r;
    x->r = y->l; y->l = x;
    x->h = 1 + max(h(x->l), h(x->r));
    y->h = 1 + max(h(y->l), h(y->r));
    return y;
}

Node* ins(Node* r, int k) {
    if (!r) return new Node(k);
    if (k < r->d) r->l = ins(r->l, k);
    else if (k > r->d) r->r = ins(r->r, k);
    else return r;
    r->h = 1 + max(h(r->l), h(r->r));
    int b = bal(r);
    if (b > 1 && k < r->l->d) return rotR(r);
    if (b < -1 && k > r->r->d) return rotL(r);
    if (b > 1 && k > r->l->d) { r->l = rotL(r->l); return rotR(r); }
    if (b < -1 && k < r->r->d) { r->r = rotR(r->r); return rotL(r); }
    return r;
}

Node* find(Node* r, int k) {
    if (!r || r->d == k) return r;
    return k < r->d ? find(r->l, k) : find(r->r, k);
}

void in(Node* r) {
    if (r) { in(r->l); cout << r->d << " "; in(r->r); }
}

int main() {
    Node* r = 0;
    for (int x : {20,10,30,25}) r = ins(r, x);
    in(r); cout << endl;
    cout << (find(r, 25) ? "Found" : "Not Found");
}

```
