# What is Typescript

Let's first address what Typescript **isn't**. Typescript is **not** an *entirely* different language from Javascript. It doesn't **replace** Javascript. You may often hear it spoken about as if it's a distinct language in conversation with other developers i.e.: "I know Go lang, Javascript, Typescript, etc..." but don't think that means learning Typescript requires learning something entirely new- Typescript is a **superset** of Javascript, which means it's just Javascript with additional features. Everything you've learned about Javascript is still important and valid, adding Typescript to your skillset just means taking that Javascript knowledge to the *next level*, not replacing it with something else. This also means that if you've put off learning Typescript before- then you should stop worrying. You can start using Typescript immediately and slowly implement more of typescript's features as you learn. 

It's an incremental process just like learning anything else like React, Tailwind, or Next. So don't be intimidated! By the end of this guide you'll have a solid understanding of the basics, a great reference for any of the common issues you'll face, and the knowledge to confidently hop into any Typescript codebase and understand everything that's going on. Let's start that first incremental step with an overview of the basic types- and then we can hop into a project and use them with react!

# Basic Types

Let's make this painless. Hop into the [official typescript playground](https://www.typescriptlang.org/play) and just delete all of the code they provide us.

You'll see a code editor to the left- and as we type we'll see any errors in our code pop up on the right.

Let's add some simple Javascript to the page:
```js
let userName = "Billy";
let userAge = 22;
```
Done. No errors. This is completely valid Typescript! And we haven't even had to set any types! So let's change a value after we've declared it.
```js
let userName = "Billy";
let userAge = 22;
userAge = "old";
```

We'll get an error:
```bash
Type 'string' is not assignable to type 'number'.
```

So what gives? We didn't set a type for anything yet, why does it tell us we can't make a string a number? Because you don't have to directly tell Typescript to assign a type to a variable (explicit), it will also infer the types of everything based on the initial value (implicit).

So we actually implicitly set the types to "string" and "number" just by declaring them. If we **explicitly** type them it might be more obvious what the issue is:
```js
let userName:string = "Billy";
let userAge:number = 22;
userAge = "old";
```
`userAge` is a number, but we assigned it a 'string' value. This is very helpful. This stops us from writing code where we declare a variable as a string or object- and then later try to map over it like an array. Typescript knows and keeps track of our variable types and will yell at us when we do something wrong.

Let's look at some basic types and examples:
```js
let userName:string; // "Hello" or "Brandon"
let userAge:number; // 200 or 12.5 or -49
let isActive:boolean; // true or false

let interests:string[]; // ["Hey","Brandon"]
let favoriteNumbers:number[]; // [200,12.5,-49]

let usuallyBad:any; // anything at all

let linkedInLink:undefined; // undefined
let facebookLink:null; // null
```

Most of pretty obvious- but notice that you can make an `array` out of any of the basic types by just adding `[]` to the end. This tells Typescript that the variable will be an array **of** that type.

You also see 'any' listed as a type. For the most part- if you write this you're doing something wrong. You really want to only do this in special circumstances like when using a third party library that doesn't have types, when creating some dynamic data that might rely on unpredictable user input, or for example in a `try...catch` block as the type of 'error'.

# Multiple Types
You've seen that we assign a type to each variable- either implicitly or explicitly- and that Typescript get's mad if we change it. But sometime we really do want to have a variable hold more than one type of value. What if the `facebookLink` in the above example could also be a string depending upon what we get back from our database or an API?

We can use a 'union type' with the `|` symbol. 
```js
let facebookLink:null | string;
facebookLink = "http://somelink.com";
facebookLink = null;
```
Now `facebookLink` can be either null OR string. And we won't get any errors for changing the type around. 

# Objects
```js
type UserObject = {
    name:string;
    age:number;
    favoriteColor:string;
}

OR

interface UserObject{
	name:string;
	age:number;
	favoriteColor:string;
}
```

Creating an object type is straightforward. The syntax is virtually identical to creating an object. You can then just apply this type to an object you create and typescript will make sure all of those values inside are correctly typed:

