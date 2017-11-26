# Event-Calendar-in-C

#include <stdio.h> 
#include<stdlib.h> 
#include <string.h> 
char* months[] = {"Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec","Jan","Feb"}; 
char* month[] = {"mar","apr","may","jun","jul","aug","sep","oct","nov","dec","jan","feb"}; 
char* days[]= { "sunday","monday", "tuesday", "wednesday", "thursday", "friday", "saturday" }; 
int Day(int date,int month,int year); 
void eventadd();
void eventview();
void eventedit();

main() 
{
 int k,m,year,i,j,flag=0,count=0,dates,input; 
 char str[3],day[100]; 
 printf("\t\t\tDigital Event Calender\n\n");
 printf("\nEnter first 3 alphabets of month of the year ex:-for January enter Jan\n"); 
 scanf("%s",str); 
 for(i=0; i<12; i++) 
 { 
 if(!strcmp(str,months[i]) || !strcmp(str,month[i])) 
 {
  m=i+1;
  flag=1; 
  break; }
   }
    if(flag==0)
	 { 
	 printf("Invalid Month\n"); 
	 exit(0);
	  }
 printf("\nEnter year between 1500 to 3000\n");
 scanf("%d",&year);
 for(j=0; j<1; j++){
 if(year>=1500 && year<=3000) 
 {
  count=1; 
  break; }
   }
    if(count==0)
	 { 
	 printf("Invalid year\n"); 
	 exit(0);
	  }
	
  if(m==1 || m==3 || m==5 || m==6 || m==8 || m==10 || m==11)
   { dates=31; } 
  if(m==2 || m==4 || m==7 || m==9)
   { dates=30; }
  if(m==12) 
  { if(year%400==0||year%4==0)
   { dates=29; }
    else 
	{ dates=28; }
	 }
  printf("\n");
  printf(" Sunday Monday  Tuesday  Wednesday  Thursday  Friday  Saturday \n");
  for(i=1;i<=dates;i++)
   { int finalday=Day(i,m,year);
    if(finalday==0) 
	printf("%4d",i); 
	if(finalday==1) 
	{ if(i!=1)
	  printf("%8d",i);
	  else printf("%12d",i);
	   }
	if(finalday==2)
	 { if(i!=1)
	   printf("%8d",i);
	   else printf("%20d",i);
	    }
    if(finalday==3)
	 { if(i!=1)
	    printf("%9d",i);
	   else
	    printf("%29d",i);
		 }
	if(finalday==4)
	 { if(i!=1)
	    printf("%11d",i); 
	   else 
	    printf("%40d",i);
		 }
	if(finalday==5)
	 { if(i!=1)
	    printf("%10d",i);
	   else
	    printf("%50d",i);
		 }
	if(finalday==6)
	 { if(i!=1)
	    printf("%8d\n",i);
	   else 
	    printf("%58d\n",i);
		 }
		  }
	printf("\n");
	
	printf("\nEnter the following from given options:");
	printf("\n");
	puts("\n+-------- Manage Events ----------+\n"
        "|  1. To Add New Event          |\n"
        "|  2. To View an Event          |\n"
        "|  3. To Add In a Saved Event   |\n"
        "|  4. To Overwright an Event    |\n"
        "|  5. Exit                      |\n"
        "+---------------------------------+\n");
    scanf("%d", &input);
    if(input==1){
    	eventadd();

	}
	if(input==2){
		eventview();
	}
	if(input==3){
		eventedit();
	}
	if(input==4){
    	eventadd();
	}
	if(input==5){
		exit(5);
		}
    
	 }
	 
//for determining the day and date allingment.
	int Day(int k,int m,int year)
	{
	  int D,C,i,f,finalday,flag=0;
	  char day[100];
	  if(k<=0||k>31) 
	  { printf("Invalid Date\n");
	   exit(0); }
	  if(m==11||m==12)
	   { year=year-1; }
	  D=year%100;
	  C=year/100; 
	  f = (k+(((13*m)-1)/5)+D+(D/4)+(C/4))-(2*C); 
	  if(f>=0)
	   { finalday=f%7; } 
	  else
	   { finalday=((f%7)+7)%7; } 
	return(finalday);
	 }
	 
//for adding an event on a specific date.
	void eventadd(){
	FILE *efile;
	char c,file[14];
	printf("Enter the date from the above calendar: (Ex:dd.mm.yyyy.txt)\n");
	scanf("%s", &file);
	printf("\nEnter event description:\n\n");
	efile=fopen(file,"w");
	while(c!='.'){
		c=getche();
		fputc(c,efile);
	}
	fclose(efile);
	puts("\n| Event successfully added.|\n");
}

//for viewing an event on a specific date.
	void eventview(){
	FILE *efile;
	char ch,file[14];
	printf("Enter the date from the above calendar: (Ex:dd.mm.yyyy.txt)\n");
	scanf("%s", &file);
	printf("\nSaved event on this date are:\n");
	puts("(Ecah event is separated by'.')\n\n");
	efile=fopen(file,"r");
	if(efile==NULL){
		printf("\nEvent does not exist");
		exit(0);}
	while(!feof(efile)){
		ch=getc(efile);
		printf("%c",ch);
	}
	fclose(efile);
}

//for adding an event on a already saved event on a specific date.
	void eventedit(){
	FILE *efile;
	char c,file[14];
	printf("Enter the date from the above calendar: (Ex:dd.mm.yyyy.txt)\n");
	scanf("%s", &file);
	printf("Enter event description:\n\n");
	efile=fopen(file,"a");
	while(c!='.'){
		c=getche();
		fputc(c,efile);
	}
	fclose(efile);
	puts("\n| Event successfully added.|\n");
}
