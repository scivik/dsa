# dsa

## 1
```cpp
#include <iostream>
#include <string>

using namespace std;

class Student {
public:
    int rollNo;
    string name;
    float sgpa;
};

void displayList(Student arr[], int n) {
    cout << "Roll No\tName\tSGPA\n";
    for (int i = 0; i < n; i++) {
        cout << arr[i].rollNo << "\t" << arr[i].name << "\t" << arr[i].sgpa << "\n";
    }
    cout << endl;
}

void swapStudents(Student &a, Student &b) {
    Student temp = a;
    a = b;
    b = temp;
}

// Bubble Sort
void sortByRollNo(Student arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j].rollNo > arr[j + 1].rollNo) {
                swapStudents(arr[j], arr[j + 1]);
            }
        }
    }
}

// Insertion Sort
void sortAlphabetically(Student arr[], int n) {
    for (int i = 1; i < n; i++) {
        Student key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j].name > key.name) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

// Quick Sort
int partition(Student arr[], int low, int high) {
    float pivot = arr[high].sgpa;
    int i = low - 1;
    for (int j = low; j <= high - 1; j++) {
        if (arr[j].sgpa >= pivot) {
            i++;
            swapStudents(arr[i], arr[j]);
        }
    }
    swapStudents(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(Student arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Binary Search
int binarySearchByName(Student arr[], int low, int high, string name) {
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid].name == name) {
            return mid;
        }
        if (arr[mid].name < name) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return -1;
}

int main() {
    const int n = 10; // Assuming there are at least 10 records in the database
    Student studentList[n] = {
        {101, "John", 8.5},
        {102, "Alice", 9.2},
        {103, "Bob", 8.7},
        // Add more records as needed
    };

    // a) Sort by Roll No (Bubble Sort)
    sortByRollNo(studentList, n);
    cout << "Sorted by Roll No:\n";
    displayList(studentList, n);

    // b) Sort alphabetically (Insertion Sort)
    sortAlphabetically(studentList, n);
    cout << "Sorted alphabetically:\n";
    displayList(studentList, n);

    // c) Sort by SGPA (Quick Sort) to find top 10 toppers
    quickSort(studentList, 0, n - 1);
    cout << "Top 10 Toppers:\n";
    displayList(studentList, min(10, n));

    // d) Search students by SGPA
    float searchSGPA;
    cout << "Enter SGPA to search: ";
    cin >> searchSGPA;
    cout << "Students with SGPA " << searchSGPA << ":\n";
    for (int i = 0; i < n; i++) {
        if (studentList[i].sgpa == searchSGPA) {
            cout << studentList[i].rollNo << "\t" << studentList[i].name << "\n";
        }
    }

    // e) Search student by name (Binary Search)
    string searchName;
    cout << "Enter name to search: ";
    cin >> searchName;
    int result = binarySearchByName(studentList, 0, n - 1, searchName);
    if (result != -1) {
        cout << "Student found at index " << result << ":\n";
        cout << studentList[result].rollNo << "\t" << studentList[result].name << "\t" << studentList[result].sgpa << "\n";
    } else {
        cout << "Student not found.\n";
    }

    return 0;
}
```

## 2

