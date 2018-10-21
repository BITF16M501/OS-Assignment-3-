# OS-Assignment-3-
Create an array of 1000 and make 10 thread .......
#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
int label=-100;
int array[1000];
int totalsum=0;
void *Sum(void * args){
int start= (int)args;
int end=start+100;
int sum=0;
for(int i=start;i<end;i++)
sum+=array[i];
return ((void *)sum);
}
int main()
{
for(int i=0;i<1000;i++)
array[i]=i;
int status_t[10];
pthread_t thread_arr[10];
for(int i=0;i<10;i++)
pthread_create(&thread_arr[i],NULL,Sum,(void *)(array[i*100]));
for(int i=0;i<10;i++)
pthread_join(thread_arr[i],(void **)& status_t[i]);
for(int i=0;i<10;i++)
totalsum+=status_t[i];
printf("\nTotal sum of 1000 numbers by 10 threads %d\n",totalsum);
return 0;
}
