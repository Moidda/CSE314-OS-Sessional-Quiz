# Pthread
Declaring pthread
```c
pthread_t thread1;
pthread_t thread2;
```

Creating/initializing pthread
```c
void* foo(void* args) {
    int* id = (int*)args;                  // convert from void* to int* 
    printf("Inside thread %d\n", (*id));   // print value of id
}

int *args1, *args2;
*args1 = 1;         // value of args1 is 1
*args2 = 2;         // value of args2 is 2
pthread_create(&thread1, NULL, foo, (void*)args1)
pthread_create(&thread2, NULL, foo, (void*)args2)
```

```pthread_join(&thrd, status)``` blocks the calling thread until the specified thread ```thrd``` terminates
```c
pthread_join(thread1, NULL);
pthread_join(thread2, NULL);
```

The same can be done with ```pthread_exit(status)```
```c
pthread_exit(0);
```

The second argument of ```pthread_create()``` is for defining thread attribute. Thread attributes are defined using ```pthread_attr_t```
```c
pthread_attr_t ta;
pthread_attr_init(&ta);
pthread_attr_setschedpolicy(&ta, SCHED_RR);     // round robin scheduling

pthread_t thrd;
pthread_create(&thrd, &ta, foo, (void*)args);
```


# Semaphore
Declaring semaphore
```c
#include <semaphore.h>
sem_t empty_count
```
Counting semaphore initialized to 5
```c
sem_init(&empty_count, 0, 5);
```
Decrease semaphore by 1. \
Waits/blocks if cannot decrease
```c
sem_wait(&empty_count)
```
Increase semaphore by 1
```c
sem_post(&empty_count)
```

# Mutex
Declaration
```c
pthread_mutext_t mtx;
```
Initialization
```c
pthread_mutex_init(&mtx, NULL);
```
Lock unlock
```c
pthread_mutex_lock(&mtx)
// critical region
pthread_mutex_unlock(&mtx)
```
```pthread_mutex_unlock(&mtx)``` raises error if 
- mtx is already unlocked
- mtx is owned by another thread