```js
let myObject:UserObject = {
    name:"hello",
    age:20,
    favoriteColor:"red"
}
```
If you were to change `age` to a string you'd get a Typescript Error. You would also get a Typescript Error if you added any new keys to the object that weren't defined in the type- or if you didn't include all the keys:
```js
let myObject:UserObject = {
    name:"hello",
    age:20,
    favoriteColor:"red",
    id:2, //error
}
// or
let myObject:UserObject = { // error
    name:"hello",
    favoriteColor:"red",
}
```

# Why Use Typescript?
So far all we've discussed just feels like adding restrictions to your code. So what is the real benefit and why do so many people love using Typescript? **Because** of the restrictions. Restrictions are **good**. When developing by yourself- You restrict yourself from using your variables or methods incorrectly. This means you won't have *as many* confusing bugs that are hard to track down. You'll be able to catch these bugs before you even run the code.

What you're really doing is *describing* your code and how it behaves to the typescript compiler and your code editor. By learning to describe your code accurately- you will not only write safer and less buggy code, but you'll become a **stronger developer**. You'll more clearly understand all code, not just your own. 

The benefits really shine when working in a team. By adding all these types and 'restrictions' to the code you write- you can enforce **how** other people on your team use your code. If you write a function that **explicitly** takes a string as an argument and returns an array- no one on your team will accidentally pass in a number to the function. And they'll know the return type without even looking at your code just by hovering over your function they imported.

You'll get access to powerful autocomplete features not only in your own code, but when using code written by another teammate. You won't need to dig through their code to figure out what's happening- your code editor will just know. For example- after defining this `Post` type, when you create an object with that type then your editor will help you write the rest:

![406b60295a44dba9e3b79a5cc5e7f0f2.png](/406b60295a44dba9e3b79a5cc5e7f0f2.png)

Or after it's already been written or imported- you will get assistance from your editor when keying into the object:

![2dcd552090b31ba0b9fbda5c63db1496.png](/2dcd552090b31ba0b9fbda5c63db1496.png)

As you can see it's a powerful tool not just for you, but for collaboration.

# Project Setup

Let's jump right in and create a new NextJS project. Don't just read- open up a code editor and follow along. Get the muscle memory working!

Run 
`npx create-next-app@latest`
In your terminal. Follow the commands.
![2b84c26d59304a308ee656aeff3d6cac.png](/2b84c26d59304a308ee656aeff3d6cac.png)

You should have new project all spun-up and ready to use Typescript in! 

The only file that should be new to you is the `tsconfig.json` file in the root directory. Let's open it up and take a quick look at what NextJS generated for us.

We should have a config file with "compilerOptions", "include", and "exclude". What do all these options mean? Like I said before, typescript is just a superset of javascript- and it can't actually run in the browser or in node by itself. It actually gets "compiled" into javascript when we start our dev environment or when we build the application. These settings tell the typescript compiler exactly **how** to compile our Javascript. For instance- the `target` option tells the compiler what version and features of Javascript to build. Older versions will support more browsers, and newer versions will support more features like 'async/await' out of the box without the compiler having to create extra code to get it to work.

The [docs](https://www.typescriptlang.org/tsconfig) have a comprehensive list of these options: but for the most part you won't need to change anything in a prebuilt config like this- Next (or whatever other package you use to scaffold your project like Vite, create-react-app), will include all the appropriate libraries and targets for you to get started.


# What we're building
We'll create a quick application that pulls data from 2 public APIs and generates fake user profiles using that data. It won't be fancy- but it will let us explore using typescript with APIs, React props and components, and event handlers. 

## Let's fetch some data

Let's open up our 'homepage' at `app/page.tsx` and delete essentially everything to give us a blank slate to work from. We'll also modify the function to be 'async' so that we can fetch data inside.

```js
export default async function Home() {
  return <main></main>;
}
```

First we can fetch some data inside our `Home()` function from a free and public API. `https://peoplegeneratorapi.live/api/`

```js
  const userResponse = await fetch(
    "https://peoplegeneratorapi.live/api/person/5"
  );
  const users = await userResponse.json();
```
This will give us an array of 5 people to work with, and we can iterate over that data and display it in a map. So our code looks like this:

```js
export default async function Home() {
  const userResponse = await fetch(
    "https://peoplegeneratorapi.live/api/person/5"
  );
  const users = await userResponse.json();
  return (
    <main>
      {users.map((user) => (
        <div key={user.username}>{user.name}</div>
      ))}
    </main>
  );
}
```

This runs and works fine- but you'll notice a typescript error:

![762ab4a94bb6a33e5ba2dcb8944350fa.png](/762ab4a94bb6a33e5ba2dcb8944350fa.png)

This is typescript telling you that it has no idea what type of data 'user' is. And because of that, it can't be sure if `user.username` or `user.name` are what you want or if they even exist. We can fix this by creating a 'User' type. This will make Typescript stop yelling at us, AND make it easier for us to key into data with autocomplete.

Let's go to the top of this file and define a 'User' interface (you'll usually use interface for objects). And inside that interface we need to tell Typescript what kind of keys a User will have, and what **types** those keys are. To figure this out we need to go to our API and look at a response. APIs will often include sample responses to help you figure this out, and sometimes it will be in the documentation for each endpoint. Worst case scenario you can just console log the response back and look at the keys/values.