```cpp
#include<iostream>
#include<string.h>
using namespace std;
struct node
{ int prn,rollno;
char name[50];
struct node *next;
};
class info
{
node
*s=NULL,*head1=NULL,*temp1=NULL,*head2=NULL,*temp2=NULL,*head=NULL,*temp=NULL;
int b,c,i,j,ct;
char a[20];
public:
node *create();
void insertp();
void insertm();
void delm();
void delp();
void dels();
void display();
void count();
void reverse();
void rev(node *p);
void concat();
} ;
node *info::create()
{ node *p=new(struct node);
cout<<"enter name of student ";
cin>>a;
strcpy(p->name,a);
cout<<"\n enter prn no. of student \n";
cin>>b;
p->prn=b;
cout<<"enter student rollno";
cin>>c;
p->rollno=c;
p->next=NULL;
return p;
}
void info::insertm()
{
node *p=create();
if(head==NULL)
{ 
    head=p;
}
else
{ 
    temp=head;
while(temp->next!=NULL)
{ 
    temp=temp->next;
}
temp->next=p;
}
}
void info::insertp()
{
node *p=create();
if(head==NULL)
{ head=p;
}
else
{ 
    temp=head;
head=p;
head->next=temp->next;
}
}
void info::display()
{ if(head==NULL)
{ cout<<"linklist is empty";
}
else
{
temp=head;
cout<<" prn rolln0 NAME \n";
while(temp->next!=NULL)
{ cout<<" \n"<<temp->prn<<" "<<temp->rollno<<" "<<temp->name;
temp=temp->next;
}
cout<<" "<<temp->prn<<" "<<temp->rollno<<" "<<temp->name;
}
}
void info::delm()
{ int m,f=0;
cout<<"\n enter the prn no. of student whose data you want to delete";
cin>>m;
temp=head;
while(temp->next!=NULL)
{
if(temp->prn==m)
{ s->next=temp->next;
delete(temp); f=1;
}
s=temp;
temp=temp->next;
} if(f==0)
{ cout<<"\n sorry memeber not deleted "; }
}
void info::delp()
{ temp=head;
head=head->next;
delete(temp);
}
void info::dels()
{
temp=head;
while(temp->next!=NULL)
{ s=temp;
temp=temp->next;
} s->next=NULL;
delete(temp);
}
void info::count()
{ temp=head; ct=0;
while(temp->next!=NULL)
{ temp=temp->next; ct++; }
ct++;
cout<<" Count of members is:"<<ct;
}
void info::reverse()
{ rev(head); }
void info::rev(node *temp)
{ if(temp==NULL)
{ return; }
else
{ rev(temp->next); }
cout<<" "<<temp->prn<<" "<<temp->rollno<<" "<<temp->name;
}
void info::concat()
{ int k,j;
cout<<"enter no. of members in list1";
cin>>k;
head=NULL;
for(i=0;i<k;i++)
{ insertm();
head1=head;
} head=NULL;
cout<<"enter no. of members in list2";
cin>>j;
for(i=0;i<j;i++)
{ insertm();
head2=head;
} head=NULL;
temp1=head1;
while(temp1->next!=NULL)
{ temp1=temp1->next; }
temp1->next=head2;
temp2=head1;
cout<<" prn rolln0 NAME \n";
while(temp2->next!=NULL)
{
cout<<"\n "<<temp2->prn<< "temp2=temp2->next";
"<<temp2->rollno<<" "<<temp2->name<<\n";;
}
cout<<"\n "<<temp2->prn<<" "<<temp2->rollno<<" "<<temp2->name<<"\n";
}
int main()
{ info s;
int i;
char ch;
do{
cout<<"\n choice the options";
cout<<"\n 1. To insert president ";
cout<<"\n 2. To insert member ";
cout<<"\n 3. To insert secretary ";
cout<<"\n 4. To delete president ";
cout<<"\n 5. To delete member ";
cout<<"\n 6. To delete secretary ";
cout<<"\n 7. To display data ";
cout<<"\n 8. Count of members";
cout<<"\n 9. To display reverse of string ";
cout<<"\n 10.To concatenate two strings ";
cin>>i;
switch(i)
{ case 1: s.insertp();
break;
case 2: s.insertm();
break;
case 3: s.insertm();
break;
case 4: s.delp();
break;
case 5: s.delm();
break;
case 6: s.dels();
break;
case 7: s.display();
break;
case 8: s.count();
break;
case 9: s.reverse();
break;
case 10: s.concat();
break;
default: cout<<"\n unknown choice";
}
cout<<"\n do you want to continue enter y/Y \n";
cin>>ch;
}while(ch=='y'||ch=='Y');
return 0;
}
```

## 3

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <sstream>

using namespace std;

// Node class for the linked list
class Node {
public:
    int data;
    Node* next;

    Node(int val) : data(val), next(nullptr) {}
};

// Stack class using a linked list
class LinkedListStack {
private:
    Node* top;

public:
    LinkedListStack() : top(nullptr) {}

    void push(int val) {
        Node* newNode = new Node(val);
        newNode->next = top;
        top = newNode;
    }

    int pop() {
        if (isEmpty()) {
            cerr << "Stack is empty. Cannot pop.\n";
            return -1; // Assuming -1 as an error value
        }

        int poppedValue = top->data;
        Node* temp = top;
        top = top->next;
        delete temp;

        return poppedValue;
    }

    int peek() {
        if (isEmpty()) {
            cerr << "Stack is empty. Cannot peek.\n";
            return -1; // Assuming -1 as an error value
        }
        return top->data;
    }

    bool isEmpty() {
        return top == nullptr;
    }
};

