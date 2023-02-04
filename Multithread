#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>

pthread_t philosopher[5];
pthread_mutex_t chopstick[5];

void *func(int n)
{
    printf("\nPhilosopher % d is thinking.", n);
    pthread_mutex_lock(&chopstick[n]);
    pthread_mutex_lock(&chopstick[(n + 1) % 5]);

    printf("\nPhilosopher % d is eating.", n);

    sleep(3);
    pthread_mutex_unlock(&chopstick[n]);
    pthread_mutex_unlock(&chopstick[(n + 1) % 5]);
    printf("\nPhilosopher % d Finished eating ", n);
}

int main()
{
    int i, k;
    void *message;
    for (i = 1; i <= 5; i++)
    {
        k = pthread_mutex_init(&chopstick[i], NULL);
        if (k == -1)
        {
            printf("Failed to initialize the mutex\n");
            exit(1);
        }
    }
    for (i = 1; i <= 5; i++)
    {
        k = pthread_create(&philosopher[i], NULL, (void *)func, (int *)i);
        if (k != 0)
        {
            printf("Error in thread creation.\n");
            exit(1);
        }
    }
    for (i = 1; i <= 5; i++)
    {
        k = pthread_join(philosopher[i], &message);
        if (k != 0)
        {
            printf("Failed to join the thread.\n");
            exit(1);
        }
    }
    for (i = 1; i <= 5; i++)
    {
        k = pthread_mutex_destroy(&chopstick[i]);
        if (k != 0)
        {
            printf("Mutex destroyed.\n");
            exit(1);
        }
    }
    return 0;
}
