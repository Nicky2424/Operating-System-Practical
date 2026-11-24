# Practical 3: Advanced Linux Commands

## Aim
To study Linux commands related to process control, communication and file protection.

## Theory
Linux provides commands to manage processes, communicate with users and control file permissions.

## Commands

### 1. ps
Displays currently running processes.
```bash
ps
```

### 2. ps -ef
Displays all running processes.
```bash
ps -ef
```

### 3. kill
Terminates a process using its process ID (PID). Only use it on a process you own and have permission to stop.
```bash
kill PID
```

### 4. chmod
Changes file permissions.
```bash
chmod 644 sample.txt
```

### 5. write
Sends a message to another logged-in user (where supported).
```bash
write username
```

### 6. mesg
Controls whether other users can send messages to your terminal.
```bash



# Practical 4: Process Creation using fork() and exec()

## Aim
To study process creation using fork() and execution using exec() system calls.

## Theory
- fork(): Creates a new child process.
- exec(): Replaces the current process with a new program.
- getpid(): Returns the process ID.
- getppid(): Returns the parent process ID.

## Program (C)

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main()
{
    pid_t pid = fork();

    if (pid < 0)
    {
        printf("Fork failed\n");
    }
    else if (pid == 0)
    {
        printf("Child Process\n");
        printf("Child PID: %d\n", getpid());
        execlp("ls", "ls", NULL);
    }
    else
    {
        wait(NULL);
        printf("Parent Process\n");
        printf("Parent PID: %d\n", getpid());
    }

    return 0;
}
```

## Result
Successfully studied process creation using fork() and program execution using exec().





# Practical 5: Kernel Version and CPU Information

## Aim
To display Linux kernel version and CPU information.

## Commands

### 1. uname
Displays system information.
```bash
uname
```

### 2. uname -a
Displays complete system information.
```bash
uname -a
```

### 3. uname -r
Displays kernel version.
```bash
uname -r
```

### 4. lscpu
Displays CPU information.
```bash
lscpu
```

### 5. cat /proc/cpuinfo
Displays detailed CPU information.
```bash
cat /proc/cpuinfo
```

## Result
Successfully studied Linux kernel version and CPU information.






# Practical 6: Memory Information in Linux

## Aim
To display memory information in a Linux system.

## Commands

### 1. free
Displays memory usage.
```bash
free
```

### 2. free -h
Displays memory usage in human-readable format.
```bash
free -h
```

### 3. cat /proc/meminfo
Displays detailed memory information.
```bash
cat /proc/meminfo
```

### 4. top
Displays running processes and memory usage.
```bash
top
```

### 5. vmstat
Displays virtual memory statistics.
```bash
vmstat
```

## Result
Successfully studied memory information and memory usage in Linux.






# Practical 7: File Copying using open(), read(), write() and close()

## Aim
To write a C program to copy the contents of one file into another using system calls.

## Theory
- open(): Opens a file.
- read(): Reads data from a file.
- write(): Writes data into a file.
- close(): Closes a file.

## Program (C)

```c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main()
{
    int source, destination;
    char buffer[100];
    int n;

    source = open("input.txt", O_RDONLY);

    if (source < 0)
    {
        printf("Unable to open source file\n");
        return 1;
    }

    destination = open("output.txt",
        O_WRONLY | O_CREAT | O_TRUNC, 0644);

    if (destination < 0)
    {
        printf("Unable to create destination file\n");
        close(source);
        return 1;
    }

    while ((n = read(source, buffer, sizeof(buffer))) > 0)
    {
        write(destination, buffer, n);
    }

    close(source);
    close(destination);

    printf("File copied successfully\n");

    return 0;
}
```

## Result
Successfully copied file contents using Linux system calls.





# Practical 8: First Come First Serve (FCFS) Scheduling

## Aim
To implement the FCFS CPU scheduling algorithm.

## Theory
FCFS is a non-preemptive CPU scheduling algorithm. The process that arrives first gets the CPU first.

## Program (C)

