

# MyNote_Mongoose

https://mongoosejs.com/docs/index.html

https://mongoosejs.com/docs/api.html

```js
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:xxxxx');

const db = mongoose.connection;

db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
    
    var kittySchema = new mongoose.Schema({
        name: String
    });

    kittySchema.methods.speak = function () {
        var greeting = this.name
            ? "Meow name is " + this.name
            : "I don't have a name";
        console.log(greeting);
    }
    /*
        kittySchema.methods('speak', function () {
        var greeting = this.name
            ? "Meow name is " + this.name
            : "I don't have a name";
        console.log(greeting);
        });
    */

    var Kitten = mongoose.model('Kitten', kittySchema);

    var silence = new Kitten({ name: 'Silence' });
    console.log(silence.name); // 'Silence'

    var fluffy = new Kitten({ name: 'fluffy' });
    fluffy.speak(); // "Meow name is fluffy"

    fluffy.save(function (err, fluffy) {
        if (err) return console.error(err);
        fluffy.speak();
    });

    Kitten.find(function (err, kittens) {
        if (err) return console.error(err);
        console.log(kittens);
    })
    
});


```

```js
Mongoose.prototype.connect()
// https://mongoosejs.com/docs/api.html#mongoose_Mongoose-connect
```

drop database

```js
db.dropDatabase();
```

Save

```js
<Model>.save((err, <model>) => {
    
});

<Model>.save()
	.then(<model> => {
    	return <model>; // it will pass to next .then()
	})
	.then(<model> => {
    	
	})
	.catch(err => {
    	
	});

// save() not block to flow, it mean syn
```

Print all

```js
function printAll(){
    <Model.prototype>.find(<Query>).sort(/* ... */)
    	.then( <model> => {
        
    	})
    	.catch(err => {
        	
    	})
}
```

Promise

```js
Promise.all(<Promise>, ...)
	.then()
	.catch(err => {});
```

CRUD

```js
async function insertXXX(XXXobj){
    let xxx = new XXX(XXXobj);
    try{
   		let doc = await xxx.save();
        if(!doc) return ;
    }
    catch(err){
        console.log(err);
    }
}

async function getXXXbyYYY(yyy){
    let result;
    await XXX.findOne( <Query> )
    	.then(<Function>)
        .catch(<Function>);
    return result;
}

async function printAllXXX(){
    await XXX.find().sort( <Query> )
    	.then( docs => docs.forEach(doc => doc.print()) )
        .catch(<Function>);
}

async function updateXXX(XXX){
    let result;
    await XXX.findOneAndUpdate( <Query> ) // return original to then
    	.then(<Function>)
        .catch(<Function>);
    return result;
}

async function deleteXXX(XXX){
    let result;
    await XXX.findOneAndRemove( <Query> )
    	.then(<Function>)
        .catch(<Function>);
    return result;
}
```













