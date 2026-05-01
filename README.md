#include <iostream>
using namespace std;
struct subject{
    string title;
    string ISBN;
    string author;
    int edition;
};
class sub{
private:
    subject subjects[1000];
    int count=0;
public:
    void addSubject(){
        if(count>=1000){
            cout<<"Subject Limit Reached!"<<endl;
            return;
        }
        cout<<"Enter Subject Title: ";
        cin>>subjects[count].title;
        cout<<"Enter ISBN: ";
        cin>>subjects[count].ISBN;
        cout<<"Enter Author Name: ";
        cin>>subjects[count].author;
        cout<<"Enter Edition: ";
        cin>>subjects[count].edition;
        count++;
        cout<<"Subject Added Successfully!"<<endl;
    }
    void printsubject(){
        if(count==0){
            cout<<"No Subjects Found"<<endl;
            return;
        }
        for(int i=0;i<count;i++){
            cout<<"\nTitle: "<<subjects[i].title<<endl;
            cout<<"ISBN: "<<subjects[i].ISBN<<endl;
            cout<<"Author: "<<subjects[i].author<<endl;
            cout<<"Edition: "<<subjects[i].edition<<endl;
        }
    }
    void searchSubject(string searchtitle){
        for(int i=0;i<count;i++){
            if(subjects[i].title==searchtitle){
                cout<<"Subject Found!"<<endl;
                cout<<"Title: "<<subjects[i].title<<endl;
                cout<<"ISBN: "<<subjects[i].ISBN<<endl;
                cout<<"Author: "<<subjects[i].author<<endl;
                cout<<"Edition: "<<subjects[i].edition<<endl;
                return;
            }
        }
        cout<<"Subject Not Found"<<endl;
    }
    void updatesubject(string updatetitle){
        for(int i=0;i<count;i++){
            if(subjects[i].title==updatetitle){
                cout<<"Enter New ISBN: ";
                cin>>subjects[i].ISBN;
                cout<<"Enter New Author: ";
                cin>>subjects[i].author;
                cout<<"Enter New Edition: ";
                cin>>subjects[i].edition;
                cout<<"Subject Updated Successfully!"<<endl;
                return;
            }
        }
        cout<<"Subject Not Found"<<endl;
    }
    void deletesubject(string deletetitle){
        for(int i=0;i<count;i++){
            if(subjects[i].title==deletetitle){
                for(int j=i;j<count-1;j++){
                    subjects[j]=subjects[j+1];
                }
                count--;
                cout<<"Subject Deleted Successfully!"<<endl;
                return;
            }
        }
        cout<<"Subject Not Found!"<<endl;
    }
};
struct session{
    string subjectName;
    int hours;
    session* link;
};
class study{
private:
    session* start;
public:
    study(){
	 start=NULL; 
	 }
    void addSession(){
        session* newSession=new session;
        cout<<"Enter Subject Name: ";
        cin>>newSession->subjectName;
        cout<<"Enter Study Hours: ";
        cin>>newSession->hours;
        newSession->link=NULL;
        if(start==NULL){
            start=newSession;
        }
        else{
            session* temp=start;
            while(temp->link!=NULL){
                temp=temp->link;
            }
            temp->link=newSession;
        }
        cout<<"Study Session Added Successfully!"<<endl;
    }
    void displaySchedule(){
        if(start==NULL){
            cout<<"No Study Sessions Found!"<<endl;
            return;
        }
        session* temp=start;
        while(temp!=NULL){
            cout<<"\nSubject: "<<temp->subjectName<<endl;
            cout<<"Hours: "<<temp->hours<<endl;
            temp=temp->link;
        }
    }
    void deleteSession(string name){
        if(start==NULL){
            cout<<"No Sessions to Delete"<<endl;
            return;
        }
        session* temp=start;
        session* prev=NULL;
        while(temp!=NULL && temp->subjectName!=name){
            prev=temp;
            temp=temp->link;
        }
        if(temp==NULL){
            cout<<"Session Not Found!"<<endl;
            return;
        }
        if(prev==NULL){
            start=temp->link;
        }
        else{
            prev->link=temp->link;
        }
        delete temp;
        cout<<"Session Deleted Successfully!"<<endl;
	}
    void updateHours(string name){
        session* temp=start;
        while(temp!=NULL){
            if(temp->subjectName==name){
                cout<<"Enter New Study Hours: ";
                cin>>temp->hours;
                cout<<"Study Hours Updated Successfully!"<<endl;
                return;
            }
            temp=temp->link;
        }
        cout<<"Session Not Found!"<<endl;
    }
};
class Adaptive{
private:
    string subject[5];
    int hours[5];
    int score[5];
    int risk[5];
public:
    void run(){
        cout<<"\nENTER SUBJECT DATA"<<endl;
        for(int i=0;i<5;i++){
            cout<<"\nSubject "<<i+1<<endl;
            cout<<"Name: ";
            cin>>subject[i];
            cout<<"Study Hours: ";
            cin>>hours[i];
            cout<<"Test Score: ";
            cin>>score[i];
            risk[i]=100-score[i];
        }
        for(int u=4;u>=1;u--){
            for(int i=0;i<u;i++){
                if(score[i]>score[i+1]){
                    swap(score[i],score[i+1]);
                    swap(hours[i],hours[i+1]);
                    swap(risk[i],risk[i+1]);
                    swap(subject[i],subject[i+1]);
                }
            }
        }
        cout<<"\nSUBJECT REPORT"<<endl;
        for(int i=0;i<5;i++){
            cout<<"\nSubject: "<<subject[i]<<endl;
            cout<<"Hours: "<<hours[i]<<endl;
            cout<<"Score: "<<score[i]<<endl;
            cout<<"Risk: "<<risk[i]<<endl;
        }
        cout<<"\nPRIORITY STUDY ORDER"<<endl;
        bool found=false;
        for(int i=0;i<5;i++){
            if(score[i]<50){
                cout<<"- "<<subject[i]<<endl;
                found=true;
            }
        }
        if(!found)
            cout<<"No Weak Subjects Found!"<<endl;
    }
};
#define MAX_ACTIONS 10
class Stack {
private:
    string actions[MAX_ACTIONS];
    int top;
public:
    Stack(){
	 top=-1;
	  }
    void push(string action){
        if(top==MAX_ACTIONS-1){
            cout<<"Stack Overflow! Cannot save more actions.\n";
        }else{
            top++;
            actions[top]=action;
            cout<<"Action Saved Successfully!\n";
        }
    }
    void pop(){
        if(top==-1){
            cout<<"Nothing to Undo!\n";
        }else{
            cout<<"Undo Action: "<<actions[top]<<endl;
            top--;
        }
    }
    void display(){
        if(top==-1){
            cout<<"No Actions Stored.\n";
        }
		else{
            cout<<"\nStored Actions:\n";
            for(int i=top;i>=0;i--){
                cout<<actions[i]<<endl;
            }
        }
    }
};
void predictResult(){
    int totalSubjects;
    float totalMarks=0, score;
    cout<<"Enter number of subjects: ";
    cin>>totalSubjects;
    for(int i=1;i<=totalSubjects;i++){
        cout<<"Enter marks of subject "<<i<<": ";
        cin>>score;
        totalMarks+=score;
    }
    float average = totalMarks / totalSubjects;
   cout<<"\nAverage Marks: "<<average<<endl;
    if(average>=80)
        cout<<"Prediction: Excellent Result\n";
    else if(average>=60)
        cout<<"Prediction: Good Result\n";
    else if(average>=40)
        cout<<"Prediction: Pass\n";
    else
        cout<<"Prediction: Needs Improvement\n";
}
int main(){
    sub subjectSystem;
    study studySystem;
    Adaptive adaptiveSystem;
    Stack student4;
    int choice=0;
    string name, action;
    while(choice!=15){
        cout<<"\n1.Add Subject"<<endl;
        cout<<"2.Display Subjects"<<endl;
        cout<<"3.Search Subject"<<endl;
        cout<<"4.Update Subject"<<endl;
        cout<<"5.Delete Subject"<<endl;
        cout<<"6.Add Study Session"<<endl;
        cout<<"7.Display Study Schedule"<<endl;
        cout<<"8.Delete Study Session"<<endl;
        cout<<"9.Update Study Hours"<<endl;
        cout<<"10.Run Adaptive System"<<endl;
        cout<<"11.Save Action (Student 4)"<<endl;
        cout<<"12.Undo Last Action (Student 4)"<<endl;
        cout<<"13.Display Actions (Student 4)"<<endl;
        cout<<"14.Predict Exam Result (Student 4)"<<endl;
        cout<<"15.Exit"<<endl;
        cout<<"Enter Choice: ";
        cin >> choice;
        if(cin.fail()){
            cin.clear();
            cin >> choice;
            cout<<"Invalid input! Enter number only."<<endl;
            continue;
        }
        switch(choice){
            case 1: subjectSystem.addSubject();
			 break;
            case 2: subjectSystem.printsubject(); 
			break;
            case 3:
                cout<<"Enter Title: ";
                cin>>name;
                subjectSystem.searchSubject(name);
                break;
            case 4:
                cout<<"Enter Title: ";
                cin>>name;
                subjectSystem.updatesubject(name);
                break;
            case 5:
                cout<<"Enter Title: ";
                cin>>name;
                subjectSystem.deletesubject(name);
                break;
            case 6: studySystem.addSession(); 
			break;
            case 7: studySystem.displaySchedule();
			 break;
            case 8:
                cout<<"Enter Name: ";
                cin>>name;
                studySystem.deleteSession(name);
                break;
            case 9:
                cout<<"Enter Name: ";
                cin>>name;
                studySystem.updateHours(name);
                break;
            case 10: adaptiveSystem.run(); 
			break;
            case 11:
                cout<<"Enter action (single word): ";
                cin>>action;
                student4.push(action);
                break;
            case 12: student4.pop();
			 break;
            case 13: student4.display();
			 break;
            case 14: predictResult(); 
			break;
            case 15: cout<<"Exiting Program!"<<endl; 
			break;
            default: cout<<"Invalid Choice!"<<endl;
        }
    }

    return 0;
}
