Data Migration Techniques

Data Migration-> It is also called as Data Transfer. Data Migration means migrating the data from Legacy system to 
SAP system.

Legacy System -> The system other than the SAP system is called as Legacy system. It is also called as Non-SAP system. 
                 It contains the data to be transferred.


Steps of Data Migration :

1) Extracting the data -> Extracting the data from the Legacy system into a file .
2) Coverting the data ->  Coverting the data to appropriate format. This is called as Conversion.
3) Importing the data ->  Importing the data in to SAP system. 
4) Verifying the data ->  Checking the accuracy of data in SAP system. 

Data Migration Techniques/Tools:

1) BDC( Batch Data Communication)
2) LSMW( Legacy System Migration Workbench)
3) BAPI( Business Application Programming Interface)  


                                     BDC( Batch Data Communication)

The purpose of BDC is to transfer data from Non-SAP( Legacy) system to SAP system.

Principle - BDC Works on the principle of Screen recording.   

Transaction code for Recording : SHDB

Precautions for Recording : 

a) Never Use F4 & F1 help.
b) Do not pass wrong values.


BDC Methods -> There are 3 methods for BDC.

1) Call Transaction Method 

2) Session Method

3) Direct Input Method.

Call transaction Method and Session Method are called as Batch Input methods.


1) Call Transaction Method -> 

   Call transaction 'Transaction Code' USING ( BDC Internal table) MODE 'A or N or E' 
   UPDATE 'A or S or L'  Messages INTO ( Internal table).
  
   Example : Call transaction 'MM01' USING LT_BDCDATA MODE 'A' UPDATE 'S' Messages INTO LT_MESSTAB.  

   Processing Modes -> 
   A -> All screen( It will show screen by screen processing)
   N -> No Screen( It will not show any screen, directly we will get a output).
   E -> Error( If there is a Error in BDC - It will show the screen where the error is, 
        If there is no Error - It will not show any screen )
           

  UPDATE Modes->
  
  A -> Asynchoronous( COMMIT WORK)
  The called transaction does not wait for any updates to be completed.
  Results in faster execution of the data transfer program.


  S -> Synchronous( Sync between the sender and receiver , COMMIT WORK AND WAIT)
  
  The called transaction waits for any updates that it produces to be completed.
  Execution is slower than with asynchronous updating because called
  transactions wait for updating to be completed. 

  P1         P2
  Sender     Receiver
  Called     Calling 
   

  L -> Local Update 
  If the data is updated locally, the update of the database will not be processed
  in a separate process, the update functions are run in the same dialog process.
  

2) Session Method -> Use Function Modules - BDC_OPEN_GROUP , BDC_INSERT, BDC_CLOSE_GROUP

   Run the Session with the help of transaction code : SM35.

   Processing Modes : Foreground , Display Errors only, Background.

Question : What is the significance of KEEP parameter in BDC_OPEN_GROUP?

Answer : Indicator to keep processed sessions.( Keep = 'X' - Processed sessions will remain in SM35 , KEEP = ' '( Processed session will not be available ) ).

HOLDDATE -> To lock a session for a specified date.


3) Direct Input Method -> Direct Inputs are standard SAP programs to post the data in to SAP.
Examples for direct input programs are:

RFBIBL00 - FI( Finance)
RMDATIND - MM( Material Management)
RVAFSS00 - SD
RAALTD11 - AM
RKEVEXTO - CO-PA

**************************************************************************************************************************************************

LSMW(Legacy System Migration Workbench)

1) It is a ABAP Workbench tool which is used to transfer data from Non-SAP( Legacy) system to SAP system.

2) Transaction Code : LSMW

3) LSMW works best for Master data, one doesn’t require to use much coding while using LSMW.

4) This method is preferred by Functional SAP Consultants rather than Technical Consultants for data migration.

5) We can Export and Import a LSMW.

Difference between BDC and LSMW->

LSMW is for Functional consultants which does not require much coding, while BDC is designated for technical consultant. 


Project -> Specifies the name of the data transfer project.
           More than one subproject can be assigned to a project.

Subproject-> Specifies the name of the subproject
             A subproject can have an unlimited number of objects.

Object-> An object corresponds to a business object.
         Examples- Material Master, Client Master etc.
         An object is assigned to a subproject.

Example -> Project ->Datamigration
           Subproject->Materials
           Object->Matcreate

           Project ->Datamigration
           Subproject->Materials
           Object->Matchange

           Project ->Datamigration
           Subproject->Client
           Object->Clntcreate 

           Project ->Datamigration
           Subproject->Client
           Object->Clntchange

LSMW Methods : 1) Direct Input
               2) Batch Input Recording
               3) Business Object Method(BAPI)
               4) IDOC(Intermediate Document) 

*************************************************************************************************************************************************************
                                BAPI(Business Application Programming Interface)

1) It is a technique which is used to conduct large scale data migration from legacy system to SAP system.
2) BAPIs in the SAP systems are implemented as a Functional Modules.

 BAPI =  Function Module + Business Object.

3) BAPI is always Preferable as compared to BDC for Data Migration.


Create and Change Material Master Data :  BAPI_MATERIAL_SAVEDATA   