```c
#include <stdio.h>

int main()
{
    int n, bt[20], wt[20], tat[20];
    float avgwt = 0, avgtat = 0;

    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++)
    {
        printf("Enter burst time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
    }

    wt[0] = 0;

    for (int i = 1; i < n; i++)
        wt[i] = wt[i - 1] + bt[i - 1];

    for (int i = 0; i < n; i++)
    {
        tat[i] = wt[i] + bt[i];
        avgwt += wt[i];
        avgtat += tat[i];
    }

    printf("\nProcess\tBT\tWT\tTAT\n");

    for (int i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t%d\n",
               i + 1, bt[i], wt[i], tat[i]);

    printf("Average Waiting Time = %.2f\n", avgwt / n);
    printf("Average Turnaround Time = %.2f\n", avgtat / n);

    return 0;
}
```

## Result
Successfully implemented FCFS CPU scheduling.







# Practical 9: Shortest Job First (SJF) Scheduling

## Aim
To implement non-preemptive SJF CPU scheduling.

## Theory
SJF selects the process having the smallest burst time first.

## Program (C)

```c
#include <stdio.h>

int main()
{
    int n, bt[20], p[20], wt[20], tat[20];
    float avgwt = 0, avgtat = 0;

    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++)
    {
        p[i] = i + 1;
        printf("Enter burst time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
    }

    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            if (bt[i] > bt[j])
            {
                int temp = bt[i];
                bt[i] = bt[j];
                bt[j] = temp;

                temp = p[i];
                p[i] = p[j];
                p[j] = temp;
            }
        }
    }

    wt[0] = 0;

    for (int i = 1; i < n; i++)
        wt[i] = wt[i - 1] + bt[i - 1];

    for (int i = 0; i < n; i++)
    {
        tat[i] = wt[i] + bt[i];
        avgwt += wt[i];
        avgtat += tat[i];
    }

    printf("\nProcess\tBT\tWT\tTAT\n");

    for (int i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t%d\n",
               p[i], bt[i], wt[i], tat[i]);

    printf("Average WT = %.2f\n", avgwt / n);
    printf("Average TAT = %.2f\n", avgtat / n);

    return 0;
}
```

## Result
Successfully implemented non-preemptive SJF scheduling.





# Practical 10: Priority CPU Scheduling

## Aim
To implement non-preemptive Priority CPU scheduling.

## Theory
Priority scheduling assigns a priority to each process. The process with the highest priority is executed first. In this program, a smaller priority number represents higher priority.

## Program (C)

```c
#include <stdio.h>

int main()
{
    int n, bt[20], p[20], pr[20], wt[20], tat[20];
    float avgwt = 0, avgtat = 0;

    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++)
    {
        p[i] = i + 1;

        printf("Enter burst time for P%d: ", i + 1);
        scanf("%d", &bt[i]);

        printf("Enter priority for P%d: ", i + 1);
        scanf("%d", &pr[i]);
    }

    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            if (pr[i] > pr[j])
            {
                int temp = pr[i];
                pr[i] = pr[j];
                pr[j] = temp;

                temp = bt[i];
                bt[i] = bt[j];
                bt[j] = temp;

                temp = p[i];
                p[i] = p[j];
                p[j] = temp;
            }
        }
    }

    wt[0] = 0;

    for (int i = 1; i < n; i++)
        wt[i] = wt[i - 1] + bt[i - 1];

    for (int i = 0; i < n; i++)
    {
        tat[i] = wt[i] + bt[i];
        avgwt += wt[i];
        avgtat += tat[i];
    }

    printf("\nProcess\tBT\tPriority\tWT\tTAT\n");

    for (int i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t\t%d\t%d\n",
               p[i], bt[i], pr[i], wt[i], tat[i]);

    printf("Average WT = %.2f\n", avgwt / n);
    printf("Average TAT = %.2f\n", avgtat / n);

    return 0;
}
```

## Result
Successfully implemented non-preemptive Priority scheduling.





# Practical 11: Sum of N Numbers using Pthreads

## Aim
To calculate the sum of N numbers using POSIX threads (Pthreads).

## Theory
Pthreads is a library used to create and manage threads in a program.

