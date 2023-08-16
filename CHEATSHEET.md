# Cheat Sheet
### This cheatsheet is organized not by typescript concept- but by programming concept, making it easy to find what you need without knowing what it's called in Typescript. ie Sections are broken into "Objects","Arrays", and "Functions"
### Extended examples are included- but often they are more explicit than needed. Your code will often be much more simple.


# Objects

## Static object with specific fields
```ts
interface User {
    id: number;
    name: string;
    email: string;
}
```
## Optional fields in an object
```ts
interface OptionalUser {
    id?: number;      // Optional field
    name: string;
    email?: string;   // Optional field
}
```

## Readonly properties in an object
```ts
interface ImmutableUser {
    readonly id: number;
    readonly name: string;
    readonly email: string;
}
```

## Dynamic object with any key/value pair
```ts
interface AnyOb{
	[key:string]:any;
}
```

## Dynamic object with any key/value pair + required fields
```ts
interface AnyOb{
    id:number;
    [key:string]:any;
}
```

## Functions in Object
```ts
interface Utils {
    add: (a:number,b:number)=>number;
    onClick: (e:React.MouseEvent<HTMLElement>)=>void;
}
```

## Combining Objects
```ts
interface User{
    id:number;
    name:string;
}

interface Options{
    theme: "dark" | "light";
    autoSave:boolean;
}

type UserWithOptions = User & Options;
```

## Combining Objects with Extends
```ts
interface User{
    id:number;
    name:string;
}

interface UserWithOptions extends User{
    theme: "dark" | "light";
    autoSave:boolean;
}
```

## Nested Objects
```ts
interface Profile {
    user: {
        id: number;
        name: string;
    };
    address: {
        street: string;
        city: string;
        zip: string;
    };
}
// OR

interface User{
	id:number;
	name:string;
}
interface Address{
	street:string;
	city:string;
	zip:string;
}
interface Profile{
	user:User;
	address:Address;
}
```


## Generics with Objects (API Example)
```ts
interface APIResponse<T> {
    [key:string]:any;
    data: T;
}
interface User{
    id:number;
    name:string;
    email:string;
}
interface Post{
    id:number;
    title:string;
    content:string;
}

let userAPIResult: APIResponse<User> = { //Generic with User
    success:true,
    timestamp:"1997-02-08-18:23:11",
	responseCode:"200",
    data: { // data must be of type User
        id: 1,
        name: "John",
        email: "john@example.com"
    }
};
let postAPIResult: APIResponse<Post> = { // Generic with Post
    success:true,
    timestamp:"1997-02-08-18:23:11",
    data: { // data must be of type Post
        id: 1,
        title: "Welcome to my blog",
        content: "No one really reads these ..."
    }
};

let getAllPostsAPIResult: APIResponse<Post[]> = { // Generic with Post Array
    success:true,
    timestamp:"1997-02-08-18:23:11",
    data: [ // Data must be array of Post
    {
        id: 1,
        title: "Welcome to my blog",
        content: "No one really reads these ..."
    },
    {
        id: 2,
        title: "Thanks for reading, Mom",
        content: "I appreciate all the support ..."
    },
    
    ]
};
```

## Omit keys from Object
```ts
interface UserModelType{
    id:number;
    name:string;
    email:string;
    password:string;
}

type PublicUser = Omit<UserModelType,"password">;

let apiResponseGetUsersForClient:PublicUser[] = [
    {
        id:0,
        name:"Chloe",
        email:"chloefrfr@email.com"
    },
    {
        id:1,
        name:"Alice",
        email:"ally22@email.com"
    },
    {
        id:2,
        name:"Antonio",
        email:"antonio_1990@email.com"
    },
    
]

// OR , omit multiple:
type PublicUser = Omit<UserModelType,"password" | "email">;

let apiResponseGetUsersForClient:PublicUser[] = [
    {
        id:0,
        name:"Chloe",
    },
    ...
    
```