int evaluatePostfixExpression(const string& exp) {
    LinkedListStack stack;
    stringstream ss(exp);
    string token;

    while (ss >> token) {
        if (isdigit(token[0]) || (token[0] == '-' && token.length() > 1 && isdigit(token[1]))) {
            // If the token is a number (positive or negative), convert it to an integer and push it onto the stack
            int value = stoi(token);
            stack.push(value);
        } else if (token == "+" || token == "-" || token == "*" || token == "/") {
            // If the token is an operator, pop the top two elements from the stack, perform the operation, and push the result back onto the stack
            int operand2 = stack.pop();
            int operand1 = stack.pop();

            if (token == "+") {
                stack.push(operand1 + operand2);
            } else if (token == "-") {
                stack.push(operand1 - operand2);
            } else if (token == "*") {
                stack.push(operand1 * operand2);
            } else if (token == "/") {
                stack.push(operand1 / operand2);
            }
        } else {
            cerr << "Invalid token encountered: " << token << endl;
            return -1; // Assuming -1 as an error value
        }
    }

    if (!stack.isEmpty()) {
        return stack.pop();
    } else {
        cerr << "Invalid postfix expression." << endl;
        return -1; // Assuming -1 as an error value
    }
}

int main() {
    string postfixExpression = "5 3 8 * + 10 -"; // Example postfix expression
    int result = evaluatePostfixExpression(postfixExpression);
    
    if (result != -1) {
        cout << "Result of the postfix expression is: " << result << endl;
    }

    return 0;
}
```

## 4
```cpp
#include<iostream>
using namespace std;
const int MAX=5;
class Job
{
int id;
int priority;
friend class Queue;
public:
void getdata()
{
cout<<"\nENter Job id: ";
cin>>id;
cout<<"\nEnter Job priority: ";
cin>>priority;
}
void putdata()
{
cout<<"\n\t"<<id;
cout<<"\t\t"<<priority;
}
};

class Queue
{
int front,rear;
Job queue[MAX];
public:
Queue()
{
front=rear=-1;
}
bool isEmpty();
bool isFull();
void insert();
void remove();
void display();

};
bool Queue::isEmpty()
{
if(front==(rear+1)||rear==-1)
return 1;
else return 0;
}

bool Queue::isFull()
{
if(rear==MAX-1)
{
return 1;
}
else
return 0;
}
void Queue::insert()
{
Job j;

if(isFull())
{
cout<<"\nQueue is Full.";
}
else
{
j.getdata();
if(rear==-1)//empty
{
front++;
rear++;

queue[rear]=j;
}
else
{

int i=rear;
while(i>=front && queue[i].priority>j.priority)
{
queue[i+1]=queue[i];
i--;
}
queue[i+1]=j;
rear++;
}
cout<<"\nJob Added To Queue.";
}
}

void Queue::remove()
{
if(rear==-1||front==(rear+1))
{
cout<<"\nQueue is Empty.";
}
else
{
front++;
cout<<"\nJob Processed From Queue.";
}
}
void Queue::display()
{
if(isEmpty())
{
cout<<"\nQueue is Empty.";
}
else
{
for(int i=front;i<=rear;i++)
{
queue[i].putdata();
}
}
}

int main()
{

int ch;
Queue q;

do
{

cout<<"\n\n****MENU****\n";
cout<<"1.Insert job\n";
cout<<"2.Display jobs\n";
cout<<"3.Remove job\n";
cout<<"4.Exit\n";

cout<<"Choice: ";
cin>>ch;

switch(ch)
{

case 1: q.insert();
break;

case 2: cout<<"\n\tJob id ";
cout<<"\t  Job priority ";
q.display();
break;

case 3: q.remove();
}
}while(ch!=4);
return 0;
}
```
## 5
```cpp
#include<iostream>
//#include
//#include
using namespace std;
#define SIZE 5
// ERROR HANDLINH NOT DOne

//    program is not working correct.
//
class dequeue
{

int a[10],front,rear,count;

public:
dequeue();
void add_at_beg(int);
void add_at_end(int);
void delete_fr_front();
void delete_fr_rear();
void display();
};


dequeue::dequeue()
{
front=-1;
rear=-1;
count=0;
}


void dequeue::add_at_beg(int item)
{
int  i;
if(front==-1)
{
front++;
rear++;
a[rear]=item;
count++;
}
else if(rear>=SIZE-1)
{
cout<<"\nInsertion is not possible,overflow!!!!";
}
else
{
for(i=count;i>=0;i--)
{
a[i]=a[i-1];
}
a[i]=item;
count++;
rear++;
}
}



