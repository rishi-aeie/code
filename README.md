#include <stdio.h>

#define MAX 10

// Queue for BFS
int queue[MAX];
int front = -1;
int rear = -1;

// Stack for DFS
int stack[MAX];
int top = -1;

// ---------- QUEUE FUNCTIONS ----------

// Enqueue function
void enqueue(int value) {

    if(rear == MAX - 1)
        return;

    if(front == -1)
        front = 0;

    queue[++rear] = value;
}

// Dequeue function
int dequeue() {

    if(front == -1 || front > rear)
        return -1;

    return queue[front++];
}

// ---------- STACK FUNCTIONS ----------

// Push function
void push(int value) {

    if(top == MAX - 1)
        return;

    stack[++top] = value;
}

// Pop function
int pop() {

    if(top == -1)
        return -1;

    return stack[top--];
}

// ---------- BFS FUNCTION ----------

void BFS(int graph[MAX][MAX], int vertices, int start) {

    int visited[MAX] = {0};

    int node;

    front = rear = -1;

    visited[start] = 1;

    enqueue(start);

    printf("BFS Traversal: ");

    while(front <= rear) {

        node = dequeue();

        printf("%d ", node);

        for(int i = 0; i < vertices; i++) {

            if(graph[node][i] == 1 && visited[i] == 0) {

                visited[i] = 1;

                enqueue(i);
            }
        }
    }

    printf("\n");
}

// ---------- DFS FUNCTION ----------

void DFS(int graph[MAX][MAX], int vertices, int start) {

    int visited[MAX] = {0};

    int node;

    top = -1;

    push(start);

    printf("DFS Traversal: ");

    while(top != -1) {

        node = pop();

        if(visited[node] == 0) {

            visited[node] = 1;

            printf("%d ", node);

            for(int i = vertices - 1; i >= 0; i--) {

                if(graph[node][i] == 1 && visited[i] == 0) {

                    push(i);
                }
            }
        }
    }

    printf("\n");
}

// ---------- MAIN FUNCTION ----------

int main() {

    int vertices;

    int graph[MAX][MAX];

    printf("Enter number of vertices: ");
    scanf("%d", &vertices);

    printf("Enter adjacency matrix:\n");

    for(int i = 0; i < vertices; i++) {

        for(int j = 0; j < vertices; j++) {

            scanf("%d", &graph[i][j]);
        }
    }

    BFS(graph, vertices, 0);

    DFS(graph, vertices, 0);

    return 0;
}
