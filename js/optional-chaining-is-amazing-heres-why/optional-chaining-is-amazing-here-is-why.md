**Optional Chaining** is the new javascript operator, which is included as part of EcmaScript 2020. The operator works for objects, arrays, and functions. They don't enable anything in terms of functionality, but they make the code a lot easy to read and write. Let's see how:

I'm sure that we all in our coding experience have faced a common problem, for which we already have a solution.

**The Problem**

```javascript
{
    data: {
        user: {
            fullname: "Soumya Mishra"
            wishlist: ["wId_101", "wId_102"]
        }
    }
}

// Error prone-version, could throw.
const wishlistItem = db.user.wishlist.length;
```

Let's assume that the above object is for loggedIn user details along with users wishlist data. Now, there can be users who have not added anything to their wishlist, so the wishlist property in the object might not be present for those users. But we have to pull the wishlist Ids from this object and make another request to fetch data.

Till date, we choose any 1 from the below ways to handle such scenarios.

**The Solution**

```javascript
const wishlistIds =
    data ?
    (data.user ?
        (data.user.wishlist ?
            data.user.wishlist :
            []) :
        []) :
    [];
const wishlistItemCount = wishlistIds.length;

OR

const wishlistIds = [];
if (data && data.user && data.user.wishlist) {
    wishlistIds = data.user.wishlist;
}
const wishlistItemCount = wishlistIds.length;
```

This is something just for the small object, assume it for more complex object structure. Even if one writes the code correctly, it will not provide any readability.

**The Magic Solution**

Now we will see how we can achieve the above solution in just 1 line.

```javascript
const wishlistItemCount = data?.user?.wishlist?.length;
```

This magic solution has been achieved through **Optional Chaining (?.) Operator**.

Now let's see how this Operator works with different data types in javascript. It only works with **Arrays**, **Objects** & **Functions**.

**Optinal Chaining with Dynamic Properties**

Optional Chaining works well with the dynamic properties with a different syntax. Let us see how:

> The syntax for dynamic properties:
  ?.[ ]

```javascript
const userdata = {
    data : {
        user: {
            name: Ram Kumar,
            socialMediaAccounts: ['twitter', 'linkedIn'],
            primarySocialMedia: 'twitter',
            socialLinks: {
                twitter: 'https://twitter.com/mishraaSoumya',
                linkedIn: 'https://www.linkedin.com/in/mishraa-soumya/'
            }
        }
    }
}

const primarySocialMedia = data?.user?.primarySocialMedia;
// the value of primarySocialMedia can be different or dynamic property.
const socialMediaIUrl = data?.user?.socialLinks?.[primarySocialMedia];
```

Let me explain the above example how it works. So, In an app, a user can have multiple socialMediaAccounts, but there can be only 1 primary account, which can be different and dynamic. So, while pulling the url for primary social media account, a developer has to ensure that the dynamic value is a property in socialLinks object.

The same syntax works with the **arrays** also, where you are not sure if the index will always be part of the array. Check the below example:

```javascript
// If the `usersArray` is `null` or `undefined`,
// then `userName` gracefully evaluates to `undefined`.
const userIndex = 13;
const userName = usersArray?.[userIndex].name;
```

**Optional Chaining with Function Calls**

Optional Chaining operator also works with Function Calls, but with an additional syntax form.

> // Syntax for Function Calls
?.( )

```typescript
interface InputProps = {
    value: string;
    onBlur?: Function;
    onChange: Function;
}

const inputProps: InputProps = {
    value,
    onBlur,
    onChange
}

const onBlurHandler = inputProps?.onBlur?.();
```

So, now you don't have to write multiple checks for your component props before actually calling the function.

**Properties of Optional Chaining**

The optional chaining operator has few properties: *short-circuiting*, *stacking*, and *optional deletion*. Let's go through these properties with an example.

1. **Short-Circuiting**: It means the if LHS of the expression evaluates to null or undefined, then the RHS is not evaluated.

> a?.[++x]

In the above example, x is only incremented, if a is not null/undefined.

2. **Stacking**: It means that more than 1 optional chaining operator can be used on a sequence of property accesses. Also, you can use different forms of the operator in the same sequence.

```javascript
const handler = db?.user?.[13]?.onClick?.();
```

So, you can combine all forms of optional chaining operator in a sequence.

3. **Optional Delete**: It means that the delete operator can be combined with an optional chain.

```javascript
delete db?.user;
```

So, the user in the db object is only deleted if db is not null.

