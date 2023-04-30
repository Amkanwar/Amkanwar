You decided to use Singly Linked Lists, SLL, to store all the Persons, Customers, Employees, Driver_Employees, Managers, and Driver_Managers. 
 
For that, you created a generic class called Node to represent a unit stored in a SLL containing its ID, next*, prev*, and other data depending on the type of the Node (Person, Customer, Employee, Driver_Employee, Manager, or Driver_Manager.)
 
You also created a NodeList to contain the SLL Head*, Tail*, type, name, and methods to insert_at_the_end and delete a node with a specific ID. 
 
Moreover, you decided to add a Menu that would work continuously until the user choose the option to close the program. This Menu enables the user to add a new object, delete an object with a given ID, print the content of a given SLL, and close the program.
 
-----------------------------------------------
 
Draw the new Inheritance Hierarchy


In NodeList class, Code deleteNode(int oldNode) correctly


Update all the classes so you can print the content of each SLL as requested in the Menu


Fix the Menu Code so the Delete and Print options works correctly


Deign a proper test to check that your code works correctly on all the possible scenarios.
 
 
#include <iostream>
#include <limits>
 
using namespace std;
 
int id_count = 1;
 
int generateID()
{
    int id = id_count;
    id_count++;
    return id;
}
 
class Node
{
  public:
 
  int id;
 
  Node* prev = NULL;
  Node* next = NULL;
 
  string nodeType = "Node";
 
  void setId(int newId)
  { 
      id = newId;
  }
 
  int getId()
  {
      return id;
  }
 
  Node(int newId)
  {
      id = newId;
  }
 
  virtual void print()
  {
      cout <<"Type: Node -- ID: " << id << endl;
  }
 
};
 
class Person: public Node
{
    private:
   
    string Name;
    string Email;
    string Gender;
    string nodeType = "Person";
   
    public:
   
    //Person(){}
   
    Person(string n, string e, string g):Node(id = generateID())
    {
        Name = n;
        Email = e;
        Gender = g;
    }
   
    virtual string getType()
    {
        return nodeType;
    }
   
    void setName(string n){
        Name = n;}
       
    void setEmail(string n){
        Email = n;}
       
    void setGender(string n){
        Gender = n;}
 
    string getName(){
        return Name;}
       
    string getEmail(){
        return Email;}
       
    string getGender(){
        return Gender;}
       
    virtual void print()
    {
        cout << "Type: " << nodeType <<" -- ID: " << id << " -- Name: " << Name <<" -- Email: " << Email << " -- Gender: " << Gender << endl;
    }
       
};
 
class Customer: virtual public Person
{
    private:
   
    string DeliveryAddress;
    string nodeType = "Customer";
   
    public:
   
    Customer(string n, string e, string g, string d):Person(n, e, g)
    {
        DeliveryAddress = d;
    }
   
    string getType()
    {
        return nodeType;
    }
   
    void setDeliveryAddress(string n){
        DeliveryAddress = n;}
       
    string getDeliveryAddress(){
        return DeliveryAddress;}
       
};
 
class Employee: virtual public Person
{
    private:
   
    float Salary;
    string nodeType = "Employee";
   
    public:
   
    //Employee(){}  
    
    Employee(string n, string e, string g, float s):Person(n, e, g)
    {
        Salary = s;
    }
   
    string getType()
    {
        return nodeType;
    }
   
    void setSalary(float n){
        Salary = n;}
       
    float getSalary(){
        return Salary;}
       
};
 
class Driver_Employee: virtual public Employee
{
    private:
   
    int License;
   
    int numberOfDeliveries;
   
    string nodeType = "Driver_Emplpoyee";
   
    public:
   
    Driver_Employee(string n, string e, string g, float s, int l, int num):Person(n, e, g), Employee(n, e, g, s)
    {
        License = l;
        numberOfDeliveries = num;
    }
   
    string getType()
    {
        return nodeType;
    }
   
    void setLicense(int n){
        License = n;}
       
    void setNumberOfDeliveries(int n){
        numberOfDeliveries = n;}
       
    int getLicense(){
        return License;}
       
    int getNumberOfDeliveries(){
        return numberOfDeliveries;}
       
};
 
class Manager: virtual public Employee
{
    private:
   
    float AnnualBonus;
   
    string nodeType = "Manager";
   
    public:
   
    Manager(string n, string e, string g, float s, float a):Person(n, e, g), Employee(n, e, g, s)
    {
        AnnualBonus = a;
    }
   
    string getType()
    {
        return nodeType;
    }
   
    void setAnnualBonus(float n){
        AnnualBonus = n;}
       
    float getAnnualBonus(){
        return AnnualBonus;}
 
       
};
 
class Driver_Manager: public Driver_Employee, public Manager
{
 
    private:
 
    string nodeType = "Driver_Manager";
 
    public:
    
