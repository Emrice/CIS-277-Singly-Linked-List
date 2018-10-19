# CIS-277-Singly-Linked-List

/*
Class: CIS-277-001
Professor: Alan Eliscu
Date: 10/08/2018
Name: Marlen 

This assignment is an enhancement of the example provided in the textbook for linking airports.
Assume the user provides you with the following 2 items of information for as many different airports as they desire:
1.  Standard 3 character airport code ///   2.  Distance from New York City's LaGuardia
Airport to the specified airport, in miles.
The head of the list should be represented with an element whose value is 'LGA' and whose distance is 0.
Airport codes will be provided in order of closest to furthest away.
Create a singly linked list to house each of the airports as a node in the same order in which it was provided (nearest to furthest).
Each node should contain both the airport code and the entered distance.
Once the list is built, develop an additional function which allows the user to search for a
user-specified code and then output all other codes and distances which follow it in the list.
*/

#include <iostream>
#include <stdlib.h>
#include <string>
#include <cstdio>
#include <cstdlib>
using namespace std;

class Node
{
    private:
        string airports;
        double miles;
        Node* currentNext;      //Pointer -> current next variable of Node
    public:
        string getAirports()    //Returns data values
            { return airports; };
        double getMiles()
            { return miles; }
        Node* getCurrentNext()  //Returns pointer for next node
            { return currentNext; };
        void LinkNodes(Node* newNodeAddress)      //sets next pointer = to newNode's address
            { currentNext = newNodeAddress; };
        void SetNodeData(string newNodeData, double newNodeMiles)  //sets data = to newNode's data
            { airports = newNodeData; miles = newNodeMiles; };
};

class LinkList
{
    private:
        Node *head;
    public:
        LinkList()
            { head = NULL; };   //initializes head to be equal to null
        void InsertNode (string, double);
        void InsertNode();      //creates a new node
        void SearchList();
        void DisplayList();
};

int main ()
{
    LinkList listAirports;
    int choice = 0;
    listAirports.InsertNode("LGA", 0);

    cout <<"\tDisclaimer: For option 1 you will need to input airports in order from closest to farthest away.\n";
    cout <<"\n:::::::::::::::::::: AIRPORT PROGRAM ::::::::::::::::::::\n";

    while (choice != 4)
    {
        cout <<"\n\n::::::::::Options:::::::::: \n";
        cout << "1. Add Airport\n";
        cout << "2. Search for an Airport\n";
        cout << "3. Display all airports\n";
        cout << "4. Exit.\n\n";
        cout << "Option: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
            {
                listAirports.InsertNode();
                cout << endl;
                break;
            }
            case 2:
            {
                listAirports.SearchList();
                cout << endl;
                break;
            }
            case 3:
            {
                listAirports.DisplayList();
                cout << endl;
                break;
            }
            case 4:
            default:
                cout << "Program Terminating....\n\n";

        }
    }

    cout << "\n:::::::::::::::::::: END OF PROGRAM ::::::::::::::::::::\n";

    system("pause");
    return 0;
}

void LinkList::InsertNode (string code = "LGA", double distance = 0)
{
    Node* newNode = new Node();     //New Node

    newNode->SetNodeData(code, distance);
    newNode->LinkNodes(NULL);     //sets the 'next' section of newly made node point to null

    Node *temp = head;      //Temp pointer points to the same address as head

    if (temp != NULL)       //If temp is not equal to NULL
    {
        while ( temp->getCurrentNext() != NULL)    //While the 'next' section of the node isnt pointing to the end of the list
        {
            temp = temp->getCurrentNext();     //Gets 'next' part of current node and makes it equal to temp ---->
                                            //Temp is now pointing to what the previous node's 'next' was pointing to.
        }

        temp->LinkNodes(newNode);     //if it is pointing to null it sets the current nodes 'next' pointer --->
                                            //to the newNode that was made in this function
    }
    else        //If temp is equal to NULL
    {
        head = newNode;     //Address of the first node is assigned to head
    }
}

void LinkList::InsertNode ()
{
    Node* newNode = new Node();     //New Node
    string input;
    double distance;

    cout << "Enter airport 3 letter code (Format: NWK):  ";
    cin >> input;

    cout << "Distance from LaGuardia Airport (in miles): ";
    cin >> distance;

    newNode->SetNodeData(input, distance);
    newNode->LinkNodes(NULL);     //sets the 'next' section of newly made node point to null

    Node *temp = head;      //Temp pointer points to the same address as head

    if (temp != NULL)       //If temp is not equal to NULL
    {
        while ( temp->getCurrentNext() != NULL)    //While the 'next' section of the node isnt pointing to the end of the list
        {
            temp = temp->getCurrentNext();     //Gets 'next' part of current node and makes it equal to temp ---->
                                            //Temp is now pointing to what the previous node's 'next' was pointing to.
        }

        temp->LinkNodes(newNode);     //if it is pointing to null it sets the current nodes 'next' pointer --->
                                            //to the newNode that was made in this function
    }
    else        //If temp is equal to NULL
    {
        head = newNode;     //Address of the first node is assigned to head
    }
}

void LinkList::SearchList ()
{
    string value;
    bool x = false;
    Node *temp = head;

    if (temp == NULL)
    {
        cout << "\n No Airports Found. \n";
        return;
    }

    cout << "Enter airport code to search for: ";
    cin >> value;

    while (x == false)
    { // As long as the node hasnt been found
        if (value == temp->getAirports() )
        { // if the value is == getCode()
            x = true; // Then the 'found' variable is set to true
        }
        else if (temp->getCurrentNext() == NULL)
        { // Else if the nodes 'next' pointer == NULL or the end of the list, print the message and break out of the loop
            cout << "\nThe airport code '" << value << "' was not found.\n\n";
            break;
        }
        else
        {
            temp = temp->getCurrentNext();  // Get the next node and set it as the current node
        }
  }

  if(x)
  { // if the variable has been found (found == true)
    while (temp != NULL)
    { // as long as 'temp' doesnt equal to NULL
      cout << "\nAirport: " << temp->getAirports() << " - " << temp->getMiles() << " MILES ---> "; // print this with the airport code and the miles
      temp = temp->getCurrentNext(); // set the current node to the next node (get the next node in the list)
    }
    cout << "End of List\n";
  }
}

void LinkList::DisplayList ()
{
    Node *temp = head;

    if (temp == NULL)
    {
         cout << "\n No Airports Found. \n";
         return;
    }


    if ( temp->getCurrentNext() == NULL)
    {
        cout << "Airport: " << temp->getAirports() <<  " - " << temp->getMiles() << " MILES ----> End of List\n";
    }
    else
    {
        while( temp != NULL)
        {
            cout << "\nAirport: " << temp->getAirports() << " - " << temp->getMiles() << " MILES ---> ";
            temp = temp->getCurrentNext();
        };

        cout << "End of List\n\n\n";
    }
}