But luckily this API well documented. If we go to https://peoplegeneratorapi.live/ 

![094c0e93e9ab6f0c1b015d5bbc143f35.png](/094c0e93e9ab6f0c1b015d5bbc143f35.png)

So we can just fill this out.
```js
interface User {
  name: string;
  age: number;
  job: string;
  incomeUSD: number;
  creditScore: number;
  ccNumber: string;
  married: boolean;
  hasChildren: boolean;
  height: number;
  weight: number;
  eyeColor: string;
  email: string;
  gender: string;
  hasDegree: boolean;
  bloodType: string;
  username: string;
  politicalLeaning: number;
  religion: string;
  address: {
    streetAddress: string;
    city: string;
    state: string;
    country: string;
    zip: string;
    geonameId: number;
    phoneNumber: string;
    ipAddress: string;
    countryCode: string;
  };
  doB: string;
  gpa: number;
}

```

We can break the address up if we wanted to. We can make an Address interface aswell and just assign the address key of the User to Address:
```js
interface User {
  ... etc
  address: Address;
  
}
interface Address {
  streetAddress: string;
  city: string;
  state: string;
  country: string;
  zip: string;
  geonameId: number;
  phoneNumber: string;
  ipAddress: string;
  countryCode: string;
}
```

Great. Now we can **explicitly** tell Typescript that the response we get back will be an **array of Users**.
```js
  const userResponse = await fetch(
    "https://peoplegeneratorapi.live/api/person/5"
  );
  const users: User[] = await userResponse.json();
```

Now our Typescript error is gone. AND as an added bonus- we have autocomplete!

![ec75a1914bcc86a9b508c186e9852bd6.png](/ec75a1914bcc86a9b508c186e9852bd6.png)

Before we build out a user card- let's rework it into a component. Let's map around this component we're about to build instead:
```ts
      {users.map((user) => (
        <UserCard key={user.username} name={user.name} email={user.email} />
      ))}
```
We'll pass in props for name and email, and try rendering those.

Make a new folder called `components` and let's add a `UserCard.tsx` file.

```ts
export default function UserCard() {
  return (
    <article>

    </article>
  );
}
```
We want to take in the email and name props- but in typescript we can't just put them in the arguments- we need to specify what type each argument is.
We can do this in a lot of ways. If there are only a couple props, we can just  destructure the arguments and then give a type to the desctructured object like so:
```ts
export default function UserCard({
  name,
  email,
} : {
  name: string;
  email: string;
}) {
  return (
    <article>
      {name} {email}
    </article>
  );
}

```

You'll often see people create a 'Props' interface instead to make it easier to modify and read:
```ts
interface Props {
  name: string;
  email: string;
}
export default function UserCard({ name, email }: Props) {
  return (
    <article>
      {name} {email}
    </article>
  );
}

```

If we wanted to make the email or another field optional we could just add a `?` to the name of the key.

```js
interface Props {
  name: string;
  email?: string;
}
```

But what we really want is to get everything about the User. We could pass in our `user` from the map as a prop- 

![751330d659ab7aafddf2381f8b6fb3ea.png](/751330d659ab7aafddf2381f8b6fb3ea.png)

but then would we have to recreate the type in this file, too?

