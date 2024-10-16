       #include <stdio.h>
       #include <stdlib.h>
       #include <string.h>


          typedef struct {
          char jobName[20];
          char jobDescription[100];
         int jobPriority;
         } Job;


       typedef struct {
          char name[20];
          int id;
          char skills[20];
       } Person;

       typedef struct {
       Job* jobs;
       int front;
       int rear;
       int size;
      } Queue;

       Queue* createQueue(int size) {
       Queue* q = (Queue*)malloc(sizeof(Queue));
      q->jobs = (Job*)malloc(size * sizeof(Job));
      q->front = 0;
      q->rear = 0;
      q->size = size;
      return q;
        }


      void enqueue(Queue* q, Job job) {
        if ((q->rear + 1) % q->size == q->front) {
        printf("Queue is full. Cannot add more jobs.\n");
        return;
      }
      q->jobs[q->rear] = job;
      q->rear = (q->rear + 1) % q->size;
      }
       Job dequeue(Queue* q) {
          }

        void assignTasks(Queue* jobQueue, Person person) {
        Job job;
        int i = jobQueue->front;
        while (i != jobQueue->rear) {
        job = jobQueue->jobs[i];
        if (strstr(job.jobDescription, person.skills) != NULL) {
            printf("%s is assigned to %s.\n", person.name, job.jobName);
        }
        i = (i + 1) % jobQueue->size;
    }
     }

    int main() {
    int numJobs;
    printf("Enter the number of jobs: ");
    scanf("%d", &numJobs);

    Queue* jobQueue = createQueue(numJobs);

    Job job;
    int choice;
    while (1) {
        printf("1. Add job\n");
        printf("2. Assign tasks\n");
        printf("3. Print queue\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter job name: ");
                scanf("%s", job.jobName);
                printf("Enter job description: ");
                scanf("%s", job.jobDescription);
                printf("Enter job priority (1: high, 2: medium, 3: low): ");
                scanf("%d", &job.jobPriority);
                enqueue(jobQueue, job);
                break;
            case 2:
				{

                Person person;
                printf("Enter person's name: ");
                scanf("%s", person.name);
                printf("Enter person's ID: ");
                scanf("%d", &person.id);
                printf("Enter person's skills: ");
                scanf("%s", person.skills);
                assignTasks(jobQueue, person);
				}

                break;
            case 3:
                printQueue(jobQueue);
                break;
            case 4:
                return 0;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }
}
