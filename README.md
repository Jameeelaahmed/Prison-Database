# Prison-Database
It’s used to simulate the prison database.
It has all the data about each prisoner as medical state , Crime state , social state etc…

Create table prisoner (
Prisoner_ID int not null primary key,
Prisoner_Fname varchar(30) ,
Prisoner_Lname varchar(30) ,
Prisoner_birthdate date ,
prisoner_governorate varchar(30) ,
prisoner_Countery varchar(30)
);
Create table prisoner_address
(
prisoner_address_ID int primary key,
Prisoner_ID int references prisoner (Prisoner_ID),
)

Create table prisoner_phonenumber
(
prisoner_phonenumber_ID int primary key,
Prisoner_ID int references prisoner (Prisoner_ID),
)

create table visitor 
(
visitor_ID int primary key,
visitor_Fname varchar(30),
visitor_Lname varchar(30),
visitor_gender varchar(10),
visitor_birthdate date,
visitor_governorate varchar(30),
visitor_country varchar(30),
)
Create table visitor_address
(
visitor_address_ID int primary key,
visitor_ID int references visitor(visitor_ID),
)

Create table visitor_phonenumber
(
prisoner_phonenumber_ID int primary key,
visitor_ID int references visitor(visitor_ID),
)

create table prisoner_visitor (
PrisonerVisitor_ID int primary key,
visitor_ID int references visitor(visitor_ID),
Prisoner_ID int references prisoner (Prisoner_ID),
start_Time int ,
end_Time int,
visit_date date,
)
create table Financial_state(
Financial_ID int primary key,
Class varchar(30),
Financial_StartDate date,
Financial_EndDate date,
Prisoner_ID int foreign key references prisoner (Prisoner_ID),
)
create table MoneySource
(
Money_source_ID int primary key,
Financial_ID int foreign key references  Financial_state(Financial_ID),
)
create table Crime_State
(
Crime_state int Primary key,
Date_of_charge date,
Duration_of_charge int,
crime_StartDate date,
crime_EndDate date,
Prisoner_ID int foreign key references prisoner (Prisoner_ID),
)
create table judged_casses
(
judged_casses_ID int primary key,
Crime_state int foreign key references Crime_State(Crime_State)
)
create table Accussed_Casses
(
accussed_casses_ID int primary key,
Crime_state int foreign key references Crime_State(Crime_State)
)
create table Case_Describtion
(
Case_Describtion_ID int primary key,
Crime_state int foreign key references Crime_State(Crime_State)
)
create table Situation_in_prison
(
SIN_ID int primary key,
Arrive_Date date ,
Exit_Date date,
Type_of_Imprisonment varchar(10),
Exit_Date_in_case_he_is_arole_model varchar(100),
Reciever_name varchar(30),
Prisoner_ID int foreign key references prisoner (Prisoner_ID),
)
create table Crime_Type
(
Crime_Type_ID int primary key,
SIN_ID int foreign key references Situation_in_prison (SIN_ID),
)
create table Crime_Description
(
Crime_Description_ID int primary key,
SIN_ID int foreign key references Situation_in_prison (SIN_ID),
)
create table Job_Type
(
Job_Type_ID int primary key,
SIN_ID int foreign key references Situation_in_prison (SIN_ID),
)

create table Political_State
(
Political_State_ID int primary key,
Political_Prisoner varchar(10),
Member_of_a_Secret_Organization  varchar(10),
State_Security_File varchar(10),
Political_Start_Date date,
Political_End_Date date,
)
create table political_prisoner
(
Political_prisoner_ID int Primary key,
Political_State_ID int foreign key references Political_State(Political_State_ID),
Prisoner_ID int foreign key references prisoner (Prisoner_ID),
)

create table job_career
(
job_career_ID int primary key,
job_type varchar(50),
job_position varchar(50),
job_address varchar(50),
job_StartDate date,
job_EndDate date,
)
create table job_prisoner
(
job_prisoner_ID int primary key,
job_career_ID int foreign key references job_career(job_career_ID),
Prisoner_ID int foreign key references prisoner (Prisoner_ID),
)
 create table Medical_health
 (
 Medical_ID int primary key,
 Medical_State varchar(10) ,
 Medical_StartDate Date,
 Medical_EndDate Date,
 )
 Create table Medical_prisoner 
 (
 Medical_prisoner_ID int primary key,
 Medical_ID int foreign key references Medical_health(Medical_ID),
 Prisoner_ID int foreign key references prisoner (Prisoner_ID),
 )
 
 create table Education
 (
 Education_ID int primary key,
 continue_to_Study varchar(10),
 Educ_StartDate date,
 Educ_EndDate date,
 )
 create table Education_Prisoner
 (
 Education_prisoner_ID int primary key,
 Prisoner_ID int foreign key references prisoner (Prisoner_ID),
 Education_ID int foreign key references Education(Education_ID),
 )
 create table Qualification
 (
 Qualification_ID int primary key ,
  Education_ID int foreign key references Education(Education_ID),
 )
  create table social_state
  (
  Social_state_ID int primary key,
  Marital_status varchar(30),
  Responsaple_for_a_family varchar(10),
  Reputation varchar(100),
  Social_StartDate date,
  Social_EndDate date,
  Prisoner_ID int foreign key references prisoner (Prisoner_ID),
  )
  create table Behavior
  (
   Behavior int primary key,
   Social_state_ID int foreign key references social_state(Social_state_ID),
  )

  select count(prisoner_ID) as num_of_prisoners from prisoner
  @@@select COUNT(Prisoner_ID) ,Type_of_Imprisonment,Job_Type_ID from prisoner as p inner join Situation_in_prison as s on p.Prisoner_ID=s.
  @@select PRI.Prisoner_ID, S.*,M.*,F.*,P.* from prisoner as PRI inner join Medical_prisoner as M on PRI.Prisoner_ID=M.Prisoner_ID 
 @@, prisoner inner join social_state as S on prisoner.Prisoner_ID=S.Prisoner_ID ,prisoner inner join political_prisoner as Po on prisoner.Prisoner_ID= 
  @@Financial_state as F,Political_State as P, social_state as S
  select prisoner.Prisoner_ID from prisoner inner join Situation_in_prison on prisoner.Prisoner_ID= Situation_in_prison.Prisoner_ID 
  where Arrive_Date between '2012' and '2020'
