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
```

Let's assume that the above object is for loggedIn user details along with users wishlist data. Now, there can be users who have not added anything to their wishlist, so the wishlist property in the object might be not present. But we have to capture the wishlist Ids and make another request to fetch data.

Till date, we choose any 1 from the below ways to handle such scenarios.

**The Solution**

```javascript

```