Not at all. Typescript interfaces and types can be imported and exported just like anything else. We can take our User and Address interfaces from `app/page.tsx` and put them in a different file to import as we need. Let's create a `types` folder in the root and an `index.ts` file inside of it:

```ts
// types/index.ts
export interface User {
 ... etc ...
}
export interface Address {
 ... etc ...
}
```
Notice we 'export' these types. Now we can import `User` at the top of our `app/page.tsx`
```ts
import UserCard from "@/components/UserCard";
import type { User } from "@/types/";

export default async function Home() {
  const userResponse = await fetch(
    "https://peoplegeneratorapi.live/api/person/5"
  );
  const users: User[] = await userResponse.json();
  return (
    <main>
      {users.map((user) => (
        <UserCard key={user.username} user={user} />
      ))}
    </main>
  );
}

```

And import it into `components/UserCard.tsx` as well. Let's flesh out the component a bit and utilize some of the data we're getting. Try it yourself- it's incredibly easy because typescript will help us key into each value even if we don't remember the exact name.

```ts
import type { User } from "@/types/";

export default function UserCard({ user }: { user: User }) {
  return (
    <article className="flex flex-col items-center justify-center w-[35rem] h-full p-4 space-y-4 bg-white rounded-lg shadow-md">
      <section className="flex flex-row items-center justify-around w-full h-1/2 space-y-4">
        <img
          className="w-20 h-full rounded-full"
          src={
            "https://api.dicebear.com/6.x/adventurer-neutral/svg?seed=" +
            user.username
          }
        />

        <section className="flex flex-col items-center justify-center w-1/3 h-full">
          <h2 className="text-xl font-bold text-black">{user.name}</h2>

          <p className="text-sm text-gray-500">{user.email}</p>
        </section>
        <section className="w-1/3">
          <p className="text-sm text-gray-500">{user.address.phoneNumber}</p>
          <p className="text-sm text-gray-500">{user.address.streetAddress}</p>
          <p className="text-sm text-gray-500">{user.address.city}</p>
          <p className="text-sm text-gray-500">{user.address.zip}</p>
        </section>
      </section>
    </article>
  );
}

```

Let's create another component and call it `CardPage.tsx`. Inside of it we'll do our mapping over the user cards and add some basic pagination.

```ts
"use client"

import { User } from "@/types/";
import UserCard from "@/components/UserCard";

export default function CardDisplay({ users }: { users: User[] }) {
	return (
	<article>
 <section className="flex flex-col items-center gap-2">
        {users.map((user) => (
          <UserCard key={user.username} user={user} />
        ))}
      </section>

      {/* page selection section */}
      <section>
        <div className="flex justify-center gap-2 mt-4">

          {[...Array(5)].map((_, i) => (
            <button key={i} className="bg-gray-200 rounded-md px-2 py-1">
              {i + 1}
            </button>
          ))}
        </div>
      </section>
</article>
);
}
```

Then we can replace our `app/page.tsx` contents to render this cardDisplay component. This tiny restructure let's us do datafetching serverside within the page.tsx, and then use hooks and onClicks in our CardDisplay.tsx later:
```ts
import type { User } from "@/types/";
import CardDisplay from "@/components/CardDisplay";
export default async function Home() {
  const userResponse = await fetch(
    "https://peoplegeneratorapi.live/api/person/5"
  );
  const users: User[] = await userResponse.json();
  return (
    <main className="text-black">
      <CardDisplay users={users} />
    </main>
  );
}
```

This is what it looks like now:

![d2f258f04cd6c49444ccee3e5507c741.png](/d2f258f04cd6c49444ccee3e5507c741.png)


## Hooks and Events

Continuing to work on `CardDisplay.tsx` now, let's add some states and get the pagination working! Import `useState` and `useEffect` at the top. And inside the `CardDisplay` function let's create some states:

```ts
  const [page, setPage] = useState(0);
  const [slicedUsers, setSlicedUsers] = useState<User[]>([]);
```
The first state, `page`, is just like a state we'd create with regular Javascript. The second one, `slicedUsers` is a little different and leverages Typescript's 'generics'. In typescript- you can create functions and interfaces that are 'generic'. That means they accept and utilize different types.

