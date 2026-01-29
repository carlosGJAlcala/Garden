---
title: "Ejemplo De Practica En C"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - c++
---

Metodo main y como se llamar una clase  hay que incluir main.

```c
#include <stdio.h>

> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Algoritmos/Quick-Sort|Quick Sort]].

#include <iostream>
#include "control/Core.hpp"
#include "vista/Vista.hpp"
using namespace std;

int main(int argc, char **argv)
{
    Vista* vista = new Vista();
    vista->MainInterface();
	return 0;
}

```

```c
#ifndef VISTA_HPP
#define VISTA_HPP
#include "control/Core.hpp"
class Vista
{
public:
    Vista();
    ~Vista();
    void MainInterface();
};

#endif // VISTA_HPP

```

```c
#include "Vista.hpp"
#include <stdio.h>
#include <iostream>

#include <thread>

using namespace std;
Core* core;


Vista::Vista()
{
core=new Core();

}

Vista::~Vista()
{
}
 void Vista::MainInterface(){
Stack* stack;
Queue* queue;    
List* list;
stack=core->getStack();
queue=core->getQueue();
list=core->getList();
    int select=0;
    char a;
    int status = 0;
    //thread thread_object(callable)


    cout<<"\n Making new a stack, a new queue and a enw list...\n";
    cout<<"\n Generate random numbers: \n";
    core->Generation(stack, queue, list);
    cout<<"\nData Generation succeed and numbers save in file.\n";
    do{
            cout<<"---------------------------------------------------------";
            cout<<"---------------------------------------------------------";
    cout<<"\nPress 1 if you want to sort of DS \n";
    cout<<"\nPress 2 if you want to search one number\n";
    cout<<"\nPress 3 if you want to wacth data number\n";
    cout<<"\nPress 4 if you want to remove a number\n";
    cout<<"\nPress 5 if you want to add a number\n";
    cout<<"\nPress 6 if you want to save DS in file\n";
    cout<<"\nPress 7 if you want to exist\n";
    cout<<"---------------------------------------------------------";
        cout<<"---------------------------------------------------------";
    cin>> status;

   
    switch(status){
       
            case (1):
            system("cls");
            cout<<"***********************************************";
            cout<<"\nPress 1 if you want to sort of Stack  \n";
            cout<<"\nPress 2 if you want to sort of Queue \n";
            cout<<"\nPress 3 if you want to sort of List  \n";
            cout<<"\nPress 4 if you want to go back to menu  \n";
            cout<<"***********************************************";
            cin>> select;
            switch(select){
                case(1):
                core->SortStack(stack);
                break;
                case(2):
                core->BublesortQueue(*queue);
                break;
                case(3):
                core->setList(core->QuicksortList(list)); 
                break;
                case(4):
                                system("cls"); 

                break;
            }
            break;
              
            case (2):
            system("cls");
            cout<<"***********************************************";
            cout<<"\nPress 1 if you want to serch in Stack  \n";
            cout<<"\nPress 2 if you want to serch in Queue \n";
            cout<<"\nPress 3 if you want to serch in List  \n";
            cout<<"\nPress 4 if you want to go back to menu  \n";
            cout<<"***********************************************";
            cin>> select;
            switch(select){
                case(1):
                cout<<"***********************************************";
                cout<<"\nPress 1 if you want to look for the higher number\n";
                cout<<"Press 2 if you want to look for  the 100 smaller numbers\n";
                cout<<"\nPress 3 if you want to go back to menu  \n";
                cout<<"***********************************************";
                cin>> select;
                switch(select){
                    case(1):
                        core->sequentiaSearchStackHigherNumber(stack);
                    break;
                    case(2):
                    core->sequentiaSearchStack100Number(stack);
                    break;
                             case(3):
                                             system("cls"); 

                break;
                }
              
                break;
                case(2):
                system("cls");
                cout<<"***********************************************";
                cout<<"\nPress 1 if you want to look for the higher number\n";
                cout<<"Press 2 if you want to look for  the 100 smaller numbers\n";
                cout<<"\nPress 3 if you want to go back to menu  \n";
                cout<<"***********************************************";
                cin>> select;
                switch(select){
                    case(1):
                        core->sequentiaSearchQueueHigherNumber(queue);
                    break;
                    case(2):
                    core->sequentiaSearchQueue100Number(queue);
                    break;
                             case(3):
                                             system("cls"); 

                break;
                }

                break;
                case(3):
                system("cls");
                cout<<"***********************************************";
                cout<<"\nPress 1 if you want to look for the higher number\n";
                cout<<"Press 2 if you want to look for  the 100 smaller numbers\n";
                                cout<<"\nPress 3 if you want to go back to menu  \n";

                cout<<"***********************************************";
                cin>> select;
                switch(select){
                    case(1):
                        core->sequentiaSearchListHigherNumber(list);
                    break;
                    case(2):
                        core->sequentiaSearchListHigherNumber(list);
                    break;
                case(3):
                                system("cls"); 

                break;
                }

                break;
                case(4):
                system("cls"); 
                break;
            }
            break;
            case (3):
            system("cls");
            cout<<"***********************************************";
            cout<<"\nPress 1 if you want to watcth of Stack  \n";
            cout<<"\nPress 2 if you want to watcth of Queue \n";
            cout<<"\nPress 3 if you want to watcth of List  \n";
                        cout<<"\nPress 4 if you want to go back to menu  \n";
            cout<<"***********************************************";
            cin>> select;
            switch(select){
                case(1):
                core->watchStack(stack);
                break;
                case(2):
                core->watchQueue(queue);
                break;
                case(3):
                core->watchList(list);
                break;
                case(4):
                system("cls"); 
                break;
            }
       
            break;
            case (4):
            system("cls");
            cout<<"***********************************************";
            cout<<"\nSelect number from data structure for delete: \n";
            cout<<"***********************************************";
            cin>> select;
            
            queue->QueueDelete(select);
            list->ListDelete(select);
            stack ->DeleteStack(select);
            
      
            break;
            case (5):
            system("cls");    
            cout<<"\nSelect number for add to  data structure \n";
            cin>> select;
            core->IntroduceNumber(select,stack,queue,list);
            break;
            case (6):
            system("cls");
            cout<<"***********************************************";
            cout<<"\nPress 1 if you want to save stack in file \n";
            cout<<"\nPress 2 if you want to save Queue in file \n";
            cout<<"\nPress 3 if you want to save List  in file \n";
            cout<<"\nPress 4 if you want to go back to menu  \n";
            cout<<"***********************************************";
            cin>> select;
            switch(select){
                case(1):
                core->saveFileStack(stack);
                break;
                case(2):
                core->saveFileQueue(queue);
                break;
                case(3):
                core->saveFileList(list); 
                
                break;
                case(4):
                system("cls"); 
                break;
            }           
            break;
            case (7):  
            system("cls");      
            cout<<"\nEnd of the program";
            break;
    }
} 
    while(status!=7);
}

```