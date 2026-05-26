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



#include <stdio.h>

// ---------- QUICK SORT ----------

// Swap function
void swap(int arr[], int i, int j) {

    int temp;

    temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

// Partition function
int partition(int arr[], int low, int high) {

    int pivot = arr[high];

    int i = low - 1;

    for(int j = low; j < high; j++) {

        if(arr[j] < pivot) {

            i++;

            swap(arr, i, j);
        }
    }

    swap(arr, i + 1, high);

    return i + 1;
}

// Quick Sort function
void quickSort(int arr[], int low, int high) {

    if(low < high) {

        int pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);

        quickSort(arr, pi + 1, high);
    }
}

// ---------- MERGE SORT ----------

// Merge function
void merge(int arr[], int left, int mid, int right) {

    int n1 = mid - left + 1;

    int n2 = right - mid;

    int L[n1], R[n2];

    // Copy elements into temporary arrays
    for(int i = 0; i < n1; i++) {

        L[i] = arr[left + i];
    }

    for(int j = 0; j < n2; j++) {

        R[j] = arr[mid + 1 + j];
    }

    int i = 0;
    int j = 0;
    int k = left;

    // Merge arrays
    while(i < n1 && j < n2) {

        if(L[i] <= R[j]) {

            arr[k] = L[i];
            i++;
        }

        else {

            arr[k] = R[j];
            j++;
        }

        k++;
    }

    // Remaining elements of L[]
    while(i < n1) {

        arr[k] = L[i];
        i++;
        k++;
    }

    // Remaining elements of R[]
    while(j < n2) {

        arr[k] = R[j];
        j++;
        k++;
    }
}

// Merge Sort function
void mergeSort(int arr[], int left, int right) {

    if(left < right) {

        int mid = (left + right) / 2;

        mergeSort(arr, left, mid);

        mergeSort(arr, mid + 1, right);

        merge(arr, left, mid, right);
    }
}

// ---------- DISPLAY FUNCTION ----------

void display(int arr[], int n) {

    for(int i = 0; i < n; i++) {

        printf("%d ", arr[i]);
    }

    printf("\n");
}

// ---------- MAIN FUNCTION ----------

int main() {

    int n;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    int arr1[n], arr2[n];

    printf("Enter elements:\n");

    for(int i = 0; i < n; i++) {

        scanf("%d", &arr1[i]);

        arr2[i] = arr1[i];
    }

    // Quick Sort
    quickSort(arr1, 0, n - 1);

    printf("\nArray after Quick Sort:\n");

    display(arr1, n);

    // Merge Sort
    mergeSort(arr2, 0, n - 1);

    printf("\nArray after Merge Sort:\n");

    display(arr2, n);

    return 0;
}
