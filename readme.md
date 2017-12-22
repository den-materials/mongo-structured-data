<!--
Creator: Ilias Tsangaris
Market: SF
-->

![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

<!--WDI5 9:04 -->
<!--9:06 WDI4 -->

# Structured Data in Mongo

<!--Developers recommended that we teach this as a "work in progress"--that is, use embedded data where it makes sense, then use embedded data where it DOESN'T make sense, talk about why, and then introduce referenced data to "fix" it-->

### Why is this important?
<!-- framing the "why" in big-picture/real world examples -->
*This workshop is important because:*

Organizing stored data in a predictable way essential to making it useful and actionable when an application performs searches and queries to derive information for its users.

### What are the objectives?
<!-- specific/measurable goal for students to achieve -->
*After this workshop, developers will be able to:*

* Gain a deeper understanding of Mongo's ability to handle data organization
* Compare and contrast embedded & referenced data
* Design routes for nested resources
* Build the appropriate queries for nested relationships

### Where should we be now?
<!-- call out the skills that are prerequisites -->
*Before this workshop, developers should already be able to:*

* CRUD data in Mongo
* Use Mongoose to write a [Schema](http://mongoosejs.com/docs/guide.html)

## Data Organization in Mongo

There are two ways to form relationships in a document-based database...

#### Embedded Data

* **Embedded Data** is a document directly nested *inside* of other data

> Uniquely identifying information, address information, user-generated content.

In Mongo directly, we treate embedded data as a field that is itself an object. We can use JavaScript notation to define the object directly.

#### Referenced Data

* **Referenced Data** contains an *id* of a document that can be found somewhere else

> Memberships, relationships, shared content

In this scenario, we store the data we want in a new collection, then reference it. For example, if we want our `Account` documents to reference our
`Orders` documents, we need to create two collections - `Accounts` and `Orders`. We create an `order` and then add the `order id` to a field in the `account` document.
If we want to see the `order` information associated to an `account`, we first need to search for our `account` and then once we have the `account`
we can search for the `order` information.



There is generally a tradeoff between *efficiency* (embedded) and *consistency* (referenced) depending on which one you choose.

### Scenario: 

For each situation would you use embedded or referenced data? Discuss with a partner and be prepared to explain why.

<!--WDI4 9:13 turning over to devs -->

* A `User` that has many `Tweets`?
* A `Food` that has many `Ingredients`?

### Implementation with Mongoose

Tip: Noteworthy code lines are denoted with the comment: `NOTE`.

**Referencing Data**

```javascript
var foodSchema = new Schema({
  name: {
    type: String,
    default: ""
  },
  ingredients: [{
    type: Schema.Types.ObjectId,  // NOTE: Referencing
    ref: 'Ingredient'
  }]
});

var ingredientSchema = new Schema({
  title: {
    type: String,
    default: ""
  },
  origin: {
    type: String,
    default: ""
  }
});
```

**Embedding Data**

```javascript
var tweetSchema = new Schema({
  body: {
    type: String,
    default: ""
  }
});

var userSchema = new Schema({
  username: {
    type: String,
    default: ""
  },
  tweets: [tweetSchema]	  // NOTE: Embedding
});
```

## Queries Exercise

<!--This Exercise is a lost cause.  I'd say the instructor should just type this out, with devs at half-mast the whole time. -->

#### Goal

Create and navigate through relational data in MongoDB

#### Setup
* startup mongoDB with `mongod`
* `cd` into the folder `starter-code` in this directory
* `npm install` to bring down all the dependencies
* `node console.js` to view the output of your queries

#### Tips
* save your successful code into your text-editor for each successful step
* `<command>` + `<up>` will bring you to the last thing you entered in the repl 

> Note: All your models will be nested inside an object `db`.

#### Steps

	1) Create a user
	
	2) Create tweets embedded in that user
	
	3) List all the users
	
	4) List all tweets of a specific user
	
	5) Create several ingredients
	
	6) Create a food that references those ingredients
	
	7) List all the Foods
	
	8) List all the ingredients in a Food

<!--WDI5 9:39 -->

## Licensing
All content is licensed under a CC­BY­NC­SA 4.0 license.
All software code is licensed under GNU GPLv3. For commercial use or alternative licensing, please contact legal@ga.co.