void dequeue::add_at_end(int item)
{

if(front==-1)
{
front++;
rear++;
a[rear]=item;
count++;
}
else if(rear>=SIZE-1)
{
cout<<"\nInsertion is not possible,overflow!!!";
return;
}
else
{
a[++rear]=item;
}


}



void dequeue::display()
{

for(int i=front;i<=rear;i++)
{
cout<<a[i]<<" "; }
}


void dequeue::delete_fr_front()
{
if(front==-1)
{
cout<<"Deletion is not possible:: Dequeue is empty";
return;
}
else
{
if(front==rear)
{
front=rear=-1;
return;
}
cout<<"The deleted element is "<<a[front];
front=front+1;
}


}

void dequeue::delete_fr_rear()
{
if(front==-1)
{
cout<<"Deletion is not possible:Dequeue is empty";
return;
}
else
{
if(front==rear)
{
front=rear=-1;
}
cout<<"The deleted element is "<< a[rear];
rear=rear-1;
}


}



int main()
{
int c,item;
dequeue d1;

do
{
cout<<"\n\n****DEQUEUE OPERATION****\n";
cout<<"\n1-Insert at beginning";
cout<<"\n2-Insert at end";
cout<<"\n3_Display";
cout<<"\n4_Deletion from front";
cout<<"\n5-Deletion from rear";
cout<<"\n6_Exit";
cout<<"\nEnter your choice<1-4>:";
cin>>c;

switch(c)
{
case 1:
cout<<"Enter the element to be inserted:";
cin>>item;
d1.add_at_beg(item);
break;

case 2:
cout<<"Enter the element to be inserted:";
cin>>item;
d1.add_at_end(item);
break;

case 3:
d1.display();
break;

case 4:
d1.delete_fr_front();
break;
case 5:
d1.delete_fr_rear();
break;

case 6:
exit(1);
break;

default:
cout<<"Invalid choice";
break;
}

}while(c!=7);
return 0;

}
```
## 6

```cpp
#include <iostream>
#include <string.h>
using namespace std;

struct node // Node Declaration
{
    string label;
    //char label[10];
    int ch_count;
    struct node *child[10];
} * root;

class GT // Class Declaration
{
public:
    void create_tree();
    void display(node *r1);

    GT()
    {
        root = NULL;
    }
};

void GT::create_tree()
{
    int tbooks, tchapters, i, j, k;
    root = new node;
    cout << "Enter name of book : ";
    cin.get();
    getline(cin, root->label);
    cout << "Enter number of chapters in book : ";
    cin >> tchapters;
    root->ch_count = tchapters;
    for (i = 0; i < tchapters; i++)
    {
        root->child[i] = new node;
        cout << "Enter the name of Chapter " << i + 1 << " : ";
        cin.get();
        getline(cin, root->child[i]->label);
        cout << "Enter number of sections in Chapter : " << root->child[i]->label << " : ";
        cin >> root->child[i]->ch_count;
        for (j = 0; j < root->child[i]->ch_count; j++)
        {
            root->child[i]->child[j] = new node;
            cout << "Enter Name of Section " << j + 1 << " : ";
            cin.get();
            getline(cin, root->child[i]->child[j]->label);
        }
    }
}

void GT::display(node *r1)
{
    int i, j, k, tchapters;
    if (r1 != NULL)
    {
        cout << "\n-----Book Hierarchy---";
        cout << "\n Book title : " << r1->label;
        tchapters = r1->ch_count;
        for (i = 0; i < tchapters; i++)
        {

            cout << "\nChapter " << i + 1;
            cout << " : " << r1->child[i]->label;
            cout << "\nSections : ";
            for (j = 0; j < r1->child[i]->ch_count; j++)
            {
                cout << "\n"<< r1->child[i]->child[j]->label;
            }
        }
    }
    cout << endl;
}

int main()
{
    int choice;
    GT gt;
    while (1)
    {
        cout << "-----------------" << endl;
        cout << "Book Tree Creation" << endl;
        cout << "-----------------" << endl;
        cout << "1.Create" << endl;
        cout << "2.Display" << endl;
        cout << "3.Quit" << endl;
        cout << "Enter your choice : ";
        cin >> choice;
        switch (choice)
        {
        case 1:
            gt.create_tree();
        case 2:
            gt.display(root);
            break;
        case 3:
            cout << "Thanks for using this program!!!";
            exit(1);
        default:
            cout << "Wrong choice!!!" << endl;
        }
    }
    return 0;
}
```
## 7
```cpp
#include <iostream> 
using namespace std; 

