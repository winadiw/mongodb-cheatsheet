# mongodb-cheatsheet
mongodb-cheatsheet, copyright to Brad Traversy from Traversy Media (YouTube)

//First Initalize, run it as a service  
mongod --directoryperdb --dbpath C:\mongodb\data\db --logpath C:\mongodb\log\mongo.log --logappend --install  

net start MongoDB  
  
//Run in the shell  
mongo  
  
//Show list of DB  
show dbs  
  
//Switch and Create DB  
use mycustomers  
  
//Show current db  
db  
  
//Create User  
db.createUser({  
	user:"brad",  
	pwd:"1234",  
	roles: ["readWrite", "dbAdmin"]  
});  
  
//Create Collections (similar to Tables in RDBMS)  
db.createCollection('customers');  
  
//See all collections  
show collections  
  
//Insert a document into that collection  
db.customers.insert({first_name:"John", last_name:"Doe"});  
  
//See documents in a collection  
db.customers.find();  
  
//In a prettier way  
db.customers.find().pretty();  
  
//Insert multiple documents. You can add fields on the fly.  
db.customers.insert([{first_name:"Steven", last_name:"Smith"}, {first_name:"Joan", last_name:"Johnson", gender:"female"}]);  
  
//To add gender in John Doe a.k.a UPDATE. First param is criteria, next parameter is what we want to REPLACE WITH (DESTROYS OLD DATA)  
db.customers.update({first_name: "John"},{first_name: "John", last_name: "Doe", gender:"male"});  
  
//Using SET operator to only set certain fields. Keep other fields the same  
db.customers.update({first_name: "Steven"},{$set: {gender:"male"}});  
  
//Using INC to increment numeric values. This will increment age fields by 5  
db.customers.update({first_name: "Steven"},{$inc:{age:5}});  
  
//Using UNSET to remove a field  
db.customers.update({first_name:"Steven"},{$unset:{age:1}});  
  
//If this is not found, insert it. Use UPSERT  
db.customers.update({first_name:"Mary"}, {first_name: "Mary", last_name:"Samson"}, {upsert: true});  
  
//Renaming Fields, using RENAME  
db.customers.update({first_name:"Steven"}, {$rename: {"gender":"sex"}});  
  
//Remove documents. It will delete with first_name Steven.  
db.customers.remove({first_name: "Steven"});  
  
//Use justOne to delete first document found  
db.customers.remove({first_name: "Steven"},{justOne: true});  
  
//Add multiple documents example  
db.customers.insert([  
	{  
		first_name : "Troy",  
		last_name : "Makons",  
		gender : "male",  
		age : 33,  
		address : {  
			street : "432 Essex st",  
			city : "Lawrence",  
			state : "MA"  
		},  
		memberships : ["mem1", "mem2"],  
		balance : 125.32  
	},  
	{  
		first_name : "Beth",  
		last_name : "Jenkins",  
		gender : "female",  
		age : 23,  
		address : {  
			street : "411 Blue st",  
			city : "Boston",  
			state : "MA"  
		},  
		memberships : ["mem2", "mem3"],  
		balance : 505.33  
	},  
	{  
		first_name : "Sharon",  
		last_name : "Thompson",  
		gender : "female",  
		age : 35,  
		address : {  
			street : "19 Willis st",  
			city : "Worchester",  
			state : "MA"  
		},  
		memberships : ["mem1", "mem2"],  
		balance : 99.99  
	},  
	{  
		first_name : "William",  
		last_name : "Jackson",  
		gender : "male",  
		age : 43,  
		address : {  
			street : "11 Albany st",  
			city : "Boston",  
			state : "MA"  
		},  
		memberships : ["mem1"],  
		balance : 333.23  
	},  
	{  
		first_name : "Timothy",  
		last_name : "Wilkins",  
		gender : "male",  
		age : 53,  
		address : {  
			street : "22 School st",  
			city : "Amesbury",  
			state : "MA"  
		},  
		memberships : ["mem3", "mem4"],  
		balance : 22.25  
	}]);  

  
//Find with parameters  
db.customers.find({first_name:"Sharon"});  
  
//Find Sharon and Troy  
db.customers.find({$or:[{first_name:"Sharon"}, {first_name:"Troy"}]});  
  
//Greater Than, Less Than Operators. $gt, $lt  
db.customers.find({age: {$lt: 40}});  
  
//Find in the object. Use double quotes  
db.customers.find({"address.city": "Boston"});  
  
//Find in the array  
db.customers.find({memberships: "mem1"});  
  
//Sorting in find. Minus for DESC.  
db.customers.find().sort({last_name: 1});  
db.customers.find().sort({last_name: -1});  
  
//Count documents  
db.customers.find().count();  

//Limit the findings  
db.customers.find().limit(4);  

//Limit and sort  
db.customers.find().limit(4).sort({last_name: 1});  

//Iterate through stuff using foreach  
db.customers.find().forEach(function(doc) {  
	print("Customer Name: " + doc.first_name)  
});  











































