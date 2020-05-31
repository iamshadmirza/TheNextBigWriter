Nullish Coalescing Operator( **??** ) is one of the features of **ES2020**. It gives the ability to truly check the **nullish** values. It is another logical operator other than OR ( || ) , AND ( && ) and NOT ( ! ) operators.

####**How it works?**

The operator returns its **Right Hand Side (RHS)** operand when its **Left Hand Side (LHS)** operand is **null** or **undefined**, otherwise it will return the LHS operand.

Let's see how it works through some examples:

![Nullish-Coalescing-Operator-Ex-1](https://res.cloudinary.com/dyyr6kwla/image/upload/v1590838686/nullish-coalescing/nullish-example-1_xaqjn0.png)

In the above example, the component Search has a prop [[searchBoxPlaceholder]].
As the prop is an optional one, so the component uses a default value when the prop is undefined. This is a best use-case of Nullish Coalescing operator because the developer doesn't wants to restrict component to always have a placeholder for the search input box. So using this an empty string can also be passed for the prop and the component will not use the default value for placeholder and would instead do not show a placeholder string, which can not be accomplished using the logical OR operator.

Below are few other examples, which will give idea about more of it's use-cases.

![Few-Other-Examples](https://res.cloudinary.com/dyyr6kwla/image/upload/v1590839423/nullish-coalescing/few-other-examples_ohz48e.png)

####**Comparison with other similar operators**

The operator is simiar to logical **OR** operator and **Default Assignment** opertaor. If you would have noticed in the first example, then we are just assigning a default value to the prop [[searchBoxPlaceholder]], which can also be done in following way:

![Compare-With-Default-Assignment](https://res.cloudinary.com/dyyr6kwla/image/upload/v1590841955/nullish-coalescing/comp_compare-with-default-assignment_nhpvqn.png)

The above example will no doubt work, but only if the value of prop [[searchBoxPlaceholder]] is undefined. But if the value for prop is [[null]], then the default assignment will not work.

Also, the logical operator **OR** works in similar manner, but it works for all the falsy values. Let us see with the below example what difference comes in the evaluation for the same condition with OR operator.

![Compare-With-OR-Operator](https://res.cloudinary.com/dyyr6kwla/image/upload/v1590842888/nullish-coalescing/compare-with-OR-operator_wsmnua.png)

Now, in the above example, the OR operator serves the purpose of assigning default value, in case the prop is any of the falsy values. But what if the user of the component doesn't wants to set any value for the placeholder. The OR operator will not allow to do this, as the empty string ( '' ) is a falsy value. So, now if we use **Nullish Coalescing Operator ( ?? )**. We can solve this problem and prop can accept empty string and will not show a placeholder value.

#### **Summary**

* The nullish coalesing operator ( ?? ) is used to assign a default value, against the nullish values (null && undefined).

* The operator has a very low prcedence in the [MDN Table](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#Table). It has higher precedence than Logical AND ( && ) and Logical OR ( || ).

* The operator cannot be chained with && and || operators without using any explicit parentheses.

#### **Support**

* Check [Can I Use](https://caniuse.com/#search=nullish%20coalescing) for the browser support.

* Node JS support start from 14+ version.

----

That's all for the article. Thanks for reading it. Please comment your feedback and suggestions.

[Twitter](https://twitter.com/mishraaSoumya) | [LinkedIn](https://www.linkedin.com/in/mishraa-soumya/)