    Driver_Manager(string n, string e, string g, float s, int l, int num, float a):Person(n, e, g), Employee(n, e,g, s), Driver_Employee(n, e, g, s, l, num), Manager(n, e, g, s, a)
    {
       
    }
   
    string getType()
    {
        return nodeType;
    }
   
 
};
 
class NodeList: public Node
{
    private:
   
    Node* Head = NULL;
    Node* Tail = NULL;
    string name, nodeType;
   
    public:
   
    NodeList(string n, string type):Node(generateID())
    {
        Head = NULL;
        Tail = NULL;
        name = n;
        nodeType = type;
    }
   
    string getType() {return nodeType;}
   
    void setType(string nType) {nodeType = nType;}
 
    void insertLast(Node* newNode)
    {
      if(Head == NULL)
      {
          Head = newNode;
          Tail = newNode;
      }
      else
      {
        Tail->next = newNode;
        Tail= newNode;
      }
    }
   
    void deleteNode(int oldNode)
    {
   
    }
   
    virtual void print()
    {
        if(getType() == "Node")
        {
            Node* ptr = Head;
            while(ptr != NULL)
            {
                ptr->print();
                ptr = ptr->next;
            }
        }
        else if(getType() == "Person")
        {
            Node* ptr = Head;
            Person* ptr2;
            while(ptr != NULL)
            {
                ptr2 = dynamic_cast<Person*>(ptr);
                ptr2->print();
               
                ptr = ptr->next;
            }
        }
        else if(getType() == "Customer")
        {
 
        }
        else if(getType() == "Employee")
        {
 
        }
        else if(getType() == "Driver_Employee")
        {
 
        }
        else if(getType() == "Manager")
        {
 
        }
        else if(getType() == "Driver_Manager")
        {
 
        }
    }
 
};
 