## Omit keys from an Object using another Object
```ts
type UserModel={
    id:number,
    name:string;
    role:string;
    interests:string[];
    age:number;
    numberOfComments:number;
    password:string; // we want to remove these
    location:string; // we want to remove these
    email:string; // we want to remove these
}
type PrivateKeys = {
    password:string;
    location:string;
    email:string;
}

type PublicUserModel = Omit<UserModel, keyof PrivateKeys>;
let ob:PublicUserModel = {
    id:0,
    name:"Jacob",
    role:"admin",
    interests:["fishing","catching fish"],
    age:33,
    numberOfComments:42
}
```

## Pick Keys from Object
```ts
interface Todo {
    title: string;
    description: string;
    completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;
```

## Make all keys in Object Optional
```ts
interface Todo {
    title: string;
    description: string;
    completed: boolean;
}
type PartialTodo = Partial<Todo>;

let partialTodo:PartialTodo = {
    title:"Finish this object"
}

```

## Make all keys in Object Required
```ts
interface TodoWithOptionalCompleted {
    title: string;
    description: string;
    completed?: boolean;
}
type MandatoryTodo = Required<TodoWithOptionalCompleted>

let mandatory:MandatoryTodo = { // Error, this type needs "completed"
    title:"Finish this object",
    description:"Mostly typing"
}
```


# Arrays

## Array of specific type
```ts
type NumberArray = number[];
type StringArray = string[];
```
## Array with multiple specific types (a tuple)
```ts
type TupleArray = [number, string];
```
## Array with any type
```ts
type AnyArray = any[];
```

## Array with multiple types in any position (Union)
```ts
type UnionArray = (number | string)[];
const unionArray: UnionArray = ["hey","now", 3];
const otherUnionArray:UnionArray = [2,2,3,5,"Breakfast"]
```
## Array with some required types + any type
```ts
type SpecificArray = [number, ...any[]];
OR
type SpecificArray = [number,string, ...any[]];

```

## Array of Objects
```ts
interface User{
    id:number;
    name:string;
}

type UserArray = User[];
const myUserArray:UserArray = [
    {
        id:0,
        name:"bill"
    },
	...
]

OR

const myUserArray:User[] = [
    {
        id:0,
        name:"bill"
    },
	...
]
```

# Functions

## Argument Types
```ts
function multiply(num1:number,num2:number){
    return num1 * num2;
}
```

## Return Types
```ts
function multiply(num1:number,num2:number) : number{
    return num1 * num2;
}
```

## Arguments of multiple types (Union)
```ts
function getLength(arg: string | any[]){
    return arg.length;
}
// works because strings and arrays both have a 'length' 
```

## Optional Arguments
```ts
function printName(firstName: string, lastName?: string) {
    console.log(`${firstName} ${lastName}`);
}
```

## Overloads 
```ts
// define the signatures we want here
function merge(a: string, b: string): string;
function merge(a: number, b: number): number;

// create the actual function
function merge(a:any, b:any) {
    return a + b;
}
// Now calling 'merge' will only accept 2 strings
// or 2 numbers as the arguments.
```

## Generics, functions with generic arguments
```ts
function getLength<T>(someArg:T){
    return someArg;
}
// T can be any type.


function getLength<T>(someArg:T,somearg2:T){
    return [someArg,somearg2];
}
// T can be any type, but both arguments must be the same
// type.

```

## Generics, specifying return type
```ts
function getLength<T>(someArg:T)  : T {
    return someArg;
}
// this function must return the same type that it takes in
// as an argument


function getLength<T>(someArg:T)  : T[] {
    return new Array(someArg);
}
// This function must return an Array of the type it was given
// as an argument.
```

## Multiple generic types in a function
```ts

function getLength<T,U>(someArg:T,somearg2:U){
    return [someArg,somearg2];
}
```

## Specific types of a Generic
```ts
function getLength<T extends string>(someArg:T)  : T[] {
    return new Array(someArg);
}
// function must accept a string and return an array of strings
```

