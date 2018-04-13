/* SUNIL KUMAR SAINI
SEC=K1624B53
REG =11607798
QUESTION NUMBER = 2
*/

#include<stdio.h>
#include<conio.h>
#include<math.h>

struct times
{
       int p,arrival_time,brust_time,wating_time,trun_around_time,rnt;
      
};


void sortarrival_time(struct times a[],int n)
{
       int i,j;
       struct times temp;
       for(i=0;i<n;i++)
       {
              for(j=i+1;j<n;j++)
              {
                     if(a[i].arrival_time > a[j].arrival_time)
                     {
                           temp = a[i];
                           a[i] = a[j];
                           a[j] = temp;
                     }
              }
       }
       return;
}

int main()
{
       int i,j,n,time,remain,flag=0,ts;
       struct times a[100];
       float avgwt=0,average_time=0;
       printf("\n WELCOME IN PROGRAMM");
       printf("Round Robin Scheduling Algorithm\n");
       printf("Enter Number Of Processes : ");
       scanf("%d",&n);
       remain=n;
       for(i=0;i<n;i++)
       {
              printf("Enter arrival time and Burst time for Process P%d : ",i);
              scanf("%d%d",&a[i].arrival_time,&a[i].brust_time);
              a[i].p = i;
              a[i].rnt = a[i].brust_time;
       }
       sortarrival_time(a,n);
       printf("Enter Time Slice OR Quantum Number : ");
       scanf("%d",&ts);
       printf("\n*************************\n");
       printf("Gantt Charrival_time\n");
       printf("0");
       for(time=0,i=0;remain!=0;)
       {
              if(a[i].rnt<=ts && a[i].rnt>0)
              {
                     time = time + a[i].rnt;
                     printf(" -> [P%d] <- %d",a[i].p,time);
                     a[i].rnt=0;
                     flag=1;
              }
              else if(a[i].rnt > 0)
              {
                     a[i].rnt = a[i].rnt - ts;
                     time = time + ts;
                     printf(" -> [P%d] <- %d",a[i].p,time);
              }
              if(a[i].rnt==0 && flag==1)
              {
                     remain--;
                     a[i].trun_around_time = time-a[i].arrival_time;
                     a[i].wating_time = time-a[i].arrival_time-a[i].brust_time;
                     avgwt = avgwt + time-a[i].arrival_time-a[i].brust_time;
                     average_time = average_time + time-a[i].arrival_time;
                     flag=0;
              }
              if(i==n-1)
                     i=0;
              else if(a[i+1].arrival_time <= time)
                     i++;
              else
                     i=0;
       }
       printf("\n\n");
       
       printf("Pro\tArrival_timei\tBrust_timei\tTrun_around_timei\tWating_timei\n");
       
       for(i=0;i<n;i++)
       {
              printf("P%d\t%d\t%d\t%d\t%d\n",a[i].p,a[i].arrival_time,a[i].brust_time,a[i].trun_around_time,a[i].wating_time);
       }
       printf("@@@%%%%%%$$$$$$*****!!!!!!!\n");
       avgwt = avgwt/n;
       average_time = average_time/n;
       printf("Average Waiting Time : %.2f\n",avgwt);
       printf("Average Turnaround Time : %.2f\n",average_time);
       printf("\nTHANKS YOU FOR THIS TASK");
       return 0;
}