void eventsHandler(NodeList* Persons, NodeList* Customers, NodeList* Employees, NodeList* Driver_Employees, NodeList* Managers, NodeList* Driver_Managers)
{
   
    cout << endl;
   
    cout << "Please choose one of the following actions to perform (Write the number of the required action):" << endl << endl;
   
    cout << "1. Add a new Person, Customer, Employee, Driver_Employee, Manager, or Driver_Manager." << endl;
   
    cout << "2. Print all Persons, Customers, Employees, Driver_Employees, Managers, or Driver_Managers." << endl;
   
    cout << "3. Delete a Person, Customer, Employee, Driver_Employee, Manager, or Driver_Manager." << endl;
   
    cout << "4. Exit the Program." << endl << endl;
 
    int action;   
 
    cin >> action;
   
    cout << endl;
   
    // Source for cin validation code: https://www.hackerearth.com/practice/notes/validating-user-input-in-c/
    if(cin.fail())
    {
         cin.clear();
         cin.ignore(numeric_limits<streamsize>::max(),'\n');
         cout << "Unrecognised Action!" << endl << endl << endl;  
    }
    switch(action)
    {
        case 1:
        {
            cout << "   Please choose one of the following options: " << endl << endl;
            cout << "   1: Add a new Person." << endl;
            cout << "   2: Add a new Customer." << endl;
            cout << "   3: Add a new Employee." << endl;
            cout << "   4: Add a new Driver_Employee." << endl;
            cout << "   5: Add a new Manager." << endl;
            cout << "   6: Add a new Driver_Manager." << endl << endl;
           
            int action2;
            cin >> action2;
            cout << endl;
           
            switch(action2)
            {
                case 1:
                {
                    string name, email, gender;
                   
                    cout << "       Please enter the new Person" << endl << endl << "       Name: ";
                    cin >> name;
                    cout << endl << "       Email: ";
                    cin >> email;
                    cout << endl << "       Gender: ";
                    cin >> gender;
                    cout << endl;
                   
                    Person* nPerson = new Person(name, email, gender);
                   
                    Persons->insertLast(nPerson);
                    
                    break;
                }   
                case 2:
                {
                    string name, email, gender, DeliveryAddress;
                   
                    cout << "       Please enter the new Customer" << endl << endl << "       Name: ";
                    cin >> name;
                    cout << endl << "       Email: ";
                    cin >> email;
                    cout << endl << "       Gender: ";
                    cin >> gender;
                    cout << endl << "       Delivery Address: ";
                    cin >> DeliveryAddress;
                    cout << endl;
                   
                    Customer* newCustomer = new Customer(name, email, gender, DeliveryAddress);
                   
                    Customers->insertLast(newCustomer);
                   
                    break;   
                }
                
                case 3:
                {
                    string name, email, gender;
                    float salary;
                   
                    cout << "       Please enter the new Employee" << endl << endl << "       Name: ";
                    cin >> name;
                    cout << endl << "       Email: ";
                    cin >> email;
                    cout << endl << "       Gender: ";
                    cin >> gender;
                    cout << endl << "       Salary: ";
                    cin >> salary;
                    cout << endl;
                   
                    Employee* newEmployee = new Employee(name, email, gender, salary);
                   
                    Employees->insertLast(newEmployee);
                   
                    break;               
                }
               
                case 4:
                {
                    string name, email, gender;
                    float salary;
                    int license;
                   
                    cout << "       Please enter the new Driver_Employee" << endl << endl << "       Name: ";
                    cin >> name;
                    cout << endl << "       Email: ";
                    cin >> email;
                    cout << endl << "       Gender: ";
                    cin >> gender;
                    cout << endl << "       Salary: ";
                    cin >> salary;
                    cout << endl << "       License: ";
                    cin >> license;
                    cout << endl;
                   
                    Driver_Employee* newDriver_Employee = new Driver_Employee(name, email, gender, salary, license, 0);
                    
                    Driver_Employees->insertLast(newDriver_Employee);
                   
                    break;                           
                }
           
                case 5:
                {
                    string name, email, gender;
                    float salary, AnnualBonus;
                   
                    cout << "       Please enter the new Manager" << endl << endl << "       Name: ";
                    cin >> name;
                    cout << endl << "       Email: ";
                    cin >> email;
                    cout << endl << "       Gender: ";
                    cin >> gender;
                    cout << endl << "       Salary: ";
                    cin >> salary;
                    cout << endl << "       AnnualBonus: ";
                    cin >> AnnualBonus;
                    cout << endl;
                   
                    Manager* newManager = new Manager(name, email, gender, salary, AnnualBonus);
                   
                    Managers->insertLast(newManager);
                   
                    break;                         
                }
               
                case 6:
                {
                    string name, email, gender;
                    float salary, AnnualBonus;
                    int license;
                    
                    cout << "       Please enter the new Driver_Manager" << endl << endl << "       Name: ";
                    cin >> name;
                    cout << endl << "       Email: ";
                    cin >> email;
                    cout << endl << "       Gender: ";
                    cin >> gender;
                    cout << endl << "       Salary: ";
                    cin >> salary;
                    cout << endl << "       AnnualBonus: ";
                    cin >> AnnualBonus;
                    cout << endl << "       License: ";
                    cin >> license;
                    cout << endl;
                   
                    Driver_Manager* newDriver_Manager = new Driver_Manager(name, email, gender, salary, license, 0, AnnualBonus);
                   
                    Driver_Managers->insertLast(newDriver_Manager);
                   
                    break;                         
                }
               
                default:
                {
                    cout << "Unrecognised Action!" << endl << endl << endl;
                }
               
            }
           
            break;
        }
       
        case 2:
        {
            cout << "   Please choose one of the following options: " << endl << endl;
            cout << "   1: Print all Persons." << endl;
            cout << "   2: Print all Customers." << endl;
            cout << "   3: Print all Employees." << endl;
            cout << "   4: Print all Driver_Employees." << endl;
            cout << "   5: Print all Managers." << endl;
            cout << "   6: Print all Driver_Managers." << endl << endl;
           
           
            
                
            break;
        }
           
        case 3:
        {
            cout << "   Please choose one of the following options: " << endl << endl;
            cout << "   1: Delete a Person." << endl;
            cout << "   2: Delete a Customer." << endl;
            cout << "   3: Delete an Employee." << endl;
            cout << "   4: Delete a Driver_Employee." << endl;
            cout << "   5: Delete a Manager." << endl;
            cout << "   6: Delete a Driver_Manager." << endl << endl;
           
            
            
            switch(action2)
            {
                case 1:
                {
                    Persons->print();
                   
                    cout << endl << "Which Person you want to delete?" << endl;
                  
                    
                    break;
                }
               
                case 2:
                {               
                 
                }
               
                case 3:
                {               
                    
                }               
                case 4:
                {               
                    
                }
                
                case 5:
                {              
                    
                }
               
                case 6:
                {               
                    
                }
               
                default:
                cout << "Unrecognised Action!" << endl << endl << endl;
            }
 
           
            break;
        }
       
        
        case 4:
        {
   
           exit(0);
           break;
        }
        
        default:
        {
            cout << "Unrecognised Action!" << endl << endl << endl;
        }
       
    }
}
 
int main()
{
 
    NodeList* Persons = new NodeList("Persons", "Person");
    NodeList* Customers = new NodeList("Customers", "Customer");
    NodeList* Employees = new NodeList("Employees", "Employee");
    NodeList* Driver_Employees = new NodeList("Driver_Employees", "Driver_Employee");
    NodeList* Managers = new NodeList("Managers", "Manager");
    NodeList* Driver_Managers = new NodeList("Driver_Managers", "Driver_Manager");
   
    cout << "Welcome to Q8Fashion Co. System!" << endl << endl;
    
    while(true)
   {
        eventsHandler(Persons, Customers, Employees, Driver_Employees, Managers, Driver_Managers);
    }
 
    return 0;
}