## Multiple specific types of a Generic
```ts
function getLength<T extends string | number>(someArg:T)  : T[] {
    return new Array(someArg);
}
// Can be either a string or a number. And return either a string or a number.

```
## Generics with Custom Types
```ts
interface Post{
    id:number;
    author:string;
    content:string;
    category:"Blog"|"Article";
    createdAt:string;
}
interface Comment{
    id:number;
    author:string;
    content:string;
    postId:number;
    likes:number;
    createdAt:string;

}
// Accepts an array of Comments
// Or an array of Posts
// and returns the newest one
function getNewest<T extends Post | Comment>(arrayOfItems: T[]) {
    if (!arrayOfItems.length) return null;

    const sorted = arrayOfItems.sort((a, b) => 
        new Date(b.createdAt).getTime() - new Date(a.createdAt).getTime()
    );

    return sorted[0];
}
```

```ts
interface Circle{
    x:number;
    y:number;
    radius:number;
}
interface Rect{
    x:number;
    y:number;
    width:number;
    length:number;
}


function setShapeToOrigin<T extends Circle | Rect>(circleOrRect:T): T {
    circleOrRect.x=0;
    circleOrRect.y=0;
    return circleOrRect;
}
```

```ts
function fetchData<T>(endpoint: string): Promise<T> {
    return fetch(endpoint).then(response => response.json());
}

const users = fetchData<User[]>("/api/users");
const products = fetchData<Product[]>("/api/products");
```
## Tagging (Tagged Unions)
```ts
//adding explicit mandatory values lets you 'tag' types
//or just enforce a mandatory value for other reasons
interface Circle{
    type:"circle", // tag
    x:number;
    y:number;
    radius:number;
}
interface Rect{
    type:"rect", //tag
    x:number;
    y:number;
    length:number;
    width:number;
}
interface LineSegment{
    type:"line", //tag
    x:number;
    y:number;
    x2:number;
    y2:number;
}
type Shapes = Circle | Rect | LineSegment; //Tagged union


function moveShape(shape:Shapes){
    switch(shape.type){
        // can determine which type we have with the 'type' tag.
    }
}
```




## Keyof with Generics
```ts
interface Ob{
    name:string;
    id:number;
}
let obArray:Ob[] = [
    {
        id:1,
        name:"Bob"
    },
    {
        id:2,
        name:"Sarah"
    },
    {
        id:3,
        name:"Abed"
    },
    
]

function getAllValuesOfKey<T>(array:T[],key: keyof T){
    for(let i=0;i<array.length;i++){
        console.log(array[i][key]);
    }
}
// second argument MUST be a key of the type that obArray is.
getAllValuesOfKey(obArray,"name")

```

## Keyof with Generics and tags (database example)
```ts
interface IPost{
    type:"post"; // tagging the type
    id:number;
    name:string;
    likes:number;
    commentCount:number;
    createdAt:string;
    updatedAt:string;
}
interface IUser{
    type:"user"; // tagging the type
    id:number;
    name:string;
    email:string;
    createdAt:string;
    updatedAt:string;
}
function sortModelBy<T extends IPost | IUser>(model: T, key: keyof T) {
    switch (model.type){ //checking the tag
        case  "post":
        return PostModel.query({sortBy:key});
        case "user":
        return UserModel.query({sortBy:key});
    }
```

# React Event Handlers
```ts
function handleClick(event: React.MouseEvent<HTMLButtonElement>) {
  console.log(`Clicked at coordinates: (${event.clientX}, ${event.clientY})`);
}
<button onClick={handleClick}>Click me!</button>
```

```ts
function handleClick(event: React.MouseEvent<HTMLAnchorElement>) {
  console.log(`Clicked at coordinates: (${event.clientX}, ${event.clientY})`);
}
 <a onClick={handleClick}>Click me!</a>
```