struct tree 
{ 
tree *l, *r; 
int data; 
}*root = NULL, *p = NULL, *np = NULL, *q; 
void create() 
{ 
int value,c = 0;  
while (c < 7) 
{ 
if (root == NULL) 
{ 
root = new tree; 
cout<<"enter value of root node\n"; 
cin>>root->data; 
root->r=NULL; 
root->l=NULL; 
} 
else 
{ 
p = root; 
cout<<"enter value of node\n"; 
cin>>value; 
while(true) 
{ 
if (value < p->data) 
{ 
if (p->l == NULL) 
{ 
p->l = new tree; 
p = p->l; 
p->data = value; 
p->l = NULL; 
p->r = NULL; 
cout<<"value entered in left\n"; 
break; 
} 
else if (p->l != NULL) 
{ 
p = p->l; 
} 
} 
else if (value > p->data) 
{ 
if (p->r == NULL) 
{ 
p->r = new tree; 
p = p->r; 
p->data = value;
p->l = NULL; 
p->r = NULL; 
cout<<"value entered in right\n"; 
break; 
} 
else if (p->r != NULL) 
{ 
p = p->r; 
} 
} 
} 
} 
c++; 
} 
} 
void inorder(tree *p) 
{ 
if (p != NULL) 
{ 
inorder(p->l); 
cout<<p->data<<endl; 
inorder(p->r); 
} 
} 
void preorder(tree *p) 
{ 
if (p != NULL) 
{ 
cout<<p->data<<endl; 
preorder(p->l); 
preorder(p->r); 
} 
} 
void postorder(tree *p) 
{ 
if (p != NULL) 
{ 
postorder(p->l); 
postorder(p->r); 
cout<<p->data<<endl; 
} 
} 
int main() 
{ 
create(); 
cout<<"printing traversal in inorder\n"; 
inorder(root); 
cout<<"printing traversal in preorder\n"; 
preorder(root); 
cout<<"printing traversal in postorder\n"; 
postorder(root); 

}
```

## 8
```cpp
#include <iostream>
using namespace std;
struct Node {
int data;
Node* left;
Node* right;
Node(int val) {
data = val;
left = nullptr;
right = nullptr;
}
};
class BST {
private:
Node* root;
Node* insertUtil(Node* root, int val) {
if (root == nullptr) {
return new Node(val);
}
if (val < root->data) {
root->left = insertUtil(root->left, val);
} else if (val > root->data) {
root->right = insertUtil(root->right, val);
}
return root;
}
int longestPathUtil(Node* root) {
if (root == nullptr) {
return 0;
}
int leftDepth = longestPathUtil(root->left);
int rightDepth = longestPathUtil(root->right);
return 1 + max(leftDepth, rightDepth);
}
int findMinUtil(Node* root) {
if (root == nullptr) {
cout << "Tree is empty." << endl;
return -1; // Return some default value indicating empty tree
}
while (root->left != nullptr) {
root = root->left;
}
return root->data;
}
Node* swapPointersUtil(Node* root) {
if (root == nullptr) {
return nullptr;
}
Node* temp = root->left;
root->left = root->right;
root->right = temp;
swapPointersUtil(root->left);
swapPointersUtil(root->right);
return root;
}
Node* searchUtil(Node* root, int val) {
if (root == nullptr || root->data == val) {
return root;
}
if (val < root->data) {
return searchUtil(root->left, val);
} else {
return searchUtil(root->right, val);
}
}
public:
BST() {
root = nullptr;
}
void insert(int val) {
root = insertUtil(root, val);
}
int longestPath() {
return longestPathUtil(root);
}
int findMin() {
return findMinUtil(root);
}
void swapPointers() {
root = swapPointersUtil(root);
}
bool search(int val) {
Node* result = searchUtil(root, val);
return result != nullptr;
}
};
int main() {
BST tree;
// Inserting values into the BST
int values[] = {5, 3, 7, 1, 4, 6, 9};
int numValues = sizeof(values) / sizeof(values[0]);
for (int i = 0; i < numValues; i++) {
tree.insert(values[i]);
}
// Example usage of BST functionalities
cout << "Longest path in the tree: " << tree.longestPath() << endl;
cout << "Minimum value in the tree: " << tree.findMin() << endl;
cout << "Swapping left and right pointers at every node..." << endl;
tree.swapPointers();
int searchVal = 6;
cout << "Searching for value " << searchVal << ": ";
if (tree.search(searchVal)) {
cout << "Found!" << endl;
} else {
cout << "Not Found!" << endl;
}
return 0;
}
```
## 9
```cpp
#include <iostream> 
#include <vector> 
#include <queue> 
using namespace std; 
class Graph { 
private: 
int V; 
vector<vector<int>> adjList; 
public: 
Graph(int vertices) { 
V = vertices; 
adjList.resize(V); 
} 
void addEdge(int src, int dest) { 
adjList[src].push_back(dest); 
} 
 void DFS(int start) { 
vector<bool> visited(V, false); 
DFSUtil(start, visited); 
} 
void DFSUtil(int vertex, vector<bool>& visited) { visited[vertex] = true; 
cout << vertex << " "; 
for (int i = 0; i < adjList[vertex].size(); ++i) { int adjVertex = adjList[vertex][i]; 
if (!visited[adjVertex]) { 
DFSUtil(adjVertex, visited); 
} 
} 
} 
 void BFS(int start) { 
vector<bool> visited(V, false); 
queue<int> queue; 
visited[start] = true; 
queue.push(start); 
while (!queue.empty()) { 
int current = queue.front(); 
cout << current << " "; 
queue.pop(); 
for (int i = 0; i < adjList[current].size(); ++i) { int adjVertex = adjList[current][i]; 
if (!visited[adjVertex]) { 
visited[adjVertex] = true;
queue.push(adjVertex); 
} 
} 
} 
} 
}; 
int main() { 
int V, E; 
cout << "Enter the number of vertices: "; 
cin >> V; 
cout << "Enter the number of edges: "; 
cin >> E; 
Graph graph(V); 
cout << "Enter " << E << " edges (format: source destination):" << endl; for (int i = 0; i < E; ++i) { 
int src, dest; 
cin >> src >> dest; 
graph.addEdge(src, dest); 
} 
int startVertex; 
cout << "Enter the starting vertex for traversal: "; 
cin >> startVertex; 
cout << "DFS traversal starting from vertex " << startVertex << ": "; graph.DFS(startVertex); 
cout << endl; 
cout << "BFS traversal starting from vertex " << startVertex << ": "; graph.BFS(startVertex); 
cout << endl; 
return 0; 
}
```
## 10
```cpp
#include <iostream> 
#include <vector> 
#include <algorithm> 
using namespace std; 
struct Edge { 
int src, dest, weight; 
}; 
class Graph { 
private: 
int V; 
vector<Edge> edges; 
public: 
Graph(int vertices) : V(vertices) {} 
void addEdge(int src, int dest, int weight) { 
Edge edge; 
edge.src = src; 
edge.dest = dest; 
edge.weight = weight; 
edges.push_back(edge); 
} 
int find(vector<int>& parent, int i) { 
if (parent[i] == -1) 
return i; 
return find(parent, parent[i]); 
} 
void unionSet(vector<int>& parent, int x, int y) { 
int xroot = find(parent, x); 
int yroot = find(parent, y); 
parent[xroot] = yroot; 
} 
void kruskalMST() { 
vector<Edge> result(V - 1); 
sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) { return a.weight < b.weight; 
}); 
vector<int> parent(V, -1); 
int e = 0; 
int i = 0; 
while (e < V - 1 && i < edges.size()) { 
Edge next_edge = edges[i++]; 
int x = find(parent, next_edge.src); 
int y = find(parent, next_edge.dest); 
if (x != y) {
result[e++] = next_edge; 
unionSet(parent, x, y); 
} 
} 
cout << "Minimum Spanning Tree formed by connecting offices with minimum  cost:" << endl; 
for (int j = 0; j < V - 1; ++j) { 
cout << result[j].src << " - " << result[j].dest << " : " << 
result[j].weight << endl; 
} 
} 
}; 
int main() { 
int numOffices, numConnections; 
cout << "Enter the number of offices: "; 
cin >> numOffices; 
cout << "Enter the number of connections: "; 
cin >> numConnections; 
Graph graph(numOffices); 
cout << "Enter " << numConnections << " connections in the format: src dest cost" << endl; 
for (int i = 0; i < numConnections; ++i) { 
int src, dest, cost; 
cin >> src >> dest >> cost; 
graph.addEdge(src, dest, cost); 
} 
graph.kruskalMST(); 
return 0; 
}
```