A thread is a small unit of execution within a process.

## Program (C)

```c
#include <stdio.h>
#include <pthread.h>

int n;
int sum = 0;

void *calculate_sum(void *arg)
{
    for (int i = 1; i <= n; i++)
        sum += i;

    return NULL;
}

int main()
{
    pthread_t thread;

    printf("Enter N: ");
    scanf("%d", &n);

    pthread_create(&thread, NULL, calculate_sum, NULL);

    pthread_join(thread, NULL);

    printf("Sum = %d\n", sum);

    return 0;
}
```

## Compilation
```bash
gcc practical11.c -o practical11 -pthread
```

## Execution
```bash
./practical11
```

## Result
Successfully calculated the sum of N numbers using Pthreads.






# Practical 12: Memory Allocation Algorithms

## Aim
To implement First Fit, Best Fit and Worst Fit memory allocation algorithms.

## Theory

1. First Fit: Allocates the first memory block that is large enough.
2. Best Fit: Allocates the smallest suitable memory block.
3. Worst Fit: Allocates the largest available memory block.

## Program (C)

```c
#include <stdio.h>

void firstFit(int block[], int m, int process[], int n)
{
    int allocation[20];

    for (int i = 0; i < n; i++)
        allocation[i] = -1;

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (block[j] >= process[i])
            {
                allocation[i] = j;
                block[j] -= process[i];
                break;
            }
        }
    }

    printf("\nFirst Fit:\n");
    for (int i = 0; i < n; i++)
        printf("P%d -> %s\n", i + 1,
               allocation[i] == -1 ? "Not Allocated" : "Allocated");
}

void bestFit(int block[], int m, int process[], int n)
{
    int allocation[20];

    for (int i = 0; i < n; i++)
        allocation[i] = -1;

    for (int i = 0; i < n; i++)
    {
        int best = -1;

        for (int j = 0; j < m; j++)
        {
            if (block[j] >= process[i] &&
                (best == -1 || block[j] < block[best]))
                best = j;
        }

        if (best != -1)
        {
            allocation[i] = best;
            block[best] -= process[i];
        }
    }

    printf("\nBest Fit:\n");
    for (int i = 0; i < n; i++)
        printf("P%d -> %s\n", i + 1,
               allocation[i] == -1 ? "Not Allocated" : "Allocated");
}

void worstFit(int block[], int m, int process[], int n)
{
    int allocation[20];

    for (int i = 0; i < n; i++)
        allocation[i] = -1;

    for (int i = 0; i < n; i++)
    {
        int worst = -1;

        for (int j = 0; j < m; j++)
        {
            if (block[j] >= process[i] &&
                (worst == -1 || block[j] > block[worst]))
                worst = j;
        }

        if (worst != -1)
        {
            allocation[i] = worst;
            block[worst] -= process[i];
        }
    }

    printf("\nWorst Fit:\n");
    for (int i = 0; i < n; i++)
        printf("P%d -> %s\n", i + 1,
               allocation[i] == -1 ? "Not Allocated" : "Allocated");
}

int main()
{
    int m, n;
    int original[20], process[20], blocks[20];

    printf("Enter number of memory blocks: ");
    scanf("%d", &m);

    for (int i = 0; i < m; i++)
    {
        printf("Enter block size: ");
        scanf("%d", &original[i]);
    }

    printf("Enter number of processes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++)
    {
        printf("Enter process size: ");
        scanf("%d", &process[i]);
    }

    for (int i = 0; i < m; i++)
        blocks[i] = original[i];
    firstFit(blocks, m, process, n);

    for (int i = 0; i < m; i++)
        blocks[i] = original[i];
    bestFit(blocks, m, process, n);

    for (int i = 0; i < m; i++)
        blocks[i] = original[i];
    worstFit(blocks, m, process, n);

    return 0;
}
```

## Result
Successfully implemented First Fit, Best Fit and Worst Fit memory allocation algorithms.






mesg
```

### 7. tty
Displays the terminal name.
```bash
tty
```

## Result
Studied Linux commands used for process management, communication and file protection.
