# question1
round robin algorithm


#include<stdio.h> 
 
struct job{ 
 	int id;  	int arrivalTime; 
 	int bustTime; 
 	 
 	int rbt; 
 	int cmpt; 
}f[100], s[100], m[100]; 
 
/*instruction function provides with all the instruction for the alorithm */ 
 
void instruction(){ 
 printf("\nWelcome, please follow these instruction for proper functioning of the program" 
 	 	 	"\n**>Enter time in 2400 hours format. example for 10:30 am enter 1030" 
   "\n**>Enter Query arrival times in ascending order, i.e., in real time arrival manner\n" 
 	 	 	"\n**>Enter Query arrival times between 1000 and 1200 beacause linux expert is avaliable between these time only \n" 
 	 	 	"\nAll Time units are in minutes. \n\n" 
 	 	 	); 
} 
 
 
 
 
int n, fc=0, sc=0, mc=0; 
 
 
 
 
/* mergerAlgo function will merger both faculty(f[]) and student array(s[]) into m[] according to the priority */ 
 
void mergerAlgo(){  	int isc=0, ifc= 0, min, flag;  	if( fc!=0  && sc!=0){  	 	while(isc<sc && ifc<fc){ 
 	 	 	if(f[ifc].arrivalTime == s[isc].arrivalTime){ 
 	 	 	 	m[mc] = f[ifc]; 
 	 	 	 	mc++;  	 	 	 	ifc++; 
 	 	 	 	m[mc]= s[isc]; 
 	 	 	 	mc++; 
 	 	 	 	isc++; 
 	 	 	} 
 	 	 	else if(f[ifc].arrivalTime < s[isc].arrivalTime){ 
 	 	 	 	m[mc]= f[ifc]; 
 	 	 	 	mc++; 
 	 	 	 	ifc++; 
 	 	 	} 
 	 	 	else if(f[ifc].arrivalTime > s[isc].arrivalTime){ 
 	 	 	 	m[mc]= s[isc]; 
 	 	 	 	mc++; 
 	 	 	 	isc++; 
 	 	 	} 
 	 	 	else; 
 	 	} 
 	 	if(mc != (fc+sc)){  	 	 	if(fc!=ifc){  	 	 	 	while(ifc!=fc){ 
 	 	 	 	 	m[mc]= f[ifc];  	 	 	 	 	mc++;  	 	 	 	 	ifc++; 
 	 	 	 	} 
 	 	 	} 
 	 	 	else if(sc!=isc){  	 	 	 	while(isc!=sc){ 
 	 	 	 	 	m[mc]= s[isc]; 
 	 	 	 	 	mc++;  	 	 	 	 	isc++; 
 	 	 	 	} 
 	 	 	} 
 	 	} 
 	} 
 	else if(fc==0){ 
 	 	while(isc!=sc){  	 	 	m[mc]= s[isc];  	 	mc++;  	 	isc++; 
	 	} 
} 
 	else if(sc==0){ 
 	 	while(ifc!=fc){  	 	 	m[mc]= f[ifc]; 
 	 	 	mc++;  	 	 	ifc++; 
 	 	} 
 	} 
 	else { 
 	 	printf("\n No valid Jobs available\n"); 
 	} 
} 
 
int quantam; 
 
/* roundRobinAlgo function  implements round robin alorithm */ 
 
void roundRobinAlgo(){ 
 	int time= m[0].arrivalTime, mark=0, cc=0, i, rc; 
 	while(time!=120 && cc!=mc){  	 	for(i=0; i<=mark; i++){ 
 	 	 	if(m[i].rbt > quantam){ 
 	 	 	 	time += quantam;  	 	 	 	m[i].rbt -= quantam; 
 	 	 	} 
 	 	 	else if(m[i].rbt <=quantam && m[i].rbt !=0){ 
 	 	 	 	time += m[i].rbt;  	 	 	 	m[i].rbt =0;  	 	 	 	m[i].cmpt = time; 
 	 	 	 	cc++;  	 	 	} 
 	 	 	else; 
 	 	} 
 	 	int start = mark+1;  	 	for(rc= start; rc<mc; rc++){ 
 	 	 	if(m[rc].arrivalTime <= time){  	 	 	 	mark++; 
 	 	 	} 
 	 	} 
 	} 	 
} 
 
 
/*printFunction function implements the output from the roundRobinAlgo */ 
 
 
void printFunction(){  	int i=0, total=0, sum=0;   	double avg; 
 	printf("\nSummary for the Execution\n"); 
 	printf("\nQuery ID\tArrival Time\tRessolving Time\tCompletion Time\tTurn Around 
Time\tWaiting Time"); for(i; i<mc; i++){  	printf("\n%d\t\t%d\t\t%d\t\t%d\t\t%d\t\t\t%d", 
	 	m[i].id, (m[i].arrivalTime+1000), m[i].bustTime, (m[i].cmpt+1000), (m[i].cmpt-
m[i].arrivalTime), ((m[i].cmpt-m[i].arrivalTime)- m[i].bustTime)); 
 	 	total= m[i].cmpt; 
 	 	sum+= (m[i].cmpt-m[i].arrivalTime); 
 	} 
 	avg = sum/mc; 
 	printf("\n\nTotal time Spent for all queries: %d", total); 
 	printf("\nAverage query time: %lf", avg); 
 	printf("\nProcess Execution Complete"); 
} 
 
/* inputFunction takes all the input fo-r the algorithm*/ 
 
void inputFunction(){  	int map,  i, t; 
 	printf("Enter total no of queries: "); scanf("%d", &n);  	if(n==0) { printf("\n No queries\n"); } 
 	else{ 
 	 	printf("\nEnter Quantam for each Process: "); scanf("%d", &quantam);  	 	printf("\nEnter 1 for faculty and 2 for student\n");  	 	for(i=0; i<n; i++){ 
 	 	 	printf("\nJob Type (1/2): "); scanf("%d", &map); 
 	 	 	if(map==1){ 
 	 	 	 	printf("Query Id: "); scanf("%d", &f[fc].id);  	 	 	 	printf("Arrival Time: "); scanf("%d", &t);  	 	 	 	if(t<1000 || t>1200){  	 	 	 	 	printf("\nEnter Correct time");  	 	 	 	 	inputFunction(); 
 	 	 	 	} 
 	 	 	 	else{f[fc].arrivalTime= t-1000;} 
    printf("Resolving Time: "); scanf("%d", &f[fc].bustTime);  f[fc].rbt= f[fc].bustTime;  
 	 	 	 	fc++; 
 	 	 	} else{ 
 	 	 	 	printf("Query Id: "); scanf("%d", &s[sc].id);  	 	 	 	printf("Arrival Time: "); scanf("%d", &t);   	 	 	 	if(t<1000 || t>1200){  	 	 	 	 	printf("\nEnter Correct time\n"); 
 	 	 	 	 	inputFunction(); 
 	 	 	 	} 
 	 	 	 	else {s[sc].arrivalTime= t-1000; } 
    printf("Resolving Time: "); scanf("%d", &s[sc].bustTime);  s[sc].rbt= s[sc].bustTime; 
 	 	 	 	sc++; 
 	 	 	} 
 	 	} 
 	} 
} 
 
 
 
main(){  	instruction(); inputFunction(); 
mergerAlgo(); 
 	roundRobinAlgo(); 
 	printFunction(); 
} 
 
