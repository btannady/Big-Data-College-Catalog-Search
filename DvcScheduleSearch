/*Programmer: Benedict Tannady*/

#define _CRT_SECURE_NO_WARNINGS

#include <iostream>
#include <string> /*to_string*/
#include <fstream>
#include <set>
#include <map>

using namespace std;

#include <cstring> /*for strtok and strcpy*/
#include <cstdlib> /*atoi*/

/*function prototypes*/
void displayTermPrep(int & , string &, string &);

int main(){
    
    /*Programmer's Identification*/
    cout << "Programmer: Benedict Tannady"<< endl;
    cout << "Programmer's ID: 1591141" << endl;
    cout << "File: " << __FILE__ << endl;
    
    /*-----------------------------------------------------------------------*/
    cout << "---------------------------------------------------------------" << endl;
    
    map<string, set<int>> allClass;
    set<int>termThingy;
    
    // for parsing the inputfile
    char* token;
    char buf[1000];
    const char* const tab = "\t";
    
    // open the input file
    ifstream fin;
    fin.open("dvc-schedule.txt");
    if (!fin.good()) throw "I/O error";
    
    // read the input file
    while (fin.good())
    {
        // read the line
        string line;
        getline(fin, line);
        strcpy(buf, line.c_str());
        
        if (buf[0] == 0) continue; // skip blank lines
        
        //parse the line
        //        const string term(token = strtok(buf, tab));
        const string seasonTerm((token = strtok(buf, " ")) ? token : "");
        const string yearTerm((token = strtok(0, tab)) ? token : "");
        const string section((token = strtok(0, tab)) ? token : "");
        const string course((token = strtok(0, tab)) ? token : "");
        const string instructor((token = strtok(0, tab)) ? token : "");
        const string whenWhere((token = strtok(0, tab)) ? token : "");
        if (course.find('-') == string::npos) continue; // invalid line: no dash in course name
        const string subjectCode(course.begin(), course.begin() + course.find('-'));
        
        /*----------------------------------------------------*/
        // if I get this far, then it's a valid record
        
        //         cout << seasonTerm << '|' << yearTerm << '|' << section << '|'
        //         << course << '|' << instructor << '|'
        //         << whenWhere << '|' << subjectCode << endl;
        
        //        cout << term << '|' << section << '|'
        //        << course << '|' << instructor << '|'
        //        << whenWhere << '|' << subjectCode << endl;
        
        /*----------------------------------------------------*/
        
        /*have to do something with each term data, converting it to numerical form*/
        int termVal;
        
        if(seasonTerm == "Spring")
        {
            termVal = atoi((yearTerm + "1").c_str());
        }
        else if(seasonTerm == "Summer")
        {
            termVal = atoi((yearTerm + "2").c_str());
        }
        else
        {
            termVal = atoi((yearTerm + "3").c_str());
        }
        
        termThingy.insert(termVal);
        
        /*insert all the data in a sorted map, with each key (course) being paired with the corresponding highest termThingy value (meaning the latest term the course was found in, latest term is organized using the set feature)*/
        allClass.insert(pair<string, set<int>> (course, termThingy) );
        
    }
    fin.close();
    /*-----------------------------------------------------------------------*/
    /*entering while-loop that doesn't end program until "X" or "x" is input by the user*/
    
    string userInput;
    string courseDisplay = "";
    int termFirstDisplay = 0;
    int termLastDisplay = 0;
    
    while(true)
    {
        
        /*responsible for the displaying and obtaining input between the user*/
        cout << "Enter a course name (like, COMSC-210) to search for the last semester course offered [X/x to exit]: ";
        cin >> userInput;
        
        /*Check for loop exit-condition*/
        if(userInput == "X" || userInput == "x")break;
        
        bool foundStatus = false;
        
        /*Look up the course and output the first time that course was offered*/
        for(map<string, set<int>>::iterator map_it = allClass.begin(); map_it != allClass.end(); ++map_it)
        {
            if(map_it->first == userInput)
            {
                
                courseDisplay = map_it->first;
                foundStatus = true;
                int tempCounter = 0;
                for(set<int>::iterator set_it = map_it->second.begin(); set_it != map_it->second.end(); set_it++)
                {
                    if(tempCounter == 2)break;
                    termFirstDisplay = *set_it;
                    tempCounter++;
                    
                }
                
                break;
            }
        }
        
        /*Look up the course and output the last time that course was offered*/
        for(map<string, set<int>>::iterator map_it = allClass.begin(); map_it != allClass.end(); ++map_it)
        {
            if(map_it->first == userInput)
            {
                
                courseDisplay = map_it->first;
                foundStatus = true;
                
                for(set<int>::iterator set_it = map_it->second.begin(); set_it != map_it->second.end(); set_it++)
                {
                    
                    termLastDisplay = *set_it;
                    
                }
                
                break;
            }
        }
        
        if(foundStatus == false)
        {
            cout << userInput << " could not be found as far back as the year 2000" << endl;
        }
        else
        {
            string seasonTermDisplay = "";
            string yearTermDisplay = "";
            displayTermPrep(termFirstDisplay, seasonTermDisplay, yearTermDisplay);
            cout << courseDisplay << " was first offered in " << seasonTermDisplay << " " << yearTermDisplay <<  endl;
            
            seasonTermDisplay = "";
            yearTermDisplay = "";
            displayTermPrep(termLastDisplay, seasonTermDisplay, yearTermDisplay);
            cout << courseDisplay << " was last offered in " << seasonTermDisplay << " " << yearTermDisplay <<  endl;
        }
        cout << endl;
        cout << "---------------------------------------------------------------" << endl;
        
    }
    
    return 0;
}

/*Function that converts the five digit term (ex. 20171) back into word form (ex. Spring 2017)*/
void displayTermPrep(int &termValue, string &seasonTermDisplay, string &yearTermDisplay)
{
    
    /*get the converted string value of termValue*/
    string termValString = to_string(termValue);
    
    /*extract the season integer part of the termValue*/
    string seasonNumString;
    seasonNumString = termValString[4];
    
    /*now compute the seasonTermDisplay value depending on seasonTermDisplay value*/
    if(atoi(seasonNumString.c_str()) == 1)
    {
        seasonTermDisplay = "Spring";
    }
    else if(atoi(seasonNumString.c_str()) == 2)
    {
        seasonTermDisplay = "Summer";
    }
    else
    {
        seasonTermDisplay = "Fall";
    }
    
    /*now we can cut off the season part off of termValue so that yearTermDisplay can cleanly display year to user*/
    for(int i = 0; i < 4; i++)
    {
        yearTermDisplay = yearTermDisplay + termValString[i];
    }
    
}
