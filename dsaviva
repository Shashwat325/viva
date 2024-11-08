#include <iostream>
using namespace std;

class node{
public:
    int roll_no;
    int marks;
    node* next;
    node* prev;

    node(int r, int m){
        roll_no=r;
        marks=m;
        this->next=NULL;
        this->prev=NULL;
    }
};
node* split(node* head){
    node* fast=head;
    node* slow=head;
    while(fast->next && fast->next->next){
        fast=fast->next->next;
        slow=slow->next;
    }
    node* temp=slow->next;
    slow->next=NULL;
    if (temp) {
        temp->prev=NULL;
        return temp;
    }
}
node* merge(node* first, node* second) {
    if(!first){
        return second;
    }
    if(!second){
        return first;
    }
    if (first->marks<second->marks){
        first->next=merge(first->next, second);
        first->next->prev=first;
        first->prev=NULL;
        return first;
    } else {
        second->next=merge(first, second->next);
        second->next->prev=second;
        second->prev=NULL;
        return second;
    }
}
node* mergeSort(node* head) {
    if (!head || !head->next) {
        return head;
    }
    node* second=split(head);
    head=mergeSort(head);
    second=mergeSort(second);
    return merge(head,second);
}
void deletenomarks(node*& head) {
    node* temp=head;
    while (temp!=NULL) {
        if (temp->marks==-1) {
            node* toDelete=temp;
            if (temp==head) {
                head=head->next;
                head->prev=NULL;
            } 
            else{
                temp->prev->next=temp->next;
                temp->prev=NULL;
            }
            temp=temp->next;
        } else {
            temp=temp->next;
        }
    }
}
void updateMarks(node* head,int rollNo,int newMarks) {
    node* temp=head;
    while (temp!=NULL){
        if (temp->roll_no==rollNo) {
            temp->marks=newMarks;
            return;
        }
        temp=temp->next;
    }
    cout <<"Student with Roll No. "<< rollNo<<" not found."<<endl;
}

void inserthead(node*& head,int r,int m) {
    node* temp=new node(r,m);
    if (head!=NULL) {
        temp->next=head;
        head->prev=temp;
    }
    head=temp;
}

void inserttail(node*& tail,int r,int m) {
    node* temp=new node(r,m);
    tail->next=temp;
    temp->prev=tail;
    tail=temp;
}

void print(node* head){
    node* temp=head;
    while(temp!=NULL){
        cout<<"Roll No.:"<<temp->roll_no<<"\t";
        cout<<"Marks:"<<temp->marks<<endl;
        temp=temp->next;
    }
}
int main() {
    node* head=new node(101, 89);
    node* tail=head;
    inserttail(tail,102,78);
    inserttail(tail,103,-1);
    inserttail(tail,104,-1);
    inserttail(tail,105,50);
    inserthead(head,100,94);
    cout <<"list of students:"<< endl;
    print(head);
    updateMarks(head, 104, 70);
    cout<<"updates marks list :"<<endl;
    print(head);
    head = mergeSort(head);
    cout <<"sorting by marks:"<< endl;
    print(head);
    deletenomarks(head);
    cout<<"After deleting students with no marks:"<<endl;
    print(head);
    return 0;
}