```ts
// onClick
function handleClick(event: React.MouseEvent<HTMLBodyElement>) {
function handleClick(event: React.MouseEvent<HTMLDivElement>) {
function handleClick(event: React.MouseEvent<HTMLLIElement>) {
// onChange
function handleClick(event: React.ChangeEvent<HTMLInputElement>) {
function handleClick(event: React.ChangeEvent<HTMLSelectElement>) {
// onKeyDown , onKeyUp, etc..
function handleClick(event: React.KeyboardEvent<HTMLInputElement>) {

```
## Multiple Event Types
```ts
function handleClick(event: React.MouseEvent<HTMLLIElement | HTMLButtonElement>)
					  
OR

function handleClick(event: React.MouseEvent<HTMLElement>) 

<li onClick={handleClick}>Click me!</li>
<button onClick={handleClick}>Click me!</button>
```

## Form Event Types
```ts
const submitForm = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();  // Stops the form from submitting the standard way
    // handle submission logic
}
```

## Focus Event
```ts
const handleFocus = (event: React.FocusEvent<HTMLElement>) => {
```

## Asserting types in Event Handlers
```ts
 function handleClick(event: React.MouseEvent<HTMLElement>) {
    document.body.appendChild(event.target as Node);
  }
```

```ts
// Handling outside clicks
const myRef = useRef<HTMLDivElement>(null);

const handleClickOutside = (event: React.MouseEvent<HTMLElement>) => {
    if (myRef.current && !myRef.current.contains(event.target as Node)) {
        console.log("Clicked outside!");
    }
}

<div ref={myRef} onClick={handleClickOutside}>...</div>
```

```ts
// Asserting to access dom methods
function handleClick(event: React.MouseEvent<HTMLElement>) {
    (event.target as HTMLElement).innerHTML = "hey";
}
```

# API Fetching strong typing #1
```ts
/*
Hypothetical API response returns our results in a 'data' key
but also includes other relevant info i.e.
{
    responsecode:200,
    date:"1998-02-03:19:12:11",
    data:[]
}

This is overdone, but shows a lot of concepts
*/
// generic APIResponse can have a `data` key of any type[]
  interface APIResponse<T> {
    responsecode:number,
    date:string,
    data: T[];
  }
  interface User {
    id: number;
    name: string;
    email: string;
  }
  interface Post {
    id: number;
    title: string;
    comments: Comment[];
  }
  interface Comment {
    id: number;
    title: string;
    likes: number;
  }
  type Endpoint = "/user/" | "/post/";

  function getResponse<T>(endpoint: Endpoint): Promise<APIResponse<T>> {
    switch (endpoint) {
      case "/post/":
        return fetch(endpoint).then((data) => data.json());
      case "/user/":
        return fetch(endpoint).then((data) => data.json());
    }
  }

  const responseWithPosts = await getResponse<Post>("/post/");
  const responseWithUsers = await getResponse<User>("/user/");

// Benefits: Your environment will have complete knowledge of
// the return type. Autocomplete for the 'getResponse' argument
// will work.
```
## API Fetching strong typing #2
```ts
/*
Same Interfaces as before, minus the 'Endpoint' type
*/
type EndpointToType = {
    "/user/": User;
    "/post/": Post;
};

function getResponse<K extends keyof EndpointToType>(endpoint: K): Promise<APIResponse<EndpointToType[K]>> {
  return fetch(endpoint).then(data => data.json());
}
const responseWithPosts = await getResponse("/post/");
const responseWithUsers = await getResponse("/user/");
```
![a4b5cb16a8a17478fba5ea6ff9930ad0](https://github.com/brandonetter/TS-Intro/assets/4108484/095f27e3-95cd-415b-8a25-88f109ec83ba)

![578b2bfce1b668e2a1fa95a840a90ee3](https://github.com/brandonetter/TS-Intro/assets/4108484/c1b0c6c9-c8aa-4389-882d-e16aa7ca855f)


## API fetching strong typing #3 with Overloads
```ts
function getResponse(endpoint: "/user/"): Promise<APIResponse<User>>;
function getResponse(endpoint: "/post/"): Promise<APIResponse<Post>>;

function getResponse(endpoint: "/user/" | "/post/") {
    return fetch(endpoint).then((data) => data.json());
}

const responseWithPosts = await getResponse("/post/");
const responseWithUsers = await getResponse("/user/");
// Benefits: Clean to read, allows different docs for each option
```

