# mongodb-cheatsheet
mongodb-cheatsheet, copyright to Brad Traversy from Traversy Media (YouTube)

//First Initalize, run it as a service mongod --directoryperdb --dbpath
C:\mongodb\data\db --logpath C:\mongodb\log\mongo.log --logappend
--install

net start MongoDB

//Run in the shell mongo

//Show list of DB show dbs

//Switch and Create DB use mycustomers

//Show current db db

//Create User db.createUser({ user:"brad", pwd:"1234", roles:
["readWrite", "dbAdmin"] });

//Create Collections (similar to Tables in RDBMS)
db.createCollection('customers');

//See all collections show collections

//Insert a document into that collection
db.customers.insert({first\_name:"John", last\_name:"Doe"});

//See documents in a collection db.customers.find();

//In a prettier way db.customers.find().pretty();

//Insert multiple documents. You can add fields on the fly.
db.customers.insert([{first\_name:"Steven", last\_name:"Smith"},
{first\_name:"Joan", last\_name:"Johnson", gender:"female"}]);

//To add gender in John Doe a.k.a UPDATE. First param is criteria, next
parameter is what we want to REPLACE WITH (DESTROYS OLD DATA)
db.customers.update({first\_name: "John"},{first\_name: "John",
last\_name: "Doe", gender:"male"});

//Using SET operator to only set certain fields. Keep other fields the
same db.customers.update({first\_name: "Steven"},{\$set:
{gender:"male"}});

//Using INC to increment numeric values. This will increment age fields
by 5 db.customers.update({first\_name: "Steven"},{\$inc:{age:5}});

//Using UNSET to remove a field
db.customers.update({first\_name:"Steven"},{\$unset:{age:1}});

//If this is not found, insert it. Use UPSERT
db.customers.update({first\_name:"Mary"}, {first\_name: "Mary",
last\_name:"Samson"}, {upsert: true});

//Renaming Fields, using RENAME
db.customers.update({first\_name:"Steven"}, {\$rename:
{"gender":"sex"}});

//Remove documents. It will delete with first\_name Steven.
db.customers.remove({first\_name: "Steven"});

//Use justOne to delete first document found
db.customers.remove({first\_name: "Steven"},{justOne: true});

//Add multiple documents example db.customers.insert([ { first\_name :
"Troy", last\_name : "Makons", gender : "male", age : 33, address : {
street : "432 Essex st", city : "Lawrence", state : "MA" }, memberships
: ["mem1", "mem2"], balance : 125.32 }, { first\_name : "Beth",
last\_name : "Jenkins", gender : "female", age : 23, address : { street
: "411 Blue st", city : "Boston", state : "MA" }, memberships : ["mem2",
"mem3"], balance : 505.33 }, { first\_name : "Sharon", last\_name :
"Thompson", gender : "female", age : 35, address : { street : "19 Willis
st", city : "Worchester", state : "MA" }, memberships : ["mem1",
"mem2"], balance : 99.99 }, { first\_name : "William", last\_name :
"Jackson", gender : "male", age : 43, address : { street : "11 Albany
st", city : "Boston", state : "MA" }, memberships : ["mem1"], balance :
333.23 }, { first\_name : "Timothy", last\_name : "Wilkins", gender :
"male", age : 53, address : { street : "22 School st", city :
"Amesbury", state : "MA" }, memberships : ["mem3", "mem4"], balance :
22.25 }]);

//Find with parameters db.customers.find({first\_name:"Sharon"});

//Find Sharon and Troy db.customers.find({\$or:[{first\_name:"Sharon"},
{first\_name:"Troy"}]});

//Greater Than, Less Than Operators. $gt, $lt db.customers.find({age:
{\$lt: 40}});

//Find in the object. Use double quotes
db.customers.find({"address.city": "Boston"});

//Find in the array db.customers.find({memberships: "mem1"});

//Sorting in find. Minus for DESC. db.customers.find().sort({last\_name:
1}); db.customers.find().sort({last\_name: -1});

//Count documents db.customers.find().count();

//Limit the findings db.customers.find().limit(4);

//Limit and sort db.customers.find().limit(4).sort({last\_name: 1});

//Iterate through stuff using foreach
db.customers.find().forEach(function(doc) { print("Customer Name: " +
doc.first\_name) });




















