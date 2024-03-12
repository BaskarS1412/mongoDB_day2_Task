# MongoDB Task

## Design database for Zen class programme

-          users
-          codekata
-          attendance
-          topics
-          tasks
-          company_drives
-          mentors


1. Find all the topics and tasks which are thought in the month of October.
    ### Query: `db.topics.find({'date':{$gte:ISODate('2020-10-01'),$lt:ISODate('2020-10-31')}});` 
    ### `zenclass> db.tasks.find({'date':{$gte:ISODate('2020-10-01'),$lt:ISODate('2020-10-31')}});`
    
     
2. Find all the company drives which appeared between 15 oct-2020 and 31-oct-2020.
     ### Query: `zenclass> db.company_drives.find({'date':{$gte:ISODate('2020-10-15'),$lt:ISODate('2020-10-31')}});`
3. Find all the company drives and students who are appeared for the placement.
     ### Query: `zenclass> db.company_drives.find({},{'_id':0,'company_name':1,'student_id':1});`
4. Find the number of problems solved by the user in codekata.
     ### Query: `zenclass> db.users.aggregate({$project:{'_id':0,'user_name':1,'no_of_prob_solved':{$size:'$codekata_solved'}}});`
5. Find all the mentors with who has the mentee's count more than 15.
     ### Query: `zenclass> db.mentors.find({$where:'this.student_id.length > 15'},{'_id':0,'menror_name':1});`
6. Find the number of users who are absent and task is not submitted  between 15 oct-2020 and 31-oct-2020.
     ### Query: `zenclass> db.attendance.aggregate({$match:{'date':{$gte:ISODate('2020-10-15'),$lt:ISODate('2020-10-31')}}},{$project:{_id:0,date:1,no_of_absent:{$size:'$absent'}}});`.
     ### `zenclass> db.tasks.aggregate({$match:{'date':{$gte:ISODate('2020-10-15'),$lt:ISODate('2020-10-31')}}},{$project:{_id:0,name:1,date:1,no_of_not_submitted:{$size:'$not_submitted'}}});`.