This is useful if we want to *describe* something and make it typesafe- but we'll be reusing it for multiple types. For example you may have API responses that always return some **type** of data in a nested array- but the rest of the response is always the same. You could build out a generic interface to handle all the responses:

```ts
interface APIResponse<T>{ // the T is the generic 'type'
	responseCode:number;
	date:string;
	referrer:string;
	data:T[];
}
```
You can then pass in different 'types' as `T` and Typescript would know that the `APIResponse` contains a responsecode, a date, a referrer, and an array of whatever type `T` that you passed in was.

```ts
const responseForUsers:APIResponse<User> = await fetchUsers();
const responseForPosts:APIResponse<Post> = await fetchPosts();
... etc ...
```


In our case with our state, `useState` is a generic function. We can pass a type in `useState<T>`, and then typescript and our editor will know that our `slicedUsers` is an array of Users, and our `setSlicedUsers` should set an array of Users. 

Why didn't we have to do that with the other state called `page`? Just like with all types- you can be **explicit** or **implicit**. Because we passed a `0` in to that state, it was **implicitly** set as a `number` type. But because we just passed an empty array to our initial state for `slicedUsers`, we had to **explicitly** tell typescript that this is *actually* supposed to be an array of type `User`, we just don't quite have the exact data yet.

Generics are a pretty large topic, but a very powerful tool to understand. You should check the docs out and try to learn how to use them... but it's a little beyond the scope of a crash course like this.

Let's keep building out the pagination. We'll create a `useEffect` under our states that sets the value of our `slicedUsers` to sets of 5 based on the page we're on.
```ts
  useEffect(() => {
    setSlicedUsers(users.slice(page * 5, page * 5 + 5));
  }, [page, users]);
```

This will run whenever we get our `users` array from the props, and whenever the user clicks a button to change the `page`. This is client-side pagination. We'll change our main `page.tsx` to fetch all the pages at once, and then we'll control how many are shown with client-side logic.

Let's update our buttons in the pagination section. We want to add an onClick handler, and I'm going to add a 'data' attribute to the button that we can read in the handler. I like to do this to avoid creating anyonymous functions inside of a map.

```ts
          {[...Array(5)].map((_, i) => (
            <button
              key={i}
              className="bg-gray-200 rounded-md px-2 py-1"
              data-page={i}
              onClick={pageClick}
            >
              {i + 1}
            </button>
          ))}
```

We can change our className to change the background color if this button is the current 'page' as well:
```ts
              className={`${
                page === i ? "bg-gray-200" : "bg-slate-800"
              } rounded-md px-2 py-1`}
```

Now we'll make the pageClick function.
```ts
  const pageClick = (e: React.MouseEvent<HTMLButtonElement>) => {
    const page = e.currentTarget.dataset.page;
    if (page) setPage(parseInt(page));
  };
```

Event Handlers can be tricky with typescript and React. But because you have a basic understanding of how Generics work- it should make sense. We have a `MouseEvent` generic type that we can pass in more specific types to. In this case, we're clicking a button, so we use the `HTMLButtonElement`. If we wanted to accurately get the event from other elements on a mouse click, we could pass in their respective type. 

```ts
<div> -> HTMLDivElement
<a> -> HTMLAnchorElement
<body> -> HTMLBodyElement
... etc ...
```
If we want to make this handler work for multiple types of elements, there's always `HTMLElement` which should mean 'any HTMLElement'.

## Ahh that's still confusing 
It might seem complicated at first- but you just need to break it up into 2 parts:
 - What kind of event is it?
 - What element is it being triggered on?
So if we wanted the type for the `onChange` event triggered in an `<input>` tag we'd use:
`React.ChangeEvent<HTMLInputElement>`
If we wanted the `onChange` for a `<select>` tag, we'd use:
`React.ChangeEvent<HTMLSelectElement>`
If we wanted the `onKeyDown` for an `<input>` tag, we'd use:
`React.KeyboardEvent<HTMLInputElement>`

You'll get used to the event handler names pretty quick- and you'll stop using `e:any` and cheating ;)

## Progress
 

https://github.com/brandonetter/TS-Intro/assets/4108484/6c94a89a-d0f4-46c1-9fcb-56794949eed0



So far we've made a silly little app in typescript and you've learned how to use Typescript with useState, Event handlers, API response data, and Functional Component Props.

## Creating functions with Typescript and Generics

Let's get a little more advanced. I've created a mock API here

https://64dc6aade64a8525a0f6740e.mockapi.io/api/v1/

It has two endpoints: `/store` and `/car`
You can check out the responses in the browser to see the structure of each response. Just like before- you can turn those into types or interfaces. I've gone ahead and done that here- but expanded on the concepts a bit:

```ts
interface BaseDB {
  id: number;
  createdAt: Date;
}
interface StoreItem extends BaseDB {
  tag: "store";
  name: string;
  price: number;
  description: string;
}
interface VehicleItem extends BaseDB {
  tag: "car";
  model: string;
  color: string;
  make: string;
  type: VehicleType;
}
export type VehicleType =
  | "Sedan"
  | "SUV"
  | "Coupe"
  | "Convertible"
  | "Hatchback";
```

Here I've used the 'extends' keyword. If you're familiar with classes, this immediately makes sense. If not- then don't worry. It's a simple concept. `StoreItem` *extends* `BaseDB`, which means `StoreItem` has all the types inside of `BaseDB` PLUS everything we've outlined inside of `StoreItem` itself. I did this because our responses have overlap. Both of our endpoints have a 'createdAt' and 'id' column. So instead of writing it twice- you can just 'extend' another interface.

You'll see we have a `VehicleType` which is a 'union type' that can only be "Sedan", "Suv", "Coupe", "Convertible", or "Hatchback". If we know the available options ahead of time- it can be useful and nice for autocomplete to fill these types of union types out. It can prevent you from inserting invalid data- or searching for values that don't exist. 

You'll also see a `tag` key in each Item type. This will let us create a 'tagged union'. The 'tag' is a harcoded value that you can use inside your functions when dealing with these types. This should be used sparingly- but can be useful.

Here's how we can use this 'tagged union' and 'tag' key in a function:
```ts
// Create the tagged union
export type Item = StoreItem | VehicleItem;

export async function getItemById<T extends Item>(
  endpoint: T["tag"],
  id: number
): Promise<T> {
  const baseUrl = "https://64dc6aade64a8525a0f6740e.mockapi.io/api/v1/";
  const url = `${baseUrl}${endpoint}/${id}`;
  const response = await fetch(url);
  const item = await response.json();
  return item;
}

```
This creates a 'Generic' function that we can use for both the `StoreItem` and `VehicleItem` type. 
This gives us autocomplete for the endpoint:

![224d24d6c8b71e88a8dc057e1a99ab64.png](/224d24d6c8b71e88a8dc057e1a99ab64.png)

And if we properly type the Generic, typescript can give us autocomplete for the return value, too:

![7b10e19ada6db31d3282e53c562b8866.png](/7b10e19ada6db31d3282e53c562b8866.png)


That's an interesting feature- but we could also do it a better way with overloads instead of 'tags':

```ts
async function getItem( endpoint:"store",id:number): Promise<StoreItem>;
async function getItem( endpoint:"car",id:number): Promise<VehicleItem>;

async function getItem(endpoint: any,id:number) {
  const baseUrl = "https://64dc6aade64a8525a0f6740e.mockapi.io/api/v1/";
  const url = `${baseUrl}${endpoint}/${id}`;
  const response = await fetch(url);
  const item = await response.json();
  return item;
}
```
Overloads let us describe different ways a function can take shape. The first way we described was with an 'endpoint' argument of `store` and a return value of `Promise<StoreItem>`.
The second was was with an endpoint of `car` and a return value of `Promise<VehicleItem>`.

Then we write the actual function. Now whenever that function is used, Typescript will know based on the 'endpoint' argument, what type of return type to expect.

Overloading functions is a feature of vanilla Javascript- but becomes even more powerful with typescript.

Now we don't even need to be explicit with the Generic type when we call the function- but we still get all the benefits:

![9f58f8f0c91b73e9e2a6954f88bcc749.png](/9f58f8f0c91b73e9e2a6954f88bcc749.png)


## In progress:
... To be contiued- create a single function to query multiple types with different argument options using overloads. Use a nextAPI route to use this function based on request search params-> display results on page. ETA: ~1 day
